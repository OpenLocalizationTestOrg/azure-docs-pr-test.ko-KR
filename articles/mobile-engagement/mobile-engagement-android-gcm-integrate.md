---
title: "Mobile Engagement Android SDK 통합 aaaAzure"
description: "Azure Mobile Engagement용 Android SDK의 최신 업데이트 및 절차"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d72b5014-a22b-4a7f-a470-d2b8145b5b86
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/10/2016
ms.author: piyushjo
ms.openlocfilehash: e81230cbc99a209f2909cc163c4e566df67dc828
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-gcm-with-mobile-engagement"></a>어떻게 tooIntegrate Mobile Engagement와 GCM
> [!IMPORTANT]
> 이 가이드를 수행 하기 전에 Android에서 Engagement tooIntegrate 문서화 하는 방법을 hello에 설명 된 hello 통합 절차를 따라야 합니다.
> 
> 이 문서는 이미 통합 된 hello 장치 모듈 및 계획 toopush Google Play에 도달 하는 경우에 유용 합니다. toointegrate Reach 캠페인을 읽으십시오 먼저 방법을 응용 프로그램에서 Android에서 Engagement Reach tooIntegrate 합니다.
> 
> 

## <a name="introduction"></a>소개
GCM 통합 프로그램 응용 프로그램 toobe를 푸시할 수 있습니다.

항상 toohello SDK 푸시 GCM 페이로드 포함 hello `azme` hello 데이터 개체의 키입니다. 따라서 응용 프로그램에서 다른 용도로 GCM을 사용하는 경우 해당 키에 따라 푸시를 필터링할 수 있습니다.

> [!IMPORTANT]
> Android 2.2 이상을 실행하고, Google Play를 설치하고, Google 백그라운드 연결이 활성화된 장치만 GCM을 사용해 푸시될 수 있지만 지원되지 않는 장치(단지 의도만 이용하는 장치)에서 이 코드를 안전하게 통합할 수 있습니다.
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a>API 키를 가진 Google Cloud Messaging 프로젝트 만들기
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a>SDK 통합
### <a name="managing-device-registrations"></a>장치 등록 관리
각 장치 보내야 등록 명령 toohello Google 서버, 그렇지 않으면은 연결할 수 없습니다.

장치는 GCM 알림 (hello 장치가 하지 않으면 자동으로 등록 된 hello 응용 프로그램을 제거 하는 경우)에서 등록 취소도 있습니다.

사용 하지 않는 경우 [Google 재생 SDK] 또는 이미 보내지 않으면 hello 등록 의도 자신, Engagement 드립니다 hello 장치를 자동으로 등록을 만들 수 있습니다.

tooenable이 hello tooyour 다음 추가 `AndroidManifest.xml` hello 내 파일 `<application/>` 태그:

            <!-- If only 1 sender, don't forget hello \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a>등록 id toohello Engagement 푸시 서비스를 통신 하 고 알림을 받기
Hello 장치 toohello Engagement 푸시의 순서 toocommunicate hello 등록 id에서 서비스 및 해당 알림이 제공, hello tooyour 다음 추가 `AndroidManifest.xml` hello 내 파일 `<application/>` 태그 (도 관리 하는 경우 장치 등록 직접):

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your_package_name>" />
              </intent-filter>
            </receiver>

다음에서 권한을 hello 해야 프로그램 `AndroidManifest.xml` (hello 후 `</application>` 태그).

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a>Grant Mobile Engagement 액세스 tooyour GCM API 키
에 따라 [이 가이드](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) toogrant Mobile Engagement 액세스 tooyour GCM API 키입니다.

[Google 재생 SDK]:https://developers.google.com/cloud-messaging/android/start
