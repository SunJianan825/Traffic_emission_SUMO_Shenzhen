# Code and Reproduction Guide

This document describes the code included in this GitHub upload folder and how it relates to the manuscript.

## 1. Code Folder

Primary code root:

```text
code/futian_core1km_eadrl_run
```

This folder contains the as-used SUMO/TraCI EA-DRL experiment code copied from the final Futian evidence package. Python cache files were not copied.

### Environment Files

```text
code/futian_core1km_eadrl_run/requirements.txt
code/futian_core1km_eadrl_run/environment.yml
```

The workflow requires Python and SUMO/TraCI. The conda environment file specifies Python 3.10 and includes SUMO where available through conda-forge.

Typical setup:

```bash
conda env create -f code/futian_core1km_eadrl_run/environment.yml
conda activate futian5km-rl
```

If SUMO is installed manually, verify `SUMO_HOME` and the availability of `sumo`, `sumo-gui`, `netconvert`, `duarouter` and `randomTrips.py`.

## 2. Main Configuration Files

| File | Role |
|---|---|
| `configs/experiment_spec_core1km_10k.yaml` | Authoritative Futian 1-km, 154-TLS experiment configuration used by the final code path. |
| `configs/reward_variants.yaml` | Reward definitions, including the composite emission-aware reward. |
| `configs/signal_safety.yaml` | Common signal safety constraints used by all controllers. |
| `configs/incidents.yaml` | Incident/disturbance scenario support retained for extension; not central to S0-S5 main results. |

The final manuscript reports scenarios S0-S5. S6-S8 are retained in the repository for traceability and future extensions.

## 3. Source Modules

| Module | Purpose |
|---|---|
| `src/network/` | OpenStreetMap download, SUMO network conversion and network statistics. |
| `src/tls/` | Traffic-light catalogues, controllable TLS subsets and safety guards. |
| `src/demand/` | Route generation, demand scaling and departure-profile handling. |
| `src/fleet/` | Vehicle type and EV/ICE fleet handling. |
| `src/envs/futian_sumo_env.py` | SUMO/TraCI environment, observations, action masks and reward components. |
| `src/controllers/` | Fixed-time, actuated, max-pressure and RL controller implementations. |
| `src/train/` | Shared PPO-style actor-critic policy and training routines. |
| `src/eval/` | Final controller/scenario/seed evaluation routines. |
| `src/metrics/` | CO2, delay, stops, throughput, travel-time and reward-normalization utilities. |
| `src/analysis/` | Statistical summaries and result-table generation. |
| `src/utils/` | Configuration, SUMO and TLS utility functions. |

Legacy or earlier exploratory tools may remain under `src/tools/`. The final reported Futian experiment is identified by the Futian config and by `docs/source_manifest/REGION_AUDIT_FUTIAN.md`.

## 4. Shell Entry Points

```text
scripts/env_check.sh
scripts/build_network.sh
scripts/build_tls_catalog.sh
scripts/build_demand.sh
scripts/train_all.sh
scripts/eval_all.sh
scripts/analyze.sh
```

These scripts are retained as practical entry points for rebuilding network inputs, demand, training runs, evaluations and analysis.

## 5. Final Analysis Reproduction

The easiest way to reproduce the paper tables and main statistical claims is to start from:

```text
data/05_analysis/final_s0s5_8seeds/
```

Key files:

```text
all_runs_network_metrics_s0s5_8seeds.csv
summary_network_metrics_s0s5_8seeds.csv
paired_tests_eadrl_vs_baselines_s0s5_8seeds.csv
paper_grade_criteria_by_scenario.csv
paper_ready_final_s0s5_8seeds_summary.md
```

These files summarize the final 192-run S0-S5 matrix used in the manuscript.

## 6. Figure Generation Code

Figure-generation scripts are in:

```text
code/figure_generation/
```

Important subfolders:

| Folder | Description |
|---|---|
| `main_figures/` | Script and README for regenerating main/SI figure assets from the Futian package. |
| `package_generation/` | Scripts used to build or upgrade final package assets. |
| `si_0528/` | Script used to generate the 2026-05-28 SI figures from copied CSV source data. |

Figure source data are under:

```text
data/07_figures/source_data/
data/09_si_process_0528/data/
```

## 7. Manuscript and SI Sources

The final LaTeX sources are included for transparency:

```text
manuscript/main_overleaf_0528/
manuscript/si_overleaf_0528/
```

These are the source files used for the manuscript and Supplementary Information after the 2026-05-28 revision.

## 8. Limitations for Reuse

- This is a SUMO-based simulation case study.
- The demand files are synthetic route files, not observed municipal counts.
- Signal timing is inferred from the SUMO network conversion and traffic-light catalogue.
- The reported emission metric is direct simulated tailpipe CO2 only.
- Before operational deployment, the model would require field calibration, detector validation and controller-in-the-loop testing.

