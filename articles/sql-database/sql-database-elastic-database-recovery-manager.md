---
title: "복구 관리자 toofix 분할 aaaUsing 매핑할 문제 | Microsoft Docs"
description: "분할 맵 hello RecoveryManager 클래스 toosolve 문제를 사용 하 여"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 45520ca3-6903-4b39-88ba-1d41b22da9fe
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: ddove
ms.openlocfilehash: 2218fb15122f1df466e65483480461e366317f2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-recoverymanager-class-toofix-shard-map-problems"></a>Hello RecoveryManager 클래스 toofix 분할 맵 문제를 사용 하 여
hello [RecoveryManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.aspx) 클래스 검색 하 고 hello 전역 분할 맵은 (GSM)와 분할 된 데이터베이스 환경에서 로컬 분할 맵은 hello (LSM) 간의 불일치를 수정 하는 hello 기능 tooeasily ADO.Net 응용 프로그램을 제공 합니다. 

hello GSM 및 LSM 트랙 hello 매핑 분할 환경에서 각 데이터베이스의 합니다. 경우에 따라서는 hello GSM 사이의 hello LSM 중단이 발생 합니다. 이 경우 RecoveryManager 클래스 toodetect hello를 사용 하 고 hello 나누기 복구.

hello RecoveryManager 클래스 hello의 일부인 [탄력적 데이터베이스 클라이언트 라이브러리](sql-database-elastic-database-client-library.md)합니다. 

![분할된 맵][1]

용어 정의는 [탄력적 데이터베이스 도구 용어집](sql-database-elastic-scale-glossary.md)을 참조하세요. toounderstand 어떻게 hello **ShardMapManager** toomanage 사용 되는 데이터는 분할 솔루션에서 참조 [분할 맵 관리](sql-database-elastic-scale-shard-map-management.md)합니다.

## <a name="why-use-hello-recovery-manager"></a>Hello 복구 관리자를 사용 하는 이유는?
분할된 데이터베이스 환경에서는 데이터베이스당 한 개의 테넌트가 있고 서버당 여러 데이터베이스가 있습니다. 또한에 있을 수 있습니다 많은 서버 hello 환경입니다. 각 데이터베이스는 라우트된 toohello 올바른 서버 및 데이터베이스 호출 될 수 있도록 hello 분할 맵을에 매핑됩니다. Tooa에 따라 데이터베이스를 추적 **분할 키**, 각 분할에 할당 되 고 한 **키 값의 범위**합니다. 분할 키가 너무 "F." "D"에서 hello 고객 이름을 나타낼 수는 예를 들어 모든 분할 영역 (즉, 데이터베이스)의 매핑이 hello 및 해당 매핑을 범위 hello에 포함 된 **글로벌 분할 맵은 (GSM)**합니다. 각 데이터베이스에는 hello 라고 하는 hello 분할 영역에 포함 된 hello 범위는 맵도 포함 **로컬 분할 맵은 (LSM)**합니다. 응용 프로그램 tooa 분할 된 데이터베이스에 연결 되 면 hello 매핑 hello 앱 빠른 검색을 위해 함께 캐시 됩니다. hello LSM 사용 되는 toovalidate 캐시 된 데이터입니다. 

hello GSM 및 LSM 될 수 있습니다 다음 이유로 hello에 대 한 동기화:

1. 범위가 더 긴 toono 믿고 분할의 hello 삭제 사용 또는 분할 된 데이터베이스의 이름을 바꿀 수 있습니다. **분리되어 분할된 매핑**에서 분할된 데이터베이스 결과 삭제. 마찬가지로 이름이 바뀐 데이터베이스도 분리되어 분할된 데이터베이스 매핑을 발생시킬 수 있습니다. Hello 변경의 hello 의도 따라 hello 분할 toobe 제거 하거나 hello 분할 위치 toobe 업데이트 필요. 삭제 된 데이터베이스는 toorecover 참조 [삭제 된 데이터베이스 복원](sql-database-recovery-using-backups.md)합니다.
2. 지역 장애 조치(failover) 이벤트가 발생합니다. 하나 toocontinue, hello 서버 이름 및 shard map의 모든 분할 영역에 대 한 hello 응용 프로그램 및 업데이트 hello 분할 매핑 정보에 shard map manager의 데이터베이스 이름을 업데이트 해야 합니다. 지리적 장애 조치 하는 경우 이러한 복구 논리 hello 장애 조치 워크플로 내에서 자동화 해야 합니다. 복구 작업을 자동화하면 지역 지원 데이터베이스에 대해 원활한 관리 효율성을 제공하며 사람이 직접 작업하지 않아도 됩니다. 옵션 toorecover 데이터베이스 데이터 센터 중단 경우 참조 하는 방법에 대 한 toolearn [비즈니스 연속성](sql-database-business-continuity.md) 및 [재해 복구](sql-database-disaster-recovery.md)합니다.
3. 분할 또는 hello ShardMapManager 데이터베이스가 복원 된 tooan 이전 지정 시간입니다. 지정 시간 복구 백업을 사용 하 여에 대 한 toolearn 참조 [백업을 사용 하 여 복구](sql-database-recovery-using-backups.md)합니다.

Azure SQL 데이터베이스 탄력적 데이터베이스 도구, 지리적 복제 및 복원 하는 방법에 대 한 자세한 내용은 hello 다음을 참조 하십시오. 

* [개요: SQL 데이터베이스의 클라우드 무중단 업무 방식 및 데이터베이스 재해 복구](sql-database-business-continuity.md) 
* [탄력적 데이터베이스 도구 시작하기](sql-database-elastic-scale-get-started.md)  
* [ShardMap 관리](sql-database-elastic-scale-shard-map-management.md)

## <a name="retrieving-recoverymanager-from-a-shardmapmanager"></a>ShardMapManager에서 RecoveryManager 검색
hello 첫 번째 단계는 toocreate RecoveryManager 인스턴스입니다. hello [GetRecoveryManager 메서드](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getrecoverymanager.aspx) 반환 hello 현재 hello에 대 한 복구 관리자 [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) 인스턴스. tooaddress hello 분할 불일치 매핑할 특정 분할 맵 hello에 대 한 hello RecoveryManager를 먼저 검색 해야 합니다. 

   ```
    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString,  
             ShardMapManagerLoadPolicy.Lazy);
             RecoveryManager rm = smm.GetRecoveryManager(); 
   ```

이 예제에서는 hello RecoveryManager hello ShardMapManager에서에서 초기화 됩니다. hello는 ShardMap 포함 된 ShardMapManager도 이미 초기화 되었습니다. 

Hello 분할 맵 자체를 조작 하는이 응용 프로그램 코드, 이후 hello hello 팩터리 메서드에 사용 되는 자격 증명 (hello 예제에서는 앞에서 smmConnectionString) hello 참조 하는 hello GSM 데이터베이스에 대 한 읽기 / 쓰기 권한이 있는 자격 증명 해야 합니다. 연결 문자열입니다. 이러한 자격 증명은 데이터 종속 라우팅에 사용 된 자격 증명 tooopen 연결 일반적으로 다릅니다. 자세한 내용은 참조 [hello 탄력적 데이터베이스 클라이언트에서 자격 증명을 사용 하 여](sql-database-elastic-scale-manage-credentials.md)합니다.

## <a name="removing-a-shard-from-hello-shardmap-after-a-shard-is-deleted"></a>분할 영역을 삭제 한 조각 hello ShardMap에서 제거
hello [DetachShard 메서드](https://msdn.microsoft.com/library/azure/dn842083.aspx) hello 분할 맵을에서 분할 된 데이터베이스를 지정 하는 hello를 분리 한 hello 분할 된 데이터베이스와 연결 된 매핑을 삭제 합니다.  

* hello 위치 매개 변수는 hello 분할 위치, 특히 서버 이름 및 분리 중인 hello 분할 된 데이터베이스의 데이터베이스 이름입니다. 
* hello shardMapName 매개 변수는 hello shard map 이름. 이만 여러 분할 영역 맵의 hello에서 관리 하는 경우 필수 동일한 shard map manager. 선택 사항입니다. 


> [!IMPORTANT]
> 특정을 업데이트 하는 hello 매핑에 대 한 hello 범위는 비어 있는 경우에이 방법을 사용 합니다. 위의 hello 방법 이동 hello 범위에 대 한 데이터를 검사 하지 않습니다, 그리고 코드에서 tooinclude 확인 되므로 것이 좋습니다.
>

이 예제는 hello 분할 맵을에서 분할 된 데이터베이스를 제거합니다. 

   ```
   rm.DetachShard(s.Location, customerMap);
   ``` 

hello 분할 맵은 hello 분할의 hello 삭제 하기 전에 GSM hello hello 분할 위치를 반영합니다. Hello shard 삭제 되었기 때문에이 의도적인 경우도 hello 분할 키 범위 더 이상에서 사용 하 고 가정 합니다. 그렇지 않은 경우 특정 시점 복원을 실행할 수 있습니다. 이전에 시점에서 toorecover hello 분할 합니다. (이 경우 검토 hello 다음 부분 toodetect 분할 불일치가 있습니다.) toorecover, 참조 [지정 시간 복구가](sql-database-recovery-using-backups.md)합니다.

데이터베이스 삭제 hello 실수가 아니었다면 가정 하므로, hello 관리 최종 정리 동작은 hello shard map manager toodelete hello 항목 toohello 분할 합니다. 이렇게 하면 hello 응용 프로그램에서 예상 되는 정보 tooa 범위를 실수로 작성 됩니다.

## <a name="toodetect-mapping-differences"></a>toodetect 매핑 차이점
hello [DetectMappingDifferences 메서드](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.detectmappingdifferences.aspx) 선택 하 고 정보의 hello 소스로 hello 분할 영역 맵의 (로컬 또는 전역 일) 중 하나를 반환 하 고 모두 분할 영역 맵의 (GSM 및 LSM)에 대 한 매핑을 조정 합니다.

   ```
   rm.DetectMappingDifferences(location, shardMapName);
   ```

* hello *위치* hello 서버 이름과 데이터베이스 이름을 지정 합니다. 
* hello *shardMapName* 매개 변수는 hello shard map 이름입니다. 이만 여러 분할 영역 맵의 hello에서 관리 하는 경우 필요한 동일한 shard map manager. 선택 사항입니다. 

## <a name="tooresolve-mapping-differences"></a>tooresolve 매핑 차이점
hello [ResolveMappingDifferences 메서드](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.resolvemappingdifferences.aspx) hello 소스 source of truth로 hello 분할 맵 (로컬 또는 전역 일) 중 하나를 선택 하 고 모두 분할 영역 맵의 (GSM 및 LSM)에 대 한 매핑 조정 합니다.

   ```
   ResolveMappingDifferences (RecoveryToken, MappingDifferenceResolution.KeepShardMapping);
   ```

* hello *RecoveryToken* GSM hello와 hello 특정 분할에 대 한 hello LSM 간의 hello 매핑 hello 차이 열거 하는 매개 변수입니다. 
* hello [MappingDifferenceResolution 열거형](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.mappingdifferenceresolution.aspx) hello 분할 매핑 hello 차이 해결 하는 데 사용 되는 tooindicate hello 메서드입니다. 
* **MappingDifferenceResolution.KeepShardMapping** 는 것이 좋습니다 hello LSM hello 정확한 매핑을 포함 하 고 따라서 hello 매핑 hello 분할 영역에 사용 해야 합니다. 이 일반적으로 hello 경우 장애 조치가 있을: hello 분할 이제 새 서버에 상주 합니다. Hello 분할 hello GSM (hello RecoveryManager.DetachShard 방법 사용)에서 제거 해야, 이후 매핑을 GSM hello에 존재 하지 않습니다. 따라서 hello LSM 사용된 toore 해야-hello 분할 매핑을 설정 합니다.

## <a name="attach-a-shard-toohello-shardmap-after-a-shard-is-restored"></a>분할 된 데이터베이스는 복원 된 후 분할 toohello ShardMap 연결
hello [AttachShard 메서드](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.attachshard.aspx) 연결 합니다. 지정 된 분할 toohello 분할 맵을 hello 합니다. 다음 shard map 불일치를 검색 하 고 hello 분할 된 데이터베이스 복원의 hello 시점 hello 매핑 toomatch hello 분할을 업데이트 합니다. 해당 hello 데이터베이스 이므로 또한 이름이 바뀐된 tooreflect hello 원래 데이터베이스 이름을 (복원 하기 전에 hello 분할 되었습니다) hello 지정 시간 복원 hello 타임 스탬프가 추가 tooa 새 데이터베이스의 기본값을 가정 합니다. 

   ```
   rm.AttachShard(location, shardMapName)
   ``` 

* hello *위치* 매개 변수는 hello 서버 이름 및 연결 되 고 hello 분할 된 데이터베이스의 데이터베이스 이름입니다. 
* hello *shardMapName* 매개 변수는 hello shard map 이름입니다. 이만 여러 분할 영역 맵의 hello에서 관리 하는 경우 필수 동일한 shard map manager. 선택 사항입니다. 

이 예제는 이전 지정 시간에서 최근에 복원 된 분할 toohello 분할 맵을 추가 합니다. Hello 분할 (즉 hello LSM hello에 hello 분할에 대 한 매핑)을 복원한 후 GSM hello에 hello 분할 항목을 가진 잠재적으로 일치 하지 않습니다. 이 예제에서는 코드 외부에서 hello 분할이 복원 되 고 toohello hello 데이터베이스의 원래 이름을 바뀝니다. 복원 된 후 hello LSM의에서 hello 매핑은 hello 신뢰할 수 있는 매핑이 간주 됩니다. 

   ```
   rm.AttachShard(s.Location, customerMap); 
   var gs = rm.DetectMappingDifferences(s.Location); 
      foreach (RecoveryToken g in gs) 
       { 
       rm.ResolveMappingDifferences(g, MappingDifferenceResolution.KeepShardMapping); 
       } 
   ```

## <a name="updating-shard-locations-after-a-geo-failover-restore-of-hello-shards"></a>지역-장애 조치 이후 (복원) hello 분할 된 데이터베이스의 분할 위치를 업데이트합니다.
지리적 장애 조치 이면 hello 보조 데이터베이스를 액세스할 수 있도록 작성 하 고 hello 새로운 주 데이터베이스를 됩니다. hello hello 서버 및 잠재적으로 (구성)에 따라 다름 hello 데이터베이스의 이름, 원래 주 hello에서에서 다를 수 있습니다. 따라서 hello GSM의에서 hello 분할에 대 한 매핑 항목을 hello 및 LSM 수정 해야 합니다. 마찬가지로, 경우 hello 데이터베이스가 복원 된 tooa 다른 이름 또는 위치 또는 tooan 시간상에서 이전 지점 hello 분할 맵에서 불일치가 발생할 수 있습니다. Shard Map Manager hello 열려 있는 연결 toohello 올바른 데이터베이스의 hello 분포를 처리합니다. 배포는 hello 및 데이터를 분할 맵은 hello hello hello 응용 프로그램 요청의 hello 대상인 hello 분할 키 값을 기반으로 합니다. 지리적 장애 조치 후 hello 정확한 서버 이름, 데이터베이스 이름 및 분할 매핑 hello 복구 데이터베이스의 사용이 정보를 업데이트 해야 합니다. 

## <a name="best-practices"></a>모범 사례
지리적 장애 조치 및 복구는 일반적으로 의도적으로 Azure SQL 데이터베이스 비즈니스 연속성 기능 중 하나를 사용 하 여 hello 응용 프로그램의 클라우드 관리자가 관리 하는 작업입니다. 비즈니스 연속성 계획 프로세스, 절차 및 비즈니스 운영을 중단 없이 계속할 수 있음을 측정값 tooensure 필요 합니다. 메서드를 hello hello RecoveryManager 클래스의 일부 사용 되어야 사용할 수 있는이 작업 흐름 tooensure hello 내 GSM 및 LSM 최신 상태로 유지 되며 수행 하는 hello 복구 동작에 따라 합니다. 다섯 가지 기본 단계는 hello 보장 tooproperly GSM와 LSM hello 장애 조치 이벤트가 발생 한 후 정확한 정보를 반영 합니다. 안녕 응용 프로그램 코드 tooexecute 기존 도구 및 워크플로에 다음이 단계를 통합할 수 있습니다. 

1. Hello ShardMapManager에서에서 RecoveryManager hello를 검색 합니다. 
2. Hello 분할 맵에서 분할 된 hello 이전 데이터베이스를 분리 합니다.
3. Hello 새 분할 toohello 분할 맵을 hello 새 분할 위치를 포함 하 여 연결 합니다.
4. GSM 및 LSM hello 간의 매핑 hello에서 불일치를 검색 합니다. 
5. GSM hello 및 hello LSM, 트러스팅 hello LSM 간의 차이 해결 합니다. 

이 예에서는 hello 다음 단계를 수행 합니다.

1. Hello hello 장애 조치 이벤트가 발생 하기 전에 분할 위치를 반영 하는 분할 맵을에서 분할 된 데이터베이스를 제거 합니다.
2. 분할 된 데이터베이스 toohello 분할 맵은 반사 hello 새 분할 위치에 연결 (hello 매개 변수 "Configuration.SecondaryServer" hello 새 서버 이름 이지만 hello 동일한 데이터베이스 이름).
3. GSM hello 및 각 분할에 대 한 hello LSM 매핑 차이점을 검색 하 여 hello 복구 토큰을 검색 합니다. 
4. 각 분할의 LSM hello에서 트러스팅 hello 매핑에 의해 hello 불일치를 해결합니다. 
   
   ```
   var shards = smm.GetShards(); 
   foreach (shard s in shards) 
   { 
     if (s.Location.Server == Configuration.PrimaryServer) 
   
         { 
          ShardLocation slNew = new ShardLocation(Configuration.SecondaryServer, s.Location.Database); 
   
          rm.DetachShard(s.Location); 
   
          rm.AttachShard(slNew); 
   
          var gs = rm.DetectMappingDifferences(slNew); 
   
          foreach (RecoveryToken g in gs) 
            { 
               rm.ResolveMappingDifferences(g, MappingDifferenceResolution.KeepShardMapping); 
            } 
        } 
    } 
   ```

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-database-recovery-manager/recovery-manager.png

