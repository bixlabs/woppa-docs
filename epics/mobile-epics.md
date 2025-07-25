# 📱 Mobile Epics – Woppa App

## Epic: Explore Nearby Offers

### Screen: Map with Offers  
**Wireframe:** `woppa-wireframe-1-mapa.png`  
**Description:**  
This screen displays a map centered on the user's location with nearby offers shown as markers. Users can adjust the search radius, filter by category, and select markers to view associated offers in a modal or bottom sheet.

### Screen: Offer List  
**Wireframe:** `woppa-wireframe-2-listado-ofertas.png`  
**Description:**  
This screen shows a list of available offers. Users can browse offers by category and distance without using the map.

---

## Epic: Offer Redemption

### Screen: Offer Details  
**Wireframe:** `woppa-wireframe-3-detalle-oferta.png`  
**Description:**  
Displays detailed information about the selected offer, including a link to open directions in Google Maps and an option to redeem the offer.

### Screen: Payment Pending  
**Wireframe:** _Not defined_  
**Description:**  
Temporary screen shown after returning from Mercado Pago, while the backend verifies the payment status. Displays a loading or waiting message.

> Once the payment is confirmed via backend polling, the user is automatically redirected to either the success or failure screen based on the result.

### Screen: Payment (Success / Failure)  
**Wireframe:** _Not defined_  
**Description:**  
Handles the final payment result. Shows a success message if the transaction is confirmed, or an error message if the payment failed or was invalid.

### Screen: Offer Code  
**Wireframe:** `woppa-wireframe-5-obtained-cupon.png`  
**Description:**  
Displays the unique offer code that the user can present at the store. Shows current status of the offer (e.g., active, used, expired).

---

## Epic: Authentication

### Screen: Login  
**Wireframe:** `woppa-wireframe-4-register.png`  
**Description:**  
Allows users to log in with email and password or Google. Includes a logout option.

### Screen: Register  
**Wireframe:** `woppa-wireframe-4-register.png`  
**Description:**  
Enables account creation using email and password or Google. After email and password registration, a verification email is sent to confirm the user's address.

### Screen: Email Verification  
**Wireframe:** _Not defined_  
**Description:**  
Screen shown after the user clicks the verification link in their email. If using Firebase Auth, email confirmation can be completed via web link without entering a code. However, we may still display a confirmation screen to inform the user and trigger a backend check to verify their status.

> In the early stages of the project, email verification may be skipped. Since all offers must be paid through Mercado Pago, and this process requires a real user and valid payment method, it helps prevent abuse even without email validation.


### Screen: Password Reset Request  
**Wireframe:** _Not defined_  
**Description:**  
Allows users to request a password reset by entering their email.

### Screen: Password Reset Confirmation  
**Wireframe:** _Not defined_  
**Description:**  
Lets users set a new password after receiving the reset email.

> ⚠️ Note: If using Firebase Auth with default reset flow, this screen may not be needed. The user can be redirected to a Firebase-hosted page to complete the password reset without a custom UI.

---

## Epic: Account Management

### Screen: Profile  
**Wireframe:** _Not defined_  
**Description:**  
Shows the user's personal information in view-only mode.

### Screen: Purchase History  
**Wireframe:** _Not defined_  
**Description:**  
Displays a list of redeemed offers along with their corresponding codes. Offers are organized by status such as active, used, or expired.

