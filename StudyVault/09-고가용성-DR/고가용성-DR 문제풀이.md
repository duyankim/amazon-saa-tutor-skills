---
source_pdf: saa_questions.json
part: "09"
keywords: practice, ha, disaster-recovery, rto, rpo, backup
---

# 고가용성-DR 문제풀이 (8문제)

#practice #ha-dr #aws-saa

## Related Concepts
- [[고가용성과 재해복구 전략]]
- [[RDS와 Aurora]]
- [[S3 고급 기능]]

> [!hint]- 핵심 패턴 (클릭하여 보기)
> | 문제 | 정답 | 핵심 |
> |------|------|------|
> | Q#71 | **B** | ・    A(X) : 리전 장애 발생 시 리디렉션에는 탁월하나 데이터 손상에는 취약함. 글로벌  테이블에서 ... |
> | Q#453 | **D** | AWS Backup 은 컴퓨팅, 스토리지 및 데이터베이스 전반에서 AWS 서비스의 데이터 보호를  중앙 집중... |
> | Q#618 | **C** | ... |
> | Q#178 | **A** | AWS Backup 을 사용하여 EC2 및 RDS 백업을 별도의 리전에 복사하는 것은 최소한의 운영  오버헤... |
> | Q#217 | **A** | 솔루션은 기본 인프라가 정상일 때 부하를 처리할 필요가 없다고 했으므로 Active/Passive  Fail... |
> | Q#273 | **B** | ・ 웜 스탠바이는 감소된 수준의 트래픽을 즉시 처리할 수 있습니다. 그런 다음 이 기존  배포를 확장해야 하... |

---

## Question 1 - [#71] [recall]
> 한 회사는 Amazon DynamoDB 를 사용하여 고객 정보를 저장하는 쇼핑 애플리케이션을  실행합니다. 데이터 손상의 경우 솔루션 설계자는 15 분의 RPO(복구 시점 목표)와 1 시간의  RTO(복구 시간 목표)를 충족하는 솔루션을 설계해야 합니다.  이러한 요구 사항을 충족하기 위해 솔루션 설계자는 무엇을 권장해야 합니까?

> - **A**: DynamoDB 전역 테이블을 구성합니다. RPO 복구의 경우 애플리케이션이 다른 AWS  리전을 가리키도록 합니다.
> - **B**: DynamoDB 지정 시간 복구를 구성합니다. RPO 복구의 경우 원하는 시점으로  복원합니다.
> - **C**: DynamoDB 데이터를 매일 Amazon S3 Glacier 로 내보냅니다. RPO 복구의 경우 S3  Glacier 에서 DynamoDB 로 데이터를 가져옵니다.
> - **D**: DynamoDB 테이블에 대한 Amazon Elastic Block Store(Amazon EBS) 스냅샷을  15 분마다 예약합니다. RPO 복구의 경우 EBS 스냅샷을 사용하여 DynamoDB 테이블을  복원합니다.

> [!answer]- 정답 보기
> **정답: B**
>
> ・    A(X) : 리전 장애 발생 시 리디렉션에는 탁월하나 데이터 손상에는 취약함. 글로벌  테이블에서 새로 작성된 항목은 1 초 이내에 모든 복제본 테이블에 전파되는데, 이는  데이터를 잘못 건드리면 1 초 이내에 모든 복제본 테이블에 해당 변경 사항이 적용되기  때문.  전역 테이블에서 새로 작성된 항목은 일반적으로 1 초 이내에 모든 복제본 테이블에  전파됩니다.  https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/V2globaltables_H owItWorks.html  B(O) : DynamoDB 는 주문형 백업 기능을 제공합니다. 이를 통해 규정 준수 요구 사항에  대한 장기 보존 및 보관을 위해 테이블의 전체 백업을 생성할 수 있습니다. 주문형 백업을  생성하고 Amazon DynamoDB 테이블에 대한 특정 시점 복구를 활성화할 수 있습니다.  지정 시간 복구는 우발적인 쓰기 또는 삭제 작업으로부터 

---
## Question 2 - [#453] [recall]
> 회사에서 Amazon EC2 데이터 및 여러 Amazon S3 버킷에 대한 백업 전략을 구현하려고  합니다. 규정 요구 사항으로 인해 회사는 특정 기간 동안 백업 파일을 보존해야 합니다.  회사는 보유기간 동안 파일을 변조해서는 안됩니다.  이러한 요구 사항을 충족하는 솔루션은 무엇입니까?

> - **A**: AWS Backup 을 사용하여 거버넌스 모드에서 볼트 잠금이 있는 백업 볼트를 생성합니다.   필요한 백업 계획을 생성합니다.
> - **B**: Amazon Data Lifecycle Manager 를 사용하여 필요한 자동 스냅샷 정책을 생성합니다.
> - **C**: Amazon S3 파일 게이트웨이를 사용하여 백업을 생성합니다. 적절한 S3 수명 주기  관리를 구성합니다.
> - **D**: AWS Backup 을 사용하여 규정 준수 모드에서 볼트 잠금이 있는 백업 볼트를 생성합니다.  필요한 백업 계획을 생성합니다.

> [!answer]- 정답 보기
> **정답: D**
>
> AWS Backup 은 컴퓨팅, 스토리지 및 데이터베이스 전반에서 AWS 서비스의 데이터 보호를  중앙 집중화하고 자동화할 수 있는 완전 관리형 서비스입니다. AWS Backup Vault Lock 은  백업 볼트에 대한 보안 및 제어를 강화하는 데 도움이 되는 백업 볼트의 선택적 기능입니다.  규정 준수 모드에서 잠금이 활성화되고 유예 시간이 끝나면 고객, 계정/데이터 소유자 또는  AWS 가 볼트 구성을 변경하거나 삭제할 수 없습니다. 이렇게 하면 보존 기간이 만료되고  규정 요구 사항을 충족할 때까지 백업을 사용할 수 있습니다.    참조:  https://docs.aws.amazon.com/aws-backup/latest/devguide/vaultlock.html

---
## Question 3 - [#618] [recall]
> 한 회사에서는 us-east-1 리전에 볼륨으로 마운트된 SMB 파일 공유가 있는 Amazon EC2  인스턴스에 Amazon FSx for Windows File Server 를 사용하려고 합니다. 회사는 계획된  시스템 유지 관리 또는 계획되지 않은 서비스 중단에 대해 5 분의 복구 지점 목표(RPO)를  가지고 있습니다. 회사는 파일 시스템을 us-west-2 리전에 복제해야 합니다. 복제된  데이터는 5 년 동안 어떤 사용자도 삭제해서는 안 됩니다.  어떤 솔루션이 이러한 요구 사항을 충족합니까?

> - **A**: 단일 AZ 2 배포 유형을 사용하는 us-east-1 에 FSx for Windows File Server 파일  시스템을 생성합니다. AWS Backup 을 사용하여 백업을 us-west-2 에 복사하는 백업 규칙이  포함된 일일 백업 계획을 생성합니다. us-west-2 의 대상 볼트에 대해 규정 준수 모드로  AWS Backup Vault Lock 을 구성합니다. 최소 기간을 5 년으로 구성합니다.
> - **B**: 다중 AZ 배포 유형이 있는 us-east-1 에 FSx for Windows File Server 파일 시스템을  생성합니다. AWS Backup 을 사용하여 백업을 us-west-2 에 복사하는 백업 규칙이 포함된  일일 백업 계획을 생성합니다. us-west-2 의 대상 볼트에 대해 거버넌스 모드에서 AWS  Backup Vault Lock 을 구성합니다. 최소 기간을 5 년으로 구성합니다.
> - **C**: 다중 AZ 배포 유형이 있는 us-east-1 에 FSx for Windows File Server 파일 시스템을  생성합니다. AWS Backup 을 사용하여 백업을 us-west-2 에 복사하는 백업 규칙이 포함된  일일 백업 계획을 생성합니다. us-west-2 의 대상 볼트에 대해 규정 준수 모드로 AWS  Backup Vault Lock 을 구성합니다. 최소 기간을 5 년으로 구성합니다.
> - **D**: 단일 AZ 2 배포 유형이 있는 us-east-1 에 FSx for Windows File Server 파일 시스템을  생성합니다. AWS Backup 을 사용하여 백업을 us-west-2 에 복사하는 백업 규칙이 포함된  일일 백업 계획을 생성합니다. us-west-2 의 대상 볼트에 대해 거버넌스 모드에서 AWS  Backup Vault Lock 을 구성합니다. 최소 기간을 5 년으로 구성합니다.

> [!answer]- 정답 보기
> **정답: C**
>
> 

---
## Question 4 - [#178] [recall]
> 회사의 인프라는 단일 AWS 리전에 있는 Amazon EC2 인스턴스와 Amazon RDS DB  인스턴스로 구성됩니다. 회사는 별도의 리전에 데이터를 백업하려고 합니다.  최소한의 운영 오버헤드로 이러한 요구 사항을 충족하는 솔루션은 무엇입니까?

> - **A**: AWS Backup 을 사용하여 EC2 백업과 RDS 백업을 별도의 리전에 복사합니다.
> - **B**: Amazon Data Lifecycle Manager(Amazon DLM)를 사용하여 EC2 백업 및 RDS 백업을  별도의 리전에 복사합니다.
> - **C**: EC2 인스턴스의 Amazon 머신 이미지(AMI)를 생성합니다. AMI 를 별도의 리전에  복사합니다. 별도의 리전에서 RDS DB 인스턴스에 대한 읽기 전용 복제본을 생성합니다.
> - **D**: Amazon Elastic Block Store(Amazon EBS) 스냅샷을 생성합니다. EBS 스냅샷을 별도의  리전에 복사합니다. RDS 스냅샷을 생성합니다. RDS 스냅샷을 Amazon S3 로 내보냅니다. S3  CRR(Cross-Region Replication)을 별도의 리전에 구성합니다.

> [!answer]- 정답 보기
> **정답: A**
>
> AWS Backup 을 사용하여 EC2 및 RDS 백업을 별도의 리전에 복사하는 것은 최소한의 운영  오버헤드로 요구 사항을 충족하는 솔루션입니다. AWS Backup 은 백업 프로세스를  간소화하고 백업을 다른 리전으로 자동 복사하여 EC2 인스턴스 및 RDS 데이터베이스에  대한 별도의 백업 프로세스 관리와 관련된 수동 작업 및 운영 복잡성을 줄입니다.    B: Amazon Data Lifecycle Manager(Amazon DLM)가 RDS 백업을 별도의 리전에 직접  복사하도록 설계되지 않았기 때문에 올바르지 않습니다.  C: Amazon 머신 이미지(AMI) 및 읽기 전용 복제본을 생성하면 전용 백업 솔루션에 비해  복잡성과 운영 오버헤드가 추가되기 때문에 올바르지 않습니다.  D: Amazon EBS 스냅샷, RDS 스냅샷 및 S3 CRR(Cross-Region Replication)을 사용하려면  여러 수동 단계와 추가 구성이 수반되어 복잡성이 증가하기 때문에 올바르

---
## Question 5 - [#217] [recall]
> 회사는  Application  Load  Balancer  뒤의  Amazon  EC2  인스턴스에서  글로벌  웹  애플리케이션을 실행합니다. 애플리케이션은 Amazon Aurora 에 데이터를 저장합니다.  회사는 재해 복구 솔루션을 만들어야 하며 최대 30 분의 다운타임과 잠재적인 데이터  손실을 허용할 수 있습니다. 솔루션은 기본 인프라가 정상일 때 부하를 처리할 필요가  없습니다.  솔루션 설계자는 이러한 요구 사항을 충족하기 위해 무엇을 해야 합니까?

> - **A**: 필요한 인프라 요소가 있는 애플리케이션을 배치합니다. Amazon Route 53 을 사용하여  활성-수동 장애 조치를 구성합니다. 두 번째 AWS 리전에서 Aurora 복제본을 생성합니다.
> - **B**: 두 번째 AWS 리전에서 애플리케이션의 축소된 배포를 호스팅합니다. Amazon Route  53 을 사용하여 활성-활성 장애 조치를 구성합니다. 두 번째 리전에서 Aurora 복제본을  생성합니다.
> - **C**: 두 번째 AWS 리전에서 기본 인프라를 복제합니다. Amazon Route 53 을 사용하여  활성-활성 장애 조치를 구성합니다. 최신 스냅샷에서 복원된 Aurora 데이터베이스를  생성합니다.
> - **D**: AWS Backup 으로 데이터를 백업합니다. 백업을 사용하여 두 번째 AWS 리전에 필요한  인프라를 생성합니다. Amazon Route 53 을 사용하여 활성-수동 장애 조치를 구성합니다. 두  번째 리전에서 Aurora 두 번째 기본 인스턴스를 생성합니다.

> [!answer]- 정답 보기
> **정답: A**
>
> 솔루션은 기본 인프라가 정상일 때 부하를 처리할 필요가 없다고 했으므로 Active/Passive  Failover 를 사용하면 됨. 따라서 A,D 둘 중 하나가 답.  A(O) : Q: Amazon Aurora 는 교차 리전 복제를 지원하나요? 예. 물리적 또는 논리적 복제를  사용하여 교차 리전 Aurora 복제본을 설정할 수 있습니다. Amazon RDS 콘솔에서 교차   리전 복제본을 새로운 기본 복제본으로 승격할 수 있습니다. 논리적(binlog) 복제의 경우,  승격 프로세스는 워크로드에 따라 다르지만 보통 몇 분 정도 걸립니다. 승격 프로세스를  시작하면 교차 리전 복제가 중단됩니다. https://aws.amazon.com/ko/rds/aurora/faqs/  D(X) : 굳이 AWS Backup 을 사용하지 않아도 오로라 교차 리전 복제본 (Aurora Cross  Region Replica)를 사용하면 됨. 그리고 글로벌 웹 애플리케이션을 사용한다고 했는데 이런  

---
## Question 6 - [#273] [application]
> 빠르게 성장하는 전자상거래 회사는 단일 AWS 리전에서 워크로드를 실행하고 있습니다.  솔루션 설계자는 다른 AWS 리전을 포함하는 재해 복구(DR) 전략을 생성해야 합니다.  회사는 대기 시간을 최소화하면서 DR 지역에서 데이터베이스를 최신 상태로 유지하기를  원합니다. DR 지역의 나머지 인프라는 감소된 용량으로 실행되어야 하며 필요한 경우  확장할 수 있어야 합니다.  가장 낮은 RTO(복구 시간 목표)로 이러한 요구 사항을 충족하는 솔루션은 무엇입니까?

> - **A**: 파일럿 라이트 배포와 함께 Amazon Aurora 글로벌 데이터베이스를 사용합니다.
> - **B**: 웜 대기 배포와 함께 Amazon Aurora 글로벌 데이터베이스를 사용합니다.
> - **C**: 파일럿 라이트 배포와 함께 Amazon RDS 다중 AZ DB 인스턴스를 사용합니다.
> - **D**: 웜 대기 배포와 함께 Amazon RDS 다중 AZ DB 인스턴스를 사용합니다.

> [!answer]- 정답 보기
> **정답: B**
>
> ・ 웜 스탠바이는 감소된 수준의 트래픽을 즉시 처리할 수 있습니다. 그런 다음 이 기존  배포를 확장해야 하므로 파일럿 라이트보다 RTO 시간이 더 짧습니다. 파일럿 라이트를  사용하려면 먼저 인프라를 배포한 다음 워크로드가 요청을 처리할 수 있기 전에 리소스를  확장해야 하기 때문입니다.  https://aws.amazon.com/ko/blogs/architecture/disaster-recovery-dr-architecture-on-aw s-part-iii-pilot-light-and-warm-standby/  A(X) : 파일럿 라이트를 사용하기 때문에 오답.  B(O) : Amazon Aurora 글로벌 데이터베이스는 여러 리전에 걸쳐 자동으로 복제를 진행  Amazon Aurora Global Database 는 단일 Amazon Aurora 데이터베이스를 여러 AWS  리전으로 확장할 수 있는 기능입니다. 데이터베이스 성능에 전혀 영향을 주지 않고   데이터를 복제하고, 

---
## Question 7 - [#475] [application]
> 회사에서 Amazon Elastic Container Service(Amazon ECS)를 사용할 컨테이너화된  애플리케이션을 설계하고 있습니다. 애플리케이션은 내구성이 뛰어나고 RPO(복구 지점  목표)가 8 시간인 다른 AWS 리전에 데이터를 복구할 수 있는 공유 파일 시스템에  액세스해야 합니다. 파일 시스템은 리전 내의 각 가용 영역에 탑재 대상을 제공해야  합니다.  솔루션 설계자는 AWS Backup 을 사용하여 다른 리전에 대한 복제를 관리하려고 합니다.  이러한 요구 사항을 충족하는 솔루션은 무엇입니까?

> - **A**: 다중 AZ 배포가 있는 Windows 파일 서버용 Amazon FSx
> - **B**: 다중 AZ 배포가 있는 NetApp ONTAP 용 Amazon FSx
> - **C**: 표준 스토리지 클래스가 있는 Amazon Elastic File System(Amazon EFS)
> - **D**: OpenZFS 용 Amazon FSx

> [!answer]- 정답 보기
> **정답: C**
>
> 

---
## Question 8 - [#539] [analysis]
> 회사에서 AWS 클라우드를 사용하여 온프레미스 DR(재해 복구) 구성을 개선하려고 합니다.  회사의 핵심 프로덕션 비즈니스 애플리케이션은 가상 머신(VM)에서 실행되는 Microsoft  SQL Server Standard 를 사용합니다. 애플리케이션의 RPO(복구 시점 목표)는 30 초  이하이고 RTO(복구 시간 목표)는 60 분입니다. DR 솔루션은 가능한 한 비용을 최소화해야  합니다.  이러한 요구 사항을 충족하는 솔루션은 무엇입니까?

> - **A**: Always On 가용성 그룹과 함께 Microsoft SQL Server Enterprise 를 사용하여 온프레미스  서버와 AWS 간에 다중 사이트 활성/활성 설정을 구성합니다.
> - **B**: AWS 에서 SQL Server 데이터베이스용 웜 대기 Amazon RDS 를 구성합니다. 변경 데이터  캡처(CDC)를 사용하도록 AWS DMS(AWS Database Migration Service)를 구성합니다.
> - **C**: 디스크 변경 사항을 AWS 에 파일럿 라이트로 복제하도록 구성된 AWS Elastic Disaster  Recovery 를 사용합니다.
> - **D**: 타사 백업 소프트웨어를 사용하여 매일 밤 백업을 캡처합니다. Amazon S3 에 보조 백업  세트를 저장합니다.

> [!answer]- 정답 보기
> **정답: B**
>
> 

---

> [!summary]- 패턴 요약 (클릭하여 보기)
> DR 전략: Backup < Pilot Light < Warm Standby < Active-Active
> RTO = 복구 시간 / RPO = 데이터 손실 허용 시간
>
> 취약 개념 발견 시 -> [[Exam Traps]] 참조
