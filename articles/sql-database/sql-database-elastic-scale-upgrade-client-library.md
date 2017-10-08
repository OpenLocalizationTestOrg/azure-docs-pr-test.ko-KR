---
title: "aaaUpgrade toohello 최신 탄력적 데이터베이스 클라이언트 라이브러리 | Microsoft Docs"
description: "Nuget을 사용하여 앱 및 라이브러리 업그레이드"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 0a546510-76e7-465e-9271-f15ff0cfa959
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: cc2c9179be4c53ca59cd24d832127cf277c6e695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-an-app-toouse-hello-latest-elastic-database-client-library"></a>app toouse hello 최신 탄력적 데이터베이스 클라이언트 라이브러리를 업그레이드 합니다.
새 버전의 hello [탄력적 데이터베이스 클라이언트 라이브러리](sql-database-elastic-database-client-library.md) Visual Studio에서 NuGetand hello NuGetPackage 관리자 인터페이스를 통해 사용할 수 있습니다. 업그레이드 버그 수정 포함 및 hello 클라이언트 라이브러리의 새로운 기능에 대 한 지원.

**Hello 최신 버전에 대 한:** 너무 이동[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)합니다.

Azure SQL 데이터베이스 toosupport 새로운 기능에 저장 된 기존 Shard Map Manager 메타 데이터를 변경할 뿐만 아니라 hello 새 라이브러리와 함께 응용 프로그램을 다시 빌드하십시오.

순서 대로 다음이 단계를 수행 하면 이전 버전의 hello 클라이언트 라이브러리 더 이상 사용자 환경에 있는 메타 데이터 개체를 업데이트할 때 즉, 업그레이드 한 후 이전 버전의 메타 데이터 개체를 만들 수 없습니다.   

## <a name="upgrade-steps"></a>업그레이드 단계
**1. 응용 프로그램을 업그레이드합니다.** Visual Studio, 다운로드 및 참조 hello 최신 클라이언트 라이브러리 버전 hello library;을 사용 하는 개발 프로젝트의 모든 열로 그런 다음 다시 작성 하 고 배포 합니다. 

* Visual Studio 솔루션에서 **도구** --> **NuGet 패키지 관리자** -->  **솔루션용 NuGet 패키지 관리**를 선택합니다. 
* (Visual Studio 2013) Hello 왼쪽된 패널에서 선택 **업데이트**를 선택한 후 hello **업데이트** hello 패키지에서 단추 **Azure SQL 데이터베이스 탄력적인 크기 조정 클라이언트 라이브러리** hello에 나타나는 창입니다.
* (Visual Studio 2015) 설정 hello 필터 상자 너무**사용 가능한 업그레이드**합니다. Hello 패키지 tooupdate를 선택 하 고 hello 클릭 **업데이트** 단추입니다.
* (Visual Studio 2017) Hello 대화의 hello 위쪽 선택 **업데이트**합니다. Hello 패키지 tooupdate를 선택 하 고 hello 클릭 **업데이트** 단추입니다.
* 빌드와 배포를 수행합니다. 

**2. 스크립트를 업그레이드합니다.** 사용 중인 경우 **PowerShell** toomanage 분할 스크립트 [hello 새 라이브러리 버전을 다운로드](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) 하 고 스크립트를 실행 하는 hello 디렉터리에 복사 합니다. 

**3. 분할/병합 서비스를 업그레이드합니다.** Hello 탄력적 데이터베이스 분할 / 병합 도구 tooreorganize 분할 된 데이터를 사용 하는 경우 [다운로드 하 여 hello 최신 버전의 hello 도구 배포](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/)합니다. 서비스를 찾을 수 hello에 대 한 업그레이드 단계를 자세히 [여기](sql-database-elastic-scale-overview-split-and-merge.md)합니다. 

**4. 분할된 데이터베이스 맵 관리자 데이터베이스를 업그레이드합니다**. Azure SQL 데이터베이스에서 분할 맵은 지 원하는 hello 메타 데이터를 업그레이드 합니다.  이 작업은 두 가지 방법, 즉 PowerShell이나 C#을 사용하여 수행할 수 있습니다. 아래에는 두 옵션이 모두 나와 있습니다.

***옵션 1: PowerShell을 사용하여 메타데이터 업그레이드***

1. NuGet에 대 한 최신 명령줄 유틸리티 hello 다운로드 [여기](http://nuget.org/nuget.exe) tooa 폴더를 저장 합니다. 
2. 명령 프롬프트를 열고, toohello 탐색 문제 hello 명령과 동일한 폴더:`nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`
3. Hello 새 클라이언트 DLL 버전 방금 다운로드 한, 예를 들어 있는 toohello 하위 폴더를 이동 합니다.`cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`
4. Hello 탄력적 데이터베이스 클라이언트 업그레이드 스크립틀릿 hello에서 다운로드 [스크립트 센터](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9), 및 DLL 같은 포함 된 폴더로 hello hello로 저장 합니다.
5. 해당 폴더의 hello 명령 프롬프트에서 "PowerShell.\upgrade.ps1"를 실행 하 고 hello 프롬프트를 따릅니다.

***옵션 2: C#을 사용하여 메타데이터 업그레이드***

또는 사용자 ShardMapManager 열리고 모든 분할 영역에 대해 반복 hello 메서드를 호출 하 여 hello 메타 데이터 업그레이드를 수행 하는 Visual Studio 응용 프로그램을 만들 [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) 및 [ UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) 다음이 예제와 같이: 

    ShardMapManager smm =
       ShardMapManagerFactory.GetSqlShardMapManager
       (connStr, ShardMapManagerLoadPolicy.Lazy); 
    smm.UpgradeGlobalStore(); 

    foreach (ShardLocation loc in
     smm.GetDistinctShardLocations()) 
    {   
       smm.UpgradeLocalStore(loc); 
    } 

이러한 메타데이터 업그레이드 기술은 여러 번 적용해도 안전합니다. 예를 들어 경우 이전 클라이언트 버전이 이미 업데이트 한 후 분할 영역을 실수로 만듭니다를 실행할 수 있습니다 업그레이드 다시 모든 분할 영역 tooensure에서 해당 hello 최신 메타 데이터 버전이 인프라 전반에 걸쳐 있는지 합니다. 

**참고:** hello 클라이언트 라이브러리의 새 버전이 공개 날짜까지 toowork 이전 버전의 Azure SQL DB, 그 반대로 줄에 hello Shard Map Manager 메타 데이터를 계속 합니다.   그러나 hello hello 최신 클라이언트 메타 데이터의에서 새로운 기능 중 일부의 tootake 장점은 toobe 업그레이드 해야 합니다.   Note 모든 사용자 데이터 또는 응용 프로그램 관련 데이터를 생성 하 고 hello Shard Map Manager에서 사용 하는 유일한 개체 메타 데이터 업그레이드에 영향을 주지 않습니다.  및 응용 프로그램은 위에서 설명한 hello 업그레이드 순서를 통해 toooperate 계속 합니다. 

## <a name="elastic-database-client-version-history"></a>탄력적 데이터베이스 클라이언트 버전 기록
버전 기록에 대 한 이동 너무[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]:./media/sql-database-elastic-scale-upgrade-client-library/nuget-upgrade.png

