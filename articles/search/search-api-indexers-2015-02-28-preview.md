---
title: "인덱서 작업(Azure Search 서비스 REST API: 2015-02-28-Preview) | Microsoft Docs"
description: "인덱서 작업(Azure 검색 서비스 REST API: 2015-02-28-Preview)"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 42b5f85c-8304-4bc7-8e1e-a9c76b8ca25a
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: eugenesh
ms.openlocfilehash: 4dd9591072b44eeabae6eac1182b4eea10fd4a22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="indexer-operations-azure-search-service-rest-api-2015-02-28-preview"></a>인덱서 작업(Azure 검색 서비스 REST API: 2015-02-28-Preview)
> [!NOTE]
> 이 문서에서는 hello에는 인덱서 설명 [2015-02-28-미리 보기 REST API](search-api-2015-02-28-preview.md)합니다. 이 API 버전에는 문서 추출 기능이 있는 Azure Blob 저장소 인덱서와 Azure 테이블 저장소 인덱서의 미리 보기 버전 및 기타 향상된 기능이 추가되었습니다. 또한 API hello 인덱서를 포함 하 여 Azure SQL 데이터베이스, Azure Vm 및 Azure Cosmos DB에서 SQL Server에 대 한 일반 공급 (GA) 인덱서를 지원 합니다.
> 
> 

## <a name="overview"></a>개요
Azure 검색 데이터 통합할 수 몇 가지 일반적인 데이터 소스와 직접 hello 필요 toowrite 코드 tooindex를 제거 합니다. 이 대화 상자이 tooset, hello Azure 검색 API toocreate를 호출 하 고 관리할 수 **인덱서** 및 **데이터 소스**합니다. 

**인덱서** 는 데이터 원본을 대상 검색 인덱스에 연결하는 리소스입니다. 인덱서는 hello 같은 방법으로 다음에 사용 됩니다. 

* Hello 데이터 toopopulate 인덱스의 일회성 복사를 수행 합니다.
* 일정에 따라 hello 데이터 소스에 변경한 내용으로 인덱스를 동기화 합니다. hello 일정은 hello 인덱서 정의의 일부입니다.
* 요청 시 tooupdate 필요에 따라 인덱스를 호출 합니다. 

**인덱서** 정기적으로 업데이트 tooan 인덱스를 만들 때 유용 합니다. 인라인 일정을 인덱서 정의의 일부로 설정하거나 [인덱서 실행](#RunIndexer)을 사용하여 요청 시 실행할 수 있습니다. 

A **데이터 소스** toobe이 필요한 데이터를 지정 합니다. 자격 증명 tooaccess hello 데이터를 지정 및 정책 tooenable Azure 검색 tooefficiently hello 데이터 (예: 수정 되거나 삭제 된 데이터베이스 테이블의 행)의 변경 내용을 식별 합니다. 이는 독립된 리소스로 정의되므로 여러 인덱서에서 사용할 수 있습니다.

데이터 원본 hello는 현재 지원 됩니다.

* **Azure SQL Database** 및 **Azure VM의 SQL Server** 대상 연습은 [이 문서](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)를 참조하세요. 
* **Azure Cosmos DB**. 대상 연습은 [이 문서](search-howto-index-documentdb.md)를 참조하세요. 
* **Azure Blob 저장소**를 포함 하 여 hello 다음 문서 형식을: PDF, Microsoft Office (DOCX/DOC, XSLX/XLS, PPTX/PPT, MSG), HTML, XML, 우편 번호, 및 일반 텍스트 파일 (JSON 포함). 대상 연습은 [이 문서](search-howto-indexing-azure-blob-storage.md)를 참조하세요.
* **Azure Table Storage**. 대상 연습은 [이 문서](search-howto-indexing-azure-tables.md)를 참조하세요.

향후 hello에서 추가 데이터 원본에 대 한 지원을 추가 하려고 합니다. 이러한 의사 결정을 우선 순위를 지정 하는 데 toohelp hello에 사용자 의견을 제공 [Azure 검색 사용자 의견 포럼](http://feedback.azure.com/forums/263029-azure-search)합니다.

참조 [서비스 제한](search-limits-quotas-capacity.md) 최대 관련된 tooindexer 및 데이터 원본 리소스 제한에 대 한 합니다.

## <a name="typical-usage-flow"></a>일반적인 사용 흐름
지정된 `data source` 또는 `indexer` 리소스에 대한 간단한 HTTP 요청(POST, GET, PUT, DELETE)을 통해 인덱서 및 데이터 원본을 만들고 관리할 수 있습니다.

자동 인덱싱은 일반적으로 다음 4단계 프로세스를 통해 설정됩니다.

1. 인덱싱된 toobe 해야 하는 hello 데이터를 포함 하는 hello 데이터 소스를 식별 합니다. Azure 검색 데이터 원본에 hello 데이터 형식을 모두 지원 되지 않을 수 염두에서에 둬야 합니다. 참조 [지원 데이터 형식 간의](https://msdn.microsoft.com/library/azure/dn798938.aspx) hello 목록에 대 한 합니다.
2. 스키마가 데이터 원본과 호환되는 Azure 검색 인덱스를 만듭니다.
3. [데이터 원본 만들기](#CreateDataSource)에 설명된 대로 Azure 검색 데이터 원본을 만듭니다.
4. [인덱서 만들기](#CreateIndexer)에 설명된 대로 Azure 검색 인덱서를 만듭니다.

모든 대상 인덱스 및 데이터 소스 조합에 대해 하나의 인덱스를 생성하도록 계획해야 합니다. 동일한 hello에 쓰는 여러 인덱서를 포함할 수 있습니다 인덱스 및 있습니다 hello 다시 사용할 수 여러 인덱서에 동일한 데이터 원본. 그러나 인덱서는 한 번에 하나의 데이터 원본만 사용할 수 있으며 tooa 단일 인덱스에만 쓸 수 있습니다. 

인덱서를 만든 후 hello를 사용 하 여 해당 실행 상태를 검색할 수 있습니다 [인덱서 상태 가져오기](#GetIndexerStatus) 작업 합니다. 언제 든 지 인덱서를 실행할 수도 있습니다 (대신 또는 더하기 toorunning에서 일정에 따라 주기적으로 것) hello를 사용 하 여 [인덱서 실행](#RunIndexer) 작업 합니다.

<!-- MSDN has 2 art files plus a API topic link list -->


## <a name="create-data-source"></a>데이터 원본 만들기
Azure 검색에서는 데이터 원본은 대상 인덱스의 임시 또는 예약 된 데이터 새로 고침에 대 한 hello 연결 정보를 제공 하는 인덱서를 함께 사용 됩니다. HTTP POST 요청을 사용하여 Azure 검색 서비스 내에 새 데이터 원본을 만들 수 있습니다.

    POST https://[service name].search.windows.net/datasources?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

또는 PUT을 사용 하 여 하 고 hello URI에서 hello 데이터 원본 이름을 지정할 수 있습니다. 데이터 소스 hello가 없는 경우 생성 됩니다.

    PUT https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]

> [!NOTE]
> hello 허용 되는 데이터 원본의 최대 수는 가격 책정 계층에 따라 다릅니다. 무료 서비스 hello too3 데이터 소스를 수 있습니다. 표준 서비스에서는 50개까지 사용할 수 있습니다. 자세한 내용은 [서비스 제한](search-limits-quotas-capacity.md)을 참조하세요.
> 
> 

**요청**

모든 서비스 요청에는 HTTPS를 사용해야 합니다. hello **데이터 원본 만들기** POST 또는 PUT 메서드를 사용 하 여 요청을 생성할 수 있습니다. POST를 사용할 때는 hello 데이터 원본 정의와 함께 hello 요청 본문에서 데이터 원본 이름을 제공 해야 합니다. PUT을 사용 hello 이름은 hello URL의 일부입니다. 데이터 원본 hello가 존재 하지 않는 경우 자동으로 만들어집니다. 이미 있는 경우 업데이트 된 toohello 새 정의입니다. 

hello 데이터 원본 이름은 소문자 여야, 문자 또는 숫자로 시작, 없습니다 슬래시나 마침표를을 있어야 128 자 미만입니다. Hello 데이터 원본 이름은 문자 또는 숫자로 시작 된 후 hello 나머지 hello 이름 포함할 수 있습니다는 문자, 숫자 및 대시만 hello 대시를 연속 되지 않은 상태로. 자세한 내용은 [이름 지정 규칙](https://msdn.microsoft.com/library/azure/dn857353.aspx)을 참조하세요.

hello `api-version` 가 필요 합니다. hello 현재 버전은 `2015-02-28`합니다.

**요청 헤더**

다음 목록 hello 필요한 hello와 선택적 요청 헤더를 설명 합니다. 

* `Content-Type`: 필수 사항입니다. 너무 설정 합니다.`application/json`
* `api-key`: 필수 사항입니다. hello `api-key` 가 사용 되는 tooauthenticate hello 요청 tooyour 검색 서비스입니다. 문자열 값, 고유 tooyour 서비스 이며 hello **데이터 원본 만들기** 요청에 포함 해야 합니다는 `api-key` 헤더 (것과 반대로 tooa 쿼리 키)로 tooyour 관리자 키를 설정 합니다. 

Hello 서비스 이름 tooconstruct hello 요청 URL을 해야 합니다. 두 hello 서비스 이름을 가져올 수 있습니다 및 `api-key` hello에 대 한 서비스 대시보드에서 [Azure 포털](https://portal.azure.com/)합니다. 참조 [hello 포털에서 검색 서비스 만들기](search-create-service-portal.md) 페이지 탐색 도움말에 대 한 합니다.

<a name="CreateDataSourceRequestSyntax"></a>
**요청 본문 구문**

hello hello 요청 본문에 선택적 데이터 변경 검색 뿐만 아니라 hello 데이터 원본, 자격 증명 tooread hello 데이터의 형식을 포함 하는 데이터 원본 정의 포함 되어 있으며 데이터 삭제 검색 정책을 사용 하는 tooefficiently 식별 변경했습니다 또는 삭제 된 hello 데이터 원본의 데이터를 정기적으로 예약 된 인덱서를 함께 사용 하면 됩니다. 

hello hello 요청 페이로드 구조를 지정 하는 것에 대 한 구문은 다음과 같습니다. 이 항목에서 샘플 요청이 추가로 제공됩니다.

    { 
        "name" : "Required for POST, optional for PUT. hello name of hello data source",
        "description" : "Optional. Anything you want, or nothing at all",
        "type" : "Required. Must be one of 'azuresql', 'documentdb', 'azureblob', or 'azuretable'",
        "credentials" : { "connectionString" : "Required. Connection string for your data source" },
        "container" : { "name" : "Required. hello name of hello table, collection, or blob container you wish tooindex" },
        "dataChangeDetectionPolicy" : { Optional. See below for details }, 
        "dataDeletionDetectionPolicy" : { Optional. See below for details }
    }

요청에는 다음과 같은 속성 hello 포함 됩니다. 

* `name`: 필수 사항입니다. hello hello 데이터 원본의 이름입니다. 데이터 원본 이름 해야만 소문자, 숫자 또는 대시만 포함, 시작 되거나 끝나서와 대시 및 제한 too128 자입니다.
* `description`: 선택적 설명입니다. 
* `type`: 필수 사항입니다. 지원 되는 hello 데이터 원본 유형 중 하나 여야 합니다.
  * `azuresql` - Azure SQL 데이터베이스 또는 Azure VM의 SQL Server
  * `documentdb` - Azure Cosmos DB
  * `azureblob` - Azure Blob Storage
  * `azuretable` - Azure Table Storage
* `credentials`:
  * 필요한 hello `connectionString` 속성 hello 데이터 원본에 대 한 hello 연결 문자열을 지정 합니다. hello 연결 문자열의 형식은 hello hello 데이터 원본 유형에 따라 달라 집니다. 
    * Azure SQL hello 일반적인 SQL Server 연결 문자열입니다. Hello Azure 포털 tooretrieve hello 연결 문자열을 사용 하는 경우 사용 하 여 hello `ADO.NET connection string` 옵션입니다.
    * Azure Cosmos DB에 대 한 hello 연결 문자열 형식에 따라 hello에 있어야: `"AccountEndpoint=https://[your account name].documents.azure.com;AccountKey=[your account key];Database=[your database id]"`합니다. 모든 hello 값은 필수입니다. Hello에서 찾을 수 있습니다 [Azure 포털](https://portal.azure.com/)합니다.  
    * Azure Blob 및 테이블 저장소에 대 한 hello 저장소 계정 연결 문자열입니다. hello 형식이 설명 되어 [여기](https://azure.microsoft.com/documentation/articles/storage-configure-connection-string/)합니다. HTTPS 끝점 프로토콜이 필요합니다.  
* `container`필수: hello를 사용 하 여 hello 데이터 tooindex 지정 `name` 및 `query` 속성: 
  * `name`, 필수:
    * Azure SQL: hello 테이블 또는 뷰를 지정합니다. `[dbo].[mytable]`과 같은 스키마로 한정된 이름을 사용할 수 있습니다.
    * DocumentDB: hello 컬렉션을 지정합니다. 
    * Azure Blob 저장소: hello 저장소 컨테이너를 지정합니다.
    * Azure 테이블 저장소: hello hello 테이블 이름을 지정합니다. 
  * `query`, 선택 사항:
    * DocumentDB: toospecify를 Azure 검색에서 인덱싱할 수 있는 플랫 스키마로 임의 JSON 문서 레이아웃을 평면화 하는 쿼리 수 있습니다.  
    * Azure Blob 저장소: toospecify를 hello blob 컨테이너 내에 있는 가상 폴더 있습니다. Blob 경로 대 한 예를 들어 `mycontainer/documents/blob.pdf`, `documents` hello 가상 폴더도 사용할 수 있습니다.
    * Azure 테이블 저장소: toospecify를 필터 집합을 가져온 행 toobe hello는 쿼리 있습니다.
    * Azure SQL: 쿼리는 지원되지 않습니다. 이 기능이 필요하면 [이 제안](https://feedback.azure.com/forums/263029-azure-search/suggestions/9893490-support-user-provided-query-in-sql-indexer)
* 선택적 hello `dataChangeDetectionPolicy` 및 `dataDeletionDetectionPolicy` 속성은 다음과 같습니다.

<a name="DataChangeDetectionPolicies"></a>
**데이터 변경 검색 정책**

hello 용도 데이터 변경 검색 정책을 tooefficiently 변경 된 데이터 항목을 식별 합니다. 지원 되는 정책은 hello 데이터 소스 형식에 따라 다릅니다. 아래 섹션에서 각 정책에 대해 설명합니다. 

***상위 워터마크 변경 검색 정책*** 

이 정책을 사용 하 여 데이터 원본 열 또는 hello 다음 조건을 충족 하는 속성을 포함 하는 경우:

* 모든 삽입 hello 열에 대 한 값을 지정 합니다. 
* 모든 업데이트 tooan 항목은 또한 hello 열의 hello 값을 변경 합니다. 
* hello 값이 열의 각 변경에 따라 카운터가 증가 합니다.
* 필터 절 비슷한 toohello 다음을 사용 하는 쿼리 `WHERE [High Water Mark Column] > [Current High Water Mark Value]` 효율적으로 실행할 수 있습니다.

예를 들어, Azure SQL 데이터 원본에는 인덱스를 사용 하는 경우 `rowversion` 열이 hello 이상적인 후보로 hello 상위 워터 마크 정책으로 사용 합니다. 

이 정책은 다음과 같이 지정할 수 있습니다.

    { 
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "[a row version or last_updated column name]" 
    } 

Hello를 사용 해야 Azure Cosmos DB 데이터 소스를 사용할 경우 `_ts` Azure Cosmos DB에서 제공 하는 속성입니다. 

사용 하 여 상위 워터 마크 변경 검색 정책을 기반으로 blob의 마지막 수정 타임 스탬프; Azure Blob 데이터 원본, Azure 검색을 자동으로 사용 하는 경우 이러한 정책을 toospecify는 직접 필요 하지 않습니다.   

***SQL 통합 변경 검색 정책***

SQL 데이터베이스에서 [변경 내용 추적](https://msdn.microsoft.com/library/bb933875.aspx)을 지원하는 경우 SQL 통합 변경 내용 추적 정책을 사용하는 것이 좋습니다. 이 정책은 hello 가장 효과적인 변경 내용 추적, 있으며 스키마에 있는 명시적 "소프트 삭제" 열 toohave 필요 없이 Azure 검색 tooidentify 삭제 된 행을 있습니다.

통합된 변경 내용 추적 hello 다음 SQL Server 데이터베이스 버전부터 사용할 수 있습니다. 

* Azure VM SQL Server를 사용하는 경우 SQL Server 2008 R2.
* Azure SQL 데이터베이스 V12(Azure SQL 데이터베이스를 사용하는 경우)  

SQL 통합 변경 내용 추적 정책을 사용할 때는 별도의 데이터 삭제 검색 정책을 지정하지 마세요. 이 정책은 삭제된 행 식별을 기본적으로 지원합니다. 

이 정책은 테이블에만 사용할 수 있으며 보기에는 사용할 수 없습니다. 이 정책을 사용 하려면 먼저 사용 중인 hello 테이블에 대 한 추적 tooenable 변경을 해야 합니다. 지침은 [변경 내용 추적 설정 및 해제](https://msdn.microsoft.com/library/bb964713.aspx) 를 참조하세요.    

Hello를 구성할 때는 **데이터 원본 만들기** 요청, SQL 통합된 변경 내용 추적 정책을 다음과 같이 지정할 수 있습니다.

    { 
        "@odata.type" : "#Microsoft.Azure.Search.SqlIntegratedChangeTrackingPolicy" 
    }

<a name="DataDeletionDetectionPolicies"></a>
**데이터 삭제 검색 정책**

데이터 삭제 검색 정책의 hello 목적은 tooefficiently 삭제 된 데이터 항목을 식별 합니다. 현재만 지원 hello 정책은 hello `Soft Delete` 삭제 된 hello 값에 따라 항목을 식별할 수 있는 정책은 `soft delete` 열 이나 hello 데이터 원본의 속성입니다. 이 정책은 다음과 같이 지정할 수 있습니다.

    { 
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "hello column that specifies whether a row was deleted", 
        "softDeleteMarkerValue" : "hello value that identifies a row as deleted" 
    }

> [!NOTE]
> 문자열, 정수 또는 부울 값이 있는 열만 지원됩니다. 값으로 사용 되는 hello `softDeleteMarkerValue` hello 해당 열에 정수나 부울 보유 하는 경우에는 문자열 이어야 합니다. 예를 들어 데이터 소스에 표시 된 hello 값이 1 이면 사용 `"1"` hello로 `softDeleteMarkerValue`합니다.    
> 
> 

<a name="CreateDataSourceRequestExamples"></a>
**요청 본문 예제**

일정에 따라 실행 되는 인덱서에서 toouse hello 데이터 원본으로 지정 하려는 경우 보여 주는이 예제 toospecify 변경 하는 방법 및 삭제 검색 정책: 

    { 
        "name" : "asqldatasource",
        "description" : "a description",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" },
        "dataChangeDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy", "highWaterMarkColumnName" : "RowVersion" }, 
        "dataDeletionDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy", "softDeleteColumnName" : "IsDeleted", "softDeleteMarkerValue" : "true" }
    }

Hello 데이터의 일회성 복사본에 대 한 toouse hello 데이터 원본만 가져오려는 경우 hello 정책 생략할 수 있습니다.

    { 
        "name" : "asqldatasource",
        "description" : "anything you want, or nothing at all",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" }
    } 

**응답**

요청이 성공적으로 실행되면 '201 생성됨'이 반환됩니다. 

<a name="UpdateDataSource"></a>

## <a name="update-data-source"></a>데이터 원본 업데이트
HTTP PUT 요청을 사용하여 기존 데이터 원본을 업데이트할 수 있습니다. Hello 요청 URI에 hello 데이터 소스 tooupdate의 hello 이름을 지정합니다.

    PUT https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

hello `api-version` 가 필요 합니다. hello 현재 버전은 `2015-02-28`합니다. [Azure Search API 버전](https://msdn.microsoft.com/library/azure/dn864560.aspx)에는 대체 버전에 대한 세부 정보 및 추가 정보가 있습니다.

hello `api-key` (것과 반대로 tooa 쿼리 키)로 관리자 키 여야 합니다. Toohello 인증 섹션에서 참조 [검색 서비스 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn 키에 대 한 자세한 합니다. [Hello 포털에서 검색 서비스 만들기](search-create-service-portal.md) tooget hello 서비스 URL과 키 속성 hello 요청에서 사용 하는 방법을 설명 합니다.

**요청**

hello 요청 본문 구문은 hello와 같습니다 [데이터 원본 만들기 요청](#CreateDataSourceRequestSyntax)합니다.

기존 데이터 원본의 경우 일부 속성을 업데이트할 수 없습니다. 예를 들어 hello 유형의 기존 데이터 원본 변경할 수 없습니다.  

기존 데이터 원본에 대해 toochange hello 연결 문자열을 원하지 리터럴 hello를 지정할 수 있습니다 `<unchanged>` hello 연결 문자열에 대 한 합니다. 데이터 소스 tooupdate 필요 있고 보안에 중요 한 데이터 이므로 편리해 진 toohello 연결 문자열 없는 경우에 유용 합니다.

**응답**

요청이 성공적으로 실행되면 새 데이터 원본이 생성된 경우 ‘201 생성됨’이 반환되고 기존 데이터 원본이 업데이트된 경우 ‘204 콘텐츠 없음’이 반환됩니다.

<a name="ListDataSource"></a>

## <a name="list-data-sources"></a>데이터 원본 나열
hello **데이터 원본 목록** 작업 Azure 검색 서비스의 hello 데이터 원본의 목록을 반환 합니다. 

    GET https://[service name].search.windows.net/datasources?api-version=[api-version]
    api-key: [admin key]

hello `api-version` 가 필요 합니다. hello 현재 버전은 `2015-02-28`합니다. 

hello `api-key` (것과 반대로 tooa 쿼리 키)로 관리자 키 여야 합니다. Toohello 인증 섹션에서 참조 [검색 서비스 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn 키에 대 한 자세한 합니다. [Hello 포털에서 검색 서비스 만들기](search-create-service-portal.md) tooget hello 서비스 URL과 키 속성 hello 요청에서 사용 하는 방법을 설명 합니다.

**응답**

요청이 성공적으로 실행되면 '200 OK'가 반환됩니다.

아래에는 예제 응답 본문이 나와 있습니다.

    {
      "value" : [
        {
          "name": "datasource1",
          "type": "azuresql",
          ... other data source properties
        }]
    }

참고에 관심이 toojust hello 속성 아래로 hello 응답을 필터링 할 수 있습니다. 데이터 원본 이름 목록만 하려는 경우 OData hello를 사용 하는 예를 들어 `$select` 쿼리 옵션:

    GET /datasources?api-version=205-02-28&$select=name

이 경우 위 예제는 hello hello 응답은 다음과 같이 표시 됩니다. 

    {
      "value" : [ { "name": "datasource1" }, ... ]
    }

검색 서비스에 데이터 원본 많이 있는 경우 유용한 기술 toosave 대역폭입니다.

<a name="GetDataSource"></a>

## <a name="get-data-source"></a>데이터 원본 가져오기
hello **데이터 원본 가져오기** Azure 검색에서 hello 데이터 원본 정의 가져옵니다.

    GET https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    api-key: [admin key]

hello `api-version` 가 필요 합니다. hello 현재 버전은 `2015-02-28`합니다. 

hello `api-key` (것과 반대로 tooa 쿼리 키)로 관리자 키 여야 합니다. Toohello 인증 섹션에서 참조 [검색 서비스 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn 키에 대 한 자세한 합니다. [Hello 포털에서 검색 서비스 만들기](search-create-service-portal.md) tooget hello 서비스 URL과 키 속성 hello 요청에서 사용 하는 방법을 설명 합니다.

**응답**

상태 코드: 응답에 성공하면 ‘200 OK’가 반환됩니다.

hello 응답은에 비슷한 tooexamples [예제 요청은 데이터 원본 만들기](#CreateDataSourceRequestExamples): 

    { 
        "name" : "asqldatasource",
        "description" : "a description",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" },
        "dataChangeDetectionPolicy" : { 
            "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName" : "RowVersion" }, 
        "dataDeletionDetectionPolicy" : { 
            "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
            "softDeleteColumnName" : "IsDeleted", 
            "softDeleteMarkerValue" : "true" }
    }

> [!NOTE]
> Hello를 설정 하지 마십시오 `Accept` 요청 헤더에 너무`application/json;odata.metadata=none` 경우 그렇게이 API를 호출 하면 `@odata.type` hello 응답에서 생략 특성 toobe 간에 데이터 변경 및 데이터 삭제 검색 수 toodifferentiate 됩니다 서로 다른 형식의 정책입니다. 
> 
> 

<a name="DeleteDataSource"></a>

## <a name="delete-data-source"></a>데이터 원본 삭제
hello **데이터 원본 삭제** 작업 Azure 검색 서비스에서 데이터 원본을 제거 합니다.

    DELETE https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> 인덱서가 있어도 삭제 하는 hello 데이터 소스를 참조할 경우 hello 삭제 작업이 계속 진행 됩니다. 그러나 이러한 인덱서는 다음에 실행할 때 오류 상태로 전환됩니다.  
> 
> 

hello `api-version` 가 필요 합니다. hello 현재 버전은 `2015-02-28`합니다. 

hello `api-key` (것과 반대로 tooa 쿼리 키)로 관리자 키 여야 합니다. Toohello 인증 섹션에서 참조 [검색 서비스 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn 키에 대 한 자세한 합니다. [Hello 포털에서 검색 서비스 만들기](search-create-service-portal.md) tooget hello 서비스 URL과 키 속성 hello 요청에서 사용 하는 방법을 설명 합니다.

**응답**

상태 코드: 응답에 성공하면 ‘204 콘텐츠 없음’이 반환됩니다.

<a name="CreateIndexer"></a>

## <a name="create-indexer"></a>인덱서 만들기
HTTP POST 요청을 사용하여 Azure 검색 서비스 내에서 새 인덱서를 만들 수 있습니다.

    POST https://[service name].search.windows.net/indexers?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

또는 PUT을 사용 하 여 하 고 hello URI에서 hello 데이터 원본 이름을 지정할 수 있습니다. 데이터 소스 hello가 없는 경우 생성 됩니다.

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]

> [!NOTE]
> hello 최대 인덱서 허용 수는 가격 책정 계층에 따라 다릅니다. 무료 서비스 hello too3 인덱서를 수 있습니다. 표준 서비스에서는 50개까지 사용할 수 있습니다. 자세한 내용은 [서비스 제한](search-limits-quotas-capacity.md)을 참조하세요.
> 
> 

hello `api-version` 가 필요 합니다. hello 현재 버전은 `2015-02-28`합니다. 

hello `api-key` (것과 반대로 tooa 쿼리 키)로 관리자 키 여야 합니다. Toohello 인증 섹션에서 참조 [검색 서비스 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn 키에 대 한 자세한 합니다. [Hello 포털에서 검색 서비스 만들기](search-create-service-portal.md) tooget hello 서비스 URL과 키 속성 hello 요청에서 사용 하는 방법을 설명 합니다.

<a name="CreateIndexerRequestSyntax"></a>
**요청 본문 구문**

hello hello 요청 본문을 hello 데이터 소스와 hello 대상 인덱스 인덱스와 선택적 인덱싱 일정 및 매개 변수를 지정 하는 인덱서 정의 포함 합니다. 

hello hello 요청 페이로드 구조를 지정 하는 것에 대 한 구문은 다음과 같습니다. 이 항목에서 샘플 요청이 추가로 제공됩니다.

    { 
        "name" : "Required for POST, optional for PUT. hello name of hello indexer",
        "description" : "Optional. Anything you want, or null",
        "dataSourceName" : "Required. hello name of an existing data source",
        "targetIndexName" : "Required. hello name of an existing index",
        "schedule" : { Optional. See Indexing Schedule below. },
        "parameters" : { Optional. See Indexing Parameters below. },
        "fieldMappings" : { Optional. See Field Mappings below. },
        "disabled" : Optional boolean value indicating whether hello indexer is disabled. False by default.  
    }

**인덱서 일정**

인덱서는 선택적으로 일정을 지정할 수 있습니다. 일정에 따라가 있는 경우 hello 인덱서 일정에 따라 주기적으로 실행 됩니다. 일정 hello 특성 뒤에 있습니다.

* `interval`: 필수 사항입니다. 인덱서 실행 간격 또는 기간을 지정하는 기간 값입니다. hello 최소 간격은 5 분이 허용 가장 긴 hello은 1 일입니다. 형식은 XSD "dayTimeDuration" 값( [ISO 8601 기간](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) 값의 제한된 하위 집합)이어야 합니다. 이 대 한 hello 패턴은: `"P[nD][T[nH][nM]]"`합니다. 예를 들어 15분 간격이면 `PT15M`, 2시간 간격이면 `PT2H`입니다. 
* `startTime`: 필수 사항입니다. UTC 날짜/시간 hello 인덱서 실행을 시작 해야 합니다. 

**인덱서 매개 변수**

인덱서는 필요에 따라 동작에 영향을 주는 여러 매개 변수를 지정할 수 있습니다. 모든 hello 매개 변수는 선택적입니다.  

* `maxFailedItems`: 인덱서 실행 오류가 간주 되기 전에 hello toobe 실패할 수 있는 항목 수 인덱스입니다. 기본값은 0입니다. 실패 한 항목에 대 한 내용은 hello 반환한 [인덱서 상태 가져오기](#GetIndexerStatus) 작업 합니다. 
* `maxFailedItemsPerBatch`: 인덱서 실행 오류가 간주 되기 전에 각 일괄 처리의 인덱싱된 toobe 실패할 수 있는 항목의 hello 수 있습니다. 기본값은 0입니다.
* `base64EncodeKeys`: 문서 키를 base-64로 인코딩할지 여부를 지정합니다. Azure 검색에서는 문서 키에 포함할 수 있는 문자에 제한이 적용됩니다. 그러나 원본 데이터의 hello 값에 유효 하지 않은 문자를 포함할 수 있습니다. 문서 키로 값 등 필요한 tooindex 인 경우이 플래그 tootrue는 설정할 수 있습니다. 기본값은 `false`입니다.
* `batchSize`: 단일 일괄 처리 순서 tooimprove 성능이 hello hello 데이터 소스에서 읽고 인덱싱된 항목 수를 지정 합니다. hello 기본 hello 데이터 소스 형식에 따라 달라 집니다: SQL Azure 및 Azure Cosmos DB에 대 한 1000 이며 Azure Blob 저장소에 10입니다.

**필드 매핑**

Hello 대상 인덱스의 hello 데이터 소스 tooa 다른 필드 이름을에서 필드 매핑을 toomap 필드 이름을 사용할 수 있습니다. `_id`필드가 있는 원본 테이블을 예로 들어보겠습니다. Azure 검색 hello 필드 이름을 바꿀 수 있으므로 밑줄로 시작 하는 필드 이름을 허용 하지 않습니다. 이렇게 hello를 사용 하 여 `fieldMappings` 다음과 같이 hello 인덱서 속성: 

    "fieldMappings" : [ { "sourceFieldName" : "_id", "targetFieldName" : "id" } ] 

여러 필드 매핑을 지정할 수 있습니다. 

    "fieldMappings" : [ 
        { "sourceFieldName" : "_id", "targetFieldName" : "id" },
        { "sourceFieldName" : "_timestamp", "targetFieldName" : "timestamp" },
     ]

원본 필드 이름과 대상 필드 이름 모두 대/소문자를 구분하지 않습니다.

<a name="FieldMappingFunctions"></a>
***필드 매핑 함수***

필드 매핑을 사용 하 여 사용 되는 tootransform 소스 필드 값을 수도 있습니다 *함수 매핑*합니다.

현재 `jsonArrayToStringCollection`함수만 지원됩니다. JSON 배열로 hello 대상 인덱스의 collection (edm.string) 필드에 서식이 지정 된 문자열을 포함 하는 필드를 구문 분석 합니다. SQL에는 네이티브 컬렉션 데이터 형식이 없기 때문에 이 함수는 특히 Azure SQL 인덱서와 함께 사용됩니다. 다음과 같이 사용할 수 있습니다. 

    "fieldMappings" : [ { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } } ] 

예를 들어 경우 hello 원본 필드 hello 문자열이 포함 `["red", "white", "blue"]`, 다음 형식의 hello 대상 필드 `Collection(Edm.String)` hello 3 값으로 채울 수 `"red"`, `"white"` 및 `"blue"`합니다.

해당 hello 참고 `targetFieldName` 속성은 선택 사항; 두면 hello `sourceFieldName` 값이 사용 됩니다. 

<a name="CreateIndexerRequestExamples"></a>
**요청 본문 예제**

hello 다음 예제에서는 hello에서 참조 하는 hello 테이블에서 데이터를 복사 하는 인덱서로 `ordersds` 데이터 원본 toohello `orders` UTC 2015 년 1 월 1 일에 시작 하 고 1 시간 마다 실행 하는 일정에는 인덱스입니다. 각 일괄 처리당 인덱싱하지 toobe 실패 하는 5 개 이하의 항목이 10 개 미만의 항목 총에서 인덱싱된 toobe를 실패 한 경우 각 인덱서 호출은 성공적으로 수행 됩니다. 

    {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" },
        "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 5, "base64EncodeKeys": false }
    }

**응답**

요청이 성공적으로 실행되면 '201 생성됨'이 반환됩니다.

<a name="UpdateIndexer"></a>

## <a name="update-indexer"></a>인덱서 업데이트
HTTP PUT 요청을 사용하여 기존 인덱서를 업데이트할 수 있습니다. Hello 요청 URI에 hello 인덱서 tooupdate의 hello 이름을 지정합니다.

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

hello `api-version` 가 필요 합니다. hello 현재 버전은 `2015-02-28`합니다. 

hello `api-key` (것과 반대로 tooa 쿼리 키)로 관리자 키 여야 합니다. Toohello 인증 섹션에서 참조 [검색 서비스 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn 키에 대 한 자세한 합니다. [Hello 포털에서 검색 서비스 만들기](search-create-service-portal.md) tooget hello 서비스 URL과 키 속성 hello 요청에서 사용 하는 방법을 설명 합니다.

**요청**

hello 요청 본문 구문은 hello와 같습니다 [인덱서 만들기 요청](#CreateIndexerRequestSyntax)합니다.

**응답**

요청이 성공적으로 실행되면 새 인덱서가 생성된 경우 ‘201 생성됨’이 반환되고 기존 인덱서가 업데이트된 경우 ‘204 콘텐츠 없음’이 반환됩니다.

<a name="ListIndexers"></a>

## <a name="list-indexers"></a>인덱서 나열
hello **인덱서 나열** 작업 Azure 검색 서비스의 인덱서 hello 목록을 반환 합니다. 

    GET https://[service name].search.windows.net/indexers?api-version=[api-version]
    api-key: [admin key]


hello `api-version` 가 필요 합니다. hello 미리 보기 버전을 `2015-02-28-Preview`합니다. [Azure 검색 버전 관리](https://msdn.microsoft.com/library/azure/dn864560.aspx) 에서는 대체 버전에 대한 세부 정보 및 추가 정보를 제공합니다.

hello `api-key` (것과 반대로 tooa 쿼리 키)로 관리자 키 여야 합니다. Toohello 인증 섹션에서 참조 [검색 서비스 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn 키에 대 한 자세한 합니다. [Hello 포털에서 검색 서비스 만들기](search-create-service-portal.md) tooget hello 서비스 URL과 키 속성 hello 요청에서 사용 하는 방법을 설명 합니다.

**응답**

요청이 성공적으로 실행되면 '200 OK'가 반환됩니다.

아래에는 예제 응답 본문이 나와 있습니다.

    {
      "value" : [
      {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        ... other indexer properties
      }]
    }

참고에 관심이 toojust hello 속성 아래로 hello 응답을 필터링 할 수 있습니다. 예를 들어 인덱서 이름 목록만 원할 경우 사용 hello OData `$select` 쿼리 옵션:

    GET /indexers?api-version=2014-10-20-Preview&$select=name

이 경우 위 예제는 hello hello 응답은 다음과 같이 표시 됩니다. 

    {
      "value" : [ { "name": "myindexer" } ]
    }

검색 서비스에 인덱서 많이 있는 경우 유용한 기술 toosave 대역폭입니다.

<a name="GetIndexer"></a>

## <a name="get-indexer"></a>인덱서 가져오기
hello **Get Indexer** Azure 검색에서 인덱서 정의 hello를 가져옵니다.

    GET https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    api-key: [admin key]

hello `api-version` 가 필요 합니다. hello 미리 보기 버전을 `2015-02-28-Preview`합니다. 

hello `api-key` (것과 반대로 tooa 쿼리 키)로 관리자 키 여야 합니다. Toohello 인증 섹션에서 참조 [검색 서비스 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn 키에 대 한 자세한 합니다. [Hello 포털에서 검색 서비스 만들기](search-create-service-portal.md) tooget hello 서비스 URL과 키 속성 hello 요청에서 사용 하는 방법을 설명 합니다.

**응답**

상태 코드: 응답에 성공하면 ‘200 OK’가 반환됩니다.

hello 응답은에 비슷한 tooexamples [인덱서 만들기 예제 요청은](#CreateIndexerRequestExamples): 

    {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" },
        "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 5, "base64EncodeKeys": false }
    }


<a name="DeleteIndexer"></a>

## <a name="delete-indexer"></a>인덱서 삭제
hello **인덱서 삭제** 작업 Azure 검색 서비스에서 인덱서를 제거 합니다.

    DELETE https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    api-key: [admin key]

인덱서를 삭제 하면 해당 시점에 진행 중인 인덱서 실행 hello toocompletion, 실행 되지만 추가 없습니다 실행이 예약 됩니다. 시도 toouse 없는 인덱서 하면 HTTP 상태 코드 404 찾을 수 없습니다. 

hello `api-version` 가 필요 합니다. hello 미리 보기 버전을 `2015-02-28-Preview`합니다. 

hello `api-key` (것과 반대로 tooa 쿼리 키)로 관리자 키 여야 합니다. Toohello 인증 섹션에서 참조 [검색 서비스 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn 키에 대 한 자세한 합니다. [Hello 포털에서 검색 서비스 만들기](search-create-service-portal.md) tooget hello 서비스 URL과 키 속성 hello 요청에서 사용 하는 방법을 설명 합니다.

**응답**

상태 코드: 응답에 성공하면 ‘204 콘텐츠 없음’이 반환됩니다.

<a name="RunIndexer"></a>

## <a name="run-indexer"></a>인덱서 실행
일정에 따라 주기적으로 더하기 toorunning, hello 통해 필요에 따라 인덱서 호출할 수도 있습니다 **인덱서 실행** 작업: 

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=[api-version]
    api-key: [admin key]

hello `api-version` 가 필요 합니다. hello 미리 보기 버전을 `2015-02-28-Preview`합니다. 

hello `api-key` (것과 반대로 tooa 쿼리 키)로 관리자 키 여야 합니다. Toohello 인증 섹션에서 참조 [검색 서비스 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn 키에 대 한 자세한 합니다. [Hello 포털에서 검색 서비스 만들기](search-create-service-portal.md) tooget hello 서비스 URL과 키 속성 hello 요청에서 사용 하는 방법을 설명 합니다.

**응답**

상태 코드: 응답에 성공하면 ‘202 수락됨'이 반환됩니다.

<a name="GetIndexerStatus"></a>

## <a name="get-indexer-status"></a>인덱서 상태 가져오기
hello **인덱서 상태 가져오기** hello 현재 상태와 실행 기록을 인덱서를 검색 하는 작업: 

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=[api-version]
    api-key: [admin key]


hello `api-version` 가 필요 합니다. hello 미리 보기 버전을 `2015-02-28-Preview`합니다. 

hello `api-key` (것과 반대로 tooa 쿼리 키)로 관리자 키 여야 합니다. Toohello 인증 섹션에서 참조 [검색 서비스 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn 키에 대 한 자세한 합니다. [Hello 포털에서 검색 서비스 만들기](search-create-service-portal.md) tooget hello 서비스 URL과 키 속성 hello 요청에서 사용 하는 방법을 설명 합니다.

**응답**

상태 코드: 응답에 성공하면 ‘200 OK’가 반환됩니다.

hello 응답 본문 (있는 경우) 전반적인 인덱서 상태, 마지막 인덱서 호출 hello 뿐 아니라 최근 인덱서 호출 기록 hello에 대 한 정보를 포함 합니다. 

아래에 샘플 응답 본문이 나와 있습니다. 

    {
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
         },
        "executionHistory":[ {
            "status":"success",
             "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        }]
    }

**인덱서 상태**

인덱서 상태 hello 다음 값 중 하나일 수 있습니다.

* `running`해당 hello 인덱서 정상적으로 실행 되 고 나타냅니다. 있으므로 정보에 hello 인덱서 실행의 일부 계속 실패할 수 있습니다, 것이 좋습니다 toocheck hello `lastResult` 속성 뿐입니다. 
* `error`hello 인덱서 해당 사용자가 직접 해결할 수 없는 오류가 발생 했음을 나타냅니다. 예를 들어 hello 데이터 원본 자격 증명, 만료 되었거나 hello 스키마 hello 데이터 원본의 또는 hello 대상 인덱스의 주요에서 변경 된 방식으로 합니다. 

**인덱서 실행 결과**

인덱서 실행 결과에는 단일 인덱서 실행에 대한 정보가 포함됩니다. hello로 hello 최신 결과 표시는 `lastResult` hello 인덱서 상태의 속성입니다. Hello로 반환 있으면 기타 최근 결과 `executionHistory` hello 인덱서 상태의 속성입니다. 

인덱서 실행 결과 다음과 같은 속성 hello를 포함 되어 있습니다. 

* `status`: hello 실행의 상태입니다. 자세한 내용은 아래의 [인덱서 실행 상태](#IndexerExecutionStatus) 를 참조하세요. 
* `errorMessage`: 실패한 실행에 대한 오류 메시지입니다. 
* `startTime`: hello 시간 (UTC)이이 실행이 시작 되었습니다.
* `endTime`: hello 시간 (UTC)이이 실행이 중지 되었습니다. Hello 실행이 아직 진행 중인 경우에이 값이 설정 되지 않았습니다.
* `errors`: 항목 수준 오류(있는 경우)의 배열입니다. 각 항목은 문서 키(`key` 속성) 및 오류 메시지(`errorMessage` 속성)를 포함하고 있습니다. 
* `itemsProcessed`: hello이 실행 중 시도 인덱서 tooindex hello 데이터 원본 항목 (예를 들어 테이블 행)의 수입니다. 
* `itemsFailed`: hello이 실행 중 실패 한 항목 수입니다.  
* `initialTrackingState`: 항상 `null` hello 첫 번째 인덱서 실행에 대 한 hello 데이터 변경 내용 추적 정책을 사용 하는 경우 또는 hello 사용 되는 데이터 원본에 설정 되지 않았습니다. 이러한 정책을 사용 하는 경우 후속 실행에서이 값 hello 첫 번째 (최소) 변경을 내용 추적 해당이 실행에서 처리 하는 값을 나타냅니다. 
* `finalTrackingState`: 항상 `null` hello 데이터 변경 내용 추적 정책을 사용 하는 hello 데이터 원본에서는 사용 되지 않습니다. 그렇지 않으면 hello 최신 (최대) 변경을 내용 추적에서이 실행이 성공적으로 처리 하는 값을 나타냅니다. 

<a name="IndexerExecutionStatus"></a>
**인덱서 실행 상태**

인덱서 실행 상태를 단일 인덱서 실행의 hello 상태를 캡처합니다. Hello 다음 값을 가질 수 있습니다.

* `success`hello 인덱서 실행이 성공적으로 완료 되었음을 나타냅니다.
* `inProgress`hello 인덱서 실행 진행 중임을 나타냅니다. 
* `transientFailure` : 인덱서 실행에 실패했음을 나타냅니다. 자세한 내용은 `errorMessage` 속성을 참조하세요. hello 실패 수에 필요 하지 않거나 사용자가 직접 toofix-예를 들어 hello 데이터 원본과 hello 대상 인덱스 간의 스키마 비 호환성을 해결이 필요한 사용자 작업을 임시 데이터 원본 가동 중지 시간이 없습니다. 인덱서 호출은 일정(있는 경우)에 따라 계속 진행됩니다. 
* `persistentFailure`사용자의 개입을 필요로 하는 방식으로 해당 hello 인덱서 실패 했음을 나타냅니다. 이 상태에서는 예약된 인덱서 실행이 중지됩니다. Hello 문제를 해결 한 후 다시 설정 하는 인덱서 API toorestart hello 예약 실행 오류를 사용 합니다. 
* `reset`해당 hello 인덱서가 호출 tooReset 인덱서 API (아래 참조)로 다시 설정 된 것을 나타냅니다. 

<a name="ResetIndexer"></a>

## <a name="reset-indexer"></a>인덱서 다시 설정
hello **인덱서 다시 설정** 작업 hello 변경 내용 추적 hello 인덱서와 관련 된 상태를 다시 설정 합니다. 이렇게 하면 tootrigger 처음부터 인덱싱을 다시 수행 (예: 데이터 원본 스키마가 변경 된 경우) 또는 hello 인덱서와 관련 된 데이터 원본에 대 한 toochange hello 데이터 변경 검색 정책을 있습니다.   

    POST https://[service name].search.windows.net/indexers/[indexer name]/reset?api-version=[api-version]
    api-key: [admin key]

hello `api-version` 가 필요 합니다. hello 미리 보기 버전을 `2015-02-28-Preview`합니다. 

hello `api-key` (것과 반대로 tooa 쿼리 키)로 관리자 키 여야 합니다. Toohello 인증 섹션에서 참조 [검색 서비스 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn 키에 대 한 자세한 합니다. [Hello 포털에서 검색 서비스 만들기](search-create-service-portal.md) tooget hello 서비스 URL과 키 속성 hello 요청에서 사용 하는 방법을 설명 합니다.

**응답**

상태 코드: 응답에 성공하면 ‘204 콘텐츠 없음'이 반환됩니다.

## <a name="mapping-between-sql-data-types-and-azure-search-data-types"></a>SQL 데이터 형식과 Azure 검색 데이터 형식 사이의 매핑
<table style="font-size:12">
<tr>
<td>SQL 데이터 형식</td>    
<td>허용되는 대상 인덱스 필드 유형</td>
<td>참고 사항</td>
</tr>
<tr>
<td>bit</td>
<td>Edm.Boolean, Edm.String</td>
<td></td>
</tr>
<tr>
<td>int, smallint, tinyint</td>
<td>Edm.Int32, Edm.Int64, Edm.String</td>
<td></td>
</tr>
<tr>
<td>bigint</td>
<td>Edm.Int64, Edm.Int64, Edm.String</td>
<td></td>
</tr>
<tr>
<td>real, float</td>
<td>Edm.Double, Edm.String</td>
<td></td>
</tr>
<tr>
<td>smallmoney, money<br>decimal<br>numeric
</td>
<td>Edm.String</td>
<td>Azure 검색에서는 decimal 형식을 Edm.Double로 변환하면 정밀도가 떨어지기 때문에 이를 지원하지 않습니다.
</td>
</tr>
<tr>
<td>char, nchar, varchar, nvarchar</td>
<td>Edm.String<br/>Collection(Edm.String)</td>
<td>참조 [필드 매핑 함수](#FieldMappingFunctions) 방법에 대 한 자세한 내용은이 문서의 tootransform는 collection (edm.string)로 문자열 열</td>
</tr>
<tr>
<td>smalldatetime, datetime, datetime2, date, datetimeoffset</td>
<td>Edm.DateTimeOffset, Edm.String</td>
<td></td>
</tr>
<tr>
<td>uniqueidentifer</td>
<td>Edm.String</td>
<td></td>
</tr>
<tr>
<td>geography</td>
<td>Edm.GeographyPoint</td>
<td>SRID가 4326 (hello 기본값) 인 POINT 유형의 지리 인스턴스만 지원 됩니다.</td>
</tr>
<tr>
<td>rowversion</td>
<td>해당 없음</td>
<td>변경 내용 추적에 사용할 수 있지만 행 버전 열 hello 검색 인덱스에 저장할 수 없습니다.</td>
</tr>
<tr>
<td>time, timespan<br>binary, varbinary, image,<br>xml, geometry, CLR 형식</td>
<td>해당 없음</td>
<td>지원되지 않음</td>
</tr>
</table>

## <a name="mapping-between-json-data-types-and-azure-search-data-types"></a>JSON 데이터 형식과 Azure 검색 데이터 형식 사이의 매핑
<table style="font-size:12">
<tr>
<td>JSON 데이터 형식</td>    
<td>허용되는 대상 인덱스 필드 유형</td>
<td>참고 사항</td>
</tr>
<tr>
<td>bool</td>
<td>Edm.Boolean, Edm.String</td>
<td></td>
</tr>
<tr>
<td>정수</td>
<td>Edm.Int32, Edm.Int64, Edm.String</td>
<td></td>
</tr>
<tr>
<td>부동 소수점 숫자</td>
<td>Edm.Double, Edm.String</td>
<td></td>
</tr>
<tr>
<td>string</td>
<td>Edm.String</td>
<td></td>
</tr>
<tr>
<td>기본 형식의 배열, 예: ["a", "b", "c"]</td>
<td>Collection(Edm.String)</td>
<td></td>
</tr>
<tr>
<td>날짜처럼 보이는 문자열</td>
<td>Edm.DateTimeOffset, Edm.String</td>
<td></td>
</tr>
<tr>
<td>GeoJSON point 개체</td>
<td>Edm.GeographyPoint</td>
<td>GeoJSON 지점은 JSON 개체의 형식에 따라 hello: {"type": "Point", "coordinates": [long, lat]} </td>
</tr>
<tr>
<td>기타 JSON 개체</td>
<td>해당 없음</td>
<td>지원되지 않음. Azure 검색에서는 현재 기본 형식과 문자열 컬렉션만 지원합니다.</td>
</tr>
</table>
