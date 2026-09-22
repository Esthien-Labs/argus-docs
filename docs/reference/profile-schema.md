# Profile Schema

Full JSON schema for Argus profiles.

## Root object

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `schema_version` | string | Yes | Must be `"1.0"` |
| `profile_id` | string | Yes | Unique identifier |
| `applicable_standards` | array | Yes | List of standard references |
| `producer_config` | object | Yes | Command source configuration |
| `receiver_config` | object | Yes | Actuator configuration |
| `command_limits` | object | Yes | Numeric bounds |
| `fault_corpus` | object | Yes | Fault cases to test |

## producer_config

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | string | Yes | Producer identifier |
| `interface_type` | string | Yes | Interface type |
| `command_rate_hz` | number | Yes | Command frequency |
| `sequence_policy` | object | Yes | Sequence handling rules |

## receiver_config

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | string | Yes | Receiver identifier |
| `controller_type` | string | Yes | Controller type |
| `max_latency_deadline_ms` | number | Yes | Maximum allowed latency |
| `safety_function_class` | string | Yes | SIL/ASIL class |

## sequence_policy

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `sequence_rollover` | string | Yes | `monotonic_64` or `wrap_16` |
| `stale_data_age_ms` | number | Yes | Staleness threshold |
| `reset_epoch` | string | Yes | When sequence resets |
| `queue_overflow_behavior` | string | Yes | `drop_oldest` or `reject` |
| `invalid_numeric_behavior` | string | Yes | `reject` or `clamp` |

## fault_corpus

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `faults` | array | Yes | List of fault cases |

### fault object

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `fault_id` | string | Yes | Unique fault identifier |
| `fault_kind` | string | Yes | Fault category |
| `description` | string | No | Human-readable description |
| `expected_state` | string | Yes | Expected safety response |
