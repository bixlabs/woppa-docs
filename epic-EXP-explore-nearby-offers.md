# 🧩 Epic: Explore Nearby Offers

**KEY**: `EXP`

---

## 📄 Functional Description
This epic enables users to discover nearby promotional offers through an intuitive map interface and list view, without requiring registration. Users can explore 2x1 (1+1) offers from local businesses in two main categories (Gastronomía and Farmacia), filter by category, and access detailed offer information. The epic focuses on providing immediate value to encourage user engagement and eventual registration.

---

## 💻 Target Platform
This epic applies to:
- `mobile`

---

## 🧭 Functional Scope
Main flows and interactions included in this epic:
- Map-based offer exploration with geolocation
- List-based offer browsing as alternative view
- Category filtering between Gastronomía and Farmacia
- Location permission handling with São Paulo fallback
- Offer marker interaction and preview
- Seamless navigation to offer details
- Non-blocking registration call-to-action

---

## 🚫 Out of Scope
Explicitly excluded elements:
- Advanced filtering beyond category (price, distance, rating)
- User favorites or bookmarking features (mentioned for future phases)
- Real-time push notifications for new offers
- Social sharing functionality
- Advanced map features (routing, directions within map)
- Offer comparison tools

---

## 🖼 Wireframes Referenced in Epic
List of wireframes that apply to this epic and the stories that use them.

- `woppa-wireframe-1-mapa.png` → used in: EXP-001, EXP-002, EXP-004, EXP-005
- `woppa-wireframe-2-listado-ofertas.png` → used in: EXP-003, EXP-006
- Both wireframes show registration button (handled by Authentication epic, not user story in this epic)

---

## 🔍 Epic-level Ambiguities

List any unclear, undefined, or mismatched areas affecting the epic as a whole.

- 🔁 **Undefined logic**: Map marker clustering behavior when multiple offers exist at same location
- 📊 **Business decision pending**: Exact radius definition for "descuentos cerca" counter
- 📋 **Missing validation rules**: Specific coordinates for São Paulo default location
- 🧩 **External dependency unclear**: Google Maps API integration specifics and rate limits
- ⚠️ **Uncovered edge case**: Behavior when location services are disabled system-wide vs app-level
- 🧭 **Mismatch between document and wireframe**: Requirements mention expansion/contraction of search radius but wireframe doesn't show this control
- 🔄 **UX flow clarification needed**: Wireframes show "Obtener oferta" in exploration views but should be "Ver detalle" to avoid confusion with actual purchase action

---

## 🧵 User Stories

---

### 🔹 `EXP-001` – Map View with Geolocation

**Summary**:  
Display an interactive map centered on user's location with fallback to São Paulo when location access is denied.

**Justification**:  
Provides immediate visual context of nearby offers, reducing friction by not requiring registration upfront.

**User Story**:  
"As a user, I want to see a map of my area when I open the app, so that I can immediately discover nearby offers without any barriers."

**🎯 Objective**:  
User sees a functional map interface that automatically centers on their location or provides a sensible default.

**⛓ Dependencies**:  
Google Maps API integration, device location services

**✅ Acceptance Criteria**:
- App requests location permission on first map access
- If permission granted, map centers on user's current location
- If permission denied, map centers on São Paulo (specific coordinates TBD)
- Map displays urban grid optimized for promotion identification
- Location permission can be changed and map updates accordingly

**🧰 Technical Tasks**:
- Integrate Google Maps SDK for mobile
- Implement location permission request flow
- Set up São Paulo default coordinates configuration
- Create map styling for urban promotion display
- Handle location permission state changes
- Implement map loading states and error handling
- Add basic performance optimizations for MVP: debounce offer fetching during map movements, load offers only for visible map bounds

**⚙️ External Setup / Config Required**
- Google Maps API key setup
- Google Cloud Console project configuration
- Location services permissions in app manifest

**❗ Pending Confirmations**
- Exact coordinates for São Paulo default location center point
- Specific map styling preferences and branding elements
- Debounce timing for offer fetching during map movements (recommended: 300-500ms)

**📝 Notes & Observations**
- Requirements mention expanding/contracting search radius but wireframe doesn't show this control - may be future enhancement
- Interactive map approach chosen for familiar UX (similar to Google Maps/Uber) with minimal performance optimizations for MVP
- Advanced optimizations like preventing map re-initialization can be addressed in future phases when usage scales

**🖼 Wireframe Reference**
- Exists: Yes
- Filename: woppa-wireframe-1-mapa.png

---

### 🔹 `EXP-002` – Display Offers as Map Markers

**Summary**:  
Show promotional offers as categorized markers on the map with clustering support for locations with multiple offers.

**Justification**:  
Visual representation of offers allows users to quickly identify opportunities in their area and understand offer density.

**User Story**:  
"As a user, I want to see offers displayed as clear icons on the map, so that I can quickly identify what types of promotions are available nearby."

**🎯 Objective**:  
All active offers are visible as categorized markers with clear visual distinction and clustering when needed.

**⛓ Dependencies**:  
Backend API for offer data, map implementation from EXP-001

**✅ Acceptance Criteria**:
- Offers display as circular icons with category-specific colors
- Gastronomía offers use pink (#E573E2) with fork/knife icon
- Farmacia offers use green (#3AD4AC) with medical icon
- Markers show number when multiple offers exist at same location
- Markers are clickable and responsive to user interaction
- Map handles up to 100+ markers without performance degradation
- Markers update when moving map to new areas

**🧰 Technical Tasks**:
- Design and implement custom map marker components
- Create clustering logic for multiple offers at same location
- Implement category-specific marker styling
- Set up real-time offer data fetching from backend API
- Add marker interaction handling
- Implement marker clustering for performance
- Create marker animations for better UX
- Add map bounds-based offer loading with debounce to prevent excessive offer API calls

**⚙️ External Setup / Config Required**
- Backend API endpoints for offer data retrieval
- Image assets for category icons
- Map marker clustering configuration

**❗ Pending Confirmations**
- Exact clustering distance threshold for grouping offers
- Behavior when cluster numbers exceed 2 digits
- Whether to show inactive/expired offers with different styling

**📝 Notes & Observations**
- Wireframe shows numbered markers but clustering logic needs definition
- Icon design should be accessible and recognizable at small sizes
- Debounced offer fetching prevents excessive backend API calls when user moves map quickly
- Advanced Google Maps cost optimizations can be addressed in future phases when usage scales

**📉 PERT Estimation Candidate**
```
PERT:
- Optimistic: Clustering behavior well-defined, standard marker implementation
- Realistic: Some custom clustering requirements, performance optimization needed
- Pessimistic: Complex clustering requirements, significant performance challenges
Justification: Clustering behavior and performance requirements have uncertainties that could significantly impact implementation complexity.
```

**🖼 Wireframe Reference**
- Exists: Yes
- Filename: woppa-wireframe-1-mapa.png

---

### 🔹 `EXP-003` – Offer List View

**Summary**:  
Display offers in a vertical list format as an alternative to map view, showing key offer information in easily scannable cards.

**Justification**:  
Provides alternative interface for users who prefer list browsing or have map performance issues.

**User Story**:  
"As a user, I want to see offers in a list format, so that I can quickly scan through available promotions without using the map interface."

**🎯 Objective**:  
Complete list view with offer cards showing all essential information and clear call-to-action.

**⛓ Dependencies**:  
Backend API for offer data, offer detail navigation

**✅ Acceptance Criteria**:
- List displays offers in vertical card format
- Each card shows business image (or placeholder), business name, category icon, urgency label (if applicable), conditions, 1+1 benefit label, and "Ver detalle" button
- Cards are ordered by proximity and relevance
- List supports infinite scroll or pagination
- Cards are tappable to access offer details
- List view maintains filter state from map view
- Images load efficiently with proper placeholders

**🧰 Technical Tasks**:
- Design and implement offer card component
- Create list view layout and scrolling behavior
- Implement image loading with placeholders and caching
- Add infinite scroll or pagination logic
- Integrate with offer data API (reuse cached data from map when possible)
- Implement card interaction and navigation
- Add loading states and error handling
- Optimize list performance for large offer sets with image lazy loading

**⚙️ External Setup / Config Required**
- Image CDN configuration for offer photos
- Default placeholder images for missing business photos

**❗ Pending Confirmations**
- Maximum character limit for business descriptions in cards
- Exact sorting algorithm for offer ordering
- Placeholder image strategy when businesses don't provide photos

**📝 Notes & Observations**
- Wireframe shows "2x1" but requirements specify "1+1" - using "1+1" per business decisions
- Wireframe shows "Obtener oferta" button but should be "Ver detalle" to avoid confusion - actual offer acquisition happens in Offer Details screen
- Image quality and loading performance critical for user experience
- Urgency labels are managed by Woppa team, not merchants

**🖼 Wireframe Reference**
- Exists: Yes
- Filename: woppa-wireframe-2-listado-ofertas.png

---

### 🔹 `EXP-004` – Category Filtering

**Summary**:  
Enable users to filter offers by category (Gastronomía and Farmacia) across both map and list views.

**Justification**:  
Allows users to focus on specific types of offers they're interested in, improving relevance and reducing cognitive load.

**User Story**:  
"As a user, I want to filter offers by category, so that I can focus on the type of businesses I'm interested in visiting."

**🎯 Objective**:  
Functional filter system that works consistently across map and list views with clear visual feedback.

**⛓ Dependencies**:  
Map markers (EXP-002), list view (EXP-003)

**✅ Acceptance Criteria**:
- Filter buttons appear at top of both map and list views
- Gastronomía and Farmacia filters can be toggled independently
- Both categories active by default (show all offers)
- Filter state persists when switching between map and list views
- Visual indicators show which filters are active
- Offer counter updates to reflect filtered results
- Filtering happens in real-time without page refresh

**🧰 Technical Tasks**:
- Implement category filter UI components
- Create filter state management system
- Add real-time filtering logic for map markers
- Add real-time filtering logic for list view
- Implement filter persistence across view switches
- Update offer counter based on active filters
- Add filter visual feedback and transitions
- Implement filter reset functionality if needed

**⚙️ External Setup / Config Required**
- None specific to this story

**❗ Pending Confirmations**
- Whether filters should be exclusive (radio buttons) or inclusive (checkboxes) - requirements suggest both can be active
- Default state when user returns to app - all categories or last selected state

**📝 Notes & Observations**
- Requirements clarify both categories can be active simultaneously
- Filter state should be maintained during session but may reset between app launches
- Visual design should make active/inactive states clearly distinguishable

**🖼 Wireframe Reference**
- Exists: Yes
- Filename: woppa-wireframe-1-mapa.png

---

### 🔹 `EXP-005` – Offer Marker Interaction

**Summary**:  
Enable users to tap map markers to view basic offer information and navigate to full offer details.

**Justification**:  
Provides quick offer preview without leaving map context while offering path to detailed information.

**User Story**:  
"As a user, I want to tap on offer markers, so that I can quickly see basic offer information and decide if I want to learn more."

**🎯 Objective**:  
Smooth interaction flow from marker tap to offer preview to optional detailed view.

**⛓ Dependencies**:  
Map markers (EXP-002), offer details screen (from Offer Redemption epic)

**✅ Acceptance Criteria**:
- Tapping marker opens preview showing business name and offer type
- Preview includes "Ver detalle" button to navigate to full offer details
- Preview can be dismissed by tapping outside or close button
- For clustered markers, shows list of offers at that location with individual "Ver detalle" buttons
- Preview loads within 1 second of marker tap
- Preview works for both single offers and clustered offers
- Smooth animations for preview appearance/dismissal

**🧰 Technical Tasks**:
- Design and implement marker preview component (modal/tooltip/bottom sheet)
- Add marker tap event handling
- Create clustered marker interaction logic
- Implement preview-to-details navigation
- Add preview dismissal behavior
- Create preview loading states
- Implement smooth preview animations
- Handle edge cases for preview positioning

**⚙️ External Setup / Config Required**
- None specific to this story

**❗ Pending Confirmations**
- Preview format: modal, tooltip, or bottom sheet
- Information included in preview vs full details
- Behavior for clustered markers with many offers

**📝 Notes & Observations**
- Requirements mention tooltip/modal options but don't specify preference
- Preview should use "Ver detalle" button instead of "Obtener oferta" for clear UX flow - actual offer acquisition happens in Offer Details screen
- Need to balance information shown vs maintaining map context
- Clustered marker interaction may need special handling

**📉 PERT Estimation Candidate**
```
PERT:
- Optimistic: Simple modal implementation with basic preview
- Realistic: Need to handle clustering and choose optimal preview format
- Pessimistic: Complex clustered marker interactions and multiple preview formats
Justification: Preview format and clustered marker behavior not clearly defined, affecting implementation complexity.
```

**🖼 Wireframe Reference**
- Exists: Yes
- Filename: woppa-wireframe-1-mapa.png

---

### 🔹 `EXP-006` – Navigation Between Map and List Views

**Summary**:  
Provide seamless navigation between map and list views while maintaining filter state and user context.

**Justification**:  
Offers users flexibility to choose their preferred browsing method without losing their current session state.

**User Story**:  
"As a user, I want to switch between map and list views, so that I can browse offers in the format that works best for me at the moment."

**🎯 Objective**:  
Smooth view switching with preserved state and consistent user experience across both views.

**⛓ Dependencies**:  
Map view (EXP-001), list view (EXP-003), category filtering (EXP-004)

**✅ Acceptance Criteria**:
- Clear navigation options to switch between map and list views
- Filter state persists when switching views
- Location context maintained between views
- View switch happens within 1 second
- Visual indicators show current active view
- Smooth transitions between views
- Both views show same offer dataset

**🧰 Technical Tasks**:
- Implement view navigation UI (tabs, buttons, or bottom navigation)
- Create state management for view switching
- Ensure filter state persistence across views
- Implement smooth view transitions
- Add loading states for view switches
- Optimize data sharing between views
- Handle edge cases for view switching

**⚙️ External Setup / Config Required**
- None specific to this story

**❗ Pending Confirmations**
- Navigation UI pattern: tabs, floating action button, or menu option
- Whether views should share data or load independently

**📝 Notes & Observations**
- Not explicitly shown in wireframes but implied by having two separate views
- Need to ensure data consistency between views
- Performance optimization important for smooth switching

**🖼 Wireframe Reference**
- Exists: Partially (shows both views separately)
- Filename: woppa-wireframe-1-mapa.png and woppa-wireframe-2-listado-ofertas.png

---

### 🔹 `EXP-007` – Location Services Management

**Summary**:  
Handle various location permission states and provide user controls for location access and updates.

**Justification**:  
Ensures robust handling of location services across different user preferences and device states.

**User Story**:  
"As a user, I want the app to handle my location preferences gracefully, so that I can control my privacy while still discovering relevant offers."

**🎯 Objective**:  
Comprehensive location handling that respects user preferences and provides clear options for location management.

**⛓ Dependencies**:  
Map view (EXP-001)

**✅ Acceptance Criteria**:
- Handle location permission denied gracefully with clear fallback
- Show appropriate messaging when location is disabled
- Provide option to enable location from within app
- Include floating button to return to current location
- Button shows different states for location enabled/disabled
- Handle location changes when user moves
- Respect user choice to keep location disabled

**🧰 Technical Tasks**:
- Implement comprehensive location permission handling
- Create location state management system
- Add floating action button for location control
- Implement location update logic
- Handle all permission states (granted, denied, never ask again)
- Add appropriate user messaging for each state
- Implement location re-centering functionality
- Handle background/foreground location updates

**⚙️ External Setup / Config Required**
- Location permissions configuration in app manifest
- Background location handling if needed

**❗ Pending Confirmations**
- Whether app should continue requesting location after denial
- Background location update frequency and battery impact
- Specific messaging for different location permission states

**📝 Notes & Observations**
- Requirements mention floating button for returning to current location
- Need to balance location accuracy with battery consumption
- Privacy considerations important for user trust

**📉 PERT Estimation Candidate**
```
PERT:
- Optimistic: Standard location handling with simple state management
- Realistic: Need comprehensive permission handling and user messaging
- Pessimistic: Complex permission states and edge cases require extensive handling
Justification: Location permission handling can be complex with many edge cases and platform-specific behaviors.
```

**🖼 Wireframe Reference**
- Exists: Partially (shows location icon but not detailed states)
- Filename: woppa-wireframe-1-mapa.png

---

## 🔗 External Dependencies (Not Stories in This Epic)

**Registration Call-to-Action Button**: Both map and list views include a "Registrarse" button in the top-right corner that navigates to the Authentication epic. This is a UI reference only - the registration functionality belongs to the Authentication epic.

- Button should show friendly text (e.g., "Quiero registrarme" instead of "Registrarse")
- For logged-in users, shows "Mi cuenta" instead
- Button doesn't block exploration functionality
- Navigation to registration/login flow handled by Authentication epic

---

## 🧪 Post-analysis: Story Set Review

After analyzing all stories, I've identified the following:

**No overlapping stories detected** - Each story has a distinct functional scope.

**Logical grouping confirmed**:
- Foundation stories (EXP-001, EXP-002, EXP-003) establish core functionality
- Interactive stories (EXP-004, EXP-005, EXP-006) build on foundation with user interactions  
- Supporting story (EXP-007) enhances the experience

**Dependencies are well-defined** and create a logical implementation sequence.

**Story coherence is strong** - All stories contribute to the epic's objective of enabling offer exploration without registration barriers.

**UX Flow Clarification Identified**: During analysis, it was identified that wireframes show "Obtener oferta" buttons in multiple places (list view and marker previews) which could confuse users. The correct flow should be:
- **Exploration views** (list cards, marker previews): "Ver detalle" button → navigates to offer details
- **Offer Details screen** (Offer Redemption epic): "Obtener oferta" button → initiates purchase process

This ensures a clear user journey: Explore → Review Details → Obtain Offer.

---

## 📌 Stories with High Risk or Pending Decisions

Stories in this epic that include pending confirmations or PERT estimation:
- **EXP-002** (Display Offers as Map Markers) - PERT candidate due to clustering behavior uncertainty
- **EXP-005** (Offer Marker Interaction) - PERT candidate due to undefined preview format
- **EXP-007** (Location Services Management) - PERT candidate due to complex permission handling

Stories with multiple pending confirmations:
- **EXP-001** (Map View with Geolocation) - Default coordinates and performance requirements
- **EXP-002** (Display Offers as Map Markers) - Clustering behavior and performance thresholds
- **EXP-003** (Offer List View) - Sorting algorithm and image handling
- **EXP-005** (Offer Marker Interaction) - Preview format and clustered marker behavior

---

## 📊 Epic Estimation Summary

To be completed manually:

- Total user stories: **7**
- Stories with high uncertainty: **3**
- Stories pending confirmation: **6**

### Manual 3-point Estimation for Epic (PERT)

```
- Optimistic: [To be estimated based on individual story estimates]
- Realistic: [To be estimated based on individual story estimates]  
- Pessimistic: [To be estimated based on individual story estimates]
```