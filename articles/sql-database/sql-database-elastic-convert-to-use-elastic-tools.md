---
title: "tooscale 아웃 데이터베이스 aaaMigrate 기존 | Microsoft Docs"
description: "Shard map manager 만들어 분할 된 데이터베이스 toouse 탄력적 데이터베이스 도구 변환"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 8c851d8e-8fd5-4327-89c1-9178b20ddd69
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: fa2c9e3699f30667cf547d1faadf4504609199be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-existing-databases-tooscale-out"></a>기존 데이터베이스 tooscale 아웃 마이그레이션
Azure SQL 데이터베이스 데이터베이스 도구를 사용 하 여 기존 확장 분할 된 데이터베이스를 쉽게 관리할 (hello 같은 [탄력적 데이터베이스 클라이언트 라이브러리](sql-database-elastic-database-client-library.md)). 먼저 기존 데이터베이스 toouse hello 집합을 변환 해야 [shard map manager](sql-database-elastic-scale-shard-map-management.md)합니다. 

## <a name="overview"></a>개요
toomigrate 기존 분할 된 데이터베이스. 

1. Hello 준비 [shard map manager 데이터베이스](sql-database-elastic-scale-shard-map-management.md)합니다.
2. Hello 분할 맵을 만듭니다.
3. Hello 개별 분할 된 데이터베이스를 준비 합니다.  
4. 매핑 toohello 분할 맵을 추가 합니다.

이러한 기술은 두 hello를 사용 하 여 구현할 수 있습니다 [.NET Framework 클라이언트 라이브러리](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), 있거나 hello PowerShell 스크립트에 [Azure SQL DB-탄력적 데이터베이스 도구 스크립트](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)합니다. 여기에 hello 예제는 hello PowerShell 스크립트를 사용합니다.

ShardMapManager hello에 대 한 자세한 내용은 참조 [분할 맵 관리](sql-database-elastic-scale-shard-map-management.md)합니다. Hello 탄력적 데이터베이스 도구 개요를 참조 하십시오. [탄력적 데이터베이스 기능 개요](sql-database-elastic-scale-introduction.md)합니다.

## <a name="prepare-hello-shard-map-manager-database"></a>Hello shard map manager 데이터베이스를 준비
hello shard map manager는 hello 데이터 toomanage 수평 확장 된 데이터베이스를 포함 하는 특별 한 데이터베이스입니다. 기존 데이터베이스를 사용하거나 새 데이터베이스를 만들 수 있습니다. 참고는 동일한 분할 영역으로 데이터베이스는 데이터베이스 역할을 하는 shard map manager hello 되어서는 안 됩니다. PowerShell 스크립트 hello 데이터베이스가 만들어지지 않습니다 hello 드립니다 note도 합니다. 

## <a name="step-1-create-a-shard-map-manager"></a>1단계: 분할된 데이터베이스 맵 관리자 만들기
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are hello server name and database name 
    # for hello new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="tooretrieve-hello-shard-map-manager"></a>tooretrieve hello shard map manager
를 만든 후이 cmdlet과 hello shard map manager을 검색할 수 있습니다. Toouse hello ShardMapManager 개체 할 때마다이 단계가 필요 합니다.

    # Try tooget a reference toohello Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-hello-shard-map"></a>2 단계: hello 분할 맵 만들기
분할 맵 toocreate hello 종류를 선택 해야 합니다. hello 데이터베이스 아키텍처에 따라 hello 선택: 

1. 데이터베이스 마다 단일 테 넌 트 (말해서 참조 hello [용어집](sql-database-elastic-scale-glossary.md).) 
2. 데이터베이스당 다중 테넌트(두 가지 형식):
   1. 목록 매핑
   2. 범위 매핑

단일 테넌트 모델은 **목록 매핑** 분할된 데이터베이스 맵을 만듭니다. 테 넌 트 당 하나의 데이터베이스만 hello 단일 테 넌 트 모델을 할당합니다. 관리를 단순화하므로 SaaS 개발자에게 효과적인 모델입니다.

![목록 매핑][1]

hello 다중 테 넌 트 모델 할당 하는 여러 테 넌 트 tooa 단일 데이터베이스 (및 여러 데이터베이스에 걸쳐 테 넌 트의 그룹을 배포할 수 있습니다). 각 테 넌 트 toohave 작은 데이터 요구를 예상 하는 경우이 모델을 사용 합니다. 이 모델을 사용 하 여 테 넌 트 tooa 데이터베이스 범위 할당 **범위 매핑**합니다. 

![범위 매핑][2]

사용 하 여 다중 테 넌 트 데이터베이스 모델을 구현할 수 있습니다는 *목록 매핑* tooassign 여러 테 넌 트 tooa 단일 데이터베이스입니다. 예를 들어 d b 1은 1에서 5, 테 넌 트 id에 대 한 정보를 사용 하는 toostore DB2 7 테 넌 트 및 테 넌 트 10에 대 한 데이터를 저장 하며 

![단일 DB의 다중 테넌트][3] 

**다음 옵션 중 하나를 선택합니다.**

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a>옵션1: 목록 매핑에 대한 분할된 데이터베이스 맵 만들기
Hello ShardMapManager 개체를 사용 하 여 분할 맵을 만듭니다. 

    # $ShardMapManager is hello shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a>옵션 2: 범위 매핑에 대한 분할된 데이터베이스 맵 만들기
해당 tooutilize이 매핑 패턴에 유의 테 넌 트 id 값이 필요한 toobe 연속 범위 며 hello 범위에 허용 가능한 toohave 간격이 hello 데이터베이스를 만들 때 단순히 hello 범위를 건너뜁니다.

    # $ShardMapManager is hello shard map manager object 
    # 'RangeShardMap' is hello unique identifier for hello range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a>옵션 3: 단일 데이터베이스의 목록 매핑
2단계 옵션 1과 같이 이 패턴을 설정할 때도 목록 맵을 만들어야 합니다.

## <a name="step-3-prepare-individual-shards"></a>3단계: 개별 분할된 데이터베이스 준비
각 분할 (데이터베이스) toohello shard map 관리자를 추가 합니다. 이 매핑 정보를 저장 하기 위한 hello 개별 데이터베이스를 준비 합니다. 각각의 분할된 데이터베이스에서 이 메서드를 실행합니다.

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # hello $ShardMap is hello shard map created in step 2.


## <a name="step-4-add-mappings"></a>4단계: 매핑 추가
매핑 hello 추가 만든 분할 영역 맵의 hello 종류에 따라 다릅니다. 목록 맵을 만든 경우 목록 매핑을 추가합니다. 범위 맵을 만든 경우 범위 매핑을 추가합니다.

### <a name="option-1-map-hello-data-for-a-list-mapping"></a>옵션 1: 목록 매핑에 대 한 hello 데이터 매핑
각 테 넌 트에 대 한 목록 매핑을 추가 하 여 hello 데이터를 매핑하십시오.  

    # Create hello mappings and associate it with hello new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-hello-data-for-a-range-mapping"></a>옵션 2: 범위 매핑에 대 한 hello 데이터 매핑
모든 hello 테 넌 트 id 범위-데이터베이스 연결에 대 한 hello 범위 매핑을 추가 합니다.

    # Create hello mappings and associate it with hello new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-hello-data-for-multiple-tenants-on-a-single-database"></a>4 단계 옵션 3: 단일 데이터베이스에서 여러 테 넌 트에 대 한 hello 데이터 매핑
각 테 넌 트에 대 한 추가 ListMapping hello 실행 (위의 1, 옵션). 

## <a name="checking-hello-mappings"></a>Hello 매핑을 확인 하는 중
다음 명령을 사용 하 여 hello 기존 분할 영역 및 연결 된 hello 매핑을 대 한 정보를 쿼리할 수 있습니다.  

    # List hello shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a>요약
Hello 설치를 완료 한 후 toouse hello 탄력적 데이터베이스 클라이언트 라이브러리를 시작할 수 있습니다. 또한 [데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md) 및 [다중 분할된 데이터베이스 쿼리](sql-database-elastic-scale-multishard-querying.md)를 사용할 수도 있습니다.

## <a name="next-steps"></a>다음 단계
Hello PowerShell 스크립트에서 가져와서 [Azure SQL DB 탄력적 데이터베이스 도구 sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)합니다.

hello 도구가 GitHub에도 있는: [Azure/탄력적인-db-도구](https://github.com/Azure/elastic-db-tools)합니다.

다중 테 넌 트 모델 tooa 단일 테 넌 트 모델에서 분할 / 병합 도구 toomove 데이터 tooor hello를 사용 합니다. [분할 병합 도구](sql-database-elastic-scale-get-started.md)를 참조하세요.

## <a name="additional-resources"></a>추가 리소스
다중 테넌트 SaaS(software-as-a-service) 데이터베이스 응용 프로그램의 일반적인 데이터 아키텍처 패턴에 대한 정보는 [Azure SQL 데이터베이스를 사용한 다중 테넌트 SaaS 응용 프로그램의 설계 패턴](sql-database-design-patterns-multi-tenancy-saas-applications.md)을 참조하세요.

## <a name="questions-and-feature-requests"></a>질문 및 기능 요청
질문에 게 연락 하세요 hello에 toous [SQL 데이터베이스 포럼](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) 기능 요청에 대 한 하십시오 추가할 toohello [SQL 데이터베이스 피드백 포럼](https://feedback.azure.com/forums/217321-sql-database/)합니다.

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

