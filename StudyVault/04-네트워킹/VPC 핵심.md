---
source_pdf: saa_questions.json
part: "04"
keywords: vpc, subnet, nacl, security-group, nat-gateway, vpc-peering, transit-gateway
---

# VPC 핵심 (★★★)

#aws-saa #networking

## Overview Table

| 구성요소 | 범위 | 기능 |
|---------|------|------|
| VPC | 리전 | 가상 프라이빗 클라우드 |
| 서브넷 | AZ | 퍼블릭/프라이빗 분리 |
| 인터넷 게이트웨이(IGW) | VPC | 인터넷 연결 (퍼블릭) |
| NAT Gateway | AZ | 프라이빗 → 인터넷 단방향 |
| 보안 그룹 | 인스턴스 | 상태 기반(Stateful) 방화벽 |
| NACL | 서브넷 | 상태 비기반(Stateless) 방화벽 |

---

## 보안 그룹 vs NACL

```
인터넷
  ↓
[NACL — 서브넷 경계, Stateless]
  ↓
[보안 그룹 — 인스턴스 경계, Stateful]
  ↓
EC2 인스턴스
```

| 항목 | 보안 그룹 | NACL |
|------|----------|------|
| 상태 | **Stateful** (응답 자동 허용) | **Stateless** (인/아웃 별도 규칙) |
| 범위 | 인스턴스 수준 | 서브넷 수준 |
| 규칙 | Allow만 | Allow + **Deny** |
| 평가 | 모든 규칙 | 번호 순서대로 (첫 번째 매칭) |

> [!important] Stateful vs Stateless
> 보안 그룹: 인바운드 허용 → 응답 아웃바운드 자동 허용
> NACL: 인바운드 허용해도 아웃바운드 규칙 별도 필요

---

## VPC 연결 옵션

| 방법 | 대상 | 전이 | 비용 |
|------|------|------|------|
| **VPC Peering** | VPC ↔ VPC | **불가** | 낮음 |
| **Transit Gateway** | N개 VPC 허브 | **가능** | 중간 |
| **VPC Endpoint** | AWS 서비스 (S3/DynamoDB) | - | 낮음 |
| **PrivateLink** | VPC ↔ 서비스 (단방향) | - | 중간 |

```
VPC Peering (전이 불가):
A ↔ B, B ↔ C → A와 C는 통신 불가 (직접 Peering 필요)

Transit Gateway (전이 가능):
VPC-A ─┐
VPC-B ─┼─ TGW ─→ 모두 통신 가능
VPC-C ─┘
```

---

## VPC Endpoint 유형

| 유형 | 대상 서비스 | 특징 |
|------|------------|------|
| **Gateway Endpoint** | S3, DynamoDB | 라우팅 테이블 사용, 무료 |
| **Interface Endpoint** | 대부분의 AWS 서비스 | ENI 사용, 비용 발생 |

---

## NAT Gateway vs NAT Instance

| 항목 | NAT Gateway | NAT Instance |
|------|------------|-------------|
| 관리 | AWS 관리형 | 사용자 관리 |
| 가용성 | AZ 내 고가용성 | 단일 EC2 |
| 대역폭 | 최대 100Gbps | 인스턴스 타입 의존 |
| 비용 | 더 비쌈 | 저렴 |
| 권장 | **현재 권장** | 레거시 |

---

## Exam/Test Patterns

| 시나리오/키워드 | 답 |
|----------------|-----|
| "프라이빗 EC2 인터넷 접근" | **NAT Gateway** |
| "IP 차단 (특정 IP Deny)" | **NACL** (보안 그룹은 Deny 불가) |
| "3개 이상 VPC 연결" | **Transit Gateway** |
| "S3를 인터넷 없이 VPC에서 접근" | **VPC Gateway Endpoint** |
| "VPC 간 1:1 연결" | **VPC Peering** |

## Related Notes
- [[로드밸런서와 Route 53]]
- [[하이브리드 네트워킹]]
- [[보안 서비스]]
- [[네트워킹 문제풀이]]
