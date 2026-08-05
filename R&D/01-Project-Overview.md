# AlistraGIS R&D Project Overview

## Purpose of this record

This note records the technical purpose, scope and development context of AlistraGIS. It is intended to support the engineering knowledge base and the preparation of a UK R&D tax relief claim. It is not, by itself, a conclusion that every activity or cost qualifies.

## Product summary

AlistraGIS is an enterprise geospatial platform designed for the planning, construction, operation, auditing and handover of fibre-optic networks. The platform combines an interactive GIS map with operational workflows that would otherwise be spread across mapping tools, spreadsheets, photographs, forms, messaging and separate project-management systems.

The system has been developed using React, TypeScript and Vite, with Leaflet/react-leaflet for mapping and Firebase services for authentication, database storage and file storage. Deployments have been made through Vercel. The architecture is now being moved towards a modular, API-first platform.

## Business problem

Fibre delivery teams need to manage large numbers of interconnected physical assets, including poles, chambers, ducts, cables, joints, distribution points, homes, cabinets, exchanges and splice relationships. The data must remain geographically accurate while also supporting construction progress, quality assurance, permits, PIA evidence, production returns, handover records and access controls.

General-purpose mapping and workflow products do not directly model all of these relationships or the field processes required by AlistraGIS. The development therefore includes custom data models, map behaviour, fibre continuity logic, validation rules and operational modules.

## Main technical objectives

1. Render and edit large fibre-network datasets without unacceptable map slowdown or browser instability.
2. Keep map assets synchronised for multiple users while controlling Firestore reads, writes and conflicts.
3. Represent fibre connectivity, feeder relationships, splitter paths, splices and end-to-end continuity as a usable network topology.
4. Import and normalise industry geospatial formats, including GeoJSON, KML, KMZ and GPKG, into the internal asset model.
5. Separate client organisations, projects, areas, users and permissions without accidental data leakage.
6. Expose platform capabilities through secure, versioned APIs without breaking the existing application.
7. Provide a practical field experience on tablets and mobile devices while preserving complex desktop GIS functions.
8. Maintain traceable audit, evidence and change records suitable for regulated operational environments.
9. Explore future automated network design and engineering assistance through the FRIDAY AI concept.

## Major platform areas

- Alistra Map API and interactive GIS viewport
- Projects and organisation boundaries
- Fibre assets and lifecycle operations
- Production and daily returns
- Mission Control project workspace
- Audits and QA/walk-off workflows
- Health and Safety documentation
- PIA and permit management
- BOQ and stock comparison
- Reports and handover
- User, role and session management
- Fibre topology and continuity
- File and evidence storage
- Openreach-related imports, overlays and checks
- Future AI-assisted network design

## Current development state

AlistraGIS remains in active development and is approaching broader testing. Earlier development used test data and focused on establishing the core map, asset editing, permissions and operational workflows. Current work includes modularisation, API architecture, performance, security, data ownership, mobile/tablet usability and enterprise readiness.

AlistraGIS Ltd was incorporated in late July 2026. Work performed before incorporation must be separated from expenditure incurred by the company. The development history remains useful evidence of the technical journey, but qualifying cost treatment requires accounting review.

## R&D documentation principle

For each candidate R&D project, this vault should record:

- the baseline technology available at the time;
- the technological advance sought;
- the uncertainty that could not readily be resolved;
- the experiments, prototypes and failed approaches;
- the work performed by competent professionals;
- when the uncertainty was resolved or development ceased;
- the evidence and expenditure linked to the work.
