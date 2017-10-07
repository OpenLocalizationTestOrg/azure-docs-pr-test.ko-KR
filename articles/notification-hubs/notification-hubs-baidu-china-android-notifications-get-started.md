---
title: "aaaGet Baidu를 사용 하 여 Azure 알림 허브 시작 | Microsoft Docs"
description: "이 자습서에 설명 방법을 Baidu를 사용 하 여 toouse Azure 알림 허브 toopush 알림 tooAndroid 장치입니다."
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 23bde1ea-f978-43b2-9eeb-bfd7b9edc4c1
ms.service: notification-hubs
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: mobile-baidu
ms.workload: mobile
ms.date: 08/19/2016
ms.author: yuaxu
ms.openlocfilehash: 2767fdd3bb04674e7a531634237cc05cd8c21cb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a>Baidu를 사용하여 Notification Hubs 시작
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>개요
Baidu 클라우드 푸시는 중국어 클라우드 서비스 toosend 푸시 알림을 toomobile 장치를 사용할 수 있습니다. 이 서비스는 중국, 여기서 다양 한 앱 저장소 및 푸시의 hello 존재 tooAndroid 되어 복잡 한 푸시 알림 배달 서비스, 또한 Android 하지 않는 장치는 일반적으로 연결 된 tooGCM (Google의 toohello 가용성에서 유용 클라우드 메시징)입니다.

## <a name="prerequisites"></a>필수 조건
이 자습서를 사용하려면 다음이 필요합니다.

* Android SDK (가정 Eclipse를 사용 하는) hello에서 다운로드할 수 있는 <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android 사이트</a>
* [Mobile Services Android SDK]
* [Baidu 푸시 Android SDK]

> [!NOTE]
> toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F)을 참조하세요.
> 
> 

## <a name="create-a-baidu-account"></a>Baidu 계정 만들기
Baidu toouse Baidu 계정이 있어야 합니다. 이미 있는 경우, toohello 로그인 [Baidu 포털] toohello 다음 단계를 건너뛰고 있습니다. 그렇지 않으면 hello 방법에 대 한 지침을 참조 toocreate Baidu 계정.  

1. Toohello 이동 [Baidu 포털] hello 클릭**登录**(**로그인**) 링크 합니다. 클릭**立即注册**toostart hello 계정 등록 프로세스.
   
   ![][1]
2. 필요한 hello 세부 정보를 입력-전화/전자 메일 주소, 암호 및 확인 코드-클릭 **등록**합니다.
   
   ![][2]
3. 하면 받게 될 전자 메일 toohello 전자 메일 주소를 입력 했는지와 링크 tooactivate Baidu 계정.
   
   ![][3]
4. tooyour 전자 메일 계정, hello Baidu 활성화 메일을 열고 고 hello 활성화 링크 tooactivate Baidu 계정을 클릭 합니다.
   
   ![][4]

활성화 된 Baidu 계정 있으면 toohello 로그인 [Baidu 포털]합니다.

## <a name="register-as-a-baidu-developer"></a>Baidu 개발자로 등록
1. Toohello에 로그인 한 후 [Baidu 포털], 클릭**更多 >>** (**자세한**).
   
      ![][5]
2. Hello에서 아래로 스크롤하여**站长与开发者服务 (개발자 서비스 및 웹 마스터)** 섹션 및 클릭**百度开放云平台**(**Baidu 클라우드 플랫폼을 열고**).
   
      ![][6]
3. Hello 다음 페이지에서 클릭**开发者服务**(**개발자 서비스**) hello 오른쪽 위 모퉁이에 있습니다.
   
      ![][7]
4. Hello 다음 페이지에서 클릭**注册开发者**(**등록 개발자**) hello 오른쪽 위 모퉁이에 hello 메뉴에서 합니다.
   
      ![][8]
5. 이름, 설명 및 확인 문자 메시지를 수신할 휴대폰 번호를 입력하고 **送验证码**(**확인 코드 보내기**)를 클릭합니다. 국제 전화 번호에 대 한 괄호 안에 tooenclose hello 국가 코드가 필요 합니다. 예를 들어 미국 번호는 **(1)1234567890**입니다.
   
      ![][9]
6. 다음 hello 다음 예제에에서 나와 있는 것 처럼 확인 번호와 함께 텍스트 메시지를 받게 됩니다.
   
      ![][10]
7. Hello 메시지에서 hello 확인 번호 입력**验证码**(**확인 코드**).
8. 마지막으로, hello Baidu 계약을 수락 하 고 클릭 하 여 hello 개발자 등록을 완료**提交**(**전송**). Hello 등록 성공적으로 완료 되는 페이지 다음에 대해 표시 됩니다.
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a>Baidu 클라우드 푸시 프로젝트 만들기
Baidu 클라우드 푸시 프로젝트를 만들면 앱 ID, API 키 및 비밀 키를 받게 됩니다.

1. Toohello에 로그인 한 후 [Baidu 포털], 클릭**更多 >>** (**자세한**).
   
      ![][5]
2. Hello에서 아래로 스크롤하여**站长与开发者服务**(**개발자 서비스 및 웹 마스터**) 섹션 및 클릭**百度开放云平台**(**Baidu 클라우드 플랫폼을 열고**).
   
      ![][6]
3. Hello 다음 페이지에서 클릭**开发者服务**(**개발자 서비스**) hello 오른쪽 위 모퉁이에 있습니다.
   
      ![][7]
4. Hello 다음 페이지에서 클릭**云推送**(**클라우드 푸시**) hello에서**云服务**(**클라우드 서비스**) 섹션.
   
      ![][12]
5. 등록 된 개발자 인 경우 되 면 참조**管理控制台**(**관리 콘솔**) hello 상단 메뉴에서 합니다. **开发者服务管理**(**개발자 서비스 관리**)를 클릭합니다.
   
      ![][13]
6. Hello 다음 페이지에서 클릭**创建工程**(**프로젝트 만들기**).
   
      ![][14]
7. 응용 프로그램 이름을 입력하고 **创建**(**만들기**)를 클릭합니다.
   
      ![][15]
8. Baidu 클라우드 푸시 프로젝트를 성공적으로 만들면 **AppID**, **API 키** 및 **비밀 키**가 포함된 페이지가 표시됩니다. 적어 hello API 키 및 비밀 키를 나중에 사용 합니다.
   
      ![][16]
9. 클릭 하 여 푸시 알림에 hello 프로젝트 구성**云推送**(**클라우드 푸시**) hello 왼쪽된 창에서.
   
      ![][31]
10. Hello 다음 페이지에서 클릭 hello**推送设置**(**설정을 푸시**) 단추입니다.
    
    ![][32]  
11. Hello 구성 페이지에서 추가 hello에서 Android 프로젝트에서 사용 하 여 hello 패키지 이름을**应用包名**(**응용 프로그램 패키지**) 필드를 선택한 다음 클릭**保存设置**드 ( **저장**).  
    
    ![][33]

Hello 참조**保存成功!**(**성공적으로 저장했습니다!**) 메시지가 나타납니다.

## <a name="configure-your-notification-hub"></a>알림 허브 구성
1. Toohello 로그인 [Azure 클래식 포털], 클릭 하 고 **+ 새로 만들기** hello hello 화면 맨 아래에 있습니다.
2. **App Services**, **Service Bus**, **Notification Hub** 및 **빠른 생성**을 차례로 클릭합니다.
3. 에 대 한 이름을 제공 하면 **알림 허브**을 선택 hello **지역** 및 hello **Namespace** 여기이 알림 허브를 만들 한 다음 클릭  **새 알림 허브 만들기**합니다.  
   
      ![][17]
4. 알림 허브를 만든 hello 네임 스페이스를 클릭 한 다음 클릭 **알림 허브** hello 위쪽에 있습니다.
   
      ![][18]
5. 생성을 클릭 한 다음 선택 hello 알림 허브 **구성** hello 상단 메뉴에서 합니다.
   
      ![][19]
6. Toohello 아래로 스크롤하여 **baidu 알림 설정** 섹션 고 hello API 키와 가져온 hello Baidu 콘솔에서 이전에 프로그램 Baidu 클라우드 푸시 프로젝트에 대 한 비밀 키를 입력 합니다. **Save**를 클릭합니다.
   
      ![][20]
7. Hello 클릭 **대시보드** hello 알림 허브에 대 한 hello 위쪽 탭을 클릭 한 다음 **연결 문자열 보기**합니다.
   
      ![][21]
8. Hello 메모 **DefaultListenSharedAccessSignature** 및 **DefaultFullSharedAccessSignature** hello에서 **연결 정보에 액세스** 창.
   
    ![][22]

## <a name="connect-your-app-toohello-notification-hub"></a>응용 프로그램 toohello 알림 허브를 연결 합니다.
1. Eclipse ADT에서 새로운 Android 프로젝트를 만듭니다(**파일** > **새로 만들기** > **Android 응용 프로그램 프로젝트**).
   
    ![][23]
2. 입력 한 **응용 프로그램 이름** 해당 hello 확인 **최소 필요한 SDK** 버전이 너무 설정 되어**API 16: Android 4.1**합니다.
   
    ![][24]
3. 클릭 **다음** hello 마법사 hello 될 때까지 다음 계속 **만들 활동** 창이 나타납니다. 다음 사항을 확인 **빈 활동** 가 선택 마지막으로 선택 **마침** toocreate 새 Android 응용 프로그램입니다.
   
    ![][25]
4. 해당 hello 있는지 확인 **프로젝트 빌드 대상** 올바르게 설정 되어 있습니다.
   
    ![][26]
5. Hello에서 hello 0.4.jar 허브-알림-파일을 다운로드 **파일** hello 탭 [알림-허브-Android-SDK Bintray에](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4)합니다. Hello 파일 toohello 추가 **libs** Eclipse 프로젝트 및 새로 고침 hello 폴더 *libs* 폴더입니다.
6. 다운로드 하 고 hello 압축을 풀면 [Baidu 푸시 Android SDK]개방형 hello **libs** 폴더를 연 다음 복사 hello **pushservice x.y.z 형식이 며** jar 파일 및 hello **armeabi**  &  **mips** 폴더 hello에 **libs** Android 응용 프로그램의 폴더입니다.
7. 열기 hello **AndroidManifest.xml** 파일의 Android 프로젝트를 마우스 hello Baidu SDK에서 필요로 하는 hello 사용 권한을 추가 합니다.
   
        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.READ_PHONE_STATE" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.WRITE_SETTINGS" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
        <uses-permission android:name="android.permission.DISABLE_KEYGUARD" />
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name="android.permission.ACCESS_DOWNLOAD_MANAGER" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />
8. Hello 추가 **android: name** 속성 tooyour **응용 프로그램** 요소 **AndroidManifest.xml**, 대체 *yourprojectname* ( 예제에서는 **com.example.BaiduTest**). 이 프로젝트 이름을 hello Baidu 콘솔에서 구성한 하나 hello 일치 하는지 확인 합니다.
   
        <application android:name="yourprojectname.DemoApplication"
9. Hello 같은 hello 후 hello 응용 프로그램 요소에 구성이 추가 **합니다. MainActivity** 활동 요소 대체 *yourprojectname* (예를 들어 **com.example.BaiduTest**):
   
        <receiver android:name="yourprojectname.MyPushMessageReceiver">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.MESSAGE" />
                <action android:name="com.baidu.android.pushservice.action.RECEIVE" />
                <action android:name="com.baidu.android.pushservice.action.notification.CLICK" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.PushServiceReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED" />
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
                <action android:name="com.baidu.android.pushservice.action.notification.SHOW" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.RegistrationReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.METHOD" />
                <action android:name="com.baidu.android.pushservice.action.BIND_SYNC" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.intent.action.PACKAGE_REMOVED"/>
                <data android:scheme="package" />
            </intent-filter>
        </receiver>
   
        <service
            android:name="com.baidu.android.pushservice.PushService"
            android:exported="true"
            android:process=":bdservice_v1"  >
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.PUSH_SERVICE" />
            </intent-filter>
        </service>
10. 라는 새 클래스 추가 **ConfigurationSettings.java** toohello 프로젝트.
    
     ![][28]
    
     ![][29]
11. 다음 코드 tooit hello를 추가 합니다.
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    hello 값 설정 **API_KEY** 내용 검색 hello Baidu 클라우드 프로젝트에서 이전 버전에서와 **NotificationHubName** hello Azure 클래식 포털에서에서 알림 허브 이름으로 및  **NotificationHubConnectionString** DefaultListenSharedAccessSignature hello Azure 클래식 포털에서에서 사용 합니다.
12. 라는 새 클래스 추가 **DemoApplication.java**, 다음 코드 tooit hello 추가:
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. 이라는 다른 새 클래스를 추가 **MyPushMessageReceiver.java**, 다음 코드 tooit hello를 추가 합니다. 핸들 hello hello Baidu 푸시 서버 로부터 받은 푸시 알림을 hello 클래스입니다.
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG tooLog */
            public static NotificationHub hub = null;
            public static String mChannelId, mUserId;
            public static final String TAG = MyPushMessageReceiver.class
                    .getSimpleName();
    
            @Override
            public void onBind(Context context, int errorCode, String appid,
                    String userId, String channelId, String requestId) {
                String responseString = "onBind errorCode=" + errorCode + " appid="
                        + appid + " userId=" + userId + " channelId=" + channelId
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
                mChannelId = channelId;
                mUserId = userId;
    
                try {
                    if (hub == null) {
                        hub = new NotificationHub(
                                ConfigurationSettings.NotificationHubName,
                                ConfigurationSettings.NotificationHubConnectionString,
                                context);
                        Log.i(TAG, "Notification hub initialized");
                    }
                } catch (Exception e) {
                   Log.e(TAG, e.getMessage());
                }
    
                registerWithNotificationHubs();
            }
    
            private void registerWithNotificationHubs() {
               new AsyncTask<Void, Void, Void>() {
                  @Override
                  protected Void doInBackground(Void... params) {
                     try {
                         hub.registerBaidu(mUserId, mChannelId);
                         Log.i(TAG, "Registered with Notification Hub - '"
                                 + ConfigurationSettings.NotificationHubName + "'"
                                 + " with UserId - '"
                                 + mUserId + "' and Channel Id - '"
                                 + mChannelId + "'");
                     } catch (Exception e) {
                         Log.e(TAG, e.getMessage());
                     }
                     return null;
                 }
               }.execute(null, null, null);
            }
    
            @Override
            public void onSetTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onSetTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onDelTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onDelTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onListTags(Context context, int errorCode, List<String> tags,
                    String requestId) {
                String responseString = "onListTags errorCode=" + errorCode + " tags="
                        + tags;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onUnbind(Context context, int errorCode, String requestId) {
                String responseString = "onUnbind errorCode=" + errorCode
                        + " requestId = " + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onNotificationClicked(Context context, String title,
                    String description, String customContentString) {
                String notifyString = "title=\"" + title + "\" description=\""
                        + description + "\" customContent=" + customContentString;
                Log.d(TAG, notifyString);
            }
    
            @Override
            public void onMessage(Context context, String message,
                    String customContentString) {
                String messageString = "message=\"" + message + "\" customContentString=" + customContentString;
                Log.d(TAG, messageString);
            }
        }
14. 열기 **MainActivity.java**, hello toohello 다음 추가 **onCreate** 메서드:
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. 다음 가져오기 조건 hello 위쪽 hello를 엽니다.
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-tooyour-app"></a>보낼 알림 tooyour 앱
Hello에 알림을 전송 하 여 앱에서 알림 받기 신속 하 게 테스트할 수 있습니다 [Azure 포털](https://portal.azure.com/) hello를 사용 하 여 **보낼** hello 화면에 다음 그림과 같이 hello 알림 허브에서 단추:

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

푸시 알림은 일반적으로 호환 라이브러리를 사용하는 Mobile Services 또는 ASP.NET과 같은 백 엔드 서비스에서 전송됩니다. Hello REST API를 사용할 수는 라이브러리에 백 엔드에 대해 사용할 수 없는 경우 직접 toosend 알림 메시지입니다.

이 자습서에서는 단순하게 유지 하 고 방금 hello.NET SDK를 사용 하 여 백 엔드 서비스는 대신 콘솔 응용 프로그램에서 알림 허브에 대 한 알림을 전송 하 여 클라이언트 앱을 테스트 보여 줍니다. Hello 권장 [사용 하 여 알림 허브 toopush 알림 toousers](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) ASP.NET 백 엔드에서 알림을 보내기 위한 hello 다음 단계로 자습서입니다. 그러나 다음 방법 hello 알림을 보내는 데 사용할 수 있습니다.

* **REST 인터페이스**: hello를 사용 하 여 모든 백 엔드 플랫폼에서 알림을 지원할 수 있습니다 [REST 인터페이스](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx)합니다.
* **Microsoft Azure 알림 허브.NET SDK**: Visual Studio 용 Nuget 패키지 관리자 hello 실행 [Install-package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)합니다.
* **Node.js**: [어떻게 toouse Node.js에서 알림 허브](notification-hubs-nodejs-push-notification-tutorial.md)합니다.
* **모바일 앱**: 방법의 예에 대 한 알림 허브와 통합 된 Azure 앱 서비스 모바일 앱 백 엔드에서 toosend 알림을 참조 [추가 tooyour 모바일 앱 푸시 알림](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md)합니다.
* **Java / PHP**: toosend 알림을 사용 하 여 REST Api를 hello 하는 방법의 예제를 보려면 "어떻게 toouse Java/PHP에서 알림 허브" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

## <a name="optional-send-notifications-from-a-net-console-app"></a>(선택 사항) .NET 콘솔 응용 프로그램에서 알림 보내기
이 섹션에서는 .NET 콘솔 앱을 사용하여 알림을 전송하는 방법을 보여줍니다.

1. 새 Visual C# 콘솔 응용 프로그램을 만듭니다.
   
    ![][30]
2. Hello 패키지 관리자 콘솔 창에서에서 설정 hello **기본 프로젝트** tooyour 새 콘솔 응용 프로그램 프로젝트를 선택한 다음 hello 콘솔 창에 다음 명령을 hello를 실행 합니다.
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    이 명령은 추가 참조 toohello Azure 알림 허브 SDK hello를 사용 하 여 <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification 허브 NuGet 패키지</a>합니다.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. 파일 열기 hello **Program.cs** hello 다음 추가 및 문을 사용 하 여:
   
        using Microsoft.Azure.NotificationHubs;
4. 프로그램 `Program` 클래스, 메서드 뒤 hello를 추가 하 고, 바꿀 *DefaultFullSharedAccessSignatureSASConnectionString* 및 *NotificationHubName* hello 값이 적용 해야 합니다.
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. Hello 뒤에 있는 줄을 추가 하면 **Main** 메서드:
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a>앱 테스트
정당한는 실제 휴대폰으로이 응용 프로그램 연결 tootest USB 케이블을 사용 하 여 전화 tooyour 컴퓨터 hello 합니다. 이 작업에 연결 된 hello 전화 앱을 로드 합니다.

tootest hello 에뮬레이터 hello Eclipse 위쪽 도구 모음에서이 응용 프로그램 클릭 **실행**, 다음 응용 프로그램을 선택 하 고: hello 에뮬레이터를 로드, 시작 및 실행 hello 응용 프로그램입니다.

hello 앱 hello 'userId' 및 'channelId' hello Baidu 푸시 알림 서비스에서에서 검색 하 고 hello 알림 허브에 등록 합니다.

테스트 알림을 toosend hello 디버그 탭 hello Azure 클래식 포털을 사용할 수 있습니다. Visual Studio에 대 한 hello.NET 콘솔 응용 프로그램을 빌드한 경우 Visual Studio toorun hello 응용 프로그램에서 hello F5 키를 눌러만 합니다. hello 응용 프로그램에는 장치 또는 에뮬레이터의 hello 상위 알림 영역에 표시 되는 알림을 보냅니다.

<!-- Images. -->
[1]: ./media/notification-hubs-baidu-get-started/BaiduRegistration.png
[2]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationInput.png
[3]: ./media/notification-hubs-baidu-get-started/BaiduConfirmation.png
[4]: ./media/notification-hubs-baidu-get-started/BaiduActivationEmail.png
[5]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationMore.png
[6]: ./media/notification-hubs-baidu-get-started/BaiduOpenCloudPlatform.png
[7]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperServices.png
[8]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperRegistration.png
[9]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationInput.png
[10]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationConfirmation.png
[11]: ./media/notification-hubs-baidu-get-started/BaiduDevConfirmationFinal.png
[12]: ./media/notification-hubs-baidu-get-started/BaiduCloudPush.png
[13]: ./media/notification-hubs-baidu-get-started/BaiduDevSvcMgmt.png
[14]: ./media/notification-hubs-baidu-get-started/BaiduCreateProject.png
[15]: ./media/notification-hubs-baidu-get-started/BaiduCreateProjectInput.png
[16]: ./media/notification-hubs-baidu-get-started/BaiduProjectKeys.png
[17]: ./media/notification-hubs-baidu-get-started/AzureNHCreation.png
[18]: ./media/notification-hubs-baidu-get-started/NotificationHubs.png
[19]: ./media/notification-hubs-baidu-get-started/NotificationHubsConfigure.png
[20]: ./media/notification-hubs-baidu-get-started/NotificationHubBaiduConfigure.png
[21]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionStringView.png
[22]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionString.png
[23]: ./media/notification-hubs-baidu-get-started/EclipseNewProject.png
[24]: ./media/notification-hubs-baidu-get-started/EclipseProjectCreation.png
[25]: ./media/notification-hubs-baidu-get-started/EclipseBlankActivity.png
[26]: ./media/notification-hubs-baidu-get-started/EclipseProjectBuildProperty.png
[27]: ./media/notification-hubs-baidu-get-started/EclipseBaiduReferences.png
[28]: ./media/notification-hubs-baidu-get-started/EclipseNewClass.png
[29]: ./media/notification-hubs-baidu-get-started/EclipseConfigSettingsClass.png
[30]: ./media/notification-hubs-baidu-get-started/ConsoleProject.png
[31]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig1.png
[32]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig2.png
[33]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig3.png

<!-- URLs. -->
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Baidu 푸시 Android SDK]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk
[Azure 클래식 포털]: https://manage.windowsazure.com/
[Baidu 포털]: http://www.baidu.com/
