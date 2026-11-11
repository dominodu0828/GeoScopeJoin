# GeoScopeJoin reproduction artifact

Artifact for **[Experiment, Analysis, and Benchmark] GeoScopeJoin: When Does Exact
Spatial Query Reuse Pay?** Prepared for ICDE 2027; submission/acceptance is not
claimed by this repository.

## Manuscript and revision evidence (12 November 2026)

[Read the revised manuscript](GeoScopeJoin-2026-11-12.pdf) or [download its LaTeX sources and evidence](GeoScopeJoin-evidence-2026-11-12.zip). The PDF includes the four-tool Round 5 disclosure and cites the EDBT 2026 version of IMP. Table V reports the amortization results for 1, 10, and 100 requests. The ZIP includes the session-based uncertainty analysis, the all-ten-session sensitivity check, the synthetic bidirectional NoData fixture, the Round 2 window manifest, and both files needed to verify the freeze-digest discrepancy in Section V-A. Compare the SHA-256 of evidence/freeze_g0.json with the freeze_sha256 field inside evidence/e1_report.json using the command in the ZIP README.

To run the two revision checks, restore the [v1.0.0 reproduction artifact](https://github.com/dominodu0828/GeoScopeJoin/releases/tag/v1.0.0) as described below and extract the revision ZIP into a subdirectory named `paper_evidence_revision_20261112` under the restored root. Run the two scripts listed in the ZIP's README with the project dependencies installed.

| File | SHA-256 |
| --- | --- |
| Manuscript PDF | `018805568d02bca3dd6d6245b4187078e24c849070ceb045fa5c0110a7b46be2` |
| Revision ZIP | `8d59ade321966cb661c622d11613c4004b72d56a677736f91bf24d360a163ce8` |

## Obtain the complete artifact

Download `GeoScopeJoin-reproduction-v1-deduplicated.zip` (263 MB) from this
repository's Releases and verify against `SHA256SUMS-compact.txt`. Extract it and run:

```sh
python restore_artifact.py GeoScopeJoin-restored
cd GeoScopeJoin-restored
python verify_artifact.py
```

This lossless package stores identical snapshots once. Restoration recreates all
7,172 original files and the complete inventory byte for byte (verified before
publication). Allow 1.8 GB for the restored tree. It includes code, original source
archives, point snapshots, historical session outputs, protocols and reports.
The source ZIP alone does not include the large inputs or run directories.
The old non-deduplicated archive name in the preserved internal README is
superseded by the compact release distribution.

## Environment

Use Python 3.13. Create a virtual environment and install the pinned dependencies:

```sh
python -m venv .venv
# Windows: .venv\Scripts\activate
# Linux/macOS: source .venv/bin/activate
python -m pip install -r requirements.txt
python verify_artifact.py
```

From the extracted root, run the correctness gates first:

```sh
python -I round5_evaluation/code/run_g0.py
python -I round5_evaluation/code/run_e5.py
```

Full measurement commands (historical durations are estimates, not guarantees):

```sh
python -I round5_evaluation/code/run_e2.py --skip-timing
python -I round5_evaluation/code/run_e2.py --skip-counts --blocks 30
python -I round5_evaluation/code/run_e1.py --amortization
python -I round5_evaluation/code/run_e4.py
python -I round5_evaluation/code/run_e3.py
python -I round5_evaluation/tools/recompute_amort.py
python -I round5_evaluation/tools/make_reports.py
python -I round5_evaluation/tools/make_latex_tables.py
```

The full measurement sequence takes hours and overwrites current report files;
historical reports remain in `historical_results/`. Exact elapsed times and
confidence intervals depend on hardware and runtime conditions. Correctness gates,
source hashes and the controlled counting identity are the portable checks.

## Evidence and limits

- Historical reports: `historical_results/reports/R5_RESULTS.md` and
  `CLAIM_LEDGER_R5.csv`; original per-session records: `round5_evaluation/runs/`.
- Shenzhen is a same-epoch R2022A/R2023A revision pair. São Paulo is a cross-epoch
  R2023A sequence; 2025/2030 are projections, not observed changes.
- E2 is a controlled mechanism experiment. E5 uses a selected real OSM node move.
- Real NoData transitions and a third comparable release remain unavailable.
- No configuration in the reported E1 comparison passed the protocol-specified 5%
  end-to-end service threshold. This is not a new spatial indexing algorithm.
- `PUBLICATION_CHANGES.md` describes the path portability change and validation.
- `THIRD_PARTY_NOTICES.md` provides dataset licenses and attribution.

The old 99 KB packet is preserved as historical evidence; use this complete
release instead. Its old statement that nothing is published describes its
pre-publication state and does not describe this repository.
