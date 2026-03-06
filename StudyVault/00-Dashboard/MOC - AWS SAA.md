---
source_pdf: saa_questions.json
part: all
keywords: MOC, study map, aws-saa, solutions-architect-associate
---

# AWS Solutions Architect Associate — 학습 맵

#dashboard #aws-saa

## Overview
- **시험**: AWS Certified Solutions Architect – Associate (SAA-C03)
- **문제 은행**: 724문제 (Korean) — `saa_questions.json`
- **학습 방식**: 도메인별 개념 노트 + 기존 문제은행 참조 연습

> [!important] 시험 도메인 가중치 (SAA-C03)
> | 도메인 | 가중치 |
> |--------|--------|
> | 복원력 있는 아키텍처 설계 | 26% |
> | 고성능 아키텍처 설계 | 24% |
> | 안전한 애플리케이션 및 아키텍처 설계 | 30% |
> | 비용 최적화 아키텍처 설계 | 20% |

---

## Topic Map

| 섹션 | 소스 | 개념 노트 | 문제 수 | 상태 |
|------|------|-----------|---------|------|
| 01-컴퓨팅 | saa_questions.json | [[EC2 기초]], [[Lambda와 서버리스]], [[컨테이너 ECS-EKS]], [[Auto Scaling]] | 190문제 | [ ] |
| 02-스토리지 | saa_questions.json | [[S3 핵심 개념]], [[S3 고급 기능]], [[EBS-EFS-FSx]], [[Glacier와 수명주기]] | 94문제 | [ ] |
| 03-데이터베이스 | saa_questions.json | [[RDS와 Aurora]], [[DynamoDB]], [[ElastiCache]], [[기타 데이터베이스]] | 131문제 | [ ] |
| 04-네트워킹 | saa_questions.json | [[VPC 핵심]], [[로드밸런서와 Route 53]], [[CloudFront와 API Gateway]], [[하이브리드 네트워킹]] | 130문제 | [ ] |
| 05-보안-및-IAM | saa_questions.json | [[IAM 핵심]], [[암호화와 KMS]], [[보안 서비스]], [[계정 관리]] | 50문제 | [ ] |
| 06-애플리케이션통합 | saa_questions.json | [[SQS와 SNS]], [[Kinesis]], [[EventBridge와 Step Functions]] | 48문제 | [ ] |
| 07-분석 | saa_questions.json | [[Athena와 Glue]], [[EMR과 Redshift]], [[OpenSearch와 QuickSight]] | 37문제 | [ ] |
| 08-마이그레이션-및-전송 | saa_questions.json | [[데이터 마이그레이션 서비스]], [[스토리지 마이그레이션]] | 36문제 | [ ] |
| 09-고가용성-DR | saa_questions.json | [[고가용성과 재해복구 전략]] | 3문제 | [ ] |
| 10-비용최적화 | saa_questions.json | [[비용 최적화 전략]] | 5문제 | [ ] |

---

## Practice Notes

| 문제셋 | 문항 수 | 링크 |
|--------|---------|------|
| 컴퓨팅 문제풀이 | 190문제 | [[컴퓨팅 문제풀이]] |
| 스토리지 문제풀이 | 94문제 | [[스토리지 문제풀이]] |
| 데이터베이스 문제풀이 | 131문제 | [[데이터베이스 문제풀이]] |
| 네트워킹 문제풀이 | 130문제 | [[네트워킹 문제풀이]] |
| 보안-및-IAM 문제풀이 | 50문제 | [[보안-및-IAM 문제풀이]] |
| 애플리케이션통합 문제풀이 | 48문제 | [[애플리케이션통합 문제풀이]] |
| 분석 문제풀이 | 37문제 | [[분석 문제풀이]] |
| 마이그레이션-및-전송 문제풀이 | 36문제 | [[마이그레이션-및-전송 문제풀이]] |
| 고가용성-DR 문제풀이 | 3문제 | [[고가용성-DR 문제풀이]] |
| 비용최적화 문제풀이 | 5문제 | [[비용최적화 문제풀이]] |

---

## Study Tools

| 도구 | 설명 | 링크 |
|------|------|------|
| Exam Traps | 시험 함정/오답 포인트 모음 | [[Exam Traps]] |
| Quick Reference | 전체 치트시트 | [[빠른 참조]] |

---

## Tag Index

| Tag | 관련 주제 | 규칙 |
|-----|-----------|------|
| `#aws-saa` | 전체 AWS SAA | 최상위 태그 — 모든 노트에 부착 |
| `#compute` | EC2, Lambda, ECS, Auto Scaling | 도메인 태그 |
| `#storage` | S3, EBS, EFS, FSx, Glacier | 도메인 태그 |
| `#database` | RDS, Aurora, DynamoDB, ElastiCache | 도메인 태그 |
| `#networking` | VPC, Route 53, CloudFront, ALB/NLB | 도메인 태그 |
| `#security` | IAM, KMS, WAF, Shield, GuardDuty | 도메인 태그 |
| `#integration` | SQS, SNS, Kinesis, EventBridge | 도메인 태그 |
| `#analytics` | Athena, Glue, EMR, Redshift | 도메인 태그 |
| `#migration` | DMS, DataSync, Snowball, Storage Gateway | 도메인 태그 |
| `#ha-dr` | 재해복구, RTO/RPO, Multi-Region | 도메인 태그 |
| `#cost-optimization` | 비용 최적화, Savings Plans | 도메인 태그 |
| `#practice` | 모든 문제풀이 파일 | 유형 태그 |
| `#exam-traps` | 시험 함정 포인트 | 유형 태그 |

> **태그 규칙**: 최상위(`#aws-saa`) → 도메인 → 세부기술. 세부 태그는 반드시 도메인 태그와 함께 부착.

---

## Weak Areas
- [ ] 미측정 → 학습 후 업데이트 → [[Exam Traps]]

---

## Non-core Topic Policy

| 소스 | 내용 | 처리 |
|------|------|------|
| saa_questions.json | 724문제 Korean AWS SAA | **포함** — 전체 처리 |
| README.md | 프로젝트 안내 | **제외** — 학습 내용 아님 |
| skills/ | Claude 스킬 파일 | **제외** — 학습 내용 아님 |
