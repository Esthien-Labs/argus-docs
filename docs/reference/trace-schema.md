# Trace Schema

JSON schema for Atlas native trace format.

## Root object

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `manifest` | object | Yes | Trace metadata |
| `commands` | array | Yes | Command messages |

## manifest

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `schema_version` | string | Yes | Must be `"1.0"` |
| `session_id` | string | Yes | Unique session identifier |
| `producer_id` | string | Yes | Command source identifier |
| `receiver_id` | string | Yes | Actuator identifier |
| `trace_format` | string | No | Format hint |
| `sequence_policy` | object | No | Sequence handling rules |

## command

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `sequence_number` | integer | Yes | Monotonic sequence |
| `timestamp_us` | integer | Yes | Microsecond timestamp |
| `clock_domain_id` | string | No | Clock source identifier |
| `event_type` | string | Yes | `command`, `status`, `fault` |
| `payload` | object | Yes | Command data |

## payload

Payload fields depend on interface type. For differential drive:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `velocity_lin_mps` | number | Yes | Linear velocity (m/s) |
| `velocity_ang_rads` | number | Yes | Angular velocity (rad/s) |
| `controller_state` | string | No | `nominal`, `degraded`, `fault` |
| `fault_flags` | integer | No | Bitfield of active faults |
| `rearm_requested` | boolean | No | Recovery request |

## Example

```json
{
  "manifest": {
    "schema_version": "1.0",
    "session_id": "abc-123",
    "producer_id": "nav_stack",
    "receiver_id": "drive_controller"
  },
  "commands": [
    {
      "sequence_number": 0,
      "timestamp_us": 1000000,
      "event_type": "command",
      "payload": {
        "velocity_lin_mps": 0.5,
        "velocity_ang_rads": 0.1
      }
    }
  ]
}
```
