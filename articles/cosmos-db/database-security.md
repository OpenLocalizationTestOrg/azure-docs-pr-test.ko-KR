---
title: "aaaDatabase 보안-Azure Cosmos DB | Microsoft Docs"
description: "Azure Cosmos DB에서 데이터에 대해 데이터베이스 보호 및 데이터 보안을 제공하는 방법을 알아봅니다."
keywords: "nosql 데이터베이스 보안, 정보 보안, 데이터 보안, 데이터베이스 암호화, 데이터베이스 보호, 보안 정책, 보안 테스트"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: a02a6a82-3baf-405c-9355-7a00aaa1a816
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: mimig
ms.openlocfilehash: 85ffa62f611bfad00bf3fc5dbe536f91f97f1113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-database-security"></a>Azure Cosmos DB 데이터베이스 보안

이 문서에서는 데이터베이스 보안 모범 사례를 설명 하 고 방지 하 고 검색 toodatabase 위반 응답 Azure Cosmos DB toohelp에서 제공 되는 주요 기능입니다.
 
## <a name="whats-new-in-azure-cosmos-db-security"></a>Azure Cosmos DB 보안의 새로운 기능은 무엇인가요?

이제 휴지 상태의 암호화를 모든 Azure 지역에서 Azure Cosmos DB에 저장된 문서 및 백업에 대해 사용할 수 있습니다. 이러한 영역의 신규 및 기존 고객에 대해 미사용 데이터의 암호화가 자동으로 적용됩니다. 부분이 필요 tooconfigure 없습니다. 수 있게 마찬가지로 전에 hello 혜택 알 데이터 안전 하 게 미사용 데이터 암호화와 같은 훌륭한 대기 시간, 처리량, 가용성 및 기능 hello 합니다.

## <a name="how-do-i-secure-my-database"></a>내 데이터베이스를 보호하려면 어떻게 하나요? 

데이터 보안은 사용자, hello 고객와 데이터베이스 공급자 간에 공유 책임입니다. 선택한 hello 데이터베이스 공급자에 따라 수행 하는 책임 hello 양을 달라질 수 있습니다. 온-프레미스 솔루션을 선택 하면 필요한 tooprovide 끝점 보호 toophysical 보안-은 간단한 작업이 있는 하드웨어에서 모든 항목입니다. Azure Cosmos DB와 같은 PaaS 클라우드 데이터베이스 공급자를 선택할 경우 관여해야 하는 부분이 상당히 줄어듭니다. 이미지, Microsoft의에서 빌려 온 다음 hello [클라우드 컴퓨팅에 대 한 책임을 공유](https://aka.ms/sharedresponsibility) 백서를 Azure Cosmos DB와 같은 PaaS 공급자와 함께 사용자의 책임 감소 하는 방법을 보여 줍니다.

![고객 및 데이터베이스 공급자 책임](./media/database-security/nosql-database-security-responsibilities.png)

이전 다이어그램에서는 높은 수준의 클라우드 보안 구성 요소를 hello 하지만 항목 필요 한가요 tooworry에 대 한 데이터베이스 솔루션에 맞게? 와 다른 솔루션 tooeach를 어떻게 수 있습니까? 

Hello를 요구 사항 검사 목록에 나오는 toocompare 데이터베이스 시스템에 사용 하는 것이 좋습니다.

- 네트워크 보안 및 방화벽 설정
- 사용자 인증 및 세분화된 사용자 제어
- 국가별 오류에 대 한 전역적으로 tooreplicate 데이터 기능
- 기능 tooperform 장애 조치의 데이터 센터 tooanother
- 데이터 센터 내에서 로컬 데이터 복제
- 자동 데이터 백업
- 백업에서 삭제된 데이터 복원
- 중요한 데이터 보호 및 격리
- 공격 모니터링
- Tooattacks 응답
- 기능 toogeo fence 데이터 tooadhere toodata 거 버 넌 스 제한
- 보호된 데이터 센터에서 서버의 물리적 보호

확실 한, 최근 보일 수 있지만 및 [대규모 데이터베이스 위반](http://thehackernews.com/2017/01/mongodb-database-security.html) 나중에 요구 사항을 준수 하는 hello의 hello 간단 하지만 중요 한 중요도 기억할:
- Toodate 위로 유지 되는 패치가 적용 된 서버
- HTTPS(기본값)/SSL 암호화
- 강력한 암호를 사용하는 관리 계정

## <a name="how-does-azure-cosmos-db-secure-my-database"></a>Azure Cosmos DB는 내 데이터베이스를 어떻게 보호하나요?

Hello 목록 앞에 다시 살펴 보겠습니다-이러한 보안 요구 사항을의 개수는 Azure Cosmos DB 제공? 하나씩 모두 살펴봅니다.

구체적으로 자세히 살펴보겠습니다.

|보안 요구 사항|Azure Cosmos DB의 보안 접근 방식|
|---|---|---|
|네트워크 보안|IP 방화벽을 사용 하 여 hello 첫 번째 수준의 보호 toosecure 데이터베이스 됩니다. Azure Cosmos DB는 인바운드 방화벽 지원을 위해 정책 중심 IP 기반 액세스 제어를 지원합니다. hello IP 기반 액세스 제어는 기존 데이터베이스 시스템에서 사용 하는 비슷한 toohello 방화벽 규칙이 있지만 Azure Cosmos DB 데이터베이스 계정에 컴퓨터 또는 클라우드 서비스의 승인 된 집합에서 액세스할 수 있도록 확장 됩니다. <br><br>Azure Cosmos DB 특정 IP 주소 (168.61.48.0), IP 범위 (168.61.48.0/8) 및 Ip 및 범위를 조합해 tooenable 있습니다를 수 있습니다. <br><br>이 허용된 목록 이외의 컴퓨터에서 보내는 모든 요청은 Azure Cosmos DB에서 차단됩니다. 요청에서 컴퓨터를 승인 하며 클라우드 서비스 다음을 완료 해야 hello 인증 프로세스 toobe toohello 리소스를 제어 하는 액세스를 제공 합니다.<br><br>자세한 내용은 [Azure Cosmos DB 방화벽 지원](firewall-support.md)을 참조하세요.|
|권한 부여|Azure Cosmos DB는 권한 부여를 위해 HMAC(해시 기반 메시지 인증 코드)를 사용합니다. <br><br>Hello 비밀 계정 키를 사용 하 여 각 요청은 해시 및 hello 다음 s e-64로 인코딩된 해시 각 호출 tooAzure Cosmos DB와 함께 보내집니다. hello Azure Cosmos DB 서비스 사용 하 여 hello 올바른 비밀 키와 속성 toogenerate 해시를 다음 hello 요청에 hello 하나 있는 hello 값과 비교 toovalidate hello 요청 합니다. Hello 두 값이 일치 하 고 hello 작업이 성공적으로 인증 되는지 hello 요청은 처리, 그렇지 않으면 인증 실패로 이며 hello 요청이 거부 됩니다.<br><br>하나를 사용할 수는 [마스터 키](secure-access-to-data.md#master-keys), 또는 [리소스 토큰](secure-access-to-data.md#resource-tokens) 문서와 같은 tooa 리소스 세밀 한 액세스를 허용 합니다.<br><br>자세한 내용을 알아보세요 [tooAzure Cosmos DB 리소스 액세스 보안](secure-access-to-data.md)합니다.|
|사용자 및 사용 권한|Hello를 사용 하 여 [마스터 키](#master-key) hello 계정에 대 한 사용자 리소스 및 사용 권한 리소스 데이터베이스당 만들 수 있습니다. A [리소스 토큰](#resource-token) 권한과 데이터베이스에 연결 되며 hello 사용자가 액세스할 수 있는지 여부를 결정 (읽기 / 쓰기, 읽기 전용 또는 권한 없음) tooan 응용 프로그램 데이터베이스의 리소스에 hello 합니다. 응용 프로그램 리소스에는 컬렉션, 문서, 첨부 파일, 저장 프로시저, 트리거 및 UDF가 포함됩니다. hello 리소스 토큰은 다음 인증 tooprovide 중에 사용 하거나 toohello 리소스 액세스를 거부 합니다.<br><br>자세한 내용을 알아보세요 [tooAzure Cosmos DB 리소스 액세스 보안](secure-access-to-data.md)합니다.|
|Active Directory 통합(RBAC)| 또한이 테이블 다음에 나오는 hello 스크린샷에 표시 된 대로 액세스 제어 (IAM)를 사용 하 여 hello Azure 포털에서에서 액세스 toohello 데이터베이스 계정을 제공할 수 있습니다. IAM은 역할 기반 액세스 제어를 제공하며 Active Directory와 통합됩니다. 개인 및 hello 다음 이미지와 같이 그룹에 대 한 기본 제공된 역할 또는 사용자 지정 역할을 사용할 수 있습니다.|
|글로벌 복제|Azure Cosmos DB 단추의 hello로 Azure의 전세계 데이터 센터 중 하나를 클릭 하 여 데이터 tooany tooreplicate를 사용 하면 턴키 글로벌 배포를 제공 합니다. 전역 복제를 사용 하 여 hello 전 세계 tooyour 데이터 대기 시간이 짧은 액세스를 제공 하 고 전역으로 확장할 수 있습니다.<br><br>보안의 hello 컨텍스트에서 전역 복제 국가별 장애 로부터 데이터 보호를 시나리오.<br><br>[데이터를 글로벌 배포](distribute-data-globally.md)에 대한 자세한 정보|
|지역별 장애 조치|데이터를 둘 이상의 데이터 센터에 복제한 경우 지역 데이터 센터가 오프라인으로 전환되면 Azure Cosmos DB가 사용자 작업을 자동으로 롤오버합니다. 데이터가 복제 되어 hello 영역을 사용 하 여 장애 조치 지역 우선 순위가 지정 된 목록을 만들 수 있습니다. <br><br>[Azure Cosmos DB의 지역별 장애 조치(Failover)](regional-failover.md)에서 자세히 알아보세요.|
|로컬 복제|단일 데이터 센터 내 에서도 Azure Cosmos DB 자동으로 데이터를 복제 나타낼 때 항상 사용 가능한 다양 한 hello [일관성 수준](consistency-levels.md)합니다. 이렇게 하면  [99.99% 작동 시간 가용성 SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db)가 보장되고 다른 데이터베이스 서비스가 제공할 수 없는 재정적 보장이 함께 제공됩니다.|
|자동 온라인 백업|Azure Cosmos DB 데이터베이스는 정기적으로 백업되며 georedundant 저장소에 저장됩니다. <br><br>[Azure Cosmos DB로 자동 온라인 백업 및 복원](online-backup-and-restore.md)에서 자세히 알아보세요.|
|삭제된 데이터 복원|hello 자동화 된 온라인 백업 데이터가 될 수 있습니다 사용된 toorecover 수 실수로 삭제 한를 너무 ~ hello 이벤트가 발생 한 후 30 일입니다. <br><br>[Azure Cosmos DB로 자동 온라인 백업 및 복원](online-backup-and-restore.md)에서 자세히 알아보세요.|
|중요한 데이터 보호 및 격리|Hello 지역에 나열 된 모든 데이터 [새로운?](#whats-new) 이제 휴지 암호화 됩니다.<br><br>PII 및 다른 기밀 데이터 수 격리 toospecific 컬렉션 및 읽기 / 쓰기 또는 읽기 전용 액세스로 제한 toospecific 사용자 일 수 있습니다.|
|공격 모니터|감사 로깅 및 활동 로그를 사용하여 계정에서 정상 및 비정상적인 활동을 모니터링할 수 있습니다. Hello 작업이 발생 한 hello 상태 hello 작업 및 다음이 표는 hello 스크린 샷에 표시 된 것 처럼 훨씬 더 hello 작업을 시작한 사용자 리소스에 대해 어떤 작업이 볼 수 있습니다.|
|Tooattacks 응답|Azure 지원 tooreport 잠재적 공격 연결한, 되 면 5 단계 사고 대응 프로세스는 시작 됩니다. hello 5 단계 과정의 hello 목표 문제가 감지 될 한 확인이 시작 된 후 toorestore 일반 서비스 보안 및 작업 최대한 빨리입니다.<br><br>자세한 내용을 알아보세요 [hello 클라우드에서에서 Microsoft Azure 보안 응답](https://aka.ms/securityresponsepaper)합니다.|
|지오-펜싱|Azure Cosmos DB는 독립적인 지역(예: 독일, 중국, US Gov)에 대해 데이터 거버넌스 및 준수를 보장합니다.|
|보호된 기능|Azure Cosmos DB의 데이터는 SSD의 Azure 보호된 데이터 센터에 저장됩니다.<br><br>[Microsoft 글로벌 데이터 센터](https://www.microsoft.com/en-us/cloud-platform/global-datacenters)에 대한 자세한 정보|
|HTTPS/SSL/TLS 암호화|모든 클라이언트-서비스 Azure Cosmos DB 상호 작용에는 SSL/TLS 1.2가 적용됩니다. 또한 모든 데이터 센터 내부 및 데이터 센터 간 복제에는 SSL/TLS 1.2가 적용됩니다.|
|휴지 상태의 암호화|Azure Cosmos DB에 저장된 모든 데이터는 미사용 암호화됩니다. 자세한 내용은 [Azure Cosmos DB 미사용 암호화](.\database-encryption-at-rest.md)를 참조하세요.|
|패치된 서버|관리 되는 데이터베이스와 Azure Cosmos DB hello 필요 toomanage 및 패치 서버를 자동으로 수행 되를 제거 합니다.|
|강력한 암호를 사용하는 관리 계정|하드 toobelieve 것에 필요 toomention이 요구이 사항은 일부 경쟁사와는 달리 Azure Cosmos DB에서 암호가 없는 불가능 한 toohave 관리 계정을 없지만 합니다.<br><br> SSL 및 HMAC 비밀 기반 인증을 통한 보안이 기본적으로 반영됩니다.|
|보안 및 데이터 보호 인증서|Azure Cosmos DB에는 [ISO 27001](https://www.microsoft.com/en-us/TrustCenter/Compliance/ISO-IEC-27001), [EUMC(European Model Clauses)](https://www.microsoft.com/en-us/TrustCenter/Compliance/EU-Model-Clauses) 및 [HIPAA](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA) 인증이 있습니다. 기타 인증서는 현재 작업 중입니다.|

hello 다음 스크린샷은 액세스 제어 (IAM)를 사용 하 여 Active directory 통합 (RBAC) hello Azure 포털에서에서: ![hello 데이터베이스 보안을 보여 주는-Azure 포털에서에서 액세스 제어 (IAM)](./media/database-security/nosql-database-security-identity-access-management-iam-rbac.png)

hello 다음 스크린샷은 감사 로깅을 사용 하는 방법 및 활동 로그 toomonitor 계정: ![Azure Cosmos DB에 대 한 활동 로그](./media/database-security/nosql-database-security-application-logging.png)

## <a name="next-steps"></a>다음 단계

마스터 키와 리소스 토큰에 대 한 자세한 내용은 참조 하십시오. [보안 액세스 tooAzure Cosmos DB 데이터](secure-access-to-data.md)합니다.

Microsoft 인증서에 대한 자세한 내용은 [Azure 보안 센터](https://azure.microsoft.com/support/trust-center/)를 참조하세요.
