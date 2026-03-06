---
source_pdf: saa_questions.json
part: "01"
keywords: ecs, eks, fargate, container, kubernetes
---

# 컨테이너 ECS-EKS (★★)

#aws-saa #compute

## Overview Table

| 항목 | ECS | EKS |
|------|-----|-----|
| 오케스트레이터 | AWS 자체 | Kubernetes |
| 학습 곡선 | 낮음 | 높음 |
| 이식성 | AWS 전용 | 클라우드 이식 가능 |
| 런치 타입 | EC2, Fargate | EC2, Fargate, Managed Node |

---

## ECS vs EKS 선택 기준

```
기존 Kubernetes 사용 중? → EKS
AWS 네이티브, 간단 운영?  → ECS
멀티클라우드 이식성?       → EKS
```

---

## Fargate (서버리스 컨테이너)

- EC2 인스턴스 **프로비저닝/관리 불필요**
- ECS와 EKS 모두 지원
- 태스크 단위 격리 — 보안 강화
- 요금: 태스크당 vCPU + 메모리 사용 시간

> [!tip] Fargate 선택 시점
> "운영 복잡성 최소화" + "컨테이너" 키워드 → **ECS Fargate** 우선 고려

---

## ECS 핵심 구성요소

```
Cluster  → Task Definition → Task (실행 중 컨테이너)
Service  → Task 개수 유지 + ELB 통합
ECR      → 컨테이너 이미지 레지스트리
```

---

## Exam/Test Patterns

| 시나리오/키워드 | 답 |
|----------------|-----|
| "컨테이너 서버리스 실행" | **ECS Fargate** |
| "기존 Kubernetes 마이그레이션" | **EKS** |
| "EC2 없이 컨테이너" | **Fargate** |
| "컨테이너 이미지 저장소" | **ECR** |
| "마이크로서비스 오케스트레이션" | **ECS or EKS** |

## Related Notes
- [[Lambda와 서버리스]]
- [[Auto Scaling]]
- [[로드밸런서와 Route 53]]
- [[컴퓨팅 문제풀이]]
