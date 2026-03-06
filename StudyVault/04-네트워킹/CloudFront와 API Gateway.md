---
source_pdf: saa_questions.json
part: "04"
keywords: cloudfront, api-gateway, edge, cdn, caching, global-accelerator
---

# CloudFront와 API Gateway (★★★)

#aws-saa #networking

## CloudFront 개요

```
사용자 → [CloudFront 엣지 POP] → [오리진]
              ↑ 캐시 히트          S3 / ALB / EC2 / Custom
              (지연 없음)
```

| 항목 | 값 |
|------|-----|
| 엣지 POP | 전 세계 400+ |
| 캐시 | 정적 + 동적 콘텐츠 |
| 프로토콜 | HTTP/HTTPS, WebSocket |
| 오리진 | S3, ALB, EC2, HTTP 서버 |
| 보안 | OAC/OAI, WAF, Shield 통합 |

---

## CloudFront vs S3 Transfer Acceleration vs Global Accelerator

| 서비스 | 최적화 | 캐싱 | 고정 IP | 주요 용도 |
|--------|--------|------|---------|---------|
| **CloudFront** | HTTP 콘텐츠 | O | X | 웹/미디어 CDN |
| **S3 Transfer Acceleration** | S3 업로드 | X | X | S3 대용량 업로드 |
| **Global Accelerator** | TCP/UDP | X | O (Anycast) | 게임/IoT/비HTTP |

> [!warning] CloudFront vs Global Accelerator 혼동
> 캐싱 + HTTP → CloudFront
> 고정 IP + TCP/UDP + 비캐싱 → Global Accelerator

---

## CloudFront Origin Access Control (OAC)

```
사용자 → CloudFront (서명된 요청) → S3 버킷
                                   (퍼블릭 차단 유지)
```
- S3 버킷을 **퍼블릭으로 열지 않고** CloudFront를 통해서만 접근
- OAI(레거시) → OAC(권장)

---

## API Gateway 핵심

| 항목 | REST API | HTTP API | WebSocket API |
|------|----------|---------|--------------|
| 기능 | 풍부 | 단순/저렴 | 양방향 |
| 비용 | 높음 | 70% 저렴 | - |
| 캐싱 | O | X | X |
| 권한 부여 | 다양 | JWT/Lambda | Lambda |

```
클라이언트 → API Gateway → Lambda (서버리스 백엔드)
                        → ECS/EC2 (HTTP 통합)
                        → DynamoDB (직접 통합)
                        → Step Functions
```

---

## Lambda@Edge & CloudFront Functions

| 항목 | CloudFront Functions | Lambda@Edge |
|------|---------------------|-------------|
| 실행 | 뷰어 요청/응답 | 뷰어+오리진 요청/응답 |
| 지연 | <1ms | 수ms |
| 용도 | 헤더조작, URL 리다이렉트 | A/B 테스트, 인증 |

---

## Exam/Test Patterns

| 시나리오/키워드 | 답 |
|----------------|-----|
| "S3 정적 사이트 전 세계 배포" | **CloudFront + S3** |
| "S3를 CloudFront로만 접근 제한" | **OAC (Origin Access Control)** |
| "서버리스 REST API" | **API Gateway + Lambda** |
| "고정 IP 글로벌 앱" | **Global Accelerator** |
| "CloudFront 엣지 인증 처리" | **Lambda@Edge** |
| "DDoS 보호 + CDN" | **CloudFront + Shield** |

## Related Notes
- [[로드밸런서와 Route 53]]
- [[Lambda와 서버리스]]
- [[보안 서비스]]
- [[네트워킹 문제풀이]]
