# 🧩 Epic: Coupon Operations Management

**KEY**: `COUPON-OPS-BACK`

---

## 📄 Functional Description
Basic coupon lifecycle management for Woppa staff to handle essential coupon operations using AdminJS. Focused on MVP functionality including coupon status management, manual redemption support for merchants, and basic stock control. Provides simple interface for coupon oversight, status changes, and merchant support with audit trails.

---

## 💻 Target Platform
This epic applies to:
- `back-office` (AdminJS interface)

---

## 🧭 Functional Scope
Main flows and interactions included in this epic:
- Coupon status monitoring and individual coupon lookup
- Manual status changes from "paid" to "redeemed" when merchants need support
- Payment status management: marking coupons as "paid by Woppa" for merchant tracking
- Basic coupon oversight and support functionality
- Basic audit logging for coupon status changes
- Simple search functionality for coupon lookup by code
- Manual association of coupons with redemptions for inconsistency resolution

---

## 🚫 Out of Scope
Explicitly excluded elements:
- System-wide coupon monitoring dashboards
- Payment dispute resolution workflows
- Fraud detection and prevention systems
- Bulk operations on multiple coupons
- Advanced analytics and performance metrics
- Automated expired coupon cleanup processes
- Merchant training and guidance systems
- Complex reporting and compliance monitoring

---

## 🖼 Wireframes Referenced in Epic
List of wireframes that apply to this epic and the stories that use them.

- No specific wireframes exist for back-office coupon management screens
- AdminJS will provide default CRUD interface with customizations

---

## 🔍 Epic-level Ambiguities

- 📐 Missing wireframe: No wireframes exist for back-office coupon management screens
- 📊 Business decision pending: Specific procedures for manual status changes
- 📋 Missing validation rules: Coupon code format and validation requirements
- 🔁 Undefined logic: Stock management procedures and merchant notification requirements

---

## 🧵 User Stories

---

### 🔹 `COUPON-OPS-BACK-001` – Coupon Status Lookup and Management

**Summary**:  
Provide AdminJS-based interface for staff to lookup individual coupons and view their current status and details.

**Justification**:  
Staff need to quickly lookup coupon information to support merchant inquiries and resolve redemption issues.

**User Story**:  
"As a Woppa staff member, I want to lookup coupon details by code, so that I can support merchants and resolve redemption issues."

**🎯 Objective**:  
Create AdminJS resource for coupons with search capability and detailed view showing complete coupon lifecycle information.

**⛓ Dependencies**:  
- AdminJS setup with Node.js backend
- PostgreSQL database with coupons table
- Prisma ORM integration
- Staff authentication system

**✅ Acceptance Criteria**:
- List displays: coupon code, offer name, business name, customer info, current status, generation date, redemption date
- Search functionality by coupon code (primary lookup method)
- Status indicators with clear visual distinction (generated, paid, redeemed, expired)
- Detailed view shows complete coupon information including associated offer and business
- Display offer expiration and coupon validity information
- Show audit trail of status changes with timestamps
- AdminJS default interface with custom field configurations

**🧰 Technical Tasks**:
- Configure AdminJS resource for coupon model
- Implement coupon code search functionality
- Customize list view fields for essential coupon information
- Set up detailed view with complete coupon lifecycle data
- Add status indicators with appropriate styling
- Integrate with related offer and business data display
- Configure pagination and sorting options

**⚙️ External Setup / Config Required**
- AdminJS installation and configuration
- Coupon model definition in Prisma schema with relationships
- Database indexes on coupon code for search performance
- Staff authentication middleware setup

**❗ Pending Confirmations**
- Coupon code format and search requirements
- Required fields for coupon lookup and display
- Integration level with offer and business information

**📝 Notes & Observations**
- AdminJS provides built-in search and CRUD interface
- Coupon code search is primary functionality for merchant support
- Focus on essential information display for quick issue resolution

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 3.5 hours
- Realistic: 5.5 hours
    - AdminJS Configuration: ~1h
    - Status indicators with visual styling: ~1h
    - Search functionality setup: ~1h
    - Relationships and detailed view: ~1.5h (coupon→offer→business→user data integration)
    - Audit trail display configuration: ~0.5h
    - Testing: ~0.5h
- Pessimistic: 8 hours
- Final PERT Estimate: 5.5h
```

**🖼 Wireframe Reference**
- Exists: No
- AdminJS default interface with coupon search

---

### 🔹 `COUPON-OPS-BACK-002` – Manual Coupon Status Changes

**Summary**:  
Enable staff to manually change coupon status from "paid" to "redeemed" when merchants need support or cannot mark redemption themselves.

**Justification**:  
Merchants may need assistance marking coupons as redeemed due to technical issues or lack of access to their panel.

**User Story**:  
"As a Woppa staff member, I want to manually mark coupons as redeemed, so that I can support merchants who cannot access their panel or have technical issues."

**🎯 Objective**:  
Create AdminJS custom action to change coupon status with proper validation and audit logging.

**⛓ Dependencies**:  
- Coupon Status Lookup (COUPON-OPS-BACK-001)
- Audit logging system

**✅ Acceptance Criteria**:
- "Mark as Redeemed" action button available on coupon detail view
- Action only available for coupons in "paid" status
- Single click changes status from "paid" to "redeemed" with timestamp
- Action requires mandatory comment field explaining reason for manual change
- Action logs change with staff member ID, timestamp, and justification comment
- Success confirmation message displayed
- Status change reflected immediately in coupon list and merchant panel
- Automatic stock reduction if offer has stock control configured

**🧰 Technical Tasks**:
- Create AdminJS custom action for status change
- Implement status validation (only paid → redeemed allowed)
- Add mandatory comment field for justification
- Implement status change logic with timestamp updates
- Add audit logging for manual status changes
- Integrate with stock management system for automatic reduction
- Add success/error handling and user feedback

**⚙️ External Setup / Config Required**
- Audit logging database schema for status changes
- Stock management integration for automatic reduction
- Validation rules for status transitions

**❗ Pending Confirmations**
- Specific validation rules for manual status changes
- Required justification comment guidelines
- Stock reduction behavior for manual redemptions

**📝 Notes & Observations**
- Critical functionality for merchant support
- Proper audit trail essential for accountability
- Integration with existing merchant panel redemption system

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 4 hours
- Realistic: 6.5 hours
    - AdminJS custom action with comment form: ~2h (modal, validation, UX)
    - Status validation logic: ~1h
    - Stock integration with edge cases: ~1.5h (stock tracking, error handling, rollback scenarios)
    - Audit logging integration: ~1h
    - Testing and validation: ~1h (status transitions, stock scenarios, error cases)
- Pessimistic: 9 hours
- Final PERT Estimate: 6.5h
```

**🖼 Wireframe Reference**
- Exists: No
- AdminJS action interface with status change form

---

### 🔹 `COUPON-OPS-BACK-003` – Manual Coupon-Redemption Association

**Summary**:  
Enable staff to manually associate coupon codes with redemptions when there are system inconsistencies or tracking issues.

**Justification**:  
System inconsistencies may occur where coupons and redemptions exist but are not properly linked, requiring manual intervention to resolve tracking issues.

**User Story**:  
"As a Woppa staff member, I want to manually associate coupon codes with redemptions, so that I can resolve tracking inconsistencies and ensure accurate coupon lifecycle management."

**🎯 Objective**:  
Provide interface to manually link coupon codes with redemption records when automatic tracking fails or inconsistencies occur.

**⛓ Dependencies**:  
- Coupon Status Lookup (COUPON-OPS-BACK-001)
- Manual Coupon Status Changes (COUPON-OPS-BACK-002)
- Audit logging system

**✅ Acceptance Criteria**:
- "Associate with Redemption" action available on coupon detail view
- Action only available when coupon status indicates inconsistency or tracking issue
- Interface to search and select matching redemption records
- Mandatory comment field explaining reason for manual association
- Action logs association with staff member ID, timestamp, and justification
- Both coupon and redemption records updated to reflect proper linkage
- Success confirmation message displayed
- Audit trail shows complete history of manual associations

**🧰 Technical Tasks**:
- Create AdminJS custom action for manual association (reuses existing custom action infrastructure)
- Implement redemption record search and selection interface
- Add validation logic for coupon-redemption compatibility
- Implement association logic with proper database updates
- Add mandatory comment field for justification (reuses existing comment system)
- Add audit logging for manual associations (reuses existing audit system)
- Add success/error handling and user feedback

**⚙️ External Setup / Config Required**
- Database schema updates for manual association tracking
- Redemption record access and search functionality
- Audit logging database schema (already configured)

**❗ Pending Confirmations**
- Criteria for identifying coupons eligible for manual association
- Redemption record search and matching requirements
- Validation rules for coupon-redemption compatibility

**📝 Notes & Observations**
- Exception handling functionality for system inconsistencies
- Reuses existing custom action and audit infrastructure
- Important for maintaining data integrity and merchant trust

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 4 hours
- Realistic: 7.5 hours
    - AdminJS custom action: ~1h (reuses existing infrastructure)
    - Redemption search interface: ~4h (search by multiple criteria, pagination, selection UI)
    - Association logic and validation: ~1.5h (compatibility checks, database updates, error handling)
    - Audit logging and testing: ~1h (complex scenarios, validation testing)
- Pessimistic: 12 hours
- Final PERT Estimate: 7.7h
```

**🖼 Wireframe Reference**
- Exists: No
- AdminJS action interface with redemption search and association

---

### 🔹 `COUPON-OPS-BACK-004` – Payment Status Management

**Summary**:  
Enable staff to mark coupons as "paid by Woppa" to track which codes have been financially processed for merchant payment calculations.

**Justification**:  
Merchants need visibility into which codes have been paid by Woppa versus pending payment, as specified in requirements for "códigos ya pagados por WOPPA" and "códigos pendientes de pago" tracking.

**User Story**:  
"As a Woppa staff member, I want to mark coupons as paid by Woppa, so that merchants can track which codes have been financially processed and calculate pending payments accurately."

**🎯 Objective**:  
Create AdminJS custom action to mark coupons as "paid by Woppa" with proper validation, batch processing capabilities, and audit logging for payment tracking.

**⛓ Dependencies**:
- Coupon Status Lookup (COUPON-OPS-BACK-001)
- Manual Coupon Status Changes (COUPON-OPS-BACK-002)
- Audit logging system

**✅ Acceptance Criteria**:
- "Mark as Paid by Woppa" action button available on coupon detail view
- Action only available for redeemed coupons that haven't been marked as paid
- Single click changes payment status to "paid by Woppa" with timestamp
- Action requires mandatory comment field for payment batch reference or justification
- Action logs payment status change with staff member ID, timestamp, and batch reference
- Success confirmation message displayed
- Payment status reflected immediately in merchant sales tracking
- Optional batch selection functionality for processing multiple coupons simultaneously

**🧰 Technical Tasks**:
- Create AdminJS custom action for payment status marking (reuses existing infrastructure)
- Implement payment status validation (only redeemed → paid allowed)
- Add mandatory comment field for batch reference/justification
- Implement payment status change logic with timestamp updates
- Add audit logging for payment status changes (reuses existing audit system)
- Integrate with merchant sales tracking system for real-time updates
- Add success/error handling and user feedback
- Optional: Add batch processing interface for multiple coupons

**⚙️ External Setup / Config Required**
- Database schema extension for payment status tracking
- Audit logging database schema (already configured)
- Integration with merchant sales tracking system
- Payment batch reference system (optional)

**❗ Pending Confirmations**
- Payment processing workflow and batch reference requirements
- Integration timing with merchant payment calculations
- Bulk payment marking requirements vs. individual processing

**📝 Notes & Observations**
- Critical for accurate merchant payment tracking and financial reconciliation
- Reuses existing custom action and audit infrastructure significantly reducing development time
- Essential for transparency in merchant-Woppa financial relationship

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 2.5 hours
- Realistic: 4.5 hours
    - AdminJS custom action: ~0.5h (reuses existing infrastructure)
    - Payment status validation logic: ~1h
    - Integration with merchant sales tracking: ~1.5h (real-time updates, data sync)
    - Audit logging and testing: ~1.5h (payment scenarios, validation testing)
- Pessimistic: 7 hours
- Final PERT Estimate: 4.5h
```

**🖼 Wireframe Reference**
- Exists: No
- AdminJS action interface with payment status marking

---

## 📊 Epic Estimation Summary

Epic totals:

- Total user stories: 4
- Stories with moderate complexity: 4
- Stories leveraging AdminJS and existing infrastructure: 4

### Manual 3-point Estimation for Epic (PERT)

```
- Optimistic: 14h
- Realistic: 24h  
- Pessimistic: 36h
- Final PERT Estimate: 24.3h
```
---