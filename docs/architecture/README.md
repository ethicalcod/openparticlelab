# OpenParticleLab Architecture

## 1. Overview

OpenParticleLab is an independent scientific data exploration and reproducibility platform.

The system is designed to allow users to:

1. discover scientific datasets
2. inspect dataset metadata
3. select a specific dataset version
4. configure an analysis
5. execute scientific computations
6. inspect generated results
7. visualize results
8. preserve analysis provenance
9. reproduce previous analyses

The initial scientific data source is CERN Open Data.

> OpenParticleLab is an independent project and is not affiliated with or endorsed by CERN.

---

## 2. Architectural Style

OpenParticleLab uses a layered web application architecture.

```text
React + TypeScript
        |
        | HTTP / JSON
        |
Django REST Framework
        |
        +-------------------+
        |                   |
        v                   v
     MySQL          Scientific Analysis
     Database             Engine
                            |
                            v
                    Scientific Datasets
```

The initial implementation is intentionally modular so that asynchronous
processing can be introduced later without redesigning the entire system.

---

## 3. Frontend

Technology:

* React
* TypeScript
* Vite

Responsibilities:

* dataset discovery
* dataset metadata display
* analysis configuration
* visualization
* analysis history
* result inspection
* reproducibility information

The frontend communicates with the backend exclusively through the REST API.

---

## 4. Backend

Technology:

* Python
* Django
* Django REST Framework

Responsibilities:

* authentication
* dataset metadata management
* dataset version management
* analysis configuration
* analysis execution
* result persistence
* provenance tracking
* REST API
* validation
* business logic

The backend is responsible for coordinating scientific computation rather than placing scientific processing logic directly inside API views.

---

## 5. Database

Technology:

* MySQL

The database stores application metadata rather than large scientific datasets.

Examples of stored information:

* users
* datasets
* dataset versions
* dataset files
* analyses
* analysis parameters
* analysis results
* execution jobs

Large scientific files should not be stored directly inside MySQL.

---

## 6. Scientific Analysis Layer

The scientific analysis layer uses Python scientific libraries.

Initial libraries:

* NumPy
* Pandas
* SciPy
* PyArrow

Initial analyses:

* descriptive statistics
* distributions
* histograms
* correlations
* dataset comparison

Scientific computation should be separated from HTTP request handling.

---

## 7. Dataset Provenance

A dataset is treated as a logical scientific resource.

A dataset may have multiple versions.

An analysis references a specific dataset version rather than only the logical dataset.

This is important for reproducibility.

```text
Dataset
   |
   +-- DatasetVersion 1
   |
   +-- DatasetVersion 2
   |
   +-- DatasetVersion 3
                |
                +-- Analysis
```

An analysis performed against DatasetVersion 2 must remain associated with DatasetVersion 2 even if DatasetVersion 3 later becomes available.

---

## 8. Asynchronous Processing

The initial version may execute small analyses synchronously.

Future versions will support:

```text
Django API
    |
    v
Celery
    |
    v
Redis
    |
    v
Analysis Worker
```

This allows long-running scientific analyses to execute independently from HTTP requests.

---

## 9. External Scientific Data

OpenParticleLab initially integrates with CERN Open Data.

The application should store metadata and references to external scientific resources whenever practical rather than downloading entire datasets unnecessarily.

Large scientific datasets should be processed using external compute resources such as Kaggle or Google Colab when required.

---

## 10. Resource-Conscious Design

The local development computer has limited CPU, RAM and storage.

Therefore:

* the local machine is primarily a development environment
* large datasets should not be stored locally unnecessarily
* large scientific computations should use Kaggle or Google Colab
* large artifacts should be persisted externally
* MySQL should contain metadata rather than raw scientific datasets
* frontend and backend development should remain lightweight
* expensive processing should support checkpointing where practical

The project should avoid unnecessary background services during early development.

---

## 11. Security Boundary

The frontend must never connect directly to MySQL.

The communication path is:

```text
React
  |
  v
Django REST API
  |
  v
MySQL
```

Database credentials are stored in environment variables and must never be committed to Git.

---

## 12. Initial Deployment Model

During development:

```text
Browser
   |
   v
React development server
   |
   v
Django development server
   |
   v
MySQL
```

Production deployment will be designed later.

---

## 13. Future Architecture

The long-term architecture may become:

```text
                    ┌─────────────────┐
                    │ React / TS      │
                    └────────┬────────┘
                             │
                                           ▼
                    ┌─────────────────┐
                    │ Django REST API │
                    └────────┬────────┘
                             │
              ┌──────────────┼──────────────┐
              │              │              │
                     ▼                    ▼                    ▼
           MySQL          Redis          Dataset
                             │           Services
                                           ▼
                          Celery
                             │
                                           ▼
                    Scientific Workers
                             │
                                           ▼
                    Analysis Artifacts
```

The architecture will evolve incrementally through project releases.

---

## 14. Design Principle

The primary architectural principle is:

> Separate scientific computation, application logic, persistence, and presentation while maintaining enough provenance to reproduce an analysis.

