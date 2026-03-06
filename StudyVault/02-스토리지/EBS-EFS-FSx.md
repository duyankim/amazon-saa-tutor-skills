---
source_pdf: saa_questions.json
part: "02"
keywords: ebs, efs, fsx, block-storage, file-storage, nfs, smb
---

# EBS-EFS-FSx (★★★)

#aws-saa #storage

## Overview Table 비교

| 항목 | EBS | EFS | FSx for Windows | FSx for Lustre |
|------|-----|-----|-----------------|---------------|
| 유형 | 블록 | 파일(NFS) | 파일(SMB) | 파일(Lustre) |
| OS | Linux/Windows | **Linux only** | Windows | Linux |
| 연결 | 단일 EC2* | 다수 EC2 동시 | 다수 | 다수 |
| 리전/AZ | AZ 종속 | 리전 범위 | AZ 또는 Multi-AZ | AZ |
| 스케일 | 수동 | 자동 | 자동 | 자동 |

*io2 Block Express는 멀티-어태치 지원 (동일 AZ 내)

---

## EBS 볼륨 타입

| 타입 | 유형 | 최대 IOPS | 사용 케이스 |
|------|------|----------|------------|
| **gp3** | 범용 SSD | 16,000 | 기본 선택, 독립적 IOPS 설정 |
| **gp2** | 범용 SSD | 16,000 | 레거시 (gp3 권장) |
| **io2** | 프로비전드 SSD | 256,000 | 고성능 DB, 멀티-어태치 |
| **io1** | 프로비전드 SSD | 64,000 | io2 이전 세대 |
| **st1** | 처리량 최적화 HDD | 500 | 빅데이터, 로그 |
| **sc1** | 콜드 HDD | 250 | 가장 저렴, 비자주 접근 |

> [!warning] HDD 타입 제한
> st1/sc1은 **부팅 볼륨으로 사용 불가**

---

## EFS 특징

```
마운트 타겟: 각 AZ에 생성
접근:       다수 EC2 동시 NFS 마운트
스케일:     자동 (페타바이트까지)
클래스:     Standard / Infrequent Access (수명주기 정책)
성능:       General Purpose / Max I/O
```

---

## FSx 제품군

| 제품 | 프로토콜 | 주요 특징 |
|------|---------|---------|
| **FSx for Windows** | SMB | Active Directory 통합, DFS 네임스페이스 |
| **FSx for Lustre** | Lustre | HPC/ML, S3 직접 연동, 초고성능 |
| **FSx for NetApp ONTAP** | NFS/SMB/iSCSI | 멀티프로토콜, 데이터 중복제거 |
| **FSx for OpenZFS** | NFS | ZFS 기능, 스냅샷 |

---

## Exam/Test Patterns

| 시나리오/키워드 | 답 |
|----------------|-----|
| "다수 Linux EC2 파일 공유" | **EFS** |
| "Windows 파일 서버 AD 통합" | **FSx for Windows** |
| "HPC/ML S3 연동 고성능" | **FSx for Lustre** |
| "고IOPS DB 스토리지" | **EBS io2** |
| "EC2 기본 OS 볼륨" | **EBS gp3** |
| "비자주 대용량 순차 읽기" | **EBS st1** |

## Related Notes
- [[S3 핵심 개념]]
- [[EC2 기초]]
- [[스토리지 문제풀이]]
