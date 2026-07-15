# DFD Analysis Examples

> Reference input/output pairs. Use when you need to calibrate your output format.

---

## Example 1: Structured Text Input (Grocery Booking System)

### Input

```json
{
  "structured_input": {
    "users": ["customers", "vendors", "admins"],
    "systempurpose": "A grocery booking system to buy groceries",
    "keyfeatures": "login, search products, add products to cart, checkout and pay, inventory management, user management by admins",
    "hostingenvironment": "AWS",
    "sensitivedata": "credit card numbers, address, phone",
    "thirdpartyservices": ["stripe for payments", "google sso for login"],
    "accessmethods": ["mobile app"],
    "cybercontrols": ["MFA", "RBAC", "encryption in transit", "TLS 1.3", "WAF", "logging and monitoring"]
  }
}
```

### Output

```json
{
  "DFD features": {
    "external_entities": [
      "Customers",
      "Vendors",
      "Admins",
      "Stripe",
      "Google SSO"
    ],
    "processes": [
      "Login",
      "Search Products",
      "Add Product To Cart",
      "Checkout And Pay",
      "Inventory Management",
      "User Management"
    ],
    "data_stores": [
      "Product Database",
      "Order Database"
    ],
    "data_flows": [
      "1. Customers → Login → Google SSO",
      "2. Google SSO → Login → Customers",
      "3. Admins → Login → Google SSO",
      "4. Google SSO → Login → Admins",
      "5. Vendors → Login → Google SSO",
      "6. Google SSO → Login → Vendors",
      "7. Customers → Search Products → Product Database",
      "8. Product Database → Search Products → Customers",
      "9. Customers → Add Product To Cart → Order Database",
      "10. Order Database → Add Product To Cart → Customers",
      "11. Customers → Checkout And Pay → Stripe",
      "12. Stripe → Checkout And Pay → Customers",
      "13. Vendors → Inventory Management → Product Database",
      "14. Product Database → Inventory Management → Vendors",
      "15. Admins → User Management → Google SSO",
      "16. Google SSO → User Management → Admins"
    ],
    "deployment": "AWS Cloud Environment",
    "piidata": [
      "Credit Card Numbers",
      "Address",
      "Phone"
    ],
    "trust_boundaries": [
      {
        "name": "Internet Zone",
        "components": [],
        "children": [
          {"name": "Customer Network", "components": ["Customers"], "children": []},
          {"name": "Vendor Network", "components": ["Vendors"], "children": []},
          {"name": "Admin Network", "components": ["Admins"], "children": []}
        ]
      },
      {
        "name": "AWS Cloud (Protected)",
        "components": [],
        "children": [
          {"name": "DMZ", "components": ["Login", "Search Products", "Add Product To Cart"], "children": []},
          {"name": "Application Zone", "components": ["Checkout And Pay", "Inventory Management", "User Management"], "children": []},
          {"name": "Data Zone", "components": ["Product Database", "Order Database"], "children": []}
        ]
      },
      {
        "name": "External Services Zone",
        "components": ["Stripe", "Google SSO"],
        "children": []
      }
    ],
    "complex_processes": ["Checkout And Pay"],
    "assets": [
      {
        "id": "A01",
        "name": "User Credentials",
        "description": "Login credentials for customers, vendors, and admins",
        "associatedNodes": ["Login", "Google SSO"],
        "sensitivity": "high"
      },
      {
        "id": "A02",
        "name": "Payment Card Data",
        "description": "Credit card numbers used for checkout",
        "associatedNodes": ["Checkout And Pay", "Stripe"],
        "sensitivity": "high"
      },
      {
        "id": "A03",
        "name": "Customer PII",
        "description": "Personal information including address and phone",
        "associatedNodes": ["Order Database"],
        "sensitivity": "medium"
      },
      {
        "id": "A04",
        "name": "Product Inventory Data",
        "description": "Product catalog and stock levels",
        "associatedNodes": ["Product Database", "Inventory Management"],
        "sensitivity": "low"
      }
    ],
    "security_controls": [
      {
        "id": "C01",
        "name": "Multi-Factor Authentication",
        "type": "authentication",
        "description": "MFA required for user authentication",
        "associatedNodes": ["Login"],
        "associatedEdges": ["1", "2", "3", "4", "5", "6"]
      },
      {
        "id": "C02",
        "name": "Role-Based Access Control",
        "type": "authorization",
        "description": "RBAC for different user roles (customers, vendors, admins)",
        "associatedNodes": ["User Management", "Inventory Management"],
        "associatedEdges": []
      },
      {
        "id": "C03",
        "name": "TLS 1.3 Encryption",
        "type": "encryption_transit",
        "description": "All data encrypted in transit using TLS 1.3",
        "associatedNodes": [],
        "associatedEdges": ["1", "2", "3", "4", "5", "6", "7", "8", "9", "10", "11", "12", "13", "14", "15", "16"]
      },
      {
        "id": "C04",
        "name": "Web Application Firewall",
        "type": "network",
        "description": "WAF protecting public-facing endpoints",
        "associatedNodes": ["Login", "Search Products", "Add Product To Cart", "Checkout And Pay"],
        "associatedEdges": []
      },
      {
        "id": "C05",
        "name": "Security Logging",
        "type": "monitoring",
        "description": "Comprehensive logging and monitoring of security events",
        "associatedNodes": ["Login", "Checkout And Pay", "User Management"],
        "associatedEdges": []
      }
    ],
    "threat_actors": [
      {
        "id": "T01",
        "name": "Malicious Customer",
        "description": "Attacker posing as legitimate customer to steal data or commit fraud",
        "targetAssets": ["A01", "A02", "A03"],
        "entryPoints": ["Customers"],
        "threatCategory": "external"
      },
      {
        "id": "T02",
        "name": "Credential Stuffing Bot",
        "description": "Automated attack using stolen credentials from data breaches",
        "targetAssets": ["A01"],
        "entryPoints": ["Customers", "Vendors", "Admins"],
        "threatCategory": "automated"
      },
      {
        "id": "T03",
        "name": "Malicious Insider",
        "description": "Vendor or admin with malicious intent",
        "targetAssets": ["A02", "A03", "A04"],
        "entryPoints": ["Vendors", "Admins"],
        "threatCategory": "insider"
      },
      {
        "id": "T04",
        "name": "Third-Party Compromise",
        "description": "Attack through compromised Stripe or Google SSO integration",
        "targetAssets": ["A01", "A02"],
        "entryPoints": ["Stripe", "Google SSO"],
        "threatCategory": "third_party"
      }
    ]
  }
}
```

---

## Example 2: Image-Derived Input (Healthcare Portal)

### Input

> *Model receives an image of a DFD showing:*
> - Stick figures labeled "Patients" and "Doctors"
> - Cloud shape labeled "AWS"
> - Circles: "Login", "Book Appointment", "View Records", "Prescribe"
> - Cylinders: "Patient DB", "Appointment DB"
> - Rectangle: "Twilio" (with SMS icon)
> - Dashed boundary around everything inside a box labeled "HIPAA Zone"
> - Double-bordered circle on "View Records"

### Extracted Elements (Phase 2)

| Type | Elements |
|------|----------|
| External Entities | Patients, Doctors, Twilio |
| Processes | Login, Book Appointment, View Records, Prescribe |
| Data Stores | Patient Database, Appointment Database |
| Complex Processes | View Records (double-border) |

### Output

```json
{
  "DFD features": {
    "external_entities": ["Patients", "Doctors", "Twilio"],
    "processes": ["Login", "Book Appointment", "View Records", "Prescribe"],
    "data_stores": ["Patient Database", "Appointment Database"],
    "data_flows": [
      "1. Patients → Login → Patient Database",
      "2. Patient Database → Login → Patients",
      "3. Doctors → Login → Patient Database",
      "4. Patient Database → Login → Doctors",
      "5. Patients → Book Appointment → Appointment Database",
      "6. Appointment Database → Book Appointment → Patients",
      "7. Appointment Database → Book Appointment → Twilio",
      "8. Twilio → Book Appointment → Patients",
      "9. Patients → View Records → Patient Database",
      "10. Patient Database → View Records → Patients",
      "11. Doctors → View Records → Patient Database",
      "12. Patient Database → View Records → Doctors",
      "13. Doctors → Prescribe → Patient Database",
      "14. Patient Database → Prescribe → Doctors"
    ],
    "deployment": "AWS Cloud Environment",
    "piidata": ["Patient Health Records", "Personal Information", "Appointment Details"],
    "trust_boundaries": [
      {
        "name": "Internet Zone",
        "components": [],
        "children": [
          {"name": "Patient Network", "components": ["Patients"], "children": []},
          {"name": "Doctor Network", "components": ["Doctors"], "children": []}
        ]
      },
      {
        "name": "AWS Cloud (HIPAA Zone)",
        "components": [],
        "children": [
          {"name": "DMZ", "components": ["Login", "Book Appointment"], "children": []},
          {"name": "Application Zone", "components": ["View Records", "Prescribe"], "children": []},
          {"name": "Data Zone", "components": ["Patient Database", "Appointment Database"], "children": []}
        ]
      },
      {
        "name": "External Services Zone",
        "components": ["Twilio"],
        "children": []
      }
    ],
    "complex_processes": ["View Records"],
    "assets": [
      {
        "id": "A01",
        "name": "Patient Health Records (PHI)",
        "description": "Protected health information including diagnoses, prescriptions, and medical history",
        "associatedNodes": ["View Records", "Prescribe", "Patient Database"],
        "sensitivity": "high"
      },
      {
        "id": "A02",
        "name": "Patient PII",
        "description": "Names, contact info, and demographic data",
        "associatedNodes": ["Login", "Patient Database"],
        "sensitivity": "high"
      },
      {
        "id": "A03",
        "name": "Appointment Data",
        "description": "Scheduling and visit details",
        "associatedNodes": ["Book Appointment", "Appointment Database"],
        "sensitivity": "medium"
      }
    ],
    "security_controls": [],
    "threat_actors": [
      {
        "id": "T01",
        "name": "Unauthorized Data Accessor",
        "description": "Attacker attempting to access patient health records",
        "targetAssets": ["A01", "A02"],
        "entryPoints": ["Patients"],
        "threatCategory": "external"
      },
      {
        "id": "T02",
        "name": "Malicious Insider",
        "description": "Healthcare worker accessing records beyond their authorization",
        "targetAssets": ["A01"],
        "entryPoints": ["Doctors"],
        "threatCategory": "insider"
      }
    ]
  }
}
```

---

## Example 3: Natural Language Input (SaaS Dashboard)

### Input

> "We're building a SaaS analytics dashboard. Users are business analysts and admins. Main features are login with Okta, create dashboards, view reports, export data as CSV, manage team members. We use PostgreSQL on GCP. Sensitive data includes business metrics and user emails. We have OpenAI for AI-powered insights."

### Structured Input (Model Converts First)

```json
{
  "structured_input": {
    "users": ["Business Analysts", "Admins"],
    "systempurpose": "SaaS analytics dashboard for business intelligence",
    "keyfeatures": "login, create dashboards, view reports, export data, manage team members, AI-powered insights",
    "hostingenvironment": "GCP",
    "sensitivedata": "business metrics, user emails",
    "thirdpartyservices": ["Okta for SSO", "OpenAI for AI insights"],
    "accessmethods": ["web browser"],
    "cybercontrols": []
  }
}
```

### Output

```json
{
  "DFD features": {
    "external_entities": ["Business Analysts", "Admins", "Okta", "OpenAI"],
    "processes": ["Login", "Create Dashboards", "View Reports", "Export Data", "Manage Team Members", "AI-Powered Insights"],
    "data_stores": ["Dashboard Database", "Report Database", "Team Database"],
    "data_flows": [
      "1. Business Analysts → Login → Okta",
      "2. Okta → Login → Business Analysts",
      "3. Admins → Login → Okta",
      "4. Okta → Login → Admins",
      "5. Business Analysts → Create Dashboards → Dashboard Database",
      "6. Dashboard Database → Create Dashboards → Business Analysts",
      "7. Business Analysts → View Reports → Report Database",
      "8. Report Database → View Reports → Business Analysts",
      "9. Business Analysts → Export Data → Report Database",
      "10. Report Database → Export Data → Business Analysts",
      "11. Admins → Manage Team Members → Team Database",
      "12. Team Database → Manage Team Members → Admins",
      "13. Business Analysts → AI-Powered Insights → OpenAI",
      "14. OpenAI → AI-Powered Insights → Business Analysts"
    ],
    "deployment": "GCP Cloud Environment",
    "piidata": ["Business Metrics", "User Emails"],
    "trust_boundaries": [
      {
        "name": "Internet Zone",
        "components": [],
        "children": [
          {"name": "Analyst Network", "components": ["Business Analysts"], "children": []},
          {"name": "Admin Network", "components": ["Admins"], "children": []}
        ]
      },
      {
        "name": "GCP Cloud (Protected)",
        "components": [],
        "children": [
          {"name": "DMZ", "components": ["Login"], "children": []},
          {"name": "Application Zone", "components": ["Create Dashboards", "View Reports", "Export Data", "Manage Team Members", "AI-Powered Insights"], "children": []},
          {"name": "Data Zone", "components": ["Dashboard Database", "Report Database", "Team Database"], "children": []}
        ]
      },
      {
        "name": "External Services Zone",
        "components": ["Okta", "OpenAI"],
        "children": []
      }
    ],
    "complex_processes": ["AI-Powered Insights"],
    "assets": [
      {
        "id": "A01",
        "name": "User Credentials",
        "description": "SSO tokens and session data managed by Okta",
        "associatedNodes": ["Login", "Okta"],
        "sensitivity": "high"
      },
      {
        "id": "A02",
        "name": "Business Intelligence Data",
        "description": "Proprietary business metrics and analytics",
        "associatedNodes": ["Dashboard Database", "Report Database", "View Reports", "Create Dashboards"],
        "sensitivity": "high"
      },
      {
        "id": "A03",
        "name": "User PII",
        "description": "User emails and team member information",
        "associatedNodes": ["Team Database", "Manage Team Members"],
        "sensitivity": "medium"
      }
    ],
    "security_controls": [],
    "threat_actors": [
      {
        "id": "T01",
        "name": "Corporate Espionage Actor",
        "description": "Competitor seeking access to proprietary business metrics",
        "targetAssets": ["A02"],
        "entryPoints": ["Business Analysts"],
        "threatCategory": "external"
      },
      {
        "id": "T02",
        "name": "Disgruntled Employee",
        "description": "Insider with valid access exfiltrating business data",
        "targetAssets": ["A02", "A03"],
        "entryPoints": ["Admins"],
        "threatCategory": "insider"
      },
      {
        "id": "T03",
        "name": "Compromised AI Provider",
        "description": "Data leakage through OpenAI API integration",
        "targetAssets": ["A02"],
        "entryPoints": ["OpenAI"],
        "threatCategory": "third_party"
      }
    ]
  }
}
```

---

## Common Anti-Examples

### ❌ Invalid: Direct entity-to-store flow

```
"3. Customer → Product Database"
```

**Fix:** `"3. Customer → Search Products → Product Database"`

### ❌ Invalid: Direct entity-to-entity flow

```
"5. Stripe → Customer"
```

**Fix:** `"5. Stripe → Checkout And Pay → Customer"`

### ❌ Invalid: Missing return flow

```
"7. Customer → Search Products → Product Database"
(no flow 8 returning results)
```

**Fix:** Add `"8. Product Database → Search Products → Customer"`

### ❌ Invalid: Orphan process

Processes listed but never appearing in any flow → must be connected. Run Phase 5 orphan resolution.

### ❌ Invalid: Inconsistent naming

```
"associatedNodes": ["login"]    ← lowercase
"processes": ["Login"]          ← capitalized
```

Names must match exactly across all fields.
