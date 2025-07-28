# 🧩 Epic: Mobile Account Management

**KEY**: `ACC-MOB`

---

## 📄 Functional Description
This epic enables registered users to manage their account information, view their purchase history, configure app settings, and access their purchased coupons through a comprehensive account management system on the mobile application.

---

## 💻 Target Platform
This epic applies to:
- `mobile`

---

## 🧭 Functional Scope
Main flows and interactions included in this epic:
- View personal profile information (read-only)
- Access comprehensive purchase history with offer status tracking and coupon code access
- Basic support access for account management (LGPD compliance)

---

## 🚫 Out of Scope
Explicitly excluded elements:
- Payment method management (deferred to future phase per business decisions)
- Account deletion functionality (only support link provided for LGPD compliance)
- Social sharing of profile or achievements
- Referral program or loyalty points management
- Cross-device synchronization features
- Account settings and notification preferences management
- Favorites management (deferred, pending business confirmation)
- User logout functionality (covered in AUTH-MOB epic)

---

## 🖼 Wireframes Referenced in Epic
List of wireframes that apply to this epic and the stories that use them.

- Profile screen: _Not defined_ → used in: ACC-MOB-001, ACC-MOB-004
- Purchase history list screen: _Not defined_ → used in: ACC-MOB-002
- Purchase detail screen: _Not defined_ → used in: ACC-MOB-003

---

## 🔍 Epic-level Ambiguities

- 📐 Missing wireframe: All account management screens lack visual specifications
- 📊 Business decision pending: Data retention policy and user data export requirements
- 🧩 External dependency unclear: Integration requirements with Mercado Pago for payment history
- 🧭 Mismatch between document and wireframe: Requirements mention phone number collection but business decision excludes it

---

## 🧵 User Stories

---

### 🔹 `ACC-MOB-001` – User Profile Display

**Summary**:  
Display user's personal information in a read-only profile view with basic account details stored in our database.

**Justification**:  
Users need to view their account information to verify their identity and ensure data accuracy.

**User Story**:  
"As a registered user, I want to view my profile information, so that I can confirm my account details are correct."

**🎯 Objective**:  
User can access and view their complete profile information in a clear, organized layout.

**⛓ Dependencies**:  
- User authentication system
- User data model with first name, last name, email, profile image URL
- Backend database storing user profile data

**✅ Acceptance Criteria**:
- Display user's first name and last name
- Show registered email address
- Indicate authentication method (email/password or Google)
- Display profile picture if available
- Include navigation back to main app
- Handle missing profile image gracefully with default avatar

**🧰 Technical Tasks**:
- Create profile view screen component
- Implement user data retrieval from backend database
- Implement profile image loading with fallback to default avatar
- Add image caching for profile pictures
- Implement navigation integration
- Add loading states and error handling
- Ensure data privacy compliance (LGPD)

**⚙️ External Setup / Config Required**
- Backend API endpoints for user profile retrieval
- Image storage and CDN for profile pictures
- Default avatar assets

**❗ Pending Confirmations**
- Profile picture size and format requirements
- Data display format preferences (Brazilian Portuguese localization)

**📝 Notes & Observations**
- No wireframe available - UI design needs to be created
- Business decision simplified registration to only first name, last name, email
- Profile images stored as URLs in our database

**🖼 Wireframe Reference**
- Exists: No
- Filename or page: _Not defined_

---

### 🔹 `ACC-MOB-002` – Purchase History List

**Summary**:  
Display a simple list of user's purchased offers with basic status tabs for easy access to active vs completed purchases.

**Justification**:  
Users need to quickly find their active coupons and review their purchase history in a simple, organized way.

**User Story**:  
"As a registered user, I want to view my purchase history in a simple list, so that I can quickly access my active coupons and see my completed purchases."

**🎯 Objective**:  
User can browse their purchases through simple tabs (Active/Completed) and easily access purchase details.

**⛓ Dependencies**:  
- User authentication system
- Purchase data storage with offer snapshot at time of purchase
- Coupon status tracking system

**✅ Acceptance Criteria**:
- Display simple tabs: "Active" and "Completed"
- Show chronological list of purchases within each tab
- Display simple card with: offer/business name (TBD), purchase date, avatar image (TBD: offer or business image)
- Show coupon status indicator on card
- Include purchase date clearly visible
- Tap any purchase card to navigate to detailed view (ACC-MOB-003)
- Handle empty state when user has no purchases in each tab
- Simple pull-to-refresh for updates

**🧰 Technical Tasks**:
- Create purchase history list component with tab navigation
- Implement backend API for purchase data retrieval with offer snapshots
- Design simple card layout with avatar, name, date, and status
- Add tab switching functionality (Active/Completed)
- Add navigation to purchase detail screen
- Implement simple pull-to-refresh mechanism
- Create empty state design for each tab
- Design status indicators for coupon state
- Handle circular avatar images with fallback

**⚙️ External Setup / Config Required**
- Database schema for purchase history with offer snapshots
- Image storage and CDN setup for offer/business images
- Default avatar images for fallback

**❗ Pending Confirmations**
- Whether to show offer name or business name on card
- Whether avatar shows offer image or business image
- Exact status labels to use (Active vs Completed, etc.)
- Card design and information hierarchy

**📝 Notes & Observations**
- No wireframe available - needs simple UI design
- Simplified for MVP - no search, filters, or complex features
- Uses offer snapshot data taken at time of purchase (immutable)
- Purchase confirmation assumed - no payment status checking needed
- Focus on simplicity and quick access to active coupons
- Card design allows for future expansion of displayed information

**🖼 Wireframe Reference**
- Exists: No
- Filename or page: _Not defined_

---

### 🔹 `ACC-MOB-003` – Purchase Detail View

**Summary**:  
Display detailed information for a specific purchase, including business details, coupon code, and redemption options.

**Justification**:  
Users need to access detailed information about their purchases, view and copy coupon codes, and get directions to the business for redemption.

**User Story**:  
"As a registered user, I want to view the complete details of a specific purchase, so that I can access my coupon code, get business information, and navigate to the location for redemption."

**🎯 Objective**:  
User can view comprehensive purchase details with easy access to coupon codes and business information for successful redemption.

**⛓ Dependencies**:  
- Purchase history system (ACC-MOB-002)
- Coupon code generation and storage system
- Business/offer data systems
- Google Maps integration

**✅ Acceptance Criteria**:
- Display complete business information: name, address, category, contact details
- Show detailed offer information: type (1+1), description, terms and conditions
- Display large, easy-to-read coupon code with copy-to-clipboard functionality
- Show purchase details: purchase date, price paid, payment method
- Display current status with clear visual indicators: "Active", "Redeemed", "Expired"
- Include expiration date and time remaining (if active)
- Show redemption instructions specific to the business
- Include "Get Directions" button linking to Google Maps with business location
- Display business category icon and offer image
- Handle different coupon states (active, expired, used) with appropriate UI
- Include back navigation to purchase history list

**🧰 Technical Tasks**:
- Create purchase detail screen component
- Implement coupon code display with large, clear formatting
- Add copy-to-clipboard functionality for coupon codes
- Implement Google Maps integration for directions
- Design status-specific UI (active, expired, used states)
- Add business information display layout
- Handle deep linking to specific purchase details
- Add back navigation to purchase history
- Create responsive layout for all purchase information
- Implement image loading for business and offer photos

**⚙️ External Setup / Config Required**
- Google Maps API integration
- Clipboard API access permissions
- Deep linking configuration for purchase details

**❗ Pending Confirmations**
- Copy-to-clipboard behavior and user feedback
- Specific redemption instructions format
- Business contact information to display (phone, Instagram, etc.)

**📝 Notes & Observations**
- No wireframe available - needs comprehensive UI design for detail view
- Must handle all coupon states gracefully with clear visual feedback
- Consider accessibility for coupon code display and copying
- Integration point between purchase tracking and offer redemption

**🖼 Wireframe Reference**
- Exists: No
- Filename or page: _Not defined_

---

### 🔹 `ACC-MOB-004` – Support Access for Account Deletion

**Summary**:  
Provide users with access to support channel for account deletion requests to comply with LGPD regulations.

**Justification**:  
Users must have a way to request account deletion to comply with Brazilian LGPD data protection regulations.

**User Story**:  
"As a registered user, I want to access support to request account deletion, so that I can exercise my data privacy rights under LGPD."

**🎯 Objective**:  
User can easily contact support to request account deletion and data removal from their profile area.

**⛓ Dependencies**:  
- User authentication system
- Support system integration (WhatsApp)
- LGPD compliance framework

**✅ Acceptance Criteria**:
- Display "Delete Account" or "Contact Support" option in profile area
- Clear messaging about account deletion process
- Direct link to WhatsApp support channel for deletion requests
- Include brief explanation of data deletion rights under LGPD
- Display app version information

**🧰 Technical Tasks**:
- Add account deletion request link to profile screen
- Integrate WhatsApp support contact functionality
- Create clear messaging about deletion process
- Add LGPD compliance information display
- Design support contact interface

**⚙️ External Setup / Config Required**
- WhatsApp Business API setup for support
- LGPD compliance procedures for account deletion
- Support team training for deletion requests

**❗ Pending Confirmations**
- Exact support contact method (WhatsApp vs email vs form)
- Messaging and wording for account deletion option
- LGPD compliance procedures for handling deletion requests

**📝 Notes & Observations**
- Simplified to focus only on account deletion support
- Complies with Brazilian LGPD data protection regulations
- WhatsApp integration mentioned in requirements for support
- Account deletion handled through support rather than automated feature

**🖼 Wireframe Reference**
- Exists: No
- Filename or page: _Not defined_

---

## 🧪 Post-analysis: Story Set Review

After analyzing all stories in this epic, I've identified the following considerations:

**Story Dependencies:**
- All stories depend on user authentication system - this should be implemented first
- ACC-MOB-003 (Purchase Detail) depends on ACC-MOB-002 (Purchase History List) for navigation
- ACC-MOB-002 and ACC-MOB-003 form a cohesive purchase management flow
- ACC-MOB-004 provides minimal support integration needed for LGPD compliance

**Missing Integration Points:**
- Profile display (ACC-MOB-001) needs coordination with registration/authentication epic
- Purchase detail (ACC-MOB-003) needs integration with business/offer data systems and Google Maps
- Support system integration needs WhatsApp Business API setup
- Backend needs to implement offer snapshot storage at time of purchase (immutable data)

**User Flow Optimization:**
- Separated purchase list from purchase detail for better UX and maintainability
- ACC-MOB-002 simplified to basic tabs (Active/Completed) for MVP
- ACC-MOB-002 → ACC-MOB-003 creates logical navigation flow
- Profile (ACC-MOB-001) serves as entry point to account management features
- Support access (ACC-MOB-004) provides LGPD compliance without complexity

**Consistency Improvements:**
- All stories need consistent error handling and loading states
- Navigation patterns should be unified across all account management screens
- Empty states need consistent messaging and visual design
- Status indicators should be consistent between list and detail views

**Story optimization performed:**
- Separated purchase history list from purchase detail for better UX
- Simplified purchase list to basic card design with minimal information
- Implemented offer snapshot approach (immutable data at time of purchase)
- Eliminated Mercado Pago webhook dependency for purchase list (purchases assumed confirmed)
- Simplified support access to focus only on account deletion
- Removed favorites management (deferred pending business confirmation)
- Removed account settings (not needed for MVP)
- Removed logout functionality (covered in AUTH-MOB epic)

---

## 📌 Stories with High Risk or Pending Decisions

List all stories in this epic that include:
- ❗ Confirmations pending: ACC-MOB-001, ACC-MOB-002, ACC-MOB-003, ACC-MOB-004
- 📉 PERT estimation block: None (all stories now have standard complexity)
- Any ambiguity label: All stories (missing wireframes)

**High-risk stories requiring immediate attention:**
1. **ACC-MOB-003** - Purchase Detail View: Complex integration with business data, Google Maps, and coupon systems

**Medium risk:**
1. **ACC-MOB-004** - Support Access: LGPD compliance requirements and WhatsApp integration setup

**Lower risk:**
1. **ACC-MOB-001** - Profile Display: Simplified with user data stored in our database, no external API dependencies
2. **ACC-MOB-002** - Purchase History List: Simplified to basic tabs and list, no complex integrations needed

---

## 📊 Epic Estimation Summary

To be completed manually:

- Total user stories: 4
- Stories with high uncertainty: 1
- Stories pending confirmation: 4

### Manual 3-point Estimation for Epic (PERT)

```
- Optimistic: 36h
- Realistic: 60h
- Pessimistic: 88h
```

**Estimation factors:**
- All screens lack wireframes requiring additional design time
- Purchase detail view requires complex integration with business data and Google Maps
- LGPD compliance requirements for Brazilian market
- Copy-to-clipboard functionality
- Navigation flow between purchase list and detail views
- Simplified purchase list with basic tabs reduces complexity significantly
- User data stored in our database eliminates external API dependencies for profile display
- No payment status integration needed for purchase list (purchases assumed confirmed)