# Your First Report

This guide walks through the evidence report produced by `argus regression-eval`.

## Run the evaluation

```bash
argus regression-eval --sample --out out/my-first-report
```

## Output files

```
out/my-first-report/
  regression_report.json     # Machine-readable results
  regression_report.md       # Human-readable summary
  regression_report.html     # Shareable browser report
  evidence_manifest.json     # Cryptographic attestation
  sample_trace.atlas-trace.json  # The synthetic trace used
```

## Understanding the report

### Evidence class

Every report declares its evidence class:

```json
{
  "evidence_class": "digital_source_verification",
  "evidence_boundary": "Software simulation only. No hardware measurements."
}
```

This is not a claim of hardware performance - it's a statement of what the evidence covers.

### Fault case results

Each fault case shows:

- **fault_id**: Unique identifier (e.g., `fc_001_stale`)
- **fault_kind**: Category (stale_command, missing_burst, etc.)
- **outcome**: PASS or FAIL
- **expected_state**: What the safety envelope should do
- **actual_state**: What it did

```json
{
  "fault_id": "fc_001_stale",
  "fault_kind": "stale_command",
  "outcome": "PASS",
  "expected_state": "safe_halt",
  "actual_state": "safe_halt"
}
```

### Standards citations

The manifest cites specific standard sections:

```json
{
  "applicable_standards": [
    {
      "standard": "ISO 3691-4:2023",
      "sections": ["5.2.3", "5.3.1", "6.4.2"]
    }
  ]
}
```

## Using the report

The evidence package is suitable for:

- Engineering review and sign-off
- Safety case dossier inclusion
- Audit trail documentation
- Regression tracking over releases

## Next steps

- [Evidence Classes](../guides/evidence-classes.md) - Understand what each class means
- [Custom Profiles](../guides/custom-profiles.md) - Create a profile for your system
