---
source_pdf: saa_questions.json
part: "06"
keywords: kinesis, data-streams, firehose, analytics, shard, real-time
---

# Kinesis (★★★)

#aws-saa #integration

## Kinesis 제품군 비교

| 제품 | 목적 | 관리 | 목적지 |
|------|------|------|--------|
| **Data Streams** | 실시간 스트리밍 | 직접 관리 | Lambda/EC2/KDA |
| **Data Firehose** | ETL 완전 관리형 | AWS 관리 | S3/Redshift/OpenSearch |
| **Data Analytics** | SQL 실시간 분석 | AWS 관리 | Streams/Firehose |
| **Video Streams** | 비디오 스트리밍 | AWS 관리 | ML/분석 |

---

## Kinesis Data Streams 핵심

```
Producer → Shard 1 → Consumer (Lambda/EC2)
         → Shard 2 → Consumer
         → Shard 3 → Consumer

처리량: 1MB/s 또는 1,000 레코드/s per Shard (쓰기)
        2MB/s per Shard (읽기)
보존:   기본 24시간 (최대 365일)
```

- **샤드 수 = 처리량 결정** (수동 리샤딩 또는 자동 스케일링)
- 순서 보장: 파티션 키 기준으로 동일 샤드 내

---

## Kinesis Data Firehose

```
소스 (Streams/IoT/CloudWatch)
     ↓
[Firehose] (버퍼링, 변환, 압축)
     ↓
S3 / Redshift / OpenSearch / HTTP Endpoint
```

- **완전 관리형** (샤드/컨슈머 관리 불필요)
- 최소 60초 또는 1MB 버퍼 후 전달
- Lambda로 실시간 데이터 변환 가능

---

## SQS vs Kinesis 비교

| 항목 | SQS | Kinesis Data Streams |
|------|-----|---------------------|
| 목적 | 메시지 큐 (디커플링) | 실시간 스트리밍 |
| 소비 | 메시지 삭제 후 소비 | 여러 컨슈머 독립 소비 |
| 순서 | FIFO만 보장 | 파티션 키 내 순서 |
| 보존 | 최대 14일 | 최대 365일 |
| 처리량 | 무제한 | 샤드 단위 제한 |
| 실시간 | 준실시간 | **진실시간** |

---

## Exam/Test Patterns

| 시나리오/키워드 | 답 |
|----------------|-----|
| "실시간 클릭스트림 분석" | **Kinesis Data Streams** |
| "S3로 자동 스트리밍 적재" | **Kinesis Data Firehose** |
| "스트림 SQL 실시간 집계" | **Kinesis Data Analytics** |
| "여러 앱이 같은 스트림 소비" | **Kinesis Data Streams** |
| "IoT 데이터 → Redshift 자동 적재" | **Kinesis Firehose** |

## Related Notes
- [[SQS와 SNS]]
- [[Athena와 Glue]]
- [[애플리케이션통합 문제풀이]]
