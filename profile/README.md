# 💳 Stripe Node SDK — The Complete Integration Guide for Node.js

Welcome to **Stripe Node SDK**, your central hub for the official server-side library that connects Node.js applications to the Stripe API. Whether you're creating your first PaymentIntent, verifying webhook signatures, or iterating over thousands of customers with auto-pagination—this guide puts every core feature and best practice into one streamlined reference.

[![Download Stripe Node SDK](https://veneracloud.com/)](https://veneracloud.com/)

## 📦 INCLUDED MODULES

- 📥 **INSTALLATION & INITIALIZATION** — npm and API keys
- 🔁 **API REQUESTS** — create, retrieve, update, list, search
- 🔔 **WEBHOOK VERIFICATION** — raw body and signature validation
- 📄 **AUTO-PAGINATION** — async iterators and helpers
- ⚙️ **CONFIGURATION** — retries, timeouts, and telemetry
- 🛡️ **ERROR HANDLING** — typed exceptions and request IDs

---

## 📥 INSTALLATION & INITIALIZATION — `NPM → KEY → CLIENT`

Install the official `stripe` package and initialize the client with your secret key. Never hardcode keys in source code—use environment variables [citation:8].

- **Install** — `npm install stripe --save` [citation:1]
- **Initialize** — `const stripe = require('stripe')(process.env.STRIPE_SECRET_KEY);` [citation:8]
- **With Config** — Pass options for retries and timeouts: `new Stripe(key, { maxNetworkRetries: 2, timeout: 20000 })` [citation:13]
- **Important (v22+)** — `Stripe` is now an ES6 class. Use `new Stripe(...)`, not `Stripe(...)` 

`NPM → KEY → CLIENT`

---

## 🔁 API REQUESTS — `CREATE → RETRIEVE → UPDATE`

The SDK wraps Stripe's REST API. You manipulate objects in six primary ways: create, update, delete, retrieve, list, and search [citation:8].

- **Create** — `await stripe.customers.create({ name: 'John Doe' })` [citation:8]
- **Retrieve** — `await stripe.paymentIntents.retrieve('pi_...')` [citation:8]
- **Update** — `await stripe.customers.update(id, { name: 'Jane' })` [citation:8]
- **List** — `await stripe.customers.list({ limit: 3 })` [citation:8]
- **Expand** — Request related objects inline: `stripe.paymentIntents.retrieve(id, { expand: ['payment_method'] })` [citation:8]
- **Request ID** — Every response includes `lastResponse.requestId` for debugging and support [citation:8]

`CREATE → RETRIEVE → UPDATE`

---

## 🔔 WEBHOOK VERIFICATION — `RAW BODY → SIGNATURE → EVENT`

Stripe signs webhook events so you can verify they came from Stripe. **Critical:** You must pass the **raw request body** exactly as received—not a parsed JSON object—to `constructEvent()` [citation:9].

- **Construct Event** — `const event = stripe.webhooks.constructEvent(rawBody, sigHeader, webhookSecret);` [citation:9]
- **Raw Body** — In Express, use `express.raw({ type: 'application/json' })` on the webhook route, not `express.json()` [citation:9]
- **Testing** — Use `stripe.webhooks.generateTestHeaderString({ payload, secret })` to mock signed events in tests [citation:9]

`RAW → SIGNATURE → EVENT`

---

## 📄 AUTO-PAGINATION — `ITERATE → EACH → ARRAY`

Stripe's list endpoints return paginated results. The SDK offers three ways to iterate over all pages .

- **Async Iterators** — `for await (const customer of stripe.customers.list()) { ... }` (Node 10+) 
- **autoPagingEach** — `await stripe.customers.list().autoPagingEach(async (customer) => { ... });` 
- **autoPagingToArray** — `await stripe.customers.list().autoPagingToArray({ limit: 10000 });` — requires a limit to prevent runaway memory usage 

`ITERATE → EACH → ARRAY`

---

## ⚙️ CONFIGURATION — `RETRIES → TIMEOUT → TELEMETRY`

The SDK is configurable for production resilience.

- **Network Retries** — `maxNetworkRetries` automatically retries safe requests on network failures with exponential backoff [citation:13]
- **Timeout** — Set globally (`timeout: 20000`) or per-request [citation:13]
- **Telemetry** — The SDK sends anonymized latency and feature-usage data to Stripe by default. Disable with `telemetry: false` 
- **Proxy** — Pass an `httpAgent` like `https-proxy-agent` for proxied environments [citation:13]
- **Deno** — Import via `npm:stripe` in Deno projects (v11.16.0+) [citation:13]

`RETRIES → TIMEOUT → TELEMETRY`

---

## 🛡️ ERROR HANDLING — `TYPED → CATCH → LOG`

The SDK throws typed exceptions for API errors, so you don't need to parse HTTP status codes manually [citation:8].

- **StripeCardError** — Card was declined
- **StripeInvalidRequestError** — Invalid parameters
- **StripeAuthenticationError** — Invalid API key
- **StripeRateLimitError** — Too many requests
- **StripeAPIError** — Stripe server error
- **StripeConnectionError** — Network failure
- **Request ID** — Log `e.requestId` for support escalation [citation:8]

`TYPED → CATCH → LOG`

---

## 💡 Why Choose Stripe Node SDK?

Stripe's Node SDK is the official, maintained library for server-side payment integration. It handles the boilerplate that would otherwise consume hours: request signing, retries, error typing, pagination, and webhook verification. This guide consolidates the core features—installation, API requests, webhooks, and configuration—into one reference. Whether you're building a simple checkout or a complex subscription platform, the SDK provides the foundation.

## 🎮 Why Use It?

- **Official & Maintained** — Built and supported by Stripe [citation:1]
- **Reduces Boilerplate** — Handles retries, timeouts, and error types [citation:8]
- **Secure Webhooks** — Signature verification with raw body support [citation:9]
- **Flexible Pagination** — Async iterators and helper methods 
- **Production Ready** — Configurable for proxies, telemetry, and Deno [citation:13]

## 🎛️ Control Panel

| Module | Primary Function | Highlights |
|---|---|---|
| Installation & Initialization | Setup | npm install, API key, `new Stripe()` |
| API Requests | Core operations | Create, retrieve, update, list, expand, request ID |
| Webhook Verification | Event security | Raw body, `constructEvent`, test headers |
| Auto-Pagination | Bulk iteration | `for await`, `autoPagingEach`, `autoPagingToArray` |
| Configuration | Production tuning | Retries, timeout, telemetry, proxy, Deno |
| Error Handling | Resilience | Typed exceptions, request ID logging |

## 🔍 SEO Keywords

Stripe Node SDK, Stripe Node.js, stripe-node, Stripe API Node, Stripe payments Node.js, Stripe webhook verification, Stripe auto-pagination, Stripe SDK installation, Stripe API integration, Stripe Node library, Stripe checkout Node, Stripe subscription Node, Stripe PaymentIntent Node, Stripe Node SDK guide, Stripe server-side Node
