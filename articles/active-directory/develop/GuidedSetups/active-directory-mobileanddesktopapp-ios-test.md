---
title: "AD aaaAzure v2 iOS 테스트 시작 | Microsoft Docs"
description: "iOS(Swift) 응용 프로그램이 Azure Active Directory v2 끝점으로 보호되는 액세스 토큰을 필요로 하는 API를 호출하는 방식"
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
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 98c73eddabf9664feb19ac6878e9d7315b9aa79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="test-querying-hello-microsoft-graph-api-from-your-ios-application"></a>IOS 응용 프로그램에서 Graph API Microsoft hello를 쿼리 하는 테스트

키를 눌러 `Command`  +  `R` hello 시뮬레이터에 있는 toorun hello 코드입니다.

![샘플 스크린샷](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

준비 tootest, 누릅니다 *' Microsoft Graph API 호출 '* 하면 사용자 이름 및 암호 입력 정보 요청된 tootype 됩니다.

### <a name="consent"></a>동의
hello tooyour 응용 프로그램에 로그인 하는 처음으로 있습니다 나타납니다 toohello 비슷한 아래 동의 화면, tooexplicitly에 동의 해야 하는 경우:

![동의 화면](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a>예상 결과
Hello에 hello Microsoft Graph API 호출에서 반환 된 사용자 프로필 정보 표시 되어야 *로깅* 섹션.

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>범위 및 위임된 권한에 대한 자세한 내용

Microsoft Graph API hello 필요 hello `user.read` tooread hello 사용자 프로필의 범위입니다. 이 범위는 Microsoft 등록 포털에서 등록된 모든 응용 프로그램에서 기본적으로 자동 추가됩니다. 일부 다른 Microsoft Graph용 API와 백 엔드 서버용 사용자 지정 API에는 추가 범위가 필요할 수 있습니다. 예를 들어 Microsoft Graph에 대해 범위를 hello `Calendars.Read` 필요한 toolist hello 사용자 일정은 합니다. 순서로 tooaccess hello 응용 프로그램의 컨텍스트에서 사용자의 일정, tooadd hello 필요한 `Calendars.Read` 위임 권한 toohello 응용 프로그램 등록 정보를 hello 추가 `Calendars.Read` 범위 toohello `acquireTokenSilent` 호출 합니다. hello 사용자 hello 범위 수를 늘리면 추가 동의 대 한 안내가 수 있습니다.

<!--end-collapse-->



