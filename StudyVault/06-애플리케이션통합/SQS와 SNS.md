---
source_pdf: saa_questions.json
part: "06"
keywords: sqs, sns, fanout, dlq, fifo, pub-sub, decoupling
---

# SQS와 SNS (★★★)

#aws-saa #integration

## Overview Table

| 항목 | SQS | SNS |
|------|-----|-----|
| 패턴 | 큐 (Pull) | Pub/Sub (Push) |
| 소비자 | 1개 (또는 여러 인스턴스가 경쟁) | 다수 구독자 동시 |
| 보존 | 최대 14일 | 저장 없음 |
| 순서 | Standard: 없음 / FIFO: 보장 | - |
| 재시도 | DLQ로 실패 메시지 격리 | 재시도 정책 |

---

## SQS 큐 유형

| 항목 | Standard | FIFO |
|------|----------|------|
| 순서 | 보장 없음 | **엄격한 순서** |
| 처리 | At-least-once | **Exactly-once** |
| 처리량 | 무제한 | 300 TPS (배치 3,000) |
| 이름 | - | `.fifo` 접미사 필수 |

---

## SQS 핵심 설정

```
Visibility Timeout: 메시지 처리 중 숨김 시간 (기본 30초)
Message Retention:  1분 ~ 14일 (기본 4일)
Delay Queue:        메시지 전달 지연 (최대 15분)
Long Polling:       빈 응답 감소, 비용 절감 (최대 20초)
DLQ:               maxReceiveCount 초과 시 메시지 이동
```

> [!warning] Visibility Timeout 설정
> 처리 시간보다 Visibility Timeout이 짧으면 동일 메시지 중복 처리 발생

---

## SNS 팬아웃 패턴

```
단일 이벤트 → 다수 대상 동시 전달:

이벤트 →  SNS Topic
            ├─ SQS Queue A → Worker A
            ├─ SQS Queue B → Worker B  ← 권장 패턴
            ├─ Lambda C
            └─ Email/SMS

(SNS → SQS → Lambda: 버퍼링 + 재처리 가능)
```

---

## SNS FIFO + SQS FIFO

- SNS FIFO → SQS FIFO: 순서 보장 팬아웃
- 금융 거래, 재고 업데이트 등 순서 중요한 이벤트

---

## Exam/Test Patterns

| 시나리오/키워드 | 답 |
|----------------|-----|
| "서비스 간 느슨한 결합" | **SQS** |
| "순서 보장 + Exactly-once" | **SQS FIFO** |
| "1 이벤트 → 다수 시스템 전파" | **SNS 팬아웃** |
| "처리 실패 메시지 격리" | **SQS DLQ** |
| "이메일/SMS 즉시 알림" | **SNS** |
| "S3 이벤트 → 여러 시스템" | **S3 → SNS → SQS × N** |

## Related Notes
- [[Kinesis]]
- [[EventBridge와 Step Functions]]
- [[Lambda와 서버리스]]
- [[애플리케이션통합 문제풀이]]
