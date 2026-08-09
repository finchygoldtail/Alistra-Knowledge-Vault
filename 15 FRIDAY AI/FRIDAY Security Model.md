---
status: live
updated: 2026-08-08
related: ["[[API Security Assessment 2026-08-08]]", "[[Permissions Model]]", "[[Decision Log]]"]
---

# FRIDAY Security Model

Stage 10 of the commercial go-live programme. Reviewed the live `fridayChat` implementation (`functions/src/friday/fridayCallables.ts`, `fridayProductionTool.ts`, `nvidiaClient.ts`, `fridayConfig.ts`) against every scenario the programme asks for. This is a code-level review, not live adversarial testing against the actual NVIDIA model — deliberately, since `isPaidAiAllowed()` defaults to `false` and there is no paid code path in this feature at all; actually invoking the live model to test prompt-injection resistance would mean either enabling paid AI (not done without explicit sign-off) or burning the free-tier allowance, and in any case the finding below is that FRIDAY's safety doesn't depend on the model behaving — it's enforced structurally, so behavioral testing against the model wouldn't add much.

## The core property: FRIDAY cannot reach data it isn't allowed to see, regardless of what it's asked

FRIDAY has exactly **one** tool, `getProjectProduction`, and its OpenAI-compatible tool schema declares `parameters: { type: "object", properties: {}, additionalProperties: false }` — the model is not offered any parameter to fill in (no `businessId`, `projectId`, or anything else). More importantly, the server doesn't just rely on the model respecting that empty schema: when a tool call comes back, `fridayCallables.ts` calls `getProjectProduction({ firestore, context })` using the **function-scoped `context` variable** — the same server-resolved `StorageContext` from `resolveStorageContext(request, firestore)` that every other Cloud Function in the codebase uses, derived entirely from the caller's own verified Firebase Auth token and Firestore membership doc. Whatever JSON arguments the model actually emitted in its tool-call response are never read or used. So even a fully "jailbroken" model that emits `{"companyId": "some-other-company"}` as its tool arguments gets ignored — the data returned is always scoped to the real caller, because the code path to fetch it never had a way to be pointed anywhere else.

This means the specific tests the programme asks for come out as follows:

| Test | Result |
|---|---|
| Asking FRIDAY for another customer's project | **Cannot succeed** — the only data-fetching tool is hard-scoped server-side to the caller's own company, with no parameter surface for the model to redirect it |
| Asking for admin-only records | **No privilege escalation possible** — `getProjectProduction` reads map assets via the same `loadAssets` path any business member can already read directly (membership-only, not role-gated); FRIDAY exposes nothing a regular "user"-role member couldn't already see themselves |
| Prompting FRIDAY to "ignore permission rules" | **Structurally moot** — there's nothing to ignore; the tool has no permission parameter to bypass in the first place. The system prompt also explicitly instructs "never bypass user permissions" and "never reveal secrets, credentials, tokens or system configuration," but that's a second line of defence, not the actual control |
| Tool-call manipulation | Covered above — server ignores model-supplied arguments entirely for the one tool that exists |
| Prompt injection | No retrieval/RAG in this v1 (no external documents or search results are fed into context), so there's no untrusted-content injection surface yet. The user's own chat message is the only injectable input, and since FRIDAY cannot write anything and cannot fetch cross-tenant data regardless of what it's told, the worst realistic outcome of a successful "jailbreak" is an off-brand or unhelpful reply, not a data or write exposure |
| Retrieval leakage | N/A for this version — revisit this row when/if a retrieval or document-search tool is added |
| Sensitive logging | Checked `nvidiaClient.ts` and `fridayCallables.ts` directly — no `console.log` of message content, replies, or the API key anywhere; `writeStorageAuditEvent` logs only `eventType` (`friday.chat.requested`/`.completed`/`.failed`) and a `safeErrorCode`, never the chat content itself |
| Dangerous write actions | FRIDAY has **zero** write capability — one read-only tool, full stop. The system prompt also explicitly states this ("you have no write capability, and must never claim to have performed a write action") |

## Other controls already in place (cost/abuse, not permissions, but worth recording here)

- **Hard zero-cost guard**: `isPaidAiAllowed()` is checked first, before any DB or network call, and defaults to `false` with no paid code path anywhere in the feature — a deliberate fail-safe against accidental cost exposure, not just a config default.
- **Per-user rate limiting**: enforced via a Firestore transaction against `businesses/{companyId}/fridayRateLimits/{uid}` inside the callable (Admin SDK, not client-writable — this collection was one of the five gaps closed in [[Decision Log]]'s Stage 4 entry, previously writable directly by any business member via the client SDK, which would have let a user reset their own rate limit).
- **No retry on failure**: `runFridayCompletion` deliberately has no retry logic, so a failed or quota-exhausted call surfaces immediately rather than silently burning through the free-tier allowance via automatic retries.
- **Request/response caps**: message length capped (`maxMessageChars`), response tokens capped (`maxResponseTokens`), request timeout enforced (`requestTimeoutMs`), at most one tool-driven follow-up call per invocation (2 NVIDIA calls max per user message).

## Conclusion

FRIDAY's permission model is sound by construction, not by policy — the safety property doesn't rely on the model refusing bad requests, it relies on the model never being given a way to make one. No fixes were needed for this stage. The one dependency worth naming: this entire analysis assumes `resolveStorageContext` itself is trustworthy, which is the same shared assumption every other function in [[API Security Assessment 2026-08-08]] rests on.
