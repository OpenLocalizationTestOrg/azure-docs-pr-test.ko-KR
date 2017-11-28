---
title: "aaaIndexing Azure 검색을 통해 Azure Blob 저장소"
description: "Azure 검색 tooindex Azure Blob 저장소 및 추출 텍스트에서 설명 하는 방법에 대해 알아봅니다"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 2a5968f4-6768-4e16-84d0-8b995592f36a
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/22/2017
ms.author: eugenesh
ms.openlocfilehash: 1bdd34e66a4a9192ed88cacbc7b8456d0dcdfeb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-documents-in-azure-blob-storage-with-azure-search"></a>Azure Search로 Azure Blob Storage에서 문서 인덱싱
이 문서에서는 어떻게 toouse Azure 검색 tooindex 문서 (Pdf와 같은 Microsoft Office 문서 및 다른 몇 가지 일반적인 형식) Azure Blob 저장소에 저장 합니다. 첫째, 설정 및 구성 blob 인덱서의 hello 기본 사항을 설명 합니다. 그런 다음, 동작 및 가능성이 tooencounter는 시나리오의 깊은 탐색을 제공 합니다.

## <a name="supported-document-formats"></a>지원되는 문서 형식
hello blob 인덱서 hello 문서 형식 뒤에서 텍스트를 추출할 수 있습니다.:

* PDF
* Microsoft Office 형식: DOCX/DOC, XLSX/XLS, PPTX/PPT, MSG(Outlook 전자 메일)  
* HTML
* XML
* ZIP
* EML
* RTF
* 일반 텍스트 파일([일반 텍스트 인덱싱](#IndexingPlainText)도 참조)
* JSON([JSON BLOB 인덱싱](search-howto-index-json-blobs.md) 참조)
* CSV([CSV BLOB 인덱싱](search-howto-index-csv-blobs.md) 미리 보기 기능 참조)

> [!IMPORTANT]
> CSV 및 JSON 배열에 대한 지원은 현재 미리 보기 상태입니다. 이러한 형식은 버전을 사용 하 여 사용할 수 있는 **2016-09-01-미리 보기** hello.NET SDK의 hello REST API 또는 버전 2.x-미리 보기의 합니다. 미리 보기 API는 테스트 및 평가 용도로 제공되며 프로덕션 환경에는 사용되지 않는다는 점을 유념하세요.
>
>

## <a name="setting-up-blob-indexing"></a>BLOB 인덱싱 설정
다음을 사용하여 Azure Blob Storage 인덱서를 설정할 수 있습니다.

* [쉬운 테이블](https://ms.portal.azure.com)
* Azure Search [REST API](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations)
* Azure Search [.NET SDK](https://aka.ms/search-sdk)

> [!NOTE]
> 일부 기능 (예: 필드 매핑)는 아직 hello 포털에서 사용할 수 있고 toobe 프로그래밍 방식으로 사용.
>
>

여기서 hello 흐름을 hello REST API를 사용 하 여 보여 줍니다.

### <a name="step-1-create-a-data-source"></a>1단계: 데이터 소스 만들기
데이터 원본은 데이터 tooindex, 필요한 자격 증명 tooaccess hello 데이터 및 정책 tooefficiently hello 데이터 (새, 수정 또는 삭제 된 행)의 변경 내용을 식별할를 지정 합니다. 데이터 원본을 사용할 수 있습니다 hello에 여러 인덱서에서 동일 서비스 항목을 검색 합니다.

Blob 인덱싱에 대 한 다음과 같은 필수 속성 hello hello 데이터 원본에 있어야 합니다.

* **이름** hello hello 데이터 원본 검색 서비스 내에서 고유 이름입니다.
* **type**은 `azureblob`여야 합니다.
* **자격 증명** hello로 hello 저장소 계정 연결 문자열을 제공 `credentials.connectionString` 매개 변수입니다. 참조 [어떻게 toospecify 자격 증명](#Credentials) 아래의 세부 정보에 대 한 합니다.
* **container**는 저장소 계정에 있는 컨테이너를 지정합니다. 기본적으로 hello 컨테이너 내 모든 blob는 검색할 수 있습니다. 특정 가상 디렉터리의 tooindex blob만 하려는 경우 선택적 hello를 사용 하 여 해당 디렉터리를 지정할 수 있습니다 **쿼리** 매개 변수입니다.

toocreate 데이터 원본:

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "<optional-virtual-directory-name>" }
    }   

에 대 한 자세한 hello 만들기 Datasource API 참조 하세요. [데이터 원본 만들기](https://docs.microsoft.com/rest/api/searchservice/create-data-source)합니다.

<a name="Credentials"></a>
#### <a name="how-toospecify-credentials"></a>어떻게 toospecify 자격 증명 ####

다음이 방법 중 하나에 hello blob 컨테이너에 대 한 hello 자격 증명을 제공할 수 있습니다.

- **전체 액세스 저장소 계정 연결 문자열**: `DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>`. Toohello 저장소 계정 블레이드를 탐색 하 여 hello Azure 포털에서에서 hello 연결 문자열을 가져올 수 있습니다 > 설정 > 클래식 저장소 계정에는 키 또는 설정 > 선택 키 (저장소 계정은 Azure 리소스 관리자)에 대 한 합니다.
- **저장소 계정 공유 액세스 서명을** (SAS) 연결 문자열: `BlobEndpoint=https://<your account>.blob.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<hello signature>&spr=https&se=<hello validity end time>&srt=co&ss=b&sp=rl` hello SAS hello 나열 하 고 컨테이너 및 개체에 대해 읽기 권한이 있어야 합니다. (이 경우 blob).
-  **컨테이너 공유 액세스 서명을**: `ContainerSharedAccessUri=https://<your storage account>.blob.core.windows.net/<container name>?sv=2016-05-31&sr=c&sig=<hello signature>&se=<hello validity end time>&sp=rl` hello SAS hello 나열 하 고 hello 컨테이너에 대해 읽기 권한이 있어야 합니다.

저장소 공유 액세스 서명에 대한 자세한 내용은 [공유 액세스 서명 사용](../storage/common/storage-dotnet-shared-access-signature-part-1.md)을 참조하세요.

> [!NOTE]
> SAS 자격 증명을 사용 하는 경우 만료 기한을 지나더라도 tooupdate hello 데이터 원본 자격 증명 갱신 된 서명 tooprevent 정기적으로 사용 해야 합니다. Hello 인덱서 못합니다와 유사한 오류 메시지가 너무 SAS 자격 증명이 만료 되 면`Credentials provided in hello connection string are invalid or have expired.`합니다.  

### <a name="step-2-create-an-index"></a>2단계: 인덱스 만들기
hello index 특성, 문서에서 hello 필드를 지정 하 고 해당 셰이프에 hello 검색 환경을 생성 하는 다른 합니다.

다음은 어떻게 toocreate 검색 가능한이 있는 인덱스 `content` toostore hello 텍스트 blob에서 추출 된 필드:   

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
          "name" : "my-target-index",
          "fields": [
            { "name": "id", "type": "Edm.String", "key": true, "searchable": false },
            { "name": "content", "type": "Edm.String", "searchable": true, "filterable": false, "sortable": false, "facetable": false }
          ]
    }

인덱스 만들기에 자세한 내용은 [인덱스 만들기](https://docs.microsoft.com/rest/api/searchservice/create-index)를 참조하세요.

### <a name="step-3-create-an-indexer"></a>3단계: 인덱서 만들기
인덱서는 데이터 원본을 대상 검색 인덱스와 연결 하 고는 tooautomate hello 데이터 새로 고침 예약을 제공 합니다.

Hello 인덱스 및 데이터 소스를 만든 준비 toocreate hello 인덱서 수 있습니다.

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "blob-indexer",
      "dataSourceName" : "blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" }
    }

이 인덱서는 2 시간 마다 실행 됩니다 (일정 간격을 너무 설정 "PT2H"). 인덱서 toorun 30 분 마다 설정 hello 간격 너무 "에서는 PT30M"입니다. hello 가장 짧은 지원 되는 간격은 5 분입니다. hello 일정은 선택 사항-생략 하는 경우, 인덱서 만들어질 때 한 번만 실행 합니다. 그러나 언제든지 필요할 때 인덱서를 실행할 수 있습니다.   

에 대 한 자세한 내용은 hello 인덱서 API 만들기, 체크 아웃 [인덱서 만들기](https://docs.microsoft.com/rest/api/searchservice/create-indexer)합니다.

## <a name="how-azure-search-indexes-blobs"></a>Azure Search가 BLOB을 인덱싱하는 방식

Hello에 따라 [indexer 구성](#PartsOfBlobToIndex), hello blob 인덱서 저장소 메타 데이터를 인덱싱할 수 (약 대해서만 관심 hello 메타 데이터 및 tooindex 필요 하지 않은 경우에 유용함 blob의 내용을 hello), 저장소 및 콘텐츠 메타 데이터 또는 둘 다 메타 데이터 및 텍스트 콘텐츠입니다. 기본적으로 hello 인덱서 메타 데이터와 콘텐츠를 추출합니다.

> [!NOTE]
> 기본적으로 JSON 또는 CSV와 같이 구조화된 콘텐츠를 포함하는 Blob은 단일 텍스트 청크로 인덱싱됩니다. Tooindex JSON 및 CSV blob을 체계적으로 하려는 경우 참조 [JSON 인덱싱 blob](search-howto-index-json-blobs.md) 및 [CSV 인덱싱 blob](search-howto-index-csv-blobs.md) 미리 보기 기능입니다.
>
> 복합 또는 포함된 문서(예: ZIP 보관 파일 또는 첨부 파일이 있는 Outlook 메일이 포함된 Word 문서)도 단일 문서로 인덱싱됩니다.

* 라는 문자열 필드에 hello 문서의 hello 텍스트 콘텐츠를 추출할 `content`합니다.

> [!NOTE]
> Azure 검색 가격 책정 계층 hello에 따라 추출 텍스트의 양이 제한: 32, 000 자 무료 계층, basic의 경우 64, 000 및 표준, 표준 S2, S3 표준 계층에 대 한 4 백만 합니다. 경고는 잘린된 문서에 대 한 hello 인덱서 상태 응답에 포함 됩니다.  

* Hello blob에 사용자 지정 메타 데이터 속성이 있는 경우 추출 정확 하 게 합니다.
* Hello 필드 뒤에 표준 blob 메타 데이터 속성 압축이 풀립니다.

  * **메타 데이터\_저장소\_이름** (Edm.String)-hello blob의 hello 파일 이름입니다. 예를 들어 blob /my-container/my-folder/subfolder/resume.pdf를 설정한 경우 hello이 필드의 값이은 `resume.pdf`합니다.
  * **메타 데이터\_저장소\_경로** (Edm.String)-hello hello 저장소 계정을 포함 하 여 hello blob의 전체 URI입니다. 예를 들어 `https://myaccount.blob.core.windows.net/my-container/my-folder/subfolder/resume.pdf`
  * **메타 데이터\_저장소\_콘텐츠\_형식** (Edm.String)-hello 코드에 의해 지정 된 대로 콘텐츠 형식 tooupload hello blob을 사용 합니다. 예: `application/octet-stream`.
  * **메타 데이터\_저장소\_마지막\_수정** (Edm.DateTimeOffset)-hello blob에 대 한 타임 스탬프를 마지막으로 수정 합니다. 이 타임 스탬프 변경 tooidentify blob을 tooavoid hello 초기 인덱싱한 후 모든 인덱스를 다시 만들기를 사용 하는 azure 검색 합니다.
  * **metadata\_storage\_size** (Edm.Int64) - BLOB 크기(바이트).
  * **메타 데이터\_저장소\_콘텐츠\_md5** (Edm.String)-가능한 경우 hello blob 콘텐츠의 MD5 해시입니다.
* 메타 데이터 속성 특정 tooeach 문서 형식이 나열 된 hello 필드로 추출 되 [여기](#ContentSpecificMetadata)합니다.

검색 인덱스에 모든 속성 위에 hello에 대 한 toodefine 필드를 필요 하지 않습니다-바로 응용 프로그램에 필요한 hello 속성을 캡처합니다.

> [!NOTE]
> 종종 hello 필드 이름이 기존 인덱스의 문서 추출 하는 동안 생성 된 hello 필드 이름은 다르게 됩니다. 사용할 수 있습니다 **필드 매핑** toomap hello 속성 이름에서 Azure 검색 toohello 필드 이름을 검색 인덱스에 제공 합니다. 아래에 필드 매핑 사용 예제가 있습니다.
>
>

<a name="DocumentKeys"></a>
### <a name="defining-document-keys-and-field-mappings"></a>문서 키 및 필드 매핑 정의
Azure 검색에서는 hello 문서 키 문서를 고유 하 게 식별합니다. 모든 검색 인덱스는 Edm.String 형식의 키 필드를 정확히 하나만 포함해야 합니다. hello 키 필드가 toohello 인덱스 (실제로 hello 유일한 필수 필드는) 추가 되는 각 문서에 필요 합니다.  

신중 하 게 추출 된 필드를 매핑하는 toohello 인덱스에 키 필드는 것이 좋습니다. hello 후보는:

* **메타 데이터\_저장소\_이름** -이 편리한 후보가 될 수 있지만 다른 폴더에 이름과 같은 이름을 hello 사용 하 여 blob 수 있으면 1) hello 이름 고유 아닐 수 있습니다 및 2) hello 이름 문자를 포함할 수 있는 대시 등의 문서 키에 유효 하지 않습니다. Hello를 사용 하 여 잘못 된 문자를 처리할 수 있는 `base64Encode` [필드 매핑 함수](search-indexer-field-mappings.md#base64EncodeFunction) -이 작업을 수행 하는 경우 조회 같은 호출 API에 전달 하면 tooencode 문서 키를 기억 합니다. (예를 들어.NET에서 사용할 수 있습니다 hello [UrlTokenEncode 메서드](https://msdn.microsoft.com/library/system.web.httpserverutility.urltokenencode.aspx) 포함 하기 위해).
* **메타 데이터\_저장소\_경로** -hello 전체 경로 사용 하 여 반면, 고유성을 보장 하지만 hello 경로 확실 하 게 들어 `/` 않은 문자가 [문서 키에 잘못 된](https://docs.microsoft.com/rest/api/searchservice/naming-rules)합니다.  Hello를 사용 하 여 hello 키 인코딩 hello 옵션이 위의 제공 `base64Encode` [함수](search-indexer-field-mappings.md#base64EncodeFunction)합니다.
* Hello 옵션이 위의 적합 한 사용자 지정 메타 데이터 속성 toohello blob를 추가할 수 있습니다. 하지만이 옵션에 blob 업로드 프로세스 tooadd 해당 메타 데이터 속성 tooall blob 필요, 않습니다. Hello 키 필수 속성 이기 때문에 해당 속성이 없는 모든 blob 인덱싱된 toobe를 실패 합니다.

> [!IMPORTANT]
> Azure 검색을 자동으로 사용 hello hello 인덱스의 키 필드에 대 한 명시적 매핑이 없는 경우 `metadata_storage_path` 대로 키 및 base64 hello 키 값 (hello 두 번째 옵션 위의) 인코딩합니다.
>
>

이 예제에 대 한 선택 hello `metadata_storage_name` hello 문서 키로 필드입니다. 또한 가정해 인덱스가 라는 키 필드가 `key` 필드와 `fileSize` hello 문서 크기를 저장 하기 위한 합니다. 원하는 대로 toowire 높이려면 hello 필드 매핑을 만들거나 인덱서를 업데이트할 때 다음을 지정 합니다.

    "fieldMappings" : [
      { "sourceFieldName" : "metadata_storage_name", "targetFieldName" : "key", "mappingFunction" : { "name" : "base64Encode" } },
      { "sourceFieldName" : "metadata_storage_size", "targetFieldName" : "fileSize" }
    ]

toobring이 모두 함께 여기의 필드 매핑 및 기존 인덱서에 대 한 키 사용 base 64 인코딩를 추가 하는 방법:

    PUT https://[service name].search.windows.net/indexers/blob-indexer?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "dataSourceName" : " blob-datasource ",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "fieldMappings" : [
        { "sourceFieldName" : "metadata_storage_name", "targetFieldName" : "key", "mappingFunction" : { "name" : "base64Encode" } },
        { "sourceFieldName" : "metadata_storage_size", "targetFieldName" : "fileSize" }
      ]
    }

> [!NOTE]
> 필드 매핑에 대 한 자세한 정보는 toolearn 참조 [이 여기서](search-indexer-field-mappings.md)합니다.
>
>

<a name="WhichBlobsAreIndexed"></a>
## <a name="controlling-which-blobs-are-indexed"></a>인덱싱할 Blob 제어
인덱싱할 Blob과 건너뛸 Blob을 제어할 수 있습니다.

### <a name="index-only-hello-blobs-with-specific-file-extensions"></a>특정 파일 확장명을 가진 hello blob만 인덱스
Hello를 사용 하 여 지정 하는 hello 파일 이름 확장명을 가진 hello blob만 인덱싱할 수 `indexedFileNameExtensions` 인덱서 구성 매개 변수입니다. hello 값은 파일 확장명 (앞의 점)와 쉼표로 구분 된 목록을 포함 하는 문자열입니다. 예를 들어 tooindex만 번호입니다. PDF 및 합니다. DOCX blob이 작업을 수행 합니다.

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "indexedFileNameExtensions" : ".pdf,.docx" } }
    }

### <a name="exclude-blobs-with-specific-file-extensions"></a>특정 파일 확장명으로 Blob 제외
Hello를 사용 하 여 인덱싱에서 특정 파일 이름 확장명을 사용 하 여 blob를 제외할 수 `excludedFileNameExtensions` 구성 매개 변수입니다. hello 값은 파일 확장명 (앞의 점)와 쉼표로 구분 된 목록을 포함 하는 문자열입니다. 예를 들어 모든 tooindex hello로 제외 하 고 blob입니다. PNG 하 고 있습니다. JPEG 확장을 수행 합니다.

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "excludedFileNameExtensions" : ".png,.jpeg" } }
    }

`indexedFileNameExtensions` 및 `excludedFileNameExtensions` 매개 변수가 모두 있는 경우 Azure Search는 먼저 `indexedFileNameExtensions`를 확인한 후 `excludedFileNameExtensions`를 찾습니다. 이 hello 동일한 파일 확장명이 있는 경우 두 목록에에서 제외 됩니다을 인덱싱하는 것을 의미 합니다.

### <a name="dealing-with-unsupported-content-types"></a>지원되지 않는 콘텐츠 형식 처리

기본적으로 hello blob 인덱서는 지원 되지 않는 콘텐츠 형식 (예: 이미지)를 사용 하 여 blob를 발견 되는 즉시 중지 합니다. Hello에서는 물론 `excludedFileNameExtensions` 매개 변수 tooskip 특정 콘텐츠 형식입니다. 그러나 모든 hello 가능한 콘텐츠 형식의 미리 알지 못해도 tooindex blob를 할 수 있습니다. 지원 되지 않는 콘텐츠 형식 발생 하면 인덱싱 toocontinue hello 설정 `failOnUnsupportedContentType` 구성 매개 변수가 너무`false`:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "failOnUnsupportedContentType" : false } }
    }

### <a name="ignoring-parsing-errors"></a>구문 분석 오류 무시

Azure 검색 문서 추출 논리 완벽 하지 및와 같은 지원 되는 콘텐츠 형식의 tooparse 문서 실패 때로는 합니다. DOCX 또는 합니다. PDF입니다. 이 경우 인덱싱 toointerrupt hello 하지 않으려면 hello 설정 `maxFailedItems` 및 `maxFailedItemsPerBatch` 구성 매개 변수 toosome 적당 한 값입니다. 예:

    {
      ... other parts of indexer definition
      "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 10 }
    }

<a name="PartsOfBlobToIndex"></a>
## <a name="controlling-which-parts-of-hello-blob-are-indexed"></a>Hello blob의 부분 인덱싱됩니다 제어

Hello를 사용 하 여 인덱싱된 hello blob의 부분을 제어할 수 있습니다 `dataToExtract` 구성 매개 변수입니다. 다음 값에는 hello를 걸릴 수 있습니다.

* `storageMetadata`-해당 유일한 hello 지정 [표준 blob 속성 및 사용자 지정 메타 데이터](../storage/blobs/storage-properties-metadata.md) 인덱싱됩니다.
* `allMetadata`-저장소 메타 데이터를 지정 및 hello [특정 메타 데이터 콘텐츠 형식](#ContentSpecificMetadata) 추출 hello blob에서 콘텐츠 인덱싱됩니다.
* `contentAndMetadata`-모든 메타 데이터 및 hello blob에서 추출 된 텍스트 콘텐츠 인덱싱 지정 합니다. Hello 기본값입니다.

예를 들어, tooindex 유일한 hello 저장소 메타 데이터를 사용 합니다.

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "dataToExtract" : "storageMetadata" } }
    }

### <a name="using-blob-metadata-toocontrol-how-blobs-are-indexed"></a>Blob 메타 데이터 toocontrol blob 인덱싱됩니다 방법을 사용 하 여

위에서 설명한 hello 구성 매개 변수는 tooall blob를 적용 합니다. 따라, toocontrol를 어떻게 할 수도 *각 blob* 인덱싱됩니다. Hello 다음을 추가 하 여 이렇게 하려면 blob 메타 데이터 속성 및 값:

| 속성 이름 | 속성 값 | 설명 |
| --- | --- | --- |
| AzureSearch_Skip |"true" |Hello blob 인덱서 toocompletely 건너뛰기 hello blob에 지시합니다. 메타데이터와 콘텐츠 추출이 모두 시도되지 않습니다. 특정 blob 반복적으로 실패 하 고 hello 인덱싱 프로세스를 중단 하는 경우에 유용 합니다. |
| AzureSearch_SkipContent |"true" |이 해당 하는 `"dataToExtract" : "allMetadata"` 설정을 [위에](#PartsOfBlobToIndex) 특정 blob 범위 지정 된 tooa 합니다. |

## <a name="incremental-indexing-and-deletion-detection"></a>증분 인덱싱 및 삭제 감지
일정에 따라 blob 인덱서 toorun을 설정할 때 다시이 인덱싱되므로 hello hello blob의 기준으로 blob의 경우 변경 된 `LastModified` 타임 스탬프입니다.

> [!NOTE]
> 없는 toospecify 변경 검색 정책 – 증분에 인덱싱이 사용 하면 자동으로 합니다.

toosupport 삭제 문서, "일시 삭제" 접근 방식을 사용 합니다. 완전 한 hello blob을 삭제 하면 해당 문서 hello 검색 인덱스에서 제거 되지 않습니다. 대신, 단계를 수행 하는 hello를 사용 합니다.  

1. 사용자 지정 메타 데이터 속성 toohello blob tooindicate tooAzure 논리적으로 삭제 하는 검색 추가
2. 소프트 삭제 검색 정책을 hello 데이터 원본에 대해 구성
3. Hello blob (같이 hello 인덱서 상태 API)를 처리 하는 hello 인덱서 나면 hello blob를 물리적으로 삭제할 수 있습니다.

Hello 정책에 따라 메타 데이터 속성 항목이 있을 경우 삭제할 blob toobe를 고려 하는 예를 들어 `IsDeleted` hello 값을 가진 `true`:

    PUT https://[service name].search.windows.net/datasources/blob-datasource?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "my-container", "query" : "my-folder" },
        "dataDeletionDetectionPolicy" : {
            "@odata.type" :"#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",     
            "softDeleteColumnName" : "IsDeleted",
            "softDeleteMarkerValue" : "true"
        }
    }   

## <a name="indexing-large-datasets"></a>큰 데이터 집합 인덱싱

BLOB 인덱싱은 시간이 오래 걸리는 프로세스입니다. Blob tooindex 수많은 있는 경우, 데이터를 분할 하 고 동시에 여러 인덱서 tooprocess hello 데이터를 사용 하 여 인덱싱 업데이트 속도 높일 수 있습니다. 설정 방법은 다음과 같습니다.

- 데이터를 여러 BLOB 컨테이너 또는 가상 폴더로 분할합니다.
- Azure Search 데이터 원본을 컨테이너 또는 폴더당 하나씩 여러 개 설정합니다. toopoint tooa blob 폴더를 사용 하 여 hello `query` 매개 변수:

    ```
    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "my-container", "query" : "my-folder" }
    }
    ```

- 각 데이터 소스에 해당하는 인덱서를 만듭니다. 인덱서 수 지점 toohello hello 모두 동일한 대상 검색 인덱스입니다.  

- 서비스에서 하나의 검색 단위가 지정된 시점에 하나의 인덱서를 실행할 수 있습니다. 위에서 설명한 대로 여러 인덱서를 만들면 실제 병렬로 실행하는 경우에 유용합니다. toorun 병렬로, 여러 인덱서가 확장할 검색 서비스는 적절 한 개수의 파티션과 복제본을 만들어 합니다. 예를 들어 검색 서비스 6 검색 단위 (예를 들어 파티션 2 개로 x 3 복제본)가 있으면 다음 6 인덱서 동시에 실행할 수, 인덱싱 처리량을 hello six-fold 향상에서으로 인해 발생 합니다. 확장 및 용량 계획에 대해 자세히 toolearn 참조 [확장 쿼리 및 인덱싱 Azure 검색에서 워크 로드에 대 한 리소스 수준](search-capacity-planning.md)합니다.

## <a name="indexing-documents-along-with-related-data"></a>관련된 데이터와 함께 문서 인덱싱

너무 "조합" 문서를 인덱스에서 여러 원본의 할 수 있습니다. 예를 들어 blob에서 toomerge 텍스트를 Cosmos DB에 저장 된 다른 메타 데이터와 좋습니다. 다양 한 인덱서 함께 푸시 인덱싱 API 너무 여러 부분에서 검색 문서를 작성 하는 hello도 사용할 수 있습니다. 

이 toowork 인덱서 모두 및 기타 구성 요소 tooagree hello 문서 키에 필요합니다. 자세한 연습은 이 외부 아티클 [Azure Search의 다른 데이터와 문서 결합](http://blog.lytzen.name/2017/01/combine-documents-with-other-data-in.html)을 참조하세요.

<a name="IndexingPlainText"></a>
## <a name="indexing-plain-text"></a>일반 텍스트 인덱싱 

경우에 일반 텍스트를 포함 하는 blob 모두 같은 인코딩을 hello, 크게 향상 시킬 수 있습니다 인덱싱 성능을 사용 하 여 **텍스트 모드를 구문 분석**합니다. toouse 텍스트 모드에서 집합 hello를 구문 분석 `parsingMode` 구성 속성이 너무`text`:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "parsingMode" : "text" } }
    }

기본적으로 hello `UTF-8` 인코딩으로 간주 됩니다. 다른 인코딩을 toospecify hello를 사용 하 여 `encoding` 구성 속성: 

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "parsingMode" : "text", "encoding" : "windows-1252" } }
    }


<a name="ContentSpecificMetadata"></a>
## <a name="content-type-specific-metadata-properties"></a>콘텐츠 형식별 메타데이터 속성
hello 다음 표에 요약 각 문서 형식에 대해 수행 된 처리가 하 고 Azure 검색에서 추출 된 hello 메타 데이터 속성에 설명 합니다.

| 문서 형식/콘텐츠 형식 | 콘텐츠 형식별 메타데이터 속성 | 처리 세부 정보 |
| --- | --- | --- |
| HTML(`text/html`) |`metadata_content_encoding`<br/>`metadata_content_type`<br/>`metadata_language`<br/>`metadata_description`<br/>`metadata_keywords`<br/>`metadata_title` |HTML 태그를 제거하고 텍스트 추출 |
| PDF(`application/pdf`) |`metadata_content_type`<br/>`metadata_language`<br/>`metadata_author`<br/>`metadata_title` |포함된 문서를 비롯한 텍스트 추출(이미지 제외) |
| DOCX(application/vnd.openxmlformats-officedocument.wordprocessingml.document) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_character_count`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_page_count`<br/>`metadata_word_count` |포함된 문서를 비롯한 텍스트 추출 |
| DOC(application/msword) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_character_count`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_page_count`<br/>`metadata_word_count` |포함된 문서를 비롯한 텍스트 추출 |
| XLSX(application/vnd.openxmlformats-officedocument.spreadsheetml.sheet) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified` |포함된 문서를 비롯한 텍스트 추출 |
| XLS(application/vnd.ms-excel) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified` |포함된 문서를 비롯한 텍스트 추출 |
| PPTX(application/vnd.openxmlformats-officedocument.presentationml.presentation) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_slide_count`<br/>`metadata_title` |포함된 문서를 비롯한 텍스트 추출 |
| PPT(application/vnd.ms-powerpoint) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_slide_count`<br/>`metadata_title` |포함된 문서를 비롯한 텍스트 추출 |
| MSG(application/vnd.ms-outlook) |`metadata_content_type`<br/>`metadata_message_from`<br/>`metadata_message_to`<br/>`metadata_message_cc`<br/>`metadata_message_bcc`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_subject` |첨부 파일을 비롯한 텍스트 추출 |
| ZIP(application/zip) |`metadata_content_type` |Hello 보관 파일의 모든 문서에서 텍스트를 추출 합니다. |
| XML(application/xml) |`metadata_content_type`</br>`metadata_content_encoding`</br> |XML 태그를 제거하고 텍스트 추출 |
| JSON(application/json) |`metadata_content_type`</br>`metadata_content_encoding` |텍스트 추출<br/>참고: tooextract 여러 문서 필드 JSON blob에서 해야 할 경우 참조 [JSON 인덱싱 blob](search-howto-index-json-blobs.md) 대 한 자세한 내용은 |
| EML(메시지/rfc822) |`metadata_content_type`<br/>`metadata_message_from`<br/>`metadata_message_to`<br/>`metadata_message_cc`<br/>`metadata_creation_date`<br/>`metadata_subject` |첨부 파일을 비롯한 텍스트 추출 |
| RTF(application/rtf) |`metadata_content_type`</br>`metadata_author`</br>`metadata_character_count`</br>`metadata_creation_date`</br>`metadata_page_count`</br>`metadata_word_count`</br> | 텍스트 추출|
| 일반 텍스트(text/plain) |`metadata_content_type`</br>`metadata_content_encoding`</br> | 텍스트 추출|


## <a name="help-us-make-azure-search-better"></a>Azure Search 개선 지원
요청할 기능이 있거나 개선을 위한 아이디어가 있는 경우 [UserVoice 사이트](https://feedback.azure.com/forums/263029-azure-search/)를 통해 알려주세요.
