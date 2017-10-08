---
title: "Azure Mobile Engagement Android SDK에 대 한 옵션을 보고 aaaAdvanced"
description: "Toodo 보고 toocapture 분석 Azure Mobile Engagement Android SDK에 대 한 고급 하는 방법을 설명 합니다."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7da7abd5-19d6-4892-94d8-818e5424b2cd
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 5c8f4ea36c54715f4e09fd43c96132c15019a71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-engagement-on-android"></a>Android에서 Engagement를 사용한 고급 보고
> [!div class="op_single_selector"]
> * [유니버설 Windows](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-reporting.md)
> 
> 

이 항목에서는 Android 응용 프로그램에서 추가 보고 시나리오를 설명합니다. 이러한 옵션 toohello 앱 hello에서 만든를 적용할 수 있습니다 [시작](mobile-engagement-android-get-started.md) 자습서입니다.

## <a name="prerequisites"></a>필수 조건
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

hello 자습서를 완료 하셨습니까 의도적으로 직접 및 간단 하지만 있습니다는 고급 옵션을 선택할 수 있습니다.

## <a name="modifying-your-activity-classes"></a>`Activity` 클래스 수정
Hello에 [시작 자습서](mobile-engagement-android-get-started.md), toomake가 모든 toodo 지 프로그램 `*Activity` hello 해당 서브 클래스에서 상속 `Engagement*Activity` 클래스입니다. 예를 들어 레거시 작업이 `ListActivity`를 확장하는 경우 `EngagementListActivity`를 확장하도록 합니다.

> [!IMPORTANT]
> 사용 하는 경우 `EngagementListActivity` 또는 `EngagementExpandableListActivity`, 있는지 확인 호출 너무`requestWindowFeature(...);` 너무 hello 호출 전에 이루어집니다`super.onCreate(...);`, 그렇지 않으면 충돌이 발생 합니다.
> 
> 

Hello에서 이러한 클래스를 찾을 수 있습니다 `src` 폴더를 프로젝트에 복사할 수 있습니다. hello 클래스에에서도 포함 되어 hello **JavaDoc**합니다.

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a>대체 방법: `startActivity()` 및 `endActivity()` 수동 호출
처리할 수 없거나 toooverload 하지 않을 경우 사용자 `Activity` 클래스 수 대신 시작 되 고 끝나는 활동 hello를 호출 하 여 `EngagementAgent`의 메서드를 직접 합니다.

> [!IMPORTANT]
> hello Android SDK를 호출 하지 않습니다. hello `endActivity()` hello 응용 프로그램이 닫힐 경우에 메서드 (android에서는 응용 프로그램은 하며 절대로 닫히지 않습니다). 즉, *항상* toocall hello 권장 `startActivity()` hello에 대 한 메서드 `onResume` 의 콜백에 *모든* 활동 및 hello `endActivity()` hello에 대 한 메서드 `onPause()` 콜백 *모든* 활동입니다. 이 hello 유일한 방법은 toobe 있는지 세션 유출 되지 않습니다. 세션은 누락 하는 경우 hello Engagement 서비스 되지에서 연결을 끊습니다 hello Engagement 백 엔드 (이후 세션은 보류 중으로 hello 서비스 연결 상태가 유지).
> 
> 

다음은 예제입니다.

    public class MyActivity extends Some3rdPartyActivity
    {
      @Override
      protected void onResume()
      {
        super.onResume();
        String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
        EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
      }

      @Override
      protected void onPause()
      {
        super.onPause();
        EngagementAgent.getInstance(this).endActivity();
      }
    }

이 예제는 비슷한 toohello `EngagementActivity` 클래스 및 해당 소스 코드는 hello에 제공 된 변형, `src` 폴더입니다.

## <a name="using-applicationoncreate"></a>Application.onCreate() 사용
모든 코드에 배치 `Application.onCreate()` 다른 응용 프로그램에서 콜백 hello Engagement 서비스를 비롯 한 응용 프로그램의 모든 프로세스에 대 한 실행 됩니다. 불필요 한 메모리 할당 및 hello Engagement 프로세스의 스레드 등의 원하지 않는 부작용을 있을 수 있습니다 또는 중복 브로드캐스트 수신기 서비스입니다.

재정의 하는 경우 `Application.onCreate()`, hello 다음 코드 조각 hello 맨 앞에 추가 하는 것이 좋습니다 프로그램 `Application.onCreate()` 함수:

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

할 수 있는 동일한 작업에 대 한 hello `Application.onTerminate()`, `Application.onLowMemory()`, 및 `Application.onConfigurationChanged(...)`합니다.

확장할 수도 있습니다 `EngagementApplication` 확장 하는 대신 `Application`: 콜백 hello `Application.onCreate()` 프로세스 확인 및 호출 hello지 않습니다 `Application.onApplicationProcessCreate()` hello 현재 프로세스가 hello 하나의 호스팅 hello Engagement 서비스가 아닌 경우 hello 동일한 규칙이 적용에 대 한만 다른 콜백에 hello 합니다.

## <a name="tags-in-hello-androidmanifestxml-file"></a>Hello AndroidManifest.xml 파일의 태그
Hello AndroidManifest.xml 파일에 hello 서비스 태그에 hello `android:label` 특성을 사용 하면 있습니다 hello Engagement 서비스의 toochoose hello 이름을 tooend 사용자 전화 번호의 hello "실행 서비스" 화면에 표시 된 대로 합니다. 너무이 특성을 설정 하는 것이 좋습니다`"<Your application name>Service"` (예를 들어 `"AcmeFunGameService"`).

지정 하 여 hello `android:process` 특성 하면 해당 hello Engagement (Engagement hello 응용 프로그램에서 main/UI 스레드 응답이 잠재적으로 동일한 프로세스에서 실행 하는) 자체 프로세스에서 서비스를 실행 합니다.

## <a name="building-with-proguard"></a>ProGuard를 사용하여 빌드
ProGuard 응용 프로그램 패키지를 빌드하는 경우 일부 클래스 tookeep 할 수 있습니다. 다음 구성 코드 조각 hello를 사용할 수 있습니다.

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
