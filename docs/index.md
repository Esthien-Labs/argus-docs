# Argus SDK

**Safety-supervised inference for physical systems.**

The Argus SDK generates standards-mapped evidence packages from controller command traces. Load a real ROS 2 bag, MCAP file, or synthetic trace - run a declared fault corpus - and receive a signed report citing ISO 3691-4, ISO 26262, or IEC 62304 sections by name.

<div class="grid cards" markdown>

- :material-download: **Install in seconds**

    ```bash
    pip install esthien-argus-sdk
    ```

    [Installation Guide](getting-started/installation.md)

- :material-play-circle: **3 commands to your first report**

    Profile check, regression eval, evidence package.

    [Quickstart](getting-started/quickstart.md)

- :material-file-document: **Standards-mapped output**

    ISO 3691-4, ISO 26262, IEC 62304 citations by name.

    [Evidence Classes](guides/evidence-classes.md)

- :material-cog: **Customizable profiles**

    Define your controller, fault corpus, and acceptance criteria.

    [Custom Profiles](guides/custom-profiles.md)

</div>

## What Argus Does

1. **Load a command trace** - ROS 2 bag, MCAP, or native JSON
2. **Run a fault corpus** - 9 fault cases per reference profile
3. **Generate evidence** - Signed report with ISO/IEC citations

Each report explicitly states its evidence class and what it does - and does not - cover.

## Quick Example

```bash
# Check your profile
argus profile-check --profile config/profiles/regression/robot_diff_drive_ros2_v0.json

# Run evaluation with sample trace
argus regression-eval --sample

# View the report
cat out/regression-eval/regression_report.md
```

## Evidence Classes

| Class | Description |
|-------|-------------|
| `digital_source_verification` | Software simulation - no hardware required |
| `measured_partial` | Some measurements from physical hardware |
| `hardware_measured` | Full hardware bring-up with calibrated instruments |

## Reference Profiles

| Profile | Interface | Standards |
|---------|-----------|-----------|
| `robot_diff_drive_ros2_v0` | ROS 2 differential drive | ISO 3691-4:2023 |
| `can_automotive_v0` | CAN-bus torque controller | ISO 26262:2018 |
| `spi_cobot_v0` | SPI cobot actuator | ISO 10218-1:2011 |

## Support

- [GitHub Issues](https://github.com/Esthien-Labs/argus-sdk/issues)
- [Feedback Form](https://esthien.com/feedback)
- Email: founder@esthien.com
