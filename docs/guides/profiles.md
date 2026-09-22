# Profiles

A profile defines the controller, receiver, command limits, and fault corpus for an Argus evaluation.

## Reference profiles

Three profiles ship with the SDK:

| Profile | Interface | Standards | Fault cases |
|---------|-----------|-----------|-------------|
| `robot_diff_drive_ros2_v0` | ROS 2 differential drive | ISO 3691-4:2023, IEC 61508:2010 | 9 |
| `can_automotive_v0` | CAN-bus torque controller | ISO 26262:2018 | 9 |
| `spi_cobot_v0` | SPI cobot actuator | ISO 10218-1:2011, IEC 62061:2021 | 9 |

## Profile location

Reference profiles are in:
```
config/profiles/regression/
```

## Profile structure

Every profile contains:

```json
{
  "schema_version": "1.0",
  "profile_id": "robot_diff_drive_ros2_v0",
  "applicable_standards": ["ISO 3691-4:2023"],
  "producer_config": { ... },
  "receiver_config": { ... },
  "command_limits": { ... },
  "fault_corpus": { ... }
}
```

### Producer config

Describes the command source:

```json
{
  "name": "nav2_navigation_stack",
  "interface_type": "ros2_diff_drive",
  "command_rate_hz": 10.0,
  "sequence_policy": {
    "sequence_rollover": "monotonic_64",
    "stale_data_age_ms": 500.0
  }
}
```

### Receiver config

Describes the actuator:

```json
{
  "name": "ros2_control_diff_drive_controller",
  "controller_type": "motion_controller",
  "max_latency_deadline_ms": 100.0,
  "safety_function_class": "SIL2"
}
```

### Command limits

Numeric bounds for validation:

```json
{
  "max_linear_velocity_mps": 1.5,
  "max_angular_velocity_rads": 1.0
}
```

### Fault corpus

The fault cases to test:

```json
{
  "faults": [
    {
      "fault_id": "fc_001_stale",
      "fault_kind": "stale_command",
      "expected_state": "safe_halt"
    }
  ]
}
```

## Fault kinds

| Kind | Description |
|------|-------------|
| `stale_command` | Command gap exceeds staleness threshold |
| `missing_burst` | Expected command burst missing |
| `duplicate_sequence` | Same sequence number repeated |
| `out_of_order` | Commands arrive out of sequence |
| `numeric_out_of_range` | Value exceeds command limits |
| `corrupted_frame` | Invalid frame structure |
| `rearm_behavior` | Recovery from fault state |

## Next steps

- [Custom Profiles](custom-profiles.md) - Build your own profile
- [Trace Formats](trace-formats.md) - Supported input formats
