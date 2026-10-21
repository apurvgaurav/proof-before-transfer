# Proof Before Transfer

This repository contains the research artifacts for my paper, **Proof Before Transfer: Leakage-Resistant Qualification for Post-Quantum TLS Intrusion-Detection Studies**.

I examined the checks needed before interpreting an intrusion detector's performance across classical and post-quantum TLS. The study evaluated the classical stage on synthetic traffic. Later diagnostics found that every qualification record-length pattern already occurred in training with the same label. The paper reports the qualification procedure and what those diagnostics revealed about its limits.

The X25519-to-X25519MLKEM768 transfer experiment was not run.

## Download the evidence

The complete public package is [proof-before-transfer-v1.0.1.zip](proof-before-transfer-v1.0.1.zip). Its [SHA-256 checksum](proof-before-transfer-v1.0.1.zip.sha256) identifies the exact archive. The package includes its own file manifest and provenance records.

Inside the archive are the retained semantic units and feature rows, five fitted CatBoost models, fitted sigmoid coefficients, saved qualification predictions, historical scientific source, and the completed baseline diagnostics. The stored partitions contain 512 training units, 64 stopping-validation units, 64 calibration units, and 256 qualification units. Each qualification unit contains four requests.

The archive includes the R3 PCAP adapter and 24-feature extractor, their historical dependency lock and representation contract, and the exact Python bodies for R5 feature materialization, P7 prediction and P8 adjudication. These historical sources are separate from the portable verification script. The archive also contains the figure source and exports.

## Check the results

Extract the ZIP and open the `proof-before-transfer-v1.0.1` folder. With Python 3.11 or newer:

```bash
python -m pip install -r requirements-verification.txt
python verify.py --report ../verification-v1.0.1.json
```

The script checks the file hashes, stored partitions and features, saved Brier calculations, the original unit-stratified bootstrap, and the preserved baseline and calibration arithmetic. It does not refit the models or rerun the main detector on qualification data. Stored baseline coefficients are evaluated and compared with the saved predictions.

The [verification guide](VERIFICATION.md) explains each check. A [verification report](verification-v1.0.1.json) records the completed run. The historical runners are retained for inspection; they depend on the original environment and are not the supported verification command.

## Changes in version 1.0.1

I added the recovered feature-extraction source and binding records omitted from version 1.0.0. The scientific data, fitted models, saved predictions and verifier are unchanged. The new archive passed all 905 verification checks after extraction.

I also clarified the label-access limit. The historical P7 script loaded a preparation record containing labels before main-model prediction. Its prediction calls received only feature columns, and qualification scoring followed prediction. This supports feature-input separation, not process-wide label isolation or proof of the full historical tuning chronology.

## What remains unavailable

This is a deposit of the available study evidence. It does not reconstruct the entire experiment from raw captures. The exact frozen nuisance evaluator, complete qualification capture archives, final R5 semantic-unit construction source, and parts of the historical runtime and freeze records are missing. The included DEV-CAL margin file is a retrospective check, not the original calibration-time log.

[MISSING_EVIDENCE.md](MISSING_EVIDENCE.md) gives the full list. [Original artifact hashes](original_artifact_hashes.json) identify the historical objects and distinguish an included file from a recorded but unavailable archive. A matching saved result does not establish that the synthetic task was difficult or that the detector generalizes to production traffic.

The release contains the earlier baseline diagnostics. It does not claim a new harder qualification task, a representation-ablation study, or an empirical post-quantum transfer result.

## Citation and reuse

Version: **1.0.1**, released **21 October 2026**. Citation metadata is in [CITATION.cff](CITATION.cff). The current reuse status is recorded in [LICENSE_STATUS.md](LICENSE_STATUS.md).

Apurv Gaurav
