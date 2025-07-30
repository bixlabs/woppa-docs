# Epic: Offer Moderation
**KEY**: `OFFER-MODERATION-BACK`  
**Platform**: Back-Office (Woppa Staff)  
**Status**: Defined  

## Overview
Quality assurance system for offer validation with 12-hour SLA. Enables Woppa staff to review, approve, reject, or request adjustments to submitted offers. Includes mandatory comment fields for feedback, automatic email notifications, and direct publication to mobile app upon approval.

## User Stories

### Offer Review Queue

• **Story 1: Pending Offers Queue**  
  *Description:* Woppa staff view queue of offers pending review prioritized by submission time to meet 12-hour SLA. Queue shows offer name, merchant name, category, submission date, time remaining for SLA, and current status with visual indicators for urgency.

• **Story 2: Offer Detail Review**  
  *Description:* Staff access complete offer details for thorough review including all form fields, uploaded images, location verification, pricing, description, expiration date, and merchant information. Interface optimized for quick quality assessment.

• **Story 3: SLA Management**  
  *Description:* System tracks 12-hour SLA for offer review with visual indicators for offers approaching deadline, automatic escalation for overdue reviews, and SLA performance metrics for staff management and process optimization.

### Offer Decision Making

• **Story 4: Offer Approval Process**  
  *Description:* Staff approve offers that meet quality standards with single-click approval that changes status to "approved", publishes offer to mobile app immediately, sends confirmation email to merchant, and logs approval with staff identification and timestamp.

• **Story 5: Offer Rejection Process**  
  *Description:* Staff reject offers that don't meet standards with mandatory comment field explaining specific rejection reasons. System sends detailed feedback email to merchant, maintains offer in merchant's account for potential resubmission, and logs rejection with comprehensive reasoning.

• **Story 6: Request Adjustments Process**  
  *Description:* Staff request specific adjustments when offers need modifications with detailed comment field specifying required changes. System changes status to "needs adjustments", sends detailed feedback email to merchant, allows merchant to edit and resubmit, and maintains review history.

### Quality Control

• **Story 7: Image Quality Validation**  
  *Description:* Staff verify uploaded images meet quality standards including good lighting, clear product visibility, appropriate composition, and brand compliance. System provides image enhancement tools or rejection guidance for substandard images.

• **Story 8: Content Guidelines Enforcement**  
  *Description:* Staff enforce content guidelines including appropriate product descriptions, accurate pricing, valid conditions, proper categorization, and compliance with platform policies. Guidelines accessible during review for consistency.

• **Story 9: Offer Information Verification**  
  *Description:* Staff verify offer information accuracy including price validation, location verification, expiration date reasonableness, category/subcategory appropriateness, and contact information accuracy through cross-referencing with merchant data.

### Batch Operations & Efficiency

• **Story 10: Bulk Offer Operations**  
  *Description:* Staff perform bulk operations on multiple offers including bulk approval of similar offers, bulk rejection with common reasons, batch status changes, and streamlined processing during high-volume periods while maintaining quality standards.

• **Story 11: Quick Action Templates**  
  *Description:* Pre-defined comment templates for common rejection reasons and adjustment requests including image quality issues, pricing problems, description improvements, and categorization corrections. Templates save time while ensuring comprehensive feedback.

• **Story 12: Offer Comparison Tools**  
  *Description:* Staff compare similar offers from same merchant or category to ensure consistency in approval decisions, identify patterns in rejections, and maintain fair and uniform quality standards across all merchants.

### Analytics & Process Improvement

• **Story 13: Review Performance Analytics**  
  *Description:* Staff and managers view analytics on review performance including SLA compliance rates, approval/rejection ratios, common rejection reasons, staff productivity metrics, and merchant satisfaction scores to optimize the review process.

• **Story 14: Merchant Quality Tracking**  
  *Description:* System tracks merchant quality over time including approval rates by merchant, common issues by merchant, improvement trends, and quality scores to inform merchant support and partnership decisions.

• **Story 15: Review History & Appeals**  
  *Description:* Comprehensive review history for each offer including all decisions, comments, staff actions, and timestamps. Support for merchant appeals process with escalation to senior staff and decision override capabilities.

### Communication & Notifications

• **Story 16: Automated Email Notifications**  
  *Description:* System automatically sends email notifications to merchants for all status changes including approval confirmations, rejection explanations, adjustment requests, and resubmission confirmations. Emails include relevant details and next steps.

• **Story 17: Staff Communication Tools**  
  *Description:* Internal communication tools for staff including discussion threads on complex offers, escalation to senior reviewers, knowledge sharing for edge cases, and collaborative decision-making on policy questions.

## Technical Requirements

- Role-based access control for staff authentication
- 12-hour SLA tracking and alerting system
- Email notification automation
- Image viewing and basic editing tools
- Bulk operation processing capabilities
- Review analytics and reporting engine
- Integration with mobile app publication system
- Audit logging for all review decisions
- Comment template management system

## Acceptance Criteria Summary

- 12-hour SLA maintained for all offer reviews
- All review decisions include appropriate feedback comments
- Email notifications sent automatically for status changes
- Bulk operations maintain quality standards and proper logging
- Review analytics provide actionable insights for improvement
- Image quality validation prevents substandard offers
- Appeal process allows merchant feedback and corrections
- System integrates seamlessly with mobile app publication

## Dependencies

- Offer Management epic (web-panel offer creation system)
- Business Moderation epic (approved merchants only)
- Mobile app integration for offer publication
- Email service configuration
- Staff user management and authentication system
- Image storage and processing service