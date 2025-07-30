# 🧩 Epic: Business Authentication

**KEY**: `BIZ-AUTH-WEB`

---

## 📄 Functional Description
Simple business authentication system for the web panel, enabling Brazilian businesses to register, login, and manage basic authentication states. Handles business registration with pending approval workflow and basic session management through Firebase Auth.

---

## 💻 Target Platform
This epic applies to:
- `web-panel`

---

## 🧭 Functional Scope
Main flows and interactions included in this epic:
- Business registration with basic validation (email/password + business info)
- Registration state: pending approval from WOPPA staff
- Business login with approval status handling
- Password recovery (forgot password)
- Basic logout functionality
- Simple pending approval status display

---

## 🚫 Out of Scope
Explicitly excluded elements:
- WOPPA staff approval/rejection workflows (covered in BIZ-MODERATION-WEB)
- Complex profile management (handled in separate epic if needed)
- Email verification UI (uses Firebase Auth default)
- Session management complexity (handled by Firebase Auth)
- Terms & conditions management beyond simple checkbox
- Advanced authentication features (2FA, etc.)

---

## 🖼 Wireframes Referenced in Epic
List of wireframes that apply to this epic and the stories that use them.

- No specific wireframes exist for business authentication screens
- Related wireframe: `woppa-wireframe-comerciante-1.png` (promotion creation, not authentication)

---

## 🔍 Epic-level Ambiguities

- 📐 Missing wireframe: No wireframes exist for business registration or login screens
- 📊 Business decision pending: Exact CNPJ validation rules and error messages in Portuguese
- 📋 Missing validation rules: Specific format requirements for business phone numbers
- 🔁 Undefined logic: Exact messaging for pending approval state

---

## 🧵 User Stories

---

### 🔹 `BIZ-AUTH-WEB-001` – Business Registration

**Summary**:  
Enable businesses to register with basic information using Firebase Auth, leaving them in pending approval state.

**Justification**:  
Businesses need to register before they can access the platform. Registration creates account and requires WOPPA staff approval.

**User Story**:  
"As a business owner, I want to register my business on Woppa with basic information, so that I can request access to the platform."

**🎯 Objective**:  
Create Firebase Auth account with business information and set pending approval status.

**⛓ Dependencies**:  
- Firebase Auth email/password provider
- Google Maps API for address validation
- CNPJ validation service for Brazilian tax IDs
- Firestore for business data storage

**✅ Acceptance Criteria**:
- Registration form includes: business name, responsible person name/surname, commercial phone, financial phone (optional), email, CNPJ, address, password
- Email and password handled by Firebase Auth createUserWithEmailAndPassword
- Address field integrates with Google Places API
- CNPJ field validates Brazilian tax ID format
- All fields have real-time validation
- Terms & conditions checkbox is mandatory
- Registration sets account status to "pending approval" in Firestore
- Success message explains approval process and next steps

**🧰 Technical Tasks**:
- Create responsive React business registration form
- Integrate Firebase Auth createUserWithEmailAndPassword
- Implement real-time field validation (email, phone, CNPJ)
- Integrate Google Places API for address autocomplete
- Implement Brazilian CNPJ validation logic
- Store additional business data in Firestore with "pending" status
- Add terms & conditions checkbox validation
- Create registration success page with approval messaging
- Add Firebase error handling with Portuguese translations

**⚙️ External Setup / Config Required**
- Firebase project setup with Auth enabled
- Google Places API key configuration
- Brazilian CNPJ validation service
- Firestore security rules for business data

**❗ Pending Confirmations**
- Exact CNPJ validation rules and error messages in Portuguese
- Specific approval process messaging for users
- Required vs optional fields confirmation

**📝 Notes & Observations**
- No wireframe exists - UI design needed
- Focus on MVP simplicity
- Portuguese language for Brazil market

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 8 hours
- Realistic: 14.5  hours
    - Frontend UI: ~4h
    - Frontend Logic: ~3h
    - Integration: ~ 3h (google places, our backend, and firebase)
    - Backend: ~3h 
    - Manual Testing: ~1.5h
- Pessimistic: 18 hours
- Final PERT Estimate: 14 h
```

**🖼 Wireframe Reference**
- Exists: No
- Registration form design needed

---

### 🔹 `BIZ-AUTH-WEB-002` – Business Login with Approval Status

**Summary**:  
Enable businesses to login and display their approval status, blocking access if not approved.

**Justification**:  
Businesses need to login to access the platform, but must see their approval status and be blocked from main functionality until approved.

**User Story**:  
"As a business owner, I want to login to my account and see my approval status, so that I know if I can access the platform features."

**🎯 Objective**:  
Provide Firebase Auth login with approval status check and appropriate UI state.

**⛓ Dependencies**:  
- Firebase Auth system
- Business registration system (BIZ-AUTH-WEB-001)
- Firestore for approval status storage

**✅ Acceptance Criteria**:
- Login form with email and password using Firebase Auth signInWithEmailAndPassword
- After successful login, check approval status from Firestore
- If status is "pending": show alert/banner with yellow/orange color explaining account is under review
- If status is "approved": allow full platform access
- If status is "rejected": show alert/banner with red color explaining rejection with contact info
- Clear Firebase Auth error messages for invalid credentials in Portuguese
- Simple colored alerts/banners for approval status feedback (not complex UI)
- Session persistence handled by Firebase Auth

**🧰 Technical Tasks**:
- Create responsive React login form
- Implement Firebase Auth signInWithEmailAndPassword
- Add form validation and error handling
- Create approval status checking logic after login
- Build simple alert/banner components for different approval states (colored alerts)
- Create pending approval dashboard view
- Implement redirect logic based on approval status
- Add Firebase Auth error handling with Portuguese translations

**⚙️ External Setup / Config Required**
- Firebase Auth configuration
- Firestore read permissions for approval status

**❗ Pending Confirmations**
- Exact messaging for pending/rejected states
- Whether rejected users can resubmit or need to contact support

**📝 Notes & Observations**
- Critical for MVP - blocks unapproved access
- Should integrate with overall dashboard design
- Simple messaging for approval states

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 4 hours
- Realistic: 6.75 hours
    - Frontend UI: ~1.5h
    - Frontend Logic: ~1h
    - Integration: ~ 1h
    - Backend: ~2.5h (middleware implementation and status endpoint)
    - Manual Testing: ~0.75h
- Pessimistic: 10 hours
- Final PERT Estimate: 6.83 h
```

**🖼 Wireframe Reference**
- Exists: No
- Login form and approval status screens design needed

---

### 🔹 `BIZ-AUTH-WEB-003` – Password Recovery

**Summary**:  
Enable businesses to recover their password using Firebase Auth with custom initial UI.

**Justification**:  
Businesses need to recover access to their accounts when they forget passwords.

**User Story**:  
"As a business owner, I want to reset my password when I forget it, so that I can regain access to my account."

**🎯 Objective**:  
Provide password recovery using Firebase Auth sendPasswordResetEmail with custom initial UI.

**⛓ Dependencies**:  
- Firebase Auth system
- Firebase Auth email templates

**✅ Acceptance Criteria**:
- "Forgot password" link on login form
- Custom forgot password form requesting email
- Uses Firebase Auth sendPasswordResetEmail method
- Success message explains next steps (check email)
- Error handling for non-existent emails
- Firebase Auth handles email delivery and reset flow (uses default Firebase email template)
- User returns to login after successful reset

**🧰 Technical Tasks**:
- Add "Forgot Password" link to login form
- Create forgot password form component
- Implement Firebase Auth sendPasswordResetEmail
- Add email validation and error handling
- Create success/confirmation messaging
- Use default Firebase Auth email templates (no custom configuration needed)
- Add Portuguese translations for error messages

**⚙️ External Setup / Config Required**
- Firebase Auth password reset configuration (uses default templates)
- No custom email template setup required for MVP

**❗ Pending Confirmations**
- Specific success messaging preferences for forgot password flow

**📝 Notes & Observations**
- Leverages Firebase Auth default email templates
- Only need custom UI for initial forgot password form
- Keep messaging simple and clear for MVP

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 1.5 hours
- Realistic: 2.5 hours
  - Frontend UI: Input + button - 0.5h
  - Frontend logic: Validate email, handle button and send information - 0.5h
  - Integration: Firebase auth and show messages - 0.5h
  - Backend: activate email on firebase auth - 0.5h
  - Testing manual: 0.5h
- Pessimistic: 4 hours
- Final PERT Estimate: 2.6h
```

**🖼 Wireframe Reference**
- Exists: No
- Forgot password form design needed

---

### 🔹 `BIZ-AUTH-WEB-004` – Business Logout

**Summary**:  
Enable businesses to securely logout using Firebase Auth signOut.

**Justification**:  
Businesses need to securely end their session, especially on shared devices.

**User Story**:  
"As a business owner, I want to logout of my account, so that my session is securely ended."

**🎯 Objective**:  
Provide simple logout functionality using Firebase Auth with proper session cleanup.

**⛓ Dependencies**:  
- Firebase Auth system
- Login system (BIZ-AUTH-WEB-002)

**✅ Acceptance Criteria**:
- Logout button/link available when authenticated
- Uses Firebase Auth signOut() method
- Clears authentication state properly
- Redirects to login page after logout
- Works consistently across all authenticated pages

**🧰 Technical Tasks**:
- Add logout button to authenticated UI
- Implement Firebase Auth signOut functionality
- Add logout confirmation (optional)
- Implement redirect to login after logout
- Ensure consistent logout access across platform
- Add proper state cleanup in React components

**⚙️ External Setup / Config Required**
- None - uses existing Firebase Auth configuration

**❗ Pending Confirmations**
- Whether logout requires confirmation dialog
- Specific redirect behavior after logout

**📝 Notes & Observations**
- Very straightforward with Firebase Auth
- Should be consistent across all authenticated screens
- Consider logout confirmation for better UX

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 0.75 hours
- Realistic: 1.25 hours
  - Frontend UI: Logout button - 0.25h
  - Frontend logic: Firebase Auth signOut - 0.25h
  - Integration: Firebase Auth signOut - 0.25h
  - Backend: 0h
  - Testing manual: 0.5h
- Pessimistic: 2 hours
- Final PERT Estimate: 1.3h
```

**🖼 Wireframe Reference**
- Exists: No
- Logout button integration design needed

---

## 🧪 Post-analysis: Story Set Review

After analyzing all stories in the epic, I've identified the following observations:

**Dependencies and Flow**:
- Stories flow logically: Registration → Login with Status Check → Password Recovery & Logout
- All stories use Firebase Auth as foundation
- Clean separation of concerns with minimal overlap

**Consistency**:
- All stories use Firebase Auth methods consistently
- Portuguese localization requirements consistent across stories
- Firestore used only for business data and approval status
- Simple MVP approach maintained throughout

**Potential Overlaps**:
- Firebase Auth error handling should use shared error message translations
- Form validation logic can be shared between registration and password recovery
- Approval status checking might be used in other epics

**Scope Adjustments**:
- Epic correctly focused on core authentication only
- Complex profile management excluded appropriately
- Session management handled by Firebase Auth reduces complexity significantly

---

## 📌 Stories with High Risk or Pending Decisions

Stories in this epic that include confirmations pending or high uncertainty:

- **BIZ-AUTH-WEB-001**: Missing wireframes, CNPJ validation rules, approval messaging
- **BIZ-AUTH-WEB-002**: Approval state messaging, rejection resubmission process
- **BIZ-AUTH-WEB-003**: Email template design, success messaging
- **BIZ-AUTH-WEB-004**: Logout confirmation requirements

---

## 📊 Epic Estimation Summary

To be completed manually:

- Total user stories: 4
- Stories with high uncertainty: 4
- Stories pending confirmation: 4

### Manual 3-point Estimation for Epic (PERT)

```
- Optimistic: 14.25h
- Realistic: 25h
- Pessimistic: 34h
- Final PERT Estimate: 24.73 h
```

---