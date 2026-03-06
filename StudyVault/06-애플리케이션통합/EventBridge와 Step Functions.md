---
source_pdf: saa_questions.json
part: "06"
keywords: eventbridge, step-functions, workflow, event-bus, scheduler
---

# EventBridge와 Step Functions (★★)

#aws-saa #integration

## EventBridge 개요

```
이벤트 소스
├── AWS 서비스 (EC2 상태 변경, S3 이벤트 등)
├── SaaS 파트너 (Zendesk, Datadog 등)
└── 커스텀 앱
          ↓
    [EventBridge 이벤트 버스]
          ↓ (규칙 필터링)
    ├── Lambda
    ├── SQS
    ├── SNS
    ├── Step Functions
    └── API Gateway
```

---

## EventBridge 주요 기능

| 기능 | 설명 |
|------|------|
| **이벤트 버스** | 이벤트 라우팅 허브 |
| **Scheduler** | cron/rate 기반 스케줄 (CloudWatch Events 대체) |
| **Schema Registry** | 이벤트 스키마 관리 |
| **Pipes** | 소스 → 필터 → 타겟 직접 연결 |

> [!tip] CloudWatch Events vs EventBridge
> EventBridge = CloudWatch Events의 진화. 현재 EventBridge 사용 권장

---

## Step Functions 핵심

```
워크플로우 정의 (JSON/YAML):
State 1 (Task) → State 2 (Choice) → State 3 (Wait) → State 4 (Task)

지원 통합:
Lambda / DynamoDB / SQS / SNS / ECS / Glue / SageMaker / ...
```

| 모드 | 특징 |
|------|------|
| **Standard** | 최대 1년, 정확히 한 번, 감사 기록 |
| **Express** | 최대 5분, At-least-once, 고처리량 |

---

## Step Functions vs SQS+Lambda

| 항목 | Step Functions | SQS + Lambda |
|------|----------------|-------------|
| 워크플로우 가시성 | O (시각적) | X |
| 상태 관리 | 내장 | 직접 구현 |
| 오류 처리 | Retry/Catch 내장 | Lambda 코드 |
| 사용 케이스 | 복잡한 비즈니스 로직 | 단순 비동기 처리 |

---

## Exam/Test Patterns

| 시나리오/키워드 | 답 |
|----------------|-----|
| "다단계 워크플로우 오케스트레이션" | **Step Functions** |
| "Lambda → DynamoDB → 알림 순서 처리" | **Step Functions** |
| "cron 스케줄 작업" | **EventBridge Scheduler** |
| "EC2 상태 변경 시 자동 대응" | **EventBridge → Lambda** |
| "SaaS 이벤트 AWS 연동" | **EventBridge** |

## Related Notes
- [[SQS와 SNS]]
- [[Lambda와 서버리스]]
- [[애플리케이션통합 문제풀이]]
