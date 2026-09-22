# OpenParticleLab Project Specification

## 1. Purpose

OpenParticleLab is an independent scientific software project designed
to provide an interactive platform for exploring, analysing and
reproducing computational experiments using public scientific datasets.

The initial implementation will use CERN Open Data as a scientific data
source.

## 2. Primary Objective

The project aims to demonstrate practical understanding of:

- Python software development
- backend architecture
- REST API design
- relational database design
- scientific data processing
- frontend engineering
- data visualization
- reproducible computation
- testing
- containerization
- CI/CD

## 3. Core Workflow

User
    
Dataset discovery
    
Dataset selection
    
Dataset metadata
    
Analysis configuration
    
Scientific computation
    
Result generation
    
Visualization
  
Analysis persistence
    
Reproduction

## 4. Core Entities

- User
- Experiment
- Dataset
- DatasetVersion
- DatasetFile
- Analysis
- AnalysisParameter
- AnalysisResult
- ExecutionJob

## 5. Initial Analysis Capabilities

The first release will support:

- descriptive statistics
- distributions
- histograms
- correlations
- dataset comparison

## 6. Reproducibility

Each analysis should record:

- dataset
- dataset version
- dataset checksum where applicable
- selected variables
- filters
- analysis parameters
- software version
- execution timestamp
- execution duration

## 7. Resource Constraints

The local development machine has limited CPU,
RAM and storage.

Therefore:

- development should remain lightweight
- large datasets must not be stored locally unnecessarily
- large computations should use Kaggle or Google Colab
- important computational artifacts should be persisted externally
- source code must remain in Git
- computational checkpoints should be recoverable
- datasets must not be committed to Git unnecessarily

## 8. Development Environments

### Local

Used for:

- application development
- database development
- frontend development
- testing
- documentation

### Kaggle / Google Colab

Used for:

- large scientific data processing
- expensive experiments
- performance benchmarks
- memory-intensive operations

### Persistent Artifact Storage

Used for:

- checkpoints
- large processed artifacts
- experiment outputs

## 9. Non-Goals

The initial project will not attempt to:

- reproduce the complete CERN Open Data portal
- process CERN's entire data archive
- implement a production-scale distributed computing platform
- build a particle-physics reconstruction framework
- create a production CERN service

## 10. Project Identity

OpenParticleLab is an independent educational and research-software
project. It is not affiliated with CERN.
