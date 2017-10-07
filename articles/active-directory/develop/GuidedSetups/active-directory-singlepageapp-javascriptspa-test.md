---
title: "AD aaaAzure v2 JS SPA 단계별 설치-테스트 | Microsoft Docs"
description: "JavaScript SPA 응용 프로그램이 Azure Active Directory v2 끝점으로 보호되는 액세스 토큰을 필요로 하는 API를 호출하는 방식"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: b2339431a070b5c4ad4058e6c1a9b19b83c84c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>코드 테스트

> ### <a name="testing-with-visual-studio"></a>Visual Studio로 테스트
> Visual Studio를 사용 하는 키를 누릅니다 `F5` toorun 프로젝트: hello 브라우저가 열리고 너무 안내*http://localhost: {port}* hello 나타나는 *Microsoft Graph API 호출* 단추입니다.

<p/><!-- -->

> ### <a name="testing-with-python-or-another-web-server"></a>Python 또는 다른 웹 서버를 사용하여 테스트
> Visual Studio를 사용 하지 않는 경우 웹 서버를 시작 하 고 구성 되어 있는지 확인 toolisten tooa TCP 포트 hello 있는 폴더에 따라 프로그램 *index.html* 파일입니다. Python을 시작할 수 있습니다 수신 hello 응용 프로그램의 폴더에서 hello 명령 프롬프트 / 터미널에서 실행 하 여 toohello 포트 hello:
> 
> ```bash
> python -m http.server 8080
> ```
>  그런 다음 유형과 hello 브라우저를 열고 *http://localhost:8080* 또는 *http://localhost: {port}* -경우 hello *포트* 해당 웹 서버가 toohello 포트 에 수신 대기합니다. Hello로 index.html 페이지의 hello 내용을 표시 되어야 *Microsoft Graph API 호출* 단추입니다.

## <a name="test-your-application"></a>응용 프로그램 테스트

Hello 브라우저 후 로드 하면 *index.html*, hello 클릭 *Microsoft Graph API 호출* 단추 합니다. 인 경우 hello 처음으로 hello 브라우저 이동 하면 Microsoft Azure Active Directory v2 toohello 끝점 중인 라는 메시지가 표시 toosign에서.
 
![샘플 스크린샷](media/active-directory-singlepageapp-javascriptspa-test/javascriptspascreenshot1.png)


### <a name="consent"></a>동의
hello tooyour 응용 프로그램에 로그인 하는 처음으로 표시 됩니다는 동의 화면 비슷한 toohello 다음 tooaccept 필요한:

 ![동의 화면](media/active-directory-singlepageapp-javascriptspa-test/javascriptspaconsent.png)


### <a name="expected-results"></a>예상 결과
Hello Microsoft Graph API 호출에 응답에서 반환 된 사용자 프로필 정보를 볼 수 있습니다.
 
 ![결과](media/active-directory-singlepageapp-javascriptspa-test/javascriptsparesults.png)

Hello에서 확보 하는 hello 토큰에 대 한 기본 정보를 볼 있습니다 *액세스 토큰* 및 *ID 토큰 클레임* 상자입니다.

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>범위 및 위임된 권한에 대한 자세한 내용

Microsoft Graph API hello 필요 hello `user.read` tooread hello 사용자 프로필의 범위입니다. 이 범위는 Microsoft 등록 포털에서 등록된 모든 응용 프로그램에서 기본적으로 자동 추가됩니다. 일부 다른 Microsoft Graph용 API와 백 엔드 서버용 사용자 지정 API에는 추가 범위가 필요할 수 있습니다. 예를 들어 Microsoft Graph에 대해 범위를 hello `Calendars.Read` 필요한 toolist hello 사용자 일정은 합니다. 순서로 tooaccess hello 응용 프로그램의 hello 컨텍스트에서 사용자의 일정, tooadd hello 필요한 `Calendars.Read` 위임 권한 toohello 응용 프로그램 등록 정보를 hello 추가 `Calendars.Read` 범위 toohello `acquireTokenSilent` 호출 합니다. hello 사용자 hello 범위 수를 늘리면 추가 동의 대 한 안내가 수 있습니다.

백 엔드 API (권장 하지 않음) 범위에 필요 하지 않으면 hello를 사용할 수 있습니다 `clientId` hello에 hello 범위로 `acquireTokenSilent` 및/또는 `acquireTokenRedirect` 호출 합니다.

<!--end-collapse-->
