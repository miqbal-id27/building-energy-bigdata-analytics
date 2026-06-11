# Building Energy Prediction and Real-Time Streaming Portfolio

## Executive Summary

This portfolio demonstrates an end-to-end big data pipeline for building energy analytics. The project starts with batch preprocessing using PySpark to clean, join, and transform building, meter, and weather datasets into six-hour energy features. A Gradient-Boosted Tree model is then trained to predict building energy consumption and evaluated against alternative approaches. The real-time section simulates weather data production using Kafka, ingests the stream with Spark Structured Streaming, enriches it with static building metadata, applies the trained model, and writes prediction outputs to Parquet and Kafka topics. Finally, Kafka consumers visualize live prediction trends, energy aggregation, and daily shortfall or excess energy. Overall, it shows practical capability in PySpark, Kafka, streaming architecture, machine learning, and real-time operational monitoring.

## End-to-End Big Data and Real-Time Architecture

```mermaid
flowchart LR
    A[Raw datasets<br/>Building + meter + weather] --> B[PySpark batch preprocessing]
    B --> C[Feature engineering<br/>6-hour energy + weather aggregation]
    C --> D[Model training<br/>GBT energy prediction model]
    D --> E[Saved ML pipeline model]

    F[Simulated weather records<br/>every 5 seconds] --> G[Kafka topic<br/>weather5s]
    G --> H[Spark Structured Streaming]
    H --> I[Streaming enrichment<br/>schema + static joins + feature preparation]
    E --> J[Real-time prediction]
    I --> J
    J --> K[Streaming Parquet outputs]
    J --> L[Kafka output topics<br/>predictions5s + energyagg7s + dailyenergy14s]
    L --> M[Kafka consumers]
    M --> N[Real-time visualization<br/>prediction trend + aggregation + shortfall/excess]

```

## Batch Processing and Model Development

```mermaid
flowchart TD
    A[Load historical data] --> B[Define schema]
    B --> C[Clean and transform data]
    C --> D[Impute missing weather values]
    D --> E[Aggregate meter data into energy_6h]
    E --> F[Join building, meter, and weather features]
    F --> G[EDA and feature selection]
    G --> H[Train and compare ML models]
    H --> I[Save best model for streaming inference]

```

## Real-Time Streaming and Visualization

```mermaid
sequenceDiagram
    participant P as Kafka Producer
    participant K as Kafka Topic: weather5s
    participant S as Spark Structured Streaming
    participant M as Saved GBT Model
    participant O as Kafka/Parquet Outputs
    participant V as Visualization Consumer

    P->>K: Publish simulated weather batch
    K->>S: Stream records
    S->>S: Parse schema + join static building data
    S->>M: Apply trained model
    M-->>S: Return energy prediction
    S->>O: Write predictions and aggregations
    O->>V: Consume live outputs
    V->>V: Plot real-time trend and shortfall/excess

```

## Files Structure

```text
building-energy-realtime-portfolio/
├── README.md
├── LICENSE
├── .gitignore
├── requirements.txt
├── notebooks/
│   ├── 01_data_preprocessing.ipynb
│   ├── 02_building_energy_prediction_model.ipynb
│   ├── 03a_produce_streaming_data.ipynb
│   ├── 03b_stream_predict_realtime_data.ipynb
│   └── 03c_realtime_visualization.ipynb
├── docs/
│   ├── index.html
│   ├── .nojekyll
│   └── notebooks/
│       ├── 01_data_preprocessing.html
│       ├── 02_building_energy_prediction_model.html
│       ├── 03a_produce_streaming_data.html
│       ├── 03b_stream_predict_realtime_data.html
│       └── 03c_realtime_visualization.html
├── src/
├── data/
├── models/
├── outputs/
└── checkpoints/
```

## Project Components

| Step | Notebook | Purpose | Portfolio View |
|---|---|---|---|
| 1 | `01_data_preprocessing.ipynb` | Batch preprocessing and Spark-based analysis | `docs/notebooks/01_data_preprocessing.html` |
| 2 | `02_building_energy_prediction_model.ipynb` | Feature engineering, EDA, model training, and evaluation | `docs/notebooks/02_building_energy_prediction_model.html` |
| 3A | `03a_produce_streaming_data.ipynb` | Simulate and publish weather records to Kafka | `docs/notebooks/03a_produce_streaming_data.html` |
| 3B | `03b_stream_predict_realtime_data.ipynb` | Consume Kafka stream, process features, predict, and output streams | `docs/notebooks/03b_stream_predict_realtime_data.html` |
| 3C | `03c_realtime_visualization.ipynb` | Consume prediction topics and visualize results in real time | `docs/notebooks/03c_realtime_visualization.html` |

## Tech Stack

Python · PySpark · Spark SQL · Spark Structured Streaming · Kafka · Machine Learning · Parquet · 
