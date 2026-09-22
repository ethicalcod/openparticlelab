# Resource Strategy

## Local Development

The local machine is the primary development environment.

Local resources should be used for:

- Django development
- React development
- MySQL development
- API testing
- unit tests
- documentation
- small datasets

## Heavy Computation

Large or memory-intensive workloads should be executed on:

- Kaggle
- Google Colab

## Persistence

Long-running computational workflows must save recoverable
intermediate results where practical.

Important artifacts should be persisted outside temporary notebook
sessions.

## Git Policy

GitHub stores:

- source code
- configuration
- documentation
- small sample data
- tests

GitHub should not store:

- large raw datasets
- large processed datasets
- model checkpoints
- temporary experiment files

## Reproducibility

Heavy experiments should record:

- input data/version
- code commit
- configuration
- environment information
- output location
- execution status

## Recovery Principle

A temporary compute environment must never be the only location
containing important project state.
