# System Architecture Overview - Woppa MVP

High-level system architecture for the Woppa MVP, a mobile app and web platform connecting consumers with businesses through 2x1 promotions and simple discounts in Brazil.

## High-Level System Components

### Consumer Mobile App
- **Role**: Primary consumer interface for promotion discovery and redemption
- **Technology**: React Native
- **Responsibilities**:
  - Geolocation-based promotion browsing (map and list views)
  - Category filtering (Gastronomía, Farmacia)
  - User registration and authentication (email/password + Google OAuth)
  - Promotion detail viewing and redemption code generation
  - User profile and purchase history management

### Web Panel
- **Role**: Combined interface for merchants and Woppa staff with role-based access
- **Technology**: React
- **Responsibilities**:
  - **Merchant Functions**:
    - Merchant registration and profile management
    - Promotion creation with images, categories, and conditions
    - Sales history and redemption tracking
    - Promotion status monitoring (pending, approved, rejected)
    - Coupon validation and confirmation for product delivery
  - **Woppa Staff Functions**:
    - Promotion validation and approval/rejection workflow
    - Merchant verification and management
    - Promotion highlighting and tagging (urgency labels)
    - System monitoring and user activity oversight

### Core API Backend
- **Role**: Centralized business logic and data management
- **Technology**: Node.js with PostgreSQL
- **Responsibilities**:
  - RESTful API serving all frontend applications
  - Business logic for promotions, users, and redemptions
  - Authentication and authorization management
  - Database operations and data integrity
  - Integration with external services (Google APIs, AWS)

### Authentication Service
- **Role**: User identity and access management
- **Technology**: Google OAuth 2.0 + custom JWT implementation
- **Responsibilities**:
  - Consumer and merchant authentication
  - Session management and token validation
  - Profile data synchronization with Google accounts
  - Role-based access control (consumer, merchant, staff)

### File Storage Service
- **Role**: Image management and delivery
- **Technology**: AWS S3 + CloudFront CDN
- **Responsibilities**:
  - Promotion image upload and storage
  - Image optimization and resizing
  - Global content delivery via CDN
  - Secure file access control

### Geolocation Service
- **Role**: Maps and location-based functionality
- **Technology**: Google Maps API + Google Places API
- **Responsibilities**:
  - Interactive map rendering for mobile app
  - Merchant address validation and geocoding
  - Proximity-based promotion filtering
  - Location autocomplete for merchant registration

### Payment Processing Service
- **Role**: Handle payment transactions for promotion redemptions
- **Technology**: Mercado Pago API + Payment Networks (Redes de Cobranza)
- **Responsibilities**:
  - Process online payments via Mercado Pago
  - Generate payment codes for offline payment networks
  - Payment validation and confirmation
  - Transaction status tracking and notifications

## Component Interaction Model

### Data Flow Architecture

The system follows a **centralized API architecture** where all business logic flows through the Core API Backend:

```
┌─────────────────┐              ┌─────────────────┐
│   Consumer      │              │   Web Panel     │
│   Mobile App    │              │                 │
└─────────┬───────┘              │ (Merchants +    │
          │                      │  Woppa Staff)   │
          │                      └─────────┬───────┘
          │                                │
          └────────────────────────────────┘
                                 │
                    ┌─────────────▼──────────────┐
                    │     Core API Backend       │
                    └─────────────┬──────────────┘
                                  │
    ┌─────────────┬─────────────────┼─────────────────┬─────────────┐
    │             │                 │                 │             │
┌───▼───┐  ┌──────▼──────┐  ┌──────▼──────┐  ┌──────▼──────┐  ┌────▼────┐
│ Auth  │  │ File Storage│  │ Geolocation │  │ Database    │  │ Payment │
│Service│  │  Service    │  │  Service    │  │(PostgreSQL) │  │ Service │
└───────┘  └─────────────┘  └─────────────┘  └─────────────┘  └─────────┘
```

### Key Interactions

**Consumer Experience Flow:**
1. Mobile App → Core API → Geolocation Service (map data)
2. Mobile App → Core API → Database (promotion listings)
3. Mobile App → Core API → Auth Service (registration/login)
4. Mobile App → Core API → Payment Service (process payment via Mercado Pago or payment networks)
5. Mobile App → Core API → Database (redemption code generation after payment confirmation)

**Web Panel Flow:**
1. Web Panel → Core API → Auth Service (merchant/staff login with role-based access)
2. Web Panel → Core API → File Storage (promotion image uploads)
3. Web Panel → Core API → Geolocation Service (merchant address validation)
4. Web Panel → Core API → Database (promotion submission, validation, and approval)

## Key Architectural Considerations

### MVP Constraints and Shortcuts

**Monolithic Approach**: Single Node.js backend instead of microservices to accelerate development and reduce operational complexity during validation phase.

**Manual Operations**: 
- Promotion validation requires human approval (12-hour SLA)
- Redemption verification is visual at merchant location
- No automated fraud detection or real-time inventory management

**Limited Scope**:
- Only two main categories (Gastronomía, Farmacia) with predefined subcategories
- Brazil-only launch with LGPD compliance
- Manual merchant onboarding process

### Shared Services and Dependencies

**Centralized Authentication**: Single identity system serves consumers, merchants, and staff with role-based permissions through the web panel.

**Unified Data Model**: PostgreSQL database with relational design supporting users, merchants, promotions, and redemptions across all interfaces.

**External Service Dependencies**:
- Google OAuth for simplified user registration
- Google Maps/Places APIs for geolocation functionality
- AWS infrastructure for file storage and CDN delivery
- Mercado Pago API for online payment processing
- Payment networks (Redes de Cobranza) for offline transactions

### Assumptions and Trade-offs

**Technology Trade-offs**:
- React Native chosen for faster cross-platform development over native performance
- PostgreSQL with Prisma provides type safety but requires relational data modeling
- Manual validation workflow limits scalability but ensures quality control

**Business Model Assumptions**:
- 2x1 promotions only (no complex discount structures)
- Geographic proximity drives user engagement
- Dual payment flow (online via Mercado Pago, offline via payment networks)
- Staff-curated content quality over automated scale

**Scalability Considerations**:
- Database and API designed to handle expected MVP load
- File storage and CDN support growth in image content
- Authentication system can scale with user base
- Manual processes identified for future automation

### Future Evolution Paths

The architecture supports gradual enhancement without major rewrites:
- Additional payment methods can be integrated through existing Payment Service
- AI-based validation can replace manual approval workflow  
- Push notifications can be integrated through existing mobile app
- Additional categories and features can extend existing data models
- Caching layer (Redis or similar) can be added if scale demands it
- Microservices migration possible if scale demands it

---
*Document created: 2025-01-24*