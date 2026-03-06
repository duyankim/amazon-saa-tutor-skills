---
source_pdf: saa_questions.json
part: "01"
keywords: lambda, serverless, api-gateway, event-driven, concurrency
---

# Lambda와 서버리스 (★★★)

#aws-saa #compute

## Overview Table

| 항목 | Lambda | Fargate |
|------|--------|---------|
| 실행 단위 | 함수 | 컨테이너 |
| 최대 실행시간 | **15분** | 무제한 |
| 최대 메모리 | 10GB | 30GB |
| 요금 | 요청 수 + 실행시간 | vCPU + 메모리 시간 |
| 트리거 | 이벤트(API/S3/SQS 등) | ECS Task 직접 |

---

## Lambda 핵심 한계

```
실행 시간: 최대 15분 (900초)
메모리:   128MB ~ 10,240MB
임시 저장: /tmp — 10GB
동시성:   계정당 기본 1,000 (리전별)
패키지:   배포 패키지 최대 250MB (비압축)
```

> [!warning] 15분 초과 작업
> Lambda는 15분 이상 실행 불가. 장시간 처리는:
> - **AWS Batch** (배치 컴퓨팅)
> - **ECS Fargate** (컨테이너 장시간 실행)
> - **Step Functions** (워크플로우 오케스트레이션)

---

## Lambda 트리거 패턴

```
API Gateway → Lambda → DynamoDB/RDS
S3 Event    → Lambda → 이미지 처리/ETL
SQS Queue   → Lambda → 메시지 소비 (배치)
EventBridge → Lambda → 스케줄 작업
Kinesis     → Lambda → 실시간 스트림 처리
```

---

## 서버리스 아키텍처 패턴

| 패턴 | 구성 | 사용 케이스 |
|------|------|------------|
| API 백엔드 | API Gateway + Lambda + DynamoDB | REST API |
| 이벤트 처리 | S3 → Lambda → SES/SNS | 파일 업로드 알림 |
| 스케줄 작업 | EventBridge → Lambda | 배치 리포트 |
| 팬아웃 | SNS → Lambda × N | 멀티 처리 |

---

## Lambda@Edge vs CloudFront Functions

| 항목 | Lambda@Edge | CloudFront Functions |
|------|-------------|---------------------|
| 실행 위치 | CloudFront 엣지 리전 | CloudFront 엣지 POP |
| 최대 실행시간 | 5초(뷰어)/30초(오리진) | 1ms |
| 런타임 | Node.js, Python | JavaScript only |
| 용도 | 복잡한 요청 변환 | 헤더 조작/URL 리다이렉트 |

---

## Exam/Test Patterns

| 시나리오/키워드 | 답 |
|----------------|-----|
| "서버 관리 없이 코드 실행" | **Lambda** |
| "15분 이상 배치 처리" | **AWS Batch / ECS Fargate** |
| "API 서버리스 백엔드" | **API Gateway + Lambda** |
| "S3 업로드 시 자동 처리" | **S3 Event → Lambda** |
| "CloudFront 엣지에서 인증" | **Lambda@Edge** |
| "동시 실행 수 초과 방지" | **Reserved Concurrency** |

## Related Notes
- [[컨테이너 ECS-EKS]]
- [[SQS와 SNS]]
- [[EventBridge와 Step Functions]]
- [[CloudFront와 API Gateway]]
- [[컴퓨팅 문제풀이]]
