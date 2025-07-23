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

### Source of Truth
- `source-specs/requirements.docx.md`: **Primary requirements document** (183K tokens) - this is the authoritative source for all technical and functional requirements
- `source-specs/discovery-presentación-final.md`: Discovery phase findings (historical context, some details superseded by requirements.docx.md)
- `source-specs/*.png`: Wireframes for key user flows (current UI reference)

### Repository Structure
- One markdown file per epic containing:
  - Epic description and objectives
  - User stories with acceptance criteria
  - Hour-based estimates
  - Uncertainty analysis
  - JSON metadata where needed

## Requirements Analysis Guidelines

### Reading the Large Requirements Document
The `requirements.docx.md` file is 183K tokens. Use these strategies:
- Use `offset` and `limit` parameters for section reading
- Use `Grep` tool to search for specific patterns like "Épica", "Requerimiento", "Wireframe"
- Search for section headers and numbered requirements

### Epic Identification Approach
1. **Analyze functional scope** from requirements document
2. **Map to wireframes** to understand user journeys  
3. **Define epics based on business value** and user workflows
4. **Break down into implementable user stories**

## Estimation Framework

### Estimation Unit
- **Hours** for all estimates
- Include development, testing, and integration time
- Consider both frontend and backend work

### Uncertainty Analysis Factors
Assess uncertainty level (Low/Medium/High) based on:

**Technical Clarity**
- Completeness of functional requirements
- API specifications detail level
- Integration requirements clarity
- Performance requirements specificity

**Design Completeness** 
- Wireframe coverage and detail
- UI/UX specifications completeness
- Missing design states or flows
- Responsive design requirements

**External Dependencies**
- Third-party service integrations (Google OAuth, maps, etc.)
- LGPD compliance requirements
- Geolocation service dependencies
- Image storage and optimization needs

**Implementation Complexity**
- Technical architecture decisions needed
- Cross-platform considerations (iOS/Android)
- Real-time features (geolocation, filtering)
- Manual validation workflow complexity

### Uncertainty Levels
- **Low (10-20% variance)**: Clear requirements, complete wireframes, standard implementation
- **Medium (30-50% variance)**: Some ambiguity in requirements or design, moderate complexity
- **High (50-100% variance)**: Significant unknowns, complex integrations, unclear requirements

## Epic Structure Template

Each epic file should contain:

```markdown
# Epic: [Epic Name]

## Overview
- **Objective**: Business goal and user value
- **Scope**: What's included/excluded
- **Wireframes**: Reference to relevant wireframes

## User Stories

### Story 1: [Story Title]
**As a** [user type]
**I want** [functionality]
**So that** [business value]

**Acceptance Criteria:**
- [ ] Criterion 1
- [ ] Criterion 2

**Estimate:** X hours
**Uncertainty:** Low/Medium/High (reason)

## Epic Totals
- **Total Estimate**: X hours
- **Uncertainty Range**: X-Y hours
- **Risk Factors**: Key concerns
```

## Key Business Constraints to Consider

When defining epics and stories, remember these MVP constraints:
- **Manual redemption** (no POS integration)
- **LGPD compliance** required
- **Low-tech friendly** for businesses
- **Mobile-first** with data optimization
- **Geolocation with fallback** to São Paulo
- **Category focus**: Gastronomy (pink #E573E2) and Pharmacy (green #3AD4AC)

## Out of Scope (Don't Estimate)
- Digital payments integration
- Automated POS redemption
- Push notifications/mass email
- Advanced dashboards/reporting
- Referral programs/gamification
- AI content analysis