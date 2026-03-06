---
source_pdf: saa_questions.json
part: "07"
keywords: athena, glue, serverless, etl, data-catalog, s3-query
---

# Athena와 Glue (★★★)

#aws-saa #analytics

## Overview Table

| 항목 | Athena | Glue |
|------|--------|------|
| 유형 | 서버리스 쿼리 | 서버리스 ETL |
| 입력 | S3 데이터 | 다양한 소스 |
| 언어 | SQL (Presto) | Python/Scala (Spark) |
| 과금 | 스캔 TB당 $5 | DPU 시간당 |
| 주요 용도 | 임시 분석 쿼리 | 데이터 파이프라인 |

---

## Athena 핵심

```
S3 데이터 (JSON/CSV/Parquet/ORC)
     ↓
[Athena 쿼리]  ← Glue Data Catalog (메타데이터)
     ↓
결과 → S3

비용 절감: Parquet/ORC 형식 + 파티셔닝으로 스캔량 감소
```

> [!tip] Athena 비용 최적화
> 컬럼형 포맷(Parquet/ORC) 사용 시 스캔량 90%+ 감소 → 비용 절감

---

## Glue 핵심 구성요소

| 구성요소 | 역할 |
|---------|------|
| **Data Catalog** | 메타데이터 저장소 (테이블 정의) |
| **Crawlers** | 데이터 소스 자동 스캔 → 카탈로그 업데이트 |
| **ETL Jobs** | 데이터 변환 코드 실행 |
| **Glue Studio** | 시각적 ETL 파이프라인 |
| **Glue DataBrew** | 코드 없는 데이터 정제 |

```
S3/RDS/Redshift
     ↓ Crawler 스캔
  Glue Data Catalog
     ↓ Athena/Redshift Spectrum이 참조
  ETL Job (변환)
     ↓
  S3 (정제된 데이터)
```

---

## Exam/Test Patterns

| 시나리오/키워드 | 답 |
|----------------|-----|
| "S3 로그 즉시 SQL 쿼리, 최소 운영" | **Athena** |
| "S3 데이터 변환 → Redshift 적재" | **Glue ETL** |
| "데이터 소스 자동 메타데이터 수집" | **Glue Crawler** |
| "Athena 테이블 정의 어디서?" | **Glue Data Catalog** |
| "S3에서 특정 컬럼만 저비용 쿼리" | **Athena + Parquet** |

## Related Notes
- [[EMR과 Redshift]]
- [[Kinesis]]
- [[S3 핵심 개념]]
- [[분석 문제풀이]]
