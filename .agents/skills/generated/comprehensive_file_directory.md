# 🗂️ Comprehensive File & Symbol Directory

This directory lists the exact files and key symbols extracted automatically from the GitNexus clusters. Securacy contains over 2,500 symbols.

## Cluster: Appsec
| Symbol | Type | File | Line |
|--------|------|------|------|
| `find_entity` | Function | `backend/buddlyai/appsec/drawio.py` | 11 |
| `find_store` | Function | `backend/buddlyai/appsec/drawio.py` | 36 |
| `find_processes` | Function | `backend/buddlyai/appsec/drawio.py` | 45 |
| `find_matching_process` | Function | `backend/buddlyai/appsec/drawio.py` | 67 |
| `parse_flow` | Function | `backend/buddlyai/appsec/drawio.py` | 75 |
| `generate_drawio_dfd` | Function | `backend/buddlyai/appsec/drawio.py` | 128 |
| `get_id` | Function | `backend/buddlyai/appsec/drawio.py` | 152 |
| `is_system_entity` | Function | `backend/buddlyai/appsec/drawio.py` | 254 |
| `get_component_bounds` | Function | `backend/buddlyai/appsec/drawio.py` | 491 |
| `normalize_arrows` | Function | `backend/buddlyai/appsec/drawio.py` | 586 |
| `check_process_overlap` | Function | `backend/buddlyai/appsec/drawio.py` | 952 |
| `find_non_overlapping_position` | Function | `backend/buddlyai/appsec/drawio.py` | 973 |
| `optimize_process_positions` | Function | `backend/buddlyai/appsec/drawio.py` | 1006 |
| `line_circle_intersection` | Function | `backend/buddlyai/appsec/drawio.py` | 1088 |
| `get_connection_line` | Function | `backend/buddlyai/appsec/drawio.py` | 1130 |
| `avoid_arrow_intersections` | Function | `backend/buddlyai/appsec/drawio.py` | 1182 |
| `test_classic_prompt_injection_phrases` | Function | `backend/buddlyai/appsec/test_prompt_injection_detection.py` | 26 |
| `test_ai_specific_injection_tricks` | Function | `backend/buddlyai/appsec/test_prompt_injection_detection.py` | 50 |
| `test_subtle_social_engineering_prompts` | Function | `backend/buddlyai/appsec/test_prompt_injection_detection.py` | 71 |
| `test_combined_injection_attempts` | Function | `backend/buddlyai/appsec/test_prompt_injection_detection.py` | 92 |
| Flow | Type | Steps |
|------|------|-------|
| `AppsecBot → DecodeJwt` | cross_community | 8 |
| `AppsecBot → FindNodeIdByName` | cross_community | 6 |
| `AppsecBot → NormalizeNodeType` | cross_community | 5 |
| `AppsecBot → IsKnownIntegration` | cross_community | 5 |
| `AppsecBot → NameToId` | cross_community | 5 |
| `HandleSaveAnalysis → FindNodeIdByName` | cross_community | 5 |
| `PrivacyBot → GenerateDfdJSON` | cross_community | 4 |
| `AppsecBot → GenerateDfdJSON` | cross_community | 4 |
| `Generate_privacyDFD → GetOrphanedProcessEntityAndStore` | cross_community | 4 |
| `Generate_privacyDFD → _find_suitable_entity` | cross_community | 4 |
| Area | Connections |
|------|-------------|
| Services | 3 calls |
| Privacy | 1 calls |
| Dfd | 1 calls |

## Cluster: Benchmark
| Symbol | Type | File | Line |
|--------|------|------|------|
| `cleanAndParseJson` | Function | `model-compass/src/lib/utils.ts` | 7 |
| `calculateAccuracy` | Function | `model-compass/src/lib/scoring-engine.ts` | 17 |
| `normalize` | Function | `model-compass/src/lib/scoring-engine.ts` | 46 |
| `scoreCategory` | Function | `model-compass/src/lib/scoring-engine.ts` | 48 |
| `POST` | Function | `model-compass/src/app/api/benchmark/route.ts` | 25 |
| `toStr` | Function | `model-compass/src/lib/scoring-engine.ts` | 9 |
| `makeErrorResult` | Function | `model-compass/src/app/api/benchmark/route.ts` | 204 |
| Flow | Type | Steps |
|------|------|-------|
| `POST → Normalize` | intra_community | 4 |
| `POST → ToStr` | intra_community | 4 |
| `POST → CleanAndParseJson` | intra_community | 3 |

## Cluster: Cluster-98
| Symbol | Type | File | Line |
|--------|------|------|------|
| `loadSkillContent` | Function | `model-compass/src/lib/skill-loader.ts` | 3 |
| `constructSystemPrompt` | Function | `model-compass/src/lib/skill-loader.ts` | 32 |
| `runBenchmark` | Method | `model-compass/src/lib/model-runner.ts` | 12 |

## Cluster: Components
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
| Area | Connections |
|------|-------------|
| Context | 5 calls |
| Hooks | 3 calls |
| Onboarding | 1 calls |
| Components | 1 calls |

## Cluster: Components-2
| Symbol | Type | File | Line |
|--------|------|------|------|
| `apiCallDelete` | Function | `securacyfrontend/lib/api_call_config.ts` | 255 |
| `revokeApiKey` | Function | `securacyfrontend/services/mcpService.ts` | 65 |
| `AppSidebar` | Function | `securacyfrontend/components/app-sidebar.tsx` | 116 |
| `fetchThreats` | Function | `securacyfrontend/components/app-sidebar.tsx` | 160 |
| `handleSaved` | Function | `securacyfrontend/components/app-sidebar.tsx` | 184 |
| `handleRevoke` | Function | `securacyfrontend/app/home/settings/_components/api-keys-section.tsx` | 83 |
| `Plasma` | Function | `securacyfrontend/components/Plasma.tsx` | 92 |
| `setSize` | Function | `securacyfrontend/components/Plasma.tsx` | 159 |
| `LineWaves` | Function | `securacyfrontend/components/LineWaves.tsx` | 147 |
| `resize` | Function | `securacyfrontend/components/LineWaves.tsx` | 187 |
| `DecryptedText` | Function | `securacyfrontend/components/DecryptedText.tsx` | 20 |
| `getNextIndex` | Function | `securacyfrontend/components/DecryptedText.tsx` | 45 |
| `shuffleText` | Function | `securacyfrontend/components/DecryptedText.tsx` | 74 |
| `hexToRgb` | Function | `securacyfrontend/components/LetterGlitch.tsx` | 45 |
| `interpolateColor` | Function | `securacyfrontend/components/LetterGlitch.tsx` | 61 |
| `drawLetters` | Function | `securacyfrontend/components/LetterGlitch.tsx` | 115 |
| `handleSmoothTransitions` | Function | `securacyfrontend/components/LetterGlitch.tsx` | 152 |
| `animate` | Function | `securacyfrontend/components/LetterGlitch.tsx` | 173 |
| `LetterGlitch` | Function | `securacyfrontend/components/LetterGlitch.tsx` | 2 |
| `calculateGrid` | Function | `securacyfrontend/components/LetterGlitch.tsx` | 74 |
| Flow | Type | Steps |
|------|------|-------|
| `ApiKeysSection → DecodeJwt` | cross_community | 7 |
| `AppSidebar → DecodeJwt` | cross_community | 6 |
| `HandleSaved → DecodeJwt` | cross_community | 6 |
| `HandleResize → GetRandomChar` | cross_community | 4 |
| `HandleResize → GetRandomColor` | cross_community | 4 |
| `HandleResize → HexToRgb` | cross_community | 4 |
| `HandleResize → InterpolateColor` | cross_community | 4 |
| `HandleResize → DrawLetters` | cross_community | 4 |
| Area | Connections |
|------|-------------|
| _components | 3 calls |
| Hooks | 1 calls |

## Cluster: Contact
| Symbol | Type | File | Line |
|--------|------|------|------|
| `POST` | Function | `securacyfrontend/app/api/contact/route.ts` | 86 |
| `isValidEmail` | Function | `securacyfrontend/app/api/contact/route.ts` | 20 |
| `getResendErrorMessage` | Function | `securacyfrontend/app/api/contact/route.ts` | 25 |
| `escapeHtml` | Function | `securacyfrontend/app/api/contact/route.ts` | 43 |
| `validateBody` | Function | `securacyfrontend/app/api/contact/route.ts` | 51 |
| Flow | Type | Steps |
|------|------|-------|
| `POST → IsValidEmail` | intra_community | 3 |

## Cluster: Context
| Symbol | Type | File | Line |
|--------|------|------|------|
| `useAuth` | Function | `securacyfrontend/context/AuthContext.tsx` | 85 |
| `DashboardPage` | Function | `securacyfrontend/app/home/page.tsx` | 11 |
| `AuthPage` | Function | `securacyfrontend/app/(auth)/page.tsx` | 12 |
| `AccountForm` | Function | `securacyfrontend/app/home/settings/_components/account-form.tsx` | 8 |

## Cluster: Db
| Symbol | Type | File | Line |
|--------|------|------|------|
| `test_db_operations` | Function | `backend/buddlyai/tests/test_dbservice_crud.py` | 11 |
| `get_user` | Function | `backend/buddlyai/Routes/UserController.py` | 50 |
| `update_user` | Function | `backend/buddlyai/Routes/UserController.py` | 67 |
| `delete_user` | Function | `backend/buddlyai/Routes/UserController.py` | 84 |
| `save_threats` | Function | `backend/buddlyai/Routes/ThreatsController.py` | 62 |
| `delete_threat` | Function | `backend/buddlyai/Routes/ThreatsController.py` | 129 |
| `update_threat` | Function | `backend/buddlyai/Routes/ThreatsController.py` | 150 |
| `get_threat_data` | Function | `backend/buddlyai/Routes/ThreatsController.py` | 231 |
| `get_user` | Function | `backend/buddlyai/DB/DBservice.py` | 95 |
| `update_user` | Function | `backend/buddlyai/DB/DBservice.py` | 107 |
| `delete_user` | Function | `backend/buddlyai/DB/DBservice.py` | 129 |
| `insert_threat_run` | Function | `backend/buddlyai/DB/DBservice.py` | 149 |
| `insert_threat_data` | Function | `backend/buddlyai/DB/DBservice.py` | 234 |
| `get_threat_runs` | Function | `backend/buddlyai/DB/DBservice.py` | 246 |
| `get_threat_data` | Function | `backend/buddlyai/DB/DBservice.py` | 257 |
| `update_threat_run` | Function | `backend/buddlyai/DB/DBservice.py` | 389 |
| `delete_threat_run` | Function | `backend/buddlyai/DB/DBservice.py` | 415 |
| `close` | Function | `backend/buddlyai/DB/DBservice.py` | 434 |
| `main` | Function | `backend/buddlyai/DB/DBservice.py` | 441 |
| `setup_module` | Function | `backend/buddlyai/tests/test_controller.py` | 19 |
| Flow | Type | Steps |
|------|------|-------|
| `Main → Connect` | cross_community | 4 |
| `Create_user → Connect` | intra_community | 4 |
| `Main → Commit` | cross_community | 3 |
| `Save_threats → Commit` | cross_community | 3 |
| Area | Connections |
|------|-------------|
| Securacymcp | 7 calls |

## Cluster: Dfd
| Symbol | Type | File | Line |
|--------|------|------|------|
| `assignBoundary` | Function | `securacyfrontend/services/dfd/jsonToIR.ts` | 126 |
| `buildBoundaries` | Function | `securacyfrontend/services/dfd/jsonToIR.ts` | 135 |
| `nameToId` | Function | `securacyfrontend/services/dfd/jsonToIR.ts` | 169 |
| `parseDataFlowStrings` | Function | `securacyfrontend/services/dfd/jsonToIR.ts` | 194 |
| `jsonToIR` | Function | `securacyfrontend/services/dfd/jsonToIR.ts` | 237 |
| `deriveProtocol` | Function | `securacyfrontend/services/dfd/jsonToIR.ts` | 370 |
| `deriveAuthType` | Function | `securacyfrontend/services/dfd/jsonToIR.ts` | 395 |
| `parseThreatModelingData` | Function | `securacyfrontend/services/dfd/jsonToIR.ts` | 666 |
| `generateId` | Function | `securacyfrontend/services/dfd/jsonToIR.ts` | 724 |
| `parseLLMNestedBoundaries` | Function | `securacyfrontend/services/dfd/jsonToIR.ts` | 731 |
| `layoutDFDThreatModel` | Function | `securacyfrontend/services/dfd/layoutDFDThreatModel.ts` | 38 |
| `computeBoundingBox` | Function | `securacyfrontend/services/dfd/layoutDFDThreatModel.ts` | 93 |
| `addBoundary` | Function | `securacyfrontend/services/dfd/layoutDFDThreatModel.ts` | 112 |
| `parseDrawioXmlToIR` | Function | `securacyfrontend/services/dfd/xmlToIRParser.ts` | 11 |
| `layoutDFD` | Function | `securacyfrontend/services/dfd/dfdLayoutEngine.ts` | 118 |
| `irToDataFlows` | Function | `securacyfrontend/services/dfd/irToDataFlows.ts` | 34 |
| `pushHistory` | Function | `securacyfrontend/components/dfd/DFDEditor.tsx` | 224 |
| `scheduleShowUI` | Function | `securacyfrontend/components/dfd/DFDEditor.tsx` | 814 |
| `onNodeDragStop` | Function | `securacyfrontend/components/dfd/DFDEditor.tsx` | 837 |
| `onKeyDown` | Function | `securacyfrontend/components/dfd/DFDEditor.tsx` | 1021 |
| Flow | Type | Steps |
|------|------|-------|
| `PrivacyBot → FindNodeIdByName` | cross_community | 6 |
| `AppsecBot → FindNodeIdByName` | cross_community | 6 |
| `PrivacyBot → NormalizeNodeType` | cross_community | 5 |
| `PrivacyBot → IsKnownIntegration` | cross_community | 5 |
| `PrivacyBot → NameToId` | cross_community | 5 |
| `AppsecBot → NormalizeNodeType` | cross_community | 5 |
| `AppsecBot → IsKnownIntegration` | cross_community | 5 |
| `AppsecBot → NameToId` | cross_community | 5 |
| `HandleSaveAnalysis → FindNodeIdByName` | cross_community | 5 |
| `HandleSaveAnalysis → FindNodeIdByName` | cross_community | 5 |

## Cluster: E2e
| Symbol | Type | File | Line |
|--------|------|------|------|
| `ecommerce_dfd_b64` | Function | `securacymcp/tests/e2e/conftest.py` | 340 |
| `level1_dfd_b64` | Function | `securacymcp/tests/e2e/conftest.py` | 349 |
| `_minimal_png_b64` | Function | `securacymcp/tests/e2e/conftest.py` | 357 |

## Cluster: Hooks
| Symbol | Type | File | Line |
|--------|------|------|------|
| `getSecurityControlsOptions` | Function | `securacyfrontend/hooks/use-questionnaire.ts` | 39 |
| `startQuestion` | Function | `securacyfrontend/hooks/use-questionnaire.ts` | 96 |
| `getProgress` | Function | `securacyfrontend/hooks/use-questionnaire.ts` | 306 |
| `getSummary` | Function | `securacyfrontend/hooks/use-questionnaire.ts` | 337 |
| `getQuestionnaireProgress` | Function | `securacyfrontend/lib/questions.ts` | 510 |
| `getQuestionnaireSummary` | Function | `securacyfrontend/lib/questions.ts` | 586 |
| `apiCallGet` | Function | `securacyfrontend/lib/api_call_config.ts` | 158 |
| `respondPrivacyQuestion` | Function | `securacyfrontend/services/privacyquestions.ts` | 88 |
| `getPrivacyQuestionnaireProgress` | Function | `securacyfrontend/services/privacyquestions.ts` | 217 |
| `getPrivacyQuestionnaireSummary` | Function | `securacyfrontend/services/privacyquestions.ts` | 293 |
| `LoadedThreatProvider` | Function | `securacyfrontend/context/LoadedThreatContext.tsx` | 67 |
| `handleNextPrivacyQuestion` | Function | `securacyfrontend/app/home/(bots)/privacy/page.tsx` | 857 |
| `getDomainSpecificOptions` | Function | `securacyfrontend/hooks/use-questionnaire.ts` | 53 |
| `toTitleCase` | Function | `securacyfrontend/hooks/use-questionnaire.ts` | 69 |
| `getDomainFromResponse` | Function | `securacyfrontend/hooks/use-questionnaire.ts` | 76 |
| `respondQuestion` | Function | `securacyfrontend/hooks/use-questionnaire.ts` | 117 |
| Flow | Type | Steps |
|------|------|-------|
| `PrivacyBot → DecodeJwt` | cross_community | 8 |
| `AppsecBot → DecodeJwt` | cross_community | 8 |
| `OnboardingPage → DecodeJwt` | cross_community | 7 |
| `HandleNextQuestion → DecodeJwt` | cross_community | 7 |
| `HandleNextQuestion → DecodeJwt` | cross_community | 7 |
| `HandleNextPrivacyQuestion → DecodeJwt` | cross_community | 6 |
| `SubscriptionPanel → DecodeJwt` | cross_community | 6 |
| `AppSidebar → DecodeJwt` | cross_community | 6 |
| `UsageSection → DecodeJwt` | cross_community | 6 |
| `RespondQuestion → DecodeJwt` | cross_community | 6 |
| Area | Connections |
|------|-------------|
| _components | 2 calls |

## Cluster: Onboarding
| Symbol | Type | File | Line |
|--------|------|------|------|
| `fetchUser` | Function | `securacyfrontend/services/userService.ts` | 61 |
| `OnboardingPage` | Function | `securacyfrontend/app/onboarding/page.tsx` | 114 |
| `loadProfile` | Function | `securacyfrontend/app/onboarding/page.tsx` | 145 |
| `hasChanges` | Function | `securacyfrontend/app/onboarding/page.tsx` | 44 |
| Flow | Type | Steps |
|------|------|-------|
| `OnboardingPage → DecodeJwt` | cross_community | 7 |
| `Load → DecodeJwt` | cross_community | 6 |
| Area | Connections |
|------|-------------|
| Hooks | 1 calls |
| Context | 1 calls |

## Cluster: Privacy
| Symbol | Type | File | Line |
|--------|------|------|------|
| `add_exchange` | Function | `backend/buddlyai/privacy/interactive_privacy_questionnaire_langchain.py` | 45 |
| `mark_topic_complete` | Function | `backend/buddlyai/privacy/interactive_privacy_questionnaire_langchain.py` | 50 |
| `move_to_next_topic` | Function | `backend/buddlyai/privacy/interactive_privacy_questionnaire_langchain.py` | 55 |
| `get_remaining_topics` | Function | `backend/buddlyai/privacy/interactive_privacy_questionnaire_langchain.py` | 66 |
| `process_response` | Function | `backend/buddlyai/privacy/interactive_privacy_questionnaire_langchain.py` | 742 |
| `get_system_context` | Function | `backend/buddlyai/privacy/interactive_privacy_questionnaire_langchain.py` | 93 |
| `get_progress_summary` | Function | `backend/buddlyai/privacy/interactive_privacy_questionnaire_langchain.py` | 101 |
| `add_context` | Function | `backend/buddlyai/privacy/interactive_privacy_questionnaire_langchain.py` | 168 |
| `start_interview` | Function | `backend/buddlyai/privacy/interactive_privacy_questionnaire_langchain.py` | 701 |
| `generate_summary` | Function | `backend/buddlyai/privacy/interactive_privacy_questionnaire_langchain.py` | 985 |
| `save_session` | Function | `backend/buddlyai/privacy/interactive_privacy_questionnaire_langchain.py` | 1078 |
| `get_memory_summary` | Function | `backend/buddlyai/privacy/interactive_privacy_questionnaire_langchain.py` | 1106 |
| `run_interactive_session` | Function | `backend/buddlyai/privacy/interactive_privacy_questionnaire_langchain.py` | 1115 |
| `start_privacy_questionnaire` | Function | `backend/buddlyai/Routes/PrivacyController.py` | 64 |
| `get_privacy_questionnaire_progress` | Function | `backend/buddlyai/Routes/PrivacyController.py` | 180 |
| `get_privacy_questionnaire_summary` | Function | `backend/buddlyai/Routes/PrivacyController.py` | 212 |
| `respondQuestion` | Function | `securacyfrontend/lib/questions.ts` | 348 |
| `mapAnswersToAnalysisData` | Function | `securacyfrontend/app/home/(bots)/privacy/page.tsx` | 510 |
| `getAnswerForTopic` | Function | `securacyfrontend/app/home/(bots)/privacy/page.tsx` | 531 |
| `handleNextQuestion` | Function | `securacyfrontend/app/home/(bots)/privacy/page.tsx` | 588 |
| Flow | Type | Steps |
|------|------|-------|
| `PrivacyBot → DecodeJwt` | cross_community | 8 |
| `AppsecBot → DecodeJwt` | cross_community | 8 |
| `HandleNextQuestion → DecodeJwt` | cross_community | 7 |
| `HandleNextQuestion → DecodeJwt` | cross_community | 7 |
| `PrivacyBot → FindNodeIdByName` | cross_community | 6 |
| `PrivacyBot → _syncUserWithBackend` | cross_community | 6 |
| `PrivacyBot → NormalizeNodeType` | cross_community | 5 |
| `PrivacyBot → IsKnownIntegration` | cross_community | 5 |
| `PrivacyBot → NameToId` | cross_community | 5 |
| `PrivacyBot → StopSessionMonitoring` | cross_community | 5 |
| Area | Connections |
|------|-------------|
| Hooks | 2 calls |
| Services | 1 calls |
| Appsec | 1 calls |
| Dfd | 1 calls |

## Cluster: Routes
| Symbol | Type | File | Line |
|--------|------|------|------|
| `parseROIJustification` | Function | `backend/buddlyai/appsec/downloadresults.py` | 703 |
| `downloadbusinessImpactasPDF` | Function | `backend/buddlyai/appsec/downloadresults.py` | 792 |
| `load_prompt_template` | Function | `backend/buddlyai/Routes/AppSecController.py` | 45 |
| `getTopThreeThreatsWithHighestCVSSScore` | Function | `backend/buddlyai/Routes/AppSecController.py` | 55 |
| `getMitigationsForTopThreats` | Function | `backend/buddlyai/Routes/AppSecController.py` | 93 |
| `getBusinessImpactFromThreatAnalysis` | Function | `backend/buddlyai/Routes/AppSecController.py` | 440 |
| `run_threat_analysis` | Function | `backend/buddlyai/Routes/AppSecController.py` | 51 |
| `getSecuracyThreats` | Function | `backend/buddlyai/Routes/AppSecController.py` | 348 |
| `getSecuracyThreats1` | Function | `backend/buddlyai/Routes/AppSecController.py` | 386 |
| `load_threats` | Function | `backend/buddlyai/Routes/ThreatsController.py` | 180 |
| `get_threat_runs_by_user` | Function | `backend/buddlyai/DB/DBservice.py` | 373 |
| `_enrich_threats_with_cvss` | Function | `backend/buddlyai/Routes/AppSecController.py` | 75 |
| Area | Connections |
|------|-------------|
| Appsec | 2 calls |

## Cluster: Securacymcp
| Symbol | Type | File | Line |
|--------|------|------|------|
| `record_usage` | Function | `securacymcp/metering.py` | 62 |
| `get_tenant_request_count` | Function | `securacymcp/metering.py` | 176 |
| `get_db_conn` | Function | `securacymcp/db.py` | 42 |
| `release_db_conn` | Function | `securacymcp/db.py` | 49 |
| `generate_key` | Function | `securacymcp/api_keys.py` | 60 |
| `create_api_key` | Function | `securacymcp/api_keys.py` | 64 |
| `revoke_api_key` | Function | `securacymcp/api_keys.py` | 139 |
| `test_count_within_window` | Function | `securacymcp/tests/test_metering.py` | 67 |
| `test_count_excludes_old` | Function | `securacymcp/tests/test_metering.py` | 73 |
| `test_init_pool_raises_without_database_url` | Function | `securacymcp/tests/test_metering.py` | 169 |
| `test_get_db_conn_triggers_lazy_init` | Function | `securacymcp/tests/test_metering.py` | 176 |
| `test_prefix` | Function | `securacymcp/tests/test_api_keys.py` | 11 |
| `test_uniqueness` | Function | `securacymcp/tests/test_api_keys.py` | 16 |
| `test_revoke_already_revoked` | Function | `securacymcp/tests/test_api_keys.py` | 87 |
| `commit` | Function | `securacymcp/tests/conftest.py` | 51 |
| `rollback` | Function | `securacymcp/tests/conftest.py` | 54 |
| `copy_threat` | Function | `backend/buddlyai/Routes/ThreatsController.py` | 199 |
| `update_threat_json` | Function | `backend/buddlyai/Routes/ThreatsController.py` | 255 |
| `copy_threat_run` | Function | `backend/buddlyai/DB/DBservice.py` | 164 |
| `updateThreatJson` | Function | `backend/buddlyai/DB/DBservice.py` | 268 |
| Flow | Type | Steps |
|------|------|-------|
| `Require_jwt → _init_pool` | cross_community | 5 |
| `Get_structured_input_from_diagram_bytes → _refresh` | cross_community | 5 |
| `Get_structured_input_from_tf_logic → _refresh` | cross_community | 5 |
| `Get_security_threats_logic → _refresh` | cross_community | 5 |
| `Get_usage → _init_pool` | cross_community | 5 |
| `Create_api_key_endpoint → _init_pool` | cross_community | 5 |
| `Export_report_logic → _refresh` | intra_community | 5 |
| `List_api_keys_endpoint → _init_pool` | cross_community | 5 |
| `Revoke_api_key_endpoint → _init_pool` | cross_community | 5 |
| `Get_structured_input_logic → _refresh` | cross_community | 5 |
| Area | Connections |
|------|-------------|
| Tests | 8 calls |
| DB | 1 calls |
| Services | 1 calls |

## Cluster: Services
| Symbol | Type | File | Line |
|--------|------|------|------|
| `generate_key` | Function | `backend/buddlyai/Services/mcp_keys.py` | 63 |
| `create_api_key` | Function | `backend/buddlyai/Services/mcp_keys.py` | 67 |
| `list_api_keys` | Function | `backend/buddlyai/Services/mcp_keys.py` | 112 |
| `revoke_api_key` | Function | `backend/buddlyai/Services/mcp_keys.py` | 139 |
| `get_tenant_usage` | Function | `backend/buddlyai/Services/mcp_keys.py` | 158 |
| `create_api_key` | Function | `backend/buddlyai/Routes/MCPController.py` | 90 |
| `list_api_keys` | Function | `backend/buddlyai/Routes/MCPController.py` | 120 |
| `revoke_api_key` | Function | `backend/buddlyai/Routes/MCPController.py` | 126 |
| `get_usage` | Function | `backend/buddlyai/Routes/MCPController.py` | 135 |
| `generate_privacythreat_json_reasoning_claude_bedrock` | Function | `backend/buddlyai/privacy/privacy_threat_analysis_prompt.py` | 249 |
| `estimate_cost` | Function | `backend/buddlyai/Services/llm_logger.py` | 60 |
| `to_dict` | Function | `backend/buddlyai/Services/llm_logger.py` | 190 |
| `log_entry` | Function | `backend/buddlyai/Services/llm_logger.py` | 230 |
| `wrapper` | Function | `backend/buddlyai/Services/llm_logger.py` | 293 |
| `wrap_bedrock_invoke` | Function | `backend/buddlyai/Services/llm_logger.py` | 520 |
| `on_llm_end` | Function | `backend/buddlyai/Services/llm_logger.py` | 658 |
| `on_llm_error` | Function | `backend/buddlyai/Services/llm_logger.py` | 700 |
| `run_privacythreat_analysis_with_rag` | Function | `backend/buddlyai/Routes/PrivacyController.py` | 428 |
| `initiatePayment` | Function | `securacyfrontend/services/paymentService.ts` | 79 |
| `initiateExtension` | Function | `securacyfrontend/services/paymentService.ts` | 186 |
| Flow | Type | Steps |
|------|------|-------|
| `HandleGoogleLogin → IsAllowedDomain` | cross_community | 7 |
| `HandleGoogleLogin → SyncUserToCookie` | cross_community | 7 |
| `PrivacyBot → _syncUserWithBackend` | cross_community | 6 |
| `AuthProvider → IsAllowedDomain` | cross_community | 6 |
| `AuthProvider → SyncUserToCookie` | cross_community | 6 |
| `AuthProvider → _syncUserWithBackend` | cross_community | 6 |
| `Constructor → StopSessionMonitoring` | cross_community | 6 |
| `Constructor → ClearUserCookie` | cross_community | 6 |
| `Constructor → _syncUserWithBackend` | cross_community | 6 |
| `PrivacyBot → StopSessionMonitoring` | cross_community | 5 |
| Area | Connections |
|------|-------------|
| _components | 6 calls |
| Securacymcp | 3 calls |

## Cluster: Tests
| Symbol | Type | File | Line |
|--------|------|------|------|
| `report` | Function | `securacymcp/tests/e2e_pipeline_test.py` | 69 |
| `test_health_checks` | Function | `securacymcp/tests/e2e_pipeline_test.py` | 84 |
| `test_text_analysis` | Function | `securacymcp/tests/e2e_pipeline_test.py` | 110 |
| `test_threat_search` | Function | `securacymcp/tests/e2e_pipeline_test.py` | 132 |
| `test_export_report` | Function | `securacymcp/tests/e2e_pipeline_test.py` | 154 |
| `test_risk_calculation` | Function | `securacymcp/tests/e2e_pipeline_test.py` | 188 |
| `test_tools_listing` | Function | `securacymcp/tests/e2e_pipeline_test.py` | 210 |
| `test_backend_regression` | Function | `securacymcp/tests/e2e_pipeline_test.py` | 232 |
| `main` | Function | `securacymcp/tests/e2e_pipeline_test.py` | 252 |
| `cmd_create` | Function | `securacymcp/manage_keys.py` | 48 |
| `test_outputs_key` | Function | `securacymcp/tests/test_manage_keys.py` | 12 |
| `test_outputs_claude_config` | Function | `securacymcp/tests/test_manage_keys.py` | 23 |
| `test_outputs_continue_config` | Function | `securacymcp/tests/test_manage_keys.py` | 35 |
| `test_outputs_python_sdk` | Function | `securacymcp/tests/test_manage_keys.py` | 46 |
| `test_outputs_local_stdio` | Function | `securacymcp/tests/test_manage_keys.py` | 57 |
| `test_create_with_expiry` | Function | `securacymcp/tests/test_manage_keys.py` | 68 |
| `test_rejects_garbage_tenant` | Function | `securacymcp/tests/test_manage_keys.py` | 147 |
| `test_rejects_empty_tenant` | Function | `securacymcp/tests/test_manage_keys.py` | 158 |
| `test_accepts_valid_tenant` | Function | `securacymcp/tests/test_manage_keys.py` | 169 |
| `get_jwks` | Function | `securacymcp/auth.py` | 66 |
| Flow | Type | Steps |
|------|------|-------|
| `Require_jwt → _init_pool` | cross_community | 5 |
| `Get_usage → _init_pool` | cross_community | 5 |
| `Create_api_key_endpoint → _init_pool` | cross_community | 5 |
| `List_api_keys_endpoint → _init_pool` | cross_community | 5 |
| `Require_jwt → Commit` | cross_community | 4 |
| `Require_jwt → Rollback` | cross_community | 4 |
| `Require_jwt → Release_db_conn` | cross_community | 4 |
| `Require_jwt → _hash_key` | cross_community | 4 |
| `Require_jwt → _prune` | cross_community | 4 |
| `Get_usage → Commit` | cross_community | 4 |
| Area | Connections |
|------|-------------|
| Securacymcp | 19 calls |

## Cluster: Threats-modules
| Symbol | Type | File | Line |
|--------|------|------|------|
| `load_and_process_data` | Function | `backend/buddlyai/Services/threats_modules/threat_rag.py` | 39 |
| `create_embeddings` | Function | `backend/buddlyai/Services/threats_modules/threat_rag.py` | 84 |
| `retrieve_relevant_threats` | Function | `backend/buddlyai/Services/threats_modules/threat_rag.py` | 117 |
| `get_db_path` | Function | `backend/buddlyai/Services/threats_modules/threat_db.py` | 29 |
| `get_embeddings_path` | Function | `backend/buddlyai/Services/threats_modules/threat_db.py` | 40 |
| `get_all_threats` | Function | `backend/buddlyai/Services/threats_modules/threat_db.py` | 297 |
| `export_to_dataframe` | Function | `backend/buddlyai/Services/threats_modules/threat_db.py` | 415 |
| `create_privacythreat_analysis_prompt` | Function | `backend/buddlyai/privacy/privacy_threat_analysis_prompt.py` | 13 |
| `generate_privacythreat_json_with_rag` | Function | `backend/buddlyai/privacy/privacy_threat_analysis_prompt.py` | 27 |
| `create_threat_analysis_prompt` | Function | `backend/buddlyai/appsec/threat_analysis_prompt.py` | 13 |
| `generate_threat_json_with_rag` | Function | `backend/buddlyai/appsec/threat_analysis_prompt.py` | 28 |
| `analyze_threat_scenario` | Function | `backend/buddlyai/Services/threats_modules/threat_rag.py` | 147 |
| `stream_csv_from_s3` | Function | `backend/buddlyai/Services/threats_modules/s3_threatdb.py` | 72 |
| `get_csv_dataframe` | Function | `backend/buddlyai/Services/threats_modules/s3_threatdb.py` | 98 |
| `iterate_csv_files` | Function | `backend/buddlyai/Services/threats_modules/s3_threatdb.py` | 111 |
| `list_threatdb_files` | Function | `backend/buddlyai/Services/threats_modules/s3_threatdb.py` | 129 |
| `download_threatdb_files` | Function | `backend/buddlyai/Services/threats_modules/s3_threatdb.py` | 153 |
| `upload_local_threatdb` | Function | `backend/buddlyai/Services/threats_modules/s3_threatdb.py` | 246 |
| `get_s3_threatdb_manager` | Function | `backend/buddlyai/Services/threats_modules/s3_threatdb.py` | 307 |
| `upload_threatdb_to_s3` | Function | `backend/buddlyai/Services/threats_modules/s3_threatdb.py` | 318 |
| Area | Connections |
|------|-------------|
| Securacymcp | 1 calls |

## Cluster: Ui
| Symbol | Type | File | Line |
|--------|------|------|------|
| `useIsMobile` | Function | `securacyfrontend/hooks/use-mobile.ts` | 4 |
| `cn` | Function | `securacyfrontend/lib/utils.ts` | 3 |
| `Navbar` | Function | `securacyfrontend/app/home/_components/Navbar.tsx` | 17 |
| `SettingsNav` | Function | `securacyfrontend/app/home/settings/_components/settings-nav.tsx` | 16 |
| `ExpandableChatCard` | Function | `securacyfrontend/app/home/(bots)/_components/ExpandableChatCard.tsx` | 25 |
| `EditableAnalysisCard` | Function | `securacyfrontend/app/home/(bots)/_components/EditableAnalysisCard.tsx` | 104 |
| `handleChange` | Function | `securacyfrontend/app/home/(bots)/_components/EditableAnalysisCard.tsx` | 123 |
| `ChatNav` | Function | `securacyfrontend/app/home/(bots)/_components/ChatNav.tsx` | 8 |
| `TooltipContent` | Function | `securacyfrontend/components/ui/tooltip.tsx` | 36 |
| `Textarea` | Function | `securacyfrontend/components/ui/textarea.tsx` | 4 |
| `Tabs` | Function | `securacyfrontend/components/ui/tabs.tsx` | 7 |
| `TabsList` | Function | `securacyfrontend/components/ui/tabs.tsx` | 20 |
| `TabsTrigger` | Function | `securacyfrontend/components/ui/tabs.tsx` | 36 |
| `TabsContent` | Function | `securacyfrontend/components/ui/tabs.tsx` | 52 |
| `Table` | Function | `securacyfrontend/components/ui/table.tsx` | 6 |
| `TableHeader` | Function | `securacyfrontend/components/ui/table.tsx` | 21 |
| `TableBody` | Function | `securacyfrontend/components/ui/table.tsx` | 31 |
| `TableFooter` | Function | `securacyfrontend/components/ui/table.tsx` | 41 |
| `TableRow` | Function | `securacyfrontend/components/ui/table.tsx` | 54 |
| `TableHead` | Function | `securacyfrontend/components/ui/table.tsx` | 67 |

