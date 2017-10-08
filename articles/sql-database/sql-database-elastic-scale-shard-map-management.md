---
title: "Azure SQL 데이터베이스 아웃 aaaScale | Microsoft Docs"
description: "어떻게 toouse hello ShardMapManager, 탄력적 데이터베이스 클라이언트 라이브러리"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 0e9d647a-9ba9-4875-aa22-662d01283439
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 4cf670d42ad7ded98fb8d6f0830154587dd2c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-out-databases-with-hello-shard-map-manager"></a>Hello shard map manager와 함께 데이터베이스 확장
SQL Azure에서 데이터베이스 확장 tooeasily shard map manager를 사용 합니다. hello shard map manager는 분할 집합의 모든 분할 영역 (데이터베이스)에 대 한 전역 매핑 정보를 유지 하는 특별 한 데이터베이스입니다. hello 메타 데이터를 통해 응용 프로그램 tooconnect toohello 올바른 데이터베이스의 hello hello 값에 따라 **분할 키**합니다. Hello 집합의 모든 분할 hello 로컬 분할 데이터를 추적 하는 지도 포함 하는 또한 (라고 **shardlet**). 

![분할된 데이터베이스 맵 관리](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

이러한 맵은 생성 하는 방법을 이해 하는 것은 필수 tooshard 맵 관리 있습니다. 이 작업은 수행 hello를 사용 하 여 [ShardMapManager 클래스](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)hello에 [탄력적 데이터베이스 클라이언트 라이브러리](sql-database-elastic-database-client-library.md) toomanage 분할 영역에 매핑합니다.  

## <a name="shard-maps-and-shard-mappings"></a>분할된 데이터베이스 맵 및 분할된 데이터베이스 매핑
각 분할에 대 한 분할 맵 toocreate hello 종류를 선택 해야 합니다. hello 데이터베이스 아키텍처에 따라 hello 선택: 

1. 데이터베이스당 단일 테넌트  
2. 데이터베이스당 다중 테넌트(두 가지 형식):
   1. 목록 매핑
   2. 범위 매핑

단일 테넌트 모델은 **목록 매핑** 분할된 데이터베이스 맵을 만듭니다. 테 넌 트 당 하나의 데이터베이스만 hello 단일 테 넌 트 모델을 할당합니다. 관리를 단순화하므로 SaaS 개발자에게 효과적인 모델입니다.

![목록 매핑][1]

hello 다중 테 넌 트 모델 할당 하는 여러 테 넌 트 tooa 단일 데이터베이스 (및 여러 데이터베이스에 걸쳐 테 넌 트의 그룹을 배포할 수 있습니다). 각 테 넌 트 toohave 작은 데이터 요구를 예상 하는 경우이 모델을 사용 합니다. 이 모델을 사용 하 여 테 넌 트 tooa 데이터베이스 범위 할당 **범위 매핑**합니다. 

![범위 매핑][2]

사용 하 여 다중 테 넌 트 데이터베이스 모델을 구현할 수 있습니다는 *목록 매핑* tooassign 여러 테 넌 트 tooa 단일 데이터베이스입니다. 예를 들어 d b 1은 1에서 5, 테 넌 트 id에 대 한 정보를 사용 하는 toostore DB2 7 테 넌 트 및 테 넌 트 10에 대 한 데이터를 저장 하며 

![단일 DB의 다중 테넌트][3] 

### <a name="supported-net-types-for-sharding-keys"></a>분할 키에 대해 지원되는 .Net 형식
탄력적인 크기 조정 지원 hello 다음.Net Framework 형식을 분할 키로:

* 정수
* long
* GUID
* byte[]  
* datetime
* TimeSpan
* datetimeoffset

### <a name="list-and-range-shard-maps"></a>목록 및 범위 분할된 데이터베이스 맵
분할된 데이터베이스 맵은 **개별 분할 키 값의 목록**이나 **분할 키 값의 범위**를 사용하여 생성할 수 있습니다. 

### <a name="list-shard-maps"></a>목록 분할된 데이터베이스 맵
**분할 된 데이터베이스** 포함 **shardlet** 와 분할 맵에 의해 shardlet tooshards의 hello 매핑을 유지 관리 됩니다. A **목록 분할 맵은** hello 개별 키 식별 하는 값 hello shardlet 및 분할 된 데이터베이스로 제공 하는 hello 데이터베이스 간 연결입니다.  **매핑을 나열 합니다.** 은 명시적 및 서로 다른 키 값에 매핑된 toohello 수 같은 데이터베이스입니다. 예를 들어 키 1 tooDatabase A 매핑하고 3, 6 키 값이 2. 데이터베이스 참조

| 키 | 분할된 데이터베이스 위치 |
| --- | --- |
| 1 |Database_A |
| 3 |Database_B |
| 4 |Database_C |
| 6 |Database_B |
| ... |... |

### <a name="range-shard-maps"></a>범위 분할된 데이터베이스 맵
에 **범위 분할 맵은**, hello 키 범위를 쌍으로 설명 **[낮은 값, 높은 가치의)** 여기서 hello *낮은 값* hello 범위 및 hello hello최소키*귀중* hello 범위 보다 높으며 hello 첫 번째 값입니다. 

예를 들어 **[0, 100)**에는 0 이상 100 미만의 모든 정수가 포함됩니다. 범위 수 지점 toohello 데이터베이스를 동일 하 고 범위를 서로 분리 된 여러 지원 됩니다 (예: [100,200) 및 [400,600) 두 지점 tooDatabase C 아래의 hello 예에서.)

| 키 | 분할된 데이터베이스 위치 |
| --- | --- |
| [1,50) |Database_A |
| [50,100) |Database_B |
| [100,200) |Database_C |
| [400,600) |Database_C |
| ... |... |

위에 표시 된 hello 테이블 각각의의 개념적 예는 **ShardMap** 개체입니다. 각 행에는 개인의 간단한 예는 **PointMapping** (예: 목록 분할 맵은 hello) 또는 **RangeMapping** (hello 범위 분할 맵은)에 대 한 개체입니다.

## <a name="shard-map-manager"></a>분할된 데이터베이스 맵 관리자
Hello 클라이언트 라이브러리를 hello shard map manager는 분할 영역 맵의의 모음입니다. 데이터를 관리 하는 hello는 **ShardMapManager** 다음 세 위치에 유지 되는 인스턴스: 

1. **전역 분할 맵 GSM ()**: 모든 분할 영역 맵 및 매핑을 대 한 hello 리포지토리로 데이터베이스 tooserve를 지정 합니다. 특수 테이블 및 저장된 프로시저 toomanage hello 정보를 자동으로 생성 됩니다. 이 일반적으로 작은 데이터베이스 액세스 lightly 넣고 hello 응용 프로그램의 다른 요구에 따라 사용 해야 합니다. hello 테이블은 라는 특수 한 스키마 **__ShardManagement**합니다. 
2. **로컬 분할 맵 (LSM)**: 여러 개의 작은 테이블 및 분할 맵 정보 특정 toothat 분할 관리를 포함 하는 특별 한 저장된 프로시저는 분할 된 데이터베이스는 toobe 수정 toocontain를 지정 하는 모든 데이터베이스입니다. 이 정보 hello GSM의 hello 정보와 중복 이며 hello 응용 프로그램 캐시 toovalidate 분할 맵 정보 없이 GSM; hello에 대 한 모든 부하가 허용 합니다. hello 응용 프로그램 캐시 된 매핑을 여전히 유효한 경우 LSM toodetermine hello를 사용 합니다. hello 테이블 각 분할에 LSM가 hello 스키마에도 해당 toohello **__ShardManagement**합니다.
3. **Application cache**: **ShardMapManager** 개체에 액세스하는 각 응용 프로그램 인스턴스는 해당 매핑의 로컬 메모리 내 캐시를 유지 관리합니다. 이 캐시는 최근에 검색된 라우팅 정보를 저장합니다. 

## <a name="constructing-a-shardmapmanager"></a>ShardMapManager 생성
**ShardMapManager** 개체는 [팩터리](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) 패턴을 사용하여 생성됩니다. hello  **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**  hello 형식의 메서드는 자격 증명 (hello 서버 이름 및 hello GSM을 보유 하는 데이터베이스 이름 포함)는  **ConnectionString** 의 인스턴스를 반환 하는 **ShardMapManager**합니다.  

**주의 사항:** hello **ShardMapManager** 는 응용 프로그램에 대 한 hello 초기화 코드 내에서 응용 프로그램 도메인당 한 번만 인스턴스화할 수 있습니다. 만들 인스턴스의 ShardMapManager hello에 동일한 appdomain hello 응용 프로그램의 CPU 사용률이 향상 된 메모리에 발생 합니다. **ShardMapManager** 는 분할된 데이터베이스 맵을 개수와 관계없이 포함할 수 있습니다. 많은 응용 프로그램의 경우 단일 분할된 데이터베이스 맵으로 충분할 수 있지만 서로 다른 스키마에 대해서 또는 고유성을 위해서는 서로 다른 데이터베이스 집합이 사용되며 이러한 경우 다중 분할된 데이터베이스 맵을 사용하는 것이 좋습니다. 

이 코드에서는 응용 프로그램이 하면 기존의 tooopen **ShardMapManager** hello로 [TryGetSqlShardMapManager 메서드](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)합니다.  경우는 Global를 나타내는 개체 **ShardMapManager** hello 클라이언트 라이브러리가 만들어 있습니다 hello를 사용 하 여, GSM ()는 그렇지 않습니다 아직 hello 데이터베이스 내부 존재 [CreateSqlShardMapManager 메서드](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)합니다.

    // Try tooget a reference toohello Shard Map Manager 
     // via hello Shard Map Manager database.  
    // If it doesn't already exist, then create it. 
    ShardMapManager shardMapManager; 
    bool shardMapManagerExists = ShardMapManagerFactory.TryGetSqlShardMapManager(
                                        connectionString, 
                                        ShardMapManagerLoadPolicy.Lazy, 
                                        out shardMapManager); 

    if (shardMapManagerExists) 
     { 
        Console.WriteLine("Shard Map Manager already exists");
    } 
    else
    {
        // Create hello Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // hello connectionString contains server name, database name, and admin credentials 
        // for privileges on both hello GSM and hello shards themselves.
    } 

대신 Powershell toocreate 새 Shard Map Manager를 사용할 수 있습니다. [여기](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)에 예제가 있습니다.

## <a name="get-a-rangeshardmap-or-listshardmap"></a>RangeShardMap 또는 ListShardMap 가져오기
Hello를 얻을 수는 shard map manager를 만든 후 [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) 또는 [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) hello를 사용 하 여 [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [ TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), 또는 hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) 메서드.

    /// <summary>
    /// Creates a new Range Shard Map with hello specified name, or gets hello Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try tooget a reference toohello Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // hello Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a>분할된 데이터베이스 맵 관리 자격 증명
관리 및 분할 맵에 조작 하는 응용 프로그램은 hello 분할 맵을 tooroute 연결을 사용 하는 다릅니다. 

tooadminister 분할 맵 (추가 또는 분할 된 데이터베이스, 분할 영역 맵의 분할 매핑 등 변경) hello 인스턴스화해야 **ShardMapManager** 를 사용 하 여 **권한이 있는 자격 증명 읽기/쓰기 권한 모두 hello GSM 데이터베이스 및 각 분할 영역으로 사용 되는 데이터베이스**합니다. hello 자격 증명 허용 해야 두 hello의 hello 테이블에 대 한 쓰기 GSM 및 LSM 분할 맵 정보를 입력 하거나도 새 분할 영역에 LSM 테이블을 만들 때와 수정으로 합니다.  

참조 [tooaccess hello 탄력적 데이터베이스 클라이언트 라이브러리를 사용 하는 자격 증명](sql-database-elastic-scale-manage-credentials.md)합니다.

### <a name="only-metadata-affected"></a>영향을 받는 메타데이터만
Hello를 변경 하거나 채우는 사용 되는 메서드의 **ShardMapManager** 데이터 자체 hello 분할 영역에 저장 된 hello 사용자 데이터를 변경 하지 않습니다. 와 같은 예를 들어 메서드 **CreateShard**, **DeleteShard**, **UpdateMapping**등 hello shard map 메타 데이터만 영향을 줍니다. 제거 하지 않습니다, 추가 또는 hello 분할 영역에 포함 된 사용자 데이터를 변경 합니다. 대신, 이러한 메서드는 사용 되는 디자인 된 toobe 별도 작업와 함께에서 하면 toocreate 수행 실제 데이터베이스를 제거 또는 이동 하는 분할 환경 tooanother toorebalance 하나의 분할 영역에서에서 행.  (hello **분할 / 병합** 탄력적 데이터베이스 도구에 포함 된 도구에서 분할 된 데이터베이스 간에 실제 데이터 이동을 오케스트레이션 함께 이러한 Api를 활용 합니다.) 참조 [hello 탄력적 데이터베이스 분할 / 병합 도구를 사용 하 여 크기 조정](sql-database-elastic-scale-overview-split-and-merge.md)합니다.

## <a name="populating-a-shard-map-example"></a>분할된 데이터베이스 맵 채우기 예제
시퀀스 작업 toopopulate 특정 분할 맵은의 예는 다음과 같습니다. hello 코드는 다음이 단계를 수행합니다. 

1. 새로운 분할된 데이터베이스 맵이 분할된 데이터베이스 맵 관리자 내에 생성됩니다. 
2. 두 개의 서로 다른 분할 영역에 대 한 메타 데이터 hello toohello 분할 맵을 추가 됩니다. 
3. 다양 한 키 범위 매핑 추가 되 고 hello hello shard map의 전체 내용이 표시 됩니다. 

hello 코드 hello 메서드 오류가 발생 한 경우 다시 실행할 수 있도록 기록 됩니다. 분할 영역이 있는지 여부를 테스트 하는 각 요청 또는 toocreate 시도 하기 전에 매핑이 이미 존재 하기. hello이 코드에서는 데이터베이스 라는 **sample_shard_0**, **sample_shard_1** 및 **sample_shard_2** 문자열에서참조하는hello서버에이미만들어져**shardServer**합니다. 

    public void CreatePopulatedRangeMap(ShardMapManager smm, string mapName) 
        {            
            RangeShardMap<long> sm = null; 

            // check if shardmap exists and if not, create it 
            if (!smm.TryGetRangeShardMap(mapName, out sm)) 
            { 
                sm = smm.CreateRangeShardMap<long>(mapName); 
            } 

            Shard shard0 = null, shard1=null; 
            // Check if shard exists and if not, 
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetShard(new ShardLocation(
                                     shardServer, 
                                     "sample_shard_0"), 
                                     out shard0)) 
            { 
                Shard0 = sm.CreateShard(new ShardLocation(
                                            shardServer, 
                                            "sample_shard_0")); 
            } 

            if (!sm.TryGetShard(new ShardLocation(
                                    shardServer, 
                                    "sample_shard_1"), 
                                    out shard1)) 
            { 
                Shard1 = sm.CreateShard(new ShardLocation(
                                             shardServer, 
                                            "sample_shard_1"));  
            } 

            RangeMapping<long> rmpg=null; 

            // Check if mapping exists and if not,
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetMappingForKey(0, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                          new RangeMappingCreationInfo<long>
                          (new Range<long>(0, 50), 
                          shard0, 
                          MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(50, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(50, 100), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(100, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long>
                         (new Range<long>(100, 150), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(150, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(150, 200), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(200, out rmpg)) 
            { 
               sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(200, 300), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            // List hello shards and mappings 
            foreach (Shard s in sm.GetShards()
                         .OrderBy(s => s.Location.DataSource)
                         .ThenBy(s => s.Location.Database))
            { 
               Console.WriteLine("shard: "+ s.Location); 
            } 

            foreach (RangeMapping<long> rm in sm.GetMappings()) 
            { 
                Console.WriteLine("range: [" + rm.Value.Low.ToString() + ":" 
                        + rm.Value.High.ToString()+ ")  ==>" +rm.Shard.Location); 
            } 
        } 

PowerShell을 사용 하 여는 대신 스크립트 tooachieve hello 처럼 같은 결과입니다. 사용할 수 있는 일부 hello 샘플 PowerShell 예에서는 [여기](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)합니다.     

분할 영역 맵의 채워지고 나면 hello 지도와 toowork 조정 또는 데이터 액세스 응용 프로그램 만들 수 있습니다. 채우기 hello 지도 조작 하거나까지 다시 발생 하지 않아도 **지도 레이아웃** toochange 필요 합니다.  

## <a name="data-dependent-routing"></a>데이터 종속 라우팅
hello shard map manager 데이터베이스 연결 tooperform hello 응용 프로그램별 데이터 작업을 수행 해야 하는 응용 프로그램에 가장 사용 됩니다. 이러한 연결 hello 올바른 데이터베이스와 연결 되어야 합니다. 이를 **데이터 종속 라우팅**이라고 합니다. 이러한 응용 프로그램에 대 한 hello GSM 데이터베이스에 대 한 읽기 전용 권한이 있는 자격 증명을 사용 하 여 hello 공장에서 shard map manager 개체를 인스턴스화하십시오. 이후 연결에 대 한 개별 요청 toohello 적절 한 분할 데이터베이스를 연결 하기 위해 필요한 자격 증명을 제공 합니다.

이러한 응용 프로그램 (사용 하 여 **ShardMapManager** 읽기 전용 자격 증명으로 연) न ी द toohello 지방 지도나 매핑. 이러한 요구 사항을 위해, 앞서 설명한 대로 더 높은 권한의 자격 증명을 제공하는 PowerShell 스크립트 또는 관리별 응용 프로그램을 만듭니다. 참조 [tooaccess hello 탄력적 데이터베이스 클라이언트 라이브러리를 사용 하는 자격 증명](sql-database-elastic-scale-manage-credentials.md)합니다.

자세한 내용은 [데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md)을 참조하세요. 

## <a name="modifying-a-shard-map"></a>분할된 데이터베이스 맵 수정
분할된 데이터베이스 맵은 여러 방법으로 변경할 수 있습니다. Hello 분할 된 데이터베이스 및 해당 매핑을 설명 하는 hello 메타 데이터를 수정 하는 모든 메서드를 다음 hello 하지만 hello 분할 영역 내에서 데이터를 실제로 수정 하지도 만들거나 하거나 hello 실제 데이터베이스 삭제지 않습니다.  Hello에 대 한 작업 아래에서 설명 하는 hello 분할 맵은 일부 toobe 또는 데이터를 실제로 이동 하는 추가 하 고 분할 된 데이터베이스 역할을 수행 하는 데이터베이스를 제거 하는 관리 작업을 조정 해야 합니다.

이러한 메서드는 함께 수정에 사용할 수 있는 hello 빌딩 블록으로 분할 된 데이터베이스 환경에서 데이터의 전체 분포 hello 합니다.  

* 분할 된 데이터베이스 tooadd 또는 제거: 사용 하 여  **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)**  및  **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)**  hello의 [Shardmap 클래스](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx)합니다. 
  
    hello 서버 및 데이터베이스 hello 대상 분할 영역을 나타내는 이미 존재 해야 이러한 작업 tooexecute 합니다. 이러한 메서드 hello 데이터베이스 자체를 hello shard map의 메타 데이터에 대해서만에 영향을 받지를 갖지 않습니다.
* toocreate / 제거를 점 또는 범위는 매핑된 toohello 분할: 사용 하 여  **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**,  **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)**  hello의 [RangeShardMapping 클래스](https://msdn.microsoft.com/library/azure/dn807318.aspx), 및  **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)**  의 hello [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)
  
    많은 다양 한 지점 또는 범위에는 매핑된 toohello 수 동일한 분할 합니다. 이러한 메서드는 메타데이터에만 영향을 주며, 분할된 데이터베이스에 이미 존재하는 데이터에는 영향을 주지 않습니다. 데이터와 일치 하는 순서 toobe에 hello 데이터베이스에서 제거 toobe 필요 **DeleteMapping** 작업을 해야 tooperform 이러한 작업이 개별적으로 하지만 이러한 방법을 사용 하 여 함께에서 합니다.  
* toosplit 기존 범위를 두 개 또는 하나에 인접 한 범위 병합: 사용 하 여  **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)**  및  **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**합니다.  
  
    분할 및 병합 작업을 **hello 분할 toowhich 키 값이 매핑되는 변경 하지 마십시오**합니다. 분할의 두 부분으로 기존 범위를 중단 되지만 매핑된 toohello로 둘 다 동일한 분할 합니다. 매핑된 toohello 이미 있는 인접 한 두 범위에서 작동 하는 병합 단일 범위로 통합 하는 동일한 분할 합니다.  hello 점 또는 분할 간 범위 자체의 이동 필요를 사용 하 여 조정 toobe **UpdateMapping** 함께 실제 데이터를 이동 합니다.  Hello를 사용할 수 있습니다 **분할/병합** 이동이 필요한 경우 탄력적 데이터베이스의 일부인 서비스 도구 toocoordinate 분할 맵을 변경 내용 데이터 이동 합니다. 
* toore 맵 (또는 이동) 개별 포인트 또는 범위 toodifferent 조각을: 사용 하 여  **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**합니다.  
  
    데이터와 일치 하는 순서 toobe에 하나의 분할 tooanother에서 이동 toobe 할 수 있으므로 **UpdateMapping** 작업을 해야 tooperform 해당 이동 별도로 하지만 이러한 방법을 사용 하 여 함께에서 합니다.
* 온라인 및 오프 라인 tootake 매핑: 사용 하 여  **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)**  및  **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)**  toocontrol hello의 온라인 상태는 매핑입니다. 
  
    **UpdateMapping** 및 **DeleteMapping**을 비롯하여 매핑이 "오프라인" 상태인 경우에만 분할된 데이터베이스 매핑에 대한 특정 작업이 허용됩니다. 매핑이 오프라인 상태이면 해당 매핑에 포함된 특정 키를 기반으로 하는 데이터 종속 요청이 오류를 반환합니다. 또한 범위 먼저 오프 라인 상태인 경우 모든 연결에 대 한 영향을 받는 toohello 분할 영역 변경 되는 범위에 대해 쿼리에 대 한 순서 tooprevent 일치 하지 않거나 불완전 한 결과에 자동으로 중지 됩니다. 

매핑은.Net에서 변경할 수 없는 개체입니다.  모든 매핑을 변경 하는 hello 메서드 위의 코드에서 모든 참조 toothem도 무효화 합니다. toomake 새 매핑을 변경 하는 hello 메서드의 모든 매핑의 상태를 변경 하는 작업의 더 쉽게 tooperform 시퀀스를 반환 하는 it 작업에 연결 될 수 있으므로 매핑 참조 하십시오. 예를 들어 기존 25 hello 키가 포함 된 shardmap sm에서 매핑을 toodelete, 다음 hello를 실행할 수 있습니다. 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a>분할된 데이터베이스 추가
응용 프로그램 종종 필요한 toosimply 새로운 키 또는 키 범위에서 예상 되는 새 분할 영역이 toohandle 데이터 대 한 추가 분할 맵은 이미 존재 합니다. 예를 들어 테 넌 트 ID에 따라 분할 응용 프로그램 tooprovision 새로운 분할 새 테 넌 트에 대 한 하거나 데이터 분할 매월 새로운 분할 hello 새로운 달이 시작 하기 전에 사용자를 프로 비전 할 수 있습니다. 

Hello 새로운 키 값의 범위로 되어 있지 않은 경우 기존 매핑을 및 데이터 이동 없이 필요한 것이 매우 간단한 tooadd hello 새 분할 영역 및 hello 새 키 또는 범위 toothat 분할 영역을 연결 합니다. 새로운 분할된 데이터베이스를 추가하는 방법에 대한 자세한 내용은 [새로운 분할된 데이터베이스 추가](sql-database-elastic-scale-add-a-shard.md)를 참조하세요.

그러나 데이터를 이동 해야 하는 시나리오에 대 한 hello 분할 / 병합 도구가 hello 필요한 분할 맵 업데이트와 함께에서 분할 영역 간에 필요한 tooorchestrate hello 데이터를 이동을 됩니다. 사용 하 여에 대 한 내용은 분할 / 병합 yool hello, 참조 [분할 / 병합의 개요](sql-database-elastic-scale-overview-split-and-merge.md) 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
