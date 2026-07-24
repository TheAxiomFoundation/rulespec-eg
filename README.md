# rulespec-eg

Egypt RuleSpec source registry.

This repository targets the Egyptian tax-benefit surface simulated by EGYMOD (the SOUTHMOD tax-benefit microsimulation model for Egypt, UNU-WIDER; v1.0, policy years 2019-25): personal income tax under Law 91/2005 (2019 credit regime; 2020-25 progressive-with-phase-out regimes governed by amendment Laws 26/2020, 30/2023, 7/2024 - tranche-2 captures; annual personal exemption EGP 7,000 rising to 20,000; phase-out tiers over EGP 600,000), social insurance contributions under Law 148/2019 (unified regime: employee 11 percent / employer 18.75 percent of insurable salary by branch, with monthly caps), VAT under Law 67/2016 (14 percent general rate; schedule tax), and the Takaful & Karama cash transfers (statutorily codified by Law 12/2025 - top tranche-2 capture; the modeled 2019-24 systems operated administratively).

All encoded law lives under a single `eg/` namespace. The validation frame is EGYMOD v1.0 (report CR-EGYMOD-v1.0, Tables 1.6-1.7 and 2.4-2.8).

**Full-document program**: unlike the other SOUTHMOD lanes, the Egypt tranche-1 captures are sliced per structural unit (kitab/bab) via `page_windows`, and the encode backlog covers EVERY slice - the union of slices is the entire text of each captured instrument.

## Source Priority

Policy must come from the furthest upstream available source: Official Gazette (al-Jarida al-Rasmiyya / al-Waqai al-Misriyya) texts and official agency prints first (Egyptian Tax Authority law prints, NOSI law books - record the host in manifest metadata), ministry decrees next, commercial legal databases never as primary. Capture notes: official Arabic prints carry image-only or broken-glyph text layers - capture with `force_ocr`, `ocr_dpi: 400`, `ocr_language: ara` (structure and worded amounts OCR cleanly; numeral-heavy provisions carry OCR risk that the encode gates handle honestly). The Egyptian Legislation Portal (elpai.idsc.gov.eg) is subscription-gated - metadata only.

## Corpus binding

`.axiom/toolchain.toml` pins the immutable signed corpus release this repository consumes (`eg-rulespec-2026-07-24`). The shared validate workflow verifies the release object signature, content hash, and waiver-set hash on every push.

## Layout

- `eg/statutes/`, `eg/regulations/`, `eg/policies/`: encoded RuleSpec modules with mandatory companion `.test.yaml` files.
- `programs/`: declarative compose specs (one per jurisdiction/program/period).
- `data/oracles/`, `data/coverage/`: comparison-oracle references and the EGYMOD instrument map. Never legal authority.

## Parity program

Tracked on issue #1: tranche-2 captures (Law 12/2025 Takaful & Karama codification - no publicly hosted official copy located yet; PIT amendment Laws 97/2018, 26/2020, 30/2023, 7/2024; Law 79/1975 predecessor social insurance; VAT schedule-tax amendments; Takaful & Karama executive regulation) and EGYMOD parity tests per instrument.
