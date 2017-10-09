---
title: "T-SQL: Azure SQL Database 탄력적 풀 관리 | Microsoft Docs"
description: "T-SQL toomanage Azure SQL 데이터베이스 탄력적 풀을 사용 합니다."
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 4e288e17-bc3e-4255-9fbe-0a2ac0dbd7dd
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 05/27/2016
ms.author: srinia
ms.openlocfilehash: 666f131b2c88849a1a9ea83381bbc27548e93599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a>Transact-SQL로 탄력적 풀 모니터링 및 관리
이 항목에서는 확장 가능한 toomanage [탄력적 풀](sql-database-elastic-pool.md) transact-sql입니다.  또한 생성 하 고 Azure 탄력적 풀 hello 관리 수 [Azure 포털](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), REST API hello 또는 [C#](sql-database-elastic-pool-manage-csharp.md)합니다. [Transact-SQL](sql-database-elastic-pool-manage-tsql.md)을 사용하여 탄력적 풀을 만들고 여기에 데이터베이스를 넣거나 뺄 수도 있습니다.


사용 하 여 hello [Create Database (Azure SQL 데이터베이스)](https://msdn.microsoft.com/library/dn268335.aspx) 및 [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) 내부 / 외부로 탄력적 풀 toocreate 및 이동 데이터베이스 명령입니다. 이러한 명령을 사용 하기 전에 hello 탄력적 풀 존재 해야 합니다. 이러한 명령은 데이터베이스에만 적용됩니다. 새 풀 만들기 및 풀 속성 (예: min 및 max Edtu)의 hello 설정 T-SQL 명령을 사용 하 여 변경할 수 없습니다.

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>탄력적 풀에 풀링된 데이터베이스 만들기
SERVICE_OBJECTIVE 옵션 hello로 hello CREATE DATABASE 명령을 사용 합니다.   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

탄력적 풀의 모든 데이터베이스에는 hello 서비스 계층 (Basic, Standard, Premium) hello 탄력적 풀의 상속합니다. 

## <a name="move-a-database-between-elastic-pools"></a>탄력적 풀 간에 데이터베이스 이동
서비스 설정 및 수정 hello로 hello ALTER DATABASE 명령을 사용 하 여\_탄력적으로 목표 옵션\_풀입니다. Hello 대상 풀의 hello 이름 toohello 이름을 설정 합니다.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move hello database named db1 tooan elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a>탄력적 풀로 데이터베이스 이동
서비스 설정 및 수정 hello로 hello ALTER DATABASE 명령을 사용 하 여\_ELASTIC_POOL으로 목표 옵션입니다. Hello 대상 풀의 hello 이름 toohello 이름을 설정 합니다.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move hello database named db1 tooan elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a>탄력적 풀 외부로 데이터베이스 이동
Hello ALTER DATABASE 명령을 사용 하 고 hello SERVICE_OBJECTIVE tooone hello 성능 수준 (예: S0 또는 S1)를 설정 합니다.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes hello database into a stand-alone database with hello service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a>탄력적 풀에 데이터베이스 나열
사용 하 여 hello [sys.database\_서비스 \_목표 보기](https://msdn.microsoft.com/library/mt712619) toolist 모든 hello 탄력적 풀의 데이터베이스입니다. 데이터베이스 tooquery hello 뷰 toohello 마스터에 로그인 합니다.

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>탄력적 풀에 대한 리소스 사용량 데이터 가져오기
사용 하 여 hello [sys.elastic\_풀 \_리소스 \_통계 보기](https://msdn.microsoft.com/library/mt280062.aspx) 논리 서버에 탄력적 풀의 tooexamine hello 리소스 사용 통계입니다. 데이터베이스 tooquery hello 뷰 toohello 마스터에 로그인 합니다.

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a>풀링된 데이터베이스에 대한 리소스 사용량 가져오기
사용 하 여 hello [sys.dm\_ db\_ 리소스\_통계 보기](https://msdn.microsoft.com/library/dn800981.aspx) 또는 [sys.resource \_통계 보기](https://msdn.microsoft.com/library/dn269979.aspx) 의 tooexamine hello 리소스 사용 통계는 탄력적 풀의 데이터베이스입니다. 이 프로세스는 단일 데이터베이스에 대 한 유사한 tooquerying 리소스 사용.

## <a name="next-steps"></a>다음 단계
탄력적 풀을 만든 후 탄력적 작업 하 여 hello 풀에서 탄력적 데이터베이스를 관리할 수 있습니다. 탄력적 작업 용이 개수에 관계 없이 hello 풀의 데이터베이스에 대해 T-SQL 스크립트를 실행 합니다. 자세한 내용은 [탄력적 데이터베이스 작업 개요](sql-database-elastic-jobs-overview.md)를 참조하세요. 

참조 [Azure SQL 데이터베이스를 사용한 수평 확장](sql-database-elastic-scale-introduction.md): 탄력적 데이터베이스 도구 tooscale 아웃을 사용 하 여 데이터를 이동, 쿼리 또는 트랜잭션을 만드는 합니다.

