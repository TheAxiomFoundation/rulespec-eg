# rulespec-eg Agent Notes

This repo stores Egypt RuleSpec source registry materials, oracle references, and encoded policy rules. All encoded law lives under a single `eg/` namespace.

## Scope

- `eg/statutes/`: Egyptian laws - Law 91/2005 (income tax), Law 148/2019 (social insurance and pensions), Law 67/2016 (VAT), and other primary law needed for tax-benefit modeling. Tranche-1 modules are per-slice (kitab/bab citation paths) - the full-document program encodes every slice.
- `eg/regulations/`: executive regulations and ministerial/agency decrees.
- `eg/policies/`: administratively set programme rules (Takaful & Karama operational parameters pre-2025).
- `programs/`: declarative compose specs (one per jurisdiction/program/period).
- `data/coverage/`, `data/oracles/`: coverage backlog and comparison references. These are never legal authority.

## Do

- Start from the furthest upstream source: Official Gazette texts and official agency prints (ETA, NOSI) first, ministry decrees next, commercial legal databases never as primary - record the host in manifest metadata.
- Respect the capture notes (see README): force_ocr/ocr_dpi 400/ocr_language ara for the official prints (image-only or broken-glyph text layers); numeral-heavy provisions carry OCR risk - never guess a garbled number, defer honestly.
- Add RuleSpec under `eg/statutes/`, `eg/regulations/`, or `eg/policies/` with companion `.test.yaml` files.
- Cite corpus paths from modules via `module.source_verification.corpus_citation_path` (or `corpus_citation_paths`).
- Use the EGYMOD v1.0 policy window (2019-25) as the validation frame: PIT exemption EGP 7,000-20,000 with phase-out over 600,000; SIC 11% ee / 18.75% er by branch with insurable-salary caps; VAT 14%. Indexed/annual values must be corpus-grounded, never invented.
- Keep exact oracle versions in `data/oracles/oracle-index.json`. The SOUTHMOD bundle is licensed and non-redistributable - never commit bundle bytes, dataset rows, or model XML.
- Sync `axiom-encode` and `.axiom/toolchain.toml` before substantial encoding runs.

## Do Not

- Use tax-firm alerts or commercial legal databases as the first legal source when a law or instrument governs the rule.
- Invent, round, or interpolate any Egyptian monetary amount, rate band, or threshold. Every number must come verbatim from a captured official provision - OCR noise is a deferral reason, not a rounding license.
- Migrate EGYMOD, EUROMOD/SOUTHMOD, or agency calculator code mechanically as RuleSpec.
- Add generated source payload dumps, formula artifacts, `parameters.yaml`, or standalone YAML fixtures outside allowed RuleSpec roots.
- Hand-copy statute text into RuleSpec without a corpus `citation_path`.
