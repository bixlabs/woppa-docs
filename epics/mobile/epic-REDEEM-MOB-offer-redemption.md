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
- Handle payment verification through direct status check using payment ID from redirect
- Handle payment cancellation with redirection to offer details
- Generate and display unique redemption codes upon payment confirmation
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

- 📐 Missing wireframe: Payment processing states within offer code screen
- 📋 Missing validation rules: Maximum redemptions per user per offer
- 🧩 External dependency unclear: Mercado Pago webhook reliability and error scenarios
- ⚠️ Uncovered edge case: User closes app during payment processing
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
- Offer data from backend API (including available stock information)
- User location for distance calculation
- Category and subcategory mapping
- **Real-time stock availability endpoint for pre-checkout validation**

**✅ Acceptance Criteria**:
- Display offer image, business name, and category
- Show offer conditions (timing, restrictions, validity)
- Display "1+1" benefit badge clearly
- Include business address and map integration
- **Add quantity selector dropdown (1-10 units) for multiple unit purchase**
- **Display available stock and adjust quantity selector maximum to available stock**
- **Show total price calculation (quantity × unit price) in real-time**
- **Auto-adjust quantity to available stock with "Solo quedan X disponibles" message when needed**
- **Quantity selector maximum = min(system_limit=10, available_stock) - dynamic adjustment**
- Show "Obtener oferta" button prominently
- Handle missing images with appropriate placeholders
- Display error message when user returns from cancelled/failed payment
- Clear error state when user navigates away or retries
- **Handle out-of-stock offers with disabled "Obtener oferta" button and "Agotado" messaging when stock = 0 OR manually disabled by staff (Cross-epic dependency: EXP-MOB)**
- **Display grayed-out styling for unavailable offers while maintaining full offer details visibility**

**🧰 Technical Tasks**:
- Implement offer details screen layout
- Integrate with offers API endpoint
- Add image loading (images come from backend URLs)
- Implement Google Maps integration for location (static map)
- **Add quantity selector dropdown component (1-10, dynamic max based on stock)**
- **Implement real-time price calculation (quantity × unit price)**
- **Use stock from offer details API for initial display**
- **Add real-time stock validation API for pre-checkout verification**
- **Implement quantity auto-adjustment logic when stock is limited**
- Add error message display component for payment failures
- Implement error state management and clearing logic
- Add clipboard functionality for copying offer details
- **Implement conditional "Obtener oferta" button logic for unavailable offers (stock = 0 OR manually disabled)**
- **Add grayed-out styling and "Agotado" messaging for unavailable offers**

**⚙️ External Setup / Config Required**
- Google Maps API key configuration
- **Offer details API updated to include available_stock field and offer_status (active/disabled)**
- **Real-time stock validation endpoint configuration**

**❗ Pending Confirmations**
- Final button text ("Obtener oferta" vs "Quiero la oferta")
- Social media links display requirements
- **Maximum quantity limit configuration (system default: 10 units, business-configurable in future)**
- **Stock availability refresh frequency and caching strategy**

**📝 Notes & Observations**
- Wireframe shows static map but requirements mention Google Maps integration
- Instagram link mentioned in requirements but not visible in wireframe
- Category tags design needs clarification
- **Dual stock approach: offer details API for initial display, real-time endpoint for pre-checkout validation**

**🖼 Wireframe Reference**
- Exists: Yes
- Filename: `woppa-wireframe-3-detalle-oferta.png`

**📊 PERT Estimation**:
- **Optimistic**: 8 hours
- **Realistic**: 11.5 hours
  - Comments: Added complexity for quantity selector, stock validation, and real-time price calculation. Assumes AI tools acceleration.
    - Frontend UI: ~4.5h (added quantity selector and stock display)
    - Frontend Logic: ~2h (stock validation, price calculation, quantity limits)
    - Integration: ~1.5h (stock API, price calculation)
    - Backend: ~2.5h (stock availability endpoint, quantity validation)
    - Manual Testing: ~1h
- **Pessimistic**: 16 hours
- **Final PERT Estimate: 12 hours**

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
- **Validate selected quantity against current available stock before proceeding**
- **Pass selected quantity to subsequent redemption flow (REDEEM-MOB-003/004)**
- Check offer availability and current stock before proceeding
- **Display "Oferta agotada" message when stock = 0 OR offer is manually disabled by Woppa staff (indefinite stock status)**
- **Display confirmation modal when selected quantity exceeds available stock: "Querías X, solo quedan Y disponibles. ¿Continuar con Y unidades?"**
- **Handle user confirmation: proceed with adjusted quantity or cancel to retry**
- Check offer expiration status
- If user not authenticated: delegate to REDEEM-MOB-003 for context preservation and auth flow
- If user authenticated but email not verified: delegate to REDEEM-MOB-003 for email verification flow
- If user fully authenticated and stock available: call centralized proceedToPayment function directly
- Handle offer unavailability with appropriate messaging
- Prevent multiple simultaneous redemptions
- Clear loading states during validation

**🧰 Technical Tasks**:
- Implement authentication status check
- Add offer availability and stock validation
- **Add quantity validation logic (selected quantity vs available stock)**
- **Implement quantity parameter passing to subsequent flows**
- **Add quantity-aware stock checking with confirmation modal logic**
- **Implement stock insufficient confirmation modal component**
- **Add user decision handling (accept adjusted quantity or cancel)**
- Create decision logic for routing (auth needed, email verification needed, or proceed to payment)
- Integrate with centralized proceedToPayment function
- Add delegation to REDEEM-MOB-003 when context preservation needed
- Implement loading states during validation
- Add error handling for unavailable offers and out-of-stock scenarios
- Create stock checking mechanism with real-time validation

**⚙️ External Setup / Config Required**
- Authentication service integration
- Session management configuration
- **Real-time stock validation API endpoint for pre-checkout verification**

**❗ Pending Confirmations**
- Stock checking frequency and real-time validation approach
- Maximum redemptions per user per offer?
- **Offer unavailability criteria: stock = 0 vs manually disabled by staff**
- **"Agotado" messaging strategy for different unavailability reasons**
- **Stock insufficient confirmation modal design and messaging**
- **User decision flow: accept adjusted quantity vs cancel and retry behavior**

**📝 Notes & Observations**
- Clean separation: this story focuses on validation and routing decisions
- Context preservation complexity handled by REDEEM-MOB-003
- Uses centralized proceedToPayment function to avoid logic duplication
- **Two-tier stock validation: offer details API (initial) + real-time API (pre-checkout)**

**🖼 Wireframe Reference**
- Exists: No (logic/flow step)

**📊 PERT Estimation**:
- **Optimistic**: 7 hours
- **Realistic**: 9 hours
  - Comments: Added complexity for stock insufficient confirmation modal and user decision handling.
    - Frontend UI: ~1.5h (spinner, and disabled because no stock, confirmation modal component)
    - Frontend Logic: ~2.75h (stock validation + modal logic + user decisions)
    - Integration: ~1.5h (quantity parameter handling)
    - Backend: ~1.5h (quantity validation logic)
    - Manual Testing: ~1.75h
- **Pessimistic**: 13 hours
- **Final PERT Estimate: 9.5 hours**

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
- **Preserve selected quantity in context during authentication flows**
- Preserve offer context when redirecting to email verification
- Use navigation params for context preservation (MVP approach)
- **Pass quantity parameter (original or user-confirmed adjusted quantity) to centralized proceedToPayment function**
- After successful authentication, call centralized proceedToPayment function
- After successful email verification, call centralized proceedToPayment function
- Handle context loss gracefully with fallback navigation to offer details
- Avoid duplicating payment preparation logic across multiple components
- Support timeout/expiration of context preservation
- Clear context after successful payment completion or explicit cancellation

**🧰 Technical Tasks**:
- Implement navigation parameter passing for offer context
- **Add quantity parameter to navigation context preservation**
- Create centralized proceedToPayment function shared with REDEEM-MOB-002
- **Update proceedToPayment function to accept and handle quantity parameter (may be adjusted from stock confirmation)**
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
- **Optimistic**: 3.5 hours
- **Realistic**: 5.5 hours
  - Frontend UI: ~0
  - Frontend Logic: ~2.25h (refactor and restore context including quantity)
  - Integration: ~1.75h (centralize function payment with quantity and navigate)
  - Backend: ~0hs
  - Manual Testing: ~1.5
- **Pessimistic**: 8.5 hours
- **Final PERT Estimate: 5.67 hours**

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
- **Reserve stock for selected quantity temporarily (15-20 minutes TTL) before payment processing**
- **Calculate total amount (quantity × unit price) for payment preference**
- Generate Mercado Pago payment preference with offer details and reservation ID
- **Include quantity and total amount in payment preference**
- **Include quantity in payment description and item details**
- Include reservation ID in payment metadata for tracking
- Redirect user to Mercado Pago Checkout Pro
- Include proper success/failure return URLs
- Handle user cancellation of payment
- Preserve offer context and reservation ID throughout payment flow
- Display loading state during preference generation
- **Handle reservation failures gracefully (should be rare since quantity already confirmed in REDEEM-MOB-002)**
- **Support adjusted quantity reservation from stock confirmation flow**
- Auto-release reservation on payment preference generation failure

**🧰 Technical Tasks**:
- Implement stock reservation system with TTL (15-20 minutes)
- **Add quantity-based stock reservation (reserve N units of offer)**
- **Implement total amount calculation (quantity × unit price)**
- Create reservation ID generation and tracking
- Integrate Mercado Pago SDK
- Implement payment preference creation API with reservation metadata
- **Add quantity and calculated total to payment preference structure**
- **Update payment description to include quantity information**
- Create redirect mechanism to Mercado Pago
- Implement return URL handling
- Add error handling for preference generation failures
- **Add error handling for rare insufficient stock during reservation (fallback for edge cases)**
- Create payment session tracking with reservation linking
- Implement automatic reservation cleanup on failures

**⚙️ External Setup / Config Required**
- Stock reservation database schema and TTL configuration
- Reservation cleanup job/service configuration
- Mercado Pago developer account setup
- API credentials configuration (public/private keys)
- Webhook URLs configuration in Mercado Pago dashboard
- Return URLs configuration

**❗ Pending Confirmations**
- Stock reservation TTL duration (suggested: 15-20 minutes)
- Reservation cleanup frequency and mechanism
- Payment preference item description format
- User data requirements for payment processing
- Handling of multiple payment methods within Mercado Pago
- Stock unavailable messaging strategy
- **Total amount calculation formula validation (quantity × unit_price)**
- **Payment description format with quantity (e.g., "Pizza 2x1 - Cantidad: 3 unidades")**

**📝 Notes & Observations**
- No wireframe available - UI design needed for payment initiation screen
- Business decision specifies Mercado Pago Checkout Pro specifically
- Need to handle network failures during preference generation
- **Reservation failures should be rare since quantity is pre-validated and confirmed in REDEEM-MOB-002**

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
- **Optimistic**: 16 hours
- **Realistic**: 25 hours
  - Comments: Added complexity for quantity-based stock reservation, total calculation, and enhanced payment preference creation.

    - Frontend UI: ~1h (spinner and webview) 
    - Frontend Logic: ~4h (call orchestration + quantity logic + deep link)
    - Integration: ~3.5h (api call + quantity parameters + config deep link)
    - Backend: ~12.5hs
      - quantity-based stock reservation with TTL
      - total amount calculation endpoint
      - enhanced payment preference creation with quantity
      - mechanism to clean up expired reservations
      - job to clean expired 
      - webhook handling
    - Manual Testing: ~4h
- **Pessimistic**: 34 hours
- **Final PERT Estimate: 25 hours**


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
- **Automatically release quantity-based stock reservation upon cancellation detection**
- Redirect user to offer details screen (RED-001)
- Display cancellation error message on offer details
- Preserve offer context and allow retry
- Clear error state on subsequent redemption attempts
- Log cancellation events for analytics
- Handle reservation release failures gracefully

**🧰 Technical Tasks**:
- Implement cancellation detection from Mercado Pago return URLs
- **Add automatic quantity-based stock reservation release on cancellation**
- Create navigation logic back to offer details
- Integrate error messaging with offer details screen
- Add cancellation event logging
- Implement error state clearing mechanism
- Create retry flow preservation
- Handle reservation release failures and logging

**⚙️ External Setup / Config Required**
- Stock reservation system integration for cleanup
- Mercado Pago cancellation URL configuration
- Error message localization for cancellations
- Analytics event tracking setup

**❗ Pending Confirmations**
- Specific cancellation error message content
- Cancellation detection criteria vs other payment failures
- Analytics tracking requirements for cancellations
- Reservation release retry policy on failures

**📝 Notes & Observations**
- Simpler flow focusing on user-initiated cancellations only
- Integrates with RED-001 for error display
- Other payment failures handled in REDEEM-MOB-006 (offer code screen)

**🖼 Wireframe Reference**
- Exists: Yes (uses offer details wireframe with error state)
- Filename: `woppa-wireframe-3-detalle-oferta.png`

**📊 PERT Estimation**:
- **Optimistic**: 4.5 hours
- **Realistic**: 6.5 hours
  - Frontend UI: ~0h
  - Frontend Logic: ~1.5h
  - Integration: ~30m
  - Backend: ~3h (endpoint to cancel quantity-based reservation and revert stock)
  - Manual Testing: ~1.5h
- **Pessimistic**: 10.5 hours
- **Final PERT Estimate: 6.83 hours**

---

### 🔹 `REDEEM-MOB-006` – Display Redemption Code with Direct Payment Verification

**Summary**:  
Handle direct payment verification using payment ID from Mercado Pago redirect and display redemption code or error messages based on payment status.

**Justification**:  
Users need immediate feedback on payment status with seamless transition to code display or error handling.

**User Story**:  
"As a consumer, I want to see my payment status verified immediately when I return from Mercado Pago and receive my redemption code when confirmed, or clear error messaging if payment fails, so that I know the status of my purchase."

**🎯 Objective**:  
Verify payment status directly using payment ID from redirect query parameters and present redemption code or error messages.

**⛓ Dependencies**:  
- Mercado Pago payment ID from redirect query parameters
- Backend payment status API and verification system
- Backend code generation system
- Email service integration for code delivery
- Business information for the offer

**✅ Acceptance Criteria**:
- Extract payment ID from Mercado Pago redirect query parameters
- Verify payment status directly with backend using payment ID
- Display loading state while verifying payment status
- **Convert quantity-based stock reservation to definitive redemption code upon payment confirmation**
- Generate unique redemption code linked to the reservation ID
- **Display quantity prominently with redemption code (e.g., "Cantidad: 3 unidades")**
- **Include quantity information in code display screen**
- Send redemption code automatically via email upon payment confirmation
- **Include quantity and total amount in email content**
- Include offer details, business information, and usage instructions in email
- Display code prominently in large, readable format with business info
- Show business name and offer type (1+1)
- Include usage instructions in friendly language
- Display code status (active, used, expired)
- Show celebration message for successful purchase
- Display error message for payment failures (non-cancellation)
- **Release quantity-based stock reservation automatically on payment failures**
- Include close/dismiss button
- Handle code generation failures gracefully
- Handle email delivery failures gracefully (log but don't block code display)
- Handle missing or invalid payment ID in query parameters
- Ensure atomic transaction between payment confirmation and reservation conversion

**🧰 Technical Tasks**:
- Implement query parameter parsing for payment ID extraction
- Create direct payment status verification API call
- Create payment verification loading UI state
- **Implement quantity-based reservation to code conversion system with atomic transactions**
- Create code generation algorithm linked to reservation ID
- **Add quantity display component to code screen (show purchased quantity)**
- Integrate email service for automatic code delivery
- **Update email template to include quantity and total amount information**
- Create email template with offer details and business information
- Implement email delivery error handling and logging
- Create code display screen layout with multiple states (loading, success, error)
- Add code status indicator system
- Create celebration UI elements for successful payments
- Implement error messaging for payment failures with reservation cleanup
- **Add automatic quantity-based stock reservation release on payment failures**
- Add accessibility features for code reading
- Create screen capture prevention (if required)
- Implement code copying functionality (if needed)
- Add automatic navigation and state management
- Create payment status state management
- Implement error logging and tracking

**⚙️ External Setup / Config Required**
- Stock reservation to code conversion system setup
- Backend payment verification endpoint
- Email service configuration (SMTP or transactional email provider)
- Email template design and content localization
- Code generation service configuration
- Database schema for code storage and reservation linking
- Code display formatting rules
- Error tracking system integration
- Atomic transaction configuration for reservation conversion

**❗ Pending Confirmations**
- Payment ID parameter name in Mercado Pago redirect
- Code format and length requirements
- **Quantity display format in code screen (e.g., "Cantidad: 3 unidades" vs "3x promoción")**
- **Email template format for quantity and total amount display**
- Email template design and content structure
- Email delivery failure retry policy
- Final celebration message wording
- Brand mascot integration requirements
- Code copying/sharing functionality
- Error message content for payment failures
- Code generation failure handling approach
- Reservation to code conversion failure recovery strategy

**📝 Notes & Observations**
- Wireframe shows code display pattern but not verification loading states
- Direct verification approach eliminates need for polling and timeouts
- Important emotional touchpoint for user satisfaction
- Need to handle edge cases like app backgrounding during verification
- Requirements mention potential brand mascot integration
- Must ensure atomic transaction between payment confirmation and reservation-to-code conversion
- Stock reservation system prevents overselling during payment processing
- Email serves as backup access method when user has no app access or internet connectivity
- Email should be branded and include clear instructions for business presentation
- Reservation cleanup essential for stock accuracy and user experience

**🖼 Wireframe Reference**
- Exists: Yes
- Filename: `woppa-wireframe-5-obtained-cupon.png`

**📊 PERT Estimation**:
- **Optimistic**: 13 hours
- **Realistic**: 20.5 hours
  - Frontend UI: ~6h (added quantity display component)
  - Frontend Logic: ~2.5h (quantity handling logic)
  - Integration: ~1.5h (quantity data flow)
  - Backend: ~8h (quantity-based reservation conversion, email updates)
  - Manual Testing: ~2.5h
- **Pessimistic**: 26 hours
- **Final PERT Estimate: 20.17 hours**

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
- **Optimistic**: 1 hours
- **Realistic**: 2 hours
  - Frontend UI: ~0h
  - Frontend Logic: ~45m
  - Integration: ~45m (linking, navigation and analytics)
  - Backend: ~0h
  - Manual Testing: ~30m
- **Pessimistic**: 4 hours
- **Final PERT Estimate: 2.25 hours**

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
- Stories pending confirmation: 5

### Updated Manual 3-point Estimation for Epic (PERT)

```
- Optimistic: 53
- Realistic: 80h
- Pessimistic: 112h
- Final PERT Estimate: 90.8 (80.8 + 10) hours

Note: I added 10 hours to because I feel backend is underestimated. And just in case I forgot define a schema or a complex logic implementation in backend.
```