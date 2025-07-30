# Epic: Offer Management
**KEY**: `OFFER-MGMT-WEB`  
**Platform**: Web Panel (Merchants)  
**Status**: Defined  

## Overview
Complete lifecycle management of 1+1 type offers including creation, administration, and post-publication management. Covers offer creation through structured forms with product information input, category/subcategory selection, image upload with quality validation, pricing, location mapping, and expiration dates. Includes active and historical offer views, duplication capabilities, editing functionality, status management (expired/sold out), comprehensive filtering options, and organized access to past performance data with reactivation workflows.

## User Stories

### Offer Creation

• **Story 1: Create New Offer Form**  
  *Description:* Merchant creates new 1+1 offer using structured form with 10 required fields: offer name (product only), discount type (fixed as 1+1), category selection, subcategory selection, product images (1-2 required), redemption time limit, description/conditions, final price, location validation, and expiration date. Form includes real-time validation and help integration.

• **Story 2: Category & Subcategory Management**  
  *Description:* System provides category selection (Gastronomía, Farmacia) with dynamic subcategory loading based on selection. Subcategories show most popular 5 first, then expand to show up to 10 per category. Multiple categories allowed, but only one subcategory per category.

• **Story 3: Image Upload & Validation**  
  *Description:* Merchants upload 1-2 product images with quality validation (good lighting, clear product display). System validates file type (JPG/PNG), size (max 5MB), and minimum dimensions. Images are mandatory and must pass quality checks.

• **Story 4: Location & Address Integration**  
  *Description:* Merchants specify offer location using Google Maps integration. System validates address against Google Places API and prevents invalid or unrecognized addresses. Location data used for mobile app geolocation features.

• **Story 5: Offer Preview & Submission**  
  *Description:* Before final submission, merchant sees preview of how offer will appear in mobile app. Preview shows all details formatted as end users will see. Merchant can confirm and submit for review or return to edit.

### Offer Management & Status

• **Story 6: Offer Status Tracking**  
  *Description:* Merchants view status of all submitted offers: "En revisión" (under review), "Necesita ajustes" (needs adjustments), "Aprobada" (approved/active), "Agotada" (sold out), "Expirada" (expired). Status updates automatically based on staff actions and system rules.

• **Story 7: Active Offers Dashboard**  
  *Description:* Merchants view all currently active (approved) offers with key details: name, category, expiration date, current status. Includes quick actions like view details, duplicate, or mark as sold out (if applicable).

• **Story 8: Edit Pending Offers**  
  *Description:* Merchants can edit offers that are "En revisión" or "Necesita ajustes" status. Once approved, offers cannot be edited directly but can be duplicated to create new versions.

• **Story 9: Offer Duplication**  
  *Description:* Merchants can duplicate any existing offer (active, expired, or rejected) to create new offer with pre-filled data. All fields are copied and merchant can modify before submitting as new offer.

### Historical & Archive Management

• **Story 10: Historical Offers View**  
  *Description:* Merchants access archive of past offers (expired, rejected, sold out) for reference only. Historical offers cannot be edited or reactivated directly, but can be duplicated to create new versions.

• **Story 11: Offer Performance Data**  
  *Description:* For each historical offer, merchant views basic performance metrics: total coupons generated, total redeemed, dates active, and final status. Data helps inform future offer creation.

• **Story 12: Filtering & Search**  
  *Description:* Merchants filter offers by status, date range, category, and search by offer name. Filters apply to both active and historical views with clear filter state indicators.

### Workflow Integration

• **Story 13: Staff Feedback Integration**  
  *Description:* When offers are marked "Necesita ajustes" by staff, merchants see specific feedback comments and can address issues before resubmitting. System tracks revision history.

• **Story 14: Automatic Status Updates**  
  *Description:* System automatically updates offer status based on expiration dates (to "Expirada") and staff actions. Merchants receive notifications about status changes via email.

• **Story 15: Help & Support Integration**  
  *Description:* Offer creation and management screens include contextual help links and direct access to WhatsApp Business support for guidance on offer creation best practices.

## Technical Requirements

- Google Maps API for location validation
- Image processing and storage system
- Real-time form validation
- File upload with size/type restrictions
- Email notification system
- Dynamic category/subcategory loading
- Offer status state management
- Search and filtering functionality
- WhatsApp Business API integration

## Acceptance Criteria Summary

- All 10 form fields properly validated and required
- Images mandatory with quality validation
- Location must be validated through Google Maps API
- Preview shows accurate mobile app representation
- Status transitions work correctly with notifications
- Duplication creates exact copies ready for editing
- Filtering and search work across all offer states
- Staff feedback properly integrated into workflow
- Help system accessible throughout offer management

## Dependencies

- Business Authentication epic (approved merchants only)
- Back-office Offer Moderation epic for approval workflow
- Google Maps API setup
- Email service configuration
- Image storage and processing service
- WhatsApp Business API setup