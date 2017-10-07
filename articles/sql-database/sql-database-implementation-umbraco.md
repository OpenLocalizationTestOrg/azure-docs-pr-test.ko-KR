---
title: "SQL 데이터베이스 Azure 사례 연구-aaaAzure Umbraco | Microsoft Docs"
description: "Umbraco hello 클라우드의 SQL 데이터베이스 tooquickly 프로 비전 및 수천 개의 테 넌 트에 대 한 서비스를 확장을 사용 방법에 대해 알아보기"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5243d31e-3241-4cb0-9470-ad488ff28572
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 93e39e509831a5ff90f129d9537ece0b0dafef0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="umbraco-uses-azure-sql-database-tooquickly-provision-and-scale-services-for-thousands-of-tenants-in-hello-cloud"></a>Umbraco는 Azure SQL 데이터베이스 tooquickly 프로 비전 및 수천 개의 테 넌 트에 대 한 크기 조정 서비스를 사용 하 여 hello 클라우드에서
![Umbraco 로고](./media/sql-database-implementation-umbraco/umbracologo.png)

Umbraco는에서 실행할 수 있는 아무 것도 작은 캠페인 또는 브로슈어 사이트 toocomplex Fortune 500 대 기업 및 글로벌 미디어 웹 사이트 응용 프로그램 인기 있는 오픈 소스 콘텐츠 관리 시스템 (CMS)입니다. 

> "은 매우 큰 커뮤니티 Umbraco 실행 당사 포럼 및는 라이브 350, 000 개 이상의 사이트에 100, 000 개 이상의 개발자와 hello 시스템을 사용 하는 개발자의 했습니다."
> 
> - Umbraco기술 책임자, Morten Christensen
> 
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-Case-Study-Umbraco/player]
> 
> 

Umbraco Umbraco-as a Service (Uaa)에 추가 toosimplify 고객 배포: 온-프레미스 배포에 대 한 hello 필요성을 제거 하는 소프트웨어-as a service (SaaS) 제공 하는 기본 제공 확장을 제공 하 고 사용 하 여 관리 오버 헤드 제거 제품 솔루션 대신 혁신 관리에서 개발자 toofocus 합니다. Umbraco는에서 사용 하 여 이러한 혜택을 모두 Microsoft Azure에서 제공 하는 유연한 플랫폼으로-서비스 (PaaS) 모델 hello 수 tooprovide입니다.

Uaa SaaS 고객 toouse Umbraco CMS를 사용 하면 자신의 공격자 로부터 이전에 있던 기능입니다. 이러한 고객은 프로덕션 데이터베이스를 포함하는 작업 CMS 환경으로 프로비전됩니다. 고객은 개발 및 스테이징 환경의 요구 사항에 따라 tootwo 추가 데이터베이스를 추가할 수 있습니다. 새 환경이 요청되면 자동화된 프로세스가 해당 고객에게 데이터베이스를 자동으로 할당합니다. hello 새 데이터베이스는 hello 데이터베이스에 이미 미리 프로 비전 하 여 사용 가능한 데이터베이스 (그림 1 참조) Azure 탄력적 풀에서 Umbraco 때문에 (초)을 준비 합니다.

![Umbraco 프로비전 수명 주기](./media/sql-database-implementation-umbraco/figure1.png)

그림 1. UaaS(Umbraco as a Service)에 대한 프로비전 수명 주기

## <a name="azure-elastic-pools-and-automation-simplify-deployments"></a>Azure 탄력적 풀 및 자동화로 배포 간소화
Azure SQL 데이터베이스 및 기타 Azure 서비스를 사용하여 Umbraco 고객은 자신의 환경을 자체 프로비전할 수 있으며, Umbraco는 직관적인 워크플로의 일부로 데이터베이스를 쉽게 모니터링하고 관리할 수 있습니다.

1. 프로비전
   
   Umbraco는 탄력적 풀에서 사용할 수 있는 미리 프로비전된 200개의 데이터베이스 용량을 유지 관리합니다. 새 고객이 Uaa에 등록할 때 Umbraco hello 가용성 풀에서 데이터베이스를 할당 하 여 거의 실시간으로 새 CMS 환경 사용 하 여 hello 고객을 제공 합니다.
   
   가용성 풀 임계값에 도달 하면 새 탄력적 풀을 만들고 새 데이터베이스를 미리 프로 비전된 toobe 필요에 따라 toocustomers를 할당 합니다.
   
   구현은 C# 관리 라이브러리 및 Azure 서비스 버스 큐를 사용하여 완전하게 자동화되었습니다.
2. 활용
   
   고객에 하나를 사용 toothree 환경 (예: 프로덕션, 스테이징 및/또는 개발), 각 자체 데이터베이스입니다. Umbraco tooprovide 효율적인 tooover 프로 비전 하지 않고도 확장을 사용 하면 탄력적 풀, 고객 데이터베이스는 있습니다.
   
   ![Umbraco 프로젝트 개요](./media/sql-database-implementation-umbraco/figure2.png)
   
   ![Umbraco 프로젝트 세부 정보](./media/sql-database-implementation-umbraco/figure3.png)
   
   그림 2. 프로젝트 개요 및 세부 정보를 표시하는 UaaS(Umbraco-as a Service) 고객 웹 사이트
   
   Azure SQL 데이터베이스 데이터베이스 트랜잭션 단위 (DTUs) toorepresent hello 상대적 우위 실제 데이터베이스 트랜잭션에 필요한를 사용 합니다. Uaa 고객에 대 한 데이터베이스는 일반적으로 약 10 개 Dtu에서 작동 하지만 각 요청 시 탄력성 tooscale hello에 합니다. 즉, UaaS는 사용량이 최대인 시간에도 고객에게 필요한 리소스가 항상 유지되도록 합니다. 예를 들어 최근 일요일 스포츠 이벤트 중 하나의 Uaa 고객 발생 too100 Dtu 데이터베이스 최대치를 hello 게임의 hello 기간에 대 한 했습니다. Azure 탄력적 풀 있게 Umbraco toosupport 성능 저하 없이 해당 많이 필요 합니다.
3. 모니터
   
   Umbraco 모니터 데이터베이스 hello 사용자 지정 전자 메일 경고와 함께 Azure 포털 내에서 대시보드를 사용 하 여 작업 합니다.
4. 재해 복구
   
   Azure는 두 가지 DR(재해 복구) 옵션을 제공합니다. 바로 활성 지역 복제와 지역에서 복원 기능입니다. hello 회사를 선택 해야 하는 DR 옵션에 따라 다릅니다. 해당 [비즈니스 연속성 목표](sql-database-business-continuity.md)합니다.
   
   활성 지리적 복제는 hello 가장 빠른 수준의 가동 중지 시간의 hello 이벤트에 응답을 제공합니다. 활성 지리적 복제를 사용 하 여 서로 다른 지역에 서버의 toofour 읽기 가능한 보조 복제본을 만들 수 있습니다 및 실패 하는 hello 이벤트 hello 보조 복제본의 장애 조치 tooany를 시작할 수 있습니다.
   
   Umbraco는 지리적 복제, 필요 하지 않지만 활용지 않습니다 toohelp Azure 지역에서 복원은의 중단의 hello 이벤트에서 최소 가동 중지 시간을 확인 합니다. 지리적 복원은 지역 중복 Azure Storage의 데이터베이스 백업을 사용합니다. Hello 기본 지역에서 중단 될 때 백업 복사본에서 사용자가 toorestore를 허용 합니다.
5. 프로비전 해제
   
   프로젝트 환경이 삭제되면 연결된 모든 데이터베이스(개발, 스테이징 또는 라이브)가 Azure 서비스 버스 큐 정리 동안 제거됩니다. 이러한 프로세스를 자동 복원을 hello 사용 하지 않는 데이터베이스 tooUmbraco 탄력적 데이터베이스 가용성 풀에 최대 사용률을 유지 하면서 이후 프로 비전에 사용할 수 있도록 합니다.

## <a name="elastic-pools-allow-uaas-tooscale-with-ease"></a>탄력적 풀을 손쉽게 Uaa tooscale 허용
Azure 탄력적 풀을 이용 Umbraco tooover 또는 아래 프로 비전 하지 않고도 고객에 대 한 성능을 최적화할 수 있습니다. Umbraco 현재 데이터베이스가 거의 3000 19 탄력적 풀에 걸쳐, hello 기능 tooeasily와 확장 필요한 tooaccommodate로 자신의 기존 325,000 고객 또는 새 고객은 준비 toodeploy hello 클라우드에서 CMS입니다.

사실, tooMorten Christensen, Umbraco에서 기술 리드에 따라 "Uaa 이제 발생 하는 하루에 약 30 새로운 고객의 증가 합니다. 고객은 hello 시간 (초)에서 수 tooprovision 새 프로젝트를 있다는 탐, 즉시 '한 번의 클릭 배포'를 사용 하 여 개발 환경에서 업데이트 tootheir 라이브 사이트 게시 하 고 오류를 찾을 경우 처럼 신속 하 게 변경 합니다 . "

고객에게 두 번째 및/또는 세 번째 환경이 더 이상 필요하지 않은 경우 해당 환경을 간단히 제거할 수 있습니다. 다른 고객에 대 한 hello Umbraco 데이터베이스 가용성을 탄력적 풀의 일부로 사용할 수 있는 리소스를 해제 합니다.

![Umbraco 배포 아키텍처](./media/sql-database-implementation-umbraco/figure4.png)

그림 3. Microsoft Azure의 UaaS 배포 아키텍처

## <a name="hello-path-from-datacenter-toocloud"></a>데이터 센터 toocloud hello 경로
Hello Umbraco 개발자 hello 의사 결정 toomove tooa SaaS 모델 처음 만들면 hello 서비스 비용 효율적이 고 확장 가능한 방식으로 toobuild 필요 하다는 것 임을 알고 있습니다.

> "탄력적 풀은 필요에 따라 용량을 늘리고 줄일 수 있으므로 당사의 SaaS 제품에 완벽하게 딱 들어맞습니다. 프로비전도 쉬우며, 당사 설정을 통해 최대 사용률을 유지할 수 있습니다."
> 
> - Umbraco기술 책임자, Morten Christensen
> 
> 

"Toospend 싶었기 인프라를 관리 하지 않는 고객의 문제 해결을 위해 시간입니다. Toomake 싶었기 가장 많은 가치를 hello 우리의 고객 tooget 한 것을 쉽게 "Niels Hartvig, Umbraco의 창립자를 표시 합니다. "처음 라고 간주 했습니다 호스팅 스스로 hello 서버 되었지만 용량 계획 있었을 불확실 합니다." 우연히도 Umbraco는 데이터베이스 관리자를 고용하지 않았으며 이러한 방식은 UaaS 사용을 위한 핵심 가치 제안을 부각시켰습니다.

Hello Umbraco 개발자를 위한 중요 한 목표는 신속 하 고 용량 제한 없이 tooprovide Uaa 고객 tooprovision 환경에 대 한 방식으로 했습니다. 하지만 처리 급증 Umbraco 데이터 센터의 전용된 호스팅된 서비스의 초과 용량 toohandle 필요한 많을 것을 제공 합니다. 이것은 정기적으로는 활용도가 낮은 상당량의 계산 인프라를 추가하는 것을 의미하는 것이었습니다.

또한 hello Umbraco 개발 팀이 원했습니다 솔루션을 최대한 기존 코드의 많은 tooreuse 허용 합니다. Umbraco 개발자로 서 Mikkel Madsen 상태, "있었습니다. 친숙 한 Microsoft SQL Server, Microsoft Azure SQL 데이터베이스, ASP.net 및 인터넷 정보 서비스 (IIS)와 같은 अ स म र 이미 hello Microsoft 개발 도구에 만족입니다. PaaS 또는 IaaS에 투자 하기 전에 솔루션을 클라우드는 지원에 따라 Microsoft 도구와 플랫폼 toomake 변경 대량 tooour 코드 베이스 않았을 하므로 있는지 toomake 싶었기. "

모든 toomeet 해당 조건의 Umbraco 자격 다음 hello로 클라우드 파트너에 대 한 조회:

* 충분한 용량 및 안정성
* 지원 엔지니어 됩니다 해당 Umbraco toocompletely 강제 하므로, Microsoft 개발 도구는 개발 환경 불필요 한 작업
* 모든 페이지는 Uaa 경쟁 (해당 데이터에 신속 하 게 액세스할 수와 데이터가 해당 지역 규정 요구 사항을 충족 하는 위치에 저장 된 필요 tooensure 비즈니스) hello 지역/국가의 현재 상태

## <a name="why-umbraco-chose-azure-for-uaas"></a>Umbraco가 UaaS를 위해 Azure를 선택한 이유
"보다 다양 한 모든 옵션을 고려 했습니다 선택한 후 Azure 관리 효율성 및 확장성 toofamiliarity / 비용 효율성이 매력적이 모든 조건을 충족 하기 때문에 Christensen tooMorten에 따라. Azure Vm에서 hello 환경을 설정 하 고 탄력적 풀의 모든 hello 인스턴스와 각 환경에는 Azure SQL 데이터베이스 인스턴스. 개발, 스테이징 및 라이브 환경 간에 데이터베이스를 분리 하 여 수 제공 고객 강력한 성능을 격리 tooscale 일치-엄청난 달성 합니다. "

"전에, 했습니다. 웹 데이터베이스에 대 한 서버 tooprovision 수동으로 Morten 계속. 이제 toothink 항목에 대 한 사항이 있습니다. 모든 것 자동화-toocleanup 프로 비전에서. "

Morten은 Azure에서 제공 하는 기능을 확장 하는 hello로 만족도 매우 이기도 합니다. "탄력적 풀은 필요에 따라 용량을 늘리고 줄일 수 있으므로 당사의 SaaS 제품에 완벽하게 딱 들어맞습니다. 프로비전도 쉬우며, 당사 설정을 통해 최대 사용률을 유지할 수 있습니다." Morten 상태, "의 서비스 계층 기반 dtu 보증 hello 함께 탄력적 풀의 hello 단순 목록에 요청 시 hello 전원 tooprovision 새 리소스 풀 있습니다. 최근 라이브 환경에서 too100 Dtu 피크 한 큰 고객 합니다. Azure를 사용 하는 탄력적 풀 toopredict DTU 요구 사항 필요 없이 실시간으로 필요할 hello 리소스와 hello 고객의 데이터베이스를 제공 합니다. 간단히 말해서, 고객이 시간을 가져올 hello 순환 기대 하 고, 고 우리의 성능 서비스 수준 계약 만날 수. "

Mikkel Madsen 합계를 구하는: "म 했습니다 수용 hello 강력한 Azure 알고리즘 hello를 기반으로 하는 일반적인 SaaS (규모에 실시간으로에서 신규 고객 온 보 딩) 시나리오 tooour 응용 프로그램 패턴 (둘 다 개발 데이터베이스를 미리 프로 비전 및 라이브)를 연결 하는 기본 기술 (Azure SQL 데이터베이스와 함께에서 Azure 서비스 버스 큐 사용). "

## <a name="with-azure-uaas-is-exceeding-customer-expectations"></a>Azure를 사용하여 UaaS에서 고객의 기대치 부응
Azure의 클라우드 파트너로 선택, 이후 Umbraco 수 tooprovide Uaa 고객 필요한 자체 호스팅된 솔루션에서 IT 리소스 hello 투자 없이 콘텐츠 관리 성능 최적화 되었습니다. Morten 라는 "hello 개발자의 편 및 Azure를 제공 하는, 확장성 포함 되며 고객은 hello 기능, 안정성 흥분 했 됩니다. 전반적으로는 우리는 큰 혜택을 얻게 되었습니다.”라고 Norten은 말했습니다.

## <a name="more-information"></a>자세한 정보
* Azure 탄력적 풀에 대해 자세히 toolearn 참조 [탄력적 풀](sql-database-elastic-pool.md)합니다.
* Azure 서비스 버스에 대 한 자세한 toolearn 참조 [Azure 서비스 버스](https://azure.microsoft.com/services/service-bus/)합니다.
* 웹 역할 및 작업자 역할에 대해 자세히 toolearn 참조 [작업자 역할](../fundamentals-introduction-to-azure.md#compute)합니다.    
* 가상 네트워킹에 대해 자세히 toolearn 참조 [가상 네트워킹](https://azure.microsoft.com/documentation/services/virtual-network/)합니다.    
* 백업 및 복구에 대해 자세히 toolearn 참조 [비즈니스 연속성](sql-database-business-continuity.md)합니다.    
* ppols, 모니터링에 대 한 더 toolearn 참조 [풀 모니터링](sql-database-elastic-pool-manage-portal.md)합니다.    
* Umbraco는 서비스에 대 한 자세한 toolearn 참조 [Umbraco](https://umbraco.com/cloud)합니다.

