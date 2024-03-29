# CoinPact REST API Docs
![https://github.com/dimondevceo/coinpact/blob/main/banner.png](https://raw.githubusercontent.com/dimondevceo/coinpact/main/banner.png)

## Overview

CoinPact is a crypto payment gateway that allows businesses to accept payments with zero commissions and provides full control over the address to which customers send funds. This documentation outlines the REST API endpoints that users can utilize to interact with CoinPact.

### Base URL

The base URL for all API endpoints is: `https://coinpact.ch/api`

## Endpoints

### 1. Generate Checkout

#### Endpoint

- URL: `/generate_checkout`
- Method: `GET`

#### Parameters (url path)

- `product_uuid` (UUID): The UUID of the product for which the checkout is being generated (get it in dashboard > products).
- `user_wallet` (string): The user's crypto wallet address.
- `uid` (string): The unique external identifier of the user (eg. Telegram ID, User ID in your database).
- `params` (JSON): Additional parameters for checkout configuration.

#### Example

```
{
  "product_uuid": "123e4567-e89b-12d3-a456-426614174001",
  "user_wallet": "1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa",
  "uid": "user123",
  "params": "{\"param1\": \"value1\", \"param2\": \"value2\"}"
}
```

#### Response

- **Success:**
  - Status: 200 OK
  - JSON: `{ "status": "success", "checkout_token": "token123", "checkout_url": "https://coinpact.ch/api/checkout/token123" }`
- **Error:**
  - Status: 404 Not Found
  - JSON: `{"status": "error", "message": "Error message"}`

---

### 2. Generate Onboarding

#### Endpoint

- URL: `/generate_onboarding`
- Method: `GET`

#### Parameters (url path)

- `product_uuid` (UUID): The UUID of the product for which onboarding is being generated (get it in dashboard > products).
- `uid` (string): The unique identifier of the user (eg. Telegram ID, User ID in your database).
- `params` (JSON): Additional parameters for onboarding configuration.

#### Example

```
{
  "product_uuid": "123e4567-e89b-12d3-a456-426614174001",
  "uid": "user123",
  "params": "{\"param1\": \"value1\", \"param2\": \"value2\"}"
}
```

#### Response

- **Success:**
  - Status: 200 OK
  - JSON: `{ "status": "success", "onboarding_token": "token456", "onboarding_url": "https://coinpact.ch/api/onboarding/token456" }`
- **Error:**
  - Status: 404 Not Found
  - JSON: `{"status": "error", "message": "Error message"}`

---

### 3. Check User Subscription

#### Endpoint

- URL: `/check_subscription`
- Method: `GET`

#### Parameters (url path)

- `product_uuid` (UUID): The UUID of the product for which onboarding is being generated (get it in dashboard > products).
- `uid` (string): The unique identifier of the user (eg. Telegram ID, User ID in your database).

#### Example

```
{
  "product_uuid": "123e4567-e89b-12d3-a456-426614174001",
  "uid": "user123",
}
```

#### Response

- **Success:**
  - Status: 200 OK
  - JSON: `{ "status": "success", "is_subscriber": true, "is_paid": true, "subscribed_until": 1704056400.00000 }`
- **Error:**
  - Status: 404 Not Found
  - JSON: `{"status": "error", "message": "Error message"}`

---

### 4. Generate Checkout from Frontend

#### Endpoint

- URL: `/generate_checkout_f`
- Method: `GET`

#### Parameters (url path)

- `token` (string): The checkout token generated in endpoint 1.
- `user_wallet` (string): The user's crypto wallet address.

#### Example

```
{
  "token": "token789",
  "user_wallet": "bc1xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
}
```

#### Response

- **Success:**
  - Status: 200 OK
  - JSON: `{ "status": "success", "checkout_token": "token789", "checkout_url": "https://coinpact.ch/api/checkout/token789" }`
- **Error:**
  - Status: 404 Not Found
  - JSON: `{"status": "error", "message": "Error message"}`

---

### Rate Limiting

- Rate limiting is enforced to prevent abuse and server overloading.
- Requests are limited to 1 per second per IP address.

#### Example

```
{
  "status": "ratelimit",
  "message": "Too many requests, please try again in 30 seconds."
}
```

## Future Updates

- [x] Add Payment Status endpoint
- [ ] Add inline and modal checkouts
- [ ] Add custom callbacks
- [ ] Create Paylink service
- [ ] Add url shortening to onboarding and checkout
- [ ] Add Litecoin support
- [ ] Add Solana support
- [ ] Add Dash support
- [ ] Add XRP support
- [ ] Add Monero support
