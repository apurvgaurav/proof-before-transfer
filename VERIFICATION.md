# Verification scope

`verify.py` is the supported entry point for this release. It uses the Python standard library and NumPy, reads the retained evidence, and optionally writes its report outside the release directory. It does not modify the release.

```bash
python -m pip install -r requirements-verification.txt
python verify.py --report ../verification-v1.0.0.json
```

Python 3.11 or newer is required. The dependency file pins the NumPy version used for this verification adapter. It does not describe the historical training or acquisition environment.

## Checks performed

1. **Release integrity.** Verify every file against `MANIFEST.sha256`, reject unsafe or duplicate manifest paths, and repeat the integrity check after the calculations.
2. **Stored partitions and features.** Check 896 units against the retained feature source and semantic records: 512 TRAIN, 64 DEV_STOP, 64 DEV_CAL, and 256 QUAL. Check unit/slot uniqueness, recorded family/label balance, schedule identities, all 24 feature names, and the 11 categorical and 13 scalar fields. These are checks of retained records, not a reconstruction of the original partition generator or label-access chronology.
3. **Reconciliation index derivative.** Check the public index's hash, basename-only locator column, unchanged nonlocator commitment, and 256 bindings to retained feature and reconciliation rows. The absent underlying row archives and the original unmodified locator index are not verified by this public script.
4. **Saved qualification calculations.** Load numerical arrays with pickle disabled. Recompute the mean of the five saved probability vectors; report direct Brier losses, pooled and family gains, and all seed gains. Recompute the 10,000-replicate stratified bootstrap using PCG64 seed 1447780860, four family/label strata of 64 complete semantic units, and the linear fifth-percentile quantile. Compare the calculations and bootstrap-byte commitment with the retained results. Two gate conditions are only compared with recorded certificate markers: semantic overlap and historical model/calibration freeze. A matching marker does not independently prove either condition.
5. **Stored model and calibration records.** Hash the five CBM files and compare their freeze records. Check the stated historical calibrator hashes and exact coefficients. Recheck sigmoid arithmetic for 320 saved retrospective DEV-CAL records. No model is loaded to regenerate those margins. The historical joblib files are deliberately omitted; checking a recorded joblib hash is not verification of its absent public byte stream.
6. **Previously fitted baselines.** Derive the documented numeric features from the saved feature rows, check TRAIN scaler statistics and stored token counts, and replay saved logistic coefficients, stump thresholds, training-prior probability and token table. Compare 48 model/partition prediction arrays, 144 pooled/family score groups, and 10,752 per-unit prediction records. This includes arithmetic evaluation of stored baselines on qualification rows; it does not train or tune a model.

The report records failures and exits with a nonzero status if a check fails. Integrity or replay failure needs investigation; it must not be treated as a new scientific result.

## Execution boundary

The supported command performs **no new fits or main frozen-model inference; stored-baseline arithmetic replay only**. It does not call the archived scientific runners, deserialize CatBoost/joblib objects, install software, open a network connection, collect traffic, or run the post-quantum transfer experiment. The installation command above is a separate environment setup step.

The extracted P7 and P8 code under `scientific_source/r5/` records the historical calculation. P7 contains the original main-model inference and nuisance-fitting calls and depends on the missing exact nuisance evaluator. These files are source evidence, not runnable replacements for the supported verifier. Their extraction boundaries and hashes are documented in `provenance/P7_P8_SOURCE_EXTRACTION.json`.

## Provenance and interpretation

`PROVENANCE.json` identifies retained evidence members and their source containers. `MANIFEST.sha256` commits to the current public bytes. The two commitments serve different purposes: a public derivative's hash is not the hash of its original private source. The reconciliation locator and diagnostic protocol transformations have separate derivation records.

Several historical audits retain the paths used when they were written. Their original source and findings are preserved, but their old command lines are not portable instructions. Use this guide for the supported checks and [MISSING_EVIDENCE.md](MISSING_EVIDENCE.md) for the remaining reproduction limits.

A successful verification confirms consistency of the preserved data and calculations. It cannot supply missing acquisition records, recover a missing evaluator, turn retrospective diagnostics into a prospectively independent test, or establish a post-quantum transfer effect.
