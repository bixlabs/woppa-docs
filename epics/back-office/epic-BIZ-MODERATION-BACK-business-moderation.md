# Epic: Business Moderation
**KEY**: `BIZ-MODERATION-BACK`  
**Platform**: Back-Office (Woppa Staff)  
**Status**: Defined  

## Overview
Basic administrative panel for Woppa staff to validate business registrations and manage account statuses. Focused on essential MVP functionality with simple operational workflows and basic audit trails for business onboarding management.

## User Stories

### Business Registration Management

• **Story 1: Business Registration List**  
  *Description:* Woppa staff view list of all registered businesses showing: business name, responsible person name, registration date, CNPJ, account status (pending, approved, rejected), and number of active promotions. List ordered by registration date.

• **Story 2: Registration Review**  
  *Description:* Staff access complete registration details for review including all submitted information: business name, responsible person, contact information (email, commercial phone, optional financial phone), CNPJ, address with Google Maps verification, and registration timestamp.

• **Story 3: Business Approval**  
  *Description:* Staff approve business registrations with single-click approval that changes status to "approved", sends email notification to merchant confirming account activation, and enables business access to promotion management features.

• **Story 4: Business Rejection**  
  *Description:* Staff reject business registrations with mandatory comment field explaining rejection reasons. System sends email notification to merchant with feedback and maintains registration record for potential future resubmission.

### Account Status Management

• **Story 5: Account Status Control**  
  *Description:* Staff manage business account status with ability to change status between approved/suspended/active states. Status changes are logged with timestamp and staff member identification for basic audit trail.

• **Story 6: Manual Data Editing**  
  *Description:* Staff manually edit business information when necessary including contact details, address corrections, and other basic business data. All edits logged with staff identification and timestamp for exception management.

### Basic Search and Filtering

• **Story 7: Business Search**  
  *Description:* Staff search businesses by business name, responsible person name, CNPJ, or email. Basic filtering by account status (pending, approved, rejected) to facilitate registration management workflows.

## Technical Requirements

- Staff authentication and access control
- Business registration database integration  
- Email notification system for status changes
- Basic audit logging for status changes and edits
- Simple search and filtering functionality
- Integration with Google Maps API for address verification
- CNPJ format validation

## Acceptance Criteria Summary

- Only authorized staff can access business moderation panel
- All registration approval/rejection decisions logged with timestamp and staff ID
- Email notifications sent automatically for status changes
- Search and filtering provide accurate results for business management
- Manual edits tracked for audit purposes
- Address verification integrated with Google Maps API

## Dependencies

- Business Authentication epic (web-panel registration system)
- Staff user management and authentication system
- Email service configuration
- Google Maps API integration