---
source_pdf: saa_questions.json
part: "03"
keywords: rds, aurora, multi-az, read-replica, failover, aurora-serverless
---

# RDS와 Aurora (★★★)

#aws-saa #database

## Overview Table

| 항목 | RDS | Aurora |
|------|-----|--------|
| 엔진 | MySQL/PostgreSQL/Oracle/MSSQL/MariaDB | MySQL/PostgreSQL 호환 |
| 성능 | 표준 | **5× MySQL, 3× PostgreSQL** |
| 복제본 | 최대 5 Read Replica | 최대 **15** Read Replica |
| 스토리지 | AZ별 | **3 AZ × 2 = 6개 복사본** |
| 장애복구 | 1~2분 | **30초 이내** |

---

## Multi-AZ vs Read Replica

```
                Multi-AZ (고가용성)
Primary ←→ Standby (동기 복제, 자동 장애조치)
                     ↕
              [동일 연결 엔드포인트 유지]

            Read Replica (성능/읽기 분산)
Primary → Replica1 (비동기, 별도 엔드포인트)
        → Replica2
        → Replica3 (다른 리전 가능 → 재해복구용)
```

| 항목 | Multi-AZ | Read Replica |
|------|----------|-------------|
| 목적 | **고가용성/장애복구** | **읽기 성능 향상** |
| 복제 | 동기 | 비동기 |
| 읽기 | Standby 읽기 불가 | 읽기 가능 |
| 장애조치 | 자동 | 수동 승격 |
| 과금 | 별도 인스턴스 비용 | 별도 인스턴스 비용 |

> [!warning] 자주 혼동하는 패턴
> "가용성 향상" → Multi-AZ / "읽기 성능 향상" → Read Replica
> Multi-AZ Standby는 읽기 트래픽 처리 불가 (대기 전용)

---

## Aurora 특징

```
Aurora Storage: 3 AZ에 걸쳐 6개 사본 자동 유지
Writer Endpoint: 항상 Primary 가리킴
Reader Endpoint: 읽기 부하 분산 (모든 Replica)
Custom Endpoint: 특정 Replica 그룹
```

### Aurora Serverless v2
- 0.5 ACU ~ 최대 ACU 자동 스케일링
- 간헐적/예측 불가 워크로드
- 유휴 시 최소 비용

### Aurora Global Database
- 기본 리전 1개 + 최대 5개 보조 리전
- 복제 지연 < 1초
- 재해복구 RTO < 1분

---

## RDS 백업

| 방법 | 보존 기간 | 특징 |
|------|----------|------|
| 자동 백업 | 1~35일 | PITR 지원 (5분 단위) |
| 수동 스냅샷 | 무기한 | 인스턴스 삭제 후에도 유지 |

---

## Exam/Test Patterns

| 시나리오/키워드 | 답 |
|----------------|-----|
| "DB 고가용성, 자동 장애조치" | **RDS Multi-AZ** |
| "읽기 트래픽 분산" | **Read Replica** |
| "고성능 MySQL 호환 관리형 DB" | **Amazon Aurora** |
| "간헐적 사용 DB 비용 최소화" | **Aurora Serverless** |
| "멀티 리전 DB, RPO~0" | **Aurora Global Database** |
| "데이터 복원 특정 시점" | **PITR (자동 백업)** |

## Related Notes
- [[DynamoDB]]
- [[ElastiCache]]
- [[고가용성과 재해복구 전략]]
- [[데이터베이스 문제풀이]]
