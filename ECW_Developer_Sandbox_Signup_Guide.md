# eClinicalWorks (ECW) Developer Sandbox Signup Guide

This guide walks through the process of registering for an eClinicalWorks developer sandbox environment to build and test FHIR-based integrations with the eClinicalWorks EHR — relevant to the HealthTexas Medical Group demo project.

---

## 1. Choose the Right Portal

ECW offers **two separate developer portals** depending on the type of application you're building:

| Portal | URL | Use Case |
|--------|-----|----------|
| **eClinicalWorks FHIR Developer Portal** | https://fhir.eclinicalworks.com/ecwopendev/ | Provider-facing apps, SMART on FHIR, bulk/backend services |
| **healow FHIR Developer Portal** | https://connect4.healow.com/ | Patient-facing apps, scheduling platforms, patient data access |

For HealthTexas integrations (provider dashboards, command center, scorecards), use the **eClinicalWorks FHIR Developer Portal**.

---

## 2. Create a Developer Account

1. Navigate to **https://fhir.eclinicalworks.com/ecwopendev/**
2. Click **"Sign Up"** in the top navigation bar (or go directly to `/ecwopendev/global/signup`)
3. Fill in the required registration details:
   - Full name
   - Email address
   - Organization name
   - Password
4. Submit the form and verify your email
5. Wait for account review and approval from eClinicalWorks

> **Note:** You may need a US or North American IP address to access the portal.

---

## 3. Register Your Application

Once your developer account is approved:

1. Log in to the developer portal dashboard
2. Select **"Register New App"**
3. Provide the following details:
   - **App Name** — A descriptive name for your integration
   - **App Type** — Choose between:
     - *Provider-facing* (EHR Launch / Standalone Launch via SMART on FHIR)
     - *Backend Service* (system-to-system, no user interaction)
   - **Redirect URI(s)** — The OAuth callback URL(s) for your application
   - **Scopes** — Select the FHIR resource scopes your app needs (e.g., `patient/*.read`, `user/*.read`, `launch`)
4. Submit the registration

After approval, you will receive a **`client_id`** (and `client_secret` for confidential apps) to use with the sandbox.

---

## 4. Sandbox Environment Details

### Provider-Centric (FHIR R4)

| Component | URL |
|-----------|-----|
| FHIR R4 Resource Server (Staging) | `https://staging-fhir.ecwcloud.com/fhir/r4/` |
| OAuth Authorization Server (Staging) | `https://staging-oauthserver.ecwcloud.com/oauth/oauth2/authorize` |

### Patient-Centric (healow)

| Component | URL |
|-----------|-----|
| FHIR Sandbox API | `https://fhir-sandbox.healow.com/apps/api/v1/fhir/` |

The sandbox includes sample patient data for testing. No real patient data is used.

---

## 5. Authentication Setup

ECW uses **OAuth 2.0 / SMART on FHIR** for authorization:

### For SMART on FHIR Apps (EHR Launch / Standalone)
1. Your app redirects the user to the ECW authorization endpoint
2. The user authenticates and authorizes scopes
3. ECW returns an authorization code to your redirect URI
4. Exchange the code for an access token
5. Use the access token to call FHIR API endpoints

### For Backend Services
1. Set up an endpoint that serves your **JWKS (JSON Web Key Set)** signing public key
2. Register the JWKS URI during app registration
3. Generate a signed JWT assertion
4. Exchange the JWT for an access token using the `client_credentials` grant

---

## 6. Access API Documentation

- **Getting Started Guide**: Available from the developer portal navigation after login
- **Full API Documentation**: https://fhir.eclinicalworks.com/ecwopendev/documentation#
- **FHIR R4 Specification**: https://hl7.org/fhir/R4/

---

## 7. Cost

Certified FHIR APIs are currently available to third-party application developers and eClinicalWorks customers **at no cost**. eClinicalWorks will provide at least 30 days notice before any future API licensing or usage fees take effect.

---

## 8. Tips & Troubleshooting

- **IP Restrictions**: Access may require a US/North American IP address. Use a VPN if located outside this region.
- **JWT/JWK Differences**: The JWT/JWK flow in ECW may differ from other EHR platforms (e.g., Epic). If you encounter issues, contact ECW developer support through the portal's "Contact Us" option.
- **Scope Mismatches**: Ensure the scopes requested at runtime are a subset of the scopes registered during app registration.
- **Community Support**: The [SMART on FHIR Google Group](https://groups.google.com/g/smart-on-fhir) and [HAPI FHIR Google Group](https://groups.google.com/g/hapi-fhir) have threads with ECW-specific troubleshooting.

---

## 9. Relevant Links

| Resource | URL |
|----------|-----|
| ECW Developer Portal | https://fhir.eclinicalworks.com/ecwopendev/ |
| healow Developer Portal | https://connect4.healow.com/ |
| ECW Interoperability Page | https://www.eclinicalworks.com/products-services/interoperability/ |
| ECW Blog — FHIR API | https://blog.eclinicalworks.com/topic/fhir-api |
| ECW Blog — APIs | https://blog.eclinicalworks.com/topic/apis |
| eClinicalWorks Main Site | https://www.eclinicalworks.com/ |
