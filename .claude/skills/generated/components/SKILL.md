---
name: components
description: "Skill for the _components area of Securacy. 65 symbols across 19 files."
---

# _components

65 symbols | 19 files | Cohesion: 80%

## When to Use

- Working with code in `securacyfrontend/`
- Understanding how generateBusinessImpactReport, DisplayThreatAndMitigations, getThreatMitigation work
- Modifying _components-related functionality

## Key Files

| File | Symbols |
|------|---------|
| `securacyfrontend/app/home/settings/_components/subscription-panel.tsx` | calcAmount, addMonths, fmtINR, UpgradeCards, ExtendPreview (+6) |
| `securacyfrontend/app/home/(bots)/_components/DisplayThreatAndMitigations.tsx` | DisplayThreatAndMitigations, getThreatMitigation, getThreatMitigationCompliance, getSeverityBadgeClass, getRiskLevelBadgeClass (+4) |
| `securacyfrontend/app/home/settings/_components/profile-form.tsx` | hasChanges, handleSave, load, formatDate, daysUntil (+3) |
| `securacyfrontend/app/home/(bots)/_components/DisplayPrivacyThreatAndMitigations.tsx` | downloadPDF, DisplayPrivacyThreatAndMitigations, getCategoryColor, getSeverityBadgeClass, getPriorityColor (+1) |
| `securacyfrontend/lib/api_call_config.ts` | decodeJwt, fetchAndStoreAccessToken, getValidAccessToken, apiCallPost, apiCallPut |
| `securacyfrontend/app/home/settings/_components/api-keys-section.tsx` | formatDate, ApiKeysSection, handleCreate, handleCopy |
| `securacyfrontend/services/mcpService.ts` | fetchApiKeys, createApiKey, fetchUsage |
| `securacyfrontend/app/home/(bots)/_components/UploadDropzoneCard.tsx` | handleDrop, handleFileChange, validateAndSelect |
| `securacyfrontend/app/home/pricing/_components/PricingCard.tsx` | PricingCard, formatPrice |
| `securacyfrontend/services/userService.ts` | updateUser, fetchLicense |

## Entry Points

Start here when exploring this area:

- **`generateBusinessImpactReport`** (Function) — `securacyfrontend/services/generatebusinessImpactReport.ts:10`
- **`DisplayThreatAndMitigations`** (Function) — `securacyfrontend/app/home/(bots)/_components/DisplayThreatAndMitigations.tsx:76`
- **`getThreatMitigation`** (Function) — `securacyfrontend/app/home/(bots)/_components/DisplayThreatAndMitigations.tsx:134`
- **`getThreatMitigationCompliance`** (Function) — `securacyfrontend/app/home/(bots)/_components/DisplayThreatAndMitigations.tsx:140`
- **`getSeverityBadgeClass`** (Function) — `securacyfrontend/app/home/(bots)/_components/DisplayThreatAndMitigations.tsx:152`

## Key Symbols

| Symbol | Type | File | Line |
|--------|------|------|------|
| `generateBusinessImpactReport` | Function | `securacyfrontend/services/generatebusinessImpactReport.ts` | 10 |
| `DisplayThreatAndMitigations` | Function | `securacyfrontend/app/home/(bots)/_components/DisplayThreatAndMitigations.tsx` | 76 |
| `getThreatMitigation` | Function | `securacyfrontend/app/home/(bots)/_components/DisplayThreatAndMitigations.tsx` | 134 |
| `getThreatMitigationCompliance` | Function | `securacyfrontend/app/home/(bots)/_components/DisplayThreatAndMitigations.tsx` | 140 |
| `getSeverityBadgeClass` | Function | `securacyfrontend/app/home/(bots)/_components/DisplayThreatAndMitigations.tsx` | 152 |
| `getRiskLevelBadgeClass` | Function | `securacyfrontend/app/home/(bots)/_components/DisplayThreatAndMitigations.tsx` | 175 |
| `downloadCSV` | Function | `securacyfrontend/app/home/(bots)/_components/DisplayThreatAndMitigations.tsx` | 207 |
| `handleGenerateBusinessImpactReport` | Function | `securacyfrontend/app/home/(bots)/_components/DisplayThreatAndMitigations.tsx` | 316 |
| `getStatusColor` | Function | `securacyfrontend/app/home/(bots)/_components/DisplayThreatAndMitigations.tsx` | 511 |
| `SubscriptionPanel` | Function | `securacyfrontend/app/home/settings/_components/subscription-panel.tsx` | 334 |
| `openMode` | Function | `securacyfrontend/app/home/settings/_components/subscription-panel.tsx` | 357 |
| `fetchAndStoreAccessToken` | Function | `securacyfrontend/lib/api_call_config.ts` | 42 |
| `getValidAccessToken` | Function | `securacyfrontend/lib/api_call_config.ts` | 87 |
| `apiCallPost` | Function | `securacyfrontend/lib/api_call_config.ts` | 201 |
| `downloadPDF` | Function | `securacyfrontend/app/home/(bots)/_components/DisplayThreatAndMitigations.tsx` | 267 |
| `downloadPDF` | Function | `securacyfrontend/app/home/(bots)/_components/DisplayPrivacyThreatAndMitigations.tsx` | 151 |
| `fetchApiKeys` | Function | `securacyfrontend/services/mcpService.ts` | 50 |
| `createApiKey` | Function | `securacyfrontend/services/mcpService.ts` | 55 |
| `ApiKeysSection` | Function | `securacyfrontend/app/home/settings/_components/api-keys-section.tsx` | 38 |
| `handleCreate` | Function | `securacyfrontend/app/home/settings/_components/api-keys-section.tsx` | 62 |

## Execution Flows

| Flow | Type | Steps |
|------|------|-------|
| `PrivacyBot → DecodeJwt` | cross_community | 8 |
| `AppsecBot → DecodeJwt` | cross_community | 8 |
| `OnboardingPage → DecodeJwt` | cross_community | 7 |
| `HandleNextQuestion → DecodeJwt` | cross_community | 7 |
| `HandleNextQuestion → DecodeJwt` | cross_community | 7 |
| `ApiKeysSection → DecodeJwt` | cross_community | 7 |
| `HandleNextPrivacyQuestion → DecodeJwt` | cross_community | 6 |
| `SubscriptionPanel → DecodeJwt` | cross_community | 6 |
| `DisplayThreatAndMitigations → DecodeJwt` | cross_community | 6 |
| `HandleSave → DecodeJwt` | cross_community | 6 |

## Connected Areas

| Area | Connections |
|------|-------------|
| Context | 5 calls |
| Hooks | 3 calls |
| Onboarding | 1 calls |
| Components | 1 calls |

## How to Explore

1. `gitnexus_context({name: "generateBusinessImpactReport"})` — see callers and callees
2. `gitnexus_query({query: "_components"})` — find related execution flows
3. Read key files listed above for implementation details
