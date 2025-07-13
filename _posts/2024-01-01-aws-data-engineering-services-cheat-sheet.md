---
layout: post
title: "AWS Data Engineering Services - Quick Reference Cheat Sheet"
date: 2024-01-01
categories: [aws, data-engineering, cheat-sheet]
tags: [aws, data, engineering, kinesis, glue, redshift, athena]
---

# AWS Data Engineering Services - Quick Reference Cheat Sheet

## Data Ingestion Services

### Amazon Kinesis Family
| Service | Use Case | Key Features | Limits |
|---------|----------|--------------|---------|
| **Kinesis Data Streams** | Real-time streaming | • Custom consumer apps<br>• Replay capability<br>• Low latency (< 1 second) | • 1MB record limit<br>• 1000 records/sec per shard |
| **Kinesis Data Firehose** | Near real-time delivery | • Serverless<br>• Built-in transformation<br>• Direct S3/Redshift delivery | • 60 second buffer minimum<br>• No replay capability |
| **Kinesis Analytics** | Real-time analytics | • SQL on streaming data<br>• Anomaly detection<br>• Time-windowed queries | • SQL-based processing only |

### AWS Glue
| Component | Purpose | Key Points |
|-----------|---------|------------|
| **Glue Crawlers** | Schema discovery | • Auto-detect schema changes<br>• Populate Data Catalog<br>• Schedule-based or on-demand |
| **Glue ETL Jobs** | Data transformation | • Serverless Spark<br>• Auto-scaling<br>• Built-in retry logic |
| **Glue Data Catalog** | Metadata repository | • Hive-compatible metastore<br>• Integration with Athena/EMR<br>• Schema versioning |
| **Glue DataBrew** | Visual data preparation | • No-code transformations<br>• Data profiling<br>• 250+ built-in transformations |

## Data Storage Services