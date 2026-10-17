# Safety, limitations and pre-deployment checks — DECICE_Green_Computing

**Scope:** Prophet-based electricity carbon-intensity forecast API for the IT-NO electricity zone.  
**Issued:** 2026-10-17  
**Status:** Risk guidance only. No claim is made that any checklist item is already implemented, tested, legally approved or certified.

This document supplements [DISCLAIMER.md](DISCLAIMER.md) and the existing copyright/license terms without changing either. It does not prevent claims or waive mandatory legal duties.

## Risks to assess

- Training data and model may be stale; predictions can be wrong or outside their supported scope.
- Inaccurate carbon-intensity forecasts can trigger economically inefficient or counterproductive scheduling.
- An unauthenticated public API may be abused and may not meet commercial availability or accuracy needs.

## Checks before live use

- [ ] Report model provenance, training period, validation metrics and timestamp of last retraining alongside predictions.
- [ ] Use official verified live data for consequential energy or carbon-accounting decisions; measure forecast drift.
- [ ] Test invalid dates, timezone and daylight-saving transitions, request limits and resource exhaustion.
- [ ] Do not claim forecasts are authoritative carbon accounting or guaranteed emissions reductions.

## User and maintainer responsibilities

Begin in an isolated, authorized test environment; apply least privilege, backups, monitoring and an independent review of any high-impact outputs or actions. Where a project depends on third-party providers or real equipment, comply with vendor terms and safety instructions. Report suspected security flaws privately. Record actual test evidence, versions and unresolved risks rather than inferring that documentation is proof of implementation.

**Mandatory rights preserved:** Liability, product-safety, privacy, security and consumer obligations cannot be eliminated by this notice where applicable law forbids exclusion.
