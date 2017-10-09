---
title: "데이터베이스 vs aaaSQL (PaaS)입니다. SQL Server Vm (IaaS)에서 hello 클라우드에서 | Microsoft Docs"
description: "응용 프로그램에 적합 한 클라우드 SQL Server 옵션에 알아봅니다: (PaaS) Azure SQL 데이터베이스 또는 hello 클라우드의 Azure 가상 컴퓨터에서 SQL Server."
services: sql-database, virtual-machines
keywords: "SQL Server 클라우드, 클라우드의 hello PaaS 데이터베이스의 SQL Server SQL Server, DBaaS 클라우드"
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: cjgronlund
ms.assetid: 7467f422-b77d-4b60-9cb5-0f1ec17ec565
ms.service: sql-database
ms.custom: DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: vm-windows-sql-server
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: carlrab
ms.openlocfilehash: 1b462a9a822d04dc5deb8422ed505a5d09279253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="choose-a-cloud-sql-server-option-azure-sql-paas-database-or-sql-server-on-azure-vms-iaas"></a>클라우드 SQL Server 옵션 선택: Azure SQL(PaaS) 데이터베이스 또는 Azure VM의 SQL Server(IaaS)
Azure에는 Microsoft Azure의 SQL Server 워크로드를 호스팅하는 다음과 같은 두 가지 옵션이 있습니다.

* [Azure SQL 데이터베이스](https://azure.microsoft.com/services/sql-database/): SQL 데이터베이스 네이티브 toohello 클라우드 서비스 (PaaS) 데이터베이스 또는 데이터베이스 소프트웨어-as a service (SaaS) 앱 개발을 위한 최적화 된 서비스 (DBaaS)으로 플랫폼 라고도 합니다. 대부분의 SQL Server 기능과의 호환성을 제공합니다. PaaS에 대한 자세한 내용은 [PaaS란](https://azure.microsoft.com/overview/what-is-paas/)을 참조하세요.
* [Azure 가상 컴퓨터에 SQL Server](https://azure.microsoft.com/services/virtual-machines/sql-server/): SQL Server 설치 및 클라우드에서 호스트 되 hello에 Windows Server Vm (가상 컴퓨터)에서 Azure (iaas) 인프라 라고도 실행 합니다.
  Azure 가상 컴퓨터에 대한 SQL Server는 기존 SQL Server 응용 프로그램을 마이그레이션하는 데 최적화됩니다. 모든 hello 버전 및 SQL Server의 버전은 사용할 수 있습니다. 제공 SQL server에서는 가능 하면 toohost 100% 호환성 만큼 데이터베이스 필요 하 고 실행 중인 데이터베이스 간 트랜잭션 합니다. SQL Server 및 Windows에 대한 모든 권한을 제공합니다.

각 옵션 hello Microsoft 데이터 플랫폼에 맞게 조정 및 도움말 일치 하는 hello 적절 한 옵션 tooyour 비즈니스 요구를 가져오는 방법을 알아봅니다. 비용 절감 또는 다른 모든 요소 보다 먼저 최소 관리 우선 순위를 지정할 수 있는지 여부를 가장 중요 한 hello 비즈니스 요구 사항에 대해 배달 방식을 결정 하는 데이 문서가 도움이 수 있습니다.

## <a name="microsofts-data-platform"></a>Microsoft의 데이터 플랫폼
모든 논의는 온-프레미스 SQL Server 데이터베이스와 azure의 hello 첫 번째 작업 toounderstand 중 하나는 모두 사용할 수 있는입니다. Microsoft의 데이터 플랫폼에서는 SQL Server 기술을 활용하며 물리적 온-프레미스 컴퓨터, 사설 클라우드 환경, 타사 호스팅 사설 클라우드 환경 및 공용 클라우드 전반에서 이 기술을 사용할 수 있습니다. Azure 가상 컴퓨터에 SQL Server 사용 하면 온-프레미스 및 클라우드에서 호스트 배포의 조합을 통해 toomeet 고유 하 고 다양 한 비즈니스 요구에서 이러한 동일한 집합이 서버 제품, 개발 도구 및 전문 지식을 hello를 사용 하는 동안 환경입니다.

   ![SQL Server 옵션 클라우드: hello 클라우드에서 IaaS 또는 SaaS SQL에서 SQL server 데이터베이스입니다.](./media/sql-database-paas-vs-sql-server-iaas/SQLIAAS_SQL_Server_Cloud_Continuum.png)

Hello 다이어그램에서와 같이 데이터베이스 수준 통합 및 자동화 (hello Y 축)에 의해 달성 비용 효율성 수준의 hello 및 hello 수준의 hello 인프라 (hello X 축)에 대 한 관리에서 제품 마다 이해할 수 있습니다.

응용 프로그램을 디자인할 네 가지 기본 옵션 hello 응용 프로그램의 hello SQL Server 부분 호스팅에 사용할 수 있습니다.

* 가상화되지 않은 물리적 컴퓨터의 SQL Server
* 온-프레미스 가상화 컴퓨터의 SQL Server(사설 클라우드)
* Azure 가상 컴퓨터의 SQL Server(Microsoft 공용 클라우드)
* Azure SQL 데이터베이스(Microsoft 공용 클라우드)

다음 섹션 hello, 배웁니다 SQL Server에 대 한 Microsoft 공용 클라우드 hello에: Azure SQL 데이터베이스 및 Azure Vm에서 SQL Server. 또한 응용 프로그램에 가장 적합한 옵션을 결정하는 데 영향을 미치는 일반적인 비즈니스 동인도 살펴봅니다.

## <a name="a-closer-look-at-azure-sql-database-and-sql-server-on-azure-vms"></a>Azure SQL 데이터베이스 및 Azure VM의 SQL Server에서 자세히 보기
**Azure SQL 데이터베이스** 는 관계형 데이터베이스로-a service (DBaaS) hello hello 업계 범주에 속하는 Azure 클라우드에서에서 호스팅되는 *소프트웨어-as a Service (SaaS)* 및 *플랫폼-as a Service (PaaS)* . [SQL 데이터베이스](sql-database-technical-overview.md) 는 Microsoft에서 소유하고 호스트하고 유지 관리하는 표준화된 하드웨어 및 소프트웨어를 기반으로 구축됩니다. SQL 데이터베이스와 기본 제공 특징과 기능을 사용 하 여 hello 서비스에서 직접 개발할 수 있습니다. SQL 데이터베이스 중단 없이 큰 전원 옵션 tooscale 내부 또는 외부와 종 량 제 있습니다 사용할 때

**Azure 가상 컴퓨터 (Vm)에서 SQL Server** hello 업계 범주에 속하는 *인프라-as a Service (IaaS)* hello 클라우드에서 가상 컴퓨터 내부 SQL Server toorun 있습니다. 비슷한 tooSQL 데이터베이스를 소유, 호스팅 및 Microsoft에서 관리 되는 표준화 된 하드웨어에서 생성 된 합니다. VM에서 SQL Server를 사용하는 경우 SQL Server 이미지에 이미 포함된 SQL Server 라이선스에 종량제를 사용하거나 기존 라이선스를 쉽게 사용할 수 있습니다. 또한 수 있습니다 쉽게 확장/아래로 및 일시 중지/다시 시작 hello VM 필요에 따라.

일반적으로 이러한 두 SQL 옵션은 다음과 같이 최적의 용도가 서로 다릅니다.

* **Azure SQL 데이터베이스** 전체 비용 최적화 tooreduce은 프로 비전 하 고 여러 데이터베이스를 관리 하기 위한 최소 toohello 합니다. 모든 가상 컴퓨터, 운영 체제 또는 데이터베이스 소프트웨어 toomanage 없기 때문에 진행 중인 관리 비용이 줄어듭니다. Toomanage 업그레이드 없는 고가용성 또는 [백업을](sql-database-automated-backups.md)합니다. Azure SQL 데이터베이스는 단일 관리 되는 데이터베이스의 hello 수가 크게 향상 시킬 일반적으로 IT 또는 개발 리소스입니다.
* **Azure Vm에서 실행 중인 SQL Server** 마이그레이션 응용 프로그램 tooAzure 기존 컨트롤이 나 기존 온-프레미스 하이브리드 배포에서 응용 프로그램 toohello 클라우드 확장을 위해 최적화 됩니다. 또한 SQL Server 가상 컴퓨터 toodevelop에 사용 하 고 기존의 SQL Server 응용 프로그램을 테스트할 수 있습니다. Azure Vm에서 SQL server에서는 전용된 SQL Server 인스턴스 및 클라우드 기반 VM 대해서 hello 모든 관리 권한을 있습니다. 이미 조직에는 IT 리소스 사용 가능한 toomaintain hello 가상 컴퓨터에는 완벽 한 선택은. 이러한 기능을 통해 toobuild 고도로 사용자 지정 된 시스템 tooaddress 하면 응용 프로그램의 특정 성능 및 가용성 요구 사항입니다.

다음 표에 hello hello SQL 데이터베이스 및 Azure Vm에서 SQL Server의 주요 특징을 요약 합니다.

| **최적 용도:** | **Azure SQL Database** | **Azure 가상 컴퓨터의 SQL Server** |
| --- | --- | --- |
|  |개발 및 마케팅에 시간 제약이 따르는 클라우드용으로 설계된 새 응용 프로그램 |최소한의 변경으로 빠른 마이그레이션 toohello 클라우드를 필요로 하는 기존 응용 프로그램입니다. 신속한 개발 및 테스트 시나리오 toobuy 온-프레미스 비-프로덕션 SQL Server 하드웨어를 원하지 않는 경우. |
|  | Hello 데이터베이스에 대 한 기본 제공 고가용성, 재해 복구 및 업그레이드 해야 하는 팀입니다. |SQL Server에 대한 고가용성, 재해 복구 및 패치를 구성하고 관리할 수 있는 팀 자동화된 기능을 제공하는 일부 팀은 이를 크게 간소화합니다. | |
|  | Toomanage hello 기본 운영 체제 및 구성 설정을 원하지 않는 팀을 선택 합니다. |모든 관리 권한이 있는 사용자 지정 환경이 필요합니다. | |
|  | Too4 TB의 데이터베이스 또는 일 수 있는 더 큰 데이터베이스 [가로 또는 세로로 분할](sql-database-elastic-scale-introduction.md#horizontal-and-vertical-scaling) 확장 패턴을 사용 합니다. |SQL Server 인스턴스와 too64 TB 저장 합니다. hello 인스턴스 필요에 따라 많은 데이터베이스를 지원할 수 있습니다. | |
|  | [SaaS(Software-as-a-Service) 응용 프로그램 빌드](sql-database-design-patterns-multi-tenancy-saas-applications.md) |엔터프라이즈 및 하이브리드 응용 프로그램 마이그레이션 및 빌드 | |
|  | | |
| **리소스:** |IT tooemploy 하지 않으려면 hello 기본 인프라의 구성 및 관리에 대 한 리소스에는 있지만 toofocus hello 응용 프로그램 계층에서 원하는 합니다. |구성 및 관리를 위한 일부 IT 리소스가 있습니다. 자동화된 기능을 제공하는 일부 팀은 이를 크게 간소화합니다. |
| **총 소유 비용** |하드웨어 비용을 제거하고 관리 비용을 절감합니다. |하드웨어 비용을 제거합니다. |
| **비즈니스 연속성:** |Azure SQL 데이터베이스 추가 toobuilt의 오류 내결함성 인프라 기능에서 기능을와 같은 제공 [자동화 된 백업을](sql-database-automated-backups.md), [시점에 복원](sql-database-recovery-using-backups.md#point-in-time-restore), [지역에서복원](sql-database-recovery-using-backups.md#geo-restore), 및 [활성 지리적 복제](sql-database-geo-replication-overview.md) tooincrease 비즈니스 연속성 합니다. 자세한 내용은 [SQL 데이터베이스 비즈니스 연속성 개요](sql-database-business-continuity.md)를 참조하세요. |Azure VM의 SQL Server를 사용하면 데이터베이스의 특정 요구에 맞게 고가용성 및 재해 복구 솔루션을 설정할 수 있습니다. 따라서 시스템을 응용 프로그램에 최적화할 수 있습니다. 필요한 경우 장애 조치(Failover)를 직접 테스트하고 실행할 수 있습니다. 자세한 내용은 [Azure 가상 컴퓨터의 SQL Server에 대한 고가용성 및 재해 복구](../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md)를 참조하세요. |
| **하이브리드 클라우드:** |온-프레미스 응용 프로그램은 Azure SQL 데이터베이스의 데이터에 액세스할 수 있습니다. |Azure Vm에서 SQL Server를 사용 하면 hello 클라우드에 부분적으로 실행 되는 응용 프로그램을 가질 수 있습니다 및 부분적으로 온-프레미스입니다. 예를 들어 온-프레미스 네트워크 및 Active Directory 도메인 toohello 클라우드를 통해을 확장할 수 있습니다 [Azure 가상 네트워크](../virtual-network/virtual-networks-overview.md)합니다. 또한 [Azure의 SQL Server 데이터 파일](http://msdn.microsoft.com/library/dn385720.aspx)을 사용하여 온-프레미스 데이터 파일을 Azure 저장소에 저장할 수도 있습니다. 자세한 내용은 참조 [Server 2014 하이브리드 클라우드 소개 tooSQL](http://msdn.microsoft.com/library/dn606154.aspx)합니다. |
|  | 지원 [SQL Server 트랜잭션 복제](https://msdn.microsoft.com/library/mt589530.aspx) 구독자 tooreplicate 데이터로 합니다. |완벽 하 게 지원 [SQL Server 트랜잭션 복제](https://msdn.microsoft.com/library/mt589530.aspx), [AlwaysOn 가용성 그룹](../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md), Integration Services, 및 tooreplicate 데이터 로그 전달 합니다. 또한 기존의 SQL Server 백업은 완벽하게 지원됩니다. | |
|  | | |

## <a name="business-motivations-for-choosing-azure-sql-database-or-sql-server-on-azure-vms"></a>Azure SQL 데이터베이스 또는 Azure VM의 SQL Server를 선택하는 경우 비즈니스 동기
### <a name="cost"></a>비용
현금, strapped를 시작 하는 또는 인지 시간이 제약 조건, 제한 된 자금 되어 작동 하는 설정 된 회사에서 팀 종종 hello 기본 드라이버 결정할 때 어떻게 toohost 데이터베이스입니다. 이 섹션에서는 hello 청구에 대 한 설명 및 두 가지 관계형 데이터베이스 옵션 toothese 간주 라이선스 사용 하 여 Azure의 기본 사항: SQL 데이터베이스 및 Azure Vm에서 SQL Server. 또한 hello 총 응용 프로그램 비용 계산에 대 한 알아봅니다.

#### <a name="billing-and-licensing-basics"></a>청구 및 라이선스 기본 사항
**SQL 데이터베이스** 은 toocustomers 라이선스와 서비스를 판매 합니다.  [Azure VM에 대한 SQL Server](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md) 는 분당 지불하는 라이선스로 판매됩니다. 기존 라이선스가 있다면 사용할 수 있습니다.  

현재 **SQL 데이터베이스** 고정 된 요금이 hello 서비스 계층과 성능 수준을 선택 하면를 기반으로 시간당 청구 됩니다는 모두 몇 가지 서비스 계층에서 사용할 수 있습니다. 또한 일반 [데이터 전송 요금](https://azure.microsoft.com/pricing/details/data-transfers/)으로 발신 인터넷 트래픽에 대해 요금이 청구됩니다. Basic, Standard, Premium, hello 및 RS Premium 서비스 계층은 설계 된 여러 성능 수준이 toomatch toodeliver 예측 가능한 성능을 응용 프로그램의 최대 요구 사항입니다. 서비스 계층 및 응용 프로그램의 다양 한 처리량이 필요한 성능 수준 toomatch 간에 변경할 수 있습니다. 에 포함 된 데이터베이스 높은 트랜잭션 볼륨 및 요구 사항 toosupport 많은 동시 사용자가 hello Premium 서비스 계층을 권장 합니다. Hello 지원 hello 현재 서비스 계층에 대 한 최신 정보를 참조 하십시오. [Azure SQL 데이터베이스 서비스 계층](sql-database-service-tiers.md)합니다. 만들 수도 있습니다 [탄력적 풀](sql-database-elastic-pool.md) 데이터베이스 인스턴스 간에 tooshare 성능 리소스입니다.

와 **SQL 데이터베이스**, hello 데이터베이스 소프트웨어를 자동으로 구성, 패치, 있으며 업그레이드 microsoft에서 관리 비용이 감소 합니다. 또한 [기본 제공 백업](sql-database-automated-backups.md) 기능을 사용하여 비용을 크게 절감할 수 있으며, 특히 데이터베이스 수가 많을 경우 그 효과가 큽니다.

와 **Azure Vm에서 SQL Server**, (포함 하는 라이선스) hello 플랫폼에서 제공 SQL Server 이미지 중 하나를 사용 하거나 SQL Server 라이선스를 가져올 수 있습니다. 모든 hello 지원 되는 SQL Server 버전 (2008R2, 2012, 2014, 2016) 이므로 (Developer, Express, Web, Standard, Enterprise) 버전에서 사용할 수 있습니다. Hello 이미지의 Bring Your-소유-라이선스 버전 (BYOL)도 사용할 수 있습니다. Azure 이미지를 제공 하는 hello를 사용 하 여 hello 운영 비용 hello VM 크기 및 선택한 SQL Server의 hello 버전에 따라 다릅니다. VM 크기 또는 SQL Server 버전에 관계 없이 hello VM 디스크에 대 한 Azure 저장소 비용 hello와 함께 SQL Server 및 Windows Server의 분당 라이선스 비용을 지불합니다. hello 분당 청구 옵션 추가 SQL Server 라이선스를 구입 하지 않고도 필요한 만큼 오래 동안 SQL Server toouse가 있습니다. 사용자 고유의 SQL Server 라이선스 tooAzure를가지고 올 경우 Windows Server 및 저장소 비용만 요금이 청구 됩니다. 고유한 라이선스 가져오기에 대한 자세한 내용은 [Azure에서 Software Assurance를 통한 라이선스 이동](https://azure.microsoft.com/pricing/license-mobility/)을 참조하세요.

#### <a name="calculating-hello-total-application-cost"></a>Hello 총 응용 프로그램 비용 계산
클라우드 플랫폼을 사용 하 여 시작할 때 hello 실행 비용을 응용 프로그램에 hello 개발 및 관리 비용와 hello 공용 클라우드 플랫폼 서비스 비용 포함 됩니다.

Azure Vm의 SQL 데이터베이스 및 SQL Server에서 실행 되는 응용 프로그램에 대 한 자세한 비용 계산 hello 다음과 같습니다.

**Azure SQL 데이터베이스를 사용하는 경우:**

*총 응용 프로그램 비용 = 최소 관리 비용 + 소프트웨어 개발 비용 + SQL 데이터베이스 서비스 비용*

**Azure VM의 SQL Server를 사용하는 경우:**

*총 응용 프로그램 비용 = 매우 최소화된 소프트웨어 개발 비용 + 관리 비용 + SQL Server 및 Windows Server 라이선스 비용 + Azure Storage 비용*

가격 책정에 대 한 자세한 내용은 다음 리소스는 hello 참조:

* [SQL 데이터베이스 가격](https://azure.microsoft.com/pricing/details/sql-database/)
* [SQL](https://azure.microsoft.com/pricing/details/virtual-machines/#sql) 및 [Windows](https://azure.microsoft.com/pricing/details/virtual-machines/#windows)에 대한 [가상 컴퓨터 가격 책정](https://azure.microsoft.com/pricing/details/virtual-machines/)
* [Azure 가격 계산기](https://azure.microsoft.com/pricing/calculator/)

> [!NOTE]
> SQL 데이터베이스에 적용되거나 사용할 수 없는 SQL Server의 기능 하위 집합이 있습니다. 자세한 내용은 [SQL Database 기능](sql-database-features.md) 및 [SQL Database Transact-SQL 정보](sql-database-transact-sql-information.md)를 참조하세요. 기존 SQL Server 솔루션 toohello 클라우드에 이동 하는 경우 참조 [SQL Server 데이터베이스 tooAzure SQL 데이터베이스 마이그레이션](sql-database-cloud-migrate.md)합니다. 기존 온-프레미스 SQL Server 응용 프로그램 tooSQL 데이터베이스를 마이그레이션하는 경우에 클라우드 서비스를 제공 하는 hello 기능 활용 응용 프로그램 tootake hello를 업데이트 하는 것이 좋습니다. 사용을 고려할 수는 예를 들어 [Azure 웹 앱 서비스](https://azure.microsoft.com/services/app-service/web/) 또는 [Azure 클라우드 서비스](https://azure.microsoft.com/services/cloud-services/) toohost 응용 프로그램 계층 tooincrease 비용 이점입니다.
> 
> 

### <a name="administration"></a>관리
많은 기업에 대 한 hello 의사 결정 tootransition tooa 클라우드 서비스는 있는 그대로 훨씬 그대로 관리의 복잡성을 오프 로드 하는 방법에 대 한 비용입니다. 와 **SQL 데이터베이스**, Microsoft hello 기반 하드웨어를 관리 합니다. Microsoft 자동으로 복제 모든 데이터 tooprovide 높은 가용성, 구성 및 hello 데이터베이스 소프트웨어를 업그레이드, 부하 분산 관리 하며 서버 오류가 발생 하는 경우 투명 한 장애 조치를 수행 합니다. 데이터베이스 tooadminister 계속할 수 있지만 toomanage hello 데이터베이스 엔진, 서버 운영 체제 또는 하드웨어 더 이상 필요 합니다.  계속 하는 항목의 예제 데이터베이스 및 로그인, 인덱스 및 쿼리 튜닝 및 감사 및 보안 tooadminister 포함 합니다.

와 **Azure Vm에서 SQL Server**를 완전히 제어할 hello 운영 체제 및 SQL Server 인스턴스 구성 해야 합니다. VM으로 중인지 tooyou toodecide tooupdate/업그레이드에는 운영 체제 및 데이터베이스 소프트웨어 hello와 때 tooinstall 바이러스 백신 같은 추가 소프트웨어. 일부 자동화 된 기능에는 toodramatically 단순화 패치, 백업, 고가용성 제공 됩니다. 또한 해당 저장소 구성, 디스크, hello 수 및 hello hello VM 크기를 제어할 수 있습니다. Azure에서는 필요에 따라 VM의 toochange hello 크기 있습니다. 자세한 내용은 [Azure용 가상 컴퓨터 및 클라우드 서비스 크기](../virtual-machines/windows/sizes.md)를 참조하세요. 

### <a name="service-level-agreement-sla"></a>SLA(서비스 수준 계약)
IT 부서의 경우 SLA(서비스 수준 계약)의 작동 시간 의무를 충족하는 일이 가장 우선합니다. 이 섹션에서는 SLA의 적용 살펴보겠습니다 tooeach 데이터베이스 호스팅 옵션입니다.

Microsoft는 **SQL Database** Basic, Standard Premium 및 Premium RS 서비스 계층에 대해 99.99%의 가용성 SLA를 제공합니다. Hello 최신 정보를 참조 하십시오. [서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/sql-database/)합니다. Hello SQL 데이터베이스 서비스 계층 및 지원 hello 비즈니스 연속성 계획에 대 한 최신 정보를 참조 하십시오. [서비스 계층](sql-database-service-tiers.md)합니다.

에 대 한 **Azure Vm에서 실행 중인 SQL Server**, Microsoft 99.95%의 가용성 SLA 적용 됩니다. 가상 컴퓨터를 방금 hello를 제공 합니다. 이 SLA hello VM에서 실행 중인 (예: SQL Server) hello 프로세스를 다루지 않습니다 있으며 가용성 집합에 두 개 이상의 VM 인스턴스를 호스트 합니다. Hello 최신 정보를 보려면 참조 hello [VM SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/)합니다. 데이터베이스 고가용성 (HA) 내의 Vm 구성 해야 hello 지원 고가용성 옵션 중 하나에서 SQL Server와 같은 [AlwaysOn 가용성 그룹](http://blogs.technet.com/b/dataplatforminsider/archive/2014/08/25/sql-server-alwayson-offering-in-microsoft-azure-portal-gallery.aspx)합니다. 고가용성이 지원 되는 옵션을 사용 하 여 추가 SLA를 제공 하지 않습니다 이지만 tooachieve 사용 > 99.99% 데이터베이스 가용성입니다.

### <a name="market"></a>시간 toomarket
**SQL 데이터베이스** 는 클라우드로 설계 된 응용 프로그램에 대 한 hello 오른쪽 솔루션 개발자의 생산성과 빠른 시간을 단축이 중요 합니다. 프로그래밍 방식으로 DBA와 유사한 기능을 통해 이므로 클라우드 설계자 및 개발자를 위한 완벽 한 hello 기본 운영 체제 및 데이터베이스를 관리 하기 위한 hello 요구를 낮춥니다. 예를 들어 hello를 사용할 수 있습니다 [REST API](http://msdn.microsoft.com/library/azure/dn505719.aspx) 및 [PowerShell Cmdlet](http://msdn.microsoft.com/library/mt740629.aspx) tooautomate 수천 개의 데이터베이스에 대 한 관리 작업을 관리 하 고 있습니다. 와 같은 기능 [탄력적 풀](sql-database-elastic-pool.md) hello 응용 프로그램 계층에서 toofocus를 허용 하 고 솔루션 toohello 시장을 더 빠르게 제공 합니다.

**Azure Vm에서 실행 중인 SQL Server** 기존 또는 새 응용 프로그램에서는 큰 데이터베이스를 서로 관련 된 데이터베이스 또는 SQL Server 또는 Windows의 tooall 기능에 액세스 하는 경우에 완벽 합니다. Toomigrate 기존 하려는 경우 가장 잘 맞는 온-프레미스로 응용 프로그램 및 데이터베이스 tooAzure 이기도-됩니다. Toochange hello 프레젠테이션, 응용 프로그램 및 데이터 계층 않아도 이후 rearchitecting 기존 솔루션에 시간과 예산을 저장 합니다. 대신, 및 hello Azure 플랫폼에서 요구 될 수 있는 몇 가지 성능 최적화를 수행 하 여 모든 솔루션 tooAzure 마이그레이션하는 방법에 집중할 수 있습니다. 자세한 내용은 [Azure 가상 컴퓨터의 SQL Server에 대한 성능 모범 사례](../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md)를 참조하세요.

## <a name="summary"></a>요약
이 문서는 Azure 가상 컴퓨터(VM)에서 SQL 데이터베이스 및 SQL Server를 탐색했고 결정하는 데 영향을 줄 수 있는 일반적인 비즈니스 동인을 설명했습니다. hello 다음은 제안 tooconsider 있습니다에 대 한 요약입니다.

**Azure SQL 데이터베이스** 를 선택하는 경우:

* 새 클라우드 기반 응용 프로그램 빌드 tootake 활용 hello 비용 절감 효과 및 성능 최적화 클라우드 서비스로 제공 됩니다. 이 방법을 사용 완전히 관리 되는 클라우드 서비스의 hello 이점이 더 낮은 초기 시간을 단축, 주며 장기 비용 최적화를 제공할 수 있습니다.
* Microsoft toohave 원하는 데이터베이스에 대 한 일반 관리 작업을 수행 하 고 데이터베이스에 대 한 더 강력한 가용성 Sla를 필요로 합니다.

**Azure VM의 SQL Server** 를 선택하는 경우:

* 기존 온-프레미스 응용 프로그램 toomigrate 싶거나 toohello 클라우드 확장 하려는 엔터프라이즈 응용 프로그램 toobuild 4TB 보다 큰 경우. 이 방법은 hello 활용할 100 %SQL 호환성을 큰 데이터베이스의 용량, SQL Server 및 Windows 및 보안 터널링 tooon-프레미스에 대 한 모든 권한 제공합니다. 이 방법은 기존 응용 프로그램의 개발 및 수정에 대한 비용을 최소화합니다.
* 기존 IT 리소스가 있다면 패치, 백업 및 데이터베이스 고가용성을 궁극적으로 활용할 수 있습니다. 일부 자동화된 기능은 이러한 작업을 크게 간소화합니다. 

## <a name="next-steps"></a>다음 단계
* 참조 [첫 번째 Azure SQL 데이터베이스](sql-database-get-started-portal.md) tooget SQL 데이터베이스를 시작 합니다.
* [SQL 데이터베이스 가격 책정](https://azure.microsoft.com/pricing/details/sql-database/)을 참조하세요.
* 참조 [Azure에서 SQL Server 가상 컴퓨터를 프로 비전](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md) tooget Azure Vm에서 SQL Server 시작 합니다.

