# Custom Profiles

Build a profile for your specific controller and actuator.

## Template

```json
{
  "schema_version": "1.0",
  "profile_id": "my_robot_v0",
  "applicable_standards": ["ISO 3691-4:2023"],
  "producer_config": {
    "name": "my_navigation_stack",
    "interface_type": "ros2_diff_drive",
    "command_rate_hz": 10.0,
    "sequence_policy": {
      "sequence_rollover": "monotonic_64",
      "stale_data_age_ms": 500.0,
      "reset_epoch": "controller_start",
      "queue_overflow_behavior": "drop_oldest",
      "invalid_numeric_behavior": "reject"
    }
  },
  "receiver_config": {
    "name": "my_motion_controller",
    "controller_type": "motion_controller",
    "max_latency_deadline_ms": 100.0,
    "safety_function_class": "SIL2"
  },
  "command_limits": {
    "max_linear_velocity_mps": 1.5,
    "max_angular_velocity_rads": 1.0
  },
  "fault_corpus": {
    "faults": [
      {
        "fault_id": "fc_001_stale",
        "fault_kind": "stale_command",
        "description": "Command gap exceeds stale threshold",
        "expected_state": "safe_halt"
      }
    ]
  }
}
```

## Validate

```bash
argus profile-check --profile my_robot_v0.json
```

## Interface types

| Type | Description |
|------|-------------|
| `ros2_diff_drive` | ROS 2 differential drive |
| `ros2_ackermann` | ROS 2 Ackermann steering |
| `can_torque` | CAN-bus torque commands |
| `spi_actuator` | SPI actuator interface |

## Safety function classes

| Class | Standard |
|-------|----------|
| `SIL1` | IEC 61508 |
| `SIL2` | IEC 61508 |
| `SIL3` | IEC 61508 |
| `ASIL_A` | ISO 26262 |
| `ASIL_B` | ISO 26262 |
| `ASIL_C` | ISO 26262 |
| `ASIL_D` | ISO 26262 |

## Fault corpus

Include at minimum:

1. `stale_command` - Staleness detection
2. `missing_burst` - Missing command detection
3. `numeric_out_of_range` - Limit enforcement

See [Profile Schema](../reference/profile-schema.md) for full specification.
