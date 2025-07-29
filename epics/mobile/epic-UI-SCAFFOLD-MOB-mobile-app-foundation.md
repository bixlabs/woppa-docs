# 🧩 Epic: Mobile App Foundation & UI Scaffolding

**KEY**: `UI-SCAFFOLD-MOB`

---

## 📄 Functional Description
This epic covers the foundational UI components and navigation structure that will be used across all screens in the Woppa mobile app. It provides the core scaffolding infrastructure including app header, drawer navigation, toast notifications, loading systems, and design system setup. This foundational epic enables consistent user experience and developer productivity across all feature epics (Authentication, Explore Offers, Offer Redemption, Account Management).

---

## 💻 Target Platform
This epic applies to:
- `mobile`

---

## 🧭 Functional Scope
Main components and infrastructure included in this epic:
- App header/bar with hamburger menu, location display, and registration button
- Drawer navigation system accessible via hamburger menu
- Navigation system setup using Expo Router for screen transitions
- Global toast notification system for user feedback
- Global loading system for app-wide loading states
- Theme and design system using NativeWind/Tailwind CSS
- Foundation for consistent styling and component reusability

---

## 🚫 Out of Scope
Explicitly excluded elements:
- Feature-specific components (category filters, offer cards, etc.)
- Authentication logic (handled in Authentication epic)
- Screen-specific content and business logic
- Complex animation systems beyond basic transitions
- User profile functionality (handled in Account Management epic)
- Push notification infrastructure
- Advanced theming features (dark mode for MVP)

---

## 🖼 Wireframes Referenced in Epic
List of wireframes that apply to this epic and the stories that use them.

- `woppa-wireframe-1-mapa.png` → used in: UI-SCAFFOLD-MOB-001 (shows app header structure)
- `woppa-wireframe-2-listado-ofertas.png` → used in: UI-SCAFFOLD-MOB-001 (shows app header consistency)
- `woppa-wireframe-4-register.png` → used in: UI-SCAFFOLD-MOB-006 (shows app branding and theme)
- Hamburger menu from wireframes → used in: UI-SCAFFOLD-MOB-002 (drawer navigation)

---

## 🔍 Epic-level Ambiguities

- 🧩 **Navigation Framework**: Confirmed using Expo Router for file-based navigation
- 🎨 **Styling Framework**: Confirmed using NativeWind for Tailwind CSS in React Native
- 📱 **Target React Native Version**: Confirmed 0.80+ per tech stack document
- 🔧 **State Management**: Confirmed using Zustand for UI state management
- 📐 **Missing wireframes**: Drawer menu content not defined in existing wireframes
- 🎯 **Component Library**: Use existing React Native UI libraries (react-native-elements, @react-native-community, etc.)
- 🔄 **Loading Strategy**: Use react-native-loading-spinner-overlay or similar library
- 📢 **Toast Library**: Use react-native-toast-message or react-native-flash-message
- 🚀 **Implementation Philosophy**: Leverage mature libraries instead of custom low-level implementations

---

## 🧵 User Stories

---

### 🔹 `UI-SCAFFOLD-MOB-001` – App Header/AppBar Component

**Summary**:  
Consistent app header component displayed across main application screens with navigation, location, and registration access.

**Justification**:  
Provides unified navigation experience and consistent branding across all app screens while enabling core functionality access.

**User Story**:  
"As a mobile app user, I want a consistent header across main app screens, so that I can easily navigate, see my location, and access registration."

**🎯 Objective**:  
Create reusable header component that provides consistent navigation and branding across the application.

**⛓ Dependencies**:  
Expo Router configuration, geolocation services, authentication navigation.

**✅ Acceptance Criteria**:
- Header component renders consistently across main app screens (map, offers list)
- Hamburger menu icon (≡) opens drawer navigation when tapped
- Location display shows current location with pin icon and proper formatting
- "Registrarse" button navigates cleanly to authentication flow
- Header adapts to different screen sizes and device orientations
- Component styled with NativeWind/Tailwind CSS classes
- Safe area handling works correctly on all devices (notched screens, etc.)
- Header maintains consistent height and spacing across screens

**🧰 Technical Tasks**:
- Create reusable `AppHeader` component with TypeScript
- Implement hamburger menu button with drawer navigation integration
- Add location display component with geolocation integration
- Create "Registrarse" button with authentication navigation
- Add responsive design handling for different screen sizes
- Implement safe area insets for iOS devices with notches
- Style component using NativeWind/Tailwind CSS classes
- Add component prop interface for customization options

**⚙️ External Setup / Config Required**
- NativeWind configuration for Tailwind CSS classes
- Expo Router navigation setup
- Safe area context provider configuration

**❗ Pending Confirmations**
- Final header height and spacing specifications
- Location display format and fallback behavior
- Hamburger icon design details

**📝 Notes & Observations**
- Header is visible in wireframes 1 and 2 with consistent structure
- Location text shows "Mi ubicación Montevideo, Uruguay" in wireframes
- Registration button appears consistently in top right

**🖼 Wireframe Reference**
- Exists: Yes
- Filename: `woppa-wireframe-1-mapa.png`, `woppa-wireframe-2-listado-ofertas.png`

**📊 PERT Estimation**:
- **Optimistic**: 4 hours
- **Realistic**: 6 hours
  - Comments: Using UI library components reduces custom styling work. Standard navigation integration.
    - Frontend UI: ~2h (header layout with UI library components)
    - Frontend Logic: ~2h (navigation integration, location display)
    - Integration: ~1h (Expo Router, geolocation)
    - Backend: ~0h (no backend needed)
    - Manual Testing: ~1h (multiple devices, orientations)
- **Pessimistic**: 8 hours
- **Final PERT Estimate: 6.67 hours**

---

### 🔹 `UI-SCAFFOLD-MOB-002` – Drawer Navigation (Sidebar)

**Summary**:  
Side navigation menu accessible via hamburger icon that provides main app section navigation.

**Justification**:  
Essential navigation pattern for mobile apps that allows access to different app sections without cluttering the main interface.

**User Story**:  
"As a mobile app user, I want a side navigation menu, so that I can access different sections of the app."

**🎯 Objective**:  
Implement functional drawer navigation that provides smooth access to main app sections.

**⛓ Dependencies**:  
Expo Router drawer configuration, gesture handling library, UI state management.

**✅ Acceptance Criteria**:
- Drawer slides open from left when hamburger menu icon is tapped
- Drawer can be closed by tapping outside drawer area or using swipe gesture
- Navigation menu items are clearly visible and easily tappable
- Drawer state is properly managed (open/closed) across app navigation
- Smooth slide animation for drawer open/close transitions
- Navigation items navigate correctly to their target screens
- Drawer content styled with NativeWind/Tailwind CSS classes
- Drawer works consistently across different device sizes

**🧰 Technical Tasks**:
- Configure Expo Router drawer navigation structure
- Create basic drawer content with placeholder navigation items (2-3 dummy links)
- Style drawer content using NativeWind/Tailwind CSS and UI library components
- Test drawer open/close functionality
- Ensure drawer is ready for easy addition of real navigation links in future epics

**⚙️ External Setup / Config Required**
- Expo Router drawer configuration in app layout
- React Native Gesture Handler setup
- Drawer navigation item structure definition

**❗ Pending Confirmations**
- Specific navigation items to include in drawer menu
- Drawer width and visual design specifications
- Navigation item icons and labels

**📝 Notes & Observations**
- Hamburger menu icon visible in wireframes suggests drawer navigation
- Drawer content not defined in existing wireframes - needs design input
- Logout functionality excluded per user request (handled in Account Management epic)

**🖼 Wireframe Reference**
- Exists: Partial
- Note: Hamburger menu icon visible in wireframes 1-2, but drawer content not shown

**📊 PERT Estimation**:
- **Optimistic**: 2 hours
- **Realistic**: 4 hours
  - Comments: Basic drawer setup with placeholder content. Expo Router handles most complexity.
    - Frontend UI: ~1h (basic drawer layout with placeholder items)
    - Frontend Logic: ~1h (basic navigation structure)
    - Integration: ~1h (Expo Router drawer configuration)
    - Backend: ~0h (no backend needed)
    - Manual Testing: ~1h (open/close functionality)
- **Pessimistic**: 6 hours
- **Final PERT Estimate: 5.17 hours**

---

### 🔹 `UI-SCAFFOLD-MOB-003` – Navigation System Setup

**Summary**:  
Core navigation system configuration using Expo Router for seamless screen transitions and app structure.

**Justification**:  
Provides fundamental navigation infrastructure required by all app features and ensures consistent navigation behavior.

**User Story**:  
"As a developer, I want a properly configured navigation system, so that users can navigate between screens smoothly."

**🎯 Objective**:  
Establish robust navigation foundation with drawer, stack, and nested navigation patterns.

**⛓ Dependencies**:  
Expo Router library, React Navigation dependencies, TypeScript configuration.

**✅ Acceptance Criteria**:
- Expo Router is properly configured with app directory structure
- Drawer navigation integrates seamlessly with hamburger menu
- Stack navigation handles screen transitions with proper back button behavior
- Deep linking is supported for authentication and offer flows
- Navigation state is properly managed and persisted
- TypeScript types are defined for all route parameters
- Nested navigation (drawer + stack) works without conflicts
- Navigation performance is smooth on both iOS and Android

**🧰 Technical Tasks**:
- Install and configure Expo Router with latest version
- Set up app directory structure for file-based routing
- Configure drawer + stack navigation pattern integration
- Define TypeScript interfaces for route parameters
- Implement navigation state persistence
- Add deep linking configuration for key app flows
- Set up navigation guards and protection for authenticated routes
- Add navigation performance optimization

**⚙️ External Setup / Config Required**
- Expo Router installation and configuration
- App.json configuration for deep linking
- TypeScript configuration for navigation types

**❗ Pending Confirmations**
- Deep linking URL scheme structure
- Navigation state persistence requirements
- Route protection strategy for authenticated content

**📝 Notes & Observations**
- Expo Router provides file-based routing similar to Next.js
- Requires specific directory structure in app/ folder
- Integration with drawer navigation needs careful configuration

**🖼 Wireframe Reference**
- Exists: No
- Note: Infrastructure component, no direct wireframe reference

**📊 PERT Estimation**:
- **Optimistic**: 6 hours
- **Realistic**: 8 hours
  - Comments: Expo Router v3+ has excellent documentation and examples. Configuration is straightforward.
    - Configuration Setup: ~2h (Expo Router, directory structure)
    - Navigation Integration: ~2h (drawer + stack patterns)
    - TypeScript Setup: ~1h (route types, parameters)
    - Deep Linking: ~1.5h (URL scheme, route handling)
    - Testing & Debugging: ~1.5h (navigation flows, edge cases)
- **Pessimistic**: 12 hours
- **Final PERT Estimate: 9.67 hours**

---

### 🔹 `UI-SCAFFOLD-MOB-004` – Toast Notification System

**Summary**:  
Global toast notification system providing user feedback for actions across the entire application.

**Justification**:  
Essential for user experience to provide immediate feedback on actions like form submissions, API calls, and errors.

**User Story**:  
"As a mobile app user, I want to receive feedback messages, so that I know when actions succeed or fail."

**🎯 Objective**:  
Implement comprehensive toast system that works consistently across all app screens and features.

**⛓ Dependencies**:  
Toast library (react-native-toast-message or similar), global provider setup.

**✅ Acceptance Criteria**:
- Toast library displays different message types (success, error, warning, info)
- Toasts appear at appropriate screen position with proper z-index
- Toasts auto-dismiss after configurable duration (default 3 seconds)
- Library handles toast queuing and display management
- Toasts can be manually dismissed by user tap or swipe
- Toast types styled using library's theming system
- Toast system accessible from any screen or component
- Library provides smooth animations for toast appearance and dismissal

**🧰 Technical Tasks**:
- Install and configure toast library (react-native-toast-message or similar)
- Set up global toast provider in App.tsx
- Configure toast themes and styling
- Create simple toast utility functions for easy usage
- Test toast functionality across different screens
- Configure toast positioning and behavior

**⚙️ External Setup / Config Required**
- Toast library installation and configuration
- Global provider integration in app root
- Theme configuration for toast styling

**❗ Pending Confirmations**
- Toast positioning preference (top vs bottom of screen)
- Auto-dismiss duration for different message types
- Maximum number of simultaneous toasts

**📝 Notes & Observations**
- Toast system will be used by authentication, offers, and other epics
- Need to ensure toasts don't interfere with navigation or modal dialogs
- Consider accessibility features for visually impaired users

**🖼 Wireframe Reference**
- Exists: No
- Note: UI feedback component, not shown in wireframes

**📊 PERT Estimation**:
- **Optimistic**: 1 hours
- **Realistic**: 2 hours
  - Comments: Using mature toast library eliminates need for custom implementation. Simple configuration and integration.
    - Library Setup: ~0.5h (installation, basic configuration)
    - Integration: ~0.5h (global provider, App.tsx setup)
    - Configuration: ~0.5h (themes, positioning, behavior)
    - Manual Testing: ~0.5h (different scenarios)
- **Pessimistic**: 4 hours
- **Final PERT Estimate: 3.33 hours**

---

### 🔹 `UI-SCAFFOLD-MOB-005` – Global Loading System

**Summary**:  
Global loading system providing visual feedback during app operations, API calls, and navigation transitions.

**Justification**:  
Essential user experience component that prevents user confusion during loading states and provides professional app feel.

**User Story**:  
"As a mobile app user, I want visual feedback when the app is loading, so that I know the app is working and not frozen."

**🎯 Objective**:  
Implement comprehensive loading system that can be triggered globally and prevents user interaction during loading.

**⛓ Dependencies**:  
Loading library (react-native-loading-spinner-overlay or similar), global state management.

**✅ Acceptance Criteria**:
- Loading library provides full-screen overlay when active
- Loading indicator is visually appealing and matches app branding
- Loading state can be triggered from any screen or component
- Loading overlay prevents user interaction while active
- Loading component works seamlessly with app navigation
- Library handles different loading contexts (navigation, API, authentication)
- Loading indicator styled using library's theming system
- Library provides smooth animations for loading show/hide transitions

**🧰 Technical Tasks**:
- Install and configure loading library (react-native-loading-spinner-overlay or similar)
- Set up global loading provider/context
- Configure loading indicator styling and branding
- Create simple loading utility functions for easy usage
- Test loading functionality across different screens
- Configure loading behavior and animations

**⚙️ External Setup / Config Required**
- Loading library installation and configuration
- Global provider integration in app root
- Theme configuration for loading styling

**❗ Pending Confirmations**
- Loading indicator design and branding elements
- Loading timeout duration for different operations
- Loading overlay opacity and styling

**📝 Notes & Observations**
- Skeleton screens excluded for MVP per user request
- Focus on simple, general loading indicators
- Loading system will be used by all feature epics

**🖼 Wireframe Reference**
- Exists: No
- Note: Infrastructure component, not shown in wireframes

**📊 PERT Estimation**:
- **Optimistic**: 1 hours
- **Realistic**: 3 hours
  - Comments: Using mature loading library eliminates need for custom overlay implementation. Simple configuration.
    - Library Setup: ~0.5h (installation, basic configuration)
    - Integration: ~1h (global provider, context setup)
    - Configuration: ~1h (styling, branding, behavior)
    - Manual Testing: ~0.5h (different scenarios)
- **Pessimistic**: 5 hours
- **Final PERT Estimate: 3.67 hours**

---

### 🔹 `UI-SCAFFOLD-MOB-006` – Theme & Design System

**Summary**:  
Comprehensive design system and theme configuration using NativeWind for consistent styling across the application.

**Justification**:  
Provides unified visual language and developer efficiency through consistent styling patterns and reusable design tokens.

**User Story**:  
"As a developer, I want a consistent design system, so that the app has cohesive styling across all screens."

**🎯 Objective**:  
Establish complete design system foundation with colors, typography, spacing, and component patterns.

**⛓ Dependencies**:  
NativeWind library, Tailwind CSS configuration, wireframe design analysis.

**✅ Acceptance Criteria**:
- NativeWind is properly configured and integrated with React Native
- Tailwind CSS classes work seamlessly in React Native components
- Color palette matches wireframe designs and branding
- Typography scale is consistent across all components
- Spacing system provides predictable and consistent layout
- Design tokens are defined as reusable constants
- Theme supports light mode (dark mode excluded for MVP)
- All foundational components use design system patterns

**🧰 Technical Tasks**:
- Install and configure NativeWind for React Native project
- Set up Tailwind CSS configuration with custom theme
- Define color palette based on wireframe analysis
- Create typography scale with consistent font sizes and weights
- Establish spacing system for margins, padding, and gaps
- Define component styling patterns and conventions
- Create design token constants for reusability
- Document design system usage guidelines

**⚙️ External Setup / Config Required**
- NativeWind installation and configuration
- Tailwind CSS configuration file setup
- Font loading and configuration

**❗ Pending Confirmations**
- Final color palette from wireframe analysis
- Font family and typography specifications
- Component styling convention standards

**📝 Notes & Observations**
- NativeWind allows using Tailwind CSS classes in React Native
- Wireframes show purple/blue color scheme for branding
- Design system will be foundation for all component styling

**🖼 Wireframe Reference**
- Exists: Yes
- Filename: All wireframes for color and styling analysis

**📊 PERT Estimation**:
- **Optimistic**: 4 hours
- **Realistic**: 8 hours
  - Comments: NativeWind setup with UI library components reduces custom design system work. Focus on configuration and tokens.
    - NativeWind Setup: ~2h (installation, configuration)
    - Theme Configuration: ~3h (colors, typography, spacing with UI library)
    - Design Tokens: ~1.5h (constants, reusable patterns)
    - Documentation: ~1h (usage guidelines, examples)
    - Testing & Validation: ~0.5h (cross-component consistency)
- **Pessimistic**: 12 hours
- **Final PERT Estimate: 9 hours**

### 🔹 `UI-SCAFFOLD-MOB-007` – Main App Layout Component

**Summary**:  
Reusable layout component for main application screens that includes header, drawer navigation, and content structure.

**Justification**:  
Provides consistent layout architecture for all main app screens, reducing code duplication and ensuring uniform user experience.

**User Story**:  
"As a developer, I want a reusable main app layout, so that all primary screens have consistent navigation and structure."

**🎯 Objective**:  
Create comprehensive layout component that serves as foundation for map, offers, profile, and other main screens.

**⛓ Dependencies**:  
App Header component (UI-SCAFFOLD-MOB-001), Drawer Navigation (UI-SCAFFOLD-MOB-002), Navigation System (UI-SCAFFOLD-MOB-003).

**✅ Acceptance Criteria**:
- Layout component includes integrated AppHeader with hamburger menu
- Drawer navigation is properly configured and accessible
- Content area supports scrollable content with proper safe area handling
- Layout adapts to different screen sizes and orientations
- Consistent spacing and padding across all screens using this layout
- Layout works seamlessly with Expo Router navigation
- Loading and toast systems integrate properly with layout
- Component is reusable across different main app screens

**🧰 Technical Tasks**:
- Create MainAppLayout component with TypeScript
- Integrate AppHeader component into layout
- Configure drawer navigation within layout structure
- Add scrollable content area with safe area insets
- Implement responsive design for different screen sizes
- Add proper z-index management for overlays (toast, loading)
- Create layout prop interface for screen customization
- Test layout with different content types and lengths

**⚙️ External Setup / Config Required**
- Expo Router layout configuration
- Safe area context integration
- Drawer navigation setup

**❗ Pending Confirmations**
- Content area padding and spacing specifications
- Layout behavior during keyboard appearance
- Screen-specific customization requirements

**📝 Notes & Observations**
- Used by map screen, offers list, profile, purchase history screens
- Should integrate seamlessly with all foundation components
- Needs to handle keyboard avoidance for forms

**🖼 Wireframe Reference**
- Exists: Yes
- Filename: `woppa-wireframe-1-mapa.png`, `woppa-wireframe-2-listado-ofertas.png`
- Note: Shows main app structure with header and content

**📊 PERT Estimation**:
- **Optimistic**: 2 hours
- **Realistic**: 5 hours
  - Comments: Layout integration component building on existing foundation components and UI library.
    - Frontend UI: ~1.5h (layout structure with UI library components)
    - Frontend Logic: ~2h (navigation integration, safe area)
    - Integration: ~1h (header, drawer, router)
    - Backend: ~0h (no backend needed)
    - Manual Testing: ~0.5h (different screens, devices)
- **Pessimistic**: 8 hours
- **Final PERT Estimate: 5.33 hours**

---

### 🔹 `UI-SCAFFOLD-MOB-008` – Authentication Layout Component

**Summary**:  
Simple layout component for authentication screens without complex navigation, focused on branding and form presentation.

**Justification**:  
Provides clean, distraction-free layout for authentication flows while maintaining consistent branding and safe area handling.

**User Story**:  
"As a developer, I want a simple authentication layout, so that login and registration screens have consistent, focused design."

**🎯 Objective**:  
Create minimal layout component optimized for authentication forms and branding display.

**⛓ Dependencies**:  
Theme & Design System (UI-SCAFFOLD-MOB-006), Navigation System (UI-SCAFFOLD-MOB-003).

**✅ Acceptance Criteria**:
- Layout displays app branding/logo prominently
- Content area is centered and optimized for forms
- Safe area handling works correctly on all devices
- Layout adapts to keyboard appearance/disappearance
- No complex navigation elements (no header, no drawer)
- Consistent spacing and typography using design system
- Loading and toast systems work within authentication context
- Layout supports both portrait and landscape orientations

**🧰 Technical Tasks**:
- Create AuthLayout component with TypeScript
- Add app branding/logo display area
- Implement centered content area for forms
- Add keyboard-aware scrolling and layout adjustment
- Configure safe area insets for authentication screens
- Style component using NativeWind/design system
- Add layout animations for keyboard appearance
- Test layout with different form lengths and content

**⚙️ External Setup / Config Required**
- App branding assets (logo, colors)
- Keyboard avoidance configuration
- Safe area context integration

**❗ Pending Confirmations**
- App logo and branding specifications
- Keyboard behavior and animation preferences
- Background styling and color scheme

**📝 Notes & Observations**
- Used by login, register, forgot password, email verification screens
- Should be distraction-free to focus user on authentication
- Wireframe shows "W!" branding in register screen

**🖼 Wireframe Reference**
- Exists: Yes
- Filename: `woppa-wireframe-4-register.png`
- Note: Shows simple layout with branding and form content

**📊 PERT Estimation**:
- **Optimistic**: 2 hours
- **Realistic**: 4 hours
  - Comments: Simpler layout component with focus on branding and forms using UI library components.
    - Frontend UI: ~1.5h (layout structure, branding)
    - Frontend Logic: ~1.5h (keyboard handling, safe area)
    - Integration: ~0.5h (design system, navigation)
    - Backend: ~0h (no backend needed)
    - Manual Testing: ~0.5h (forms, keyboard, devices)
- **Pessimistic**: 7 hours
- **Final PERT Estimate: 4.17 hours**

---

## 🧪 Post-analysis: Story Set Review

After analyzing all stories, I've identified the following optimizations and observations:

**Foundation Dependencies:**
- UI-SCAFFOLD-MOB-003 (Navigation System) is a dependency for all other stories
- UI-SCAFFOLD-MOB-006 (Theme & Design System) should be implemented early to support other components
- UI-SCAFFOLD-MOB-001 (App Header) and UI-SCAFFOLD-MOB-002 (Drawer Navigation) are tightly coupled
- UI-SCAFFOLD-MOB-007 (Main App Layout) depends on stories 001, 002, and 003
- UI-SCAFFOLD-MOB-008 (Auth Layout) depends on stories 003 and 006
- UI-SCAFFOLD-MOB-004 (Toast System) and UI-SCAFFOLD-MOB-005 (Loading System) can be developed in parallel

**Consistency Improvements:**
- Minimal state management using mature libraries (no custom Zustand stores for toast/loading)
- NativeWind styling pattern with UI library components for consistency
- Expo Router integration is standardized throughout navigation components

**Scope Clarifications:**
- All stories focus on foundational infrastructure only
- Feature-specific components are explicitly excluded
- Design system provides foundation for all future component development

**No conflicts or duplications were identified.** Stories are properly scoped and provide comprehensive foundation.

---

## 📌 Stories with High Risk or Pending Decisions

- **UI-SCAFFOLD-MOB-002**: Drawer menu content not defined in wireframes, needs design input
- **UI-SCAFFOLD-MOB-003**: Expo Router configuration complexity with drawer + stack navigation
- **UI-SCAFFOLD-MOB-004**: Toast positioning and styling preferences need confirmation
- **UI-SCAFFOLD-MOB-005**: Loading indicator branding and design needs specification
- **UI-SCAFFOLD-MOB-006**: Color palette and typography specifications need wireframe analysis

---

## 📊 Epic Estimation Summary

To be completed manually:

- Total user stories: **8**
- Stories with high uncertainty: **3** (UI-SCAFFOLD-MOB-002, UI-SCAFFOLD-MOB-003, UI-SCAFFOLD-MOB-006)
- Stories pending confirmation: **6**

### Manual 3-point Estimation for Epic (PERT)
```
- Optimistic: 22 hours
- Realistic: 40 hours  
- Pessimistic: 62 hours
- Final PERT Estimate: 40.7 hours
```
