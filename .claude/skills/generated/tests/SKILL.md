---
name: tests
description: "Skill for the Tests area of Securacy. 114 symbols across 19 files."
---

# Tests

114 symbols | 19 files | Cohesion: 84%

## When to Use

- Working with code in `securacymcp/`
- Understanding how report, test_health_checks, test_text_analysis work
- Modifying tests-related functionality

## Key Files

| File | Symbols |
|------|---------|
| `securacymcp/tests/test_manage_keys.py` | test_outputs_key, test_outputs_claude_config, test_outputs_continue_config, test_outputs_python_sdk, test_outputs_local_stdio (+15) |
| `securacymcp/tests/e2e_pipeline_test.py` | _load_env_var, _load_api_key, _get_jwt_token, _auth_headers, report (+8) |
| `securacymcp/tests/test_image_resource.py` | test_loopback_blocked, test_private_ip_blocked, test_ipv6_loopback_blocked, test_http_rejected, test_link_local_blocked (+6) |
| `securacymcp/tests/test_api_keys.py` | test_create_and_verify, test_custom_scopes, test_verify_invalid_key, test_verify_non_prefix, test_expired_key_rejected (+5) |
| `securacymcp/tests/test_error_handling.py` | _make_request, test_formats_first_error, test_multiple_errors_include_detail, test_no_stack_trace_in_response, test_includes_request_id (+4) |
| `securacymcp/tests/test_live_mcp_stdio.py` | banner, save, passed, failed, skipped (+3) |
| `securacymcp/tests/test_metering.py` | test_insert_and_retrieve, test_multiple_tools_aggregation, test_tenant_isolation, test_days_filter, test_days_clamping (+2) |
| `securacymcp/manage_keys.py` | _mcp_public_url, cmd_create, cmd_revoke, main, cmd_list (+1) |
| `securacymcp/tests/test_auth_jwt.py` | test_jwks_force_refresh, test_verify_valid_access_token, test_missing_kid_raises_401, test_kid_not_in_cache_triggers_refresh, test_expired_token_raises_401 (+1) |
| `securacymcp/tools.py` | _validate_url_host, _load_compliance_mappings, map_compliance_logic, _read_image_stream, _fetch_image_secure |

## Entry Points

Start here when exploring this area:

- **`report`** (Function) — `securacymcp/tests/e2e_pipeline_test.py:69`
- **`test_health_checks`** (Function) — `securacymcp/tests/e2e_pipeline_test.py:84`
- **`test_text_analysis`** (Function) — `securacymcp/tests/e2e_pipeline_test.py:110`
- **`test_threat_search`** (Function) — `securacymcp/tests/e2e_pipeline_test.py:132`
- **`test_export_report`** (Function) — `securacymcp/tests/e2e_pipeline_test.py:154`

## Key Symbols

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

## Execution Flows

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

## Connected Areas

| Area | Connections |
|------|-------------|
| Securacymcp | 19 calls |

## How to Explore

1. `gitnexus_context({name: "report"})` — see callers and callees
2. `gitnexus_query({query: "tests"})` — find related execution flows
3. Read key files listed above for implementation details
