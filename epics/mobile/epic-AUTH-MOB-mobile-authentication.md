# 🧩 Epic: Mobile User Authentication

**KEY**: `AUTH-MOB`

---

## 📄 Functional Description
This epic covers all authentication and user account management functionality for the Woppa mobile application. It enables users to create accounts, log in, manage their credentials, and maintain authenticated sessions to access premium features like offer redemption. The authentication system serves as the gateway to personalized features and purchase history.

---

## 💻 Target Platform
This epic applies to:
- `mobile`

---

## 🧭 Functional Scope
Main flows and interactions included in this epic:
- User registration with email/password or Google OAuth
- User login with existing credentials or Google OAuth
- Email verification and account activation
- Password reset and recovery flows
- Session management and logout functionality
- Integration with offer redemption flow (authentication gating)

---

## 🚫 Out of Scope
Explicitly excluded elements:
- Phone number verification (removed per business decision 2025-01-25)
- Social media authentication beyond Google (Facebook, Instagram, Apple ID)
- Two-factor authentication (2FA)
- Profile information management (covered in Account Management epic)
- Purchase history (covered in Account Management epic)
- User preferences and favorites (covered in Account Management epic)
- Merchant/business authentication (covered in web panel)

---

## 🖼 Wireframes Referenced in Epic
List of wireframes that apply to this epic and the stories that use them.

- `woppa-wireframe-4-register.png` → used in: AUTH-MOB-001, AUTH-MOB-002, AUTH-MOB-003, AUTH-MOB-004
- `woppa-wireframe-1-mapa.png` → shows "Registrarse" button → used in: AUTH-MOB-001, AUTH-MOB-007
- `woppa-wireframe-2-listado-ofertas.png` → shows "Registrarse" button → used in: AUTH-MOB-001, AUTH-MOB-007
- (none for AUTH-MOB-005, AUTH-MOB-006, AUTH-MOB-008 - missing wireframes)

---

## 🔍 Epic-level Ambiguities

- 📐 **Missing wireframe**: Email verification screen not defined
- 📐 **Missing wireframe**: Password reset request screen not defined  
- 📐 **Missing wireframe**: Password reset confirmation screen not defined
- 📐 **Missing wireframe**: Post-registration success/onboarding screen not defined
- 🧩 **External dependency unclear**: Firebase Auth vs direct Google OAuth implementation decision pending
- 📋 **Missing validation rules**: Specific email verification requirements and timing
- 🧭 **Mismatch between document and wireframe**: Wireframe 4 doesn't show name fields (first name, last name) mentioned in business decisions
- 📊 **Business decision pending**: Session timeout duration and automatic logout policy
- ⚠️ **Uncovered edge case**: Handling of existing Google accounts that don't have required profile information
- 🧩 **Cross-authentication conflict**: Handling of same email across different auth methods (email/password vs Google) needs resolution strategy

---

## 🧵 User Stories

---

### 🔹 `AUTH-MOB-001` – Registration Flow Entry Points

**Summary**:  
Users can access the registration flow from multiple entry points throughout the app.

**Justification**:  
Provides multiple opportunities for user conversion by making registration accessible from key screens.

**User Story**:  
"As a potential user, I want to easily find and access the registration flow from various screens, so that I can create an account when I'm ready to redeem offers."

**🎯 Objective**:  
All "Registrarse" buttons lead to the unified registration/login screen with proper context preservation.

**⛓ Dependencies**:  
Navigation system, screen routing, session state management.

**✅ Acceptance Criteria**:
- "Registrarse" button is visible and accessible on map view (wireframe 1)
- "Registrarse" button is visible and accessible on offer list view (wireframe 2) 
- "Registrarse" button is visible and accessible on offer details view (wireframe 3)
- Clicking any "Registrarse" button navigates to the registration/login screen
- User context is preserved (e.g., which offer they were viewing) for post-registration redirect
- Button text changes to "Mi cuenta" or similar when user is already logged in

**🧰 Technical Tasks**:
- Implement navigation routing to registration screen from all entry points
- Create shared authentication button component with context-aware text
- Implement context preservation for post-auth redirects
- Add authentication state detection to modify button behavior
- Create navigation flow mapping for all auth entry points

**⚙️ External Setup / Config Required**
- Deep linking configuration for post-registration redirects
- Navigation library setup and route definitions

**❗ Pending Confirmations**
- Exact wording for logged-in state button ("Mi cuenta" vs other options)
- Whether "Registrarse" button should be visible when user is logged in

**📝 Notes & Observations**
- Current wireframes show "Registrarse" consistently, but need to clarify logged-in state
- Context preservation is critical for user experience after authentication

**🖼 Wireframe Reference**
- Exists: Yes
- Filenames: `woppa-wireframe-1-mapa.png`, `woppa-wireframe-2-listado-ofertas.png`, `woppa-wireframe-3-detalle-oferta.png`, `woppa-wireframe-4-register.png`

**📊 PERT Estimation**:
- **Optimistic**: ___ hours
  - _Comments: [Space for optimistic scenario assumptions]_
- **Realistic**: ___ hours
  - _Comments: [Space for realistic scenario assumptions]_
- **Pessimistic**: ___ hours
  - _Comments: [Space for pessimistic scenario assumptions]_

---

### 🔹 `AUTH-MOB-002` – Email and Password Registration

**Summary**:  
Users can create a new account using email, password, and basic personal information.

**Justification**:  
Provides traditional registration method for users who prefer not to use Google OAuth.

**User Story**:  
"As a new user, I want to create an account with my email and password, so that I can access personalized features and redeem offers."

**🎯 Objective**:  
Users can successfully create accounts with email/password and receive verification emails.

**⛓ Dependencies**:  
Email service provider, backend user creation API, password validation system.

**✅ Acceptance Criteria**:
- Registration form displays fields for: email, password, first name, last name
- Email field validates proper email format in real-time
- Password field enforces requirements: minimum 8 characters, 1 uppercase, 1 number, 1 special character
- Password field includes show/hide toggle functionality
- Form validates all required fields before enabling submission
- Successful registration sends verification email to user
- Clear error messages for validation failures and duplicate emails
- Form validates email is not already registered with Google OAuth
- Clear error message for Google-registered emails: "Este email ya está registrado con Google. Usa 'Ingresar con Google'."
- Terms and conditions checkbox is required before submission

**🧰 Technical Tasks**:
- Create registration form component with all required fields
- Implement real-time email format validation
- Add password visibility toggle functionality
- Create backend API endpoint for user registration (or use Firebase Auth)
- Integrate email service for verification emails (or use Firebase Auth)
- Implement duplicate email detection and error handling
- Implement cross-authentication email conflict detection
- Add backend API for checking existing registration methods by email
- Create consistent error messaging for authentication conflicts
- Add terms and conditions acceptance flow
- Create client-side form validation logic

**⚙️ External Setup / Config Required**
- Email service provider configuration (SendGrid, AWS SES, or similar)
- LGPD compliance review for data collection
- Terms and conditions document creation
- Email template design for verification emails

**❗ Pending Confirmations**
- Specific password complexity requirements (current: 8 chars, 1 upper, 1 number, 1 special)
- Whether email verification is required before account activation
- Error message wording for various validation failures

**📝 Notes & Observations**
- Wireframe doesn't show first name/last name fields - needs clarification against business decision
- Form should match simplified registration requirements (no phone number)

**📉 PERT Estimation Candidate**
```
PERT:
- Optimistic: 16h
- Realistic: 24h
- Pessimistic: 32h
Justification: Missing wireframe details for name fields and uncertain email verification requirements add complexity
```

**🖼 Wireframe Reference**
- Exists: Partial
- Filename: `woppa-wireframe-4-register.png`
- Note: Shows email/password fields but missing name fields mentioned in business decisions

**📊 PERT Estimation**:
- **Optimistic**: ___ hours
  - _Comments: [Space for optimistic scenario assumptions]_
- **Realistic**: ___ hours
  - _Comments: [Space for realistic scenario assumptions]_
- **Pessimistic**: ___ hours
  - _Comments: [Space for pessimistic scenario assumptions]_

---

### 🔹 `AUTH-MOB-003` – Google OAuth Registration

**Summary**:  
Users can create accounts using their Google credentials for faster onboarding.

**Justification**:  
Reduces friction in registration process and leverages existing user credentials.

**User Story**:  
"As a new user, I want to register using my Google account, so that I can quickly create an account without typing personal information."

**🎯 Objective**:  
Seamless Google OAuth integration that creates user accounts with Google profile data.

**⛓ Dependencies**:  
Google OAuth 2.0 configuration, Google Cloud Console setup, backend OAuth handling.

**✅ Acceptance Criteria**:
- "Registro con Google" button is prominently displayed on registration screen
- Clicking Google button opens native Google OAuth flow
- Successful OAuth returns user to app with account created
- User profile is populated with Google data: name, email, profile picture (if available)
- If Google account already exists in system, redirect to login instead of duplicate creation
- OAuth flow validates email is not already registered with email/password
- Clear error message for email-registered accounts: "Este email ya está registrado. Inicia sesión con email y contraseña."
- User is redirected to login tab after Google conflict error
- Error handling for OAuth cancellation or failures
- Backend creates user record with Google account linking

**🧰 Technical Tasks**:
- Integrate Google OAuth 2.0 SDK for React Native
- Configure Google Sign-In for iOS and Android
- Create backend OAuth verification and user creation flow
- Implement Google account duplicate detection
- Implement cross-authentication email conflict detection
- Add backend API for checking existing registration methods by email
- Create consistent error messaging for authentication conflicts
- Add error handling for OAuth flow failures
- Create user profile mapping from Google data
- Add Google account linking to user records
- Implement OAuth token refresh mechanisms

**⚙️ External Setup / Config Required**
- Google Cloud Console project setup
- OAuth 2.0 client credentials for iOS and Android
- Google Services configuration files (GoogleService-Info.plist, google-services.json)
- Backend OAuth verification endpoint

**❗ Pending Confirmations**
- Whether Firebase Auth or direct Google OAuth will be used
- Handling of edge cases where Google profile lacks required information

**📝 Notes & Observations**
- Tech stack shows Google OAuth 2.0 confirmed but Firebase Auth vs direct OAuth is pending decision
- Need to handle cases where Google account doesn't provide all required profile data

**📉 PERT Estimation Candidate**
```
PERT:
- Optimistic: 20h
- Realistic: 32h
- Pessimistic: 48h
Justification: Uncertainty around Firebase Auth vs direct OAuth implementation and complex OAuth flow setup
```

**🖼 Wireframe Reference**
- Exists: Yes
- Filename: `woppa-wireframe-4-register.png`

**📊 PERT Estimation**:
- **Optimistic**: ___ hours
  - _Comments: [Space for optimistic scenario assumptions]_
- **Realistic**: ___ hours
  - _Comments: [Space for realistic scenario assumptions]_
- **Pessimistic**: ___ hours
  - _Comments: [Space for pessimistic scenario assumptions]_

---

### 🔹 `AUTH-MOB-004` – User Login

**Summary**:  
Existing users can log into their accounts using email/password or Google OAuth.

**Justification**:  
Enables returning users to access their accounts and personalized features.

**User Story**:  
"As a returning user, I want to log into my account with my credentials, so that I can access my purchase history and redeem offers."

**🎯 Objective**:  
Secure and reliable login functionality for both email/password and Google OAuth methods.

**⛓ Dependencies**:  
User authentication backend, session management, Google OAuth configuration.

**✅ Acceptance Criteria**:
- "Ingreso" tab is available on auth screen (wireframe shows toggle between Registro/Ingreso)
- Login form shows email and password fields for credential login
- "Registro con Google" button works for both new registration and existing user login
- Successful login redirects user to previous context or home screen
- Failed login shows clear error messages
- Login form includes "forgot password" link
- Session is maintained across app restarts until logout
- Login state is reflected in navigation (button changes from "Registrarse" to "Mi cuenta")

**🧰 Technical Tasks**:
- Create login form component with email/password fields
- Implement login API integration with error handling
- Add Google OAuth login flow (reuse registration OAuth setup)
- Create session management and persistence
- Implement "forgot password" navigation
- Add login state management throughout app
- Create secure token storage for authenticated sessions
- Implement automatic session restoration on app launch

**⚙️ External Setup / Config Required**
- Secure token storage configuration
- Session timeout policies
- Backend authentication endpoints

**❗ Pending Confirmations**
- Session timeout duration and automatic logout policy
- Specific error messages for various login failure scenarios

**📝 Notes & Observations**
- Wireframe shows tab switching between registration and login on same screen
- Need to handle both new Google users (registration) and existing Google users (login) in single OAuth flow

**🖼 Wireframe Reference**
- Exists: Yes
- Filename: `woppa-wireframe-4-register.png`

**📊 PERT Estimation**:
- **Optimistic**: ___ hours
  - _Comments: [Space for optimistic scenario assumptions]_
- **Realistic**: ___ hours
  - _Comments: [Space for realistic scenario assumptions]_
- **Pessimistic**: ___ hours
  - _Comments: [Space for pessimistic scenario assumptions]_

---

### 🔹 `AUTH-MOB-005` – Email Verification

**Summary**:  
Users who register with email/password must verify their email address to activate their account.

**Justification**:  
Prevents abuse and ensures users have access to their registered email for future communications.

**User Story**:  
"As a newly registered user, I want to verify my email address through a verification link, so that my account is fully activated and secure."

**🎯 Objective**:  
Reliable email verification process that activates user accounts upon confirmation.

**⛓ Dependencies**:  
Email service provider, verification token generation, deep linking setup.

**✅ Acceptance Criteria**:
- Verification email is sent immediately after registration
- Email contains clear instructions and verification link
- Clicking verification link opens app and confirms account
- Verified users can access all authenticated features
- Unverified users see appropriate messaging about verification status
- Resend verification email option available if needed
- Verification links expire after reasonable time period
- Account activation is reflected in backend user status

**🧰 Technical Tasks**:
- Create email verification token generation system
- Design and implement verification email template
- Set up deep linking for verification link handling
- Create verification confirmation screen/flow
- Implement resend verification email functionality
- Add verification status checking throughout app
- Create backend verification endpoint
- Add verification status to user profile data

**⚙️ External Setup / Config Required**
- Deep linking configuration for verification URLs
- Email template design and approval
- Verification token security and expiration policies

**❗ Pending Confirmations**
- Whether email verification is required or optional for MVP
- Verification link expiration time
- Behavior for users who don't verify within time limit
- Whether unverified users can redeem offers (since payment through Mercado Pago provides some validation)

**📝 Notes & Observations**
- Existing epic notes suggest email verification might be skipped initially since Mercado Pago payment provides user validation
- No wireframe exists for verification flow

**📉 PERT Estimation Candidate**
```
PERT:
- Optimistic: 12h
- Realistic: 20h
- Pessimistic: 32h
Justification: No wireframe and uncertainty about verification requirements in MVP scope
```

**🖼 Wireframe Reference**
- Exists: No
- Note: Verification screen wireframe not defined

**📊 PERT Estimation**:
- **Optimistic**: ___ hours
  - _Comments: [Space for optimistic scenario assumptions]_
- **Realistic**: ___ hours
  - _Comments: [Space for realistic scenario assumptions]_
- **Pessimistic**: ___ hours
  - _Comments: [Space for pessimistic scenario assumptions]_

---

### 🔹 `AUTH-MOB-006` – Password Reset Flow

**Summary**:  
Users can reset their forgotten passwords through a secure email-based recovery process.

**Justification**:  
Essential functionality for users who forget their passwords and need account recovery.

**User Story**:  
"As a user who forgot my password, I want to reset it using my email address, so that I can regain access to my account."

**🎯 Objective**:  
Secure password reset process that allows users to regain account access safely.

**⛓ Dependencies**:  
Email service, password reset token system, deep linking configuration.

**✅ Acceptance Criteria**:
- "Forgot password" link is available on login screen
- Password reset request form accepts email address
- Reset email is sent to valid email addresses
- Reset link opens app and allows new password entry
- New password must meet same complexity requirements as registration
- Password reset tokens expire after reasonable time
- Account is accessible with new password after reset
- Old password is invalidated after successful reset

**🧰 Technical Tasks**:
- Add "forgot password" link to login form
- Create password reset request screen and form
- Implement password reset token generation and validation
- Create password reset email template
- Build new password entry screen with validation
- Set up deep linking for password reset URLs
- Implement backend password reset endpoints
- Add password reset confirmation and success messaging

**⚙️ External Setup / Config Required**
- Password reset email template design
- Deep linking configuration for reset URLs
- Password reset token security policies

**❗ Pending Confirmations**
- Password reset link expiration time
- Whether Firebase Auth reset flow will be used (which handles UI automatically)
- Error handling for invalid or expired reset tokens

**📝 Notes & Observations**
- Existing epic suggests Firebase Auth default reset flow might be used, which would reduce custom UI needs
- No wireframes exist for password reset screens

**📉 PERT Estimation Candidate**
```
PERT:
- Optimistic: 10h
- Realistic: 18h
- Pessimistic: 28h
Justification: No wireframes and uncertainty about Firebase Auth vs custom implementation
```

**🖼 Wireframe Reference**
- Exists: No
- Note: Password reset screens wireframes not defined

**📊 PERT Estimation**:
- **Optimistic**: ___ hours
  - _Comments: [Space for optimistic scenario assumptions]_
- **Realistic**: ___ hours
  - _Comments: [Space for realistic scenario assumptions]_
- **Pessimistic**: ___ hours
  - _Comments: [Space for pessimistic scenario assumptions]_

---

### 🔹 `AUTH-MOB-007` – Session Management and Logout

**Summary**:  
Authenticated users can manage their session state and securely log out of the application.

**Justification**:  
Essential for security and multi-user device scenarios where users need to log out.

**User Story**:  
"As a logged-in user, I want to securely log out of my account, so that my personal information is protected on shared devices."

**🎯 Objective**:  
Reliable session management with secure logout functionality and appropriate session timeout.

**⛓ Dependencies**:  
Session storage system, authentication state management, secure token handling.

**✅ Acceptance Criteria**:
- Logout option is available in user profile or account settings
- Logout clears all stored authentication tokens and session data
- User is redirected to appropriate screen after logout
- Authentication state is updated throughout app after logout
- Sessions persist across app restarts until explicit logout
- Automatic logout occurs after defined timeout period
- Authentication state is properly restored on app launch
- "Mi cuenta" button changes back to "Registrarse" after logout

**🧰 Technical Tasks**:
- Implement secure session storage and management
- Create logout functionality that clears all auth data
- Add session timeout handling with user notification
- Implement authentication state management across app
- Create session restoration logic for app launches
- Add logout confirmation dialog (if required)
- Update navigation and UI state after logout
- Implement automatic session cleanup

**⚙️ External Setup / Config Required**
- Secure storage configuration for tokens
- Session timeout policy definition
- Logout confirmation UI requirements

**❗ Pending Confirmations**
- Session timeout duration before automatic logout
- Whether logout requires confirmation dialog
- Location of logout option in app (profile screen, settings, etc.)

**📝 Notes & Observations**
- Need to determine where logout functionality will be located since profile screen wireframe doesn't exist yet
- Session management affects all other authentication stories

**🖼 Wireframe Reference**
- Exists: Partial
- Note: Entry points visible in wireframes 1-3, but logout/profile screen not defined

**📊 PERT Estimation**:
- **Optimistic**: ___ hours
  - _Comments: [Space for optimistic scenario assumptions]_
- **Realistic**: ___ hours
  - _Comments: [Space for realistic scenario assumptions]_
- **Pessimistic**: ___ hours
  - _Comments: [Space for pessimistic scenario assumptions]_

---

### 🔹 `AUTH-MOB-008` – Authentication Integration with Offer Flow

**Summary**:  
Authentication system integrates seamlessly with the offer redemption flow to gate premium features.

**Justification**:  
Ensures only authenticated users can redeem offers while maintaining smooth user experience.

**User Story**:  
"As a user viewing offers, I want to be prompted to authenticate only when needed for redemption, so that I can browse freely but complete purchases securely."

**🎯 Objective**:  
Smooth authentication integration that doesn't interrupt browsing but secures purchase flow.

**⛓ Dependencies**:  
Offer redemption flow, payment system integration, session state management.

**✅ Acceptance Criteria**:
- Users can browse offers and view details without authentication
- Authentication is required when clicking "Obtener oferta" or similar purchase buttons
- Unauthenticated users are redirected to login/register with context preserved
- After successful authentication, users continue to payment/redemption flow
- Authentication state is checked before allowing payment process
- Error handling for authentication failures during purchase flow
- Context preservation ensures users return to correct offer after auth

**🧰 Technical Tasks**:
- Implement authentication guards for offer redemption endpoints
- Create context preservation for post-auth redirects
- Add authentication state checking in purchase flow
- Implement seamless redirect to auth from offer details
- Create error handling for auth failures during purchases
- Add authentication status validation before payment processing
- Implement conditional UI based on authentication state

**⚙️ External Setup / Config Required**
- Integration points with payment system
- Error handling strategies for auth failures

**❗ Pending Confirmations**
- Exact flow after authentication (payment screen, confirmation, etc.)
- Error messaging when authentication fails during purchase
- Whether guest checkout will be supported in future

**📝 Notes & Observations**
- Critical integration point between authentication and core business functionality
- Must ensure smooth user experience for both authenticated and unauthenticated browsing

**🖼 Wireframe Reference**
- Exists: Partial
- Note: Integration points visible in offer flow wireframes but authentication transitions not explicitly shown

**📊 PERT Estimation**:
- **Optimistic**: ___ hours
  - _Comments: [Space for optimistic scenario assumptions]_
- **Realistic**: ___ hours
  - _Comments: [Space for realistic scenario assumptions]_
- **Pessimistic**: ___ hours
  - _Comments: [Space for pessimistic scenario assumptions]_

---

## 🧪 Post-analysis: Story Set Review

After analyzing all stories, I've identified the following optimizations and observations:

**Overlaps and Dependencies:**
- AUTH-MOB-002 and AUTH-MOB-003 share backend user creation logic and can reuse validation components
- AUTH-MOB-004 reuses OAuth setup from AUTH-MOB-003 for Google login
- AUTH-MOB-007 (session management) is a dependency for all other authentication stories
- AUTH-MOB-008 integrates with stories from other epics (Offer Redemption)

**Consistency Improvements:**
- All stories maintain consistent error handling patterns
- Session management approach is unified across registration, login, and logout flows
- OAuth implementation is shared between registration and login stories

**Scope Clarifications:**
- Email verification (AUTH-MOB-005) may be optional for MVP based on requirements analysis
- Password reset flow (AUTH-MOB-006) could use Firebase Auth default implementation to reduce scope
- Authentication integration (AUTH-MOB-008) bridges with payment system which has pending decisions

**No conflicts or duplications were identified.** Stories are properly scoped and complementary.

---

## 📌 Stories with High Risk or Pending Decisions

- **AUTH-MOB-002**: Missing wireframe details for name fields, uncertain email verification requirements
- **AUTH-MOB-003**: Uncertainty around Firebase Auth vs direct OAuth implementation 
- **AUTH-MOB-005**: No wireframe, unclear if email verification required for MVP
- **AUTH-MOB-006**: No wireframes, Firebase Auth vs custom implementation pending
- **AUTH-MOB-007**: Session timeout policy undefined, logout UI location unclear
- **AUTH-MOB-008**: Integration with payment system has pending architectural decisions

---

## 📊 Epic Estimation Summary

To be completed manually:

- Total user stories: **8**
- Stories with high uncertainty: **4** (AUTH-MOB-002, AUTH-MOB-003, AUTH-MOB-005, AUTH-MOB-006)
- Stories pending confirmation: **6**

### Manual 3-point Estimation for Epic (PERT)

```
- Optimistic: 
- Realistic:
- Pessimistic:
```