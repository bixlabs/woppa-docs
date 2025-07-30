# Epic: Business Moderation
**KEY**: `BIZ-MODERATION-BACK`  
**Platform**: Back-Office (Woppa Staff)  
**Status**: Defined  

## Overview
Administrative panel for Woppa staff to validate and manage business registrations. Includes approval/rejection workflows, account status management, manual data editing capabilities, and monitoring of business activity. Provides comprehensive oversight of the business onboarding process with audit trails.

## User Stories

### Business Registration Review

• **Story 1: Business Registration Queue**  
  *Description:* Woppa staff view queue of pending business registrations with key information: business name, responsible person, registration date, location, CNPJ, and current status. Queue prioritized by submission date with filtering and search capabilities.

• **Story 2: Registration Detail Review**  
  *Description:* Staff access complete registration details for thorough review including all submitted information, Google Maps location verification, CNPJ validation status, contact information, and any uploaded documents or verification materials.

• **Story 3: Business Approval Process**  
  *Description:* Staff approve business registrations after verification with single-click approval that changes status to "approved", sends email notification to merchant, enables platform access, and logs approval with staff member identification and timestamp.

• **Story 4: Business Rejection Process**  
  *Description:* Staff reject business registrations with mandatory comment field explaining rejection reasons. System sends email notification to merchant with feedback, maintains registration in system for potential resubmission, and logs rejection with detailed reasoning.

### Account Management

• **Story 5: Business Account Status Management**  
  *Description:* Staff manage ongoing business account status including suspend/reactivate accounts, view account activity history, modify account settings when necessary, and track business performance metrics to inform status decisions.

• **Story 6: Manual Data Editing**  
  *Description:* Staff manually edit business information when necessary including contact details, address corrections, CNPJ updates, and other critical business data. All edits logged with staff member identification and reasoning for audit trail.

• **Story 7: Business Activity Monitoring**  
  *Description:* Staff monitor business activity including offer creation frequency, sales performance, customer complaints, and platform usage patterns. Activity data helps inform account status decisions and support needs.

### Bulk Operations & Management

• **Story 8: Bulk Business Operations**  
  *Description:* Staff perform bulk operations on multiple businesses including bulk approval of verified businesses, bulk status changes, bulk communication sending, and batch processing of registration applications during high-volume periods.

• **Story 9: Business Search & Filtering**  
  *Description:* Comprehensive search and filtering system allowing staff to find businesses by name, CNPJ, status, registration date, location, activity level, and other criteria. Supports complex queries and saved search filters.

• **Story 10: Registration Analytics**  
  *Description:* Staff view analytics on business registration trends including approval rates, rejection reasons, geographic distribution, processing times, and staff performance metrics to optimize the onboarding process.

### Communication & Support

• **Story 11: Business Communication**  
  *Description:* Staff communicate directly with businesses through integrated messaging system including email templates for common scenarios, custom message composition, automatic status update notifications, and communication history tracking.

• **Story 12: Registration Issue Resolution**  
  *Description:* Staff resolve registration issues including CNPJ validation problems, address verification issues, incomplete documentation, and technical problems. System tracks issue resolution and common problem patterns.

• **Story 13: Support Request Management**  
  *Description:* Staff manage support requests from businesses including WhatsApp Business integration for direct communication, ticket tracking system, escalation procedures, and resolution tracking with performance metrics.

### Audit & Compliance

• **Story 14: Audit Trail Management**  
  *Description:* Comprehensive audit logging of all staff actions including registration decisions, data modifications, status changes, and communication activities. Audit trail includes timestamps, staff identification, and detailed action descriptions.

• **Story 15: Compliance Monitoring**  
  *Description:* Staff monitor compliance with registration requirements including CNPJ validation, address verification, document completeness, and regulatory compliance. System flags potential compliance issues for review.

• **Story 16: Reporting & Documentation**  
  *Description:* Generate reports on business registration activities including processing times, approval rates, common rejection reasons, staff performance, and business onboarding trends for management review and process improvement.

## Technical Requirements

- Role-based access control for staff authentication
- Business registration database integration
- Email notification system
- Audit logging and trail management
- Search and filtering capabilities
- Bulk operation processing
- Integration with Google Maps API for verification
- CNPJ validation system integration
- Reporting and analytics engine

## Acceptance Criteria Summary

- Only authorized staff can access business moderation panel
- All registration decisions properly logged with audit trail
- Email notifications sent automatically for status changes
- Bulk operations process efficiently without system impact
- Search and filtering provide accurate, fast results
- Audit trail captures all staff actions comprehensively
- Compliance monitoring flags issues accurately
- Reports provide actionable insights for process improvement

## Dependencies

- Business Authentication epic (web-panel registration system)
- Staff user management and authentication system
- Email service configuration
- Google Maps API integration
- CNPJ validation service
- Audit logging infrastructure