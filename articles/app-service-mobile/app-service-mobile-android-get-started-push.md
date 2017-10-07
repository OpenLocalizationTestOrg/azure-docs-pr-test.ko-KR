---
title: "aaaAdd 푸시 알림 tooyour Android 앱을 모바일 앱 | Microsoft Docs"
description: "모바일 앱 toosend toouse 밀어넣기 알림 tooyour Android 앱에 알아봅니다."
services: app-service\mobile
documentationcenter: android
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 9058ed6d-e871-4179-86af-0092d0ca09d3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: dcfb8463b395904b4bd0bf9bde2f71f259894066
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-android-app"></a>푸시 알림 tooyour Android 앱 추가
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>개요
이 자습서에서는 푸시 알림을 toohello 추가한 [Android 퀵 스타트] 프로젝트 레코드가 삽입 될 때마다 푸시 알림을 toohello 장치가 전송 되도록 합니다.

사용 하지 않는 경우 hello 퀵 스타트 서버 프로젝트를 다운로드, 푸시 알림 확장 패키지 hello 필요 합니다. 자세한 내용은 참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)합니다.

## <a name="prerequisites"></a>필수 조건
Hello 다음이 필요합니다.

* 프로젝트의 백 엔드에 따른 IDE

  * 이 앱에 Node.js 백 엔드가 있는 경우 [Android Studio](https://developer.android.com/sdk/index.html)
  * 이 앱에 Microsoft .Net 백 엔드가 있는 경우 [Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) 이상
* Firebase Cloud Messaging의 경우 Android 2.3 이상, Google Repository 개정 27 이상 및 Google Play Services 9.0.2 이상
* 전체 hello [Android 퀵 스타트]합니다.

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a>Firebase Cloud Messaging을 지원하는 프로젝트 만들기
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a>알림 허브 구성
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-toosend-push-notifications"></a>Azure toosend 푸시 알림 구성
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-hello-server-project"></a>Hello 서버 프로젝트에 대 한 푸시 알림을 사용 하도록 설정
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-tooyour-app"></a>푸시 알림 tooyour 앱 추가
이 섹션에서는 클라이언트 Android 앱 toohandle 푸시 알림을 업데이트할 수 있습니다.

### <a name="verify-android-sdk-version"></a>Android SDK 버전 확인
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

다음 단계는 tooinstall Google Play 서비스입니다. Google 클라우드 메시징에 개발 및 테스트를 어떤 hello에 대 한 최소 API 수준 요구 사항을 **minSdkVersion** hello 매니페스트에 속성을 따라야 합니다.

오래 된 장치를 테스트 하는 경우 참조 [설정를 Google 재생 서비스 SDK] toodetermine 아무리이 값을 설정 하 고 적절 하 게 설정할 수 있습니다.

### <a name="add-google-play-services-toohello-project"></a>Google Play 서비스 toohello 프로젝트 추가
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a>코드 추가
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-hello-app-against-hello-published-mobile-service"></a>모바일 서비스를 게시 하는 hello에 대 한 hello 응용 프로그램 테스트
USB 케이블로 Android 휴대폰을 직접 연결 하 여 또는 hello 에뮬레이터에서 가상 장치를 사용 하 여 hello 앱을 테스트할 수 있습니다.

## <a name="next-steps"></a>다음 단계
이 자습서를 완료 했으므로 tooone의 hello 다음 자습서를 계속 진행 하는 것이 좋습니다.

* [인증 tooyour Android 앱 추가](app-service-mobile-android-get-started-users.md)합니다.
  지원 되는 id 공급자를 사용 하는 Android에서 tooadd 인증 toohello todolist 퀵 스타트 프로젝트 방법에 대해 알아봅니다.
* [Android 앱에 대해 오프라인 동기화를 사용합니다](app-service-mobile-android-get-started-offline-data.md).
  오프 라인 tooadd 모바일 앱 백 엔드를 사용 하 여 tooyour 응용 프로그램을 지 원하는 방법에 대해 알아봅니다. 오프라인 동기화를 사용하면 사용자는 네트워크에 연결되어 있지 않을 때도 모바일 앱&mdash;데이터 보기, 추가 또는 수정&mdash;과 같은 상호 작용을 수행할 수 있습니다.

<!-- URLs -->
[Android 퀵 스타트]: app-service-mobile-android-get-started.md

[설정를 Google 재생 서비스 SDK]:https://developers.google.com/android/guides/setup
