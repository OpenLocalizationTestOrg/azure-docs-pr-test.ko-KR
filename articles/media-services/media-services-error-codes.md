---
title: "미디어 서비스 오류 코드 aaaAzure | Microsoft Docs"
description: "hello 항목에서는 Azure 미디어 서비스 오류 코드에 대 한 개요를 제공 합니다."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d3a62a64-7608-4b17-8667-479b26ba0d6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: de1ffd6dee8901a3051eb5032536c3669482d6b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-error-codes"></a>Azure Media Services 오류 코드
Microsoft Azure 미디어 서비스를 사용할 때는 만료 tooactions 미디어 서비스에서 지원 되지 않는 인증 토큰 등의 문제에 따라 hello 서비스에서 HTTP 오류 코드를 나타날 수 있습니다. hello 다음은 목록이 **HTTP 오류 코드** hello 가능한 원인은 해당 및 미디어 서비스에 의해 반환 될 수 있습니다.  

## <a name="400-bad-request"></a>400 잘못된 요청
hello 요청에 잘못 된 정보가 및 due 거부 되 hello 이유 뒤의 tooone:

* 지원되지 않는 API 버전이 지정되었습니다. Hello 가장 최신 버전을 참조 하십시오. [미디어 서비스 REST API 개발 설정](media-services-rest-how-to-use.md)합니다.
* 미디어 서비스의 hello API 버전을 지정 하지 않았습니다. Toospecify API 버전을 hello 하는 방법에 대 한 정보를 참조 하십시오. [미디어 서비스 REST API 참조 작업](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)합니다.
  
  > [!NOTE]
  > .NET 또는 Java Sdk tooconnect tooMedia hello를 사용 하는 경우, hello API 버전은 지정 된 서비스를 시도 하 고 미디어 서비스에 대해 일부 작업을 수행할 때마다 합니다.
  > 
  > 
* 정의되지 않은 속성이 지정되었습니다. hello 속성 이름이 hello 오류 메시지입니다. 지정된 엔터티의 구성 요소인 속성 만이 지정될 수 있습니다. 엔터티 및 해당 속성의 목록은 [Azure Media Services REST API 참조](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)를 참조하세요.
* 잘못된 속성 값이 지정되었습니다. hello 속성 이름이 hello 오류 메시지입니다. 잘못 된 속성 형식에 대 한 이전 연결이 hello 및 해당 값을 참조 하십시오.
* 필수 속성 값이 누락되었습니다.
* 지정 된 hello URL의 일부 잘못 된 값을 포함 합니다.
* 시도 된 tooupdate WriteOnce 속성을 적용 합니다.
* 시도 된 toocreate 입력된 자산을 지정 하지 않았거나 확인할 수 있는 기본 AssetFile 가진 작업을 수행 합니다.
* 시도 된 tooupdate SAS 로케이터를 수행 합니다. SAS Locator는 생성 또는 삭제만 될 수 있습니다. 스트리밍 로케이터는 업데이트될 수 있습니다. 자세한 내용은 [Locators](https://docs.microsoft.com/rest/api/media/operations/locator)를 참조하세요.
* 지원되지 않는 작업 또는 쿼리가 제출되었습니다.

## <a name="401-unauthorized"></a>401 권한 없음
(권한을 부여할 수) 전에 hello 요청을 인증할 수 없는 이유 뒤 hello의 due tooone:

* 누락된 인증 헤더입니다.
* 잘못된 인증 헤더 값입니다.
  * hello 토큰이 만료 되었습니다. 
  * hello 토큰에 잘못 된 서명이 있습니다.

## <a name="403-forbidden"></a>403 사용할 수 없음
hello 요청 due 허용 되지 않습니다 hello 이유 뒤의 tooone:

* hello 미디어 서비스 계정 없거나 삭제 되었습니다.
* hello 미디어 서비스 계정을 사용할 수 없게 되어 hello 요청 유형이 아니면 HTTP GET 합니다. 서비스 작업은 또한 403 응답을 반환합니다.
* hello 인증 토큰에 포함 되지 hello 사용자의 자격 증명 정보: AccountName 및/또는 구독 Id입니다. Hello Azure 관리 포털에서에서 미디어 서비스 계정에 대 한 hello 미디어 서비스 UI 확장 프로그램에서에서이 정보를 찾을 수 있습니다.
* hello 리소스를 액세스할 수 없습니다.
  
  * 시도 된 미디어 서비스 계정에 대해 사용할 수 없는 MediaProcessor toouse를 수행 합니다.
  * JobTemplate 정의 tooupdate 미디어 서비스에 의해 시도 했습니다.
  * 시도 된 toooverwrite 일부 다른 미디어 서비스 계정의 로케이터를 수행 합니다.
  * 시도 된 toooverwrite 다른 미디어 서비스 계정을 ContentKey를 수행 합니다.
* hello 미디어 서비스 계정에도 달했기 tooa 서비스 할당량 인해 hello 리소스를 만들 수 없습니다. Hello 서비스 할당량에 대 한 자세한 내용은 참조 하십시오. [할당량 및 제한](media-services-quotas-and-limitations.md)합니다.

## <a name="404-not-found"></a>404 찾을 수 없음
hello 요청 된 리소스에서 허용 되지 않습니다 hello 이유 뒤의 due tooone:

* 시도 된 tooupdate 존재 하지 않는 엔터티를 수행 합니다.
* 시도 된 toodelete 존재 하지 않는 엔터티를 수행 합니다.
* 시도 된 toocreate 존재 하지 않는 tooan 엔터티에 링크 하는 엔터티를 수행 합니다.
* 시도 된 tooGET 존재 하지 않는 엔터티를 수행 합니다.
* 시도 실패 한 toospecify hello 미디어 서비스 계정으로 연결 되지 않은 저장소 계정을 적용 합니다.  

## <a name="409-conflict"></a>409 충돌
hello 요청 due 허용 되지 않습니다 hello 이유 뒤의 tooone:

* 둘 이상의 AssetFile hello hello 자산 내에서 지정 된 이름을 있습니다.
* 시도한 경우를 두 번째로 toocreate 기본 AssetFile hello 자산 내에서.
* 했습니다 toocreate hello로 ContentKey 이미 사용 되는 Id를 지정 합니다.
* 했습니다 toocreate hello로 로케이터 이미 사용 되는 Id를 지정 합니다.
* 둘 이상의 IngestManifestFile hello hello IngestManifest 내에서 지정 된 이름을 있습니다.
* 시도 된 toolink 두 번째 저장소 암호화 ContentKey toohello 수행 자산 저장소를 암호화 합니다.
* 했습니다 toolink hello 동일한 ContentKey toohello 자산입니다.
* Toocreate 자산 hello와 연결 된 로케이터 tooan 자산 인 저장소 컨테이너 누락 되었거나 더 이상 시도 했습니다.
* 시도 된 로케이터 tooan 5 로케이터에에서 이미 사용 하는 자산의 toocreate를 수행 합니다. (Azure 저장소에는 하나의 저장소 컨테이너에 5 개의 공유 액세스 정책 hello 제한을 적용 합니다.)
* Hello 부모 IngestManifest에 의해 사용 되는 hello 저장소 계정과 동일한 hello 않습니다 자산 tooan IngestManifestAsset의 저장소 계정을 연결 합니다.  

## <a name="500-internal-server-error"></a>500 내부 서버 오류
Hello 요청의 hello 처리 하는 동안 미디어 서비스는 hello 처리를 계속할 수 없는 몇 가지 오류가 발생 합니다. 때문일 수 있습니다 hello 이유 뒤의 tooone:

* 자산을 만들거나 작업 hello 미디어 서비스 계정 서비스 할당량 정보를 일시적으로 사용할 수 없기 때문에 실패 합니다.
* 자산 또는 IngestManifest blob 저장소 컨테이너를 만드는 hello 계정의 저장소 계정 정보를 일시적으로 사용할 수 없기 때문에 실패 합니다.
* 기타 예기치 않은 오류.

## <a name="503-service-unavailable"></a>503 서비스를 사용할 수 없음
hello 서버는 현재 없습니다 tooreceive 요청입니다. 이 오류는 과도 한 요청을 toohello 서비스에 의해 발생할 수 있습니다. 미디어 서비스 제한 메커니즘 toohello 서비스 과도 하 게 요청 하는 응용 프로그램에 대 한 hello 리소스 사용량을 제한 합니다.

> [!NOTE]
> 검사 hello 오류 메시지 및 오류 코드 문자열 tooget 가져온 hello 이유 대 한 자세한 정보와 hello 503 오류가 있습니다. 이 오류가 항상 제한을 의미하지는 않습니다.
> 
> 

가능한 상태 설명은 다음과 같습니다.

* "서버가 사용 중입니다. 이 유형의 요청은 이전에 실행되었을 때 {0}초 이상 걸렸습니다."
* "서버가 사용 중입니다. 초당 요청이 {0} 개보다 많을 경우 제한될 수 있습니다."
* "서버가 사용 중입니다. {1}초 내에 {0}요청보다 많을 경우 제한될 수 있습니다."

toohandle이이 오류를 사용할 수 있는 권장 지 수 백오프 재시도 논리입니다. 연속된 오류 응답에 대해 재시도 간에 점진적으로 더 긴 대기 시간을 두는 것을 의미합니다.  자세한 내용은 [일시적인 오류 처리 응용 프로그램 블록(영문)](https://msdn.microsoft.com/library/hh680905.aspx)을 참조하세요.

> [!NOTE]
> 사용 중인 경우 [Azure Media Services SDK for.Net](https://github.com/Azure/azure-sdk-for-media-services/tree/master), hello SDK 여 hello 503 오류에 대 한 hello 재시도 논리 구현 되었습니다.  
> 
> 

## <a name="see-also"></a>참고 항목
[Media Services 관리 오류 코드](http://msdn.microsoft.com/library/windowsazure/dn167016.aspx)

## <a name="next-steps"></a>다음 단계
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

