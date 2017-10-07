---
title: "확장 클라우드 데이터베이스 (수평 분할)에 걸쳐 aaaReport | Microsoft Docs"
description: "toouse는 데이터베이스 데이터베이스 쿼리를 교차 하는 방법"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: c81ef5e3-41e9-4fd2-8631-868f2e168147
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: mlandzic
ms.openlocfilehash: e34f398f8d408cffd91a70fc2cfbda73daec3550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a>확장된 클라우드 데이터베이스에서 보고(미리 보기)
[탄력적 쿼리](sql-database-elastic-query-overview.md)를 사용하여 단일 연결 지점의 여러 Azure SQL 데이터베이스에서 보고서를 만들 수 있습니다. (또한 다음 이라고 알려집니다 "분할") hello 데이터베이스를 가로로 분할 되어야 합니다.

기존 데이터베이스를 설정한 경우 참조 [tooscaled 아웃 데이터베이스를 데이터베이스 마이그레이션 기존](sql-database-elastic-convert-to-use-elastic-tools.md)합니다.

toounderstand hello SQL 개체 필요한 tooquery, 참조 [수평 분할 된 데이터베이스에 걸쳐 쿼리](sql-database-elastic-query-horizontal-partitioning.md)합니다.

## <a name="prerequisites"></a>필수 조건
다운로드 및 실행 hello [탄력적 데이터베이스 도구 샘플 시작](sql-database-elastic-scale-get-started.md)합니다.

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a>분할 맵 hello 샘플 응용 프로그램을 사용 하 여 관리자 만들기
여기에서는 만듭니다 분할 맵은 다음 데이터 삽입 hello 분할 된 데이터베이스를 여러 분할 영역 함께 관리자입니다. Tooalready 문제가 발생 하는 경우 분할 된 데이터를 사용 하 여 분할 된 데이터베이스 설치 개, 단계를 수행 하는 hello를 건너뛰고 toohello 다음 섹션을 이동할 수 있습니다.

1. 빌드 및 실행 hello **탄력적 데이터베이스 도구 시작** 샘플 응용 프로그램입니다. Hello 섹션에는 7 단계까지 hello 단계에 따라 [다운로드 하 고 hello 샘플 응용 프로그램을 실행](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app)합니다. 7 단계의 hello 끝 hello 명령 프롬프트에 다음을 확인할 수 있습니다.

    ![명령 프롬프트][1]
2. Hello 명령 창에서 "1"을 입력 한 키를 누릅니다 **Enter**합니다. Hello shard map manager 만들고 두 명의 분할 된 데이터베이스 toohello 서버에 추가 합니다. 그런 다음 "3"을 입력 하 고 키를 눌러 **Enter**; hello 작업을 4 번 반복 합니다. 이 명령은 분할된 데이터베이스에 샘플 데이터행을 삽입합니다.
3. hello [Azure 포털](https://portal.azure.com) 3 개의 새 데이터베이스 서버에 표시 됩니다.

   ![Visual Studio 확인][2]

   이 시점에서 데이터베이스 간 쿼리는 hello 탄력적 데이터베이스 클라이언트 라이브러리를 통해 지원 됩니다. 예를 들어 hello 명령 창에서 옵션 4를 사용 합니다. hello 다중 분할 된 데이터베이스 쿼리 결과 항상 한 **UNION ALL** 모든 분할 영역에서 hello 결과입니다.

   Hello 다음 섹션에서는 분할 영역 간에 hello 데이터의 다양 한 쿼리를 지 원하는 샘플 데이터베이스 끝점을 만듭니다.

## <a name="create-an-elastic-query-database"></a>탄력적 쿼리 데이터베이스 만들기
1. 열기 hello [Azure 포털](https://portal.azure.com) 로그인 하십시오.
2. Hello에 새 Azure SQL 데이터베이스 만들기 분할 설치와 동일한 서버입니다. "ElasticDBQuery" hello 데이터베이스의 이름을

    ![Azure 포털 및 가격 책정 계층][3]

    > [!NOTE]
    > 기존 데이터베이스를 사용할 수 있습니다. 경우 그렇게 할 수 있습니다이 아니어야 싶다는 의사를 tooexecute hello 분할 영역 중 하나에 대 한 쿼리 합니다. 이 데이터베이스는 hello 탄력적 데이터베이스 쿼리에 대 한 메타 데이터 개체를 만드는 데 사용 됩니다.
    >

## <a name="create-database-objects"></a>데이터베이스 개체 만들기
### <a name="database-scoped-master-key-and-credentials"></a>데이터베이스-범위 마스터 키 및 자격 증명
다음은 사용 되는 tooconnect toohello 분할 맵 관리자 및 hello 분할 된 데이터베이스입니다.

1. SQL Server Management Studio 또는 Visual Studio의 SQL Server Data Tools를 엽니다.
2. TooElasticDBQuery 데이터베이스를 연결 하 고 다음 T-SQL 명령을 hello를 실행 합니다.

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    "username" 및 "password" 해야 수 hello 동일의 6 단계에서 사용 되는 로그인 정보로 [다운로드 하 고 hello 샘플 응용 프로그램을 실행](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) 에 [탄력적 데이터베이스 도구 시작](sql-database-elastic-scale-get-started.md)합니다.

### <a name="external-data-sources"></a>외부 데이터 원본
외부 데이터 원본, toocreate hello hello ElasticDBQuery 데이터베이스에서 다음 명령을 실행 합니다.

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 "CustomerIDShardMap"를 만든 경우 hello 분할 맵 및 shard map manager hello 탄력적 데이터베이스 도구 샘플을 사용 하 여 hello 분할 맵 hello 이름을입니다. 그러나이 샘플에 대 한 사용자 지정 설치를 사용 하는 경우 다음 것 응용 프로그램에서 선택한 hello shard map 이름입니다.

### <a name="external-tables"></a>외부 테이블
Hello ElasticDBQuery 데이터베이스에서 다음 명령을 실행 하 여 hello 분할 영역에 hello Customers 테이블을 일치 하는 외부 테이블을 만듭니다.

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a>탄력적 데이터베이스 T-SQL쿼리 샘플 실행
외부 데이터 원본 및 외부 테이블을 정의한 후 외부 테이블을 통해 전체 T-SQL을 사용할 수 있습니다.

Hello ElasticDBQuery 데이터베이스에서이 쿼리를 실행 합니다.

    select count(CustomerId) from [dbo].[Customers]

Hello 쿼리 하는 모든 hello 분할 영역에서 결과 집계 하 고 hello 다음 출력을 제공 알 수 있습니다.

![출력 세부 정보][4]

## <a name="import-elastic-database-query-results-tooexcel"></a>탄력적 데이터베이스 쿼리 결과 tooExcel 가져오기
 쿼리 tooan Excel 파일의 hello 결과를 가져올 수 있습니다.

1. Excel 2013을 실행 합니다.
2. Toohello 이동 **데이터** 리본.
3. **기타 원본에서**을 클릭하고 **SQL Server에서**를 클릭합니다.

   ![다른 원본에서 Excel 가져오기][5]
4. Hello에 **데이터 연결 마법사** hello 서버 이름 및 로그인 자격 증명을 입력 합니다. 그런 후 **Next**를 클릭합니다.
5. Hello 대화 상자에서 **원하는 hello 데이터가 들어 있는 Select hello 데이터베이스**선택, hello **ElasticDBQuery** 데이터베이스입니다.
6. 선택 hello **고객** hello 목록 뷰에서 테이블 마우스 클릭 **다음**합니다. **마침**을 클릭합니다.
7. Hello에 **데이터 가져오기** 양식의 **표시할 방법을 선택 tooview이이 데이터 통합 문서에서**선택, **테이블** 클릭 **확인**합니다.

행을 hello 모든 **고객** 다른 분할 영역에 저장 된 테이블을 채우는 hello Excel 시트입니다.

이제 Excel의 강력한 데이터 시각화 함수를 사용할 수 있습니다. Tooconnect BI와 데이터 통합 도구 toohello 탄력적 쿼리 데이터베이스 자격 증명 및 hello 연결 문자열을 서버 이름으로, 데이터베이스 이름에 사용할 수 있습니다. SQL Server 도구에 대한 데이터 소스로 지원 되는지 확인 합니다. Toohello 쿼리 탄력적 데이터베이스 및 다른 SQL Server 데이터베이스와 마찬가지로 외부 테이블을 연결 하는 toowith 도구에는 SQL Server 테이블을 참조할 수 있습니다.

### <a name="cost"></a>비용
Hello 탄력적 데이터베이스 쿼리 기능을 사용 하기 위한 추가 비용 없이 있습니다.

가격 정보는 [SQL 데이터베이스 가격 정보](https://azure.microsoft.com/pricing/details/sql-database/)를 참조하세요.

## <a name="next-steps"></a>다음 단계

* 탄력적 쿼리의 개요는 [탄력적 쿼리 개요](sql-database-elastic-query-overview.md)를 참조하세요.
* 수직 분할 자습서는 [데이터베이스 간 쿼리 시작(수직 분할)](sql-database-elastic-query-getting-started-vertical.md)을 참조하세요.
* 수직 분할된 데이터에 대한 구문 및 예제 쿼리는 [수직 분할된 데이터 쿼리하기](sql-database-elastic-query-vertical-partitioning.md)를 참조하세요.
* 행 분할된 데이터에 대한 구문 및 예제 쿼리는 [행 분할된 데이터 쿼리하기](sql-database-elastic-query-horizontal-partitioning.md)를 참조하세요.
* 단일 원격 Azure SQL Database 또는 수평 분할 구성표의 분할을 제공하는 데이터베이스 집합에서 TRANSACT-SQL 문을 실행하는 저장된 프로시저는 [sp\_실행 \_원격](https://msdn.microsoft.com/library/mt703714)을 참조하세요.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
