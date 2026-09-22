# Evidence Classes

Every Argus report declares its evidence class - what the evidence demonstrates and what it does not.

## Classes

| Class | Description | Hardware required |
|-------|-------------|-------------------|
| `digital_source_verification` | Software simulation only | No |
| `measured_partial` | Some hardware measurements | Partial |
| `hardware_measured` | Full hardware bring-up | Yes |

## digital_source_verification

**Default class for SDK evaluations.**

This evidence demonstrates:

- Profile schema validity
- Trace format compliance
- Fault injection and interception logic
- Report generation pipeline

This evidence does **not** demonstrate:

- Physical hardware timing
- Real-world sensor behavior
- Actuator response characteristics
- Environmental conditions

```json
{
  "evidence_class": "digital_source_verification",
  "evidence_boundary": "Software simulation only. No calibrated hardware measurements."
}
```

## measured_partial

Some measurements from physical hardware, but not complete.

Requires:

- At least one programmed target (MCU or FPGA)
- Instrument measurements for measured parameters
- Software simulation for remaining parameters

```bash
argus regression-eval --trace real_trace.mcap --evidence-class measured_partial
```

## hardware_measured

Full hardware bring-up with calibrated instruments.

Requires:

- NUCLEO-H743ZI2 programmed with Argus ESC firmware
- ULX3S-12F programmed with Argus safety bitstream
- Calibrated oscilloscope measurements
- Complete fault corpus on physical hardware

```bash
argus regression-eval --trace hardware_trace.mcap --evidence-class hardware_measured
```

## Evidence boundaries

Every report includes an explicit boundary statement:

```json
{
  "evidence_boundary": "This report covers software simulation of fault interception. It does not claim hardware timing, physical actuator behavior, or environmental conditions."
}
```

This prevents:

- Overstating simulation results as hardware performance
- Conflating evidence classes
- Misrepresenting capability

## Upgrading evidence class

To upgrade from `digital_source_verification` to `hardware_measured`:

1. Complete hardware bring-up (see firmware docs)
2. Run fault corpus on physical hardware
3. Record calibrated measurements
4. Pass `--evidence-class hardware_measured`

The SDK validates that hardware evidence requirements are met before accepting the upgrade.

## Next steps

- [Custom Profiles](custom-profiles.md) - Define your own fault corpus
- [CLI Reference](../reference/cli.md) - All command options
