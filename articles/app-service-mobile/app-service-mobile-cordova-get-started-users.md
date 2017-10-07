---
title: "모바일 앱과 함께 Apache Cordova에서 aaaAdd 인증 | Microsoft Docs"
description: "자세한 내용은 방법 toouse 모바일 앱에서 다양 한 Google, Facebook, Twitter 및 Microsoft를 비롯 한 id 공급자를 통해 Apache Cordova 앱의 Azure 앱 서비스 tooauthenticate 사용자입니다."
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 10dd6dc9-ddf5-423d-8205-00ad74929f0d
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 61a05c5ac67fd0f0bc4c9d6920954a9b464a0a8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-apache-cordova-app"></a>인증 tooyour Apache Cordova 앱 추가
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a>요약
이 자습서에서는 지원 되는 id 공급자를 사용 하는 Apache Cordova에 인증 toohello todolist 퀵 스타트 프로젝트를 추가 합니다. 이 자습서는 hello 기반 [모바일 앱 시작] 자습서 먼저 완료 해야 합니다.

## <a name="register"></a>인증에 대 한 앱을 등록 하 고 hello 응용 프로그램 서비스 구성
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[유사한 단계를 보여 주는 비디오 보기](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <a name="permissions"></a>Tooauthenticated 사용자 사용 권한 제한
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

이제 해당 익명 액세스 tooyour 백 엔드 비활성화 됨을 확인할 수 있습니다. Visual Studio에서

* Hello 자습서를 완료 하는 때 만든 열기 hello 프로젝트 [모바일 앱 시작]합니다.
* Hello에 응용 프로그램을 실행 **Google Android 에뮬레이터**합니다.
* Hello 앱 시작 된 후 연결 오류가 나타나는지 확인 합니다.

Hello 모바일 앱 백 엔드에서 리소스를 요청 하기 전에 hello 앱 tooauthenticate 사용자를 업데이트 합니다.

## <a name="add-authentication"></a>인증 toohello 앱 추가
1. 프로젝트를 열고 **Visual Studio**을 연 다음 hello `www/index.html` 편집할 수 있도록 합니다.
2. Hello 찾을 `Content-Security-Policy` hello 헤드 절의 메타 태그입니다.  허용 된 원본 hello OAuth 호스트 toohello 목록을 추가 합니다.

   | 공급자 | SDK 공급자 이름 | OAuth 호스트 |
   |:--- |:--- |:--- |
   | Azure Active Directory | aad | https://login.microsoftonline.com |
   | Facebook | Facebook | https://www.facebook.com |
   | Google | Google | https://accounts.google.com |
   | Microsoft | microsoftaccount | https://login.live.com |
   | Twitter | Twitter | https://api.twitter.com |

    다음은 Content-Security-Policy(Azure Active Directory용으로 구현됨) 예제입니다.

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    대체 `https://login.microsoftonline.com` hello 앞에 테이블에서에서 hello OAuth 호스트와 합니다.  Hello 콘텐츠 보안 정책 메타 태그에 대 한 자세한 내용은 참조 hello [콘텐츠 보안 정책 설명서]합니다.

    일부 인증 공급자에서는 적절한 모바일 장치에서 사용하는 경우 Content-Security-Policy 변경이 필요하지 않습니다.  예를 들어 Android 장치에서 Google 인증을 사용하는 경우 Content-Security-Policy를 변경하지 않아도 됩니다.

3. 열기 hello `www/js/index.js` 편집을 위해 파일을 찾을 hello `onDeviceReady()` 메서드를 hello 클라이언트 만들기 코드 hello 코드 다음에 추가 하 고:

        // Login toohello service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    이 코드는 hello 테이블 참조를 만들고 hello UI를 새로 고치는 hello 기존 코드를 대체 합니다.

    hello login() 메서드 hello 공급자와 인증을 시작합니다. hello login() 메서드는 JavaScript 프라미스를 반환 하는 비동기 함수입니다.  hello 초기화 hello 나머지는 hello 프라미스 응답 내 배치 되므로 hello login() 메서드가 완료 될 때까지 실행 되지 않습니다.

4. 방금 추가한 hello 코드에서 대체할 `SDK_Provider_Name` 로그인 공급자의 hello 이름으로 합니다. 예를 들어 Azure Active Directory의 경우 `client.login('aad')`를 사용합니다.
5. 프로젝트를 실행합니다.  Hello 프로젝트 초기화 완료 되 면 응용 프로그램 인증 공급자를 선택 하는 hello에 대 한 hello OAuth 로그인 페이지를 보여줍니다.

## <a name="next-steps"></a>다음 단계
* Azure 앱 서비스의 [인증 정보] 에 대해 자세히 알아봅니다.
* 추가 하 여 hello 자습서를 계속 [푸시 알림을] tooyour Apache Cordova 앱.

Toouse Sdk hello 하는 방법에 대해 알아봅니다.

* [Apache Cordova SDK]
* [ASP.NET 서버 SDK]
* [Node.js 서버 SDK]

<!-- URLs. -->
[모바일 앱 시작]: app-service-mobile-cordova-get-started.md
[콘텐츠 보안 정책 설명서]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html
[푸시 알림을]: app-service-mobile-cordova-get-started-push.md
[인증 정보]: app-service-mobile-auth.md
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET 서버 SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js 서버 SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
