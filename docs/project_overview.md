# Project Overview — BioSignal AI Health Analytics Demo

This public repo showcases the **data & analytics layer** for Apple Health:
- **Input:** Health Auto Export JSON (local only, user-owned).
- **Transform:** Python standardizes to `_time`, `_metric`, `value`, `unit`, `source`.
- **Store:** InfluxDB bucket `health` (InfluxDB 2.x).
- **Viz:** Grafana dashboards (HRV, Resting HR, Steps shown here as images).

> Ops, Docker, Home Assistant, MQTT, Frigate, and any passwords/tokens live in a **private repository**.

---

## Data model (tidy)
| column        | type        | notes                                  |
|---------------|-------------|----------------------------------------|
| `_time`       | timestamp   | RFC3339                                 |
| `_metric`     | string      | e.g., `hrv_sdnn`, `resting_heart_rate` |
| `value`       | float       | numeric value                           |
| `unit`        | string      | `ms`, `bpm`, `count`, `km`, etc.       |
| `source`      | string      | device/app tag                          |

---

## Current panels
- **HRV SDNN** (ms) — variability proxy, recovery/stress signal.
- **Resting Heart Rate** (bpm) — baseline load & readiness.
- **Daily Steps** — activity context.
- **7-day mean HRV** — smoothed trend.

See `/assets/*.png` in repo for examples.

---

## AI/ML roadmap (condensed)
**Descriptive**
- Metric coverage scan, data quality checks, missingness heatmaps.
- Rolling stats (7/30-day), weekly seasonality, weekend effects.

**Predictive**
- Forecasts (Prophet/ARIMA as baselines).
- Gradient boosting models for HRV/RHR with feature contributions.

**Anomaly detection**
- STL residual-based outliers (per-metric).
- HRV-RHR joint anomalies (possible infection/overreaching flags).

**Prescriptive**
- Rule-guided tips + LLM narrative tied to the timeseries facts.

**Personalization**
- Bayesian priors updated per user over time.

---

## Privacy & security
- No PHI or tokens committed.
- All exports remain local; uploads are at the user’s discretion.
- Production secrets and infra are private by design.

---

## What’s next
- Add sleep & workout intensity.
- Add readiness score prototype (transparent formula + ML variant).
- Publish a demo notebook that trains a simple forecaster and renders a Grafana snapshot.
