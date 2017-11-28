---
title: "Azure 검색 blob 인덱서가 있는 CSV aaaIndexing blob | Microsoft Docs"
description: "Azure 검색 tooindex CSV blob 하는 방법에 대해 알아봅니다"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: ed3c9cff-1946-4af2-a05a-5e0b3d61eb25
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 12/15/2016
ms.author: eugenesh
ms.openlocfilehash: f2b1ce824e62c5b3f6155c6e88887897cf1a8eae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-csv-blobs-with-azure-search-blob-indexer"></a>Azure 검색 Blob 인덱서를 사용하여 CSV Blob 인덱싱
기본적으로 [Azure 검색 Blob 인덱서](search-howto-indexing-azure-blob-storage.md) 는 단일 텍스트 청크로 구분된 텍스트 Blob을 구문 분석합니다. 그러나 CSV 데이터를 포함 하는 blob를 사용 하 여 경우가 종종 있습니다 tootreat hello blob의 각 줄을 별도 문서로. 예를 들어 hello 지정한 다음 구분 된 텍스트: 

    id, datePublished, tags
    1, 2016-01-12, "azure-search,azure,cloud" 
    2, 2016-07-07, "cloud,mobile" 

tooparse 경우가 것 2 문서로 각각 포함 된 "id", "datePublished" 및 "tags" 필드입니다.

이 문서는 Azure 검색 blob 인덱서에서 tooparse CSV blob 하는 방법을 배웁니다. 

> [!IMPORTANT]
> 이 기능은 현재 미리 보기 상태입니다. 버전을 사용 하 여 hello REST API 에서만 사용할 수는 **2015-02-28-preview**합니다. 미리 보기 API는 테스트 및 평가 용도로 제공되며 프로덕션 환경에는 사용되지 않는다는 점을 유념하세요. 
> 
> 

## <a name="setting-up-csv-indexing"></a>CSV 인덱싱 설정
tooindex CSV blob를 만들거나 hello로 인덱서 정의 업데이트할 `delimitedText` 모드를 구문 분석:  

    {
      "name" : "my-csv-indexer",
      ... other indexer properties
      "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "firstLineContainsHeaders" : true } }
    }

에 대 한 자세한 내용은 hello 인덱서 API 만들기, 체크 아웃 [인덱서 만들기](search-api-indexers-2015-02-28-preview.md#create-indexer)합니다.

`firstLineContainsHeaders`각 blob의 첫 번째 (비어 있지 않은) 줄 hello 헤더가 포함 되어 있음을 나타냅니다.
Blob는 초기 헤더 줄이 포함 안 함, hello indexer 구성 hello 헤더 지정 해야 합니다. 

    "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } } 

현재 유일한 hello utf-8 인코딩을 지원 됩니다. 또한 쉼표로 hello `','` hello 구분 기호 문자는 지원 합니다. 다른 인코딩 또는 구분 기호에 대한 지원이 필요한 경우 [UserVoice 사이트](https://feedback.azure.com/forums/263029-azure-search)를 통해 알려주세요.

> [!IMPORTANT]
> Hello 구분 된 텍스트 모드에서 Azure 검색을 구문 분석을 사용 하는 경우 데이터 원본의 모든 blob CSV 된다는 것으로 가정 합니다. Toosupport CSV의 혼합을 hello에 CSV가 아닌 blob 동일한 데이터 원본을 주시기에 [UserVoice 사이트](https://feedback.azure.com/forums/263029-azure-search)합니다.
> 
> 

## <a name="request-examples"></a>요청 예제
이 모두 결합, 다음은 hello 전체 페이로드와 예입니다. 

데이터 원본: 

    POST https://[service name].search.windows.net/datasources?api-version=2015-02-28-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "<optional, my-folder>" }
    }   

인덱서:

    POST https://[service name].search.windows.net/indexers?api-version=2015-02-28-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-csv-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } }
    }

## <a name="help-us-make-azure-search-better"></a>Azure Search 개선 지원
기능 또는 향상 된 기능에 대 한 아이디어를 설정한 경우에 게 연락 하세요에 toous 우리의 [UserVoice 사이트](https://feedback.azure.com/forums/263029-azure-search/)합니다.

