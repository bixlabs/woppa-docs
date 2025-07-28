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
- User logout functionality
- Integration with offer redemption flow (authentication gating)
- **Apple Store Compliance**: Sign in with Apple implementation required alongside Google Sign-In

---

## 🚫 Out of Scope
Explicitly excluded elements:
- Phone number verification (removed per business decision 2025-01-25)
- Social media authentication beyond Google and Apple (Facebook, Instagram)
- Two-factor authentication (2FA)
- Profile information management (covered in Account Management epic)
- Purchase history (covered in Account Management epic)
- User preferences and favorites (covered in Account Management epic)
- Merchant/business authentication (covered in web panel)

---

## 🖼 Wireframes Referenced in Epic
List of wireframes that apply to this epic and the stories that use them.

- `woppa-wireframe-4-register.png` → used in: AUTH-MOB-001, AUTH-MOB-002, AUTH-MOB-003, AUTH-MOB-007
- `woppa-wireframe-1-mapa.png` → shows "Registrarse" button → used in: AUTH-MOB-006
- `woppa-wireframe-2-listado-ofertas.png` → shows "Registrarse" button → used in: AUTH-MOB-006
- (none for AUTH-MOB-004, AUTH-MOB-005, AUTH-MOB-007 - missing wireframes for Apple button)

---

## 🔍 Epic-level Ambiguities

- 📐 **Missing wireframe**: Email verification screen not defined
- 📐 **Missing wireframe**: Password reset request screen not defined  
- 📐 **Missing wireframe**: Password reset confirmation screen not defined
- 📐 **Missing wireframe**: Post-registration success/onboarding screen not defined
- 🧩 **Tech stack confirmed**: Using Expo + Firebase Auth for authentication implementation
- 📋 **Missing validation rules**: Specific email verification requirements and timing
- 🧭 **Mismatch between document and wireframe**: Wireframe 4 doesn't show name fields (first name, last name) mentioned in business decisions
- 📊 **Business decision pending**: Session timeout duration and automatic logout policy
- ⚠️ **Uncovered edge case**: Handling of existing Google accounts that don't have required profile information
- 🧩 **Cross-authentication conflict**: Only email/password accounts conflict with Google registration (same email with different auth method)
- ⚠️ **Apple Store Requirement**: Sign in with Apple must be implemented alongside Google Sign-In per App Store Review Guidelines 4.8 (ASR & NR Login Services)
- 🔗 **Account Linking Gap**: Apple's "Hide My Email" relay addresses can create duplicate accounts for same user until account linking feature is implemented

---

## 🧵 User Stories

---

### 🔹 `AUTH-MOB-001` – Email and Password Registration

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


**🖼 Wireframe Reference**
- Exists: Partial
- Filename: `woppa-wireframe-4-register.png`
- Note: Shows email/password fields but missing name fields mentioned in business decisions

**📊 PERT Estimation**:
- **Optimistic**: 10hours
- **Realistic**: 13 hours
  - Comments: Assumes that AI tools will accelerate development, that the UI is simple, that the project scaffolding is complete (toasts). That register happens after entering name and last in a separate pre register onboarding.  That we use firebase for user registration.
    - Frontend UI: ~4h (register + names)
    - Frontend Logic: ~4h (includes auth store and showing login vs AppStack depending on the user)
    - Integration: ~ 1.5h
    - Backend: ~2h (firebase do the core, and we sync the user in our db)
    - Manual Testing: ~1.5h
- **Pessimistic**: 16 hours
- **Final PERT Estimate: 13 hours**

---

### 🔹 `AUTH-MOB-002` – Google OAuth Registration

**Summary**:  
Users can create accounts using their Google credentials for faster onboarding.

**Justification**:  
Reduces friction in registration process and leverages existing user credentials.

**User Story**:  
"As a new user, I want to register using my Google account, so that I can quickly create an account without typing personal information."

**🎯 Objective**:  
Seamless Google OAuth integration that creates user accounts with Google profile data.

**⛓ Dependencies**:  
Firebase Auth configuration, Expo Firebase integration, Google Sign-In provider setup.

**✅ Acceptance Criteria**:
- "Registro con Google" button is prominently displayed on registration screen
- Clicking Google button opens native Google OAuth flow via Firebase Auth
- Successful OAuth returns user to app with account created or authenticated
- User profile is populated with Google data: name, email, profile picture (if available)
- If Google account already exists in system, authenticate user automatically (expected behavior)
- OAuth flow validates email is not already registered with email/password method
- Clear error message for email/password conflicts: "Este email ya está registrado con contraseña. Inicia sesión con email y contraseña."
- User is redirected to login tab after email/password conflict error
- Error handling for OAuth cancellation or failures
- Firebase Auth handles user record creation and Google account linking

**🧰 Technical Tasks**:
- Integrate Firebase Auth with Google Sign-In provider in Expo
- Configure Google Sign-In using Expo's AuthSession or Firebase SDK
- Set up Firebase Auth Google provider configuration
- Implement email/password conflict detection (not Google account duplicates)
- Handle existing Google account authentication automatically
- Create error messaging for email/password auth conflicts only
- Add error handling for OAuth flow failures
- Create user profile mapping from Google data to Firestore
- Sync authenticated users with custom backend database
- Configure Firebase Auth token handling and refresh

**⚙️ External Setup / Config Required**
- Firebase project setup with Authentication enabled
- Google Sign-In provider configuration in Firebase Console
- Expo app.json configuration for Google Sign-In
- Firebase config files integration with Expo (using expo install firebase)
- Google Cloud Console OAuth 2.0 client credentials (if needed beyond Firebase)

**❗ Pending Confirmations**
- Handling of edge cases where Google profile lacks required information
- Expo-specific configuration details for Firebase Auth Google Sign-In
- **Apple Store Requirement**: Sign in with Apple must be implemented alongside Google Sign-In per App Store Review Guidelines 4.8

**📝 Notes & Observations**
- Using Expo + Firebase Auth for Google Sign-In integration simplifies configuration and token management
- Existing Google accounts should authenticate automatically, not show as duplicates
- Only email/password registrations conflict with Google registration attempts for same email
- Expo provides built-in support for Firebase Auth through expo-firebase-auth or direct Firebase SDK
- **Apple Store Compliance**: Per App Store Review Guidelines 4.8, apps using third-party login (Google) must also offer Sign in with Apple as equivalent option
- Reference: https://developer.apple.com/app-store/review/guidelines/ (Section 4.8 ASR & NR Login Services)


**🖼 Wireframe Reference**
- Exists: Yes
- Filename: `woppa-wireframe-4-register.png`

**📊 PERT Estimation**:
- **Optimistic**: 11 hours
- **Realistic**: 23 hours
  - Cloud Setup (Firebase/GCP): 2 - 4 hours
  - Library Installation & Configuration: 2 - 5 hours
  - UI Component (Button/States): 1 - 2 hours
  - Authentication Logic (Sign-in/Sign-out): 2 - 4 hours
  - Initial Configuration Debugging (SHA-1, etc.): 4 - 8 hours

- **Pessimistic**: 40 hours
- **Final PERT Estimate: 24 hours**
---

### 🔹 `AUTH-MOB-003` – User Login

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
- **Optimistic**: 3 hours
- **Realistic**: 4 hours
  - Comments: Assumes that AI tools will accelerate development, that the UI is simple, that register UI is already implemented. That we use firebase and Google OAuth is already implemented because of AUTH-MOB-002.
    - Frontend UI: ~45m
    - Frontend Logic: ~1h
    - Integration: ~ 1h
    - Backend: ~0h (firebase do all the work)
    - Manual Testing: ~1h
- **Pessimistic**: 8 hours
- **Final PERT Estimate: 4.2 hours**

---

### 🔹 `AUTH-MOB-004` – Email Verification Screen

**Summary**:  
Single verification screen that handles both post-registration and login-blocked scenarios when email verification is required.

**Justification**:  
Provides unified UX for email verification needs while authentication service handles the actual verification process.

**User Story**:  
"As a user needing email verification, I want a clear screen that explains the process and allows me to resend or check verification status, so that I can complete account activation."

**🎯 Objective**:  
Simple, reusable verification screen that works with the chosen authentication system's email verification.

**⛓ Dependencies**:  
Authentication service email verification.

**✅ Acceptance Criteria**:
- Single screen handles two contexts: post-registration and login-blocked
- **Post-registration context**: User informed that verification email was sent
- **Login-blocked context**: User informed that email verification is required to continue
- "Reenviar email" button triggers resend verification email
- "Ya verifiqué, continuar" button checks emailVerified status
- Authentication service handles verification link and email template
- Screen shows loading state while checking verification status
- Success navigation: verified users proceed to main app

**🧰 Technical Tasks**:
- Create single EmailVerificationScreen component
- Add context parameter: 'post-register' | 'login-blocked'
- Implement dynamic messaging based on context
- Add resend verification email integration
- Add email verification status checking
- Implement "Reenviar email" functionality with rate limiting
- Add loading states and error handling
- User manually returns to app after clicking email verification link
- Add navigation logic after successful verification

**⚙️ External Setup / Config Required**
- Authentication service email verification configuration
- Email template customization (if needed)

**❗ Pending Confirmations**
- Rate limiting for resend verification email (e.g., max 3 per hour)
- Error handling for email verification failures
- Final UI design and messaging will be defined with UX/UI team

**📝 Notes & Observations**
- Authentication service handles email sending, verification tokens, and web-based verification
- App only needs to show verification screen and check status
- Significantly reduces development complexity compared to custom implementation


**🖼 Wireframe Reference**
- Exists: No
- Note: UI design to be defined with UX/UI team


**📊 PERT Estimation**:
- **Optimistic**: 2 hours
- **Realistic**: 3 hours
  - Comments: Authentication service handles verification logic. Simple UI with context-based messaging and service integration. No deep linking.
    - Frontend UI: ~0.5h
    - Frontend Logic: ~1h
    - Integration: ~0.5h (resend email, status check)
    - Backend: ~0h (firebase do all the work)
    - Manual Testing: ~0.75h
- **Pessimistic**: 6 hours
- **Final PERT Estimate: 3.5 hours**

---

### 🔹 `AUTH-MOB-005` – Password Reset Flow

**Summary**:  
Simple password reset flow using Firebase Auth that allows users to reset forgotten passwords via email.

**Justification**:  
Essential functionality for users who forget their passwords and need account recovery.

**User Story**:  
"As a user who forgot my password, I want to reset it using my email address, so that I can regain access to my account."

**🎯 Objective**:  
Minimal password reset flow that leverages Firebase Auth for secure email-based password recovery.

**⛓ Dependencies**:  
Firebase Auth sendPasswordResetEmail functionality.

**✅ Acceptance Criteria**:
- "Forgot password" link is available on login screen
- Clicking link navigates to password reset screen
- Password reset screen has email input field and "Enviar reset" button
- Firebase sendPasswordResetEmail() is called with entered email
- After successful email send, user is navigated back to login screen
- Toast message "Email de recuperación enviado" is displayed on login screen
- Firebase handles reset email sending and web-based password reset process
- User manually returns to app and can login with new password
- Error handling for invalid email addresses and Firebase failures

**🧰 Technical Tasks**:
- Add "Forgot password" link to login screen
- Create password reset screen with email input and submit button
- Integrate Firebase Auth sendPasswordResetEmail() function
- Add navigation from reset screen back to login after email send
- Implement toast notification for successful email send
- Add email validation on reset screen
- Add error handling for Firebase sendPasswordResetEmail failures
- Add loading state while sending reset email

**⚙️ External Setup / Config Required**
- Firebase Auth configuration for password reset emails
- Firebase email template customization (optional)

**❗ Pending Confirmations**
- Error handling strategy for invalid emails or Firebase failures
- Toast message duration and styling
- Email validation requirements (same as registration)

**📝 Notes & Observations**
- Firebase Auth handles all password reset logic and web-based UI
- App only needs to trigger email send and provide user feedback
- No deep linking needed - user manually returns after web-based reset
- Significantly reduces development complexity


**🖼 Wireframe Reference**
- Exists: No
- Note: Password reset screens wireframes not defined

**📊 PERT Estimation**:
- **Optimistic**: 2 hours
- **Realistic**: 3 hours
  - Comments: Firebase handles reset logic. Simple screen with email input, Firebase integration, and toast notification. No deep linking for MVP.
    - Frontend UI: ~0.75h
    - Frontend Logic: ~0.75h
    - Integration: ~0.5h (sendPasswordResetEmail + error handling)
    - Backend: 0h
    - Manual Testing: ~0.75h
- **Pessimistic**: 6 hours
- **Final PERT Estimate: 3.5 hours**

---

### 🔹 `AUTH-MOB-006` – User Logout

**Summary**:  
Authenticated users can securely log out of the application.

**Justification**:  
Essential for security and multi-user device scenarios where users need to log out.

**User Story**:  
"As a logged-in user, I want to securely log out of my account, so that my personal information is protected on shared devices."

**🎯 Objective**:  
Secure logout functionality that properly clears user session and updates app state.

**⛓ Dependencies**:  
Authentication state management, secure token handling.

**✅ Acceptance Criteria**:
- Logout option is available in user profile or account settings
- Logout clears all stored authentication tokens and session data
- User is redirected to appropriate screen after logout (home/offers screen)
- Authentication state is updated throughout app after logout
- "Mi cuenta" button changes back to "Registrarse" after logout
- Firebase Auth session is properly signed out
- All cached user data is cleared from app
- Logout happens immediately without confirmation dialog

**🧰 Technical Tasks**:
- Create logout functionality that clears all auth data
- Implement Firebase Auth signOut() integration
- Update navigation and UI state after logout
- Clear all user-related cached data
- Update authentication context/store state
- Add logout button/option to profile/account screen

**⚙️ External Setup / Config Required**
- Profile screen design for logout option placement

**❗ Pending Confirmations**
- Location of logout option in app (profile screen, settings, etc.)

**📝 Notes & Observations**
- Need to determine where logout functionality will be located since profile screen wireframe doesn't exist yet
- Session persistence and timeout are handled by Firebase Auth automatically

**🖼 Wireframe Reference**
- Exists: Partial
- Note: Entry points visible in wireframes 1-3, but logout/profile screen not defined

**📊 PERT Estimation**:
- **Optimistic**: 0.5 hours
- **Realistic**: 1 hours
  - Comments: Simple logout functionality with Firebase Auth integration and UI state updates. No confirmation dialog for simplicity.
    - Frontend UI: ~0.25h (logout button)
    - Frontend Logic: ~0.25h (state management already implemented in login)
    - Integration: ~0.25h (Firebase signOut)
    - Backend: 0h (Firebase handles everything)
    - Manual Testing: ~0.25h
- **Pessimistic**: 2 hours
- **Final PERT Estimate: 1 hours**

---

### 🔹 `AUTH-MOB-007` – Sign in with Apple

**Summary**:  
Users can create accounts and log in using their Apple ID credentials to comply with App Store Review Guidelines.

**Justification**:  
Required by Apple Store Review Guidelines 4.8 when offering third-party login services like Google. Provides equivalent privacy-focused authentication option.

**User Story**:  
"As a user, I want to register and log in using my Apple ID, so that I can quickly access the app while keeping my email private if desired."

**🎯 Objective**:  
Seamless Apple Sign-In integration that creates user accounts with Apple profile data and complies with App Store requirements.

**⛓ Dependencies**:  
Apple Developer account, Expo Apple Authentication, Firebase Auth Apple provider configuration.

**✅ Acceptance Criteria**:
- "Continuar con Apple" button is prominently displayed alongside Google registration/login
- Clicking Apple button opens native Apple Sign-In flow via expo-apple-authentication
- Successful authentication returns user to app with account created or logged in
- User profile populated with Apple data: name, email (or hidden email), user identifier
- If Apple account already exists in system, authenticate user automatically
- OAuth flow validates email is not already registered with email/password method
- Clear error message for email/password conflicts: "Este email ya está registrado con contraseña. Inicia sesión con email y contraseña."
- Error handling for Apple Sign-In cancellation or failures
- Firebase Auth handles Apple account creation and linking
- Support for "Hide My Email" Apple privacy feature

**🧰 Technical Tasks**:
- Install and configure expo-apple-authentication
- Set up Firebase Auth Apple Sign-In provider
- Configure Apple Developer account Sign in with Apple capability
- Implement Apple Sign-In button and authentication flow
- Handle Apple-specific user data (including hidden emails)
- Implement email/password conflict detection for Apple accounts
- **Handle Apple email relay/alias duplicates**: Document that relay emails may create separate accounts until account linking is implemented
- Add error handling for Apple authentication failures
- Create user profile mapping from Apple data to Firestore
- Sync Apple-authenticated users with custom backend database
- Test Apple Sign-In on physical iOS devices

**⚙️ External Setup / Config Required**
- Enable Sign in with Apple capability in existing Apple Developer account
- Firebase Console Apple provider setup and service configuration
- Expo app.json configuration for Apple authentication
- Note: Assumes Apple Developer account and iOS app identifier already exist

**❗ Pending Confirmations**
- Handling of Apple's "Hide My Email" feature in user profiles
- **Account Linking Strategy**: Apple's email relay/alias can create duplicate accounts for same user until account linking is implemented
- App Store submission requirements and testing procedures

**📝 Notes & Observations**
- Required for App Store approval when using Google Sign-In
- Apple Sign-In only works on iOS devices and simulators
- Expo provides expo-apple-authentication for simplified integration
- Firebase Auth supports Apple as authentication provider
- Must handle Apple's privacy features like email hiding
- **Email Duplication Risk**: Apple's "Hide My Email" creates relay emails (e.g., abc123@privaterelay.appleid.com) that differ from user's real email, potentially creating duplicate accounts until account linking is implemented

**🖼 Wireframe Reference**
- Exists: No
- Note: Apple button should be added alongside Google button in existing wireframes

**📊 PERT Estimation**:
- **Optimistic**: 5 hours
- **Realistic**: 10 hours
  - Comments: Using Expo + Firebase Auth reduces complexity. Assumes Apple Developer account is already configured for the project.
  - Expo Apple Auth Configuration: 2-3 hours
  - Firebase Apple Provider Setup: 1-2 hours
  - UI Component (Apple Sign-In Button): 1-2 hours
  - Authentication Logic Integration: 2-3 hours
  - Testing & Debugging (iOS device required): 2-3 hours
- **Pessimistic**: 16 hours
- **Final PERT Estimate: 10.2 hours**

---


## 🧪 Post-analysis: Story Set Review

After analyzing all stories, I've identified the following optimizations and observations:

**Overlaps and Dependencies:**
- AUTH-MOB-001, AUTH-MOB-002, and AUTH-MOB-007 share backend user creation logic and can reuse validation components
- AUTH-MOB-003 reuses OAuth setup from AUTH-MOB-002 and AUTH-MOB-007 for social login
- AUTH-MOB-006 (session management) is a dependency for all other authentication stories
- AUTH-MOB-002 and AUTH-MOB-007 share similar OAuth integration patterns with Firebase Auth

**Consistency Improvements:**
- All stories maintain consistent error handling patterns
- Session management approach is unified across registration, login, and logout flows
- OAuth implementation is shared between Google and Apple registration and login stories

**Scope Clarifications:**
- Email verification (AUTH-MOB-004) may be optional for MVP based on requirements analysis
- Password reset flow (AUTH-MOB-005) could use Firebase Auth default implementation to reduce scope

**No conflicts or duplications were identified.** Stories are properly scoped and complementary.

---

## 📌 Stories with High Risk or Pending Decisions

- **AUTH-MOB-001**: Missing wireframe details for name fields, uncertain email verification requirements
- **AUTH-MOB-002**: Google OAuth configuration complexity with Expo + Firebase
- **AUTH-MOB-004**: No wireframe, unclear if email verification required for MVP
- **AUTH-MOB-005**: No wireframes, Firebase Auth vs custom implementation pending
- **AUTH-MOB-006**: Session timeout policy undefined, logout UI location unclear
- **AUTH-MOB-007**: Apple Sign-In requires iOS device testing, Apple Developer account setup, privacy feature handling

---

## 📊 Epic Estimation Summary

To be completed manually:

- Total user stories: **7**
- Stories with high uncertainty: **5** (AUTH-MOB-001, AUTH-MOB-002, AUTH-MOB-004, AUTH-MOB-005, AUTH-MOB-007)
- Stories pending confirmation: **6**

### Manual 3-point Estimation for Epic (PERT)

```
- Optimistic: 33.5 hours
- Realistic: 57 hours  
- Pessimistic: 94 hours
- Final PERT Estimate: 59.25 hours
```