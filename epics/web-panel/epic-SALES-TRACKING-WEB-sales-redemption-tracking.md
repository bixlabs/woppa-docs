# 🧩 Epic: Sales & Redemption Tracking

**KEY**: `SALES-TRACKING-WEB`

---

## 📄 Functional Description
Basic sales and redemption tracking for merchants to view their business performance using React web interface. Focused on MVP functionality allowing merchants to visualize their sales history (paid codes, redeemed codes, accumulated earnings, payments received from Woppa) and manually confirm coupon redemptions as specified in requirements. Provides simple interface for essential merchant operations without complex analytics.

---

## 💻 Target Platform
This epic applies to:
- `web-panel`

---

## 🧭 Functional Scope
Main flows and interactions included in this epic:
- Sales history visualization: paid codes, redeemed codes, accumulated earnings
- Payment tracking from Woppa (payments received and pending)
- Manual coupon redemption confirmation when customers present codes in-store
- Basic sales performance view without complex analytics

---

## 🚫 Out of Scope
Explicitly excluded elements:
- Real-time sales dashboards and analytics
- Advanced financial reporting and export functionality
- Historical data trending and comparison tools
- Email notifications for sales events
- Advanced filtering and search capabilities
- Detailed offer performance metrics and analysis
- Automated redemption processing
- Complex data visualization and charts

---

## 🖼 Wireframes Referenced in Epic
List of wireframes that apply to this epic and the stories that use them.

- No specific wireframes exist for merchant sales tracking screens
- React interface will use existing design system patterns

---

## 🔍 Epic-level Ambiguities

- 📐 Missing wireframe: No wireframes exist for merchant sales tracking interface
- 📊 Business decision pending: Exact format for sales history display and payment tracking
- 📋 Missing validation rules: Manual redemption validation procedures and error handling
- 🔁 Undefined logic: Payment calculation methods and display periods

---

## 🧵 User Stories

---

### 🔹 `SALES-TRACKING-WEB-001` – Sales History Overview

**Summary**:  
Display merchant's sales history showing paid codes, redeemed codes, accumulated earnings, and payments received from Woppa using React interface.

**Justification**:  
Merchants need visibility into their business performance through basic sales metrics as specified in requirements document.

**User Story**:  
"As a merchant, I want to view my sales history with paid codes, redeemed codes, and earnings, so that I can track my business performance with Woppa."

**🎯 Objective**:  
Create React component displaying the 5 core sales metrics from requirements: paid codes (by customers), redeemed codes, accumulated earnings, codes paid by Woppa, and codes pending payment from Woppa.

**⛓ Dependencies**:
- React web panel authentication
- PostgreSQL database with sales and payment data
- API endpoints for sales data retrieval
- Merchant authentication system

**✅ Acceptance Criteria**:
- Display total paid codes count (coupons purchased by customers)
- Show total redeemed codes count (coupons redeemed in-store by customers)
- Display accumulated earnings from all merchant offers (total revenue generated)
- Show codes already paid by Woppa (codes Woppa has financially processed to merchant)
- Display codes pending payment from Woppa (redeemed codes awaiting payment processing)
- Include date range filtering to calculate metrics for specific time periods
- Include category and subcategory filtering to view metrics by offer type
- Simple, clean layout with clear metric labels and values distinguishing customer payments vs. Woppa payments
- Data refreshes when page is loaded or refreshed or filters change
- Basic error handling for data unavailability
- Responsive design for mobile and desktop access

**🧰 Technical Tasks**:
- Create React component for sales overview
- Implement API calls for sales metrics data
- Add sales data aggregation logic with filtering capabilities
- Build simple metrics display components (counters with labels)
- Implement date range filtering functionality
- Add category and subcategory filtering components
- Implement error handling and loading states
- Style interface using existing design system
- Add responsive design considerations

**⚙️ External Setup / Config Required**
- API endpoints for sales data retrieval with filtering parameters
- Database queries for sales metrics calculations with date and category filters
- Merchant authentication middleware
- React routing configuration for sales section

**❗ Pending Confirmations**
- Exact definition of "accumulated earnings" calculation method
- Payment tracking display format and frequency
- Time period for sales metrics (all-time vs. current period)

**📝 Notes & Observations**
- Focus on essential sales metrics only as specified in requirements
- Keep implementation simple for MVP without complex analytics
- Leverage existing React components and design patterns
- Future optimization: Consider materialized views for sales metrics aggregations (post-MVP)

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 12 hours
- Realistic: 19.5 hours
    - React component development: ~2.5h (no wireframes - design decisions included)
    - API integration and data fetching: ~2h
    - Metrics display and styling: ~2.5h (dashboard layout design + responsive)
    - Date range and category filtering components: ~5h (UI/UX design + implementation)
    - Backend (sales metrics aggregation, payment calculations, filtering logic, API endpoints): ~6.5h
    - Error handling and testing: ~1h
- Pessimistic: 27 hours
- Final PERT Estimate: 19.5h
```

**🖼 Wireframe Reference**
- Exists: No
- React interface with sales metrics display

---

### 🔹 `SALES-TRACKING-WEB-002` – Manual Coupon Redemption

**Summary**:  
Enable merchants to manually confirm coupon redemptions when customers present codes in-store as specified in requirements.

**Justification**:  
Merchants need ability to manually mark coupons as redeemed when customers present them in-store for validation and inventory tracking.

**User Story**:  
"As a merchant, I want to manually confirm coupon redemptions when customers present codes in-store, so that I can validate redemptions and update coupon status."

**🎯 Objective**:  
Create React interface for manual coupon redemption with code input, validation, and status update functionality.

**⛓ Dependencies**:
- Sales History Overview (SALES-TRACKING-WEB-001)
- Coupon validation API
- Merchant ownership verification system

**✅ Acceptance Criteria**:
- Input field for coupon code entry
- Validate that coupon code exists and belongs to merchant
- Confirm coupon status is "paid" before allowing redemption
- Single click changes status from "paid" to "redeemed" with timestamp
- Success confirmation message displayed after redemption
- Clear error messages for invalid codes or validation failures
- Form validation and proper error handling
- Action updates sales metrics in real-time

**🧰 Technical Tasks**:
- Create React form component for coupon code input
- Implement coupon code validation API calls
- Add merchant ownership verification logic
- Implement status change functionality with API integration
- Add success/error message display system
- Create form validation and error handling
- Integrate with sales metrics for real-time updates
- Add proper loading states during validation

**⚙️ External Setup / Config Required**
- Coupon validation API endpoints
- Merchant ownership verification logic
- Database schema for coupon status updates
- Error message configuration and display

**❗ Pending Confirmations**
- Coupon code format and validation requirements
- Specific error message text and handling procedures
- Integration with inventory/stock management if applicable

**📝 Notes & Observations**
- Critical functionality for merchant operations and customer service
- Simple form-based interface suitable for in-store use
- Focus on reliable validation and clear user feedback

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 4 hours
- Realistic: 6 hours
    - React form component: ~1h (AI-accelerated development)
    - API integration: ~0.5h (simple POST endpoint call)
    - Error handling and user feedback: ~1h (AI-assisted patterns)
    - Backend (coupon validation, status updates, ownership verification, API endpoints): ~2h (AI-assisted with business logic)
    - Testing and integration: ~1h (real testing and system integration)
    - Buffer: ~0.5h
- Pessimistic: 8 hours
- Final PERT Estimate: 6h
```

**🖼 Wireframe Reference**
- Exists: No
- React form interface with coupon code input and validation

---

### 🔹 `SALES-TRACKING-WEB-003` – Per-Offer Performance Metrics

**Summary**:  
Display detailed performance metrics for individual offers including total coupons generated, redeemed, accumulated earnings per offer as specified in requirements.

**Justification**:  
Merchants need granular visibility into each offer's performance to understand which offers work best and optimize future campaigns.

**User Story**:  
"As a merchant, I want to see detailed metrics for each of my offers, so that I can understand which offers perform best and plan future campaigns accordingly."

**🎯 Objective**:  
Create React component displaying the 5 core metrics per offer from requirements: total coupons generated, redeemed coupons, accumulated earnings, paid codes, pending codes.

**⛓ Dependencies**:
- Sales History Overview (SALES-TRACKING-WEB-001)
- Manual Coupon Redemption (SALES-TRACKING-WEB-002)
- Backend sales data aggregation system

**✅ Acceptance Criteria**:
- Display metrics per individual offer with date range selection
- Show total coupons generated for each offer
- Display redeemed coupons count and percentage
- Calculate and show accumulated earnings (price × redeemed quantity)
- Show codes already paid by Woppa and codes pending payment
- Include filtering by date range as specified in requirements
- Include filtering by category and subcategory to focus on specific offer types
- Responsive design for mobile and desktop access
- Data refreshes when page is loaded or filters change

**🧰 Technical Tasks**:
- Create React component for per-offer metrics display
- Implement API calls for offer-specific performance data
- Add earnings calculation logic (price × redeemed quantity)
- Build metrics display components with proper formatting
- Implement date range filtering functionality
- Add category and subcategory filtering components
- Style interface using existing design system
- Add responsive design considerations
- Implement error handling and loading states

**⚙️ External Setup / Config Required**
- API endpoints for per-offer metrics retrieval with filtering parameters
- Database queries for offer performance calculations with date and category filters
- Date range filtering logic implementation
- Category and subcategory filtering logic implementation
- Payment status tracking integration

**❗ Pending Confirmations**
- Date range filter format and default periods
- Earnings calculation method and display format
- Additional performance metrics to include beyond the 5 core ones

**📝 Notes & Observations**
- Core functionality for merchants to evaluate offer success
- Focus on the 5 essential metrics specified in requirements
- Provides actionable insights for future offer planning
- Future optimization: Consider materialized views for per-offer metrics aggregations (post-MVP)

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 10 hours
- Realistic: 16.5 hours
    - React metrics component: ~3h (per-offer display design + layout decisions)
    - API integration and calculations: ~2.5h
    - Date filtering functionality: ~2h (UI/UX design + implementation)
    - Category and subcategory filtering components: ~2.5h (complex filtering UI design)
    - Backend (per-offer metrics calculations, complex aggregations, date and category filtering logic, API endpoints): ~5.5h
    - Testing and error handling: ~1h (multiple offer scenarios + responsive testing)
- Pessimistic: 23 hours
- Final PERT Estimate: 16.5h
```

**🖼 Wireframe Reference**
- Exists: No
- React interface with per-offer metrics and filtering capabilities

---

## 📊 Epic Estimation Summary

Epic totals:

- Total user stories: 3
- Stories with moderate complexity: 3
- Stories leveraging React and existing infrastructure: 3

### Manual 3-point Estimation for Epic (PERT)

```
- Optimistic: 26h
- Realistic: 42h  
- Pessimistic: 58h
- Final PERT Estimate: 42h
```

**React and Requirements-Based Impact:**
- Focus on sales metrics and redemption functionality from requirements
- Essential MVP functionality: sales history, manual coupon redemption, per-promotion metrics
- Elimination of offer management overlap with OFFER-MGMT-WEB epic
- Leveraging existing React components and design system for consistency
- Simple API integration focused on sales data aggregation and coupon validation
- **Future Performance Optimization**: Consider materialized views for sales metrics aggregations when scaling beyond MVP (reduces database query complexity and improves response times)

---