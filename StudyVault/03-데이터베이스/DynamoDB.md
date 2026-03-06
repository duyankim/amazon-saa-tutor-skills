---
source_pdf: saa_questions.json
part: "03"
keywords: dynamodb, nosql, partition-key, global-tables, dax, streams
---

# DynamoDB (★★★)

#aws-saa #database

## Overview Table

| 항목 | 값 |
|------|-----|
| 유형 | 키-값 / 문서 NoSQL |
| 지연시간 | 단일 자리 밀리초 |
| 운영 | 완전 서버리스 |
| 용량 모드 | Provisioned / On-Demand |
| 최대 항목 크기 | 400KB |

---

## 용량 모드 비교

| 모드 | 특징 | 사용 케이스 |
|------|------|------------|
| **Provisioned** | RCU/WCU 지정 + Auto Scaling | 예측 가능한 트래픽 |
| **On-Demand** | 자동 스케일, 더 비쌈 | 예측 불가/스파이크 트래픽 |

---

## DynamoDB Accelerator (DAX)

```
애플리케이션 → DAX 클러스터 → DynamoDB
              (마이크로초 캐시)
```

- DynamoDB 전용 인메모리 캐시
- 읽기 지연: 밀리초 → **마이크로초**
- 쓰기는 DynamoDB 직접 통과

> [!warning] DAX vs ElastiCache
> DAX: DynamoDB 전용 / ElastiCache: 범용 (RDS, 애플리케이션 등)

---

## DynamoDB Streams

- 항목 변경 시 스트림 이벤트 발생
- 최대 24시간 보존
- **Lambda 트리거**와 연동 → 실시간 처리

```
DynamoDB PUT/UPDATE/DELETE
    → DynamoDB Streams
        → Lambda → 다운스트림 처리
```

---

## DynamoDB Global Tables

- **멀티 리전 액티브-액티브** 복제
- 각 리전에서 읽기/쓰기 가능
- 자동 충돌 해결 (Last-writer-wins)
- 전제: **DynamoDB Streams 활성화 필수**

---

## 인덱스

| 인덱스 | 키 | 생성 시점 | 제한 |
|--------|-----|---------|------|
| **GSI** (Global Secondary Index) | 다른 파티션 키 | 생성 후 추가 가능 | 별도 RCU/WCU |
| **LSI** (Local Secondary Index) | 같은 파티션 키 | **테이블 생성 시만** | 동일 파티션 내 |

---

## Exam/Test Patterns

| 시나리오/키워드 | 답 |
|----------------|-----|
| "서버리스 키-값 단일 ms" | **DynamoDB** |
| "DynamoDB 마이크로초 캐시" | **DAX** |
| "멀티 리전 액티브-액티브" | **DynamoDB Global Tables** |
| "변경 이벤트 실시간 처리" | **DynamoDB Streams + Lambda** |
| "예측 불가 스파이크 트래픽" | **On-Demand 모드** |
| "다른 속성으로 쿼리" | **GSI** |

## Related Notes
- [[RDS와 Aurora]]
- [[ElastiCache]]
- [[Lambda와 서버리스]]
- [[데이터베이스 문제풀이]]
