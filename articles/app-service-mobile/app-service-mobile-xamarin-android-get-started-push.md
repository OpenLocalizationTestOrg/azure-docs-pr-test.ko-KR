---
title: "aaaAdd 푸시 알림 tooyour Xamarin.Android 앱 | Microsoft Docs"
description: "Azure 앱 서비스 toouse 및 Azure 알림 허브 toosend 밀어넣기 알림 tooyour Xamarin.Android 응용 프로그램에 알아봅니다"
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6f7e8517-e532-4559-9b07-874115f4c65b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: c93d1d0cae06ab15e3e3e5c4b342808b2cd49113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinandroid-app"></a>푸시 알림 tooyour Xamarin.Android 앱 추가
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>개요
이 자습서에서는 푸시 알림을 toohello 추가한 [Xamarin.Android 퀵 스타트](app-service-mobile-windows-store-dotnet-get-started.md) 프로젝트 레코드가 삽입 될 때마다 푸시 알림을 toohello 장치가 전송 되도록 합니다.

사용 하지 않는 경우 hello 퀵 스타트 서버 프로젝트를 다운로드, 푸시 알림 확장 패키지 hello 필요 합니다. 참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) 자세한 정보에 대 한 합니다.

## <a name="prerequisites"></a>필수 조건
이 자습서는 hello 다음을 사항이 필요합니다.

* 활성 Google 계정. [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302)에서 Google 계정을 등록할 수 있습니다.
* [Google Cloud Messaging 클라이언트 구성 요소](http://components.xamarin.com/view/GCMClient/).

## <a name="configure-hub"></a>알림 허브 구성
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a id="register"></a>Firebase Cloud Messaging 사용
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-toosend-push-requests"></a>Azure toosend 푸시 요청을 구성
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a id="update-server"></a>업데이트 hello 서버 프로젝트 toosend 푸시 알림
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a id="configure-app"></a>푸시 알림에 대 한 hello client 프로젝트를 구성 합니다.
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <a id="add-push"></a>푸시 알림을 코드 tooyour 앱 추가
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <a name="test"></a>앱에서 푸시 알림 테스트
Hello 에뮬레이터에서 가상 장치를 사용 하 여 hello 앱을 테스트할 수 있습니다. 에뮬레이터에서 실행할 때 필요한 추가 구성 단계가 있습니다.

1. 배포 하는 tooor 디버깅 hello Android Virtual Device (AVD) 관리자에서 다음과 같이 hello 대상으로 설정 하는 Google Api가 가상 장치에 있는지 확인 합니다.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. 클릭 하 여 Google 계정 toohello Android 장치를 추가 **앱** > **설정** > **계정을 추가**, 다음 hello 프롬프트를 따릅니다.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. 앞으로 hello todolist 앱을 실행 하 고 새 할 일 항목을 삽입 합니다. 이 이번에는 알림 아이콘 hello 알림 영역에 표시 됩니다. Hello 알림 서랍 tooview hello의 전체 텍스트 알림 hello 열 수 있습니다.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
