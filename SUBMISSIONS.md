operation: https://github.com/Release-Engineering-4/operation

model training: https://github.com/Release-Engineering-4/model-training

model service: https://github.com/Release-Engineering-4/model-service

lib-ml: https://github.com/Release-Engineering-4/lib-ml

lib-version: https://github.com/Release-Engineering-4/lib-version

app: https://github.com/Release-Engineering-4/app

## Comments for A1:

We implemented a pylint auditor with the dslinter plugin and set it up in a GitHub Actions workflow with a 90% threshold. We orgnized the project to follow the cookie cutter structure and split the code accordingly. Added DVC for pipeline management and metric reporting.

## Comments for A2:

Implemented the basics for the `model-training`, `lib-ml`, `lib-version`, `model-service` and `app` repositories.

## Comments for A3:

Added vagrant Kubernetes playbook. Migrated the Docker containerisation to Kubernetes. Added monitoring with Prometheus.