# System Architecture Overview - Woppa MVP

High-level system architecture for the Woppa MVP, a mobile app and web platform connecting consumers with businesses through 2x1 promotions and simple discounts in Brazil.

## High-Level System Components

### Consumer Mobile App
- **Role**: Primary consumer interface for promotion discovery and redemption
- **Technology**: React Native with TypeScript
- **Responsibilities**:
  - Geolocation-based promotion browsing (map and list views)
  - Category filtering and search functionality
  - User registration and authentication (email/password + Google OAuth, no phone required)
  - Promotion detail viewing with static maps and "Get Directions" functionality
  - Payment processing integration with Mercado Pago Checkout Pro
  - Alphanumeric redemption code display and management
  - User profile and purchase history management

### Business Web Panel
- **Role**: Business-facing interface for promotion management
- **Technology**: React with TypeScript and shadcn/ui
- **Responsibilities**:
  - Business registration with manual validation workflow
  - Promotion creation and management (1+1 type promotions)
  - Sales tracking and redemption analytics
  - Publication management with status monitoring
  - Manual coupon redemption confirmation

### Admin/Moderation Web Panel
- **Role**: Woppa staff interface for content and business moderation
- **Technology**: React with TypeScript (potentially shared codebase)
- **Responsibilities**:
  - Business validation and approval/rejection workflows
  - Promotion moderation with 12-hour SLA
  - Coupon operations management
  - Operational metrics dashboard
  - System monitoring and oversight

### Core API Backend
- **Role**: Centralized business logic and data management
- **Technology**: Node.js with TypeScript, PostgreSQL with Prisma ORM
- **Responsibilities**:
  - RESTful API serving all frontend applications
  - Business logic for promotions, users, and redemptions
  - Authentication and authorization management
  - Database operations and data integrity
  - Integration with external services (Google APIs, AWS, Mercado Pago)
  - Webhook handling for payment confirmations
  - Redemption code generation and validation

### Authentication System
- **Role**: User identity and access management
- **Technology**: Google OAuth 2.0 integration
- **Responsibilities**:
  - Consumer and business authentication (email/password + Google OAuth)
  - Session management and token validation
  - Profile data synchronization with Google accounts
  - Role-based access control (consumer, business, admin)
  - Simplified registration without phone number requirement

### File Storage System
- **Role**: Image management and delivery
- **Technology**: AWS S3 + CloudFront CDN
- **Responsibilities**:
  - Promotion image upload and storage
  - Image optimization and quality validation
  - Content delivery via CDN from São Paulo region
  - Secure file access control

### Geolocation System
- **Role**: Maps and location-based functionality
- **Technology**: Google Maps API + Google Places API
- **Responsibilities**:
  - Static map rendering for mobile app with "Get Directions" links
  - Business address validation and geocoding
  - Proximity-based promotion filtering
  - Address autocomplete for business registration

### Payment Processing Service
- **Role**: Handle payment transactions for promotion redemptions
- **Technology**: Mercado Pago Checkout Pro
- **Responsibilities**:
  - Process online payments via Mercado Pago Checkout Pro
  - Handle webhook notifications for payment confirmation
  - Payment validation and confirmation
  - Transaction status tracking and redemption code generation

## Component Interaction Model

### Data Flow Architecture

The system follows a **centralized API architecture** where all business logic flows through the Core API Backend:

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Consumer      │    │   Business      │    │   Admin/        │
│   Mobile App    │    │   Web Panel     │    │   Moderation    │
│                 │    │                 │    │   Web Panel     │
└─────────┬───────┘    └─────────┬───────┘    └─────────┬───────┘
          │                      │                      │
          └──────────────────────┼──────────────────────┘
                                 │
                    ┌─────────────▼──────────────┐
                    │     Core API Backend       │
                    │   (Node.js + TypeScript)   │
                    └─────────────┬──────────────┘
                                  │
    ┌─────────────┬─────────────────┼─────────────────┬─────────────┐
    │             │                 │                 │             │
┌───▼───┐  ┌──────▼──────┐  ┌──────▼──────┐  ┌──────▼──────┐  ┌────▼────┐
│ Auth  │  │ File Storage│  │ Geolocation │  │ Database    │  │ Payment │
│System │  │  (AWS S3)   │  │  (Google)   │  │(PostgreSQL)│  │(MercadoPago)│
└───────┘  └─────────────┘  └─────────────┘  └─────────────┘  └─────────┘
```

## Key Architectural Considerations

### MVP Constraints and Shortcuts

**Monolithic Approach**: Single Node.js backend instead of microservices to accelerate development and reduce operational complexity during validation phase.

**Manual Operations**: 
- Business registration requires manual validation by Woppa staff
- Promotion moderation requires human approval (12-hour SLA)
- Single-use coupon redemption with alphanumeric codes (no QR codes)
- Manual coupon validation by businesses through web panel
- No automated fraud detection or real-time inventory management

**Limited Scope**:
- Focus on 2x1 promotions and simple discounts
- Brazil-only launch with LGPD compliance and AWS São Paulo region
- Manual business onboarding and validation process
- Mercado Pago as the sole payment method (no cash networks in MVP)
- Static maps instead of dynamic interactive maps

### Shared Services and Dependencies

**Centralized Authentication**: Single identity system serves consumers, merchants, and staff with role-based permissions through the web panel.

**Unified Data Model**: PostgreSQL database with relational design supporting users, merchants, promotions, and redemptions across all interfaces.

**External Service Dependencies**:
- Google OAuth for simplified user registration (no phone number required)
- Google Maps/Places APIs for static maps and address validation
- AWS infrastructure (São Paulo region) for file storage and CDN delivery
- Mercado Pago Checkout Pro for payment processing with webhook notifications

### Assumptions and Trade-offs

**Technology Trade-offs**:
- React Native chosen for faster cross-platform development over native performance
- PostgreSQL with Prisma provides type safety but requires relational data modeling
- Manual validation workflow limits scalability but ensures quality control

**Business Model Assumptions**:
- 2x1 promotions and simple discounts (no complex discount structures)
- Geographic proximity drives user engagement
- Payment required before redemption code delivery
- Single payment method (Mercado Pago) for MVP validation
- Single-use coupons with quantity-based purchases (one presentation = full redemption)
- Staff-curated content quality over automated scale

**Scalability Considerations**:
- Database and API designed to handle expected MVP load
- File storage and CDN support growth in image content
- Authentication system can scale with user base
- Manual processes identified for future automation

### Future Evolution Paths

The architecture supports gradual enhancement without major rewrites:
- Additional payment methods (cash networks) can be integrated in future phases
- QR code redemption can replace alphanumeric codes
- Dynamic interactive maps can replace static maps
- AI-based validation can replace manual approval workflow  
- Push notifications and advanced features can be integrated
- Phone number registration can be added for enhanced verification
- Additional categories and complex promotion types can extend existing data models
- Caching layer (Redis or similar) can be added if scale demands it
- Microservices migration possible if scale demands it

---
*Document updated: 2025-01-30*