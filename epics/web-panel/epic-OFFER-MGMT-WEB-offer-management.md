# 🧩 Epic: Offer Management

**KEY**: `OFFER-MGMT-WEB`

---

## 📄 Functional Description
Comprehensive offer lifecycle management for merchants enabling creation, editing, duplication and status tracking of 1+1 promotions through React web interface. Provides structured 10-field form for offer creation with dynamic category selection, Google Maps location validation, image quality validation, and preview functionality. Includes offer status tracking through 5 distinct states and duplication capabilities for merchant convenience. Focused on essential offer management without complex analytics or sales tracking.

---

## 💻 Target Platform
This epic applies to:
- `web-panel`

---

## 🧭 Functional Scope
Main flows and interactions included in this epic:
- Offer creation using 10-field structured form with validations
- Dynamic category/subcategory selection with popular options first
- Image upload with quality validation requirements
- Google Maps integration for location validation
- Offer preview before submission for review
- Offer editing for pending/adjustment-needed offers only
- Offer status tracking (en revisión, necesita ajustes, aprobada, agotada, expirada)
- Offer duplication with pre-filled data for new submissions

---

## 🚫 Out of Scope
Explicitly excluded elements:
- Sales metrics and performance analytics (covered in SALES-TRACKING-WEB)
- Manual coupon redemption functionality (covered in SALES-TRACKING-WEB)
- Active/historical offer dashboards with detailed metrics
- Staff feedback integration via UI (handled via email for MVP)
- Complex filtering and search capabilities
- WhatsApp Business integration (handled in BIZ-AUTH-WEB)
- Offer deletion or deactivation workflows
- Bulk offer operations
- Advanced image editing or processing beyond validation

---

## 🖼 Wireframes Referenced in Epic
List of wireframes that apply to this epic and the stories that use them.

- No specific wireframes exist for merchant offer management screens
- React interface will use existing design system patterns
- Related wireframe: `woppa-wireframe-comerciante-1.png` (merchant interface reference)

---

## 🔍 Epic-level Ambiguities

- 📐 Missing wireframe: No wireframes exist for offer creation/editing forms
- 📊 Business decision pending: Exact subcategory lists for Gastronomía and Farmacia
- 📋 Missing validation rules: Specific image quality validation criteria and error messages
- 🔁 Undefined logic: "Tiempo para canjear" selector exact options and default values

---

## 🧵 User Stories

---

### 🔹 `OFFER-MGMT-WEB-001` – Offer Creation Form

**Summary**:  
Enable merchants to create new 1+1 offers using structured 10-field form with validations as specified in requirements.

**Justification**:  
Merchants need comprehensive form to create offers with all required fields including category selection, image upload, location validation, and pricing information.

**User Story**:  
"As a merchant, I want to create new 1+1 offers using a structured form with all required fields, so that I can submit promotions for review."

**🎯 Objective**:  
Provide complete offer creation form with 10 specific fields, dynamic category loading, image validation, and Google Maps integration.

**⛓ Dependencies**:
- Business authentication system (BIZ-AUTH-WEB)
- Google Maps API for location validation
- Image storage and processing service
- Backend API for offer data storage

**✅ Acceptance Criteria**:
- Form includes all 10 required fields: nombre de la publicación (product name only), tipo de descuento (fixed as "1+1"), categoría principal, subcategoría, fotos del producto (1-2 images), tiempo para canjear el beneficio, descripción, precio final, ubicación, fecha de vencimiento
- Category selection (Gastronomía, Farmacia) with multiple categories allowed
- Dynamic subcategory loading showing 5 most popular first, then up to 10 per category
- One subcategory selection per category selected
- Image upload validation: JPG/PNG, max 5MB, minimum dimensions, quality validation (good lighting, clear product)
- "Tiempo para canjear" selector with fixed options: 6 horas, 12 horas, 1 día, 3 días, 1 semana
- Location field with Google Maps validation - only accepts verified addresses
- Real-time form validation for all fields
- All fields properly validated before enabling submission
- Form submission sets offer status to "en revisión"

**🧰 Technical Tasks**:
- Create responsive React offer creation form with 10 fields
- Implement dynamic category/subcategory loading from backend
- Add image upload component with validation (file type, size, dimensions)
- Integrate Google Places API for location validation
- Create "tiempo para canjear" selector with predefined options
- Add real-time field validation
- Implement form submission to backend API
- Style form using existing design system
- Add proper error handling for validation failures

**⚙️ External Setup / Config Required**
- Google Places API configuration
- Image storage service (AWS S3 or similar)
- Backend API endpoints for offer creation
- Category/subcategory data seeding

**❗ Pending Confirmations**
- Complete subcategory lists for Gastronomía and Farmacia
- Specific image quality validation criteria
- Character limits for description field
- Default "tiempo para canjear" selection

**📝 Notes & Observations**
- Core functionality for merchant offer creation
- All 10 fields from requirements must be implemented
- Focus on comprehensive validation and user guidance
- No wireframe exists - UI design needed

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 12 hours
- Realistic: 15.5 hours
    - Frontend UI (10-field form, responsive, no wireframe): ~5h
    - Frontend Logic (Zod validation, dynamic loading): ~2h
    - Integration (Google Maps, image upload with quality validation): ~3h
    - Backend (offer CREATE endpoints, image storage): ~2.5h
    - Manual Testing: ~1h
    - Backend Testing: ~2h
- Pessimistic: 22 hours
- Final PERT Estimate: 16h
```

**🖼 Wireframe Reference**
- Exists: No
- Offer creation form design needed

---

### 🔹 `OFFER-MGMT-WEB-002` – Offer Edit Form

**Summary**:  
Enable merchants to edit existing offers that are in "necesita ajustes" status only, using same form structure.

**Justification**:  
Merchants need ability to modify offers that have been reviewed and require adjustments based on staff feedback, but not offers under review or approved offers to maintain data integrity.

**User Story**:  
"As a merchant, I want to edit my offers that need adjustments based on staff feedback, so that I can address issues and resubmit for approval."

**🎯 Objective**:  
Reuse offer creation form for editing with restrictions based on offer status.

**⛓ Dependencies**:
- Offer Creation Form (OFFER-MGMT-WEB-001)
- Offer status tracking system
- Backend API for offer updates

**✅ Acceptance Criteria**:
- Edit form only accessible for offers with status "necesita ajustes" 
- Offers "en revisión", "aprobada", "agotada", or "expirada" cannot be edited
- Form pre-populated with existing offer data
- All 10 fields editable for eligible offers
- Same validation rules as creation form apply
- Successful edit resets status to "en revisión" for re-evaluation
- Clear indication that user is editing existing offer that needs adjustments
- Non-editable offers show read-only view or redirect to duplication
- Form submission updates existing offer record and triggers re-review

**🧰 Technical Tasks**:
- Extend offer creation form component for edit mode
- Add offer data loading and form population logic
- Implement offer status validation before allowing edit
- Add edit-specific UI indicators and messaging
- Modify form submission to update instead of create
- Add proper routing for edit functionality
- Implement restrictions for non-editable offer statuses
- Add confirmation messaging for successful updates

**⚙️ External Setup / Config Required**
- Backend API endpoints for offer retrieval and updates
- Offer status validation middleware
- Routing configuration for edit pages

**❗ Pending Confirmations**
- Specific messaging for non-editable offers in different statuses
- Navigation flow after successful edit and status reset
- Staff notification process when edited offer returns to review

**📝 Notes & Observations**
- Reuses creation form logic for consistency
- Important status-based access control
- Should provide clear feedback about editability

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 3.5 hours
- Realistic: 5.5 hours
    - Frontend Logic (edit mode, data loading, reuses generated components): ~1.5h
    - Status validation and restrictions: ~1h
    - Backend (update endpoints, status validations, data retrieval): ~2h
    - Testing and error handling: ~0.5h
    - Backend Testing: ~0.5h
- Pessimistic: 8 hours
- Final PERT Estimate: 5.6h
```

**🖼 Wireframe Reference**
- Exists: No
- Edit form interface design needed

---

### 🔹 `OFFER-MGMT-WEB-003` – Offer Preview Before Submission

**Summary**:  
Display preview of how offer will appear in mobile app before final submission to allow merchant review.

**Justification**:  
Merchants need to see exactly how their offer will appear to end users to ensure accuracy and visual appeal before submission.

**User Story**:  
"As a merchant, I want to preview how my offer will look in the mobile app before submitting, so that I can ensure it appears correctly to customers."

**🎯 Objective**:  
Create preview interface that accurately represents mobile app offer display.

**⛓ Dependencies**:
- Offer Creation Form (OFFER-MGMT-WEB-001)
- Mobile app offer display components (for accurate preview)
- Image processing for preview display

**✅ Acceptance Criteria**:
- Preview accessible from offer creation/edit forms via "Pre-publicar" button
- Button only enabled when all required fields are valid
- Preview shows offer exactly as it will appear in mobile app
- Displays: offer name, category/subcategory tags, images, "1+1" benefit label, business name, conditions, location, pricing
- Preview includes mobile app styling and layout
- Merchant can confirm and submit for review or return to edit
- Clear confirmation message after submission: "Gracias por enviar tu publicación. Estamos revisándola y te notificaremos pronto"
- Preview works for both new offers and edited offers

**🧰 Technical Tasks**:
- Create mobile app-style preview component
- Implement preview data formatting to match mobile display
- Add "Pre-publicar" button to offer forms with validation
- Create preview modal or page with offer representation
- Add confirmation and submission functionality from preview
- Implement "return to edit" functionality
- Style preview to match mobile app appearance
- Add success messaging after submission

**⚙️ External Setup / Config Required**
- Mobile app styling reference for accurate preview
- Image processing for preview thumbnails
- Final submission API endpoints

**❗ Pending Confirmations**
- Exact mobile app styling for preview accuracy
- Preview display format (modal vs. full page)
- Specific success message text

**📝 Notes & Observations**
- Critical for merchant confidence in submissions
- Should match mobile app appearance exactly
- Provides final validation step before review

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 4 hours
- Realistic: 6 hours
    - Frontend UI (preview component, auto-generated): ~2h
    - Preview formatting and styling (accelerated with AI): ~1.5h
    - Integration with forms and submission: ~1h
    - Backend (submission endpoint, status management): ~1h
    - Testing and refinement: ~0.5h
- Pessimistic: 9 hours
- Final PERT Estimate: 6.17h
```

**🖼 Wireframe Reference**
- Exists: No
- Preview interface design needed

---

### 🔹 `OFFER-MGMT-WEB-004` – Offer Duplication

**Summary**:  
Enable merchants to duplicate any existing offer to create new offer with pre-filled data for easier offer creation.

**Justification**:  
Merchants need efficient way to create similar offers by duplicating existing ones rather than starting from scratch each time.

**User Story**:  
"As a merchant, I want to duplicate any of my existing offers, so that I can quickly create new offers with similar information."

**🎯 Objective**:  
Provide duplication functionality that copies all offer data and opens creation form for modification.

**⛓ Dependencies**:
- Offer Creation Form (OFFER-MGMT-WEB-001)
- Offer status tracking system
- Backend API for offer data retrieval

**✅ Acceptance Criteria**:
- Duplication available for offers in any status (active, expired, rejected, etc.)
- "Duplicate" action copies all 10 fields from original offer
- Duplication opens offer creation form with pre-filled data
- All fields remain editable in duplicated form
- Duplicated offer starts as new offer ("en revisión" status after submission)
- Clear indication that user is working with duplicated offer
- Original offer remains unchanged
- Duplication works from any offer list or detail view
- Success message confirms duplication and form pre-population

**🧰 Technical Tasks**:
- Add "Duplicate" button/action to offer interfaces
- Implement offer data retrieval for duplication
- Modify creation form to accept pre-filled data
- Add duplication logic to copy all offer fields
- Implement routing from duplication to creation form
- Add UI indicators for duplicated offers
- Ensure proper data formatting during duplication
- Add confirmation messaging for duplication success

**⚙️ External Setup / Config Required**
- Backend API endpoints for offer data retrieval
- Form state management for pre-filled data
- Routing configuration for duplication workflow

**❗ Pending Confirmations**
- Whether images are copied or need re-upload during duplication
- Specific UI placement for duplicate actions
- Confirmation requirements before duplication

**📝 Notes & Observations**
- Improves merchant efficiency significantly
- Should work across all offer statuses for maximum utility
- Consider image handling during duplication

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 3 hours
- Realistic: 6 hours
    - Frontend Logic (duplication workflow, auto-generated): ~1.5h
    - Data copying and form pre-population (accelerated): ~1h
    - Backend (data retrieval, copy logic, image handling): ~3h
    - Testing and edge cases: ~0.5h
- Pessimistic: 10 hours
- Final PERT Estimate: 6.17h
```

**🖼 Wireframe Reference**
- Exists: No
- Duplication interface and workflow design needed

---

### 🔹 `OFFER-MGMT-WEB-005` – Offer Status Tracking

**Summary**:  
Display and track offer status through the 5 defined states with automatic status updates as specified in requirements.

**Justification**:  
Merchants need visibility into offer approval process and current status to understand where their offers stand in the review workflow.

**User Story**:  
"As a merchant, I want to see the current status of all my offers, so that I know which ones are under review, approved, or need attention."

**🎯 Objective**:  
Implement comprehensive status tracking system with clear visual indicators for all 5 offer states.

**⛓ Dependencies**:
- Backend API for status management
- Staff moderation system (external)
- Email notification system
- Offer creation system

**✅ Acceptance Criteria**:
- Display 5 distinct offer states: "En revisión", "Necesita ajustes", "Aprobada", "Agotada", "Expirada"
- Visual indicators (colors, icons) for each status type
- Status updates automatically based on staff actions and system rules
- "Expirada" status automatically applied when expiration date passes
- "Agotada" status can be set manually by staff
- Clear status explanations for merchant understanding
- Status history/timestamps visible for transparency
- Email notifications sent when status changes
- Status filtering capabilities in offer lists
- Date range filtering to view offers by creation/expiration date
- Category and subcategory filtering to view offers by type
- Real-time status updates when page refreshes or filters change

**🧰 Technical Tasks**:
- Create status indicator components with appropriate styling
- Implement status display logic for offer lists and details
- Add automatic status update system for expired offers
- Create status filtering functionality
- Implement date range filtering for offer lists
- Add category and subcategory filtering components
- Implement status change notification system
- Add status history tracking and display
- Style status indicators with consistent design
- Add status-based action restrictions (edit, duplicate, etc.)

**⚙️ External Setup / Config Required**
- Backend API endpoints for status management with filtering parameters
- Scheduled jobs for automatic status updates (expiration)
- Email service configuration for status notifications
- Status change webhooks from staff moderation system
- Database queries with date range and category filtering capabilities

**❗ Pending Confirmations**
- Exact status transition rules and timing
- Visual design for status indicators
- Email notification content and timing
- Status history detail requirements

**📝 Notes & Observations**
- Core functionality for offer lifecycle management
- Should provide clear communication about offer pipeline
- Status system drives other functionality (edit permissions, etc.)

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 6 hours
- Realistic: 10 hours
    - Frontend UI (offers table/list with columns, pagination): ~4h
    - Status indicators and visual badges: ~1h
    - Date range filtering components (accelerated): ~1h
    - Category and subcategory filtering components (accelerated): ~1h
    - Backend (list API endpoints, filtering logic): ~2.5h
    - Testing and UI validation: ~0.5h
- Pessimistic: 14 hours
- Final PERT Estimate: 10h
```

**🖼 Wireframe Reference**
- Exists: No
- Status tracking interface design needed

---

### 🔹 `OFFER-MGMT-WEB-006` – Scheduled Jobs and Automation

**Summary**:  
Implement backend scheduled jobs for automated coupon expiration processing and email notifications as specified in requirements.

**Justification**:  
System requires automated processes to handle coupon expiration based on redemption time limits and send email notifications for status changes without manual intervention.

**User Story**:  
"As a system administrator, I want automated jobs to handle coupon expiration and email notifications, so that the platform operates correctly without manual intervention."

**🎯 Objective**:  
Implement scheduled jobs for coupon expiration processing and email notification system using backend job scheduling.

**⛓ Dependencies**:
- Offer creation system (OFFER-MGMT-WEB-001)
- Coupon generation system (from mobile app requirements)
- Email service configuration
- Backend job scheduling infrastructure

**✅ Acceptance Criteria**:
- Daily job to process expired coupons based on redemption time limits (6h, 12h, 1 day, 3 days, 1 week)
- Change coupon status from "pagado" to "expirado" when redemption deadline passes
- Email notification job for time-based notifications (coupon expiration alerts if needed)
- Job monitoring and error handling for failed executions
- Configurable job schedules and retry mechanisms
- Logging system for job execution tracking and debugging
- Database cleanup jobs for expired temporary data if needed

**🧰 Technical Tasks**:
- Implement job scheduling infrastructure (cron jobs or task queue)
- Create coupon expiration job with time-based logic
- Implement time-based email notifications (if required for coupon expiration)
- Add job monitoring and error handling mechanisms
- Create database queries for bulk coupon status updates
- Implement email templates for automated notifications
- Add logging and monitoring for scheduled job execution
- Configure retry mechanisms for failed jobs
- Add job execution history tracking

**⚙️ External Setup / Config Required**
- Job scheduling service configuration (cron, node-cron, or task queue)
- Email service provider setup (SendGrid, SES, or similar)
- Email templates configuration for different notification types
- Job monitoring and alerting system setup

**❗ Pending Confirmations**
- Email service provider preference and configuration
- Specific email template content and styling requirements
- Job execution frequency and timing preferences
- Error handling and retry policy specifications

**📝 Notes & Observations**
- Critical for system functionality - coupons must expire automatically
- Email notifications are required per business requirements
- Jobs should be resilient and handle failures gracefully
- Consider timezone handling for Brazilian market

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 3.5 hours
- Realistic: 6 hours
    - Job scheduling infrastructure setup: ~1.5h
    - Coupon expiration job implementation: ~2.5h
    - Time-based notifications (if needed): ~1h
    - Job monitoring and error handling: ~0.5h
    - Testing and validation: ~0.5h
- Pessimistic: 9 hours
- Final PERT Estimate: 6h
```

**🖼 Wireframe Reference**
- Exists: No
- Backend system - no UI required

---

## 📊 Epic Estimation Summary

Epic totals:

- Total user stories: 6
- Stories with moderate complexity: 5
- Stories with high complexity: 1
- Stories requiring external API integration: 5
- Backend-only stories: 1

### Manual 3-point Estimation for Epic (PERT)

```
- Optimistic: 32h
- Realistic: 49h  
- Pessimistic: 72h
- Final PERT Estimate: 50h
```

---