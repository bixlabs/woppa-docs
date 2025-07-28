# 🧩 Epic: Offer Redemption

**KEY**: `REDEEM-MOB`

---

## 📄 Functional Description
This epic enables users to redeem offers by completing the payment process and receiving unique redemption codes. It covers the complete flow from initiating an offer redemption through displaying the final coupon code that can be presented at the business location.

---

## 💻 Target Platform
This epic applies to:
- `mobile`

---

## 🧭 Functional Scope
Main flows and interactions included in this epic:
- Display detailed offer information with redemption option and error messaging
- Initiate offer redemption with authentication validation
- Process payment through Mercado Pago Checkout Pro
- Handle payment verification and status within offer code display
- Handle payment cancellation with redirection to offer details
- Generate and display unique redemption codes with integrated status verification
- Send redemption code via email as backup access method
- Navigate to directions or explore more offers

---

## 🚫 Out of Scope
Explicitly excluded elements:
- User authentication flows (handled by Authentication epic)
- Offer browsing and discovery (handled by Explore Offers epic)
- Purchase history management (handled by Account Management epic)
- Business validation of redemption codes (handled by merchant panel)
- Payment method management and selection (MVP only supports Mercado Pago)

---

## 🖼 Wireframes Referenced in Epic
List of wireframes that apply to this epic and the stories that use them.

- `woppa-wireframe-3-detalle-oferta.png` → used in: REDEEM-MOB-001
- `woppa-wireframe-5-obtained-cupon.png` → used in: REDEEM-MOB-006
- (no wireframes available for REDEEM-MOB-003, REDEEM-MOB-004, REDEEM-MOB-005 - context preservation, payment processing and cancellation handling screens)

---

## 🔍 Epic-level Ambiguities

- 📐 Missing wireframe: Payment verification loading states within offer code screen
- 🔁 Undefined logic: Payment timeout handling and retry mechanisms during verification
- 📋 Missing validation rules: Maximum redemptions per user per offer
- 🧩 External dependency unclear: Mercado Pago webhook reliability and error scenarios
- ⚠️ Uncovered edge case: User closes app during payment verification process
- 📊 Business decision pending: Criteria for redirecting to offer details vs showing error in offer code screen
- 🔀 Navigation ambiguity: Handling of user cancellation vs payment failure routing

---

## 🧵 User Stories

---

### 🔹 `REDEEM-MOB-001` – Display Offer Details

**Summary**:  
Present comprehensive offer information with clear redemption call-to-action.

**Justification**:  
Users need complete offer details to make informed redemption decisions.

**User Story**:  
"As a consumer, I want to view detailed offer information including business location, conditions, and pricing, so that I can decide whether to redeem the offer."

**🎯 Objective**:  
Display all relevant offer information with prominent redemption button.

**⛓ Dependencies**:  
- Offer data from backend API
- User location for distance calculation
- Category and subcategory mapping

**✅ Acceptance Criteria**:
- Display offer image, business name, and category
- Show offer conditions (timing, restrictions, validity)
- Display "1+1" benefit badge clearly
- Include business address and map integration
- Show "Obtener oferta" button prominently
- Handle missing images with appropriate placeholders
- Display error message when user returns from cancelled/failed payment
- Clear error state when user navigates away or retries

**🧰 Technical Tasks**:
- Implement offer details screen layout
- Integrate with offers API endpoint
- Add image loading with error handling
- Implement Google Maps integration for location (static map)
- Add responsive design for different screen sizes
- Implement share functionality (if required)
- Add error message display component for payment failures
- Implement error state management and clearing logic

**⚙️ External Setup / Config Required**
- Google Maps API key configuration
- Image CDN access for offer photos

**❗ Pending Confirmations**
- Final button text ("Obtener oferta" vs "Quiero la oferta")
- Social media links display requirements

**📝 Notes & Observations**
- Wireframe shows static map but requirements mention Google Maps integration
- Instagram link mentioned in requirements but not visible in wireframe
- Category tags design needs clarification

**🖼 Wireframe Reference**
- Exists: Yes
- Filename: `woppa-wireframe-3-detalle-oferta.png`

**📊 PERT Estimation**:
- **Optimistic**: ___ hours
  - _Comments: [Space for optimistic scenario assumptions]_
- **Realistic**: ___ hours
  - _Comments: [Space for realistic scenario assumptions]_
- **Pessimistic**: ___ hours
  - _Comments: [Space for pessimistic scenario assumptions]_

---

### 🔹 `REDEEM-MOB-002` – Initiate Offer Redemption

**Summary**:  
Handle the redemption initiation with authentication validation and offer availability checks, delegating context preservation to REDEEM-MOB-003.

**Justification**:  
Users need a clear decision point that validates prerequisites (authentication, offer availability) before proceeding to payment or redirecting to authentication flows.

**User Story**:  
"As a consumer, I want to start redeeming an offer by clicking the redemption button, so that the system can validate my eligibility and guide me to the appropriate next step."

**🎯 Objective**:  
Clean validation and routing logic that determines the next step in the redemption flow based on user authentication status and offer availability.

**⛓ Dependencies**:  
- Authentication system status check
- Offer availability validation
- Navigation system to registration/login flows
- Centralized payment function (proceedToPayment)

**✅ Acceptance Criteria**:
- Users can browse offers and view details without authentication
- Authentication is required specifically when clicking "Obtener oferta" button
- Validate user authentication status before redemption initiation
- Check offer availability and expiration
- If user not authenticated: delegate to REDEEM-MOB-003 for context preservation and auth flow
- If user authenticated but email not verified: delegate to REDEEM-MOB-003 for email verification flow
- If user fully authenticated: call centralized proceedToPayment function directly
- Handle offer unavailability with appropriate messaging
- Prevent multiple simultaneous redemptions
- Clear loading states during validation

**🧰 Technical Tasks**:
- Implement authentication status check
- Add offer availability validation
- Create decision logic for routing (auth needed, email verification needed, or proceed to payment)
- Integrate with centralized proceedToPayment function
- Add delegation to REDEEM-MOB-003 when context preservation needed
- Implement loading states during validation
- Add error handling for unavailable offers
- Create offer reservation mechanism (if needed)

**⚙️ External Setup / Config Required**
- Authentication service integration
- Session management configuration

**❗ Pending Confirmations**
- Offer reservation mechanism needed during payment process?
- Maximum redemptions per user per offer?

**📝 Notes & Observations**
- Clean separation: this story focuses on validation and routing decisions
- Context preservation complexity handled by REDEEM-MOB-003
- Uses centralized proceedToPayment function to avoid logic duplication

**🖼 Wireframe Reference**
- Exists: No (logic/flow step)

**📊 PERT Estimation**:
- **Optimistic**: ___ hours
  - _Comments: [Space for optimistic scenario assumptions]_
- **Realistic**: ___ hours
  - _Comments: [Space for realistic scenario assumptions]_
- **Pessimistic**: ___ hours
  - _Comments: [Space for pessimistic scenario assumptions]_

---

### 🔹 `REDEEM-MOB-003` – Cross-Authentication Context Preservation

**Summary**:  
Handle context preservation and navigation redirection when users need authentication or email verification during redemption flow, using a centralized payment function approach.

**Justification**:  
Users should seamlessly return to their intended redemption after completing required authentication steps without losing progress or creating duplicate payment logic.

**User Story**:  
"As a user who gets interrupted by authentication during offer redemption, I want to automatically return to my payment flow after completing auth, so that I don't lose my progress and can complete my purchase smoothly."

**🎯 Objective**:  
Seamless context preservation and restoration across authentication boundaries using simple navigation patterns and centralized payment logic.

**⛓ Dependencies**:  
- Authentication flows (AUTH-MOB epic)
- Email verification flow (AUTH-MOB-004)
- Navigation system
- Centralized payment function (proceedToPayment)

**✅ Acceptance Criteria**:
- Preserve offer context when redirecting to authentication flows
- Preserve offer context when redirecting to email verification
- Use navigation params for context preservation (MVP approach)
- After successful authentication, call centralized proceedToPayment function
- After successful email verification, call centralized proceedToPayment function
- Handle context loss gracefully with fallback navigation to offer details
- Avoid duplicating payment preparation logic across multiple components
- Support timeout/expiration of context preservation
- Clear context after successful payment completion or explicit cancellation

**🧰 Technical Tasks**:
- Implement navigation parameter passing for offer context
- Create centralized proceedToPayment function shared with REDEEM-MOB-002
- Add context restoration logic in authentication success flows
- Add context restoration logic in email verification success flows
- Implement graceful fallbacks for lost context scenarios
- Create context validation before restoration
- Add context cleanup after payment completion
- Handle navigation edge cases (app backgrounding, network issues)

**⚙️ External Setup / Config Required**
- Navigation parameter structure definition
- Context timeout configuration
- Error handling strategies for context loss

**❗ Pending Confirmations**
- Context preservation timeout duration (suggested: 30 minutes)
- Fallback behavior when context is lost or expired
- Error messaging for failed context restoration

**📝 Notes & Observations**
- Uses simple navigation params approach suitable for MVP
- Centralizes payment logic to avoid duplication between REDEEM-MOB-002 and this story
- Graceful degradation ensures users aren't completely blocked
- Context loss is rare but handled appropriately

**🖼 Wireframe Reference**
- Exists: No (cross-flow integration logic)

**📊 PERT Estimation**:
- **Optimistic**: ___ hours
  - _Comments: [Space for optimistic scenario assumptions]_
- **Realistic**: ___ hours
  - _Comments: [Space for realistic scenario assumptions]_
- **Pessimistic**: ___ hours
  - _Comments: [Space for pessimistic scenario assumptions]_

---

### 🔹 `REDEEM-MOB-004` – Process Payment via Mercado Pago

**Summary**:  
Generate payment preference and redirect user to Mercado Pago Checkout Pro.

**Justification**:  
Payment is required before redemption code delivery per business decisions.

**User Story**:  
"As a consumer, I want to complete payment for my selected offer through Mercado Pago, so that I can receive my redemption code."

**🎯 Objective**:  
Successfully redirect user to Mercado Pago with proper payment preference and handle return flow.

**⛓ Dependencies**:  
- Mercado Pago account and API credentials
- Backend payment preference generation
- User account information for payment

**✅ Acceptance Criteria**:
- Generate Mercado Pago payment preference with offer details
- Redirect user to Mercado Pago Checkout Pro
- Include proper success/failure return URLs
- Handle user cancellation of payment
- Preserve offer context throughout payment flow
- Display loading state during preference generation

**🧰 Technical Tasks**:
- Integrate Mercado Pago SDK
- Implement payment preference creation API
- Create redirect mechanism to Mercado Pago
- Implement return URL handling
- Add error handling for preference generation failures
- Create payment session tracking

**⚙️ External Setup / Config Required**
- Mercado Pago developer account setup
- API credentials configuration (public/private keys)
- Webhook URLs configuration in Mercado Pago dashboard
- Return URLs configuration

**❗ Pending Confirmations**
- Payment preference item description format
- User data requirements for payment processing
- Handling of multiple payment methods within Mercado Pago

**📝 Notes & Observations**
- No wireframe available - UI design needed for payment initiation screen
- Business decision specifies Mercado Pago Checkout Pro specifically
- Need to handle network failures during preference generation

**📉 PERT Estimation Candidate**

```
PERT:
- Optimistic: Complex external API integration, missing wireframe
- Realistic: 
- Pessimistic: 
Justification: Missing wireframe and external payment system integration complexity
```

**🖼 Wireframe Reference**
- Exists: No
- Note: UI flow simplification decision means no specific payment wireframes

**📊 PERT Estimation**:
- **Optimistic**: ___ hours
  - _Comments: [Space for optimistic scenario assumptions]_
- **Realistic**: ___ hours
  - _Comments: [Space for realistic scenario assumptions]_
- **Pessimistic**: ___ hours
  - _Comments: [Space for pessimistic scenario assumptions]_

---

### 🔹 `REDEEM-MOB-005` – Handle Payment Cancellation

**Summary**:  
Handle user-initiated payment cancellations with redirection to offer details and error messaging.

**Justification**:  
User cancellations need clear communication and easy path to retry payment.

**User Story**:  
"As a consumer, I want to be redirected back to the offer details with clear messaging when I cancel my payment, so that I can retry or understand what happened."

**🎯 Objective**:  
Redirect cancelled payments to offer details screen with appropriate error messaging.

**⛓ Dependencies**:  
- Mercado Pago cancellation detection
- Navigation system to offer details
- Error messaging system

**✅ Acceptance Criteria**:
- Detect user-initiated payment cancellation from Mercado Pago
- Redirect user to offer details screen (RED-001)
- Display cancellation error message on offer details
- Preserve offer context and allow retry
- Clear error state on subsequent redemption attempts
- Log cancellation events for analytics

**🧰 Technical Tasks**:
- Implement cancellation detection from Mercado Pago return URLs
- Create navigation logic back to offer details
- Integrate error messaging with offer details screen
- Add cancellation event logging
- Implement error state clearing mechanism
- Create retry flow preservation

**⚙️ External Setup / Config Required**
- Mercado Pago cancellation URL configuration
- Error message localization for cancellations
- Analytics event tracking setup

**❗ Pending Confirmations**
- Specific cancellation error message content
- Cancellation detection criteria vs other payment failures
- Analytics tracking requirements for cancellations

**📝 Notes & Observations**
- Simpler flow focusing on user-initiated cancellations only
- Integrates with RED-001 for error display
- Other payment failures handled in REDEEM-MOB-006 (offer code screen)

**🖼 Wireframe Reference**
- Exists: Yes (uses offer details wireframe with error state)
- Filename: `woppa-wireframe-3-detalle-oferta.png`

**📊 PERT Estimation**:
- **Optimistic**: ___ hours
  - _Comments: [Space for optimistic scenario assumptions]_
- **Realistic**: ___ hours
  - _Comments: [Space for realistic scenario assumptions]_
- **Pessimistic**: ___ hours
  - _Comments: [Space for pessimistic scenario assumptions]_

---

### 🔹 `REDEEM-MOB-006` – Display Redemption Code with Payment Verification

**Summary**:  
Handle payment verification, display loading states, and show redemption code or error messages based on payment status.

**Justification**:  
Users need immediate feedback on payment status with seamless transition to code display or error handling.

**User Story**:  
"As a consumer, I want to see my payment being processed and receive my redemption code immediately when confirmed, or clear error messaging if payment fails, so that I know the status of my purchase."

**🎯 Objective**:  
Verify payment status with backend, display appropriate loading states, and present redemption code or error messages.

**⛓ Dependencies**:  
- Mercado Pago webhook system
- Backend payment status API and verification system
- Backend code generation system
- Email service integration for code delivery
- Business information for the offer
- Real-time status polling mechanism

**✅ Acceptance Criteria**:
- Display loading state immediately when arriving from Mercado Pago
- Poll backend for payment status at appropriate intervals
- Handle webhook delays gracefully with timeout mechanisms
- Generate unique redemption code upon payment confirmation
- Send redemption code automatically via email upon payment confirmation
- Include offer details, business information, and usage instructions in email
- Display code prominently in large, readable format with business info
- Show business name and offer type (1+1)
- Include usage instructions in friendly language
- Display code status (active, used, expired)
- Show celebration message for successful purchase
- Display error message for payment failures (non-cancellation)
- Include close/dismiss button
- Handle code generation failures gracefully
- Handle email delivery failures gracefully (log but don't block code display)
- Prevent multiple polling requests

**🧰 Technical Tasks**:
- Implement payment status polling mechanism with exponential backoff
- Create payment verification loading UI state
- Add timeout handling with configurable limits
- Implement code generation algorithm and linking system
- Integrate email service for automatic code delivery
- Create email template with offer details and business information
- Implement email delivery error handling and logging
- Create code display screen layout with multiple states (loading, success, error)
- Add code status indicator system
- Create celebration UI elements for successful payments
- Implement error messaging for payment failures
- Add accessibility features for code reading
- Create screen capture prevention (if required)
- Implement code copying functionality (if needed)
- Add automatic navigation and state management
- Create payment status state management
- Implement error logging and tracking

**⚙️ External Setup / Config Required**
- Backend webhook handling setup
- Email service configuration (SMTP or transactional email provider)
- Email template design and content localization
- Polling interval configuration
- Timeout threshold configuration
- Code generation service configuration
- Database schema for code storage
- Code display formatting rules
- Status checking API integration
- Error tracking system integration

**❗ Pending Confirmations**
- Polling frequency and timeout duration
- Code format and length requirements
- Email template design and content structure
- Email delivery failure retry policy
- Final celebration message wording
- Brand mascot integration requirements
- Code copying/sharing functionality
- Error message content for payment failures
- Code generation failure handling approach

**📝 Notes & Observations**
- Wireframe shows code display pattern but not verification loading states
- Critical for user experience during webhook processing delays
- Important emotional touchpoint for user satisfaction
- Need to handle edge cases like app backgrounding during verification
- Requirements mention potential brand mascot integration
- Must ensure atomic transaction between payment and code generation
- Email serves as backup access method when user has no app access or internet connectivity
- Email should be branded and include clear instructions for business presentation

**🖼 Wireframe Reference**
- Exists: Yes
- Filename: `woppa-wireframe-5-obtained-cupon.png`

**📊 PERT Estimation**:
- **Optimistic**: ___ hours
  - _Comments: [Space for optimistic scenario assumptions]_
- **Realistic**: ___ hours
  - _Comments: [Space for realistic scenario assumptions]_
- **Pessimistic**: ___ hours
  - _Comments: [Space for pessimistic scenario assumptions]_

---

### 🔹 `REDEEM-MOB-007` – Navigate from Coupon Screen

**Summary**:  
Provide navigation options from the coupon screen to enhance user experience.

**Justification**:  
Users need convenient options to navigate to the business or continue exploring offers.

**User Story**:  
"As a consumer, I want to easily navigate to the business location or find more offers after receiving my redemption code, so that I can use my code or continue shopping."

**🎯 Objective**:  
Enable smooth navigation to business directions or offer discovery.

**⛓ Dependencies**:  
- Google Maps integration
- Offer browsing system
- Business location data

**✅ Acceptance Criteria**:
- "Go to business" button opens Google Maps with directions
- "Find more offers" button returns to offer browsing
- Close button returns to appropriate app section
- Handle Google Maps app not installed scenario
- Preserve user context for return navigation
- Track user actions for analytics

**🧰 Technical Tasks**:
- Implement Google Maps deep linking
- Create navigation to offer browsing flows
- Add close/dismiss functionality
- Handle external app integration errors
- Implement usage analytics tracking
- Create fallback for mapping failures

**⚙️ External Setup / Config Required**
- Google Maps integration configuration
- Deep linking URL schemes setup

**❗ Pending Confirmations**
- Default app section for close button navigation
- Analytics tracking requirements
- Handling users without Google Maps app

**📝 Notes & Observations**
- Wireframe shows clear navigation options
- Requirements suggest branded language for "continue exploring" actions
- Integration point with other app flows

**🖼 Wireframe Reference**
- Exists: Yes
- Filename: `woppa-wireframe-5-obtained-cupon.png`

**📊 PERT Estimation**:
- **Optimistic**: ___ hours
  - _Comments: [Space for optimistic scenario assumptions]_
- **Realistic**: ___ hours
  - _Comments: [Space for realistic scenario assumptions]_
- **Pessimistic**: ___ hours
  - _Comments: [Space for pessimistic scenario assumptions]_

---

## 🧪 Post-analysis: Story Set Review

After analyzing all stories systematically, the story set shows excellent cohesion with simplified, clear sequential flow:

**Flow Analysis:**
- REDEEM-MOB-001 → REDEEM-MOB-002 → (REDEEM-MOB-003 if auth needed OR REDEEM-MOB-004 if authenticated) → (REDEEM-MOB-005 if cancellation OR REDEEM-MOB-006 if payment processing) → REDEEM-MOB-007
- Stories represent a complete user journey from offer viewing to code usage
- Clear decision points (authentication, payment cancellation vs processing)

**Consistency Check:**
- All stories reference the same offer redemption context
- Authentication handling is consistently treated as external dependency
- Payment processing consolidated into unified approach in REDEEM-MOB-006
- Error handling patterns differentiate between cancellation (REDEEM-MOB-005) and other failures (REDEEM-MOB-006)

**Story Boundaries:**
- Each story has distinct, non-overlapping responsibilities
- Dependencies are clearly identified and external to the epic
- Success/failure paths are appropriately separated by type
- Navigation endpoints connect properly to other epics

**Architecture Improvements Made:**
- Eliminated RED-004 and RED-005 by consolidating payment verification into REDEEM-MOB-006
- Simplified payment flow by handling verification within offer code display
- Reduced complexity while maintaining comprehensive coverage
- Clearer separation of concerns between cancellation and other payment failures

The simplified story set provides more efficient implementation while maintaining complete functional coverage.

---

## 📌 Stories with High Risk or Pending Decisions

List all stories in this epic that include:
- REDEEM-MOB-004: Process Payment via Mercado Pago (missing wireframe, external API integration)
- REDEEM-MOB-005: Handle Payment Cancellation (simple redirection flow but cancellation detection logic needs clarification) 
- REDEEM-MOB-006: Display Redemption Code with Payment Verification (complex integrated functionality, missing verification state wireframes, critical payment and code generation logic)

---

## 📊 Epic Estimation Summary

To be completed manually:

- Total user stories: 7
- Stories with high uncertainty: 3 (REDEEM-MOB-004, REDEEM-MOB-005, REDEEM-MOB-006)
- Stories pending confirmation: 4

### Manual 3-point Estimation for Epic (PERT)

```
- Optimistic: 
- Realistic:
- Pessimistic:
```