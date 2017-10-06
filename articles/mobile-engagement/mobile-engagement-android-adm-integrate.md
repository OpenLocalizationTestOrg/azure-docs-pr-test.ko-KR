---
title: "Mobile Engagement Android SDK 통합 aaaAzure"
description: "Azure Mobile Engagement용 Android SDK의 최신 업데이트 및 절차"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a7d719ec-67b3-4be3-9d7f-0b61a57fe978
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c57132ff49cf8c335627a72b37f9b78529e84f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-adm-with-engagement"></a>어떻게 tooIntegrate ADM Engagement와
> [!IMPORTANT]
> 이 가이드를 수행 하기 전에 Android에서 Engagement tooIntegrate 문서화 하는 방법을 hello에 설명 된 hello 통합 절차를 따라야 합니다.
> 
> 이 문서는 이미 hello Reach 모듈 및 계획 toopush Amazon 장치를 통합 하는 경우에 유용 합니다. toointegrate Reach 캠페인을 읽으십시오 먼저 방법을 응용 프로그램에서 Android에서 Engagement Reach tooIntegrate 합니다.
> 
> 

## <a name="introduction"></a>소개
통합 ADM 푸시 Amazon Android 장치를 대상으로 하는 경우 사용자 응용 프로그램 toobe를 수 있습니다.

항상 toohello SDK 푸시 ADM 페이로드 포함 hello `azme` hello 데이터 개체의 키입니다. 따라서 응용 프로그램에서 다른 용도로 ADM을 사용하는 경우 해당 키에 따라 푸시를 필터링할 수 있습니다.

> [!IMPORTANT]
> Android 4.0.3 이상을 실행하는 Amazon Kindle 장치만 Amazon 장치 메시징을 통해 지원되지만 다른 장치에서 안전하게 이 코드를 통합할 수 있습니다.
> 
> 

## <a name="sign-up-tooadm"></a>TooADM 등록
아직 등록하지 않은 경우 Amazon 계정에서 ADM를 활성화해야 합니다.

hello 프로시저에서 자세히 설명 되어: [ <https://developer.amazon.com/sdk/adm/credentials.html>]합니다.

Hello 절차를 완료 되 면 가져오기:

* OAuth 자격 증명 (클라이언트 ID 및 클라이언트 암호) Engagement toobe 수 toopush에 대 한 장치입니다.
* 응용 프로그램에 통합해야 하는 API 키

## <a name="sdk-integration"></a>SDK 통합
### <a name="managing-device-registrations"></a>장치 등록 관리
각 장치 보내야 등록 명령 toohello ADM 서버, 그렇지 않으면은 연결할 수 없습니다.

이미 hello를 사용 하는 경우 [ADM 클라이언트 라이브러리], 이미 있고 [ADM 통합] tooandroid-sdk-adm 수신 직접 이동할 수 있습니다.

ADM를 통합 하지 아직 Engagement에 더 간단한 방법은 tooenable 경우 응용 프로그램에서:

`AndroidManifest.xml` 파일을 다음과 같이 편집합니다.

* Amazon 네임 스페이스 hello, hello 파일은 다음과 같이 시작 해야를 추가 합니다.
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* 내부 hello `<application/>` 태그,이 섹션을 추가 합니다.
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* Hello amazon 태그를 추가한 후 프로젝트 빌드 대상 Android 2.1 미만인 경우 빌드 오류를 할 수 있습니다. Toouse 있는 **Android 2.1 이상** 빌드 대상 (스 러을 사용할 수 있습니다는 `minSdkVersion` too4 설정).
* 수행 하 여 hello ADM API 키를 자산으로 통합 [이 절차]합니다.

다음 섹션에서는 hello의 hello 지침을 따릅니다.

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a>등록 id toohello Engagement 푸시 서비스를 통신 하 고 알림을 받기
Hello 장치 toohello Engagement 푸시의 순서 toocommunicate hello 등록 id에서 서비스 및 해당 알림이 제공, hello tooyour 다음 추가 `AndroidManifest.xml` hello 내 파일 `<application/>` 태그 (경우에 참여 하지 않고 ADM 사용):

        <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
          android:exported="false">
          <intent-filter>
            <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
          </intent-filter>
        </receiver>

         <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
           android:permission="com.amazon.device.messaging.permission.SEND">
          <intent-filter>
            <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
            <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
            <category android:name="<your_package_name>"/>
          </intent-filter>
        </receiver>   

다음에서 권한을 hello 해야 프로그램 `AndroidManifest.xml` (hello 전에 `</application>` 태그).

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a>Engagement OAuth 자격 증명 부여
Engagement 포털에서 OAuth 자격 증명(클라이언트 ID 및 클라이언트 암호)을 제출합니다.

[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html
[ADM 클라이언트 라이브러리]:https://developer.amazon.com/sdk/adm/setup.html
[ADM 통합]:https://developer.amazon.com/sdk/adm/integrating-app.html
[이 절차]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset
