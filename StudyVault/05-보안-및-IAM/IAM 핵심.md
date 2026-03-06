---
source_pdf: saa_questions.json
part: "05"
keywords: iam, role, policy, permission-boundary, scp, cross-account
---

# IAM 핵심 (★★★)

#aws-saa #security

## Overview Table

| IAM 요소 | 설명 |
|---------|------|
| **User** | 장기 자격증명, 사람 또는 서비스 |
| **Group** | User 집합, 정책 일괄 적용 |
| **Role** | 임시 자격증명, 서비스/교차 계정 |
| **Policy** | JSON 권한 문서 |

---

## 정책 유형

| 유형 | 연결 대상 | 사용 케이스 |
|------|----------|------------|
| **Identity Policy** | User/Group/Role | 주체가 할 수 있는 것 |
| **Resource Policy** | 리소스(S3 버킷 등) | 리소스에 접근 가능한 주체 |
| **Permission Boundary** | User/Role | 최대 허용 범위 제한 |
| **SCP** | Organizations OU/계정 | 계정 전체 최대 권한 |
| **Session Policy** | AssumeRole 시 | 세션 기간 추가 제한 |

---

## IAM 역할 (Role) 활용

```
EC2 인스턴스
  └─ Instance Profile → IAM Role → S3/DynamoDB 접근
                         (임시 자격증명 자동 갱신)

Lambda 함수
  └─ Execution Role → DynamoDB/CloudWatch 접근

교차 계정 접근:
  계정A (User) → AssumeRole → 계정B (Role) → 리소스
```

> [!important] 역할 vs 액세스 키
> EC2/Lambda에서 AWS 서비스 접근 시 **항상 IAM Role 사용**
> 액세스 키를 EC2에 직접 저장하는 것은 보안 위험

---

## 최소 권한 원칙

- 기본 **명시적 거부(Explicit Deny)** 우선
- 평가 순서: Explicit Deny → SCP → Permission Boundary → Identity Policy → Resource Policy

```
권한 평가 순서:
1. 명시적 Deny → 즉시 거부
2. SCP → 계정 최대 권한 확인
3. Permission Boundary → 역할/사용자 최대 권한
4. Identity Policy → 실제 허용 권한
5. Resource Policy → 리소스 접근 허용
```

---

## IAM Policy 구조

```json
{
  "Effect": "Allow|Deny",
  "Action": ["s3:GetObject"],
  "Resource": ["arn:aws:s3:::bucket/*"],
  "Condition": { "StringEquals": { "aws:RequestedRegion": "ap-northeast-2" } }
}
```

---

## Exam/Test Patterns

| 시나리오/키워드 | 답 |
|----------------|-----|
| "EC2에서 S3 접근" | **IAM Role (Instance Profile)** |
| "교차 계정 접근" | **IAM Role (AssumeRole)** |
| "특정 리전만 사용 허용" | **SCP 또는 Condition** |
| "개발자가 자신 역할 이상 못 만들게" | **Permission Boundary** |
| "Organizations 전체 제어" | **SCP** |
| "Lambda에서 DynamoDB 쓰기" | **Lambda Execution Role** |

## Related Notes
- [[암호화와 KMS]]
- [[보안 서비스]]
- [[계정 관리]]
- [[보안-및-IAM 문제풀이]]
