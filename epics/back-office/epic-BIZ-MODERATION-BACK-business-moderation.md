# 🧩 Epic: Business Moderation

**KEY**: `BIZ-MODERATION-BACK`

---

## 📄 Functional Description
Basic administrative panel for Woppa staff to validate business registrations and manage account statuses using AdminJS. Focused on essential MVP functionality with simple operational workflows, basic audit trails, and CRUD operations for business onboarding management. Provides streamlined interface for registration approval, status management, and basic business data editing.

---

## 💻 Target Platform
This epic applies to:
- `back-office` (AdminJS interface)

---

## 🧭 Functional Scope
Main flows and interactions included in this epic:
- Business registration list view with status indicators
- Individual registration review with complete business information
- Single-click approval/rejection workflow with email notifications
- Basic account status management (pending/approved/rejected/suspended)
- Manual business data editing for exception handling
- Simple search and filtering by business name, CNPJ, status
- Basic audit logging for status changes and edits

---

## 🚫 Out of Scope
Explicitly excluded elements:
- Complex analytics and reporting dashboards
- Advanced communication systems or messaging
- Bulk operations for multiple businesses
- WhatsApp Business API integration
- Complex compliance monitoring automation
- Advanced audit trail features beyond basic logging
- Performance metrics and business activity monitoring

---

## 🖼 Wireframes Referenced in Epic
List of wireframes that apply to this epic and the stories that use them.

- No specific wireframes exist for back-office administration screens
- AdminJS will provide default CRUD interface with customizations

---

## 🔍 Epic-level Ambiguities

- 📐 Missing wireframe: No wireframes exist for back-office administration screens
- 📊 Business decision pending: Specific email templates for approval/rejection notifications
- 📋 Missing validation rules: Exact audit logging requirements and retention
- 🔁 Undefined logic: Staff role definitions and access levels

---

## 🧵 User Stories

---

### 🔹 `BIZ-MODERATION-BACK-001` – Business Registration List View

**Summary**:  
Provide AdminJS-based list view of all registered businesses with key information and status indicators.

**Justification**:  
Staff need to see all business registrations in a single view to manage the approval queue efficiently.

**User Story**:  
"As a Woppa staff member, I want to view a list of all business registrations with their status, so that I can manage the approval process efficiently."

**🎯 Objective**:  
Create AdminJS resource for business entities with customized list view showing essential registration information.

**⛓ Dependencies**:  
- AdminJS setup with Node.js backend
- PostgreSQL database with business registration table
- Prisma ORM integration
- Staff authentication system

**✅ Acceptance Criteria**:
- List displays: business name, responsible person name, registration date, CNPJ, status, active promotions count
- Default ordering by registration date (newest first)
- Status indicators with clear visual distinction (pending/approved/rejected/suspended)
- Pagination for large lists
- Direct links to detailed view for each business
- Last activity timestamp display
- AdminJS default list interface with custom field configurations

**🧰 Technical Tasks**:
- Configure AdminJS resource for business model
- Customize list view fields and formatting
- Implement status indicators with appropriate styling
- Add computed fields for active promotions count
- Configure pagination and sorting options
- Set up proper field formatting (dates, CNPJ display)
- Add responsive design considerations for AdminJS interface

**⚙️ External Setup / Config Required**
- AdminJS installation and configuration
- Business model definition in Prisma schema
- Staff authentication middleware setup
- Database migrations for business registration table

**❗ Pending Confirmations**
- Exact field display priorities and ordering
- Status color coding preferences
- Default page size for pagination

**📝 Notes & Observations**
- AdminJS provides built-in CRUD interface reducing development time
- Focus on essential information display for MVP
- Leverages existing database schema

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 2 hours
- Realistic: 4 hours
    - AdminJS Configuration: ~1.5h
    - Custom field setup: ~1h
    - Styling and formatting: ~1h
    - Testing: ~0.5h
- Pessimistic: 6 hours
- Final PERT Estimate: 4h
```

**🖼 Wireframe Reference**
- Exists: No
- AdminJS default interface with customizations

---

### 🔹 `BIZ-MODERATION-BACK-002` – Registration Detail Review

**Summary**:  
Enable staff to access complete business registration details through AdminJS show view.

**Justification**:  
Staff need to review all submitted business information before making approval/rejection decisions.

**User Story**:  
"As a Woppa staff member, I want to view complete registration details for a business, so that I can make informed approval decisions."

**🎯 Objective**:  
Customize AdminJS show view to display all business registration information in organized sections.

**⛓ Dependencies**:  
- Business Registration List View (BIZ-MODERATION-BACK-001)
- Business database schema with all registration fields

**✅ Acceptance Criteria**:
- Show view displays all registration fields: business name, responsible person details, contact information
- Display CNPJ in proper Brazilian format (XX.XXX.XXX/XXXX-XX)
- Show complete address as stored during registration
- Include registration timestamp and any previous status changes
- Display optional fields (financial phone, Instagram) when available
- Clear section organization: Business Info, Contact Details, Administrative Info
- AdminJS default show interface with custom field groupings

**🧰 Technical Tasks**:
- Configure AdminJS show view for business resource
- Customize field groupings and sections
- Implement CNPJ formatting for display
- Configure optional field display logic
- Add proper date/time formatting
- Implement responsive layout for AdminJS show view

**⚙️ External Setup / Config Required**
- Business model definition with all registration fields
- AdminJS show view configuration

**❗ Pending Confirmations**
- Field grouping preferences and section organization
- CNPJ display format preferences
- Optional field handling strategy

**📝 Notes & Observations**
- AdminJS show view provides good foundation for detail display
- Focus on clear information presentation
- No external API integration needed - just display stored data

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 1.5 hours
- Realistic: 2.5 hours
    - AdminJS show view configuration: ~1h
    - Field formatting and grouping: ~1h
    - Testing: ~0.5h
- Pessimistic: 4 hours
- Final PERT Estimate: 2.5h
```

**🖼 Wireframe Reference**
- Exists: No
- AdminJS default show view with custom sections

---

### 🔹 `BIZ-MODERATION-BACK-003` – Business Approval Process

**Summary**:  
Implement single-click business approval through AdminJS actions with email notification.

**Justification**:  
Staff need efficient way to approve valid business registrations and notify merchants of account activation.

**User Story**:  
"As a Woppa staff member, I want to approve business registrations with one click, so that valid businesses can start using the platform."

**🎯 Objective**:  
Create AdminJS custom action for business approval with automated email notification and status change.

**⛓ Dependencies**:  
- Registration Detail Review (BIZ-MODERATION-BACK-002)
- Email service configuration
- Business status management system

**✅ Acceptance Criteria**:
- "Approve" action button available on business detail view
- Single click changes status from "pending" to "approved"
- Automatic email notification sent to business owner
- Action logs approval with staff member ID and timestamp
- Success confirmation message displayed
- Status change reflected immediately in list view
- Action only available for businesses in "pending" status

**🧰 Technical Tasks**:
- Create AdminJS custom action for approval
- Implement status change logic in backend
- Configure email notification service integration
- Add audit logging for approval actions
- Implement action permissions and validation
- Create email template for approval notification
- Add success/error handling and user feedback

**⚙️ External Setup / Config Required**
- Email service configuration (SMTP/SendGrid/etc.)
- Email template setup for approval notifications
- Audit logging database schema
- Staff permissions configuration

**❗ Pending Confirmations**
- Email template content and format
- Specific audit logging requirements
- Staff permission levels for approval actions

**📝 Notes & Observations**
- AdminJS custom actions provide clean integration
- Email notifications are critical for business communication
- Focus on simple, reliable approval process

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 3 hours
- Realistic: 5 hours
    - AdminJS custom action setup: ~1.5h
    - Email integration: ~1.5h
    - Audit logging: ~1h
    - Testing and validation: ~1h
- Pessimistic: 7 hours
- Final PERT Estimate: 5h
```

**🖼 Wireframe Reference**
- Exists: No
- AdminJS action interface with custom approval button

---

### 🔹 `BIZ-MODERATION-BACK-004` – Business Rejection Process

**Summary**:  
Implement business rejection workflow through AdminJS with mandatory comments and email notification.

**Justification**:  
Staff need to reject invalid registrations with clear feedback to help businesses understand issues.

**User Story**:  
"As a Woppa staff member, I want to reject business registrations with explanatory comments, so that businesses understand why they were rejected."

**🎯 Objective**:  
Create AdminJS custom action for business rejection with required comment field and automated email notification.

**⛓ Dependencies**:  
- Registration Detail Review (BIZ-MODERATION-BACK-002)
- Email service configuration
- Business status management system

**✅ Acceptance Criteria**:
- "Reject" action button available on business detail view
- Action opens modal/form requiring mandatory comment field
- Status changes from "pending" to "rejected" after confirmation
- Email notification sent to business with rejection reason
- Action logs rejection with staff member ID, timestamp, and comment
- Comment character limit (500 characters maximum)
- Success confirmation message displayed
- Rejected businesses remain in system for potential resubmission

**🧰 Technical Tasks**:
- Create AdminJS custom action for rejection with form
- Implement modal/form for rejection comment input
- Add comment validation and character limits
- Implement status change and comment storage logic
- Configure email notification with rejection reason
- Add audit logging for rejection actions
- Create email template for rejection notification
- Implement form validation and error handling

**⚙️ External Setup / Config Required**
- Email service configuration for rejection notifications
- Database schema for storing rejection comments
- Email template setup for rejection notifications
- Extended audit logging capabilities

**❗ Pending Confirmations**
- Rejection comment guidelines and examples
- Email template tone and content
- Character limits for rejection comments

**📝 Notes & Observations**
- AdminJS forms and modals provide good UX for comment collection
- Clear feedback helps businesses improve their applications
- Rejected businesses should be able to reapply

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

### 🔹 `BIZ-MODERATION-BACK-005` – Account Status Control

**Summary**:  
Enable staff to manage business account status through AdminJS edit interface with audit logging.

**Justification**:  
Staff need to change business account status for ongoing management and issue resolution.

**User Story**:  
"As a Woppa staff member, I want to change business account status when needed, so that I can manage active businesses and resolve issues."

**🎯 Objective**:  
Customize AdminJS edit functionality for business status management with proper logging and validation.

**⛓ Dependencies**:  
- Business Registration List View (BIZ-MODERATION-BACK-001)
- Audit logging system
- Business status definitions

**✅ Acceptance Criteria**:
- Status field editable through AdminJS edit view
- Available statuses: pending, approved, rejected, suspended, active
- Status changes logged with staff member ID and timestamp
- Dropdown selection for status values
- Validation prevents invalid status transitions
- Status change confirmation before saving
- Updated status reflected in list view immediately
- Edit action available to authorized staff only

**🧰 Technical Tasks**:
- Configure AdminJS edit view for business resource
- Implement status field as dropdown with validation
- Add status change audit logging
- Implement status transition validation rules
- Configure permissions for edit actions
- Add confirmation dialogs for status changes
- Implement real-time updates in list view
- Add proper error handling and user feedback

**⚙️ External Setup / Config Required**
- Business status enumeration in database schema
- Audit logging table for status changes
- Staff permissions configuration
- Status transition rules definition

**❗ Pending Confirmations**
- Complete list of valid business statuses
- Status transition rules and restrictions
- Staff permission levels for status changes

**📝 Notes & Observations**
- AdminJS edit interface provides good foundation
- Status management is critical for ongoing operations
- Audit trail important for accountability

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 2 hours
- Realistic: 3.5 hours
    - AdminJS edit configuration: ~1h
    - Status validation and transitions: ~1h
    - Audit logging integration: ~1h
    - Testing: ~0.5h  
- Pessimistic: 5 hours
- Final PERT Estimate: 3.5h
```

**🖼 Wireframe Reference**
- Exists: No
- AdminJS edit interface with status dropdown

---

### 🔹 `BIZ-MODERATION-BACK-006` – Manual Data Editing

**Summary**:  
Enable staff to manually edit business information through AdminJS with audit logging for exception management.

**Justification**:  
Staff need ability to correct business information errors and handle special cases that require manual intervention.

**User Story**:  
"As a Woppa staff member, I want to edit business information when necessary, so that I can correct errors and handle special cases."

**🎯 Objective**:  
Configure AdminJS edit functionality for business data with comprehensive audit logging and validation.

**⛓ Dependencies**:  
- Registration Detail Review (BIZ-MODERATION-BACK-002)
- Audit logging system
- Google Maps API integration

**✅ Acceptance Criteria**:
- Edit access to all business registration fields through AdminJS
- Real-time validation for email, phone, CNPJ formats
- Google Places integration for address editing
- All edits logged with staff member ID, timestamp, and changed fields
- Edit history visible in business detail view
- Confirmation required before saving changes
- Edit permissions restricted to authorized staff
- Original values preserved in audit trail

**🧰 Technical Tasks**:
- Configure AdminJS edit view with all business fields
- Implement field validation for edited data
- Add Google Places integration for address editing
- Create comprehensive audit logging for field changes
- Implement edit history display in detail view
- Add confirmation dialogs for data changes
- Configure field-level permissions and restrictions
- Add proper error handling and validation feedback

**⚙️ External Setup / Config Required**
- Comprehensive audit logging database schema
- Google Maps API configuration for address editing
- Field validation rules and services
- Staff permissions for data editing

**❗ Pending Confirmations**
- Which fields should be editable vs. read-only
- Audit logging detail level requirements
- Staff permission levels for different field types

**📝 Notes & Observations**
- AdminJS provides good foundation for data editing
- Comprehensive audit trail essential for data integrity
- Manual editing should be exception, not regular workflow

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 3 hours
- Realistic: 5 hours
    - AdminJS edit configuration: ~1.5h
    - Field validation setup: ~1h
    - Audit logging implementation: ~1.5h
    - Google Maps integration: ~0.5h
    - Testing: ~0.5h
- Pessimistic: 7 hours
- Final PERT Estimate: 5h
```

**🖼 Wireframe Reference**
- Exists: No
- AdminJS edit interface with custom validation

---

### 🔹 `BIZ-MODERATION-BACK-007` – Business Search and Filtering

**Summary**:  
Implement basic search and filtering functionality in AdminJS for efficient business management.

**Justification**:  
Staff need to quickly find specific businesses and filter by status for efficient registration management workflows.

**User Story**:  
"As a Woppa staff member, I want to search and filter businesses by key criteria, so that I can quickly find and manage specific registrations."

**🎯 Objective**:  
Configure AdminJS search and filtering capabilities for business resource with essential search criteria.

**⛓ Dependencies**:  
- Business Registration List View (BIZ-MODERATION-BACK-001)
- Business database schema with indexed fields

**✅ Acceptance Criteria**:
- Search functionality for business name, responsible person name, email, CNPJ
- Filter dropdown for account status (all, pending, approved, rejected, suspended)
- Filter by registration date range
- Search results highlighted in list view
- Search and filters work together (combinable)
- Clear/reset filters functionality
- Search performance optimized with database indexes
- AdminJS default search interface with custom filter options

**🧰 Technical Tasks**:
- Configure AdminJS search functionality for business resource
- Implement custom filters for status and date range
- Add database indexes for search performance
- Configure searchable fields in AdminJS
- Implement filter combinations and reset functionality
- Add search result highlighting
- Optimize search queries for performance
- Test search and filter functionality

**⚙️ External Setup / Config Required**
- Database indexes on searchable fields
- AdminJS search configuration
- Filter options configuration

**❗ Pending Confirmations**
- Priority order for search fields
- Additional filter criteria requirements
- Search result display preferences

**📝 Notes & Observations**
- AdminJS provides built-in search capabilities
- Database indexes important for search performance
- Focus on essential search criteria for MVP

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 1.5 hours
- Realistic: 2.5 hours
    - AdminJS search configuration: ~1h
    - Custom filters setup: ~1h
    - Database indexing: ~0.25h
    - Testing: ~0.25h
- Pessimistic: 4 hours
- Final PERT Estimate: 2.5h
```

**🖼 Wireframe Reference**
- Exists: No
- AdminJS search interface with custom filters

## 📊 Epic Estimation Summary

Epic totals:

- Total user stories: 7
- Stories with moderate complexity: 7
- Stories leveraging AdminJS for rapid development: 7

### Manual 3-point Estimation for Epic (PERT)

```
- Optimistic: 14.5 h
- Realistic:  25 h  
- Pessimistic: 37h
- Final PERT Estimate: 25.5 h
```
---