# Carbon Intensity Forecasting API

A lightweight **carbon intensity forecasting REST API** for the **North Italy (IT-NO) electricity zone**. It serves hourly forecasts of grid carbon intensity in **gCO₂eq/kWh** using a pre-trained [Facebook Prophet](https://facebook.github.io/prophet/) time-series model, exposed through a [FastAPI](https://fastapi.tiangolo.com/) service.

The forecasts are intended to support **carbon-aware and energy-efficient computing** decisions — for example, shifting workloads across the cloud–edge–HPC continuum to hours when the electricity grid is cleaner (lower carbon intensity).

## Role in the DECICE project

This repository is part of the **green / energy-efficient computing** work of the **DECICE** project — *Device-Edge-Cloud Intelligent Collaboration framEwork* — an **EU Horizon Europe** Research and Innovation Action (Grant Agreement No. **101092582**, call HORIZON-CL4-2022-DATA-01-02).

DECICE builds an AI-driven framework for optimising the placement and scheduling of workloads across the heterogeneous **cloud, edge and HPC** compute continuum, with **energy efficiency and sustainability** as first-class goals. Carbon-intensity forecasting like the API in this repository provides a signal that carbon-aware schedulers can use to reduce the CO₂ footprint of computing.

## What it does

- Loads a pre-trained Prophet model (`app/prophet_model.pkl`).
- Predicts hourly carbon intensity (`ci`, in gCO₂eq/kWh) with an associated `timestamp`.
- Returns forecasts as JSON for a fixed horizon (day / week / month) or an arbitrary date range.

## Endpoints

| Method | Path | Description |
|--------|------|-------------|
| `GET`  | `/` | Health check — confirms the API is running. |
| `GET`  | `/predictday` | Forecast carbon intensity for the next 24 hours. |
| `GET`  | `/predictweek` | Forecast carbon intensity for the next 7 days (168 hours). |
| `GET`  | `/predictmonth` | Forecast carbon intensity for the next 30 days (720 hours). |
| `GET`  | `/predictrange` | Forecast carbon intensity for a custom date range (`start`, `end` query parameters). |

### Example

```
GET /predictrange?start=2025-08-01T00:00:00&end=2025-08-07T23:00:00
```

Each response is a list of records shaped like:

```json
[{"timestamp": "2025-08-01T00:00:00", "ci": 210.4}, ...]
```

where `ci` is the forecasted carbon intensity in gCO₂eq/kWh.

## Quick start

Interactive API docs are available at `http://localhost:8000/docs` (Swagger UI) once the server is running.

### Run with Docker

```
docker build -t decicegreencomputing .
docker run -p 8000:8000 decicegreencomputing
```

### Run locally

```
pip install -r requirements.txt
uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

## How the model is built

The model is a [Prophet](https://facebook.github.io/prophet/) forecaster with yearly, weekly and daily seasonality, trained on hourly historical carbon-intensity data for the **IT-NO (North Italy)** zone spanning **2021–2024** (`app/dataset/IT-NO_<year>_hourly.csv`). Retraining is done with:

```
python app/train_model.py
```

which reads the CSV history, fits the Prophet model and writes `prophet_model.pkl`.

## Tech stack

- **Python 3.12**
- **FastAPI** + **Uvicorn** — web framework and ASGI server
- **Prophet** — time-series forecasting
- **pandas**, **NumPy**, **scikit-learn**, **matplotlib** — data handling and analysis
- **Docker** — containerised deployment

## Acknowledgement

This work was carried out in the context of the **DECICE** project, which has received funding from the **European Union's Horizon Europe** research and innovation programme under **Grant Agreement No. 101092582**.

## License

License deferred — this is EU-project (DECICE), institutional / collaborative work; licensing to be decided by the project and repository owner.

<!-- legal-notice: start -->
### Legal notice and responsible use

The materials in this repository are made available without warranties to the extent permitted by applicable law. **Please read the [Disclaimer and Responsible-Use Notice](DISCLAIMER.md)** before relying on or deploying them. This notice does not change any existing software license or limit rights that cannot legally be waived.
<!-- legal-notice: end -->

<!-- risk-guidance: start -->
### Operational safety and limitations

Before connecting accounts, running automation, relying on consequential outputs, or using production systems, review [project-specific safety risks and pre-deployment checks](SAFETY.md). The checklist describes precautions to **verify**, not a certification that the software currently enforces every safeguard.
<!-- risk-guidance: end -->

<!-- licensing-status: start -->
### Licensing and reuse status

**No repository-root license has yet been confirmed for this project.** Read [Rights and Licensing Status](LICENSING_STATUS.md) before copying, redistributing, or adapting code or content. A public repository and its disclaimer do not by themselves grant new reuse permissions. Existing valid third-party rights and licenses remain in effect.
<!-- licensing-status: end -->
