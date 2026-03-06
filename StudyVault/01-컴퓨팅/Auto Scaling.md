---
source_pdf: saa_questions.json
part: "01"
keywords: auto-scaling, scaling-policy, target-tracking, step-scaling, elb
---

# Auto Scaling (★★★)

#aws-saa #compute

## Overview Table

| 항목 | 설명 |
|------|------|
| 목적 | 수요에 따라 EC2 인스턴스 수 자동 조절 |
| 방향 | 수평 확장 (인스턴스 추가/제거) |
| 통합 | ELB, CloudWatch, Launch Template |
| 범위 | EC2 ASG / ECS Service / DynamoDB / Aurora |

---

## Auto Scaling 정책 유형

| 정책 | 동작 | 사용 케이스 |
|------|------|------------|
| **Simple/Step Scaling** | CloudWatch 알람 → 단계별 조정 | 명확한 임계값 |
| **Target Tracking** | 지표(CPU 40% 등) 자동 유지 | **가장 권장** |
| **Scheduled Scaling** | 시간 기반 미리 스케일 | 예측 가능한 트래픽 |
| **Predictive Scaling** | ML 기반 사전 스케일링 | 반복적 패턴 |

> [!tip] 권장 정책
> 대부분의 경우 **Target Tracking Scaling**이 가장 단순하고 효율적

---

## ASG 핵심 설정

```
Min:     최소 인스턴스 수 (절대 감소 불가)
Desired: 현재 목표 수 (Min ≤ Desired ≤ Max)
Max:     최대 인스턴스 수 (절대 초과 불가)

Cooldown: 스케일 이후 대기 시간 (기본 300초)
```

---

## ELB + Auto Scaling 연동

```
사용자 → ALB → [Target Group] → [EC2 × N]
                                     ↕
                            [Auto Scaling Group]
                                     ↕
                            [CloudWatch 지표]
```

- 신규 인스턴스 자동으로 Target Group 등록
- 비정상 인스턴스 자동 교체 (Health Check)

---

## Exam/Test Patterns

| 시나리오/키워드 | 답 |
|----------------|-----|
| "트래픽 급증 시 자동 확장" | **Auto Scaling + ALB** |
| "CPU 70% 유지" | **Target Tracking Policy** |
| "매일 오전 9시 트래픽 증가" | **Scheduled Scaling** |
| "스케일인 후 바로 다시 스케일아웃" | **Cooldown 기간 조정** |
| "인스턴스 비정상 시 자동 교체" | **ASG Health Check** |

## Related Notes
- [[EC2 기초]]
- [[로드밸런서와 Route 53]]
- [[컴퓨팅 문제풀이]]
