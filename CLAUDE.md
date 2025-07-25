# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Purpose

This repository is for **requirements analysis, epic definition, and work estimation** for the Woppa MVP project. The main objective is to transform the technical requirements into actionable epics with user stories, acceptance criteria, and hour-based estimates including uncertainty analysis.

## Project Context

**Woppa** is a mobile app and web platform MVP connecting consumers with businesses through 2x1 promotions and simple discounts in Brazil. The project focuses on business model validation rather than scalability.

### Current Phase
- Requirements gathering and analysis
- Epic definition and story breakdown  
- Work estimation with uncertainty assessment

## Key Documentation

### Initial Requirements & Wireframes
**All initial project requirements and wireframes are contained in the `source-specs/` directory:**
- `source-specs/requirements.docx.md`: Complete initial requirements document
- `source-specs/discovery-presentación-final.md`: Discovery phase findings and research
- `source-specs/woppa-wireframe-*.png`: All wireframes for user flows and UI reference
- `source-specs/woppa-wireframe-comerciante-*.png`: Business/merchant wireframes

### Source of Truth Hierarchy
- `business-decisions.md`: **Ultimate source of truth** - supersedes all other documents for any conflicts in business logic and functional requirements
- `source-specs/requirements.docx.md`: **Secondary requirements document** - use for details not covered in business-decisions.md
- `source-specs/discovery-presentación-final.md`: Discovery phase findings (historical context, some details superseded by requirements.docx.md)
- `source-specs/*.png`: Wireframes for key user flows (current UI reference)

### Epic Definitions
**All defined epics and their screens are contained in the `epics/` directory:**
- `epics/mobile-epics.md`: Epic definitions for the mobile application
- `epics/web-panel-epics.md`: Epic definitions for the web panel
- **Always check these files when you have questions about epics and their contained screens**

### Technical Documentation
- `technical/tech-stack.md`: Technology choices and pending decisions for Woppa MVP
- `technical/infrastructure.md`: Cloud infrastructure, storage, containerization, and CI/CD pipeline documentation
- `technical/system-architecture-overview.md`: High-level system components, interactions, and architectural decisions for the MVP

## Additional Guidelines
- All documents you generate must be written in English
- All your plans must be written in English
- **Always check business-decisions.md first** and prioritize it over any conflicting information in other documents
- Always refer to the initial requirements in the `source-specs/` directory when defining any plan I request
- Always take the requirements from the `source-specs/` documents and wireframes. If there's any doubt, business-decisions.md is the source of truth, followed by `source-specs/requirements.docx.md`.

## Estimation Guidelines
- For time estimation, whenever you provide a total, group by team so it's easy to see how much development work will take, which is what we will charge for in this stage.
