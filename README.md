# BioSignal AI — Apple Health Analytics Demo

Open-source demo that ingests Apple Health (Health Auto Export) data, organizes it with Python, stores it in InfluxDB, and visualizes key metrics in Grafana.  
**Focus:** practical biosignal analytics + an AI roadmap that moves from descriptive dashboards to predictive, personalized insights.

---

## What’s in this repo
- **Notebooks & scripts** to normalize Apple Health JSON into tidy time series.
- **Exported charts** (HRV, Resting HR, Steps) you can view right here.
- **Docs** explaining the pipeline and the AI roadmap.

> Production infra (compose files, secrets, HA/Frigate, etc.) lives in a **private** repo. This public repo is safe to share—no secrets.

---

## Quick look (sample outputs)

<p align="center">
  <img src="assets/HRV_SDNN.png" width="45%" />
  <img src="assets/Resting_Heart_Rate.png" width="45%" />
</p>
<p align="center">
  <img src="assets/Daily_Steps.png" width="45%" />
  <img src="assets/HRV_7_Dsy_Mean.png" width="45%" />
</p>

---

## Pipeline (high level)

1. **Export** Apple Health using *Health Auto Export* (JSON).
2. **Normalize** with Python → tidy dataframe: `_time`, `_metric`, `value`, and tags (e.g., source, unit).
3. **Store** in InfluxDB (bucket: `health`).
4. **Visualize** in Grafana (Panels for HRV, Resting HR, Steps).
5. **Roadmap to AI** (see below) for anomaly detection, forecasting, and personal coaching.

> Detailed overview: [`docs/project_overview.md`](docs/project_overview.md)

---

## Why this matters
- **HRV** reflects autonomic balance, stress, and recovery readiness.
- **Resting HR** summarizes baseline cardiovascular load.
- **Steps & Distance** add context for training load and recovery.

Combining these with sleep and activity intensity enables **AI-assisted guidance**: readiness scores, recovery recommendations, and early warning for overtraining or illness.

---

## AI & ML Roadmap (short)
- **Phase 1 (descriptive):** metric QA, gaps, and trend enrichment (7-/30-day baselines).
- **Phase 2 (predictive):** 
  - Classical: ARIMA/Prophet/ETS baselines for HRV & RHR.
  - ML: Gradient boosting for next-day RHR/HRV + feature importances.
  - **Anomaly detection** (robust z-scores / STL residuals).
- **Phase 3 (prescriptive + LLM):**
  - Rule-enhanced recommendations (sleep, hydration, deload).
  - LLM-based narrative insights using structured facts from the timeseries.
- **Phase 4 (personalization):** user-specific priors and Bayesian updating.

Full details: [`docs/upwork_project.md`](docs/upwork_project.md)

---

## Run it yourself (summary)
- Export JSON from Health Auto Export.
- Use the provided notebook/script to tidy & write to InfluxDB.
- Connect Grafana → InfluxDB (URL, org, bucket, token).
- Import example panels and start iterating.

> We keep deploy specifics in a separate private repo to avoid exposing secrets.

---

## License
MIT
