---
title: "Azure SQL Database 서비스 및 성능 계층 | Microsoft Docs"
description: "단일 데이터베이스에 대한 SQL Database 서비스 계층과 성능 수준을 비교하고 SQL 탄력적 풀을 소개합니다."
keywords: "데이터베이스 옵션, 데이터베이스 성능"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: f5c5c596-cd1e-451f-92a7-b70d4916e974
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/30/2017
ms.author: carlrab
ms.openlocfilehash: b27b78788614d32e6c0c4267fe0ce504ebd2f444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-performance-options-are-available-for-an-azure-sql-database"></a>Azure SQL Database에서 사용할 수 있는 성능 옵션은 무엇입니까?

[Azure SQL Database](sql-database-technical-overview.md)는 단일 및 [풀링된](sql-database-elastic-pool.md) 데이터베이스 모두에 대해 네 개의 서비스 계층, 즉 **기본**, **표준**, **프리미엄** 및 **프리미엄 RS**를 제공합니다. 각 서비스 계층에는 여러 성능 수준이 ([Dtu](sql-database-what-is-a-dtu.md)) 및 저장소 옵션 toohandle 다양 한 작업 및 데이터 크기입니다. 더 높은 성능 수준을 제공 계산 및 저장소 리소스가 toodeliver 점점 더 높은 처리량 및 용량을 설계 합니다. 가동 중지 시간 없이 서비스 계층, 성능 수준 및 저장소를 동적으로 변경할 수 있습니다. 
- **기본**, **표준** 및 **프리미엄** 서비스 계층에는 모두 99.99%의 작동 시간 SLA, 유연한 비즈니스 연속성 옵션, 보안 기능 및 시간별 요금 청구가 있습니다. 
- hello **프리미엄 RS** 계층 hello 동일한 성능 수준을 제공 hello 감소 SLA와 Premium 계층에는 데이터베이스 보다 낮은 수가 중복 복사본을 실행 하기 때문에 hello 다른 서비스 계층으로 합니다. 따라서 서비스 오류의 hello 이벤트에서 toorecover를 tooa 5 분 간격으로 백업에서 데이터베이스를 할 수 있습니다.

> [!IMPORTANT]
> Azure SQL 데이터베이스 리소스의 보장 된 집합을 가져옵니다 고 hello Azure 내에서 다른 데이터베이스에서 데이터베이스의 성능 특성 영향을 받지 않습니다. 

## <a name="choosing-a-service-tier"></a>서비스 계층 선택
hello 다음 표에서 예제 제공 최상의 hello 계층의 서로 다른 응용 프로그램 워크 로드에 적합 합니다.

| 서비스 계층 | 대상 워크로드 |
| :--- | --- |
| **Basic** | 일반적으로 지정된 시기에 활성 작업 한 개를 지원하는 작은 데이터베이스에 가장 적합합니다. 예를 들어 개발 또는 시험, 또는 자주 사용하지 않는 소규모 응용 프로그램에 사용되는 데이터베이스가 이에 해당합니다. |
| **Standard** |hello go-toooption 낮은 toomedium IO 성능 요구 사항으로, 여러 개의 동시 쿼리를 지 원하는 클라우드 응용 프로그램에 대 한 합니다. 예를 들어 작업 그룹 또는 웹 응용 프로그램이 이 계층에 적합한 예입니다. |
| **Premium** | 높은 IO 성능 요구 사항의 높은 트랜잭션 볼륨용으로 설계되었으며, 많은 동시 사용자를 지원합니다. 예를 들어 업무 필수 응용 프로그램을 지원하는 데이터베이스가 이 계층에 적합합니다. |
| **Premium RS** | Hello 가장 높은 가용성 보증이 필요 하지 않은 IO 집약적인 작업을 위해 설계 되었습니다. 예로 고성능 워크 로드 또는 hello 데이터베이스는 레코드 hello 시스템 하지는 분석 워크 로드를 테스트 합니다. |
|||

특정 [성능 수준](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels)의 서비스 계층 내에서 전용 리소스를 사용하여 단일 데이터베이스를 만들거나 [SQL 탄력적 풀](sql-database-service-tiers.md#elastic-pool-service-tiers-and-performance-in-edtus) 내에 데이터베이스를 만들 수도 있습니다. SQL 탄력적인 풀 hello 계산 및 저장소 리소스는 단일 논리 서버 내에서 여러 데이터베이스 간에 공유 됩니다. 

단일 데이터베이스에 사용할 수 있는 리소스는 DTU(데이터베이스 트랜잭션 단위)로 표현되며, SQL 탄력적 풀에 사용할 수 있는 리소스는 eDTU(탄력적 데이터베이스 트랜잭션 단위)로 표현됩니다. DTU 및 eDTU에 대한 자세한 내용은 [DTU 및 eDTU란?](sql-database-what-is-a-dtu.md)을 참조하세요.

toodecide 서비스 계층에서 먼저 확인 해야 하는 hello 최소 데이터베이스 기능:

| **서비스 계층 기능** | **Basic** | **Standard** | **Premium** | **Premium RS**|
| :-- | --: | --: | --: | --: |
| 최대 단일 데이터베이스 크기 | 2 GB | 250GB | 4TB*  | 500GB  |
| 최대 탄력적 풀 크기 | 156GB | 2.9TB | 4TB* | 750GB |
| 탄력적 풀의 최대 데이터베이스 크기 | 2 GB | 250GB | 500GB | 500GB |
| 풀당 최대 데이터베이스 수 | 500  | 500 | 100 | 100 |
| 최대 단일 데이터베이스 DTU | 5 | 100 | 4000 | 1000 |
| 탄력적 풀의 데이터베이스당 최대 DTU | 5 | 3000 | 4000 | 1000 |
| 데이터베이스 백업 보존 기간 | 7 일 | 35일 | 35일 | 35일 |
||||||

> [!IMPORTANT]
> Too4 TB 저장소는 hello 다음 영역에서에서 찾을 수 없습니다: 미국 East2, 미국 서 부, 미국 정부 기관용 버지니아, 서 부 유럽, 독일 중앙, 동남 아시아, 일본 동부, 오스트레일리아 동부, 중앙 캐나다 및 캐나다 동부 합니다. [현재 4TB 제한 사항](sql-database-service-tiers.md#current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize)을 참조하세요.
>

Hello 적절 한 서비스 계층을 결정 했으면 준비 toodetermine hello 성능 수준 (Dtu hello 수) 및 hello 데이터베이스에 대 한 hello 저장소 양이 됩니다. 

- hello S2, S3 성능 수준을 hello **표준** 계층 좋은 출발점 경우가 많습니다. 
- 높은 CPU 또는 IO 요구 사항이 데이터베이스에 대 한 성능 수준을 hello hello **프리미엄** 계층은 hello 오른쪽 시작 지점입니다. 
- hello **프리미엄** 계층은 더 많은 CPU와 10 배 더 많은 IO에서 toohello hello 가장 높은 성능 수준에 비해 **표준** 계층입니다.
- hello **PremiumRS** 계층은 hello의 hello 성능을 **프리미엄** 계층 감소 SLA 하면서도 저렴 한 비용입니다.

> [!IMPORTANT]
> 검토 hello [SQL 탄력적 풀](sql-database-elastic-pool.md) SQL 탄력적으로 데이터베이스를 그룹화 하는 방법에 대 한 hello 세부 정보에 대 한 항목 tooshare 계산 및 저장소 리소스 풀. 이 항목의 나머지 부분에서는 hello 서비스 계층 및 단일 데이터베이스에 대 한 성능 수준에 중점을 둡니다.
>

## <a name="single-database-service-tiers-and-performance-levels"></a>단일 데이터베이스 서비스 계층 및 성능 수준
단일 데이터베이스의 경우 각 서비스 계층 내에는 여러 성능 수준과 저장소 용량이 있습니다. 

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

## <a name="scaling-up-or-scaling-down-a-single-database"></a>단일 데이터베이스 확장 및 축소

처음으로 서비스 계층 및 성능 수준을 선택한 후에 단일 데이터베이스를 실제 환경에 따라 동적으로 확장 또는 축소할 수 있습니다.  

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-dynamically-scale-up-or-scale-down/player]
>

데이터베이스의 hello 서비스 계층 및/또는 성능 수준 변경 hello 새로운 성능 수준에서 hello 원래 데이터베이스의 복제본 만들고 toohello 복제를 통해 연결을 전환 합니다. 데이터는 손실 되지이 프로세스 동안 있지만 hello 잠시 toohello 복제본으로 전환 우리는 때를 하는 동안 연결 toohello 데이터베이스 사용할 이동 중인 일부 트랜잭션이 롤백될 수 있습니다. 통해 hello 스위치에 대 한 시간의 hello 길이 달라 지지만 일반적으로 4 초 이내이 30 초 보다 작으면 hello 시간의 99%입니다. 많은 수의 경우 hello 현재 연결에서 항공편에 트랜잭션을 사용할 수 없습니다, 그리고 hello로 hello 전환에 대 한 시간의 길이 길어질 수 있습니다.  

hello 변경 전후 hello의 서비스 계층 데이터베이스 및 hello 전체 확장 프로세스의 hello 기간 두 hello 크기에 따라 다릅니다. 예를 들어 표준 서비스 계층 내에서 변경되고 있는 250GB 데이터베이스는 6시간 내에 완료되어야 합니다. Hello의 데이터베이스에 대해 동일한 크기 즉 변경 성능 수준 3 시간 이내에 완료 해야 hello Premium 서비스 계층 내에서.

> [!TIP]
> 크기 조정 작업이 진행 중 이므로 SQL 데이터베이스의 hello 상태에 toocheck, hello 다음 쿼리를 사용할 수 있습니다: ```select * from sys.dm_operation_status```합니다.
>

* Tooa 더 높은 서비스 계층 또는 성능 수준을 업그레이드 하는 경우 더 큰 최대 크기를 명시적으로 지정 하지 않으면 hello 최대 데이터베이스 크기 증가 하지 않습니다.
* 데이터베이스 toodowngrade hello 데이터베이스는 hello hello 대상 서비스 계층의 최대 허용된 크기 보다 작아야 합니다. 
* 사용 하 여 데이터베이스를 업그레이드 하는 경우 [지리적 복제](sql-database-geo-replication-portal.md) hello 주 데이터베이스 (일반 지침)을 업그레이드 하기 전에 해당 보조 데이터베이스 toohello 원하는 성능 계층을 업그레이드를 사용 합니다. 다른 tooa 업그레이드 하는 경우 버전 ugrading hello 보조 먼저 데이터베이스가 필요 합니다. 
* 사용 하 여 데이터베이스를 다운 그레이드할 때 [지리적 복제](sql-database-geo-replication-portal.md) hello 보조 데이터베이스 (일반 지침)을 다운 그레이드 하기 전에 해당 주 데이터베이스 toohello 원하는 성능 계층을 다운 그레이드 사용 하도록 설정 합니다. 다른 tooa 다운 그레이드할 때 버전 다운 그레이드 hello 주 먼저 데이터베이스가 필요 합니다. 

* hello 복원 서비스 제공에 대 한 서로 hello 다양 한 서비스 계층입니다. Toohello 다운 그레이드 하는 경우 **기본** 계층 나면 참조 낮은 백업 보존 기간- [Azure SQL 데이터베이스 백업](sql-database-automated-backups.md)합니다.
* hello 데이터베이스에 대 한 새 속성 hello hello 변경이 완료 될 때까지 적용 되지 않습니다.


## <a name="current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize"></a>4TB 최대 크기의 P11 및 P15 데이터베이스의 현재 제한 사항

일부 지역에서는 P11 및 P15 데이터베이스의 최대 크기인 4TB를 지원합니다(앞에서 설명한 대로). hello 다음 고려 사항 및 제한 사항이 적용 tooP11 및 P15 데이터베이스 4TB maxsize에:

- (4TB 또는 4096GB 값 사용) 데이터베이스를 만들 때 hello 4TB maxsize 옵션을 선택 하면 hello hello 데이터베이스가 지원 되지 않는 지역에 구성 하는 경우 오류와 함께 명령이 실패를 만듭니다.
- 기존 P11 및 P15 데이터베이스 지원 hello 영역 중 하나에 있는 hello maxsize 저장소 too4 TB를 늘릴 수 있습니다. Hello를 사용 하 여 확인할 수 있습니다 [선택 DATABASEPROPERTYEX](https://msdn.microsoft.com/library/ms186823.aspx) 또는 hello Azure 포털에서에서 hello 데이터베이스 크기를 검사 하 여 합니다. 기존 P11 또는 P15 업그레이드 데이터베이스 에서만 수행할 수 있습니다 서버 수준 보안 주체 로그인 또는 hello dbmanager 데이터베이스 역할의 구성원. 
- 업그레이드 작업에서 실행 되는 경우는 지원 되는 지역 hello 구성이 즉시 업데이트 됩니다. hello 업그레이드 프로세스 중 hello 데이터베이스가 여전히 온라인입니다. 그러나 전체 hello를 사용할 수 없습니다 4TB hello 실제 데이터베이스 파일 였을 때까지 저장소의 toohello 새 maxsize를 업그레이드 합니다. 필요한 시간의 길이 hello 업그레이드 중인 hello 데이터베이스의 hello 크기에 따라 달라 집니다.  
- P11 또는 P15 데이터베이스를 만들거나 업데이트하는 경우 1TB와 4TB 최대 크기 중에서만 선택할 수 있습니다. 중간 저장소 크기는 현재 지원되지 않습니다. P11/P15를 만들 때에 1tb hello 기본 저장소 옵션은 미리 선택 되어 있습니다. Hello 지원 영역 중 하나에 있는 데이터베이스에 대 한 hello 최대 too4TB 새로운 또는 기존의 단일 데이터베이스에 대 한 저장소를 늘릴 수 있습니다. 다른 모든 지역의 경우 최대 크기를 1TB 이상으로 늘릴 수 없습니다. 4TB의 포함 된 저장소를 선택 하면 hello 가격 변경 되지 않습니다.
- hello 4TB 데이터베이스 maxsize 안 변경 된 too1 TB hello 실제 저장소 사용 1TB 미만인 경우에 됩니다. 따라서 P11-4TB/P15-4TB tooa P11-1TB/P15-1TB 또는 더 낮은 성능 계층 예를 들어 tooP1 P6 다운 그레이드할 수 없습니다)를 제공 하 고 hello 나머지 hello에 대 한 추가 저장소 옵션 성능 계층 될 때까지 합니다. 이러한 제한도 적용 됩니다 toohello 복원 및 시점에 포함 하 여 복사본 시나리오의 경우 지역에서 복원은 장기-단기-백업-보존 및 데이터베이스 복사본입니다. 데이터베이스 hello 4TB 옵션으로 구성 되 면 4TB maxsize와 P11/P15에이 데이터베이스의 모든 복원 작업을 실행 되어야 합니다.
- 만들거나 업그레이드는 지원 되지 않는 지역에 있는 P11/P15 데이터베이스 hello를 만들거나 경우 업그레이드 작업이 실패 하 고 다음과 같은 오류 메시지가 hello: **P11 및 P15 too4TB 저장소를 데이터베이스 미국 East2, 미국 서 부, 미국 정부 기관용 버지니아에서 사용할 수 있는 서 부 유럽, 독일 중부, 동남 아시아, 일본 동부, 오스트레일리아 동부, 캐나다 중앙 및 캐나다 동부**
- 활성 지역 복제 시나리오의 경우:
   - 지리적 복제 관계 설정: 주 데이터베이스 hello P11 또는 P15 이면 hello secondary(ies) 수도 있어야 P11 또는 P15; 더 낮은 성능 계층 4TB를 지원할 수 없기 때문에 보조 복제본으로 거부 됩니다.
   - 지리적 복제 관계에서 업그레이드 hello 주 데이터베이스: hello hello 보조 데이터베이스에서 변경 동일 트리거 hello maxsize too4 TB 주 데이터베이스에서 변경 합니다. 두 가지 업그레이드 hello 변경 hello 기본 tootake 효과에 대해 설정할 수 있어야 합니다. 지역 hello 4TB 옵션에 대 한 제한이 있습니다 (위 참조). 보조 hello 4TB를 지원 하지 않는 지역에 있으면 기본 hello 업그레이드 되지 않습니다.
- P11-4TB/P15-4TB 데이터베이스를 로드 하기 위한 hello 가져오기/내보내기 서비스를 사용 하는 것은 지원 되지 않습니다. SqlPackage.exe를 사용 하 여 너무[가져올](sql-database-import.md) 및 [내보내기](sql-database-export.md) 데이터입니다.

## <a name="manage-single-database-service-tiers-and-performance-levels-using-hello-azure-portal"></a>단일 데이터베이스 서비스 계층 및 성능 수준을 hello Azure 포털을 사용 하 여 관리

서비스 계층, 성능 수준 또는 hello Azure 포털 열기 hello를 사용 하 여 기존 또는 새 Azure SQL 데이터베이스에 대 한 저장소 양을 tooset 또는 변경 hello **성능을 구성** 클릭 하 여 데이터베이스에 대 한 창  **가격 책정 계층 (배율 Dtu)** hello 스크린 샷 뒤에 표시 된 대로-합니다. 

- 설정 하거나 작업에 대 한 hello 서비스 계층을 선택 하 여 hello 서비스 계층을 변경 합니다. 
- Hello 성능 수준 설정 또는 변경 (**Dtu**) hello를 사용 하 여 서비스 계층 내에서 **DTU** 슬라이더 합니다.
- 설정 또는 변경 hello를 사용 하 여 hello 성능 수준에 대 한 hello 저장소 양을 **저장소** 슬라이더 합니다. 

  ![서비스 계층 및 성능 수준 구성](./media/sql-database-service-tiers/service-tier-performance-level.png)

> [!IMPORTANT]
> P11 또는 P15 서비스 계층을 선택하는 경우 [4TB 최대 크기의 P11 및 P15 데이터베이스의 현재 제한 사항](sql-database-service-tiers.md#current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize)을 검토하세요.
>

## <a name="manage-single-database-service-tiers-and-performance-levels-using-powershell"></a>PowerShell을 사용하여 단일 데이터베이스 서비스 계층 및 성능 수준 관리

tooset 또는 변경 Azure SQL 데이터베이스 서비스 계층, 성능 수준 및 PowerShell을 사용 하는 저장소 용량 hello 다음 PowerShell cmdlet을 사용 합니다. PowerShell을 업그레이드 하거나 tooinstall를 필요한 경우 참조 [Azure PowerShell 설치 모듈](/powershell/azure/install-azurerm-ps)합니다. 

| Cmdlet | 설명 |
| --- | --- |
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|데이터베이스 만들기 |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|하나 이상의 데이터베이스 가져오기|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|데이터베이스의 속성 설정 또는 기존 데이터베이스를 탄력적 풀로 이동|


> [!TIP]
> PowerShell 예제 스크립트는 데이터베이스의 hello 성능 메트릭을 모니터링 하 고 더 높은 성능 수준 tooa 확장할 수 hello 성능 메트릭 중 하나에 경고 규칙을 만듭니다 참조 [모니터 및 배율 단일 SQL 데이터베이스를 사용 하 여 PowerShell](scripts/sql-database-monitor-and-scale-database-powershell.md)합니다.

## <a name="manage-single-database-service-tiers-and-performance-levels-using-hello-azure-cli"></a>단일 데이터베이스 서비스 계층 및 성능 수준을 hello Azure CLI를 사용 하 여 관리

hello 다음 이름을 사용해 서 tooset 또는 변경 Azure SQL 데이터베이스 서비스 계층, 성능 수준 및 hello Azure CLI를 사용 하 여 저장소 용량 [Azure CLI SQL 데이터베이스](/cli/azure/sql/db) 명령입니다. 사용 하 여 hello [클라우드 셸](/azure/cloud-shell/overview) 브라우저에서 toorun hello CLI 또는 [설치](/cli/azure/install-azure-cli) macOS, Linux 또는 Windows에 있습니다. SQL 탄력적 풀 만들기 및 관리에 대해서는 [탄력적 풀](sql-database-elastic-pool.md)을 참조하세요.

| Cmdlet | 설명 |
| --- | --- |
|[az sql db create](/cli/azure/sql/db#create) |데이터베이스 만들기|
|[az sql db list](/cli/azure/sql/db#list)|서버의 모든 데이터베이스 및 데이터 웨어하우스 또는 탄력적 풀의 모든 데이터베이스 나열|
|[az sql db list-editions](/cli/azure/sql/db#list-editions)|사용 가능한 서비스 목표 및 저장소 용량 제한 나열|
|[az sql db list-usages](/cli/azure/sql/db#list-usages)|데이터베이스 사용 정보 반환|
|[az sql db show](/cli/azure/sql/db#show)|데이터베이스 또는 데이터 웨어하우스 가져오기|
|[az sql db update](/cli/azure/sql/db#update)|데이터베이스 업데이트|

> [!TIP]
> 단일 Azure SQL 데이터베이스 tooa 다양 한 성능 수준을 hello 데이터베이스의 hello 크기 정보를 쿼리 한 후 크기가 조정 되는 Azure CLI 예제 스크립트에 대 한 참조 [사용 CLI toomonitor 및 단일 SQL 데이터베이스 확장](scripts/sql-database-monitor-and-scale-database-cli.md)합니다.
>

## <a name="manage-single-database-service-tiers-and-performance-levels-using-transact-sql"></a>Transact-SQL을 사용하여 단일 데이터베이스 서비스 계층 및 성능 수준 관리

tooset 또는 변경 Azure SQL 데이터베이스 서비스 계층, 성능 수준 및 Transact SQL을 사용한 저장소 양 T-SQL 명령을 수행 하는 hello를 사용 합니다. Hello Azure 포털을 사용 하 여 이러한 명령을 실행할 수 있습니다 [SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [Visual Studio Code](https://code.visualstudio.com/docs), 또는 tooan Azure SQL 데이터베이스 서버를 연결 하 고 TRANSACT-SQL 전달할 수 있는 다른 프로그램 명령입니다. 

| 명령 | 설명 |
| --- | --- |
|[CREATE DATABASE (Azure SQL Database)](/sql/t-sql/statements/create-database-azure-sql-database)|새 데이터베이스를 만듭니다. 연결 된 toohello master 데이터베이스 toocreate 새 데이터베이스 여야 합니다.|
| [ALTER DATABASE (Azure SQL Database)](/sql/t-sql/statements/alter-database-azure-sql-database) |Azure SQL 데이터베이스를 수정합니다. |
|[sys.database_service_objectives(Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스에 대 한 반환 hello edition (서비스 계층), (가격 책정 계층), 서비스 목표 및 탄력적인 풀 이름입니다. Azure SQL 데이터베이스 서버에서 toohello master 데이터베이스에 로그온 하는 경우 모든 데이터베이스에서 정보를 반환 합니다. Azure SQL 데이터 웨어하우스에 대 한 연결 된 toohello master 데이터베이스 여야 합니다.|
|[sys.database_usage(Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-usage-azure-sql-database)|Hello 수, 유형 및 Azure SQL 데이터베이스 서버에서 데이터베이스의 기간을 나열합니다.|

hello 다음 예제에서는 hello maxsize hello ALTER DATABASE 명령을 사용 하 여 변경 합니다.

 ```sql
ALTER DATABASE <myDatabaseName> 
   MODIFY (MAXSIZE = 4096 GB);
```

## <a name="manage-single-databases-using-hello-rest-api"></a>Hello REST API를 사용 하 여 단일 데이터베이스 관리

tooset 또는 변경 Azure SQL 데이터베이스 서비스 계층, 성능 수준 및 hello REST API를 사용 하 여 저장소 용량 참조 [Azure SQL 데이터베이스 REST API](/rest/api/sql/)합니다.

## <a name="next-steps"></a>다음 단계

* [DTU](sql-database-what-is-a-dtu.md)에 대해 자세히 알아봅니다.
* toolearn DTU 사용량을 모니터링 하는 방법에 대 한 참조 [모니터링 및 성능 조정](sql-database-troubleshoot-performance.md)합니다.

