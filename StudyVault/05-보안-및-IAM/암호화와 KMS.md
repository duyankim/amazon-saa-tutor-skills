---
source_pdf: saa_questions.json
part: "05"
keywords: kms, cmk, encryption, cloudhsm, envelope-encryption, secrets-manager
---

# 암호화와 KMS (★★★)

#aws-saa #security

## Overview Table

| 서비스 | 키 관리 | 하드웨어 | 사용 케이스 |
|--------|--------|---------|------------|
| **KMS (AWS Managed)** | AWS | 공유 HSM | 기본 암호화 |
| **KMS (Customer Managed)** | 고객 | 공유 HSM | 세밀한 제어 |
| **CloudHSM** | 고객 완전 제어 | **전용 HSM** | 컴플라이언스 |

---

## KMS 키 유형

| 유형 | 비용 | 로테이션 | 교차 계정 |
|------|------|---------|---------|
| **AWS Managed Key** | 무료 | 자동(연간) | X |
| **Customer Managed Key (CMK)** | $1/월 | 수동/자동 | O |
| **Custom Key Store (CloudHSM)** | 높음 | 수동 | O |

---

## 봉투 암호화 (Envelope Encryption)

```
1. KMS에서 Data Encryption Key(DEK) 생성
2. DEK로 실제 데이터 암호화
3. KMS CMK로 DEK 암호화 (Wrapped DEK)
4. 암호화된 데이터 + Wrapped DEK 저장

복호화:
Wrapped DEK → KMS → DEK → 데이터 복호화
```

> [!tip] 대용량 데이터 암호화
> KMS는 4KB 이상 직접 암호화 불가 → 봉투 암호화 사용

---

## Secrets Manager vs SSM Parameter Store

| 항목 | Secrets Manager | SSM Parameter Store |
|------|----------------|---------------------|
| 자동 로테이션 | **O** | X |
| RDS 통합 | **O** | X |
| 비용 | 비쌈 ($0.40/시크릿/월) | 무료(Standard)/유료(Advanced) |
| 크기 | 최대 64KB | Standard: 4KB / Advanced: 8KB |
| KMS 통합 | O | O |

> [!important] 자동 로테이션 = Secrets Manager
> "자동 자격증명 로테이션" → **Secrets Manager**
> 단순 설정값 저장 → **SSM Parameter Store**

---

## S3 암호화

| 방식 | 키 관리 | 감사 |
|------|--------|------|
| SSE-S3 | AWS | X |
| SSE-KMS | KMS CMK | O (CloudTrail) |
| SSE-C | 고객 제공 | - |
| 클라이언트 측 | 고객 완전 | - |

---

## Exam/Test Patterns

| 시나리오/키워드 | 답 |
|----------------|-----|
| "암호화 키 세밀한 제어, 감사" | **KMS CMK (Customer Managed)** |
| "전용 HSM, 컴플라이언스" | **CloudHSM** |
| "RDS 비밀번호 자동 로테이션" | **Secrets Manager** |
| "설정값 안전 저장, 저비용" | **SSM Parameter Store** |
| "KMS로 대용량 데이터 암호화" | **봉투 암호화 (Envelope)** |
| "S3 암호화 + 키 접근 감사" | **SSE-KMS** |

## Related Notes
- [[IAM 핵심]]
- [[보안 서비스]]
- [[S3 핵심 개념]]
- [[보안-및-IAM 문제풀이]]
