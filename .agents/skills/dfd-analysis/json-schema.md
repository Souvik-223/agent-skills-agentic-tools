# DFD Features JSON Schema

> **Always read this file.** It contains the definitive output schema, all field rules, naming conventions, and entity-to-process mapping tables.

---

## Output Structure

```json
{
  "DFD features": {
    "external_entities": ["string"],
    "processes": ["string"],
    "data_stores": ["string"],
    "data_flows": ["string"],
    "deployment": "string",
    "piidata": ["string"],
    "trust_boundaries": [TrustBoundary],
    "complex_processes": ["string"],
    "assets": [Asset],
    "security_controls": [SecurityControl],
    "threat_actors": [ThreatActor]
  }
}
```

---

## Field Specifications

### external_entities: `string[]`

Properly capitalized names of all external entities (users + third-party services).

**Normalization rules:**

| Raw Input | Normalized Output |
|-----------|-------------------|
| `customers` | `Customers` |
| `google login` | `Google SSO` |
| `stripe for payments` | `Stripe` |
| `phonePe payment` | `PhonePe` |
| `open ai` | `OpenAI` |
| `azure open ai` | `Azure OpenAI` |
| `elastic search` | `Elasticsearch` |
| `google maps` | `Google Maps` |
| `facebook login` | `Facebook SSO` |
| `twilio for sms` | `Twilio` |
| `aws s3` | `Amazon S3` |

---

### processes: `string[]`

Each word capitalized. Derived from `keyfeatures`.

**Payment rule:** Add `Process Payment` ONLY if payment handling isn't explicitly in keyfeatures via checkout/pay features.

---

### data_stores: `string[]`

Derived from processes, NOT from input directly.

**Naming derivation rules:**

| Process Pattern | Data Store Name |
|----------------|----------------|
| `Manage [Entity]` | `[Entity] Database` |
| `Manage [Entity]s` | `[Entity] Database` (singular) |
| `Manage Blog Posts` | `Blog Database` |
| `Manage Customer Information` | `Customer Database` |
| `Search Products` | `Product Database` |
| `Track Orders` | `Order Database` |
| `View Analytics` | `Analytics Database` |

**Exclusion rules:**
- No `User Database` if SSO handles authentication externally
- No `Payment Database` if payments handled entirely by third-party (Stripe, PayPal)

---

### data_flows: `string[]`

Format: `"N. Source → Process → Target"`

**Mandatory pattern:** Source → Process → Target (every flow passes through a process)

**Invalid flows (NEVER produce these):**

| Invalid | Why | Correct |
|---------|-----|---------|
| `Stripe → Payment Database` | Entity → Data Store directly | `Stripe → Process Payment → Payment Database` |
| `Customer → User Database` | Entity → Data Store directly | `Customer → Login → User Database` |
| `Stripe → Customer` | Entity → Entity directly | `Stripe → Process Payment → Customer` |

**Numbering:** Sequential integers starting at 1. Use `→` arrow symbol.

---

### deployment: `string`

Single string. Always include "Environment" suffix.

| Input | Output |
|-------|--------|
| `AWS` | `AWS Cloud Environment` |
| `GCP` | `GCP Cloud Environment` |
| `Azure` | `Azure Cloud Environment` |
| `on-premises` | `On-Premises Environment` |
| `hybrid` | `Hybrid Cloud Environment` |

---

### piidata: `string[]`

Properly capitalized sensitive data items from `sensitivedata` input.

---

### trust_boundaries: `TrustBoundary[]`

```json
{
  "name": "string",
  "components": ["string"],
  "children": [TrustBoundary]
}
```

Hierarchical nesting. `components` contains names of entities/processes/stores **inside** this zone (not in child zones). `children` contains nested sub-zones.

**Standard zones:**

| Zone | Typical Components |
|------|-------------------|
| Internet Zone | (empty) — contains child networks |
| → Customer Network | `Customers` |
| → Vendor Network | `Vendors` |
| → Admin Network | `Admins` |
| [Cloud] (Protected) | (empty) — contains DMZ, App Zone, Data Zone |
| → DMZ | Public-facing processes (Login, Search, Browse) |
| → Application Zone | Business logic (Checkout, Inventory Mgmt) |
| → Data Zone | All databases |
| External Services Zone | Third-party entities (Stripe, Google SSO) |
| PCI Zone | Payment processes (if handling card data directly) |

**Component name matching:** Names in `components` must exactly match names in `external_entities`, `processes`, or `data_stores`.

---

### complex_processes: `string[]`

Names of processes that are multi-step, critical, or high-risk. These get double-border rendering in the DFD.

Common complex processes: `Process Payment`, `AI Analysis`, `Order Fulfillment`, `Risk Assessment`.

---

### assets: `Asset[]`

```json
{
  "id": "A01",
  "name": "string",
  "description": "string",
  "associatedNodes": ["string"],
  "sensitivity": "high" | "medium" | "low"
}
```

**ID format:** `A01`, `A02`, ... sequential, no gaps.

**Priority:** Use input `assets` if provided. Otherwise derive from `sensitivedata` + processes/data stores.

**Common assets:**

| Asset | Sensitivity | Typical Associated Nodes |
|-------|------------|-------------------------|
| User Credentials | high | Login, [Auth Provider] |
| Payment Card Data | high | Checkout, [Payment Provider] |
| Customer PII | medium | [User-facing processes], [User DB] |
| Health Records (PHI) | high | [Healthcare processes] |
| Business Data | medium | [Internal processes] |
| API Keys/Secrets | high | [Integration processes] |
| Product/Inventory Data | low | [Inventory processes], [Product DB] |

---

### security_controls: `SecurityControl[]`

```json
{
  "id": "C01",
  "name": "string",
  "type": "authentication" | "authorization" | "encryption_transit" | "encryption_rest" | "monitoring" | "network" | "access_control",
  "description": "string",
  "associatedNodes": ["string"],
  "associatedEdges": ["string"]
}
```

**ID format:** `C01`, `C02`, ... sequential, no gaps.

**Type mapping:**

| Type | Controls That Map Here |
|------|----------------------|
| `authentication` | MFA, SSO, OAuth, Biometric, Password policies |
| `authorization` | RBAC, ABAC, Least Privilege, JWT, API scopes |
| `encryption_transit` | TLS, HTTPS, mTLS, VPN, E2E encryption |
| `encryption_rest` | AES-256, KMS, TDE, Disk encryption |
| `monitoring` | SIEM, Logging, IDS/IPS, Vulnerability scanning |
| `network` | WAF, Firewall, DDoS protection, Network segmentation |
| `access_control` | IP whitelisting, Rate limiting, Session management |

**`associatedEdges`:** Reference flow numbers as strings (`"1"`, `"2"`). Transit encryption controls should reference ALL flow numbers.

---

### threat_actors: `ThreatActor[]`

```json
{
  "id": "T01",
  "name": "string",
  "description": "string",
  "targetAssets": ["A01"],
  "entryPoints": ["string"],
  "threatCategory": "external" | "insider" | "third_party" | "automated"
}
```

**ID format:** `T01`, `T02`, ... sequential, no gaps.

**Priority:** Use input `threat_actors` if provided. Otherwise infer.

**Common threat actors:**

| Actor | Category | Typical Entry Points | Typical Targets |
|-------|----------|---------------------|-----------------|
| Malicious External User | `external` | User-type entities | Credentials, PII |
| Credential Stuffing Bot | `automated` | All user-type entities | Credentials |
| Malicious Insider | `insider` | Admin/Vendor entities | Business data, PII |
| Compromised Third Party | `third_party` | Third-party entities | Credentials, Payment data |
| Social Engineer | `external` | User-type entities | Credentials, PII |
| DDoS Attacker | `automated` | Public-facing processes | Availability |
| Supply Chain Attacker | `third_party` | Third-party entities | All assets |

**`targetAssets`:** Reference asset IDs (`"A01"`). **`entryPoints`:** Reference external entity names exactly.

---

## Entity-to-Process Mapping Table (Complete)

Use this to connect external entities to the correct processes in data flows.

| External Entity Type | Matches Processes Containing Keywords |
|---------------------|--------------------------------------|
| **Payment** (Stripe, UPI, PayPal, Razorpay, PhonePe) | payment, pay, checkout, transaction, billing |
| **Search** (Elasticsearch, Algolia) | search, browse, find, query, discover |
| **Maps/Location** (Google Maps, Mapbox) | map, location, track, navigate, route, delivery |
| **Authentication** (Azure AD, SSO, Okta, Auth0, Google SSO) | login, auth, sign, authenticate, authorize, identity |
| **Communication** (Twilio, SendGrid, Mailgun, SES) | track, sms, notify, message, communicate, email, confirm, alert |
| **Content Management** (Hygraph, Contentful, Sanity) | content, manage, publish, create, edit, update, cms |
| **Banking** (Bank, Plaid) | payment, transfer, financial, transaction, account |
| **AI Services** (OpenAI, Claude, Bedrock, Gemini, Azure OpenAI, Llama) | generate, analyze, predict, recommend, chat, summarize, process, assistant |
| **Cache/Queue** (Redis, RabbitMQ, Kafka, SQS) | cache, queue, session, worker, publish, subscribe |
| **Monitoring** (Datadog, Splunk, Prometheus, CloudWatch) | log, monitor, alert, trace, metrics |
| **Cloud Storage** (S3, Azure Blob, GCS) | upload, download, store, backup, archive |
| **Admin users** | create, update, delete user accounts, manage inventory, manage subscriptions |

---

## Orphan Resolution Rules

After generating all flows, check for orphans (entities/processes/stores not in any flow).

### Orphan Process

Match to entity whose **role** relates to the process function:
- Inventory/Stock processes → `Store Managers`, `Vendors`, `Warehouse Staff` (NOT `Customers`)
- Payment processes → Payment entities or `Customers`
- Admin processes → `Admins`, `System Admins`
- Analytics/Report processes → `Analysts`, `Managers`, internal systems

Then connect to the data store that would store that process's output.

### Orphan External Entity

Match to process that **needs** that entity type:
- User-type (Customers, Vendors) → User-facing processes (Login, Browse, Order)
- Service-type (Stripe, OpenAI) → Integration processes (Payment, Generate)
- Admin-type → Management processes

### Orphan Data Store

Match to process that would **read/write** that data:
- `User Database` → Login, User Management
- `Order Database` → Order, Checkout, Tracking
- `Product Database` → Search, Inventory, Catalog

**New orphan flows:** Number sequentially after last existing flow. Entity cannot directly connect to data store — must go through a process.

---

## Format Requirements Summary

| Rule | Detail |
|------|--------|
| Empty categories | Use `[]` |
| String capitalization | Proper case on all names |
| No placeholders | No `[string]` or `TODO` in output |
| Data flow format | `"N. Source → Process → Target"` |
| Deployment | Single string with "Environment" |
| Asset IDs | `A01`, `A02`... (sequential) |
| Control IDs | `C01`, `C02`... (sequential) |
| Threat IDs | `T01`, `T02`... (sequential) |
| No code fences | Raw JSON, no ` ```json ` wrapper |
