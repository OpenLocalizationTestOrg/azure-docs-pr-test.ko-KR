---
title: "Azure 테이블 저장소와 Azure 검색 aaaIndexing | Microsoft Docs"
description: "Tooindex 데이터 Azure 검색을 사용한 Azure 테이블 저장소에 저장 하는 방법에 대해 알아봅니다"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 1cc27411-d0cc-40ed-8aed-c7cb9ab402b9
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/10/2017
ms.author: eugenesh
ms.openlocfilehash: abb01a4d807cede310246b34775d8059fceb4456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="index-azure-table-storage-with-azure-search"></a>Azure Search를 사용하여 Azure Table Storage 인덱싱
이 문서에서는 Azure 검색 tooindex 데이터 toouse Azure 테이블 저장소에 저장 하는 방법을 설명 합니다.

## <a name="set-up-azure-table-storage-indexing"></a>Azure Table Storage 인덱싱 설정

다음 리소스를 사용하여 Azure Table Storage 인덱서를 설정할 수 있습니다.

* [Azure 포털](https://ms.portal.azure.com)
* Azure Search [REST API](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations)
* Azure Search [.NET SDK](https://aka.ms/search-sdk)

여기에 대해서도 설명 hello 흐름 hello REST API를 사용 하 여 합니다. 

### <a name="step-1-create-a-datasource"></a>1단계: 데이터 원본 만들기

데이터 원본이 있는 데이터 tooindex 지정, hello 필요한 자격 증명이 tooaccess hello 데이터 및 Azure 검색 tooefficiently 수 있도록 하는 hello 정책 hello 데이터의 변경 내용을 식별 합니다.

테이블 인덱싱에 대 한 다음과 같은 속성 hello hello 데이터 원본에 있어야 합니다.

- **이름** hello hello 데이터 원본 검색 서비스 내에서 고유 이름입니다.
- **type**은 `azuretable`여야 합니다.
- **자격 증명** 매개 변수에 hello 저장소 계정 연결 문자열을 포함 합니다. Hello 참조 [자격 증명을 지정](#Credentials) 자세한 내용은 섹션.
- **컨테이너** 집합 hello 테이블 이름 및 선택적 쿼리 합니다.
    - Hello를 사용 하 여 hello 테이블 이름을 지정 `name` 매개 변수입니다.
    - 필요에 따라 hello를 사용 하 여 쿼리를 지정 `query` 매개 변수입니다. 

> [!IMPORTANT] 
> 가능한 경우 성능 향상을 위해 PartitionKey에 대한 필터를 사용합니다. 다른 쿼리는 전체 테이블 검색을 수행하므로 대형 테이블에서 성능 저하가 발생합니다. Hello 참조 [성능 고려 사항](#Performance) 섹션.


datasource toocreate:

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "table-datasource",
        "type" : "azuretable",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-table", "query" : "PartitionKey eq '123'" }
    }   

데이터 원본 만들기 API hello에 대 한 자세한 내용은 참조 하십시오. [데이터 원본 만들기](https://docs.microsoft.com/rest/api/searchservice/create-data-source)합니다.

<a name="Credentials"></a>
#### <a name="ways-toospecify-credentials"></a>같은 방법으로 toospecify 자격 증명 ####

다음이 방법 중 하나에 hello 테이블에 대 한 hello 자격 증명을 제공할 수 있습니다. 

- **전체 액세스 저장소 계정 연결 문자열**: `DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>` toohello 이동 하 여 hello Azure 포털에서에서 hello 연결 문자열을 가져올 수 있습니다 **저장소 계정 블레이드** > **설정**   >  **키** (클래식 저장소 계정의 경우) 또는 **설정** > **선택키가** (Azure 리소스에 대 한 관리자 저장소 계정)입니다.
- **저장소 계정을 공유 액세스 서명 연결 문자열**: `TableEndpoint=https://<your account>.table.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<hello signature>&spr=https&se=<hello validity end time>&srt=co&ss=t&sp=rl` hello 공유 액세스 서명을 hello 나열 하 고 (이 경우 테이블) 컨테이너 및 개체 (테이블 행)에 대해 읽기 권한이 있어야 합니다.
-  **테이블 공유 액세스 서명을**: `ContainerSharedAccessUri=https://<your storage account>.table.core.windows.net/<table name>?tn=<table name>&sv=2016-05-31&sig=<hello signature>&se=<hello validity end time>&sp=r` hello 공유 액세스 서명을 hello 테이블에 대 한 쿼리 (읽기 대상) 권한이 있어야 합니다.

저장소 공유 액세스 서명에 대한 자세한 내용은 [공유 액세스 서명 사용](../storage/common/storage-dotnet-shared-access-signature-part-1.md)을 참조하세요.

> [!NOTE]
> 공유 액세스 서명 자격 증명을 사용 하는 경우 만료 기한을 지나더라도 tooupdate hello 데이터 원본 자격 증명 갱신 된 서명 tooprevent 정기적으로 사용 해야 합니다. Hello 인덱서 실패 하 고 너무 "hello 연결 문자열에 제공 된 자격 증명이 잘못 되었거나 만료 합니다."와 비슷한 오류 메시지가 공유 액세스 서명 자격 증명이 만료 되는 경우  

### <a name="step-2-create-an-index"></a>2단계: 인덱스 만들기
hello 인덱스 hello 특성 문서의 hello 필드를 지정 하 고 해당 셰이프에 hello 검색 환경을 생성 하는 다른 합니다.

toocreate 인덱스:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
          "name" : "my-target-index",
          "fields": [
            { "name": "key", "type": "Edm.String", "key": true, "searchable": false },
            { "name": "SomeColumnInMyTable", "type": "Edm.String", "searchable": true }
          ]
    }

인덱스 만들기에 자세한 내용은 [인덱스 만들기](https://docs.microsoft.com/rest/api/searchservice/create-index)를 참조하세요.

### <a name="step-3-create-an-indexer"></a>3단계: 인덱서 만들기
인덱서는 데이터 원본을 대상 검색 인덱스와 연결 하 고는 tooautomate hello 데이터 새로 고침 예약을 제공 합니다. 

Hello 인덱스 및 데이터 원본이 만들어진 후에 준비 toocreate hello 인덱서 수 있습니다:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "table-indexer",
      "dataSourceName" : "table-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" }
    }

이 인덱서는 2시간 간격으로 실행됩니다 (hello 일정 간격이 너무 설정 되어 "PT2H"입니다.) 인덱서 toorun 30 분 마다 설정 hello 간격 너무 "에서는 PT30M"입니다. hello 가장 짧은 지원 되는 간격은 5 분입니다. hello 일정은 선택 사항입니다. 생략 하는 경우 인덱서 만들어질 때 한 번만 실행 됩니다. 그러나 언제든지 필요할 때 인덱서를 실행할 수 있습니다.   

Hello 만들기 인덱서 API에 대 한 자세한 내용은 참조 하십시오. [인덱서 만들기](https://docs.microsoft.com/rest/api/searchservice/create-indexer)합니다.

## <a name="deal-with-different-field-names"></a>다른 필드 이름 처리
경우에 따라 hello 필드 이름이 기존 인덱스에 테이블의 속성 이름에 hello와 다릅니다. 검색 인덱스에 hello 테이블 toohello 필드 이름에서 필드 매핑을 toomap hello 속성 이름에 사용할 수 있습니다. 필드 매핑에 대 한 자세한 정보는 toolearn 참조 [Azure 검색 인덱서 필드 매핑 hello 차이점 datasources 및 검색 인덱스 연결](search-indexer-field-mappings.md)합니다.

## <a name="handle-document-keys"></a>문서 키 처리
Azure 검색에서는 hello 문서 키 문서를 고유 하 게 식별합니다. 모든 검색 인덱스는 `Edm.String`형식의 키 필드를 정확히 하나만 포함해야 합니다. hello 키 필드가 toohello 인덱스 추가 되는 각 문서에 필요 합니다. (실제로 hello만 필수 필드입니다.)

테이블 행에 복합 키가 있으므로 Azure Search에서 파티션 키와 행 키 값을 연결한 `Key`라는 합성 필드를 생성합니다. 예를 들어 행의 PartitionKey를 `PK1` RowKey는 `RK1`, 다음 hello `Key` 필드의 값이 `PK1RK1`합니다.

> [!NOTE]
> hello `Key` 값 대시 등의 문서 키에 유효 하지 않은 문자를 포함할 수 있습니다. Hello를 사용 하 여 잘못 된 문자를 처리할 수 있는 `base64Encode` [필드 매핑 함수](search-indexer-field-mappings.md#base64EncodeFunction)합니다. 이 작업을 수행 하는 경우 tooalso 사용 하 여 URL 해도 안전한 Base64 인코딩을 조회 같은 호출 API 문서 키를 전달 해야 합니다.
>
>

## <a name="incremental-indexing-and-deletion-detection"></a>증분 인덱싱 및 삭제 감지
행의 기준으로 새롭거나 업데이트 된 행을 reindexes 일정에 따라 테이블 인덱서 toorun을 설정할 때 `Timestamp` 값입니다. Toospecify 변경 검색 정책을 않아도 됩니다. 증분 인덱싱이 자동으로 사용됩니다.

tooindicate 특정 hello 인덱스에서 문서를 제거 해야 일시 삭제 전략을 사용할 수 있습니다. 행을 삭제 하는 대신 삭제 않으며 hello 데이터 원본의 소프트 삭제 검색 정책을 설정 하는 속성 tooindicate를 추가 합니다. 예를 들어 hello 정책 다음 고려 hello 행 속성이 있는 경우 행이 삭제 `IsDeleted` hello 값을 가진 `"true"`:

    PUT https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-table-datasource",
        "type" : "azuretable",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "table name", "query" : "<query>" },
        "dataDeletionDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy", "softDeleteColumnName" : "IsDeleted", "softDeleteMarkerValue" : "true" }
    }   

<a name="Performance"></a>
## <a name="performance-considerations"></a>성능 고려 사항

기본적으로 Azure 검색에서는 쿼리 필터를 다음 hello를 사용: `Timestamp >= HighWaterMarkValue`합니다. Azure 테이블 hello에 보조 인덱스를이 없기 때문에 `Timestamp` 이러한 유형의 쿼리는 전체 테이블 검색 하며 느립니다. 따라서 대형 테이블에 대 한 필드입니다.


다음은 테이블 인덱싱 성능을 향상시킬 수 있는 두 가지 가능한 방법입니다. 이러한 두 방법 모두 테이블 파티션을 사용합니다. 

- 데이터가 기본적으로 여러 파티션 범위로 분할될 수 있으면 각 파티션 범위에 대한 데이터 원본 및 해당 인덱서를 만듭니다. 각 인덱서는 이제 tooprocess 특정 파티션 범위만, 쿼리 성능이 개선에 있습니다. 인덱싱된 toobe 해야 하는 hello 데이터에 더 나은 고정된 파티션 수가 적은 경우: 각 인덱서만 분할 검색을 수행 합니다. 예를 들어 toocreate 처리 된 파티션 범위에 대 한 데이터 원본 키가에서 `000` 너무`100`, 다음과 같은 쿼리를 사용 하 여: 
    ```
    "container" : { "name" : "my-table", "query" : "PartitionKey ge '000' and PartitionKey lt '100' " }
    ```

- 데이터는 시간별으로 분할 하는 경우 (예를 들어 하루 또는 한 주 모든 새 파티션을 만들려면 있습니다) 방법 hello는 것이 좋습니다. 
    - Hello 폼의 쿼리를 사용 하 여: `(PartitionKey ge <TimeStamp>) and (other filters)`합니다. 
    - 사용 하 여 인덱서 진행률을 모니터링할 [인덱서 상태 API 가져오기](https://docs.microsoft.com/rest/api/searchservice/get-indexer-status), hello를 정기적으로 업데이트 하 고 `<TimeStamp>` hello 최신 성공적인 높은 수준 값을 기반으로 하는 hello 쿼리의 상태입니다. 
    - 이 접근 방식 tootrigger는 전체 인덱스를 다시 만들기, 필요한 경우 더하기 tooresetting hello 인덱서의 tooreset hello 데이터 원본 쿼리가 필요 합니다. 


## <a name="help-us-make-azure-search-better"></a>Azure Search 개선 지원
기능 요청 또는 개선에 대한 아이디어가 있는 경우 [UserVoice 사이트](https://feedback.azure.com/forums/263029-azure-search/)를 통해 제출합니다.
