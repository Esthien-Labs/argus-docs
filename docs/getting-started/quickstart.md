# Quickstart

Run your first Argus evaluation in 3 commands.

## 1. Check your profile

Validate a reference profile and see its configuration:

```bash
argus profile-check --profile config/profiles/regression/robot_diff_drive_ros2_v0.json
```

Output:
```
argus profile-check: PASS

  Profile ID      : robot_diff_drive_ros2_v0
  Schema version  : 1.0
  Standards       : ISO 3691-4:2023, IEC 61508:2010

  Producer        : nav2_navigation_stack  (ros2_diff_drive  10.0 Hz)
  Receiver        : ros2_control_diff_drive_controller  (motion_controller)
  Safety class    : SIL2

  Fault cases     : 9
```

## 2. Run evaluation with sample trace

Generate a synthetic trace, run 9 fault cases, and produce evidence:

```bash
argus regression-eval --sample
```

This creates:
```
out/regression-eval/
  regression_report.json    # Machine-readable results
  regression_report.md      # Human-readable summary
  regression_report.html    # Shareable report
  evidence_manifest.json    # Source hashes + evidence class
```

## 3. View results

```bash
cat out/regression-eval/regression_report.md
```

Or open `regression_report.html` in a browser for a formatted view.

## What just happened?

1. Argus generated a synthetic command trace matching the profile
2. Injected 9 fault conditions (stale commands, missing bursts, etc.)
3. Verified the safety envelope intercepted each fault
4. Generated a signed evidence package with ISO citations

## Next: Use a real trace

```bash
# ROS 2 bag
argus regression-eval --trace /path/to/recording.db3 --profile your_profile.json

# MCAP file  
argus regression-eval --trace /path/to/recording.mcap --profile your_profile.json
```

See [Trace Formats](../guides/trace-formats.md) for supported formats.
