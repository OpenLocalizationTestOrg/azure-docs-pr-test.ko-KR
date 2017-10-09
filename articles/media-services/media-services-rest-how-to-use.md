---
title: "aaaMedia 서비스 작업 REST API 개요 | Microsoft Docs"
description: "미디어 서비스 REST API 개요"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a5f1c5e7-ec52-4e26-9a44-d9ea699f68d9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b54f4d9123486d6cae832c9817688b0f3da5b401
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-operations-rest-api-overview"></a>Media Services Operations REST API 개요
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

hello **미디어 서비스 작업 REST** API 미디어 서비스 계정에서 작업, 자산, 액세스 정책 및 개체에 대해 다른 작업을 만드는 데 사용 됩니다. 자세한 내용은 [Media Services Operations REST API 참조](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)를 참조하세요.

Microsoft Azure 미디어 서비스는 OData 기반의 HTTP 요청을 허용하는 서비스이며 verbose JSON 또는 atom + pub 형식으로 다시 응답할 수 있습니다. 미디어 서비스 tooAzure 디자인 지침을 따르는 때문에 사용할 수 있는 옵션 헤더 집합 뿐만 아니라 tooMedia 서비스에 연결할 때 각 클라이언트가 사용 해야 하는 필수 HTTP 헤더 집합이 있습니다. hello 다음 섹션에서는 설명 hello 헤더 및 HTTP 동사를 할 때 사용할 수 있는 요청을 만들고 미디어 서비스에서 응답을 받습니다.

이 항목에서는 방법의 개요를 제공 미디어 서비스 REST v2 toouse 합니다.

## <a name="considerations"></a>고려 사항

hello 고려 사항에 따라 REST를 사용 하는 경우에 적용 됩니다.

* 엔터티를 쿼리할 때 공용 REST v2 쿼리 결과 too1000 결과 제한 하기 때문에 한 번에 반환 된 1000 엔터티 제한이 있습니다. Toouse 해야 **Skip** 및 **걸릴** (.NET) / **top** (REST)에 설명 된 대로 [.NET 예제](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) 및 [이 REST API 예제](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities)합니다. 
* 때 JSON를 사용 하 고 toouse hello 지정 **__metadata** hello를 설정 해야 합니다 (예를 들어 연결된 된 개체 tooreferences) hello 요청에는 키워드 **Accept** 헤더 너무[자세한 JSON 형식 ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/) (다음 예제는 hello 참조). Odata hello를 인식 하지 못하는 **__metadata** tooverbose 설정 하지 않으면 hello에 대 한 속성을 요청 합니다.  
  
        POST https://media.windows.net/API/Jobs HTTP/1.1
        Content-Type: application/json;odata=verbose
        Accept: application/json;odata=verbose
        DataServiceVersion: 3.0
        MaxDataServiceVersion: 3.0
        x-ms-version: 2.11
        Authorization: Bearer <token> 
        Host: media.windows.net
  
        {
            "Name" : "NewTestJob", 
            "InputMediaAssets" : 
                [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aba5356eb-30ff-4dc6-9e5a-41e4223540e7')"}}]
        . . . 

## <a name="standard-http-request-headers-supported-by-media-services"></a>미디어 서비스에서 지원하는 표준 HTTP 요청 헤더
미디어 서비스에는 모든 호출에 대 한 요청에 포함 해야 하는 필수 헤더 집합이 이며 옵션 헤더 집합도 있습니다 합니다 tooinclude 합니다. 다음 테이블 목록 hello hello 헤더 필요 합니다.

| 헤더 | 형식 | 값 |
| --- | --- | --- |
| 권한 부여 |전달자 |전달자는 hello만 권한 부여 메커니즘을 허용 합니다. hello 값도 ACS에서 제공 하는 hello 액세스 토큰을 포함 해야 합니다. |
| x-ms-version |10진수 |2.11 |
| DataServiceVersion |10진수 |3.0 |
| MaxDataServiceVersion |10진수 |3.0 |

> [!NOTE]
> 미디어 서비스 REST Api hello DataServiceVersion 및 MaxDataServiceVersion 헤더를 통해 기본 자산 메타 데이터 리포지토리;는 모든 요청에 포함 되어야 하는 OData tooexpose 사용 하기 때문에 하지만 그러지 않은 경우 다음 현재 미디어 서비스 가정 사용 중인 DataServiceVersion 값 hello 3.0 합니다.
> 
> 

hello 다음은 옵션 헤더 집합도 있습니다.

| 헤더 | 형식 | 값 |
| --- | --- | --- |
| Date |RFC 1123 날짜 |Hello 요청의 타임 스탬프 |
| 수락 |콘텐츠 형식 |hello는 hello 다음과 같은 hello 응답에 대 한 콘텐츠 형식을 요청 했습니다.<p> -application/json;odata=verbose<p> - application/atom+xml<p> 성공적인 응답 hello 페이로드로 hello blob 스트림에 포함 하는 blob 인출 같은 다른 콘텐츠 형식을 응답에 있을 수 있습니다. |
| Accept-Encoding |Gzip, deflate |GZIP 및 DEFLATE 인코딩, 해당되는 경우입니다. 참고: 큰 리소스의 경우 미디어 서비스는 이 헤더를 무시하고 압축되지 않은 데이터를 반환할 수 있습니다. |
| Accept-Language |"en", "es" 등입니다. |Hello 응답에 대 한 hello 기본 설정 언어를 지정합니다. |
| Accept-Charset |"UTF-8"과 같은 문자 집합 유형 |기본값은 UTF-8입니다. |
| X-HTTP-Method |HTTP 메서드 |PUT 또는 DELETE toouse와 같은 HTTP 메서드를 지원 하지 않는 메서드나 클라이언트가 GET 호출을 통해 터널링 된 이러한 메서드를 수 있습니다. |
| 콘텐츠 형식 |콘텐츠 형식 |PUT 또는 POST hello 요청 본문의 콘텐츠 형식을 요청합니다. |
| client-request-id |문자열 |요청 제공 hello를 식별 하는 호출자 정의 값입니다. 를 지정 하는 경우이 값은 방식으로 toomap hello 요청으로 hello 응답 메시지에 포함 됩니다. <p><p>**중요**<p>값은 2096b(2k)에서 제한되어야 합니다. |

## <a name="standard-http-response-headers-supported-by-media-services"></a>미디어 서비스에서 지원되는 표준 HTTP 응답 헤더
hello 다음에는 요청한 hello 리소스에 따라 tooyou 반환 될 수 있으며 hello tooperform 의도 한 동작 하는 헤더 집합이입니다.

| 헤더 | 형식 | 값 |
| --- | --- | --- |
| request-id |문자열 |Hello 현재 작업을 생성 하는 서비스에 대 한 고유 식별자입니다. |
| client-request-id |문자열 |있는 경우 hello 원래 요청에 hello 호출자가 지정 된 식별자입니다. |
| Date |RFC 1123 날짜 |hello 날짜 해당 hello 요청을 처리 했습니다. |
| 콘텐츠 형식 |다름 |hello hello 응답 본문의 콘텐츠 형식입니다. |
| Content-Encoding |다름 |Gzip 또는 deflate를 적절하게 합니다. |

## <a name="standard-http-verbs-supported-by-media-services"></a>미디어 서비스에서 지원되는 표준 HTTP 동사
hello 다음은 HTTP 요청을 수행할 때 사용할 수 있는 HTTP 동사의 전체 목록입니다.

| 동사 | 설명 |
| --- | --- |
| GET |반환 hello 개체의 현재 값입니다. |
| POST |제공 된 hello 데이터를 기반으로 개체를 만들거나 명령을 제출 합니다. |
| PUT |개체를 바꾸거나 명명된 개체(있는 경우)를 만듭니다. |
| 삭제 |개체를 삭제합니다. |
| MERGE |명명된 속성 변경 내용으로 기존 개체를 업데이트합니다. |
| HEAD |GET 응답에 대한 개체의 메타데이터를 반환합니다. |

## <a name="discover-media-services-model"></a>Media Services 모델 검색
toomake 미디어 서비스 엔터티 더 쉽게 검색할 수 hello $metadata 작업을 사용할 수 있습니다. Tooretrieve 허용 모든 유효한 엔터티 유형, 엔터티 속성, 연결, 함수, 작업, 및 등입니다. hello 다음 예제에서는 어떻게 tooconstruct hello URI: https://media.windows.net/API/$ 메타 데이터입니다.

추가 해야 "? api version=2.x" hello tooview hello 메타 데이터 브라우저에서 원하는 또는 요청에 hello x-ms-버전 헤더를 포함 하지 않는 경우 URI의 toohello 끝입니다.

## <a name="connect-toomedia-services"></a>TooMedia 서비스 연결

AMS API를 참조 하는 tooconnect toohello 방법에 대 한 내용은 [Azure AD 인증 액세스 hello Azure 미디어 서비스 API](media-services-use-aad-auth-to-access-ams-api.md)합니다. Toohttps://media.windows.net을 성공적으로 연결한 후 다른 Media Services URI를 지정 하는 301 리디렉션을 받게 됩니다. 후속 호출 toohello 해야 새 URI입니다.

## <a name="next-steps"></a>다음 단계

REST 사용 하 여 AMS Api tooaccess 참조 [사용 하 여 Azure AD 인증 tooaccess hello REST 사용 하 여 Azure 미디어 서비스 API](media-services-rest-connect-with-aad.md)합니다.

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

