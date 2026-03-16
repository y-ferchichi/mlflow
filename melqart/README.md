# Melqart MLflow Tracker

Drop-in replacement for the default MLflow UI, optimized for RL workloads with thousands of metrics.

## The Problem

Default MLflow UI with 3000+ metrics (common in RL pretraining):
- **265 seconds** to load
- **964 MB** of API responses sent to browser
- **Browser crashes** trying to render 5.9M data points

## The Solution

Melqart Tracker with 3000+ metrics:
- **0.03 seconds** to load (9,904x faster)
- **2.2 MB** sent to browser (435x less data)
- **Works smoothly** — on-demand fetching, LTTB downsampling, lazy rendering

## What Changes

Only the frontend HTML file. The MLflow server, REST API, database, and artifact storage are untouched.

## Usage

### Docker (recommended)

```bash
docker build -f Dockerfile.melqart -t melqart-mlflow .
docker run -p 5000:5000 melqart-mlflow mlflow server --host 0.0.0.0
```

### Kubernetes / Helm

Change the image in your Helm values:

```yaml
image:
  repository: ghcr.io/yferc/mlflow-melqart  # was ghcr.io/mlflow/mlflow
  tag: "v2.21.3"                              # same version, optimized UI
```

Everything else stays the same — same command, same args, same database, same artifacts.

### Pre-built Image

```
ghcr.io/yferc/mlflow-melqart:v2.21.3
```

Built automatically on push via GitHub Actions.
