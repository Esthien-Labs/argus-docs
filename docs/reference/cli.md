# CLI Commands

## argus profile-check

Validate a profile and print summary.

```bash
argus profile-check --profile <path>
```

**Options:**
- `--profile` - Path to profile JSON (required)
- `--verbose` - Show detailed validation output

## argus regression-eval

Run a controller regression evaluation.

```bash
argus regression-eval [options]
```

**Options:**
- `--profile <path>` - Profile to use
- `--trace <path>` - Input trace file
- `--sample` - Generate synthetic trace
- `--out <dir>` - Output directory (default: `out/regression-eval`)
- `--evidence-class <class>` - Override evidence class

## argus safety-case

Generate a digital ACEK safety assurance case.

```bash
argus safety-case --profile <path> --out <dir>
```

## argus bench

Run the EMG/IMU replay benchmark.

```bash
argus bench [options]
```

## argus benchmark-lab

Run a declared partner-evaluation scorecard.

```bash
argus benchmark-lab --scorecard <path>
```

## argus gate

Check hardware evidence gate status.

```bash
argus gate [--verbose]
```

## argus alpha-check

Run all Digital Alpha verification checks.

```bash
argus alpha-check [--verbose]
```

## Global options

All commands support:

- `--help` - Show help
- `--version` - Show version
- `--verbose` / `-v` - Verbose output
