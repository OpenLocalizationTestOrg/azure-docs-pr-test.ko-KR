---
title: "Azure CDN에서 파일 압축 aaaTroubleshooting | Microsoft Docs"
description: "Azure CDN 파일 압축과 관련된 문제를 해결합니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: a6624e65-1a77-4486-b473-8d720ce28f8b
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f00b98beaf6b3b3cd30108ece65a8191edc06ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-file-compression"></a>CDN 파일 압축 문제 해결
이 문서는 [CDN 파일 압축](cdn-improve-performance.md)관련 문제를 해결하는 데 도움이 됩니다.

이 문서에서 언제 든 지 자세한 도움말을 보려는 경우 문의할 수 있습니다에 Azure 전문가 hello [MSDN Azure hello 및 스택 오버플로 포럼 hello](https://azure.microsoft.com/support/forums/)합니다. 또는 Azure 기술 지원 인시던트를 제출할 수도 있습니다. Toohello 이동 [Azure 지원 사이트](https://azure.microsoft.com/support/options/) 클릭 **Get Support**합니다.

## <a name="symptom"></a>증상
끝점에 대한 압축이 활성화되어 있지만 파일이 압축되지 않은 상태로 반환됩니다.

> [!TIP]
> toocheck 파일 반환 되는 압축 된, toouse 도구와 같은 필요한 [Fiddler](http://www.telerik.com/fiddler) 또는 브라우저의 [개발자 도구](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/)합니다.  검사 hello HTTP 응답 헤더와 함께 반환 캐시 된 CDN 콘텐츠입니다.  명명된 `Content-Encoding` 헤더에 **gzip**, **bzip2** 또는 **deflate** 값이 있는 경우 콘텐츠가 압축된 것입니다.
> 
> ![Content-Encoding 헤더](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a>원인
몇 가지 가능한 원인은 다음과 같습니다.

* hello 요청 콘텐츠는 압축에 적합 하지 않습니다.
* 압축 hello를 사용 하지 않는 요청 된 파일 형식입니다.
* hello HTTP 요청에 유효한 압축 유형 요청 헤더를 포함 되지 않았습니다.

## <a name="troubleshooting-steps"></a>문제 해결 단계
> [!TIP]
> 새 끝점을 배포할 때와 CDN 구성 변경은 몇 시간 toopropagate hello 네트워크를 통해.  일반적으로 변경 내용은 90분 이내에 적용됩니다.  인 경우 hello 처음으로 CDN 끝점에 대 한 압축을 설정 했으면 1 ~ 2 시간 toobe hello 압축 설정을 toohello Pop 전파 되었는지 대기 하는 것이 좋습니다. 
> 
> 

### <a name="verify-hello-request"></a>Hello 요청 확인
첫째, hello 요청에 대 한 빠른 온전성 검사를 수행 해야 합니다.  브라우저의을 사용할 수 있습니다 [개발자 도구](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview hello 전송 되는 요청입니다.

* Hello 요청 tooyour 끝점 URL 보내는 확인 `<endpointname>.azureedge.net`, 및 원본 되지 않습니다.
* Hello 요청에 포함 되어 확인는 **Accept-encoding** 머리글과 hello 값에 해당 헤더에 포함 되어 **gzip**, **deflate**, 또는 **bzip2** .

> [!NOTE]
> **Akamai의 Azure CDN** 프로필은 **gzip** 인코딩만 지원합니다.
> 
> 

![CDN 요청 헤더](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a>압축 설정 확인(Standard CDN 프로필)
> [!NOTE]
> 이 단계는 CDN 프로필이 **Verizon의 Azure CDN Standard** 또는 **Akamai의 Azure CDN Standard** 프로필인 경우에만 적용됩니다. 
> 
> 

Hello에 tooyour 끝점 이동 [Azure 포털](https://portal.azure.com) hello 클릭 **구성** 단추입니다.

* 압축이 활성화되어 있는지 확인합니다.
* 콘텐츠 압축 toobe 압축 된 형식의 hello 목록에 포함 되어 hello에 대 한 hello MIME 형식을 확인 합니다.

![CDN 압축 설정](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a>압축 설정 확인(Premium CDN 프로필)
> [!NOTE]
> 이 단계는 CDN 프로필이 **Verizon의 Azure CDN Premium** 프로필인 경우에만 적용됩니다.
> 
> 

Hello에 tooyour 끝점 이동 [Azure 포털](https://portal.azure.com) hello 클릭 **관리** 단추입니다.  hello 보조 포털이 열립니다.  마우스 포인터를 놓고 hello **HTTP 큰** 누른 마우스 포인터를 놓고 hello **캐시 설정** 플라이 아웃입니다.  **압축**을 클릭합니다. 

* 압축이 활성화되어 있는지 확인합니다.
* Hello 확인 **파일 형식을** 목록 MIME 형식 (공백 없이)는 쉼표로 구분 된 목록에 포함 되어 있습니다.
* 콘텐츠 압축 toobe 압축 된 형식의 hello 목록에 포함 되어 hello에 대 한 hello MIME 형식을 확인 합니다.

![CDN 프리미엄 압축 설정](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-hello-content-is-cached"></a>Hello 콘텐츠가 캐시 되 고 확인 합니다.
> [!NOTE]
> 이 단계는 CDN 프로필이 **Verizon의 Azure CDN** 프로필(Standard 또는 Premium)인 경우에만 적용됩니다.
> 
> 

브라우저의 개발자 도구를 사용 하 여 hello 응답 헤더 tooensure hello 파일 요청 되는 hello 지역에 캐시 된 확인 합니다.

* Hello 확인 **서버** 응답 헤더입니다.  hello 헤더에는 hello 형식 있어야 **플랫폼 (POP/서버 ID)**hello 다음 예제와 같이, 합니다.
* Hello 확인 **X 캐시** 응답 헤더입니다.  hello 헤더를 읽어야 **적중**합니다.  

![CDN 응답 헤더](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-hello-file-meets-hello-size-requirements"></a>Hello 파일 hello 크기 요구 사항을 충족 하는지 확인
> [!NOTE]
> 이 단계는 CDN 프로필이 **Verizon의 Azure CDN** 프로필(Standard 또는 Premium)인 경우에만 적용됩니다.
> 
> 

압축에 적합 toobe, 파일 크기 요구 사항을 준수 하는 hello를 충족 해야 합니다.

* 128바이트 초과.
* 1MB 미만.

### <a name="check-hello-request-at-hello-origin-server-for-a-via-header"></a>Hello 요청에 대 한 hello 원본 서버에서 확인 한 **통해** 헤더
hello **통해** HTTP 헤더는 프록시 서버에 의해 전달 되 고 요청 hello toohello 웹 서버를 나타냅니다.  기본적으로 Microsoft IIS 웹 서버 hello 요청에 포함 되어 있으면 응답을 압축 하지 않습니다는 **통해** 헤더입니다.  toooverride이이 동작을 hello 다음을 수행 합니다.

* **IIS 6**: [설정 HcNoCompressionForProxies hello IIS 메타 베이스 속성에서 = "FALSE"](https://msdn.microsoft.com/library/ms525390.aspx)
* **IIS 7 이상**: [모두 설정 **noCompressionForHttp10** 및 **noCompressionForProxies** tooFalse hello 서버 구성](http://www.iis.net/configreference/system.webserver/httpcompression)

