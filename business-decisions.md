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

---
**Last Updated**: 2025-01-25