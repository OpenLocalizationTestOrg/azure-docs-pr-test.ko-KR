---
title: "Mobile Engagement Android SDK 통합 aaaAzure"
description: "Azure Mobile Engagement용 Android SDK의 최신 업데이트 및 절차"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ec3fab3-35ec-458e-bf41-6cdd69e3fa44
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 06/27/2016
ms.author: piyushjo
ms.openlocfilehash: 4ab6143771bdc0758a548abb529d6bde98fc0e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-android"></a>TooIntegrate Engagement Android에 도달 하는 방법
> [!IMPORTANT]
> 이 가이드를 수행 하기 전에 Android에서 Engagement tooIntegrate 문서화 하는 방법을 hello에 설명 된 hello 통합 절차를 따라야 합니다.
> 
> 

## <a name="standard-integration"></a>표준 통합

프로젝트에 hello SDK에서에서 Reach 리소스 파일을 복사 합니다.

* Hello에서 hello 파일 복사 `res/layout` 폴더 hello에 hello SDK로 전달 `res/layout` 응용 프로그램의 폴더입니다.
* Hello에서 hello 파일 복사 `res/drawable` 폴더 hello에 hello SDK로 전달 `res/drawable` 응용 프로그램의 폴더입니다.

`AndroidManifest.xml` 파일을 다음과 같이 편집합니다.

* 다음 단원을 hello 추가 (hello 사이 `<application>` 및 `</application>` 태그).
  
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
              <category android:name="android.intent.category.DEFAULT" />
              <data android:mimeType="text/plain" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
              <category android:name="android.intent.category.DEFAULT" />
              <data android:mimeType="text/html" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
              <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
          </activity>
          <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
            <intent-filter>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
              <category android:name="android.intent.category.DEFAULT"/>
            </intent-filter>
          </activity>
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
            <intent-filter>
              <action android:name="android.intent.action.BOOT_COMPLETED"/>
              <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
              <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
              <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
            </intent-filter>
          </receiver>
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
            <intent-filter>
              <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
            </intent-filter>
          </receiver>
* 부팅 시 클릭 하지 않은이 사용 권한을 tooreplay 시스템 알림이 필요한 (그렇지 않은 경우 디스크에 보관 되지만 더 이상 표시 되지 않습니다, 저장할 필요가 tooinclude이).
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* 복사한 다음 단원을 hello를 편집 하 여 (app 및 시스템 인수 둘 다) 알림에 사용 되는 프로그램 아이콘 지정 (hello 사이 `<application>` 및 `</application>` 태그).
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> 도달률 캠페인을 만들 때 시스템 알림을 사용하려는 경우 이 섹션은 **필수** 입니다. Android는 아이콘이 없는 시스템 알림이 표시되지 않도록 방지합니다. 이 섹션 생략 하면 최종 사용자가 되지 않도록 수 tooreceive 해당 합니다.
> 
> 

* 다음 권한을 tooadd hello 필요한 큰 그림을 사용 하 여 시스템 알림 캠페인을 만드는 경우 (hello 후 `</application>` 태그) 누락 된 경우:
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * Android M에서 응용 프로그램이 Android API level 23 이상을 대상으로 하는 경우 ``WRITE_EXTERNAL_STORAGE`` 권한에 사용자 승인이 필요합니다. [이 섹션](mobile-engagement-android-integrate-engagement.md#android-m-permissions)을 읽어보세요.
* 시스템 알림 hello에 지정할 수 있습니다에 대 한 hello 장치 해야 링 및/또는 진동 경우 캠페인에 도달 합니다. 에 대 한 toowork, 해야 toomake hello 권한 다음 선언 (hello 후 `</application>` 태그).
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  Android 시스템 알림이 표시 되지 않도록이 권한이 없으면 hello 링 또는 hello hello 도달 캠페인 관리자의 옵션 진동를 선택한 경우에 합니다.

## <a name="native-push"></a>네이티브 푸시
Reach 모듈을 구성 했으므로 tooconfigure 네이티브 푸시 toobe 수 tooreceive hello 캠페인 hello 장치에 필요 합니다.

Android에서는 다음 두 가지 서비스를 지원합니다.

* Google Play 장치: 사용 [Google Cloud Messaging] 다음 hello 여 [tooIntegrate Engagement와 GCM 안내 하는 방법을](mobile-engagement-android-gcm-integrate.md) 가이드입니다.
* Amazon 장치: 사용 [Amazon 장치 메시징] 다음 hello 여 [tooIntegrate Engagement와 ADM 안내 하는 방법을](mobile-engagement-android-adm-integrate.md) 가이드입니다.

Tootarget 하려면 Google Play와 Amazon 장치, 해당 가능한 toohave 개발에 대 한 1 AndroidManifest.xml/APK 내의 모든 항목입니다. 하지만 GCM 코드를 찾을 경우 응용 프로그램 tooAmazon를 전송할 때 거부할 수 있습니다.

이러한 경우에는 여러 APK를 사용해야 합니다.

**응용 프로그램 준비 tooreceive 및 디스플레이 캠페인에 도달 하는 이제는!**

## <a name="how-toohandle-data-push"></a>Toohandle 데이터 밀어넣기
### <a name="integration"></a>통합
응용 프로그램 toobe 수 tooreceive Reach 데이터 푸시를 하려면 toocreate의 하위 클래스가 있는 `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` hello에서 참조 하 고 `AndroidManifest.xml` 파일 (hello 사이 `<application>` 및/또는 `</application>` 태그).

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

Hello를 재정의할 수 `onDataPushStringReceived` 및 `onDataPushBase64Received` 콜백 합니다. 다음은 예제입니다.

            public class MyDataPushReceiver extends EngagementReachDataPushReceiver
            {
              @Override
              protected Boolean onDataPushStringReceived(Context context, String category, String body)
              {
                Log.d("tmp", "String data push message received: " + body);
                return true;
              }

              @Override
              protected Boolean onDataPushBase64Received(Context context, String category, byte[] decodedBody, String encodedBody)
              {
                Log.d("tmp", "Base64 data push message received: " + encodedBody);
                // Do something useful with decodedBody like updating an image view
                return true;
              }
            }

### <a name="category"></a>Category
hello 범주 매개 변수의 선택적 데이터 푸시 캠페인을 만들 때 이며 허용 하면 toofilter 데이터 푸시 합니다. 다양 한 유형의 데이터 푸시를 처리 하는 몇 가지 브로드캐스트 수신기가 있는 경우에 유용 하거나 toopush 다양 한 종류의 `Base64` 데이터 및 원하는 tooidentify의 형식으로 구문 분석 하기 전에.

### <a name="callbacks-return-parameter"></a>콜백의 반환 매개 변수
다음은 몇 가지 지침 tooproperly 핸들 hello의 반환 매개 변수 `onDataPushStringReceived` 및 `onDataPushBase64Received`:

* 브로드캐스트 수신기를 반환 해야 `null` hello 콜백에서 toohandle 데이터 밀어넣기 알 수 없는 경우. 브로드캐스트 수신기 여부 hello 데이터 푸시를 처리 해야 하는지 여부를 범주 toodetermine hello를 사용 해야 합니다.
* Hello 브로드캐스트 수신기 중 하나를 반환 해야 `true` hello 콜백에서 hello 데이터 푸시를 허용 하는 경우.
* Hello 브로드캐스트 수신기 중 하나를 반환 해야 `false` hello 콜백에서 hello 데이터 푸시를 인식 하지만 어떤 이유로 든을 무시 합니다. 예를 들어 반환 `false` hello 받은 데이터 유효 하지 않은 경우.
* 하나 브로드캐스트 수신기 반환 하는 경우 `true` 다른 하나를 반환 하는 동안 `false` hello 동일한 데이터 푸시, hello 동작을 정의 하지 않으면에 대 한 안됩니다입니다.

반환 형식은 hello hello Reach 통계에 대해서만 사용 됩니다.

* `Replied`반환 되 hello 브로드캐스트 수신기 중 하나는 증가 `true` 또는 `false`합니다.
* `Actioned`hello 중 브로드캐스트 수신기를 반환 하는 경우에 증가 `true`합니다.

## <a name="how-toocustomize-campaigns"></a>어떻게 toocustomize 캠페인
toocustomize 캠페인 hello Reach SDK에서에서 제공 하는 hello 레이아웃을 수정할 수 있습니다.

Hello 레이아웃에 사용 되는 모든 hello 식별자를 유지 하 고 뷰 텍스트 및 이미지 뷰에 대 한 특히 된 식별자를 사용 하는 hello 뷰의 hello 형식을 유지 해야 합니다. 일부 뷰가 사용된 공간만 toohide 또는 형식별 변경 될 수 있으므로 영역을 보여 줍니다. 제공 된 hello 레이아웃의 toochange hello 유형의 보기를 가져오려는 경우 hello 소스 코드를 확인 하십시오.

### <a name="notifications"></a>알림
두 가지 유형의 알림 즉, 다른 레이아웃 파일을 사용하는 시스템 알림과 앱 내 알림이 있습니다.

#### <a name="system-notifications"></a>시스템 알림
toouse hello 필요한 toocustomize 시스템 알림을 **범주**합니다. 너무를 건너뛸 수 있는[범주](#categories)합니다.

#### <a name="in-app-notifications"></a>앱 내 알림
기본적으로 앱 내 알림이 보기를 동적으로 추가 된 toohello 현재 활동 사용자 인터페이스 감사 toohello Android 메서드가 `addContentView()`합니다. 이 보기를 알림 오버레이라고 합니다. 알림 오버레이 필요 하지 않습니다 toomodify 하면 응용 프로그램에서 모든 레이아웃 때문에 빠른 통합에 매우 유용 합니다.

알림 오버레이 toomodify hello 모양을 수정할 수 hello 파일 `engagement_notification_area.xml` tooyour 필요 합니다.

> [!NOTE]
> hello 파일 `engagement_notification_overlay.xml` 알림 오버레이 hello toocreate 사용된 되는 것은 hello 파일 포함 `engagement_notification_area.xml`합니다. 또한 사용자 지정할 수 있습니다 toosuit 요구 사항 (예: hello 오버레이 내 hello 알림 영역 위치 지정).
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a>작업 레이아웃의 일부로 알림 레이아웃 포함
오버레이는 빠른 통합에 적절하지만 특수한 경우에는 불편해지거나 부작용이 있을 수 있습니다. hello 오버레이 시스템은 특수 한 작업에 대 한 쉬운 tooprevent 의도 하는 작업 수준에서 사용자 지정할 수 있습니다.

기존 프로그램 레이아웃 감사 toohello Android에서에서 tooinclude 우리의 알림 레이아웃을 결정할 수 있습니다 **포함** 문. hello 다음은 수정 된의 예가 `ListActivity` 레이아웃만 포함 하는 `ListView`합니다.

**Engagement 통합 이전:**

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

**Engagement 통합 이후:**

            <?xml version="1.0" encoding="utf-8"?>
            <LinearLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <ListView
                android:id="@android:id/list"
                android:layout_width="fill_parent"
                android:layout_height="fill_parent"
                android:layout_weight="1" />

              <include layout="@layout/engagement_notification_area" />

            </LinearLayout>

이 예에서 hello 원래 레이아웃 hello 최상위 요소는 목록 보기 사용 있으므로 부모 컨테이너를 추가 합니다. 또한 추가 `android:layout_weight="1"` toobe 수 tooadd 목록 보기 아래에서 보기를 사용 하 여 구성 `android:layout_height="fill_parent"`합니다.

hello Engagement Reach SDK는 해당 hello 알림 레이아웃이이 활동에 포함 되 고이 작업에 대 한 오버레이 추가 하지 않는 것에 자동으로 검색 합니다.

> [!TIP]
> 응용 프로그램에 ListActivity를 사용 하는 경우 표시 Reach 오버레이 수 없게 됩니다 응답할 tooclicked hello 목록 뷰의 항목에서 더 이상. 이는 알려진 문제입니다. toowork이이 문제를 해결 하는 좋습니다 hello 이전 샘플에서와 같은 고유한 목록 활동 레이아웃에서 tooembed hello 알림 레이아웃 합니다.
> 
> 

##### <a name="disabling-application-notification-per-activity"></a>작업별 응용 프로그램 알림 비활성화
Hello를 표시 하지 않으려는 경우 오버레이 toobe tooyour 활동을 추가 하 고 자체 레이아웃에 hello 알림 레이아웃을 포함 하지 않으면,이 활동 hello에 대 한 hello 오버레이 비활성화할 수 있습니다 `AndroidManifest.xml` 추가 하 여 한 `meta-data` hello 다음과에서 같은 섹션 예:

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <a name="categories"></a> 범주
레이아웃을 제공 하는 hello를 수정 하는 경우 모든 알림 hello 모양을 수정 합니다. 범주를 사용 toodefine 대상 다양 한 알림 (가능 동작)을 찾습니다. 도달률 캠페인을 만들 때 범주를 지정할 수 있습니다. 범주를 사용하면 알림과 설문 조사도 사용자 지정할 수 있습니다. 여기에 대해서는 이 문서의 뒷부분에서 설명합니다.

알림에 대 한 범주 처리기 tooregister 해야 tooadd 호출 hello 응용 프로그램 초기화 될 때.

> [!IMPORTANT]
> Hello android: 프로세스 특성에 대 한 hello 경고를 읽어 보십시오 \<android sdk-engagement 프로세스\> hello에 어떻게 진행 하기 전에 Android 주제에 참여 tooIntegrate 합니다.
> 
> 

hello 다음 예에서는 가정 hello 이전 경고를 승인 하 고의 하위 클래스를 사용 하 여 `EngagementApplication`:

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), "myCategory");
              }
            }

hello `MyNotifier` 개체는 hello 알림 범주 처리기의 hello 구현 합니다. 이 알고리즘은 구현한의 hello `EngagementNotifier` 인터페이스 또는 하위 클래스의 기본 구현은 hello: `EngagementDefaultNotifier`합니다.

같은 알림 hello는 여러 종류를 처리할 수 있는, 다음과 같이 등록할 수 있습니다.

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

tooreplace hello 기본 범주 구현 hello 다음 예제에서에서와 같은 구현을 등록할 수 있습니다.

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), Intent.CATEGORY_DEFAULT); // "android.intent.category.DEFAULT"
              }
            }

처리기에서 사용 되는 hello 현재 범주에서 재정의할 수 메서드에 대부분 매개 변수로 전달 `EngagementDefaultNotifier`합니다.

그 범주는`String` 매개 변수로 전달되거나 `getCategory()` 메서드가 있는 `EngagementReachContent` 개체에서 간접적으로 전달됩니다.

메서드를 재정의 하 여 hello 알림 생성 프로세스의 대부분을 변경할 수 있습니다 `EngagementDefaultNotifier`고급 사용자 지정 느껴집니다 무료 tootake hello 기술 문서 및 hello 소스 코드에서 참조에 대 한 합니다.

##### <a name="in-app-notifications"></a>앱 내 알림
특정 범주에 대 한 대체 레이아웃 toouse만 하려는 경우 다음 예제는 hello와 같이이 구현할 수 있습니다.

            public class MyNotifier extends EngagementDefaultNotifier
            {
              public MyNotifier(Context context)
              {
                super(context);
              }

              @Override
              protected int getOverlayLayoutId(String category)
              {
                return R.layout.my_notification_overlay;
              }


              @Override
              public Integer getOverlayViewId(String category)
              {
                return R.id.my_notification_overlay;
              }

              @Override
              public Integer getInAppAreaId(String category)
              {
                return R.id.my_notification_area;
              }
            }

**`my_notification_overlay.xml`의 예제 :**

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

볼 수 있듯이 hello 오버레이 뷰 식별자는 hello 표준 하나 보다 차이가 있습니다. 각 레이아웃에서 오버레이에 고유 식별자를 사용하는 것이 중요합니다.

**`my_notification_area.xml`의 예제 :**

            <?xml version="1.0" encoding="utf-8"?>
            <merge
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <RelativeLayout
                android:id="@+id/my_notification_area"
                android:layout_width="fill_parent"
                android:layout_height="64dp"
                android:layout_alignParentTop="true"
                android:background="#B000">

                <LinearLayout
                  android:orientation="horizontal"
                  android:layout_width="fill_parent"
                  android:layout_height="fill_parent"
                  android:gravity="center_vertical">

                  <ImageView
                    android:id="@+id/engagement_notification_icon"
                    android:layout_width="48dp"
                    android:layout_height="48dp" />

                  <LinearLayout
                    android:id="@+id/engagement_notification_text"
                    android:orientation="vertical"
                    android:layout_width="fill_parent"
                    android:layout_height="fill_parent"
                    android:layout_weight="1"
                    android:gravity="center_vertical">

                    <TextView
                      android:id="@+id/engagement_notification_title"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:singleLine="true"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Medium" />

                    <TextView
                      android:id="@+id/engagement_notification_message"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:maxLines="2"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Small" />

                  </LinearLayout>

                  <ImageView
                    android:id="@+id/engagement_notification_image"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:adjustViewBounds="true" />

                  <ImageButton
                    android:id="@+id/engagement_notification_close_area"
                    android:visibility="invisible"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:src="@android:drawable/btn_dialog"
                    android:background="#0F00" />

                </LinearLayout>

                <ImageButton
                  android:id="@+id/engagement_notification_close"
                  android:layout_width="wrap_content"
                  android:layout_height="fill_parent"
                  android:layout_alignParentRight="true"
                  android:src="@android:drawable/btn_dialog"
                  android:background="#0F00" />

              </RelativeLayout>

            </merge>

볼 수 있듯이 hello 알림 영역 보기 식별자는 hello 표준 하나 보다 차이가 있습니다. 각 레이아웃에서 알림 영역에 고유 식별자를 사용하는 것이 중요합니다.

응용 프로그램 (또는 앱에서) 알림 hello 위쪽 hello 화면에 표시 하는 범주에 속하는 간단한 예제입니다. 우리는 hello 표준 식별자 자체 hello 알림 영역에 사용 되는 변경 되지 않았습니다.

Toochange, 있다고 tooredefine hello를 원하는 경우 `EngagementDefaultNotifier.prepareInAppArea` 메서드. 것이 좋습니다 toolook hello 기술 문서 및의 hello 소스 코드에서 `EngagementNotifier` 및 `EngagementDefaultNotifier` 하려는 경우이 고급 사용자 지정의 수준입니다.

##### <a name="system-notifications"></a>시스템 알림
확장 하 여 `EngagementDefaultNotifier`를 재정의할 수 있습니다 `onNotificationPrepared` hello 기본 구현에서 사용 했던 tooalter hello 알림입니다.

예:

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

이 예제에서는 hello "진행 중" 범주를 사용할 때 진행 중인 이벤트로 표시 되는 콘텐츠에 대 한 시스템 알림.

Toobuild hello를 원하는 경우 `Notification` 개체 처음부터 반환할 수 있습니다 `false` toohello 메서드와 호출 `notify` hello에 직접 `NotificationManager`합니다. 유지 해야 하는 경우에 `contentIntent`, `deleteIntent` 알림 식별자에서 사용 하는 hello 및 `EngagementReachReceiver`합니다.

다음은 그러한 구현에 대한 올바른 예제입니다.

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content) throws RuntimeException
            {
              /* Required fields */
              NotificationCompat.Builder builder = new NotificationCompat.Builder(mContext)
                .setSmallIcon(notification.icon)              // icon is mandatory
                .setContentIntent(notification.contentIntent) // keep content intent
                .setDeleteIntent(notification.deleteIntent);  // keep delete intent

              /* Your customization */
              // builder.set...

              /* Dismiss option can be managed only after build */
              Notification myNotification = builder.build();
              if (!content.isNotificationCloseable())
                myNotification.flags |= Notification.FLAG_NO_CLEAR;

              /* Notify here instead of super class */
              NotificationManager manager = (NotificationManager) mContext.getSystemService(Context.NOTIFICATION_SERVICE);
              manager.notify(getNotificationId(content), myNotification); // notice hello call tooget hello right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a>공지만 알림
hello hello의 관리를 클릭 하는 알림 전용 알림을 재정의 하 여 사용자 지정할 수 있습니다 `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` 준비 toomodify hello `Intent`합니다. 이 메서드를 사용 하 여 있습니다 tootune hello 플래그를 쉽게.

예를 들어 tooadd hello `SINGLE_TOP` 플래그:

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

레거시 Engagement 사용자에 대 한 동작 없이 시스템 알림 URL 이제가 실행 하는 hello 응용 프로그램 작업 URL 없이 공지 사항으로이 메서드를 호출할 수 있으므로 백그라운드에서 되었으면 note 하십시오. Hello 의도 사용자 지정할 때를 고려해 야 합니다.

또한 `EngagementNotifier.executeNotifAnnouncementAction` 을(를) 처음부터 구현할 수도 있습니다.

##### <a name="notification-life-cycle"></a>알림 수명 주기
Hello에서 일부 수명 주기 메서드를 호출 hello 기본 범주를 사용할 경우 `EngagementReachInteractiveContent` tooreport 통계 및 업데이트 hello 캠페인 상태 개체:

* Hello 알림을 응용 프로그램에 표시 하거나 hello 상태 표시줄에 배치할 때 hello `displayNotification` (보고 하는 통계) 메서드를 호출 하 여 `EngagementReachAgent` 경우 `handleNotification` 반환 `true`합니다.
* Hello 알림은 해제 하는 경우 hello `exitNotification` 메서드는 통계는 보고 되며 다음 캠페인을 지금 처리할 수 있습니다.
* Hello 알림의 클릭할 경우 `actionNotification` 은 호출 통계는 보고 되 고 연결 된 hello 의도 실행 됩니다.

경우 구현 `EngagementNotifier` 바이패스 hello 기본 동작, 혼자서 toocall 이러한 수명 주기 메서드를가지고 있어야 합니다. 다음 예제는 hello hello 기본 동작이 사용 하지 않을 경우를 보여 줍니다.

* 범주 처리를 처음부터 구현한 경우처럼 `EngagementDefaultNotifier`을(를) 확장하지 않은 경우
* Hello를 문제가 시스템 알림에 대해 `onNotificationPrepared` 수정한 및 `contentIntent` 또는 `deleteIntent` hello에 `Notification` 개체입니다.
* 가 앱에서 알림을 `prepareInAppArea`있는지 toomap 사이, `actionNotification` U.I 컨트롤의 tooone 합니다.

> [!NOTE]
> 경우 `handleNotification` hello 콘텐츠 예외가 throw는 삭제 및 `dropContent` 라고 합니다. 이 사항은 통계로 보고되며 이제 다음 캠페인을 처리할 수 있습니다.
> 
> 

### <a name="announcements-and-polls"></a>알림 및 설문 조사
#### <a name="layouts"></a>레이아웃
Hello를 수정할 수 있습니다 `engagement_text_announcement.xml`, `engagement_web_announcement.xml` 및 `engagement_poll.xml` toocustomize 텍스트 공지, 웹 공지 및 설문 조사의 파일입니다.

이러한 파일 hello 제목 영역 및 hello 단추 영역에 대 한 두 가지 일반적인 레이아웃을 공유합니다. hello 제목에 대 한 hello 레이아웃은 `engagement_content_title.xml` 및 사용 하 여 hello hello 배경에 대 한 호응 그릴 수 있는 파일입니다. hello hello 작업 및 끝내기 단추 레이아웃은 `engagement_button_bar.xml` 및 사용 하 여 hello hello 배경에 대 한 호응 그릴 수 있는 파일입니다.

에 설문 조사 질문 레이아웃 hello 및 선택 항목은 동적으로 확장 하 여 여러 번 hello를 사용 하 여 `engagement_question.xml` hello 질문과 hello에 대 한 레이아웃 파일 `engagement_choice.xml` hello 선택 항목에 대 한 파일입니다.

#### <a name="categories"></a>범주
##### <a name="alternate-layouts"></a>대체 레이아웃
알림, 같이 hello 캠페인의 범주는 공지 및 설문 조사의 toohave 사용 되는 대체 레이아웃 일 수 있습니다.

예를 들어 toocreate 텍스트 공지에 대 한 범주를 확장할 수 있습니다 `EngagementTextAnnouncementActivity` hello 참조 `AndroidManifest.xml` 파일:

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

참고이 hello 범주 hello 의도에 필터를 사용 toomake hello 차이 hello 기본 알림 활동을 포함 합니다.

Reach SDK hello hello 의도 시스템 tooresolve hello 오른쪽 활동을 사용 하 여 특정 범주에 대 한 및 대체 hello 기본 범주에 hello 확인에 실패 한 경우.

Tooimplement 있는 `MyCustomTextAnnouncementActivity`, 방금 toochange hello 레이아웃 (하지만 hello 식별자 동일한 보기 유지), 하기만 하면 같은 toodefine hello 클래스에 다음 예제는 hello:

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class toouse R.layout.my_text_announcement
              }
            }

텍스트 공지 tooreplace hello 기본 범주를 바꾸면 `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` 구현에 따라 합니다.

웹 알림 및 설문 조사는 유사한 방식으로 사용자 지정할 수 있습니다.

확장할 수에 대 한 웹 알림을 `EngagementWebAnnouncementActivity` hello에서 활동이 선언 `AndroidManifest.xml` hello 다음 예제에서에서와 같이:

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in hello intent is hello data mime type -->
              </intent-filter>
            </activity>

폴링 확장 `EngagementPollActivity` 프로그램에 hello를 선언 하 고 `AndroidManifest.xml` hello 다음 예제에서에서와 같이:

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a>처음부터 구현
Hello 중 하나를 확장 하지 않고 알림 (및 설문 조사) 작업에 대 한 범주를 구현할 수 `Engagement*Activity` Reach SDK를 hello 클래스에서 제공 합니다. 이 유용한 예를 들어 toodefine hello 표준 레이아웃으로 동일한 뷰 hello를 사용 하지 않는 레이아웃 하려는 경우입니다.

와 같은 고급 알림 사용자 지정을 위한 것이 좋습니다 toolook hello 표준 구현의 hello 소스 코드에서.

다음 일부의 tookeep 염두에서은: Reach hello 콘텐츠 식별자는 추가 매개 변수가 더하기 hello 활동 특정 의도 (해당 toohello 의도 필터)가 시작 됩니다.

때 hello 만들기는 캠페인 hello 웹 사이트에서 사용자 지정한 hello 필드가 포함 된 tooretrieve hello 콘텐츠 개체를 수행 됩니다.

            public class MyCustomTextAnnouncement extends EngagementActivity
            {
              private EngagementAnnouncement mContent;

              @Override
              protected void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);

                /* Get content */
                mContent = EngagementReachAgent.getInstance(this).getContent(getIntent());
                if (mContent == null)
                {
                  /* If problem with content, exit */
                  finish();
                  return;
                }

                setContentView(R.layout.my_text_announcement);

                /* Configure views by querying fields on mContent */
                // ...
              }
            }

Hello에 hello 내용이 표시 되 보고 해야 통계의 경우 `onResume` 이벤트:

            @Override
            protected void onResume()
            {
             /* Mark hello content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

그런 다음 반드시 toocall 하거나 `actionContent(this)` 또는 `exitContent(this)` hello 활동 배경으로 모드로 전환 되기 전에 hello 콘텐츠 개체에 합니다.

호출 하지 않으면 `actionContent` 또는 `exitContent`, 통계 전송 되지 않습니다. (예: hello 캠페인에 없는 분석) 및 더 중요 한 사실은 hello hello 응용 프로그램 프로세스를 다시 시작 될 때까지 다음 캠페인을 받을 수 없습니다.

방향 또는 기타 구성 변경 내용을 hello 코드 까다로운 toodetermine 여부 hello 활동 배경 진입 여부, 수 있는지 hello 콘텐츠가 보고 되는 hello 사용자가 (하거나 hello 활동 끝났습니다 표준 구현을 사용 하면 hello 키를 누르면 `HOME` 또는 `BACK`) 하지만 not hello 방향을 변경 합니다.

다음은 hello 구현의 hello 흥미로운 부분이입니다.

            @Override
            protected void onUserLeaveHint()
            {
              finish();
            }

            @Override
            protected void onPause()
            {
              if (isFinishing() && mContent != null)
              {
                /*
                 * Exit content on exit, this is has no effect if another process method has already been
                 * called so we don't have toocheck anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

호출 하면 볼 수 있듯이 `actionContent(this)` hello 활동을 완료 한 후 `exitContent(this)` 영향을 주지 않고 안전 하 게 호출할 수 있습니다.

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html
[Amazon 장치 메시징]:https://developer.amazon.com/sdk/adm.html
