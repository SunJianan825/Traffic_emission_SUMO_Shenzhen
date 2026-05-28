# Data Description

This document describes the data included in this GitHub upload folder and how each part relates to the manuscript.

## 1. Study Area and Network Data

Location:

```text
data/03_sumo_inputs/futian_core1km_network/
```

Files:

| File | Description |
|---|---|
| `futian1km.osm.xml` | OpenStreetMap-derived road geometry for the Futian/Shenzhen Civic Center core. |
| `futian1km.net.xml` | SUMO network used for the final 154-signal experiment. |
| `net_stats_core1km.json` | Network statistics used to report network scale. |

Key study-area values:

- Reference point: Shenzhen Civic Center, 22.543694 N, 114.059623 E.
- Nominal study area: 1-km-radius core.
- SUMO original boundary: 114.044495,22.532017,114.073149,22.559587.
- Controlled signalized intersections: 154.

## 2. Traffic-Light and Vehicle-Type Data

Locations:

```text
data/03_sumo_inputs/futian_tls_core1km/
data/03_sumo_inputs/futian_vehicle_types/
```

Files:

| File | Description |
|---|---|
| `tls_catalog.json` | Traffic-light catalogue inferred from the SUMO network. |
| `tls_subset_controllable.json` | Controllable traffic-signal subset. |
| `vtypes.add.xml` | SUMO vehicle-type file, including ICE and EV emission classes. |

Fleet assumptions:

- Passenger/taxi/bus/truck shares: 0.82/0.10/0.05/0.03.
- ICE passenger cars and taxis use SUMO HBEFA3/PC_G_EU4 class.
- EV passenger cars and taxis use SUMO `zero` direct-emission class.
- CO2 outputs are direct simulated tailpipe CO2, not life-cycle emissions.

## 3. Demand and Scenario Data

Location:

```text
data/03_sumo_inputs/futian_demand_core1km/
```

Main manifest:

```text
data/03_sumo_inputs/futian_demand_core1km/demand_manifest.json
```

Final manuscript scenarios:

| Scenario | Demand scale | EV share | Role |
|---|---:|---:|---|
| S0 | 1.0 | 0.20 | Base demand and reference fleet. |
| S1 | 0.7 | 0.20 | Low-demand sensitivity case. |
| S2 | 1.3 | 0.20 | High-demand sensitivity case. |
| S3 | 1.6 | 0.20 | Oversaturated demand boundary case. |
| S4 | 1.0 | 0.10 | Low-electrification sensitivity case. |
| S5 | 1.0 | 0.35 | Medium-electrification sensitivity case. |

Additional retained scenarios:

| Scenario | Role |
|---|---|
| S6 | High-electrification scenario retained for extension. |
| S7 | Lane-closure incident scenario retained for extension. |
| S8 | Bus-dwell/disturbance scenario retained for extension. |

The main manuscript reports S0-S5 only.

## 4. Training Outputs

Location:

```text
data/04_training_outputs/
```

This folder preserves staged EA-DRL training outputs, continuation logs, server logs, local diagnostic outputs and model artifacts used to support the training-stage provenance reported in the paper and SI.

Important content:

| Folder | Description |
|---|---|
| `server_300k_training/` | Final 300k seed2 continuation artifacts. |
| `server_logs_200k_to_300k/` | Logs for final continuation from 200k to 300k. |
| `server_logs_final_s0s5/` | Logs for the final S0-S5 eight-seed evaluation. |
| `local_training_outputs/` | Earlier staged local and diagnostic training outputs. |
| `server_migration_scripts/` | Scripts and notes used for server-side runs. |

## 5. Final Analysis Data

Location:

```text
data/05_analysis/final_s0s5_8seeds/
```

Central files for paper results:

| File | Description |
|---|---|
| `all_runs_network_metrics_s0s5_8seeds.csv` | One row per scenario-controller-seed run. |
| `summary_network_metrics_s0s5_8seeds.csv` | Scenario-controller means, standard deviations and confidence intervals. |
| `paired_tests_eadrl_vs_baselines_s0s5_8seeds.csv` | Paired t-tests, Wilcoxon tests and paired effect sizes. |
| `paper_grade_criteria_by_scenario.csv` | Scenario-level EA-DRL versus max-pressure summary. |
| `paper_ready_final_s0s5_8seeds_summary.md` | Human-readable final evaluation summary. |

The final analysis matrix contains:

```text
6 scenarios x 4 controllers x 8 paired seeds = 192 completed simulations
```

## 6. Raw Results and Logs

Location:

```text
data/06_results/
```

This folder contains raw metric files, SUMO logs and server output snapshots for the final experiment. It is included for auditability. Most readers can reproduce manuscript tables from the compact CSVs in `data/05_analysis/final_s0s5_8seeds/`.

## 7. Figure and SI Source Data

Locations:

```text
data/07_figures/
data/08_si_additional_assets/
data/09_si_process_0528/
```

Important source-data files:

| File | Role |
|---|---|
| `data/07_figures/source_data/all_runs_network_metrics_s0s5_8seeds.csv` | Figure source copy of the final all-run matrix. |
| `data/07_figures/source_data/summary_network_metrics_s0s5_8seeds.csv` | Figure source copy of final summary metrics. |
| `data/07_figures/source_data/paired_tests_eadrl_vs_baselines_s0s5_8seeds.csv` | Figure source copy of paired tests. |
| `data/07_figures/source_data/stage_validation_summary_1k_60k_110k_200k_300k.csv` | Training-stage validation source data. |
| `data/09_si_process_0528/data/*.csv` | Compact SI figure source data used by the 2026-05-28 SI revision. |

## 8. Manuscript and SI Data Connection

Final LaTeX sources:

```text
manuscript/main_overleaf_0528/
manuscript/si_overleaf_0528/
```

The main paper uses the central final analysis CSVs and final figure files. The SI uses additional training, stage-validation, seed-level and figure-source data from `data/07_figures`, `data/08_si_additional_assets` and `data/09_si_process_0528`.

## 9. Data Caveats

- The demand and route files are simulation inputs generated for SUMO; they are not observed traffic counts.
- The signal timing data are inferred from SUMO network conversion and traffic-light catalogues; they are not municipal controller records.
- The CO2 metrics are direct simulated tailpipe CO2 values from SUMO.
- The repository should be cited as a simulation evidence package rather than a field-calibrated traffic-management data archive.

## 10. Attribution Notes

- Road geometry is derived from OpenStreetMap and should retain OpenStreetMap attribution.
- SUMO and TraCI are used for simulation and control interaction.
- HBEFA-style emission classes are used through SUMO vehicle emission modelling.

