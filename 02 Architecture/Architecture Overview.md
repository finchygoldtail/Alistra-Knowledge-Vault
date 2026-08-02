---
title: Architecture Overview
type: architecture
status: draft
owner: Alistair
created: 2026-08-02
updated: 2026-08-02
tags: [architecture, api-first]
---

# Architecture Overview

AlistraGIS uses a React, TypeScript and Vite frontend with Leaflet and react-leaflet for mapping. Firebase provides Authentication, Firestore and Storage. Vercel hosts the frontend deployment.

The platform is API-first. Core domains are captured in [[API Catalogue]], with modules for [[Projects API]], [[Assets API]], [[Audits API]], [[Production API]], [[Topology API]], [[Openreach API]], and [[Files API]].

## Key Architecture Notes

- [[API Gateway]]
- [[Authentication]]
- [[Permissions Model]]
- [[Data Storage Strategy]]
- [[Multi-Tenant Architecture]]
- [[Deployment Architecture]]

