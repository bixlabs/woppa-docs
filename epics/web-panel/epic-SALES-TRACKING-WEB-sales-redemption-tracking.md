# Epic: Sales & Redemption Tracking
**KEY**: `SALES-TRACKING-WEB`  
**Platform**: Web Panel (Merchants)  
**Status**: Defined  

## Overview
Comprehensive sales performance monitoring and coupon management system for merchants. Provides metrics on generated/redeemed coupons, accumulated earnings, payment tracking from Woppa, and basic redemption tracking functionality where merchants can mark coupons as "redeemed" when customers present them in-store. Includes filtering capabilities by date range, category, and coupon status with detailed financial reporting focused on merchant performance insights.

## User Stories

### Sales Performance Dashboard

• **Story 1: Sales Overview Dashboard**  
  *Description:* Merchants view comprehensive dashboard showing key metrics: total coupons generated, total redeemed, accumulated earnings, payments received from Woppa, and payments pending. Dashboard provides quick snapshot of business performance with current period data.

• **Story 2: Offer Performance Metrics**  
  *Description:* For each active and historical offer, merchants see detailed performance data: coupons generated, redemption rate, revenue generated, dates active, and current status. Metrics help evaluate offer effectiveness and inform future decisions.

• **Story 3: Financial Reporting**  
  *Description:* Merchants access detailed financial reports showing earnings breakdown by offer, payment history from Woppa, pending payments, and transaction details. Reports can be filtered by date range and exported for accounting purposes.

### Coupon Management

• **Story 4: Coupon Status Tracking**  
  *Description:* Merchants view all coupons generated from their offers with current status: "Generado" (generated), "Pagado" (paid by customer), "Redimido" (redeemed at store), "Expirado" (expired). Each coupon shows associated offer, customer info (if available), and timestamps.

• **Story 5: Manual Coupon Redemption**  
  *Description:* Merchants manually mark coupons as "redeemed" when customers present them in-store. System provides input field for coupon code entry, validates code belongs to merchant, confirms status is "paid", and updates to "redeemed" with timestamp.

• **Story 6: Redemption Validation**  
  *Description:* System prevents invalid redemptions by validating coupon codes, checking merchant ownership, verifying current status allows redemption, and confirming coupon hasn't expired. Clear error messages guide merchants through redemption process.

### Historical Data & Analytics

• **Story 7: Historical Sales Data**  
  *Description:* Merchants access historical sales data with filtering by date range, offer category, coupon status, and specific offers. Historical data includes trends, comparison periods, and performance changes over time.

• **Story 8: Redemption History**  
  *Description:* Detailed log of all redemption activities showing when, where, and which coupons were redeemed. Includes both manual redemptions by merchant and any system redemptions. Data helps with inventory planning and customer behavior analysis.

• **Story 9: Payment Tracking**  
  *Description:* Merchants track payment schedule from Woppa (monthly payments), view payment history, see breakdown of what's included in each payment, and access payment receipts or confirmations.

### Filtering & Export

• **Story 10: Advanced Filtering**  
  *Description:* Comprehensive filtering system allowing merchants to filter sales data by date range, offer category, subcategory, coupon status, payment status, and custom date periods. Filters combine logically and maintain state across sessions.

• **Story 11: Data Export**  
  *Description:* Merchants can export sales reports, coupon lists, and financial data in CSV or PDF format for external analysis or accounting purposes. Exports respect current filter settings and include relevant data only.

• **Story 12: Search Functionality**  
  *Description:* Merchants can search for specific coupons by code, customer information, offer name, or date ranges. Search works across all coupon statuses and provides quick access to specific transactions.

### Notifications & Alerts

• **Story 13: Sales Notifications**  
  *Description:* Merchants receive notifications for significant sales events: high redemption volume, unusual patterns, payment confirmations from Woppa, and monthly sales summaries. Notifications delivered via email and platform alerts.

• **Story 14: Redemption Confirmations**  
  *Description:* When merchants manually redeem coupons, system provides immediate confirmation with coupon details and updates inventory/stock counters if applicable. Confirmations include receipt information for merchant records.

## Technical Requirements

- Real-time coupon status updates
- Secure coupon code validation
- Financial data calculation and storage
- Export functionality (CSV/PDF)
- Advanced filtering and search capabilities
- Email notification system
- Data analytics and reporting engine
- Mobile-responsive dashboard interface

## Acceptance Criteria Summary

- Dashboard shows accurate real-time sales metrics
- Coupon redemption process validates codes correctly
- Only valid, paid coupons can be marked as redeemed
- Financial reports calculate earnings accurately
- Filtering and search work across all data sets
- Export functions produce complete, accurate reports
- Notifications sent for all relevant sales events
- System prevents duplicate or invalid redemptions

## Dependencies

- Offer Management epic (requires active offers to generate sales)
- Business Authentication epic (approved merchants only)
- Mobile app coupon system (coupons generated from mobile purchases)
- Payment processing system (to track payment statuses)
- Email service configuration