---
title: "Azure 미디어 서비스 REST API를 사용 하 여 aaaCreating 필터 | Microsoft Docs"
description: "이 항목에서는 클라이언트 toostream 스트림의 특정 섹션 사용할 수 있도록 toocreate 필터링 하는 방법을 설명 합니다. 미디어 서비스 스트리밍이 선택적 tooachieve를 동적 매니페스트를 만듭니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f7d23daf-7cd2-49c7-a195-ab902912ab3c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: d0b5af3b193b35f22ac70887963c2f0a06b60bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-filters-with-azure-media-services-rest-api"></a>Azure 미디어 서비스 REST API로 필터 생성
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-dynamic-manifest.md)
> * [REST (영문)](media-services-rest-dynamic-manifest.md)
> 
> 

2.11 버전부터 미디어 서비스를 사용 하면 자산에 대 한 toodefine 필터. 이러한 필터는 고객에 게 toochoose toodo 등으로 나눌 수 있는 서버 쪽 규칙: 재생 (재생 하지 않고 hello 전체 비디오), 비디오의 섹션만 고객의 장치 (처리할 수 있도록 하는 오디오 및 비디오 변환의 하위 집합을 지정 하거나 모든 hello 변환 하는 대신 연결 된 hello 자산에). 자산의 필터링이 통해 보관 **동적 매니페스트**비디오 고객의 요청 toostream 시 생성 되는 지정 된 필터에 기반 합니다.

자세한 내용을 보려면 관련된 toofilters 및 동적 매니페스트 참조 [동적 매니페스트 개요](media-services-dynamic-manifest-overview.md)합니다.

이 항목에서는 toouse REST Api toocreate이, 업데이트 하 고 필터를 삭제 하는 방법을 보여 줍니다. 

## <a name="types-used-toocreate-filters"></a>Toocreate 필터를 사용 하는 형식
hello 다음 유형은 사용할 필터를 만들 때.  

* [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)
* [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* [FilterTrackSelect 및 FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

>[!NOTE]

>미디어 서비스에서 엔터티에 액세스할 때는 HTTP 요청에서 구체적인 헤더 필드와 값을 설정해야 합니다. 자세한 내용은 [미디어 서비스 REST API 개발 설정](media-services-rest-how-to-use.md)을 참조하세요.

## <a name="connect-toomedia-services"></a>TooMedia 서비스 연결

AMS API를 참조 하는 tooconnect toohello 방법에 대 한 내용은 [Azure AD 인증 액세스 hello Azure 미디어 서비스 API](media-services-use-aad-auth-to-access-ams-api.md)합니다. 

>[!NOTE]
>Toohttps://media.windows.net을 성공적으로 연결한 후 다른 Media Services URI를 지정 하는 301 리디렉션을 받게 됩니다. 후속 호출 toohello 해야 새 URI입니다.

## <a name="create-filters"></a>필터 생성
### <a name="create-global-filters"></a>전역 Filter 생성
필터를 글로벌 필터로 toocreate HTTP 요청을 수행 하는 hello를 사용 합니다.  

#### <a name="http-request"></a>HTTP 요청
요청 헤더

    POST https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host:media.windows.net 

요청 본문 

    {  
       "Name":"GlobalFilter",
       "PresentationTimeRange":{  
          "StartTimestamp":"0",
          "EndTimestamp":"9223372036854775807",
          "PresentationWindowDuration":"12000000000",
          "LiveBackoffDuration":"0",
          "Timescale":"10000000"
       },
       "Tracks":[  
          {  
             "PropertyConditions":
                  [  
                {  
                   "Property":"Type",
                   "Value":"audio",
                   "Operator":"Equal"
                },
                {  
                   "Property":"Bitrate",
                   "Value":"0-2147483647",
                   "Operator":"Equal"
                }
             ]
          }
       ]
    }




#### <a name="http-response"></a>HTTP 응답
    HTTP/1.1 201 Created 

### <a name="create-local-assetfilters"></a>로컬 AssetFilter 생성
로컬 AssetFilter toocreate HTTP 요청을 수행 하는 hello를 사용 합니다.  

#### <a name="http-request"></a>HTTP 요청
요청 헤더

    POST https://media.windows.net/API/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net  

요청 본문 

    {   
       "Name":"AssetFilter", 
       "ParentAssetId":"nb:cid:UUID:536e555d-1500-80c3-92dc-f1e4fdc6c592", 
       "PresentationTimeRange":{   
          "StartTimestamp":"0", 
          "EndTimestamp":"9223372036854775807", 
          "PresentationWindowDuration":"12000000000", 
          "LiveBackoffDuration":"0", 
          "Timescale":"10000000" 
       }, 
       "Tracks":[   
          {   
             "PropertyConditions": 
                  [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 

#### <a name="http-response"></a>HTTP 응답
    HTTP/1.1 201 Created 
    . . . 

## <a name="list-filters"></a>필터 나열
### <a name="get-all-global-filters-in-hello-ams-account"></a>모든 전역 가져오기 **필터**hello AMS 계정에서 s
toolist 필터 HTTP 요청을 수행 하는 hello를 사용 합니다. 

#### <a name="http-request"></a>HTTP 요청
    GET https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

### <a name="get-assetfilters-associated-with-an-asset"></a>자산에 연결된 **AssetFilter**가져오기
#### <a name="http-request"></a>HTTP 요청
    GET https://media.windows.net/API/Assets('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592')/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

### <a name="get-an-assetfilter-based-on-its-id"></a>해당 ID에 따라 **AssetFilter** 가져오기
#### <a name="http-request"></a>HTTP 요청
    GET https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000


## <a name="update-filters"></a>필터 업데이트
사용 하 여 PATCH, PUT 또는 MERGE tooupdate 새 속성 값을 사용 하 여 필터를 합니다.  이 작업에 대한 자세한 내용은 [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx)를 참조하십시오.

필터를 업데이트 하는 경우 스트리밍 끝점 toorefresh hello 규칙에 대 일 분까지 걸릴 수 있으므로 합니다. Hello 콘텐츠가이 필터를 사용 하 여 제공 된 (그리고 캐시 프록시 및 CDN에 캐시 된) 하는 경우 플레이어에서 오류가 발생할 수 있습니다이 필터를 업데이트 합니다. 되기 tooclear hello 캐시 hello 필터를 업데이트 한 후 것이 좋습니다. 이 옵션을 사용할 수 없는 경우에 서로 다른 필터를 사용 하는 것이 좋습니다.  

### <a name="update-global-filters"></a>전역 Filter 업데이트
필터를 글로벌 필터로 tooupdate HTTP 요청을 수행 하는 hello를 사용 합니다. 

#### <a name="http-request"></a>HTTP 요청
헤더 요청: 

    MERGE https://media.windows.net/API/Filters('filterName') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 
    Content-Length: 384

본문 요청: 

    { 
       "Tracks":[   
          {   
             "PropertyConditions": 
             [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 

### <a name="update-local-assetfilters"></a>로컬 AssetFilter 업데이트
로컬 필터 tooupdate HTTP 요청을 수행 하는 hello를 사용 합니다. 

#### <a name="http-request"></a>HTTP 요청
헤더 요청: 

    MERGE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter')  HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

본문 요청: 

    { 
       "Tracks":[   
          {   
             "PropertyConditions": 
             [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 


## <a name="delete-filters"></a>필터 삭제
### <a name="delete-global-filters"></a>전역 Filter 삭제
필터를 글로벌 필터로 toodelete HTTP 요청을 수행 하는 hello를 사용 합니다.

#### <a name="http-request"></a>HTTP 요청
    DELETE https://media.windows.net/api/Filters('GlobalFilter') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 


### <a name="delete-local-assetfilters"></a>로컬 AssetFilter 삭제
로컬 AssetFilter toodelete HTTP 요청을 수행 하는 hello를 사용 합니다.

#### <a name="http-request"></a>HTTP 요청
    DELETE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__LocalFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

## <a name="build-streaming-urls-that-use-filters"></a>필터를 사용하는 스트리밍 URL 작성
Toopublish 및 배달 자산을 확인 하려면 어떻게 해야에 대 한 내용은 [콘텐츠 배달 tooCustomers 개요](media-services-deliver-content-overview.md)합니다.

hello 다음 예제에서는 tooadd tooyour 스트리밍 Url을 필터링 하는 방법

**MPEG DASH** 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

**Apple HLS(HTTP 라이브 스트리밍) V4**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

**Apple HLS(HTTP 라이브 스트리밍) V3**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

**부드러운 스트리밍**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)

    
## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>참고 항목
[동적 매니페스트 개요](media-services-dynamic-manifest-overview.md)

