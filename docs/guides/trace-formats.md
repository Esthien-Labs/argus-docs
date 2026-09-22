# Trace Formats

Argus accepts command traces in three formats.

## Supported formats

| Format | Extension | Dependency |
|--------|-----------|------------|
| Atlas native JSON | `.atlas-trace.json`, `.json` | None (built-in) |
| ROS 2 SQLite bag | `.db3` | None (stdlib sqlite3) |
| MCAP | `.mcap` | `pip install mcap` |

## Atlas native JSON

The simplest format - a JSON file with manifest and commands:

```json
{
  "manifest": {
    "schema_version": "1.0",
    "session_id": "uuid",
    "producer_id": "your_controller",
    "receiver_id": "your_actuator"
  },
  "commands": [
    {
      "sequence_number": 0,
      "timestamp_us": 1000000,
      "payload": {
        "velocity_lin_mps": 0.5,
        "velocity_ang_rads": 0.1
      }
    }
  ]
}
```

Generate a sample:
```bash
argus regression-eval --sample --out out/sample
cat out/sample/sample_trace.atlas-trace.json
```

## ROS 2 SQLite bag

Standard ROS 2 bag format (`.db3`). Must publish:

- `/atlas/command_trace_manifest` - Session metadata
- `/atlas/robot_commands` - Command messages

```bash
argus regression-eval --trace recording.db3 --profile your_profile.json
```

## MCAP

[MCAP](https://mcap.dev/) is a modern robotics log format. Install support:

```bash
pip install mcap
```

Then:
```bash
argus regression-eval --trace recording.mcap --profile your_profile.json
```

## Required topics

Both ROS 2 and MCAP traces must include:

### Manifest topic

Topic: `/atlas/command_trace_manifest`

```json
{
  "schema_version": "1.0",
  "session_id": "uuid",
  "producer_id": "your_controller",
  "receiver_id": "your_actuator",
  "trace_format": "atlas-trace-json",
  "sequence_policy": {
    "sequence_rollover": "monotonic_64",
    "stale_data_age_ms": 500.0
  }
}
```

### Commands topic

Topic: `/atlas/robot_commands`

```json
{
  "sequence_number": 0,
  "timestamp_us": 1000000,
  "clock_domain_id": "controller_monotonic",
  "event_type": "command",
  "payload": {
    "velocity_lin_mps": 0.5,
    "velocity_ang_rads": 0.1,
    "controller_state": "nominal",
    "fault_flags": 0,
    "rearm_requested": false
  }
}
```

## Converting existing traces

If your trace uses different topic names, convert to Atlas native JSON:

```python
import json

# Load your trace
commands = load_your_trace("recording.bag")

# Convert to Atlas format
atlas_trace = {
    "manifest": {
        "schema_version": "1.0",
        "session_id": "converted-trace",
        "producer_id": "your_controller",
        "receiver_id": "your_actuator"
    },
    "commands": commands
}

with open("converted.atlas-trace.json", "w") as f:
    json.dump(atlas_trace, f, indent=2)
```

## Next steps

- [Evidence Classes](evidence-classes.md) - Understand report classifications
- [Profiles](profiles.md) - Match trace to profile
