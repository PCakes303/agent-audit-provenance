# Agent Audit & Provenance

**Repository:** `PCakes303/agent-audit-provenance`  
**Portfolio position:** 10 / 31 public repositories  
**Maturity:** scaffolding  
**License:** [Scoped mixed-license policy](LICENSE.md).

## Purpose

Provide portable audit-event contracts and a small append-only, hash-chained JSONL prototype for traceability across agent components.

## Initial implementation

- Versioned audit-event JSON Schema.
- Deterministic canonical JSON hashing with SHA-256.
- JSONL append and full-chain verification CLI.
- Fail-closed validation of required event fields and chain integrity.
- Synthetic examples and regression tests.

## License status

This repository applies a scoped mixed-license policy: original source code and machine-readable contracts are licensed under Apache-2.0; original human-readable documentation is licensed under CC BY 4.0. Third-party material retains upstream terms. Datasets, evidence, fixtures, sample payloads, media, and material with uncertain provenance are not blanket-licensed and require separate review. See [LICENSE.md](LICENSE.md).

## Quick start

Requires Python 3.10+ and no third-party runtime dependencies.

```bash
python tools/audit_log.py append --log examples/events.jsonl --event examples/event.json
python tools/audit_log.py verify --log examples/events.jsonl
python -m unittest discover -s tests -v
```

The example log is a fixture. Copy it before appending if you want to preserve the baseline example.

## Security boundary

A hash chain detects accidental or unsophisticated modification only when a trusted prior digest is retained independently. It does not authenticate event producers, prove event truth, prevent truncation by itself, provide non-repudiation, encrypt data, or create a trusted timestamp. SHA-256 hashes are integrity links, **not digital signatures**.

Production deployment requires authenticated event ingestion, key management and signatures, externally anchored checkpoints, access controls, retention policy, privacy review, and independent security assessment.
