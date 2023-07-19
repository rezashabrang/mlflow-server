# MLflow Server

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

This repository contains a sample MLflow server setup that demonstrates how to deploy an MLflow server to manage and track machine learning experiments.

## Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

## Overview

MLflow is an open-source platform to manage the machine learning lifecycle, including experimentation, reproducibility, deployment, and sharing of models. This repository provides a sample setup for running an MLflow server, which allows you to track and compare experiments, and manage your machine learning models.

The MLflow server can be accessed through a web interface or programmatically via a REST API. It provides features like experiment tracking, model versioning, and model deployment.

## Prerequisites

Before getting started, make sure you have the following installed:

- Python 3.x
- MLflow (`pip install mlflow`)
- Docker
- Docker Compose

## Installation

1. Clone this repository to your local machine:

```
git clone https://github.com/rezashabrang/mlflow-server.git
cd mlflow-server
```

2. Build MLFlow server image:

```
docker-compose build
```

## Usage

### Starting the MLflow Server

To start the MLflow server, first create a `.env` file with `.env.example.` file structure.

Here is an example:

```
POSTGRES_USER=user
POSTGRES_PASSWORD=password
POSTGRES_DB=db
POSTGRES_PORT=5432
PGADMIN_DEFAULT_PASSWORD=password
MLFLOW_HOST=0.0.0.0
MLFLOW_WORKERS=1
MLFLOW_DEFAULT_ARTIFACT_ROOT=
MLFLOW_BACKEND_STORE_URI=postgresql://${POSTGRES_USER}:${POSTGRES_PASSWORD}@mlflow-postgres:${POSTGRES_PORT}/${POSTGRES_DB}
MLFLOW_GUNICORN_OPTS=--log-level debug
MLFLOW_SERVE_ARTIFACTS=true
MLFLOW_ARTIFACTS_DESTINATION=/arts
```

Then run the containers using docker-compose.

```
docker-compose up -d
```

This will start the server locally, and you can access the web interface by navigating to `http://localhost:5000` in your web browser.

### Running Experiments

You can use the MLflow Python library to track your machine learning experiments. For example:

```python
import mlflow
mlflow.set_tracking_uri("http://localhost:5000")  # If the path differs change here


# Start an MLflow run
with mlflow.start_run():
    # Your training and evaluation code here
    # ...

    # Log metrics, parameters, and artifacts
    mlflow.log_param("learning_rate", 0.01)
    mlflow.log_metric("accuracy", 0.85)
    mlflow.log_artifact("model.pkl")
```

### Deploying Models

Once you have trained a model and logged it as an artifact in MLflow, you can deploy it using the MLflow REST API or the web interface. MLflow supports various deployment options, including serving models with REST API endpoints and containerized deployments.

For more information on deploying models, refer to the [MLflow documentation](https://www.mlflow.org/docs/latest/models.html#deploy-a-model).

## Contributing

Contributions are welcome! If you find any issues or have suggestions for improvement, please open an issue or a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

Happy modeling and experiment tracking with MLflow! If you have any questions or need further assistance, feel free to ask. Good luck with your MLflow server repository!