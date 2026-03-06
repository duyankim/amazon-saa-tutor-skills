---
source_pdf: saa_questions.json
part: "07"
keywords: opensearch, elasticsearch, quicksight, spice, kibana, log-analysis
---

# OpenSearch와 QuickSight (★★)

#aws-saa #analytics

## OpenSearch (구 Elasticsearch)

```
로그/이벤트 데이터
     ↓ (Kinesis Firehose / Lambda)
[OpenSearch 클러스터]
     ↓
OpenSearch Dashboards (구 Kibana)
```

| 항목 | 설명 |
|------|------|
| 목적 | 전문 검색 + 로그 분석 |
| 쿼리 | OpenSearch DSL / SQL |
| 대시보드 | OpenSearch Dashboards (Kibana) |
| 통합 | Kinesis Firehose, CloudWatch Logs |

**주요 사용 케이스:**
- 애플리케이션 로그 검색/분석
- 전자상거래 제품 검색
- 보안 SIEM

---

## QuickSight

```
데이터 소스 (Redshift/Athena/S3/RDS)
     ↓
[QuickSight SPICE 캐시]
     ↓
시각화 대시보드 (웹/모바일)
```

| 항목 | 설명 |
|------|------|
| 목적 | BI 시각화/대시보드 |
| 캐시 | **SPICE** (인메모리 가속 엔진) |
| 과금 | 사용자/세션 기반 |
| ML 통합 | 이상 탐지, 예측 |

> [!tip] QuickSight Q
> 자연어로 데이터 질문 → 자동 시각화 (ML Powered)

---

## Exam/Test Patterns

| 시나리오/키워드 | 답 |
|----------------|-----|
| "로그 실시간 검색/분석" | **OpenSearch** |
| "Kibana 대시보드 AWS" | **OpenSearch Dashboards** |
| "비즈니스 BI 대시보드" | **QuickSight** |
| "Athena/Redshift 시각화" | **QuickSight** |
| "빠른 쿼리 캐싱 엔진" | **QuickSight SPICE** |

## Related Notes
- [[Athena와 Glue]]
- [[Kinesis]]
- [[분석 문제풀이]]
