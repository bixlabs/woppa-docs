# 🧩 Epic: Offer Moderation

**KEY**: `OFFER-MODERATION-BACK`

---

## 📄 Functional Description
Basic offer validation system for Woppa staff to review and moderate submitted promotions using AdminJS. Focused on essential MVP functionality with 12-hour SLA for offer review, simple approval/rejection/adjustment workflows, and automatic publication to mobile app. Provides streamlined interface for quality assurance with email notifications and basic audit trails.

---

## 💻 Target Platform
This epic applies to:
- `back-office` (AdminJS interface)

---

## 🧭 Functional Scope
Main flows and interactions included in this epic:
- Offer review queue with submission time prioritization for 12-hour SLA
- Complete offer detail review with all submitted information and images
- Three-state decision workflow: approve, reject, or request adjustments
- Automatic email notifications for all status changes
- Direct publication to mobile app upon approval
- Basic audit logging for all review decisions
- Basic offer queue management with AdminJS default interface

---

## 🚫 Out of Scope
Explicitly excluded elements:
- Complex SLA analytics and performance dashboards
- Bulk operations for multiple offers
- Advanced image editing or enhancement tools
- Merchant quality tracking and scoring systems
- Review history appeals process
- Staff communication and collaboration tools
- Advanced analytics and reporting beyond basic metrics
- Comment template management systems

---

## 🖼 Wireframes Referenced in Epic
List of wireframes that apply to this epic and the stories that use them.

- No specific wireframes exist for back-office offer moderation screens
- AdminJS will provide default CRUD interface with customizations

---

## 🔍 Epic-level Ambiguities

- 📐 Missing wireframe: No wireframes exist for back-office offer moderation screens
- 📊 Business decision pending: Specific quality guidelines and rejection criteria
- 📋 Missing validation rules: Image quality standards and requirements
- 🔁 Undefined logic: Exact SLA escalation and notification procedures

---

## 🧵 User Stories

---

### 🔹 `OFFER-MODERATION-BACK-001` – Offer Review Queue

**Summary**:  
Provide AdminJS-based list view of all submitted offers with review status and SLA tracking.

**Justification**:  
Staff need to see all submitted offers in priority order to meet 12-hour SLA requirements efficiently.

**User Story**:  
"As a Woppa staff member, I want to view a prioritized queue of offers pending review, so that I can meet the 12-hour SLA for offer validation."

**🎯 Objective**:  
Create AdminJS resource for offers with customized list view showing essential review information and SLA indicators.

**⛓ Dependencies**:  
- AdminJS setup with Node.js backend
- PostgreSQL database with offers table
- Prisma ORM integration
- Staff authentication system

**✅ Acceptance Criteria**:
- List displays: business name, offer name, category, submission date, current status, time remaining for SLA
- Default ordering by submission time (oldest first) to prioritize SLA compliance
- Status indicators with clear visual distinction (pending, approved, rejected, needs adjustments)
- Visual urgency indicators for offers approaching 12-hour deadline
- Pagination for large lists
- Direct links to detailed review for each offer
- AdminJS default list interface with custom field configurations and SLA calculations

**🧰 Technical Tasks**:
- Configure AdminJS resource for offer model
- Customize list view fields with SLA time calculations
- Implement status indicators with appropriate styling
- Add computed fields for time remaining and urgency indicators
- Configure pagination and sorting options
- Set up proper field formatting (dates, status, time remaining)
- Add SLA urgency styling (red for < 2 hours, yellow for < 6 hours)

**⚙️ External Setup / Config Required**
- AdminJS installation and configuration
- Offer model definition in Prisma schema with submission timestamps
- Staff authentication middleware setup
- Database migrations for offers table

**❗ Pending Confirmations**
- Exact SLA urgency thresholds and color coding
- Default page size for offer queue
- Specific field display priorities

**📝 Notes & Observations**
- AdminJS provides built-in CRUD interface reducing development time
- SLA tracking critical for MVP service level requirements
- Focus on essential information for quick review decisions

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 2.5 hours
- Realistic: 4 hours
    - AdminJS Configuration: ~1.5h
    - SLA calculations and styling: ~1.5h
    - Custom field setup: ~0.5h
    - Testing: ~0.5h
- Pessimistic: 6 hours
- Final PERT Estimate: 4h
```

**🖼 Wireframe Reference**
- Exists: No
- AdminJS default interface with SLA customizations

---

### 🔹 `OFFER-MODERATION-BACK-002` – Offer Detail Review

**Summary**:  
Enable staff to access complete offer details through AdminJS show view for thorough review.

**Justification**:  
Staff need to review all submitted offer information and images before making approval/rejection decisions.

**User Story**:  
"As a Woppa staff member, I want to view complete offer details and images, so that I can make informed quality decisions."

**🎯 Objective**:  
Customize AdminJS show view to display all offer information in organized sections optimized for review.

**⛓ Dependencies**:  
- Offer Review Queue (OFFER-MODERATION-BACK-001)
- Image storage service for viewing uploaded images

**✅ Acceptance Criteria**:
- Show view displays all offer fields: name, description, price, category, expiration date
- Display all uploaded images with proper sizing and quality
- Show business information and location details
- Include submission timestamp and current status
- Clear section organization: Offer Details, Images, Business Info, Review History
- AdminJS default show interface with custom field groupings and image display

**🧰 Technical Tasks**:
- Configure AdminJS show view for offer resource
- Customize field groupings and sections
- Implement image display with proper sizing
- Configure offer detail formatting (price, dates, descriptions)
- Add business information display integration
- Implement responsive layout for AdminJS show view
- Add image viewing capabilities (zoom, multiple images)

**⚙️ External Setup / Config Required**
- Image storage service integration for display
- Offer model definition with all submission fields
- Business relationship for merchant information display

**❗ Pending Confirmations**
- Image display preferences and sizing
- Field grouping priorities for review workflow
- Integration level with business information

**📝 Notes & Observations**
- AdminJS show view provides good foundation for detail display
- Image quality review is critical for offer approval
- Focus on efficient review workflow

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 2 hours
- Realistic: 3 hours
    - AdminJS show view configuration: ~1h
    - Image display setup: ~1h
    - Field formatting and grouping: ~0.5h
    - Testing: ~0.5h
- Pessimistic: 4.5 hours
- Final PERT Estimate: 3h
```

**🖼 Wireframe Reference**
- Exists: No
- AdminJS default show view with custom sections and image display

---

### 🔹 `OFFER-MODERATION-BACK-003` – Offer Approval Process

**Summary**:  
Implement single-click offer approval through AdminJS actions with status change and email notification.

**Justification**:  
Staff need efficient way to approve quality offers and make them visible in the mobile app through status change.

**User Story**:  
"As a Woppa staff member, I want to approve offers with one click, so that quality offers become visible in the mobile app."

**🎯 Objective**:  
Create AdminJS custom action for offer approval with status change to "approved" and email notification.

**⛓ Dependencies**:  
- Offer Detail Review (OFFER-MODERATION-BACK-002)
- Email service configuration

**✅ Acceptance Criteria**:
- "Approve" action button available on offer detail view
- Single click changes status from "pending" to "approved"
- Status change makes offer visible in mobile app automatically (backend filters by approved status)
- Email notification sent to merchant confirming approval
- Action logs approval with staff member ID and timestamp
- Success confirmation message displayed
- Status change reflected immediately in queue
- Action only available for offers in "pending" or "needs adjustments" status

**🧰 Technical Tasks**:
- Create AdminJS custom action for approval
- Implement status change logic to "approved"
- Configure email notification service integration
- Add audit logging for approval actions
- Create email template for approval notification
- Add success/error handling and user feedback

**⚙️ External Setup / Config Required**
- Email service configuration
- Email template setup for approval notifications
- Audit logging database schema

**❗ Pending Confirmations**
- Email template content and format
- Specific approval confirmation messaging

**📝 Notes & Observations**
- AdminJS custom actions provide clean integration
- Status change automatically makes offer visible in mobile app
- Email notifications important for merchant communication

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 2 hours
- Realistic: 3.5 hours
    - AdminJS custom action setup: ~1.5h
    - Status change logic: ~0.5h
    - Email integration: ~1h
    - Audit logging: ~0.25h
    - Testing and validation: ~0.25h
- Pessimistic: 5 hours
- Final PERT Estimate: 3.5h
```

**🖼 Wireframe Reference**
- Exists: No
- AdminJS action interface with custom approval button

---

### 🔹 `OFFER-MODERATION-BACK-004` – Offer Rejection Process

**Summary**:  
Implement offer rejection workflow through AdminJS with mandatory comments and email notification.

**Justification**:  
Staff need to reject substandard offers with clear feedback to help merchants improve submissions.

**User Story**:  
"As a Woppa staff member, I want to reject offers with explanatory comments, so that merchants understand quality standards."

**🎯 Objective**:  
Create AdminJS custom action for offer rejection with required comment field and automated email notification.

**⛓ Dependencies**:  
- Offer Approval Process (OFFER-MODERATION-BACK-003)
- Email service configuration

**✅ Acceptance Criteria**:
- "Reject" action button available on offer detail view
- Action opens modal/form requiring mandatory comment field
- Status changes from "pending" to "rejected" after confirmation
- Email notification sent to merchant with rejection reason
- Action logs rejection with staff member ID, timestamp, and comment
- Comment character limit (500 characters maximum)
- Success confirmation message displayed
- Rejected offers remain accessible to merchant for reference

**🧰 Technical Tasks**:
- Create AdminJS custom action for rejection with form modal (reuses approval infrastructure)
- Implement comment validation and storage
- Configure rejection email notification
- Add audit logging for rejection actions
- Create email template for rejection notification
- Add form validation and error handling

**⚙️ External Setup / Config Required**
- Email service configuration (already configured from approval)
- Database schema for storing rejection comments
- Email template setup for rejection notifications

**❗ Pending Confirmations**
- Rejection comment guidelines and examples
- Email template tone and content
- Character limits for rejection comments

**📝 Notes & Observations**
- AdminJS forms and modals provide good UX for comment collection
- Reuses approval infrastructure significantly reducing development time
- Clear feedback helps merchants improve future submissions

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 1.5 hours
- Realistic: 2.5 hours
    - AdminJS custom action with form modal: ~1h (reuses approval infrastructure)
    - Rejection email template: ~0.5h (copy of approval template)
    - Comment storage and validation: ~0.5h
    - Testing: ~0.5h
- Pessimistic: 4 hours
- Final PERT Estimate: 2.5h
```

**🖼 Wireframe Reference**
- Exists: No
- AdminJS action interface with custom rejection form

---

### 🔹 `OFFER-MODERATION-BACK-005` – Request Adjustments Process

**Summary**:  
Implement "needs adjustments" workflow through AdminJS allowing merchants to edit and resubmit offers.

**Justification**:  
Staff need to request specific changes for offers that have potential but need modifications before approval.

**User Story**:  
"As a Woppa staff member, I want to request specific adjustments to offers, so that merchants can fix issues and resubmit."

**🎯 Objective**:  
Create AdminJS custom action for requesting adjustments with detailed feedback and resubmission capability.

**⛓ Dependencies**:  
- Offer Rejection Process (OFFER-MODERATION-BACK-004)
- Merchant offer editing system integration

**✅ Acceptance Criteria**:
- "Request Adjustments" action button available on offer detail view
- Action opens modal/form requiring mandatory comment field with specific change requests
- Status changes from "pending" to "needs adjustments" after confirmation
- Email notification sent to merchant with detailed adjustment requests
- Merchant can edit offer and resubmit for review
- Action logs adjustment request with staff member ID, timestamp, and comments
- Resubmitted offers return to "pending" status for re-review
- Comment character limit (500 characters maximum)

**🧰 Technical Tasks**:
- Create AdminJS custom action for adjustment requests (reuses rejection infrastructure)
- Implement adjustment comment storage and validation
- Configure adjustment email notification
- Add audit logging for adjustment requests
- Create email template for adjustment requests
- Add integration with merchant editing workflow

**⚙️ External Setup / Config Required**
- Email service configuration (already configured)
- Database schema for storing adjustment comments (reuses rejection schema)
- Email template setup for adjustment requests
- Integration with merchant offer editing system

**❗ Pending Confirmations**
- Adjustment request guidelines and common scenarios
- Email template content and merchant guidance
- Resubmission workflow integration details

**📝 Notes & Observations**
- Reuses rejection infrastructure with different status and email template
- Critical for maintaining merchant relationships while ensuring quality
- Allows iterative improvement rather than outright rejection

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 1 hour
- Realistic: 2 hours
    - AdminJS custom action: ~0.5h (reuses rejection infrastructure)
    - Adjustment email template: ~0.5h (variation of rejection template)
    - Integration with merchant editing: ~0.5h
    - Testing: ~0.5h
- Pessimistic: 3 hours
- Final PERT Estimate: 2h
```

**🖼 Wireframe Reference**
- Exists: No
- AdminJS action interface with custom adjustment form

---

## 📊 Epic Estimation Summary

Epic totals:

- Total user stories: 5
- Stories with moderate complexity: 5
- Stories leveraging AdminJS and reusing infrastructure: 5

### Manual 3-point Estimation for Epic (PERT)

```
- Optimistic: 9h
- Realistic: 15h  
- Pessimistic: 22.5h
- Final PERT Estimate: 15.25h
```

---