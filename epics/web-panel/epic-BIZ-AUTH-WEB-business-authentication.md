# 🧩 Epic: Business Authentication

**KEY**: `BIZ-AUTH-WEB`

---

## 📄 Functional Description
Complete business authentication system for the web panel, enabling Brazilian businesses to register, login, manage authentication states, view their profile information, and access WhatsApp support. Handles business registration with pending approval workflow, basic session management through Firebase Auth, read-only profile display, and integrated support access throughout the platform.

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
- Business profile display (read-only) for approved merchants
- WhatsApp Business support integration throughout platform

---

## 🚫 Out of Scope
Explicitly excluded elements:
- WOPPA staff approval/rejection workflows (covered in BIZ-MODERATION-WEB)
- Profile editing capabilities (read-only only in this epic, editing in future phase)
- Email verification UI (uses Firebase Auth default)
- Session management complexity (handled by Firebase Auth)
- Terms & conditions management beyond simple checkbox
- Advanced authentication features (2FA, etc.)
- WhatsApp Business API advanced features (using direct links for MVP)
- Support ticket system or complex help features

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
- Backend Fastify API for business data storage

**✅ Acceptance Criteria**:
- Registration form includes: business name, responsible person name/surname, commercial phone, financial phone (optional), email, CNPJ, address, password
- Email and password handled by Firebase Auth createUserWithEmailAndPassword
- Address field integrates with Google Places API
- CNPJ field validates Brazilian tax ID format
- All fields have real-time validation
- Terms & conditions checkbox is mandatory
- Registration sets account status to "pending approval" in Backend Fastify API
- Success message explains approval process and next steps

**🧰 Technical Tasks**:
- Create responsive React business registration form
- Integrate Firebase Auth createUserWithEmailAndPassword
- Implement real-time field validation (email, phone, CNPJ)
- Integrate Google Places API for address autocomplete
- Implement Brazilian CNPJ validation logic
- Store additional business data in Backend Fastify API with "pending" status
- Add terms & conditions checkbox validation
- Create registration success page with approval messaging
- Add Firebase error handling with Portuguese translations

**⚙️ External Setup / Config Required**
- Firebase project setup with Auth enabled
- Google Places API key configuration
- Brazilian CNPJ validation service
- Backend Fastify API endpoints for business data

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
- Backend Fastify API for approval status storage

**✅ Acceptance Criteria**:
- Login form with email and password using Firebase Auth signInWithEmailAndPassword
- After successful login, check approval status from Backend Fastify API
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
- Create approval status checking logic after login using Backend Fastify API
- Build simple alert/banner components for different approval states (colored alerts)
- Create pending approval dashboard view
- Implement redirect logic based on approval status
- Add Firebase Auth error handling with Portuguese translations

**⚙️ External Setup / Config Required**
- Firebase Auth configuration
- Backend Fastify API endpoints for approval status

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

### 🔹 `BIZ-AUTH-WEB-005` – Business Profile Display (Read-Only)

**Summary**:  
Display business profile information in read-only format for approved merchants who have successfully logged in.

**Justification**:  
Approved merchants need to view their complete business information to verify data accuracy and have reference to their stored details.

**User Story**:  
"As an approved business owner, I want to view my complete business profile information, so that I can verify my data is correct and have access to my business details."

**🎯 Objective**:  
Provide a comprehensive read-only view of business profile data retrieved from Backend Fastify API.

**⛓ Dependencies**:  
- Firebase Auth system for authentication
- Business registration system (BIZ-AUTH-WEB-001)  
- Business login system (BIZ-AUTH-WEB-002)
- Backend Fastify API for business data retrieval

**✅ Acceptance Criteria**:
- Display business name clearly as main header
- Show responsible person name (first name + surname)
- Display commercial phone number
- Show financial phone number (if provided during registration)
- Display registered email address
- Show complete business address as stored during registration
- Display Instagram social media link if provided (optional field)
- Show CNPJ (Brazilian tax ID) for reference
- Include account creation date/registration date
- All information displayed in read-only format (no editing capabilities)
- Clean, organized layout with clear sections
- Handle missing optional fields gracefully (show "Not provided" or hide section)
- Responsive design for different screen sizes

**🧰 Technical Tasks**:
- Create responsive React business profile display component
- Implement API call to Backend Fastify to retrieve business profile data
- Design clean layout with proper typography and spacing
- Add sections for personal info, contact info, business info, and administrative info
- Handle optional fields display (Instagram, financial phone)
- Implement loading states during data retrieval
- Add error handling for API failures
- Format CNPJ display with proper Brazilian format (XX.XXX.XXX/XXXX-XX)
- Format phone numbers for Brazilian display
- Add proper date formatting for registration date
- Ensure responsive design across devices

**⚙️ External Setup / Config Required**
- Backend Fastify API endpoint for business profile retrieval (/api/business/profile)
- Proper authentication middleware to verify logged-in business
- Business data model with all required fields

**❗ Pending Confirmations**
- Exact layout and information hierarchy preferences
- Whether to show CNPJ in masked format or full format
- Date format preferences (Brazilian standard: DD/MM/YYYY)
- Handling of optional fields display strategy

**📝 Notes & Observations**
- This is read-only in first phase - editing will be separate epic/story
- Only accessible to approved businesses (login already validates this)
- No wireframe exists - UI design needed
- Should integrate with overall web panel design system
- Focus on clear information presentation

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 3 hours
- Realistic: 5.5 hours
    - Frontend UI: ~2.5h (layout design, responsive sections)
    - Frontend Logic: ~1h (data formatting, optional fields handling)
    - Integration: ~1h (API integration, error handling)
    - Backend: ~0.5h (profile endpoint)
    - Manual Testing: ~0.5h
- Pessimistic: 8 hours
- Final PERT Estimate: 5.5h
```

**🖼 Wireframe Reference**
- Exists: No
- Business profile layout design needed

---

### 🔹 `BIZ-AUTH-WEB-006` – WhatsApp Business Support Integration

**Summary**:  
Provide easy access to WhatsApp Business support throughout the web panel with pre-loaded context messages.

**Justification**:  
Businesses need quick access to support, especially during registration, promotion creation, and validation processes.

**User Story**:  
"As a business owner using the platform, I want to easily contact support when I need help, so that I can get assistance quickly through WhatsApp."

**🎯 Objective**:  
Implement WhatsApp Business integration with context-aware support access throughout the platform.

**⛓ Dependencies**:  
- WhatsApp Business API setup
- Business authentication system (all previous stories)
- Web panel navigation system

**✅ Acceptance Criteria**:
- Display "¿Necesitás ayuda?" button/link visible throughout the platform
- Button should be consistently placed and easily accessible from any screen
- Clicking opens WhatsApp conversation with Woppa's official WhatsApp Business number
- System pre-loads context message: "Hola, soy un comercio de WOPPA y necesito ayuda con..."
- After message is sent, display automatic response: "¡Gracias por contactarnos! Un miembro del equipo WOPPA responderá tu mensaje en breve."
- Integration works from any section of the business panel
- Support button has consistent styling and placement
- WhatsApp opens in new tab/window (doesn't disrupt current session)
- Works on both desktop and mobile devices

**🧰 Technical Tasks**:
- Create reusable "¿Necesitás ayuda?" button component
- Implement WhatsApp Business deep linking functionality
- Configure pre-loaded message with proper URL encoding
- Add support button to main layout/navigation component
- Ensure button is accessible from all authenticated screens
- Style button consistently with platform design
- Test WhatsApp integration across different devices and browsers
- Add proper ARIA labels for accessibility
- Implement tracking/analytics for support button usage (optional)

**⚙️ External Setup / Config Required**
- WhatsApp Business account setup
- Official WhatsApp Business phone number configuration
- WhatsApp Business API setup (if using API vs. direct links)
- Support team training for handling business queries

**❗ Pending Confirmations**
- Exact WhatsApp Business phone number to use
- Specific pre-loaded message text customization
- Button placement preferences (header, sidebar, floating)
- Whether to use WhatsApp API or direct WhatsApp links

**📝 Notes & Observations**
- Should be accessible from registration through all authenticated screens
- Can enhance business satisfaction and reduce friction
- Important for MVP as businesses may need help with platform usage
- Consider floating button vs. integrated button placement

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 2 hours
- Realistic: 3 hours
    - Frontend UI: ~1h (button component, placement)
    - Frontend Logic: ~1h (WhatsApp link generation, message encoding)
    - Integration: ~0.5h (component integration across screens)
    - Backend: ~0h (no backend needed for direct WhatsApp links)
    - Manual Testing: ~0.5h
- Pessimistic: 5 hours
- Final PERT Estimate: 3.2h
```

**🖼 Wireframe Reference**
- Exists: No
- Support button placement and design needed

## 📊 Epic Estimation Summary

Epic totals:

- Total user stories: 6
- Stories with high uncertainty: 6
- Stories pending confirmation: 6

### Manual 3-point Estimation for Epic (PERT)

```
- Optimistic: 19.25h
- Realistic: 33.5h
- Pessimistic: 47h
- Final PERT Estimate: 33.4h
```

---