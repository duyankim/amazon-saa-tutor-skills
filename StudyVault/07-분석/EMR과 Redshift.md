---
source_pdf: saa_questions.json
part: "07"
keywords: emr, redshift, hadoop, spark, data-warehouse, olap
---

# EMR과 Redshift (★★)

#aws-saa #analytics

## Overview Table

| 항목 | EMR | Redshift |
|------|-----|---------|
| 유형 | 관리형 Hadoop/Spark | 열 기반 데이터웨어하우스 |
| 관리 | EC2 클러스터 관리 | 관리형 (서버리스 옵션) |
| 프레임워크 | Hadoop/Spark/Hive/Presto | SQL (ANSI) |
| 사용 케이스 | 빅데이터 ETL/ML | OLAP 비즈니스 분석 |
| 과금 | EC2 + EMR 시간당 | 노드 시간당 |

---

## EMR 핵심

```
EMR Cluster:
  Master Node (클러스터 관리)
  Core Node   (데이터 저장 + 처리)
  Task Node   (처리만, 데이터 없음 — Spot 적합)

스토리지:
  HDFS (임시) / EMRFS (S3, 영구)
```

> [!tip] EMR 비용 최적화
> Task Node: **Spot Instance** 사용으로 비용 절감 (데이터 없으므로 중단 영향 최소)

---

## Redshift 핵심

```
Redshift Cluster:
  Leader Node → 쿼리 파싱/계획/조율
  Compute Nodes × N → 실제 데이터 저장/처리

Redshift Spectrum:
  Redshift → S3 외부 테이블 쿼리 (별도 클러스터 불필요)

Redshift Serverless:
  클러스터 없이 사용 (자동 스케일링)
```

| 기능 | 설명 |
|------|------|
| **열 기반 압축** | 분석 쿼리 I/O 최소화 |
| **MPP** | 대규모 병렬 처리 |
| **Spectrum** | S3 데이터 직접 쿼리 |
| **AQUA** | 분산 캐시 가속 |

---

## Exam/Test Patterns

| 시나리오/키워드 | 답 |
|----------------|-----|
| "Spark/Hadoop 커스텀 처리" | **EMR** |
| "페타바이트 BI/OLAP 쿼리" | **Redshift** |
| "S3 데이터 Redshift 없이 쿼리" | **Redshift Spectrum** |
| "EMR 비용 절감 Task 노드" | **Spot Instance** |
| "실시간 분석 대시보드" | **Redshift + QuickSight** |

## Related Notes
- [[Athena와 Glue]]
- [[OpenSearch와 QuickSight]]
- [[분석 문제풀이]]
