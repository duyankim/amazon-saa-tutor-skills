---
keywords: exam traps, weak areas, common mistakes, aws-saa
---

# Exam Traps (시험 함정 포인트)

#dashboard #exam-traps #aws-saa

> [!warning] 이 노트의 목적
> AWS SAA 시험에서 자주 틀리거나 헷갈리는 포인트만 모은 **오답/함정 노트**입니다.

---

## 컴퓨팅 (EC2 / Lambda / ECS)

> [!danger]- Trap: Spot vs Reserved 선택 혼동
> - **함정**: "비용 절감"이라는 말에 Spot을 고르지만, "안정적인 운영"이 전제라면 Reserved
> - **기준**: 중단 가능 → Spot / 중단 불가 + 장기 → Reserved / 단기 → On-Demand
> - [[EC2 기초]]

> [!danger]- Trap: Lambda 타임아웃 한계
> - **함정**: Lambda는 최대 **15분**. 15분 이상 작업은 EC2 or Fargate
> - 배치성 장시간 작업은 AWS Batch 또는 Fargate Task
> - [[Lambda와 서버리스]]

> [!danger]- Trap: ECS vs EKS 선택 기준
> - ECS: AWS 네이티브, 간단 — 기존 Kubernetes 불필요 시
> - EKS: Kubernetes 이식성 필요 or 이미 K8s 사용 중
> - [[컨테이너 ECS-EKS]]

---

## 스토리지 (S3 / EBS / EFS)

> [!danger]- Trap: S3 스토리지 클래스 혼동
> - **Standard-IA vs One Zone-IA**: 재현 불가 데이터 → Standard-IA (다중 AZ)
> - **Intelligent-Tiering**: 모니터링 비용 발생 — 객체 수 많을수록 유리
> - **Glacier Instant vs Flexible**: 밀리초 필요 → Instant / 분~시간 OK → Flexible
> - [[Glacier와 수명주기]]

> [!danger]- Trap: EBS vs EFS 혼동
> - EBS: **단일 EC2**에 연결 (io2 제외), AZ 종속
> - EFS: **다수 EC2** 동시 마운트, 리전 범위, Linux only
> - FSx for Windows: Windows SMB 공유 파일 시스템
> - [[EBS-EFS-FSx]]

> [!danger]- Trap: S3 Transfer Acceleration vs DataSync
> - Transfer Acceleration: **인터넷을 통한 S3 업로드 가속** (CloudFront 엣지 활용)
> - DataSync: **온프레미스 ↔ AWS 파일 동기화** (NFS/SMB)
> - [[S3 고급 기능]] [[데이터 마이그레이션 서비스]]

---

## 데이터베이스 (RDS / DynamoDB / ElastiCache)

> [!danger]- Trap: Multi-AZ vs Read Replica 혼동
> - **Multi-AZ**: 고가용성/장애복구 — 동기 복제, standby는 읽기 불가
> - **Read Replica**: 읽기 성능 향상 — 비동기 복제, 별도 엔드포인트
> - "가용성" → Multi-AZ / "읽기 성능" → Read Replica
> - [[RDS와 Aurora]]

> [!danger]- Trap: ElastiCache Redis vs Memcached
> - Redis: 다중 AZ, 지속성, Pub/Sub, 정렬셋, 복잡한 데이터구조
> - Memcached: 멀티스레드, 단순 캐시, 지속성 없음
> - "세션 관리/리더보드/Pub-Sub" → Redis
> - [[ElastiCache]]

> [!danger]- Trap: DynamoDB 용량 모드 혼동
> - **Provisioned + Auto Scaling**: 예측 가능한 트래픽
> - **On-Demand**: 예측 불가 또는 스파이크 트래픽 — 더 비쌈
> - [[DynamoDB]]

---

## 네트워킹 (VPC / Route 53 / CloudFront)

> [!danger]- Trap: ALB vs NLB 선택 혼동
> - ALB: HTTP/HTTPS, 경로/호스트 기반 라우팅, WebSocket
> - NLB: TCP/UDP, 극저지연, **고정 IP(Elastic IP)** 필요 시
> - "고정 IP가 필요" → NLB
> - [[로드밸런서와 Route 53]]

> [!danger]- Trap: VPC Peering vs Transit Gateway
> - Peering: 1:1 연결, 전이적 라우팅 **불가** (A↔B, B↔C ≠ A↔C)
> - Transit Gateway: N:N 허브, 전이적 라우팅 **가능**
> - VPC가 3개 이상 → Transit Gateway
> - [[VPC 핵심]]

> [!danger]- Trap: Route 53 라우팅 정책 혼동
> - Failover ≠ Weighted: Failover는 헬스체크 기반 / Weighted는 비율
> - Multi-Value ≠ ALB: Multi-Value는 DNS 레벨, ALB는 L7 로드밸런싱
> - [[로드밸런서와 Route 53]]

> [!danger]- Trap: CloudFront vs Global Accelerator
> - CloudFront: HTTP 콘텐츠 캐싱 CDN, 정적/동적 콘텐츠
> - Global Accelerator: TCP/UDP Anycast, 캐싱 없음, 고정 IP
> - "게임/IoT/고정 IP" → Global Accelerator / "웹 캐싱" → CloudFront
> - [[CloudFront와 API Gateway]]

---

## 보안-및-IAM

> [!danger]- Trap: IAM Role vs Resource Policy
> - 교차 계정 접근: IAM Role (assume) **또는** Resource Policy (S3 버킷 정책)
> - 단일 계정 내: 둘 다 사용 가능
> - [[IAM 핵심]]

> [!danger]- Trap: Secrets Manager vs SSM Parameter Store
> - Secrets Manager: 자동 **로테이션** 지원, 더 비쌈
> - SSM Parameter Store: 무료(Standard)/유료(Advanced), 로테이션 없음
> - "자동 로테이션" → Secrets Manager
> - [[보안 서비스]]

> [!danger]- Trap: KMS vs CloudHSM
> - KMS: 공유 하드웨어, AWS 관리, 비용 저렴
> - CloudHSM: 전용 하드웨어, 고객 완전 제어, 컴플라이언스 요구 시
> - [[암호화와 KMS]]

---

## 애플리케이션통합 (SQS / SNS / Kinesis)

> [!danger]- Trap: SQS Standard vs FIFO
> - FIFO 최대 300 TPS (배치 시 3,000) — 높은 처리량 불필요 시 FIFO
> - Exactly-once 처리 필요 → FIFO
> - [[SQS와 SNS]]

> [!danger]- Trap: Kinesis Streams vs Firehose
> - Streams: 실시간, **직접 처리**, 커스텀 컨슈머, 데이터 보관(1~365일)
> - Firehose: 완전 관리형 **목적지 전달** → S3/Redshift/OpenSearch
> - [[Kinesis]]

---

## Related
- [[MOC - AWS SAA]] → Weak Areas 섹션
- [[빠른 참조]]
