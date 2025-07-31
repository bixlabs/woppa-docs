# 🧩 Epic: Operational Metrics Dashboard

**KEY**: `METRICS-DASH-BACK`

---

## 📄 Functional Description
Basic operational metrics dashboard for Woppa staff to monitor essential platform KPIs using AdminJS interface. Focused on MVP functionality displaying the 5 core metrics specified in requirements: total active offers, weekly redemptions, active businesses (30-day period), most viewed offers, and top-performing offers by redemptions.

---

## 💻 Target Platform
This epic applies to:
- `back-office` (AdminJS interface with custom dashboard views)

---

## 🧭 Functional Scope
Main flows and interactions included in this epic:
- Simple metrics dashboard displaying the 5 core KPIs from requirements
- Basic data visualization for key operational insights
- Read-only metrics display with automatic data refresh

---

## 🚫 Out of Scope
Explicitly excluded elements:
- Real-time activity monitoring and alerts
- Geographic distribution analytics and interactive maps
- Advanced analytics and forecasting capabilities
- Custom dashboard creation and role-based views
- Automated report generation and scheduling
- Data export functionality beyond basic display
- Historical data analysis and trend comparisons
- Executive reporting and presentation materials
- Performance monitoring and system health metrics

---

## 🖼 Wireframes Referenced in Epic
List of wireframes that apply to this epic and the stories that use them.

- No specific wireframes exist for back-office metrics dashboard
- AdminJS will provide default interface with custom dashboard components

---

## 🔍 Epic-level Ambiguities

- 📐 Missing wireframe: No wireframes exist for metrics dashboard layout
- 📊 Business decision pending: Exact data refresh frequency and caching requirements
- 📋 Missing validation rules: Specific calculation methods for "active businesses" and "most viewed"
- 🔁 Undefined logic: Time periods and filtering criteria for metrics

---

## 🧵 User Stories

---

### 🔹 `METRICS-DASH-BACK-001` – Visualizar los Indicadores Clave de Actividad (KPIs)

**Summary**:  
Display core platform activity KPIs including total active offers, weekly redemptions, and active businesses count using AdminJS dashboard interface.

**Justification**:  
Staff need visibility into basic platform activity levels through key quantitative metrics to monitor operational health and growth.

**User Story**:  
"As a Woppa staff member, I want to view key activity indicators on a dashboard, so that I can monitor platform operational health and activity levels."

**🎯 Objective**:  
Create AdminJS dashboard displaying the 3 core activity KPIs with basic data visualization and automatic refresh.

**⛓ Dependencies**:  
- AdminJS setup with Node.js backend
- PostgreSQL database with offers, businesses, and redemption data
- Prisma ORM integration
- Staff authentication system

**✅ Acceptance Criteria**:
- Dashboard displays total active offers count with current timestamp
- Shows total weekly redemptions with current week indicator
- Displays active businesses count (30-day period) with calculation period clearly shown
- KPIs refresh when page is reloaded or accessed
- Simple, clean layout with clear metric labels and values
- Basic error handling and loading states for data unavailability
- Timestamp indicators showing when data was last updated

**🧰 Technical Tasks**:
- Create AdminJS custom dashboard page
- Implement database queries for active offers count
- Add weekly redemptions aggregation logic
- Create 30-day active businesses calculation
- Build simple KPI display components (counters with labels)
- Display current data on page load
- Add error handling and loading states
- Style dashboard for clear KPI presentation

**⚙️ External Setup / Config Required**
- AdminJS dashboard configuration
- Database queries optimization for KPI calculations
- Caching strategy for performance
- Staff access permissions for metrics dashboard

**❗ Pending Confirmations**
- Exact definition of "active businesses" (login-based, activity-based, offer creation, etc.)
- Data refresh frequency requirements
- Week calculation method (Monday-Sunday vs. rolling 7 days)

**📝 Notes & Observations**
- Focus on quantitative activity metrics only
- Leverage AdminJS dashboard capabilities for rapid development
- Prioritize data accuracy and performance over complex visualization
- Keep implementation simple for MVP requirements
- Future optimization: Consider materialized views for KPI aggregations (post-MVP)

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 3 hours
- Realistic: 6.5 hours
    - AdminJS dashboard setup: ~1.5h
    - Database queries and KPI calculations: ~2h
    - KPI display components: ~2h
    - Testing and validation: ~1.0h
- Pessimistic: 10 hours
- Final PERT Estimate: 6.5h
```

**🖼 Wireframe Reference**
- Exists: No
- AdminJS dashboard interface with KPI counters

---

### 🔹 `METRICS-DASH-BACK-002` – Identificar las Promociones de Mayor Rendimiento

**Summary**:  
Display top-performing offers based on redemption counts to identify most successful promotions using AdminJS list interface.

**Justification**:  
Staff need to identify which offers are performing best to understand market preferences and guide merchant strategy decisions.

**User Story**:  
"As a Woppa staff member, I want to see the top-performing offers by redemption count, so that I can identify successful promotion patterns and guide merchants."

**🎯 Objective**:  
Create AdminJS interface displaying ranked lists of most viewed offers and most redeemed offers with performance metrics.

**⛓ Dependencies**:  
- Visualizar KPIs (METRICS-DASH-BACK-001)
- Offer view tracking system
- Redemption tracking data

**✅ Acceptance Criteria**:
- Display top 5 offers with most redemptions including redemption counts and offer details
- Include offer name, business name, category, and creation date for context
- Lists show current data on page load/refresh
- Clear ranking indicators (1st, 2nd, 3rd, etc.)
- Handle cases where insufficient data exists (less than 5 offers)
- Basic filtering by time period if needed

**🧰 Technical Tasks**:
- Create redemption count aggregation queries
- Build top offers ranking logic
- Create AdminJS list components for top offers display
- Add offer details integration (name, business, category)
- Implement ranking indicators and performance metrics display
- Display current performance data on page access
- Handle edge cases (no data, ties in rankings)

**⚙️ External Setup / Config Required**
- Database indexes for performance queries
- Redemption data aggregation optimization

**❗ Pending Confirmations**
- Time period for performance calculations (all-time vs. recent period)
- Handling of ties in rankings
- Required offer details to display alongside performance metrics

**📝 Notes & Observations**
- Performance queries may need caching for efficiency
- Focus on actionable insights for merchant guidance
- Keep visualization simple with ranked lists
- Future optimization: Consider materialized views for offer performance rankings (post-MVP)

**📊 PERT Estimation**
```
📊 PERT Estimation:
- Optimistic: 2.5 hours
- Realistic: 4 hours
    - Redemption ranking logic: ~1.5h
    - Top offers display components: ~1.5h
    - Performance metrics integration: ~0.5h
    - Testing and validation: ~0.5h
- Pessimistic: 6 hours
- Final PERT Estimate: 4h
```

**🖼 Wireframe Reference**
- Exists: No
- AdminJS list interface with ranked performance data

---

## 📊 Epic Estimation Summary

Epic totals:

- Total user stories: 2
- Stories with moderate complexity: 2
- Stories leveraging AdminJS for rapid development: 2

### Manual 3-point Estimation for Epic (PERT)

```
- Optimistic: 5.5h
- Realistic: 10.5h  
- Pessimistic: 16h
- Final PERT Estimate: 10.6h
```
---