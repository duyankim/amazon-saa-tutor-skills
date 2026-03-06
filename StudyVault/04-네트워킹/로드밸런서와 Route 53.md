---
source_pdf: saa_questions.json
part: "04"
keywords: alb, nlb, route53, routing-policy, health-check, weighted, failover
---

# 로드밸런서와 Route 53 (★★★)

#aws-saa #networking

## 로드밸런서 비교

| 항목 | ALB | NLB | CLB |
|------|-----|-----|-----|
| 레이어 | L7 | L4 | L4/L7 |
| 프로토콜 | HTTP/HTTPS/WebSocket | TCP/UDP/TLS | HTTP/HTTPS/TCP |
| 고정 IP | X | **O (Elastic IP)** | X |
| 라우팅 | 경로/호스트/헤더 기반 | IP:Port 기반 | 기본 |
| 속도 | 빠름 | **초고속, 극저지연** | 보통 |
| WebSocket | O | O | X |
| 권장 | 웹 앱/마이크로서비스 | 게임/금융/IoT | 레거시 |

> [!tip] NLB 선택 조건
> "고정 IP 필요" + "TCP/UDP" + "극저지연" → **NLB**

---

## Route 53 라우팅 정책

| 정책 | 동작 | 사용 케이스 |
|------|------|------------|
| **Simple** | 단순 레코드 | 헬스체크 없음 |
| **Weighted** | 비율 분배 (%) | A/B 테스트, 블루/그린 |
| **Latency** | 최저 지연 리전 | 글로벌 성능 최적화 |
| **Failover** | 기본/보조 전환 | **헬스체크 필수**, DR |
| **Geolocation** | 사용자 지리 위치 | 규정 준수/지역별 콘텐츠 |
| **Geoproximity** | 편향 반경 기반 | Traffic Flow 필요 |
| **Multi-Value** | 최대 8개 헬시 레코드 | 로드밸런싱 근사치 |
| **IP-based** | CIDR 기반 | ISP별 라우팅 |

```
Failover 패턴:
Primary (헬스체크 정상) → 트래픽 수신
Primary 장애 → Failover → Secondary

Weighted 패턴:
레코드 A (weight=70) → 70% 트래픽
레코드 B (weight=30) → 30% 트래픽
레코드 C (weight=0)  → 0% (Blue/Green 배포)
```

---

## ALB 고급 기능

- **경로 기반 라우팅**: `/api/*` → 서비스 A, `/web/*` → 서비스 B
- **호스트 기반 라우팅**: `api.example.com` vs `web.example.com`
- **Lambda 타겟**: ALB → Lambda 함수 직접 호출
- **Sticky Session**: 특정 사용자를 동일 인스턴스에 고정

---

## Exam/Test Patterns

| 시나리오/키워드 | 답 |
|----------------|-----|
| "마이크로서비스 경로 기반 라우팅" | **ALB** |
| "고정 IP, TCP 부하분산" | **NLB** |
| "DR 페일오버 DNS" | **Route 53 Failover** |
| "A/B 테스트 50:50 분배" | **Route 53 Weighted** |
| "사용자 가장 가까운 리전" | **Route 53 Latency** |
| "특정 국가만 접근" | **Route 53 Geolocation** |

## Related Notes
- [[VPC 핵심]]
- [[Auto Scaling]]
- [[CloudFront와 API Gateway]]
- [[네트워킹 문제풀이]]
