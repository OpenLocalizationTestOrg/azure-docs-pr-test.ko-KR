---
title: "aaaHow tooUse hello Android에서 Engagement API"
description: "최신 Android SDK-tooUse Android에서 Engagement API hello 하는 방법"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 09b62659-82ae-4a55-8784-fca0b6b22eaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: article
ms.date: 07/25/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e0b2d484616c0c7874e77c5283d94c3063949ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-android"></a>TooUse는 Android에서 Engagement API hello 하는 방법
이 문서는 추가 기능 toohello 문서 [Android Mobile Engagement SDK에 대 한 고급 보고 옵션](mobile-engagement-android-advanced-reporting.md)합니다. 어떻게 toouse hello Engagement API tooreport 응용 프로그램 통계에 대 한 깊이 세부 정보에 제공 합니다.

응용 프로그램의 세션, 활동, 충돌 및 기술 정보 Engagement tooreport 하려면, 다음 hello 가장 간단한 방법은 임을 toomake 모든 염두에 둬야 프로그램 `Activity` hello 해당 하위 클래스 상속 `EngagementActivity` 클래스입니다.

예를 들어 tooreport 응용 프로그램에 대 한 특정 이벤트, 오류 및 작업, 필요한 경우 더 많은 toodo 하려는 경우 또는 tooreport 응용 프로그램의 활동에에서 있으면 다른 방식으로 hello hello에 구현 하는 보다 `EngagementActivity` toouse hello 필요 클래스 API 계약입니다.

hello Engagement API에서 제공 hello `EngagementAgent` 클래스입니다. Hello를 호출 하 여이 클래스의 인스턴스를 검색할 수 있습니다 `EngagementAgent.getInstance(Context)` 정적 메서드 (해당 hello 참고 `EngagementAgent` 반환 된 개체는 단일).

## <a name="engagement-concepts"></a>Engagement 개념
hello 다음과 같은 부분이 구체화 hello 일반적인 [Mobile Engagement 개념](mobile-engagement-concepts.md), hello Android 플랫폼에 대 한 합니다.

### <a name="session-and-activity"></a>`Session` 및 `Activity`
Hello 사용자 유휴 두 개 이상의 몇 초 유지 *활동*, 그의 시퀀스의 다음 *활동* 분할 되며 두 개의 고유한 *세션*합니다. 이러한 몇 초 hello "세션 시간 제한" 이라고 합니다.

*활동* toosay hello 된 hello 응용 프로그램의 한 화면은 주로 *활동* hello 화면에 표시 되 고 hello 화면을 닫으면이 중지 될 때 시작:이 hello 경우 hello Engagement SDK가 통합 hello를 사용 하 여 `EngagementActivity` 클래스입니다.

하지만 *활동* hello Engagement API를 사용 하 여 수동으로 제어할 수도 있습니다. 이렇게 하면 toosplit 각된 화면에 대 한 자세한 내용은 hello 사용 현황 (예: tooknown 얼마나 자주 및이 화면 안에 대화 상자 사용 되는 시간)이 화면의 여러 하위 부분 tooget 있습니다.

## <a name="reporting-activities"></a>활동 보고
> [!IMPORTANT]
> Hello를 사용 하는 경우이 섹션에 설명 된 tooreport 활동과 같은 활동 필요 하지 않습니다 `EngagementActivity` 클래스 및 변형 방법을 hello에 설명 된 대로 Android 문서에 Engagement tooIntegrate 합니다.
> 
> 

### <a name="user-starts-a-new-activity"></a>사용자가 새 활동을 시작함
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing hello current activity is required for Reach toodisplay in-app notifications, passing null will postpone such announcements and polls.

Toocall 필요한 `startActivity()` 각 시간 hello 사용자 동작을 변경 합니다. 첫 번째 호출 toothis 함수 hello 새 사용자 세션을 시작 합니다.

각 작업에 대해이 함수는 가장 좋은 곳 toocall hello `onResume` 콜백 합니다.

### <a name="user-ends-his-current-activity"></a>사용자가 현재 활동을 종료함
            EngagementAgent.getInstance(this).endActivity();

Toocall 필요한 `endActivity()` hello 사용자 자신의 마지막 활동을 완료 하는 때 한 번 이상. 이 hello Engagement SDK hello 사용자가 현재 유휴 및 hello 사용자 세션에 필요 하며 toobe 닫힌 hello 세션 시간 제한 한 번 만료 됩니다를 통해 알립니다 (호출 하는 경우 `startActivity()` hello 세션이 재개 되 단순히 hello 세션 제한 시간 만료 되기 전에).

각 작업에 대해이 함수는 가장 좋은 곳 toocall hello `onPause` 콜백 합니다.

## <a name="reporting-events"></a>이벤트 보고
### <a name="session-events"></a>세션 이벤트
세션 이벤트는 세션 동안 사용자가 수행 하는 일반적으로 사용 되는 tooreport hello 작업입니다.

**추가 데이터가 없는 예제:**

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

**추가 데이터가 있는 예제:**

            public MyActivity extends EngagementActivity {
              [...]
              @Override
              public boolean onMenuItemSelected(int featureId, MenuItem item) {
                Bundle extras = new Bundle();
                extras.putInt("id", item.getItemId());
                getEngagementAgent().sendSessionEvent("menu_selected", extras);
              }
              [...]
            }

### <a name="standalone-events"></a>독립 실행형 이벤트
반대 toosession 이벤트 독립 실행형 이벤트 세션의 hello 컨텍스트 외부에서 발생할 수 있습니다.

**예제:**

브로드캐스트 수신기 트리거될 때 발생 하는 tooreport 이벤트를 원하는 있다고 가정 합니다.

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a>오류 보고
### <a name="session-errors"></a>세션 오류
세션 오류는 일반적으로 사용 되는 tooreport hello 오류 hello 사용자 세션 동안 영향입니다.

**예제:**

            /** hello user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* hello user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a>독립 실행형 오류
반대 toosession 오류 세션의 hello 컨텍스트 외부에서 독립 실행형 오류가 발생할 수 있습니다.

**예제:**

hello 다음 예제에서는 tooreport 오류가 hello 메모리 부족 hello 전화 응용 프로그램 프로세스 동안 될 때마다 실행 하는 방법을

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a>작업 보고
### <a name="example"></a>예제
로그인 프로세스의 기간을 tooreport hello 일정 있다고 가정 합니다.

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a>작업 중 오류 보고
오류 되지 않고 작업을 실행 하는 관련된 tooa 수 toohello 현재 사용자 세션 관련 됩니다.

**예제:**

Tooreport 한다고 가정 하면 수행 하는 동안 로그인 프로세스:

[...] public void signIn(Context context, ...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try toosign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report hello error tooEngagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a>작업 중 이벤트 보고
이벤트 되지 않고 작업을 실행 하는 관련된 tooa 수 toohello 현재 사용자 세션 관련 됩니다.

**예제:**

소셜 네트워크는 한 작업 tooreport hello 총 시간 사용는 hello 하는 동안 사용자가 연결 된 toohello 서버 한다고 가정 합니다. hello 사용자 연결을 유지할 수 백그라운드에서 hello 전화는 절전 모드 또는 다른 응용 프로그램을 사용 하는 경우에 이므로 세션이 없습니다.

hello 사용자 친구에서 메시지를 받을 수, 작업 이벤트입니다.

            [...]
            public void signin(Context context, ...) {
              [...Sign in code...]
              EngagementAgent.getInstance(context).startJob("connection", null);
            }
            [...]
            public void signout(Context context) {
              [...Sign out code...]
              EngagementAgent.getInstance(context).endJob("connection");
            }
            [...]
            public void onMessageReceived(Context context) {
              [...Notify in status bar...]
              EngagementAgent.getInstance(context).sendJobEvent("message_received", "connection", null);
            }
            [...]

## <a name="extra-parameters"></a>extras 매개 변수
임의의 데이터에 연결 된 tooevents, 오류, 활동 및 작업 가능 합니다.

이 데이터는 구조화될 수 있으며, Android의 번들 클래스를 사용합니다. 이 클래스는 실제로 Android Intent의 추가 매개 변수처럼 작동합니다. 번들은 배열이나 다른 번들 인스턴스를 포함할 수 있습니다.

> [!IMPORTANT]
> Parcelable 또는 순차 가능 매개 변수 모드로 전환할 경우 해야 자신의 `toString()` 메서드는 구현 된 tooreturn 사람이 읽을 수는 문자열입니다. `bundle.putSerializable("key",value);`
> 
> [!WARNING]
> 추가 매개 변수의 스파스 배열은 지원되지 않습니다. 즉, 배열로 직렬화되지 않습니다. 추가 매개 변수에서 배열을 사용하기 전에 표준 배열로 변환해야 합니다.
> 
> 

### <a name="example"></a>예제
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a>제한
#### <a name="keys"></a>구성
각 키 hello에 `Bundle` hello 다음 정규식 일치 해야 합니다.

`^[a-zA-Z][a-zA-Z_0-9]*`

즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.

#### <a name="size"></a>크기
추가 항목은 너무 제한**1024** (한 번 인코딩된 json에서 hello Engagement 서비스에 의해) 호출당 문자입니다.

Hello 앞의 예제 JSON 전송 toohello 서버 hello 58 자입니다.

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a>응용 프로그램 정보 보고
Hello를 사용 하 여 정보 (또는 다른 응용 프로그램 관련 정보가) 추적을 수동으로 보고할 수 있습니다 `sendAppInfo()` 함수입니다.

이러한 정보를 점진적으로 보낼 수 있는 참고: 지정된 된 장치에 대 한 지정된 된 키에 대 한 최신 값 hello만 유지 됩니다.

이벤트, 기타 hello 번들 클래스는 응용 프로그램 정보를 사용 하는 tooabstract 마찬가지로 배열 또는 하위 묶습니다 (JSON 직렬화를 사용 하 여) 플랫 문자열으로 처리 됩니다.

### <a name="example"></a>예제
코드 샘플 toosend 사용자 성별 및 생년월일 다음과 같습니다.

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a>제한
#### <a name="keys"></a>구성
각 키 hello에 `Bundle` hello 다음 정규식 일치 해야 합니다.

`^[a-zA-Z][a-zA-Z_0-9]*`

즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.

#### <a name="size"></a>크기
응용 프로그램 정보는 너무 제한적**1024** (한 번 인코딩된 json에서 hello Engagement 서비스에 의해) 호출당 문자입니다.

Hello 앞의 예제 JSON 전송 toohello 서버 hello 44 자입니다.

            {"expiration":"2016-12-07","status":"premium"}
