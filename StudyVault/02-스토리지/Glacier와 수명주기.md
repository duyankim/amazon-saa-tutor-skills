---
source_pdf: saa_questions.json
part: "02"
keywords: glacier, lifecycle-policy, archival, retrieval, vault-lock
---

# Glacier와 수명주기 (★★)

#aws-saa #storage

## Glacier 검색 옵션

| 클래스 | 검색 속도 | 비용 |
|--------|----------|------|
| **Glacier Instant Retrieval** | 밀리초 | 높음 |
| **Glacier Flexible** — Expedited | 1~5분 | 중간 |
| **Glacier Flexible** — Standard | 3~5시간 | 낮음 |
| **Glacier Flexible** — Bulk | 5~12시간 | 최저 |
| **Glacier Deep Archive** — Standard | 12시간 | 매우 낮음 |
| **Glacier Deep Archive** — Bulk | 48시간 | 최저 |

---

## S3 수명주기 정책 (Lifecycle Policy)

```
생성 → [30일] → Standard-IA
              → [90일] → Glacier Flexible
                       → [180일] → Glacier Deep Archive
                                 → [365일] → 만료(삭제)
```

> [!important] 수명주기 전환 제한
> - Standard → Glacier: 최소 30일 후 가능
> - One Zone-IA → Glacier Flexible: 가능
> - Glacier 클래스 간 직접 전환: 불가 (복원 후 전환)

---

## Glacier Vault Lock

- **WORM** (Write Once Read Many) 정책 적용
- 잠금 후 정책 변경 불가 (규정 준수 아카이빙)
- 24시간 내 완료 전에는 취소 가능

---

## Exam/Test Patterns

| 시나리오/키워드 | 답 |
|----------------|-----|
| "7~10년 장기 보관, 최저 비용" | **S3 Glacier Deep Archive** |
| "분기 접근, 즉시 검색" | **S3 Glacier Instant** |
| "자동 계층 이동" | **S3 수명주기 정책** |
| "규정 준수 불변 아카이빙" | **Glacier Vault Lock** |
| "30일 후 IA, 1년 후 삭제" | **수명주기 정책 구성** |

## Related Notes
- [[S3 핵심 개념]]
- [[S3 고급 기능]]
- [[스토리지 문제풀이]]
