---
title: "hello 탄력적 데이터베이스 클라이언트 라이브러리의 자격 증명 aaaManaging | Microsoft Docs"
description: "Tooset은 tooread 전용 탄력적 데이터베이스 응용 프로그램에 대 한 관리자 자격 증명을 올바른 수준 hello 하는 방법"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 72e0edaf-795e-4856-84a5-6594f735fb7e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 218783ca2a07e3c0a4b089aa92634f32c41386e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="credentials-used-tooaccess-hello-elastic-database-client-library"></a>자격 증명 tooaccess hello 탄력적 데이터베이스 클라이언트 라이브러리 사용
hello [탄력적 데이터베이스 클라이언트 라이브러리](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) 서로 다른 세 가지 자격 증명 tooaccess hello 사용 하 여 [shard map manager](sql-database-elastic-scale-shard-map-management.md)합니다. Hello 요구에 따라 hello 액세스 가능한 가장 낮은 수준으로 hello 자격 증명을 사용 합니다.

* **관리 자격 증명**: 분할된 데이터베이스 맵 관리자를 만들고 조작하는 데 사용됩니다. (참조 hello [용어집](sql-database-elastic-scale-glossary.md).) 
* **자격 증명 액세스**: tooaccess 기존 분할 분할 영역에 대 한 관리자 tooobtain 정보를 매핑합니다.
* **연결 자격 증명**: tooconnect tooshards 합니다. 

[Azure SQL 데이터베이스에서 데이터베이스 및 로그인 관리](sql-database-manage-logins.md)를 참조하세요. 

## <a name="about-management-credentials"></a>관리 자격 증명 정보
관리 자격 증명이 사용 되는 toocreate는 [ **ShardMapManager** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) 분할 영역 맵의 조작 하는 응용 프로그램에 대 한 개체입니다. (예를 들어 참조 [탄력적 데이터베이스 도구를 사용 하 여 분할 영역이 추가](sql-database-elastic-scale-add-a-shard.md) 및 [데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md)) hello 탄력적인 크기 조정 클라이언트 라이브러리의 hello 사용자 hello SQL 사용자와 SQL 로그인 만들어지며 지 부여 hello 글로벌 분할에 대 한 읽기/쓰기 권한을 hello 데이터베이스와 모든 분할 영역 데이터베이스에 매핑합니다. 이러한 자격 증명은 사용 되는 toomaintain hello 글로벌 분할 맵 및 hello 로컬 분할 영역 맵의 변경 내용을 toohello 분할 맵을 수행 되 면입니다. 예를 들어 hello 관리 자격 증명 toocreate hello shard map manager 개체를 사용 하 여 (사용 하 여 [ **GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx): 

    // Obtain a shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmAdminConnectionString, 
            ShardMapManagerLoadPolicy.Lazy 
    ); 

hello 변수 **smmAdminConnectionString** hello 관리 자격 증명이 포함 된 연결 문자열입니다. hello 사용자 ID와 암호 읽기/쓰기 액세스 tooboth 분할 맵 데이터베이스 및 개별 분할 된 데이터베이스를 제공 합니다. hello 관리 연결 문자열에는 hello 서버 이름과 데이터베이스 이름을 tooidentify hello 글로벌 분할 맵 데이터베이스도를 포함 됩니다. 다음은 해당 용도를 위한 일반적인 연결 문자열입니다.

     "Server=<yourserver>.database.windows.net;Database=<yourdatabase>;User ID=<yourmgmtusername>;Password=<yourmgmtpassword>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;” 

Hello 형식의 값을 사용 하지 마십시오 "username@server"-대신 hello "username" 값을 사용 합니다.  즉, 자격 증명 hello shard map manager 데이터베이스와 다른 서버에 있을 수 있는 개별 분할 영역에 대해 작동 해야 합니다.

## <a name="access-credentials"></a>액세스 자격 증명
분할 영역은 분할 맵 관리 하지 않는 응용 프로그램를 맵 manager 만들 때 전역 분할 맵을 hello에 대 한 읽기 전용 권한이 있는 자격 증명을 사용 합니다. hello hello 전역 분할 맵은 이러한 자격 증명에서에서 검색 된 정보에 사용 되 [데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md) 및 toopopulate hello 분할 hello 클라이언트 캐시에 매핑합니다. hello 자격 증명이 제공 hello를 통해 동일한 호출 패턴 너무**GetSqlShardMapManager** 위와 같이 합니다. 

    // Obtain shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmReadOnlyConnectionString, 
            ShardMapManagerLoadPolicy.Lazy
    );  

Hello hello 사용 **smmReadOnlyConnectionString** 대신 하 여이 액세스에 대 한 다른 자격 증명의 tooreflect hello 사용 **관리자가 아닌** 사용자: 쓰기 이러한 자격 증명을 제공 하지 않을 hello 전역 분할 맵 사용 권한입니다. 

## <a name="connection-credentials"></a>연결 자격 증명
Hello를 사용 하는 경우 추가 자격 증명이 필요 [ **OpenConnectionForKey** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) 메서드 tooaccess 분할 키와 관련 된 분할 합니다. 이러한 자격 증명 hello 분할 영역에 있는 읽기 전용 액세스 toohello 로컬 분할 맵 테이블에 대 한 tooprovide 권한이 필요 합니다. 이 hello 분할 영역에 데이터 종속 라우팅에 대 한 필요한 tooperform 연결 유효성 검사 합니다. 이 코드 조각은 데이터 종속 라우팅의 hello 컨텍스트에서 데이터 액세스를 허용 합니다. 

    using (SqlConnection conn = rangeMap.OpenConnectionForKey<int>( 
    targetWarehouse, smmUserConnectionString, ConnectionOptions.Validate)) 

이 예제에서는 **smmUserConnectionString** hello에 대 한 연결 문자열 hello 사용자 자격 증명을 보유 합니다. Azure SQL DB의 경우 사용자 자격 증명에 대한 일반적인 연결 문자열은 다음과 같습니다. 

    "User ID=<yourusername>; Password=<youruserpassword>; Trusted_Connection=False; Encrypt=True; Connection Timeout=30;”  

Hello 관리자 자격 증명에서와 마찬가지로 수행 하지에 값을 hello 형태의 "username@server"입니다. 대신 "username"만 사용합니다.  또한 참고가 hello 연결 문자열 서버 이름과 데이터베이스 이름을 포함 되지 않습니다. 때문 hello **OpenConnectionForKey** 호출 hello 연결 toohello 올바른 hello 키를 기반으로 분할 된 데이터베이스를 자동으로 연결 됩니다. 따라서 hello 데이터베이스 이름과 서버 이름이 제공 되지 않습니다. 

## <a name="see-also"></a>참고 항목
[Azure SQL 데이터베이스에서 데이터베이스 및 로그인 관리](sql-database-manage-logins.md)

[SQL 데이터베이스 보안 설정](sql-database-security-overview.md)

[탄력적 데이터베이스 작업 시작](sql-database-elastic-jobs-getting-started.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

