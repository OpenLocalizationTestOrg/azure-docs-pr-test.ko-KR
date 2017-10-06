---
title: "404 상태 반환 aaaTroubleshooting Azure CDN 끝점 | Microsoft Docs"
description: "Azure CDN 끝점에서 404 응답 코드 문제를 해결합니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: b588a1eb-ab69-4fc7-ae4d-157c3e46f4a8
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 450bfbd641c869cfd88169a12c4b69819eaa7c26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-endpoints-returning-404-statuses"></a>404 상태를 반환하는 CDN 끝점 문제 해결
이 문서는 404 오류를 반환하는 [CDN 끝점](cdn-create-new-endpoint.md) 관련 문제를 해결하는 데 도움이 됩니다.

이 문서에서 언제 든 지 자세한 도움말을 보려는 경우 문의할 수 있습니다에 Azure 전문가 hello [MSDN Azure hello 및 스택 오버플로 포럼 hello](https://azure.microsoft.com/support/forums/)합니다. 또는 Azure 기술 지원 인시던트를 제출할 수도 있습니다. Toohello 이동 [Azure 지원 사이트](https://azure.microsoft.com/support/options/) 을 클릭할 **Get Support**합니다.

## <a name="symptom"></a>증상
CDN 프로필 및 끝점을 만든 있지만 콘텐츠 toobe hello CDN에서 사용할 수 있는 기가 나타나지 않았습니다.  Tooaccess hello CDN URL을 통해 콘텐츠 HTTP 404 상태 코드를 수신 하려는 사용자입니다. 

## <a name="cause"></a>원인
몇 가지 가능한 원인은 다음과 같습니다.

* hello 파일의 출처가 표시 toohello CDN를 되지 않습니다.
* hello 끝점 잘못 구성 됨, hello 잘못 된 위치에 CDN toolook hello를 발생 시킵니다.
* hello 호스트를 hello CDN에서에서 hello 호스트 헤더를 거부
* hello 끝점에서 CDN hello 전체 시간 toopropagate를 보지 않은

## <a name="troubleshooting-steps"></a>문제 해결 단계
> [!IMPORTANT]
> CDN 끝점을 만든 후 것 바로 됩니다 사용 하기 위해 사용할 수 대로 hello CDN 통해 hello 등록 toopropagate 시간이 걸립니다.  <b>Akamai의 Azure CDN</b> 프로필의 경우, 일반적으로 1분 이내에 전파가 완료됩니다.  <b>Verizon의 Azure CDN</b> 프로필의 경우 일반적으로 90분 이내에 전파가 완료되지만 더 오래 소요될 수도 있습니다.  Hello 단계를 완료 하는 경우이 문서를 계속 받이 있는지 404 응답, 몇 시간 toocheck 지원 티켓을 발행 하기 전에 대기 하는 것이 좋습니다.
> 
> 

### <a name="check-hello-origin-file"></a>Hello 원본 파일을 확인
첫째, hello 확인 해야 원하는 캐시 된 hello 파일 우리의 원본에서 사용할 수 있으며 공개적으로 액세스할 수 있습니다.  브라우저 tooopen In 개인 또는 Incognito 세션에 있는 가장 빠른 방법은 toodo hello 및 직접 toohello 파일을 검색 합니다.  입력 또는 hello URL hello 주소 상자에 붙여 넣습니다 하 고 원하는 hello 파일에서 발생 하는 경우 참조 하기만 됩니다.  예를 들어 toouse에 액세스할 수 있는 Azure 저장소 계정에 있는 파일 하겠습니다 `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`합니다.  볼 수 있듯이 hello 테스트 성공적으로 전달 합니다.

![성공!](./media/cdn-troubleshoot-endpoint/cdn-origin-file.png)

> [!WARNING]
> 이 파일은 공개적으로 사용할 수 있는 경우, 실제로 표시 toousers 네트워크 (가정을 hello이 가장 빠른 hello 및 가장 쉬운 방법은 tooverify 프로그램 파일을 공개적으로 사용할 수, 조직의 일부 네트워크 구성 수 있도록 하는 동안 도 호스팅되는 경우 Azure에서).  하지 않은 모바일 장치가 연결 tooyour 조직의 네트워크 또는 Azure에서 가상 컴퓨터와 같은 외부 위치의 테스트 수, 브라우저를 설정한 경우 최상의 될 것입니다.
> 
> 

### <a name="check-hello-origin-settings"></a>Hello 원본의 설정을 확인 하십시오.
Hello 파일은 공개적으로 사용할 수 있는지 확인 했으므로 이제 인터넷 hello, 우리의 원본의 설정을 확인 해야 합니다.  Hello에 [Azure 포털](https://portal.azure.com)tooyour CDN 프로필을 탐색 하 고 문제를 해결 하는 hello 끝점을 클릭 합니다.  Hello 결과에서 **끝점** 블레이드에서 hello 원본을 클릭 합니다.  

![원본이 강조 표시된 끝점 블레이드](./media/cdn-troubleshoot-endpoint/cdn-endpoint.png)

hello **원점** 블레이드 나타납니다. 

![원본 블레이드](./media/cdn-troubleshoot-endpoint/cdn-origin-settings.png)

#### <a name="origin-type-and-hostname"></a>원본 유형 및 호스트 이름
Hello 확인 **원본 형식을** 올바르며 hello 확인은 **원본 호스트 이름을**합니다.  예제에서는 `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`, URL은 hello의 호스트 이름 부분 hello `cdndocdemo.blob.core.windows.net`합니다.  이 올바른 hello 스크린 샷에서 볼 수 있습니다.  Azure 저장소, 웹 앱 및 클라우드 서비스 origin, hello **원본 호스트 이름을** 필드 이므로 드롭다운을 올바르게 맞춤법 검사에 대 한 tooworry 필요 하지 않습니다.  그러나 사용자 지정 원본을 사용하는 경우 *반드시* 호스트 이름 철자를 올바르게 입력해야 합니다.

#### <a name="http-and-https-ports"></a>HTTP 및 HTTPS 포트
hello 여기 다른 사항은 toocheck은 프로그램 **HTTP** 및 **HTTPS 포트**합니다.  대부분의 경우 80 및 443이 올바르며, 포트를 변경할 필요가 없습니다.  그러나 hello 원본 서버가 다른 포트에서 수신 하는 경우 여기 toobe가 필요 합니다입니다.  확실 하지 않은 경우 원본 파일에 대 한 hello URL에서 찾으면 됩니다.  hello HTTP 및 HTTPS 사양 hello 기본적으로 포트 80 및 443을 지정합니다. 내 URL에 `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`, 포트를 지정 하지 않으면 하므로 설정은 하 고 hello 443 기본값이 지정 됩니다.  

그러나 예를 들어 hello URL 이전 테스트를 거친 원본 파일에 대 한 `http://www.contoso.com:8080/file.txt`합니다.  참고 hello `:8080` hello 호스트 이름 세그먼트의 hello 끝에 있습니다.  Hello 브라우저 toouse 포트 되었음을 알리는 `8080` tooconnect toohello 웹 서버의에서 `www.contoso.com`tooenter 8080 hello에 필요 하므로, **HTTP 포트** 필드입니다.  것이 중요 한 toonote 이러한 포트 설정을에 영향을 어떤 포트 hello 끝점 hello 원점에서 tooretrieve 정보를 사용 합니다.

> [!NOTE]
> **Akamai에서 azure CDN** 끝점 출처에 대 한 hello 전체 TCP 포트 범위를 허용 하지 않습니다.  허용되지 않는 원본 포트 목록을 보려면 [Akamai 허용된 원본 포트의 Azure CDN](https://msdn.microsoft.com/library/mt757337.aspx)를 참조하세요.  
> 
> 

### <a name="check-hello-endpoint-settings"></a>Hello 끝점 설정 확인
Hello에 다시 **끝점** 블레이드에서 hello 클릭 **구성** 단추입니다.

![구성 단추가 강조 표시된 끝점 블레이드](./media/cdn-troubleshoot-endpoint/cdn-endpoint-configure-button.png)

끝점의 hello **구성** 블레이드 나타납니다.

![구성 블레이드](./media/cdn-troubleshoot-endpoint/cdn-configure.png)

#### <a name="protocols"></a>프로토콜
에 대 한 **프로토콜**, hello 클라이언트에서 사용 되는 hello 프로토콜 선택 되어 있는지 확인 합니다.  hello hello 클라이언트에서 사용 하는 동일한 프로토콜이 됩니다 hello hello 이전 섹션에서 올바르게 구성 하는 중요 한 toohave hello 원본 포트 이므로 tooaccess hello 원본 하나 사용 합니다.  hello 끝점 hello 기본 HTTP 및 HTTPS 포트 (80 및 443)에 관계 없이 hello 원본 포트 에서만 수신합니다.

돌아가겠습니다. tooour 가상의 예제와 `http://www.contoso.com:8080/file.txt`합니다.  기억하시겠지만 Contoso는 HTTP 포트로 `8080`을 지정했습니다. 거기에 덧붙여 HTTPS 포트로 `44300`을 지정했다고 가정해 봅시다.  `contoso`라는 끝점을 만들었다면 CDN 끝점 호스트 이름은 `contoso.azureedge.net`입니다.  에 대 한 요청 `http://contoso.azureedge.net/file.txt` hello 끝점 포트 8080 tooretrieve에 HTTP를 사용 하므로 HTTP 요청은 hello 원본에서 합니다.  HTTPS 통해 안전한 요청 `https://contoso.azureedge.net/file.txt`로 인해 hello 끝점 toouse HTTPS 포트 44300에서 검색 해 hello hello 원점에서 파일 때.

#### <a name="origin-host-header"></a>원본 호스트 헤더
hello **원본 호스트 헤더** toohello 원점 각 요청과 함께 보낸 hello 호스트 헤더 값입니다.  대부분의 경우에서이 해야 수 hello 동일 hello로 **원본 호스트 이름을** 이전 확인 합니다.  이 필드에 잘못 된 값 일반적으로 404 상태 때문에 발생 하지 않은 가능성이 toocause 어떤 hello 원점 필요에 따라 다른 4xx 상태입니다.

#### <a name="origin-path"></a>원본 경로
마지막으로 **원본 경로**를 확인해야 합니다.  기본적으로 원본 경로는 비어 있습니다.  Toonarrow hello 범위를 원하는 경우에이 필드를 사용 해야 원하는 toomake hello CDN에서 사용할 수 있는 hello 원점 호스팅 리소스입니다.  

예를 들어 내 끝점에서 원하는 모든 리소스를 사용할 수 있는 저장소 계정 toobe 내에 퇴사 하므로 **원래 경로** 비어 있습니다.  즉, 요청을 너무`https://cdndocdemo.azureedge.net/publicblob/lorem.txt` 너무 내 끝점에서 연결으로 인해`cdndocdemo.core.windows.net` 요청 `/publicblob/lorem.txt`합니다.  마찬가지로,에 대 한 요청 `https://cdndocdemo.azureedge.net/donotcache/status.png` hello 끝점 요청으로 인해 `/donotcache/status.png` hello 출처에서입니다.

하지만 경우에 어떻게 toouse hello CDN 모든 경로 대 한 원본 내에 있습니까?  예를 들어 I 하기만 tooexpose hello `publicblob` 경로입니다.  입력 */publicblob* 에 내 **원래 경로** hello 끝점 tooinsert 하 필드 */publicblob* toohello 원점 진행 중인 모든 요청 전에 합니다.  즉, 해당 hello 요청에 대 한 `https://cdndocdemo.azureedge.net/publicblob/lorem.txt` hello URL의 hello 요청 부분 실제로 수행 됩니다 `/publicblob/lorem.txt`, 추가 및 `/publicblob` toohello 시작 합니다. 에 대 한 요청에이 인해 `/publicblob/publicblob/lorem.txt` hello 출처에서입니다.  해당 경로 tooan 실제 파일 확인 되지 않으면 hello 원점 404 상태를 반환 합니다.  이 예에서 hello 올바른 URL tooretrieve lorem.txt 것 실제로 `https://cdndocdemo.azureedge.net/lorem.txt`합니다.  Hello에 포함 하지 않는 것 */publicblob* 전혀 hello 요청 부분의 hello URL 때문에 경로가 `/lorem.txt` hello 끝점 추가 `/publicblob`로 `/publicblob/lorem.txt` hello 요청 전달 toohello 원본 .

