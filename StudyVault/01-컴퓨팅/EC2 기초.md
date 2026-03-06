---
source_pdf: saa_questions.json
part: "01"
keywords: ec2, instance-types, pricing, placement-group, ebs-optimized
---

# EC2 기초 (★★★)

#aws-saa #compute

## Overview Table

| 항목 | 핵심 |
|------|------|
| 서비스 유형 | IaaS 가상 서버 |
| 가격 모델 | On-Demand / Reserved / Spot / Dedicated |
| 스토리지 | 인스턴스 스토어(임시) + EBS(영구) |
| 배치 그룹 | Cluster / Partition / Spread |
| 인터넷 연결 | 퍼블릭 서브넷 + IGW + 퍼블릭 IP |

---

## 가격 모델 비교

| 유형 | 약정 | 절감률 | 사용 케이스 |
|------|------|--------|------------|
| **On-Demand** | 없음 | 기준 | 단기/예측 불가 |
| **Reserved Standard** | 1~3년 | 최대 72% | 안정적 장기 워크로드 |
| **Reserved Convertible** | 1~3년 | 최대 54% | 인스턴스 타입 변경 필요 시 |
| **Spot** | 없음 | 최대 90% | 중단 허용 배치/분석 작업 |
| **Dedicated Host** | 선택 | - | 라이선스/컴플라이언스 |
| **Savings Plans** | 1~3년 | 최대 72% | 유연한 약정 (Compute/EC2) |

> [!warning] Spot 인스턴스 주의
> AWS가 인스턴스를 2분 전 통보 후 종료할 수 있음. 중단 불가 워크로드에 사용 불가.

---

## 배치 그룹 (Placement Group)

```
Cluster:   [AZ1: inst1 inst2 inst3 inst4]  ← 같은 AZ, 낮은 지연
Partition: [AZ1: P1] [AZ1: P2] [AZ2: P3]  ← 하드웨어 분리
Spread:    [AZ1:i1] [AZ2:i2] [AZ3:i3]     ← 완전 분리, AZ당 최대 7개
```

| 유형 | 특징 | 사용 케이스 |
|------|------|------------|
| **Cluster** | 동일 AZ, 초저지연 10Gbps | HPC, 빅데이터 |
| **Partition** | 파티션별 하드웨어 격리 | Hadoop, Kafka, Cassandra |
| **Spread** | 인스턴스별 독립 하드웨어 | 소규모 중요 인스턴스, AZ당 7개 제한 |

---

## 인스턴스 스토어 vs EBS

| 항목 | 인스턴스 스토어 | EBS |
|------|---------------|-----|
| 지속성 | 중지/종료 시 삭제 | 독립 유지 |
| 성능 | 매우 높음 (NVMe) | 높음 (gp3 최대 16K IOPS) |
| 연결 | 1:1 (분리 불가) | 탈부착 가능 |
| 용도 | 임시 버퍼/캐시 | OS/데이터 영구 저장 |

---

## Exam/Test Patterns

| 시나리오/키워드 | 답 |
|----------------|-----|
| "비용 최소화 + 중단 허용" | **Spot Instance** |
| "장기 안정적 + 비용 절감" | **Reserved Instance** |
| "HPC 클러스터 저지연 네트워크" | **Cluster Placement Group** |
| "고가용성 소수 인스턴스 격리" | **Spread Placement Group** |
| "중지 후 데이터 보존" | **EBS** (인스턴스 스토어 아님) |
| "라이선스 소켓/코어 규정" | **Dedicated Host** |

## Related Notes
- [[Auto Scaling]]
- [[EBS-EFS-FSx]]
- [[비용 최적화 전략]]
- [[EC2 기초 문제풀이]] → [[컴퓨팅 문제풀이]]
