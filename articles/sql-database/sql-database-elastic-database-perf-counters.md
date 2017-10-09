---
title: "shard map manager에 대 한 aaaPerformance 카운터"
description: "ShardMapManager 클래스 및 데이터 종속 라우팅 성능 카운터"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: b090aba0-2e30-454c-96b3-dffa281f539a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: ddove
ms.openlocfilehash: d24198563d9fa88d12e6c464dbe89bc300e72ca0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-counters-for-shard-map-manager"></a>분할된 맵 관리자에 대한 성능 카운터
성능을 hello를 캡처할 수 있습니다는 [shard map manager](sql-database-elastic-scale-shard-map-management.md)사용 하는 경우에 특히 [데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md)합니다. 카운터는 hello Microsoft.Azure.SqlDatabase.ElasticScale.Client 클래스의 메서드를 사용 하 여 만들어집니다.  

카운터를 사용 하는 tootrack hello 성능을 [데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md) 작업 합니다. 이러한 카운터는 성능 모니터 hello hello "탄력적 데이터베이스:: 분할 관리" 범주 아래에 액세스할 수 있습니다.

**Hello 최신 버전에 대 한:** 너무 이동[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)합니다. 참고 항목 [는 app toouse hello 최신 탄력적 데이터베이스 클라이언트 라이브러리를 업그레이드](sql-database-elastic-scale-upgrade-client-library.md)합니다.

## <a name="prerequisites"></a>필수 조건
* toocreate hello 성능 범주 및 카운터를 hello 사용자 hello 로컬의 일부 여야 합니다. **관리자** hello 응용 프로그램을 호스트 하는 hello 컴퓨터 그룹입니다.  
* hello 사용자 두 hello의 구성원 이어야 합니다., toocreate 성능 카운터 인스턴스 및 hello 카운터 업데이트 **관리자** 또는 **성능 모니터 사용자** 그룹입니다. 

## <a name="create-performance-category-and-counters"></a>성능 범주 및 카운터 만들기
hello의 hello CreatePeformanceCategoryAndCounters 메서드를 호출 하는 toocreate hello 카운터 [ShardMapManagmentFactory 클래스](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx)합니다. 관리자만 hello 메서드를 실행할 수 있습니다. 

    ShardMapManagerFactory.CreatePerformanceCategoryAndCounters()  

사용할 수도 있습니다 [이](https://gallery.technet.microsoft.com/scriptcenter/Elastic-DB-Tools-for-Azure-17e3d283) PowerShell 스크립트 tooexecute hello 메서드. hello 메서드는 다음 성능 카운터 hello를 만듭니다.  

* **매핑 캐시**: hello 분할 맵에 대 한 캐시 된 매핑 수입니다.
* **DDR 작업/초**: hello 분할 맵에 대 한 데이터 종속 라우팅 작업 속도입니다. 이 카운터는 호출할 때 업데이트 됩니다 너무[OpenConnectionForKey()](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) 연결 성공 toohello 대상 분할 영역에 발생 합니다. 
* **조회 캐시 적중/sec 매핑**: hello shard map의 매핑에 대 한 성공적인 캐시 조회 작업 속도입니다. 
* **조회 캐시 누락 수/초 매핑**: hello shard map의 매핑에 대 한 실패 한 캐시 조회 작업 속도입니다.
* **매핑에서에서 추가 되거나 업데이트 캐시/sec**: 속도 매핑이 추가 되 고 또는 분할 맵 hello에 대 한 업데이트에서 캐시 합니다. 
* **캐시/sec에서 매핑을 제거**: hello 분할 맵에 대 한 캐시에서 매핑을 제거 되 고 있는 비율입니다. 

성능 카운터는 프로세스마다 각각의 캐시된 분할 맵에 생성됩니다.  

## <a name="notes"></a>참고 사항
hello 다음 이벤트를 트리거할 hello 성능 카운터의 hello 만들기:  

* Hello의 초기화 [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) 와 [즉시 로드](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerloadpolicy.aspx)hello ShardMapManager 모든 분할 맵에 포함 된 경우. 여기에 hello [GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx?f=255&MSPPError=-2147217396#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerFactory.GetSqlShardMapManager%28System.String,Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerLoadPolicy%29) 및 hello [TryGetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx) 메서드.
* 분할된 맵의 성공적인 조회([GetShardMap()](https://msdn.microsoft.com/library/azure/dn824215.aspx), [GetListShardMap()](https://msdn.microsoft.com/library/azure/dn824212.aspx) 또는 [GetRangeShardMap()](https://msdn.microsoft.com/library/azure/dn824173.aspx) 사용). 
* CreateShardMap()을 사용한 분할된 맵의 성공적인 조회.

hello 성능 카운터에서 분할 맵은 hello 및 매핑을 수행 하는 모든 캐시 작업에 의해 업데이트 됩니다. 성공적으로 hello 분할 맵은 DeleteShardMap () reults hello 성능 카운터 인스턴스 삭제에 사용 하 여 제거 합니다.  

## <a name="best-practices"></a>모범 사례
* Hello ShardMapManager 개체를 만들기 전에 hello 성능 범주 및 카운터의 생성을 한 번만 수행 되어야 합니다. Hello 명령 실행할 때마다 CreatePerformanceCategoryAndCounters() 지웁니다 (모든 인스턴스에서 보고 하는 데이터 손실) hello 이전 카운터 하 고 새로 만듭니다.  
* 성능 카운터 인스턴스는 프로세스 마다 생성됩니다. 모든 응용 프로그램 충돌 또는 hello 캐시에서 분할 맵은 제거 hello 성능 카운터 인스턴스 삭제 됩니다.  

### <a name="see-also"></a>참고 항목
[탄력적 데이터베이스 기능 개요](sql-database-elastic-scale-introduction.md)  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->

