---
title: "Azure Mobile Engagement Android SDK에 대 한 aaaAdvanced 구성"
description: "고급 구성 옵션 hello Azure Mobile Engagement Android SDK와 Android 매니페스트를 포함 하 여 hello를 설명 합니다."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 37d2c09a-86fa-473d-8987-c7e35a0eb3e8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 757abf362021fd018f444cae6305524623e77062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a>Azure Mobile Engagement Android SDK용 고급 구성
> [!div class="op_single_selector"]
> * [유니버설 Windows](mobile-engagement-windows-store-advanced-configuration.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-configuration.md)
>
>

이 절차에서는 설명 방법을 tooconfigure Azure Mobile Engagement Android 앱에 대 한 다양 한 구성 옵션입니다.

## <a name="prerequisites"></a>필수 조건
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a>사용 권한 요구 사항
몇 가지 옵션 중 일부는 여기에 나열 됩니다 참조 및 hello 특정 기능에는 줄에 특정 사용 권한이 필요 합니다. 바로 앞 또는 뒤 hello 이러한 사용 권한을 toohello AndroidManifest.xml 프로젝트의 추가 `<application>` 태그입니다.

hello 사용 권한 코드 뒤에 오는 hello 테이블에서 적절 한 권한을 hello에 입력할 수 있는, hello 다음과 같은 toolook이 필요 합니다.

    <uses-permission android:name="android.permission.[specific permission]"/>


| 사용 권한 | 사용할 경우 |
| --- | --- |
| 인터넷 |필수입니다. 기본 보고용 |
| ACCESS_NETWORK_STATE |필수입니다. 기본 보고용 |
| RECEIVE_BOOT_COMPLETED |필수입니다. 장치를 다시 부팅 후 hello 알림 센터를 tooshow |
| WAKE_LOCK |권장됩니다. WiFi를 사용하거나 화면이 꺼져 있을 때 데이터를 수집합니다. |
| VIBRATE |선택 사항입니다. 알림이 수신될 때 진동을 울립니다. |
| DOWNLOAD_WITHOUT_NOTIFICATION |선택 사항입니다. Android 큰 그림 알림을 사용합니다. |
| WRITE_EXTERNAL_STORAGE |선택 사항입니다. Android 큰 그림 알림을 사용합니다. |
| ACCESS_COARSE_LOCATION |선택 사항입니다. 실시간 위치 보고를 활성화합니다. |
| ACCESS_FINE_LOCATION |선택 사항입니다. GPS 기반 위치 보고를 활성화합니다. |

Android M부터는 [일부 권한이 런타임 시 관리됩니다](mobile-engagement-android-location-reporting.md#android-m-permissions).

이미 사용 중인 경우 ``ACCESS_FINE_LOCATION``, tooalso 않아도 다음 사용 하 여 ``ACCESS_COARSE_LOCATION``합니다.

## <a name="android-manifest-configuration-options"></a>Android 매니페스트 파일 구성 옵션
### <a name="crash-report"></a>충돌 보고서
hello 사이이 코드를 추가 하는 toodisable 충돌 보고서 `<application>` 및 `</application>` 태그:

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a>버스트 임계값
기본적으로 hello Engagement 서비스 보고서는 실시간으로 기록 합니다. 응용 프로그램 보고서 로그를 자주 다를 경우 더 나은 toobuffer hello 로그 및 tooreport는 일반 기본 시간 ("모드 전환" 라고 함)에서 한 번에 모두 있습니다. toodo hello 사이 다음이 코드를 추가, `<application>` 및 `</application>` 태그:

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

버스트 모드 약간 hello 배터리 수명 늘어나지만 hello Engagement 모니터에 영향을 주: 모든 세션 및 작업 기간 둥근된 toohello 버스트 임계값 (따라서 세션 및 작업 hello 버스트 임계값 표시 되지 않는 보다 짧은) 됩니다. 버스트 임계값은 30000(30초) 이하여야 합니다.

### <a name="session-timeout"></a>세션 시간 제한
 키를 눌러 hello 여 활동을 끝낼 수 **홈** 또는 **다시** 키 유휴 hello 전화 설정 또는 다른 응용 프로그램으로 이동 합니다. 기본적으로 세션의 마지막 활동 hello 종료 후 10 초 동안 종료 됩니다. 이 방지 수 발생할 hello 사용자 이미지를 선택 하는 경우 체크 인 등 알림 세션 분할 각 시간 hello 사용자를 끝내 고 toohello 응용 프로그램을 신속 하 게 반환 합니다. 이 매개 변수 toomodify를 할 수 있습니다. toodo hello 사이 다음이 코드를 추가, `<application>` 및 `</application>` 태그:

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a>로그 보고 사용 안 함
### <a name="using-a-method-call"></a>메서드 호출 사용
로그 보내기 Engagement toostop 하려는 경우 호출할 수 있습니다.

    EngagementAgent.getInstance(context).setEnabled(false);

이 호출은 영구적이며, 공유 기본 설정 파일을 사용합니다.

Engagement 활성 상태 이면이 함수를 호출할 때 서비스 toostop hello에 대 일 분 걸릴 수 있습니다. 그러나 다음 hello 응용 프로그램을 시작할 때 모든 hello에서 hello 서비스를 시작할 없습니다 것입니다.

로그 다시 hello와 같은 함수를 호출 하 여 보고를 사용 하도록 설정할 수 `true`합니다.

### <a name="integration-in-your-own-preferenceactivity"></a>고유한 `PreferenceActivity`
이 함수를 호출하지 않고 기존 `PreferenceActivity`에서 직접 이 설정을 통합할 수 있습니다.

Hello에서 Engagement toouse 기본 설정 파일 (hello 원하는 모드)를 구성할 수 있습니다 `AndroidManifest.xml` 파일 `application meta-data`:

* hello `engagement:agent:settings:name` 키는 hello 공유 기본 설정 파일의 사용 되는 toodefine hello 이름입니다.
* hello `engagement:agent:settings:mode` 키는 hello 공유 기본 설정 파일의 사용 되는 toodefine hello 모드입니다. 사용 하 여 hello 동일한 모드에서와 같이 프로그램 `PreferenceActivity`합니다. hello 모드 숫자 변수로 전달 되어야 합니다: 상수 플래그의 조합을 코드를 사용 하는 경우 hello 총 값을 확인 합니다.

항상 engagement hello를 사용 하 여 `engagement:key` 이 설정을 관리 하기 위한 hello 기본 설정 파일 내에서 부울 키입니다.

다음 예의 hello `AndroidManifest.xml` 표시 hello 기본값:

    <application>
        [...]
        <meta-data
          android:name="engagement:agent:settings:name"
          android:value="engagement.agent" />
        <meta-data
          android:name="engagement:agent:settings:mode"
          android:value="0" />

추가 하 여 한 `CheckBoxPreference` 하나를 따르는 hello와 같은 기본 설정 레이아웃에서:

    <CheckBoxPreference
      android:key="engagement:enabled"
      android:defaultValue="true"
      android:title="Use Engagement"
      android:summaryOn="Engagement is enabled."
      android:summaryOff="Engagement is disabled." />
