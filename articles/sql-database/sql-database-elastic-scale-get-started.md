---
title: "탄력적 데이터베이스 도구 aaaGet 시작 | Microsoft Docs"
description: "기본적인 실행 방식 샘플 앱을 포함 하 여 Azure SQL 데이터베이스의 hello 탄력적 데이터베이스 도구 기능은 설명 합니다."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: CarlRabeler
ms.assetid: b6911f8d-2bae-4d04-9fa8-f79a3db7129d
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: a84e05c39dffbaef440538602f898acee6e0483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-elastic-database-tools"></a>탄력적 데이터베이스 도구 시작하기
이 문서에서는 toorun hello 샘플 응용 프로그램 수 있도록 하 여 toohello 개발자 환경을 소개 합니다. hello 예제는 간단한 분할 응용 프로그램을 만듭니다 하 고 탄력적 데이터베이스 도구의 주요 기능을 탐색 합니다. hello 샘플의 hello 함수를 보여 줍니다. [탄력적 데이터베이스 클라이언트 라이브러리](sql-database-elastic-database-client-library.md)합니다.

tooinstall hello 라이브러리 너무 이동[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)합니다. hello 라이브러리 hello 다음 섹션에에서 설명 된 hello 샘플 응용 프로그램으로 설치 됩니다.

## <a name="prerequisites"></a>필수 조건
* C#이 있는 Visual Studio 2012 이상. [Visual Studio 다운로드](http://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)에서 무료 버전을 다운로드하세요.
* NuGet 2.7 이상. tooget hello 최신 버전 참조 [NuGet 설치](http://docs.nuget.org/docs/start-here/installing-nuget)합니다.

## <a name="download-and-run-hello-sample-app"></a>다운로드 하 고 hello 샘플 응용 프로그램 실행
hello **시작-Azure sql 탄력적 DB 도구** 샘플 응용 프로그램 탄력적 데이터베이스 도구를 사용 하는 분할 응용 프로그램에 대 한 hello 개발 환경의 hello 가장 중요 한 측면을 보여 줍니다. [분할 맵 관리](sql-database-elastic-scale-shard-map-management.md), [데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md) 및 [다중 분할 쿼리](sql-database-elastic-scale-multishard-querying.md)의 주요 사용 사례를 중점적으로 소개합니다. toodownload 및 실행된 hello 샘플에는 다음이 단계를 따르십시오. 

1. Hello 다운로드 [Getting Started 샘플-Azure sql 탄력적 DB 도구](https://code.msdn.microsoft.com/windowsapps/Elastic-Scale-with-Azure-a80d8dc6) MSDN에서. 사용자가 선택한 hello 샘플 tooa 위치를 압축을 풉니다.

2. toocreate 프로젝트를 열고 hello **ElasticScaleStarterKit.sln** hello에서 솔루션 **C#** 디렉터리입니다.

3. Hello 샘플 프로젝트에 대 한 hello 솔루션을 열고 hello **app.config** 파일입니다. 그런 다음 Azure SQL 데이터베이스 서버 이름 및 사용자 로그인 정보 (사용자 이름 및 암호) hello 파일 tooadd의 hello 지침을 따릅니다.

4. 빌드하고 hello 응용 프로그램을 실행 합니다. 메시지가 표시 되 면 hello 솔루션의 Visual Studio toorestore hello NuGet 패키지를 사용 하도록 설정 합니다. 이 NuGet에서 hello hello 탄력적 데이터베이스 클라이언트 라이브러리의 최신 버전을 다운로드합니다.

5. Hello 클라이언트 라이브러리 기능에 대 한 다양 한 옵션 toolearn hello 사용해 보십시오. 참고 hello 단계 hello 콘솔 출력에서 응용 프로그램에서는 hello 및 hello 백그라운드 무료 tooexplore hello 코드 생각 합니다.
   
    ![진행][4]

축하합니다. 이제 SQL Database에서 Elastic Database 도구를 사용하는 첫 번째 분할 응용 프로그램을 빌드하고 실행했습니다. Visual Studio 또는 SQL Server Management Studio tooconnect tooyour SQL 데이터베이스를 사용 하 고 빠르게 생성 하는 샘플 hello hello 분할 확인을 수행 합니다. 새 샘플 분할 데이터베이스 및 shard map manager 데이터베이스 알게 될 hello 예제를 만들었습니다.

> [!IMPORTANT]
> 업데이트 tooAzure 및 SQL 데이터베이스와 계속 동기화 되도록에 항상 hello Management Studio의 최신 버전을 사용 하는 것이 좋습니다. [SQL Server Management Studio를 업데이트합니다](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

### <a name="key-pieces-of-hello-code-sample"></a>Hello 코드 샘플의 핵심 부분
* **분할 된 데이터베이스 및 분할 관리 매핑합니다**: hello 코드를 보여 줍니다 방법을 분할 된 데이터베이스, 범위, hello 파일의 매핑와 toowork **ShardManagementUtils.cs**합니다. 자세한 내용은 참조 [hello shard map manager와 함께 데이터베이스 확장](http://go.microsoft.com/?linkid=9862595)합니다.  

* **데이터 종속 라우팅**:에 표시 되어 트랜잭션 toohello 오른쪽 분할의 라우팅을 **DataDependentRoutingSample.cs**합니다. 자세한 내용은 [데이터 종속 라우팅](http://go.microsoft.com/?linkid=9862596)을 참조하세요. 

* **여러 분할 된 데이터베이스에서의 쿼리**: hello 파일에 설명 되어 분할 된 데이터베이스 간 쿼리 **MultiShardQuerySample.cs**합니다. 자세한 내용은 [다중 분할 쿼리](http://go.microsoft.com/?linkid=9862597)를 참조하세요.

* **빈 분할 영역이 추가**: hello 새로운 빈 분할의 추가 반복적인 hello 파일의 hello 코드에 의해 수행 됩니다 **CreateShardSample.cs**합니다. 자세한 내용은 참조 [hello shard map manager와 함께 데이터베이스 확장](http://go.microsoft.com/?linkid=9862595)합니다.

### <a name="other-elastic-scale-operations"></a>기타 탄력적인 확장 작업
* **기존 분할 분할**: hello 기능 toosplit 분할 된 데이터베이스는 hello에서 제공 **분할 / 병합 도구**합니다. 자세한 내용은 [확장된 클라우드 데이터베이스 간 데이터 이동](sql-database-elastic-scale-overview-split-and-merge.md)을 참조하세요.

* **기존 분할 영역을 병합**: hello를 사용 하 여 분할 병합도 이루어집니다 **분할 / 병합 도구**합니다. 자세한 내용은 [확장된 클라우드 데이터베이스 간 데이터 이동](sql-database-elastic-scale-overview-split-and-merge.md)을 참조하세요.   

## <a name="cost"></a>비용
hello 탄력적 데이터베이스 도구는 무료입니다. 탄력적 데이터베이스 도구를 사용 하는 경우에 Azure 사용 현황을 hello 비용 맨 위에 추가 요금이 모든 수신 하지 않습니다. 

예를 들어 hello 샘플 응용 프로그램은 새 데이터베이스를 만듭니다. 이 대 한 hello 비용 hello SQL 데이터베이스 버전을 선택 하면 hello 응용 프로그램의 Azure 사용량에 따라 다릅니다.

가격 책정 정보는 [SQL Database 가격 책정 정보](https://azure.microsoft.com/pricing/details/sql-database/)를 참조하세요.

## <a name="next-steps"></a>다음 단계
탄력적 데이터베이스 도구에 대 한 자세한 내용은 다음 페이지 hello 참조:

* 코드 샘플: 
  * [Azure SQL용 Elastic DB 도구 - 시작](http://code.msdn.microsoft.com/Elastic-Scale-with-Azure-a80d8dc6?SRC=VSIDE)
  * [Azure SQL용 Elastic DB 도구 - Entity Framework 통합](http://code.msdn.microsoft.com/Elastic-Scale-with-Azure-bae904ba?SRC=VSIDE)
  * [스크립트 센터의 분할된 데이터베이스 탄력성](https://gallery.technet.microsoft.com/scriptcenter/Elastic-Scale-Shard-c9530cbe)
* 블로그: [탄력적인 확장 발표](https://azure.microsoft.com/blog/2014/10/02/introducing-elastic-scale-preview-for-azure-sql-database/)
* Microsoft Virtual Academy: [hello 탄력적 데이터베이스 클라이언트 라이브러리 비디오로 확장을 사용 하 여 분할 구현](https://mva.microsoft.com/training-courses/elastic-database-capabilities-with-azure-sql-db-16554?l=lWyQhF1fC_6306218965) 
* 채널 9: [탄력적인 확장 개요 비디오](http://channel9.msdn.com/Shows/Data-Exposed/Azure-SQL-Database-Elastic-Scale)
* 토론 포럼: [Azure SQL Database 포럼](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)
* toomeasure 성능: [shard map manager에 대 한 성능 카운터](sql-database-elastic-database-client-library.md)

<!--Anchors-->
[hello Elastic Scale Sample Application]: #The-Elastic-Scale-Sample-Application
[Download and Run hello Sample App]: #Download-and-Run-the-Sample-App
[Cost]: #Cost
[Next steps]: #next-steps

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-get-started/newProject.png
[2]: ./media/sql-database-elastic-scale-get-started/click-online.png
[3]: ./media/sql-database-elastic-scale-get-started/click-CSharp.png
[4]: ./media/sql-database-elastic-scale-get-started/output2.png

