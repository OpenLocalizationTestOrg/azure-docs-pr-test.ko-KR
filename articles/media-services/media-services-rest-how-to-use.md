---
title: "Media Services Operations REST API 개요 | Microsoft Docs"
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
ms.openlocfilehash: eada8f2bcd2488d5ed36b0c24aa3d1b917815517
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="media-services-operations-rest-api-overview"></a>Media Services Operations REST API 개요
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

**Media Services Operations REST** API는 미디어 서비스 계정에서 작업, 자산, 액세스 정책 작성 및 개체에 대한 다른 작업에 사용됩니다. 자세한 내용은 [Media Services Operations REST API 참조](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)를 참조하세요.

Microsoft Azure 미디어 서비스는 OData 기반의 HTTP 요청을 허용하는 서비스이며 verbose JSON 또는 atom + pub 형식으로 다시 응답할 수 있습니다. 미디어 서비스는 Azure의 설계 지침을 따르기 때문에 미디어 서비스에 연결할 때 각 클라이언트가 사용해야 하는 필수 HTTP 헤더 집합뿐만 아니라 선택적 헤더로 사용할 수 있는 집합도 있습니다. 다음 섹션에서는 요청을 작성하고 미디어 서비스에서 응답을 수신할 때 사용할 수는 헤더 및 HTTP 동사를 설명합니다.

이 항목에서는 Media Services에서 REST v2를 사용하는 방법에 대한 개요를 제공합니다.

## <a name="considerations"></a>고려 사항

REST를 사용할 때 적용되는 고려 사항은 다음과 같습니다.

* 엔터티를 쿼리할 때 한 번에 반환되는 엔터티 수는 최대 1000개입니다. 공용 REST v2에서는 쿼리 결과를 1000개로 제한하기 때문입니다. [이 .NET 예제](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) 및 [이 REST API 예제](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities)에 설명된 대로 **Skip** 및 **Take**(.NET)/**top**(REST)을 사용해야 합니다. 
* JSON을 사용하고 요청(예: 연결된 개체 참조)에서 **__metadata** 키워드를 사용하도록 지정할 때 **Accept** 헤더를 [JSON 자세한 정보 표시 형식](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/)(아래 예제 참조)으로 설정해야 합니다. verbose로 설정하지 않으면 Odata에서 **__metadata** 속성을 인식하지 못합니다.  
  
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
미디어 서비스에서 작성한 모든 호출에는 귀하의 요청에 포함해야 하는 필수 헤더 집합이 있으며 포함할 수도 있는 선택적 헤더 집합도 있습니다. 필수 헤더는 다음 표에 나와 있습니다.

| 헤더 | 형식 | 값 |
| --- | --- | --- |
| 권한 부여 |전달자 |전달자는 승인된 유일한 권한 부여 메커니즘입니다. 이 값은 ACS에서 제공한 액세스 토큰도 포함해야 합니다. |
| x-ms-version |10진수 |2.11 |
| DataServiceVersion |10진수 |3.0 |
| MaxDataServiceVersion |10진수 |3.0 |

> [!NOTE]
> 미디어 서비스는 OData를 사용하여 REST API를 통해 기본 자산 메타데이터 리포지토리를 표시합니다. DataServiceVersion과 MaxDataServiceVersion 헤더는 모든 요청에 포함되어야 합니다. 그러나 그렇지 않은 경우 현재 미디어 서비스는 사용 중인 DataServiceVersion 값이 3.0이라고 가정합니다.
> 
> 

다음은 선택적 헤더의 집합입니다.

| 헤더 | 형식 | 값 |
| --- | --- | --- |
| Date |RFC 1123 날짜 |요청 타임스탬프 |
| 수락 |콘텐츠 형식 |다음과 같은 응답에 대해 요청된 콘텐츠 형식:<p> -application/json;odata=verbose<p> - application/atom+xml<p> blob 인출과 같이 다른 콘텐츠 유형이 응답에 있을 수 있습니다. 여기서 성공적인 응답은 blob 스트림을 페이로드로 포함합니다. |
| Accept-Encoding |Gzip, deflate |GZIP 및 DEFLATE 인코딩, 해당되는 경우입니다. 참고: 큰 리소스의 경우 미디어 서비스는 이 헤더를 무시하고 압축되지 않은 데이터를 반환할 수 있습니다. |
| Accept-Language |"en", "es" 등입니다. |응답에 대한 기본 언어를 지정합니다. |
| Accept-Charset |"UTF-8"과 같은 문자 집합 유형 |기본값은 UTF-8입니다. |
| X-HTTP-Method |HTTP 메서드 |PUT 또는 DELETE와 같이 HTTP 메서드를 지원하지 않는 클라이언트나 방화벽이 GET 호출을 통해 터널링된 이러한 메서드를 사용하도록 허용합니다. |
| 콘텐츠 형식 |콘텐츠 형식 |PUT 또는 POST 요청에서 요청 본문의 콘텐츠 형식입니다. |
| client-request-id |String |지정된 요청을 식별하는 호출자 정의 값입니다. 지정된 경우 이 값은 요청을 매핑하는 방법으로 응답 메시지에 포함됩니다. <p><p>**중요**<p>값은 2096b(2k)에서 제한되어야 합니다. |

## <a name="standard-http-response-headers-supported-by-media-services"></a>미디어 서비스에서 지원되는 표준 HTTP 응답 헤더
다음은 요청한 리소스 및 수행하려는 작업에 따라 사용자에게 반환될 수 있는 헤더 집합입니다.

| 헤더 | 형식 | 값 |
| --- | --- | --- |
| request-id |String |현재 작업에 대한 고유 식별자로 서비스를 생성합니다. |
| client-request-id |String |호출자가 원래 요청을 통해 지정한 식별자입니다(있는 경우). |
| Date |RFC 1123 날짜 |요청이 처리된 날짜입니다. |
| 콘텐츠 형식 |다름 |응답 본문의 콘텐츠 형식입니다. |
| Content-Encoding |다름 |Gzip 또는 deflate를 적절하게 합니다. |

## <a name="standard-http-verbs-supported-by-media-services"></a>미디어 서비스에서 지원되는 표준 HTTP 동사
다음은 HTTP 요청을 만들 때 사용할 수 있는 HTTP 동사의 전체 목록입니다.

| 동사 | 설명 |
| --- | --- |
| GET |개체의 현재 값을 반환합니다. |
| POST |제공된 데이터를 기반으로 개체를 만들거나 명령을 제출합니다. |
| PUT |개체를 바꾸거나 명명된 개체(있는 경우)를 만듭니다. |
| 삭제 |개체를 삭제합니다. |
| MERGE |명명된 속성 변경 내용으로 기존 개체를 업데이트합니다. |
| HEAD |GET 응답에 대한 개체의 메타데이터를 반환합니다. |

## <a name="discover-media-services-model"></a>Media Services 모델 검색
미디어 서비스 엔터티를 더 쉽게 검색할 수 있게 되면 $metadata 작업을 사용할 수 있습니다. 유효한 모든 엔터티 형식, 엔터티 속성, 연결, 함수, 동작 등을 검색할 수 있습니다. 다음 예제는 URI https://media.windows.net/API/$metadata를 생성하는 방법을 보여 줍니다.

브라우저에서 메타데이터를 보려면 "? api version=2.x"를 URI의 끝에 추가하거나 귀하의 요청에 x-ms-version 헤더를 포함하지 말아야 합니다.

## <a name="connect-to-media-services"></a>미디어 서비스에 연결

AMS API에 연결하는 방법에 대한 자세한 내용은 [Azure AD 인증을 사용하여 Azure Media Services API 액세스](media-services-use-aad-auth-to-access-ams-api.md)를 참조하세요. https://media.windows.net에 연결하면 다른 미디어 서비스 URI를 지정하는 301 리디렉션을 받게 됩니다. 사용자는 새 URI에 대한 후속 호출을 해야 합니다.

## <a name="next-steps"></a>다음 단계

REST를 사용하여 AMS API에 액세스하려면 [Azure AD 인증을 사용하여 REST로 Azure Media Services API 액세스](media-services-rest-connect-with-aad.md)를 참조하세요.

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

