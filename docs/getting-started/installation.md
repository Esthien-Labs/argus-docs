# Installation

## Requirements

- Python 3.11 or later
- pip (included with Python)
- No hardware required for software evaluation mode

## Install with pip

```bash
pip install esthien-argus-sdk
```

## Install with pipx (recommended for CLI use)

[pipx](https://pipx.pypa.io/) installs the CLI in an isolated environment:

```bash
pipx install esthien-argus-sdk
```

## Verify installation

```bash
python -m esthien --version
```

Expected output:
```
esthien-argus-sdk 0.7.3
```

## Optional dependencies

For MCAP trace support:

```bash
pip install mcap
```

## What's included

The SDK includes:

- `argus` CLI with all commands
- 3 reference profiles (ROS 2, CAN-bus, SPI)
- Sample trace generator
- Evidence report templates

## Next steps

- [Quickstart](quickstart.md) - Run your first evaluation in 3 commands
- [Profiles](../guides/profiles.md) - Understand the reference profiles
