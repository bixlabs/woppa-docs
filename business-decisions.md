# Business Decisions

## Document Purpose

This document contains confirmed business decisions for the Woppa MVP project. These decisions supersede any conflicting information in other documents, including requirements.docx.md. This is the ultimate source of truth for business logic and functional requirements.

## Key Business Decisions

### Payment requirement decision:
- **Date**: 2025-01-25
- **Decision**: Payment is fundamental and required before redemption code delivery. Payment must be completed successfully before user receives the coupon code.
- **Affects**: Wireframe 4 (Registration) → Wireframe 5 (Coupon) flow and all coupon redemption use cases

### Payment methods decision:
- **Date**: 2025-01-25
- **Decision**: MVP will implement only Mercado Pago Brasil integration. Cash network ("red de cobranza") will NOT be implemented in MVP scope and remains for next phase.
- **Affects**: All payment-related flows and wireframes

### UI flow simplification:
- **Date**: 2025-01-25  
- **Decision**: No specific wireframes will be created for payment flow. Implementation must follow most straightforward MVP approach where payment is completed before redemption code is generated and displayed.
- **Affects**: Wireframe 5 (Obtained Coupon) and payment flow design

### Mercado Pago implementation decision:
- **Date**: 2025-01-25
- **Decision**: Use Mercado Pago Checkout Pro for payment processing. This provides an embedded controlled experience that includes the complete purchase detail display, multiple payment methods, and control over the checkout content. Webhook notifications will inform our backend when payment is confirmed, and we maintain redirection control. Mercado Pago Link is discarded because it doesn't provide payment confirmation to the app, lacks redirection control, and doesn't allow checkout content customization.
- **Affects**: Payment flow implementation, webhook handling, and checkout experience

### Map implementation decision for offer details:
- **Date**: 2025-01-25
- **Decision**: In offer details screens, the map will be static and not dynamic. The static map serves only as a visual reference of the business location and includes a "Get Directions" button/link that opens the device's native maps application for navigation. This approach prioritizes performance, reduces complexity, and aligns with the MVP's core functionality focus.
- **Affects**: Offer details screen implementation and map integration requirements

### User registration simplification decision:
- **Date**: 2025-01-25
- **Decision**: Phone number will NOT be requested during registration in this first phase. Registration will be simplified to only require email, password, and names (first name, last name). Google Sign-In will also be supported and will obtain the same basic information (email, names, and potentially profile image) without requiring additional phone verification.
- **Affects**: Registration flow, user data model, authentication implementation, and all registration-related wireframes and user stories

### Redemption code format decision:
- **Date**: 2025-01-25
- **Decision**: Redemption codes will be displayed in alphanumeric format (characters and numbers). QR code format will NOT be implemented in the MVP scope.
- **Affects**: Coupon display, redemption code generation, merchant verification flow, and mobile account management features

### Single-use coupon clarification:
- **Date**: 2025-01-29
- **Decision**: Each coupon code is designed for single presentation and single redemption. When a user purchases multiple units (e.g., 3 units), they receive one code that, when presented once at the business, provides all purchased units of the promotion. The coupon cannot be presented multiple times - one presentation = full redemption of all purchased units.
- **Rationale**: This approach simplifies the redemption process for businesses and users, avoiding complex partial redemption tracking while maintaining the quantity-based purchase system.
- **Affects**: Epic REDEEM-MOB (offer redemption flow) - confirms current design is correct, Epic ACC-MOB (account management) - coupon displays "Cantidad: X unidades" but redeems all at once, Web panel validation system - single validation marks entire coupon as redeemed, Email templates and user instructions - emphasize single presentation for full benefit

---
**Last Updated**: 2025-01-29