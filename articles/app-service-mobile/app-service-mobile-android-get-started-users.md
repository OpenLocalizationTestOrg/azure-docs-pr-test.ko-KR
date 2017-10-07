---
title: "Android 모바일 앱에서 aaaAdd 인증 | Microsoft Docs"
description: "Toouse 다양 한 Google, Facebook, Twitter 및 Microsoft를 비롯 한 id 공급자를 통해 Android 앱의 Azure 앱 서비스 tooauthenticate 사용자의 모바일 앱 기능을 hello 하는 방법에 대해 알아봅니다."
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 1fc8e7c1-6c3c-40f4-9967-9cf5e21fc4e1
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 01f608f996c931c643790ed2778df11cf590c903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-android-app"></a>인증 tooyour Android 앱 추가
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a>요약
이 자습서에서는 지원 되는 id 공급자를 사용 하 여 Android에서 인증 toohello todolist 퀵 스타트 프로젝트를 추가 합니다. 이 자습서는 hello 기반 [모바일 앱 시작] 자습서 먼저 완료 해야 합니다.

## <a name="register"></a>인증을 위한 앱 등록 및 Azure App Service 구성
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>응용 프로그램 toohello 허용 된 외부 리디렉션 Url을 사용 하 여 추가

보안 인증을 위해서는 앱에 대한 새로운 URL 체계를 정의해야 합니다. Hello 인증 프로세스가 완료 되 면 hello 인증 시스템 tooredirect 백 tooyour 앱을 수 있습니다. 이 자습서에서는 사용 하 여 hello URL 체계 _appname_ 전체. 그러나 선택한 어떤 URL 체계도 사용 가능합니다. 고유 tooyour 모바일 응용 프로그램 이어야 합니다. hello 서버 쪽에서 tooenable hello 리디렉션:

1. Hello [Azure 포털], 응용 프로그램 서비스를 선택 합니다.

2. Hello 클릭 **인증 / 권한 부여** 메뉴 옵션입니다.

3. Hello에 **외부 리디렉션 Url 허용**, 입력 `appname://easyauth.callback`합니다.  hello _appname_ 이 문자열에는 모바일 응용 프로그램에 대 한 hello URL 체계입니다.  이 체계는 프로토콜에 대한 일반 URL 사양을 따라야 합니다(문자 및 숫자만 사용하고 문자로 시작).  Tooadjust hello 여러 위치에서 URL 체계를 사용 하 여 모바일 응용 프로그램 코드 필요 하므로 선택 하는 hello 문자열의 메모를 확인 해야 합니다.

4. **확인**을 클릭합니다.

5. **Save**를 클릭합니다.

## <a name="permissions"></a>Tooauthenticated 사용자 사용 권한 제한
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* Android Studio에서 hello 자습서와 함께 완료 hello 프로젝트를 열고 [모바일 앱 시작]합니다. Hello에서 **실행** 메뉴를 클릭 하 여 **응용 프로그램을 실행**, hello 앱 시작 된 후 401 (권한 없음) 상태 코드와 함께 처리 되지 않은 예외가 발생할 때 확인 합니다.

     이 예외는 hello 앱 시도 tooaccess hello 다시 인증 되지 않은 사용자로 종료 하지만 hello 때문에 발생 *TodoItem* 테이블에는 이제 인증이 필요 합니다.

다음으로, 모바일 앱을 다시 종료 hello에서 리소스를 요청 하기 전에 hello 앱 tooauthenticate 사용자를 업데이트 합니다. 

## <a name="add-authentication-toohello-app"></a>인증 toohello 앱 추가
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <a name="cache-tokens"></a>Hello 클라이언트에서 인증 토큰을 캐시
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a>다음 단계
이 기본 인증 자습서를 완료 했으므로 tooone의 hello 다음 자습서를 계속 진행 하는 것이 좋습니다.

* [푸시 알림 tooyour Android 앱 추가](app-service-mobile-android-get-started-push.md)합니다.
  모바일 앱 다시 tooconfigure toouse Azure 알림 허브 toosend 푸시 알림을 종료 하는 방법에 대해 알아봅니다.
* [Android 앱에 대해 오프라인 동기화를 사용합니다](app-service-mobile-android-get-started-offline-data.md).
  오프 라인 tooadd 모바일 앱 백 엔드를 사용 하 여 tooyour 응용 프로그램을 지 원하는 방법에 대해 알아봅니다. 오프라인 동기화를 사용하면 사용자는 네트워크에 연결되어 있지 않을 때도 모바일 앱&mdash;데이터 보기, 추가 또는 수정&mdash;과 같은 상호 작용을 수행할 수 있습니다.

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions tooauthenticated users]: #permissions
[Add authentication toohello app]: #add-authentication
[Store authentication tokens on hello client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
[모바일 앱 시작]: app-service-mobile-android-get-started.md
