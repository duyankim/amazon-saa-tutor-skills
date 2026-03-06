---
source_pdf: saa_questions.json
part: "03"
keywords: elasticache, redis, memcached, caching, session-store
---

# ElastiCache (★★★)

#aws-saa #database

## Redis vs Memcached 비교

| 항목 | Redis | Memcached |
|------|-------|-----------|
| 다중 AZ | O (Replication) | X |
| 지속성 | O (RDB/AOF) | X |
| 데이터 구조 | 다양 (String/List/Set/ZSet/Hash) | String만 |
| Pub/Sub | O | X |
| 클러스터 모드 | O (샤딩) | O (멀티스레드) |
| 백업/복원 | O | X |
| 트랜잭션 | O | X |

> [!tip] Redis 선택 조건
> 다중 AZ / 지속성 / Pub-Sub / 리더보드(정렬셋) / 세션 관리 → **Redis**
> 단순 캐시 / 멀티스레드 / 지속성 불필요 → **Memcached**

---

## ElastiCache 사용 패턴

```
DB 읽기 가속화:
  애플리케이션 → ElastiCache (캐시 히트)
                          → RDS (캐시 미스)

세션 관리:
  EC2 인스턴스 A → ElastiCache (세션 공유)
  EC2 인스턴스 B ↗

리더보드:
  DynamoDB → DAX (DynamoDB 전용)
  RDS      → ElastiCache Redis (정렬셋)
```

---

## Redis Cluster Mode

| 모드 | 특징 |
|------|------|
| **Cluster Mode OFF** | 단일 샤드, 최대 5개 복제본 |
| **Cluster Mode ON** | 최대 500개 샤드, 수평 확장 |

---

## Exam/Test Patterns

| 시나리오/키워드 | 답 |
|----------------|-----|
| "DB 읽기 부하 감소, 캐시" | **ElastiCache** |
| "다중 AZ 캐시, 장애복구" | **ElastiCache Redis** |
| "세션 데이터 공유" | **ElastiCache Redis** |
| "리더보드/랭킹" | **ElastiCache Redis (Sorted Set)** |
| "단순 캐시, 멀티스레드" | **ElastiCache Memcached** |
| "DynamoDB 전용 마이크로초" | **DAX** (ElastiCache 아님) |

## Related Notes
- [[RDS와 Aurora]]
- [[DynamoDB]]
- [[데이터베이스 문제풀이]]
