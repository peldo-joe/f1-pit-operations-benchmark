# Formula 1 Pit Crew Operations & Six-Sigma Consistency Benchmark

End-to-end Python motorsport operations analysis ingesting **1,301 live Formula 1 stationary pit stop telemetry records** from the **OpenF1 REST API (`api.openf1.org`)** across all 11 F1 Constructors to benchmark pit crew speed, Interquartile Range (IQR) consistency, and pit-box SLA defect rates.

## 1. Executive Summary & Motorsport Operations Problem
Raw average pit stop times in Formula 1 are heavily distorted by non-routine pit events (5-second FIA penalty holds, front-wing nosecone replacements, and practice session garage setup checks). Even within competitive 4-tire changes, evaluating a pit crew solely on single-stop peak speed (`min`) obscures process variance and costly slow-stop defects (`> 3.5s`) that cost drivers track position during undercut/overcut windows.

This pipeline classifies **1,301 stationary F1 pit events** into operational regimes, isolates **1,150 competitive 4-tire race stops (`1.8s–6.0s`)**, and ranks every F1 constructor across five Six-Sigma operational KPIs:
1. **Peak Capability (`fastest_stop_sec`)**
2. **Central Tendency (`median_stop_sec` & `mean_stop_sec`)**
3. **Process Spread (`iqr_consistency_sec` — $P_{75} - P_{25}$)**
4. **Elite Undercut Execution Rate (`% of stops <= 2.5s`)**
5. **Pit Wall SLA Defect Rate (`% of stops > 3.5s`)**
<img width="935" height="508" alt="image" src="https://github.com/user-attachments/assets/1011bdb8-a5b4-490f-92a6-eaebf9b5ea7f" />

## 2. Key Operational Findings (1,301 Live OpenF1 Telemetry Records)
* **The McLaren Speed-vs-Variance Paradox:** **McLaren (`122` stops)** recorded the **single fastest stationary pit stop on the F1 grid (`1.80s`)**, yet ranked **6th overall in median performance (`2.70s` median, `2.98s` mean)** due to high process variance (**`1.08s` IQR**) and a **`19.67%` SLA defect rate (`> 3.5s`)**—nearly triple the defect rate of the grid leaders.
* **Ferrari & Mercedes Lead on Six-Sigma Process Control:**
  * **Ferrari (`#1` — `140` stops):** Led the grid in median stop speed (**`2.50s` median, `2.61s` mean**), highest **Elite Sub-2.5s Execution Rate (`57.86%`)**, and **lowest SLA defect rate (`6.43%` > 3.5s)**.
  * **Mercedes (`#4` — `122` stops):** Achieved the **tightest process consistency in Formula 1 (`0.50s` IQR)** and the second-lowest defect rate (**`6.56%` > 3.5s**), proving that controlling tail defects beats chasing single-stop flyers.
  * **Red Bull Racing (`81` stops) & Racing Bulls (`87` stops):** Maintained elite **`0.60s` IQR** consistency with **`51.72%`** (Racing Bulls) and **`45.68%`** (Red Bull) sub-2.5s execution rates.
* **Back-of-Grid Stationary Loss:** **Haas (`3.20s` median, `32.14%` defect rate)** and **Cadillac (`3.30s` median, `40.00%` defect rate)** concede **`0.70s–0.80s` per pit stop** in stationary jack time alone compared to the front-running crews.

## 3. Repository Contents
* **`f1_pit_crew_operations_benchmark.ipynb`** — Python data pipeline (`requests`, `pandas`, `numpy`) covering live OpenF1 REST API ingestion, multi-tier operational regime classification (`np.select`), IQR/percentile benchmarking, and constructor performance visualization.
