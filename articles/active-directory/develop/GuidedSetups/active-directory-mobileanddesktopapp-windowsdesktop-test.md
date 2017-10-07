---
title: "AD aaaAzure v2 Windows 데스크톱 시작-테스트 | Microsoft Docs"
description: "Windows Desktop .NET(XAML) 응용 프로그램이 Azure Active Directory v2 끝점으로 보호되는 액세스 토큰을 필요로 하는 API를 호출하는 방식"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 0ae9612e1585c54a3fe35ba9d18f92554099b2c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>코드 테스트

순서로 tootest 키를 눌러 응용 프로그램 `F5` toorun Visual Studio에서 프로젝트. 아래와 같이 주 창이 표시됩니다.

![샘플 스크린샷](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

준비 tootest 완료 했으면 클릭 *Microsoft Graph API 호출* 하 고 실행 하는 Microsoft Azure Active Directory (조직 계정)에서 Microsoft 계정 (live.com, outlook.com) 계정 toosign 사용 합니다. 그 hello 처음으로, 요청에 사용자 toosign 창이 표시 됩니다.

![로그인](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a>동의
hello tooyour 응용 프로그램에 로그인 하는 처음으로 있습니다 나타납니다 toohello 비슷한 아래 동의 화면, tooexplicitly에 동의 해야 하는 경우:

![동의 화면](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a>예상 결과
Hello API 호출 결과 화면 hello Microsoft Graph API 호출에서 반환 된 사용자 프로필 정보를 볼 수 있습니다.

또한 표시를 통해 확보 하는 hello 토큰에 대 한 기본 정보 `AcquireTokenAsync` 또는 `AcquireTokenSilentAsync` hello 토큰 정보 상자에서:

|속성  |형식  |설명 |
|---------|---------|---------|
|이름 | {User Full name} |hello 사용자 ् य ा च े ं|
|사용자 이름 |<span>user@domain.com</span> |tooidentify hello 사용자를 사용 하는 hello 사용자 이름|
|토큰 만료 |{DateTime}         |토큰이 만료 되는 hello에 hello 시간입니다. MSAL 필요한 경우 hello 토큰을 갱신 하 여 사용자에 대 한 hello 만료 날짜를 확장 하면|
|액세스 토큰 |{String}         |토큰 문자열 hello tooHTTP 요청 권한 부여 헤더를 필요로 하는 전송 하는 전송|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>범위 및 위임된 권한에 대한 자세한 내용
Graph API 필요 hello `user.read` tooread 사용자 프로필의 범위. 이 범위는 Microsoft 등록 포털에서 등록된 모든 응용 프로그램에서 기본적으로 자동 추가됩니다. 일부 다른 Graph API와 백 엔드 서버용 사용자 지정 API에는 추가 범위가 필요합니다. 그래프에 대 한 예를 들어 `Calendars.Read` 필요한 toolist 사용자 일정은 합니다. 순서로 tooaccess hello 응용 프로그램의 컨텍스트에서 사용자의 일정, tooadd 필요한 `Calendars.Read` 응용 프로그램 등록 정보를 위임 하 고 다음 추가 `Calendars.Read` toohello `AcquireTokenAsync` 호출 합니다. Hello 범위 수를 늘리면 추가 동의 대 한 메시지가 만들 수 있습니다.

<!--end-collapse-->



