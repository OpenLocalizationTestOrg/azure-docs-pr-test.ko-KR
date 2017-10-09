---
title: "aaaSending Secure 푸시 알림을 Azure 알림 허브와"
description: "Azure에서 toosend 보안 알림 tooan Android 앱 강제 하는 방법에 대해 알아봅니다. 코드 샘플은 Java 및 C#으로 작성되었습니다."
documentationcenter: android
keywords: "푸시 알림,푸시알림,푸시 메시지,android 푸시 알림"
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: daf3de1c-f6a9-43c4-8165-a76bfaa70893
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: d07943c4691ed07acb987086228ef565e6281d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a>Azure 알림 허브를 사용하여 보안 푸시 알림 보내기
> [!div class="op_single_selector"]
> * [Windows 범용](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>개요
> [!IMPORTANT]
> toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started)을 참조하세요.
> 
> 

Microsoft Azure에서 푸시 알림 지원을 사용 하면 tooaccess 크게 간소화 됩니다. hello에 대 한 소비자 및 엔터프라이즈 응용 프로그램에서 푸시 알림 구현 하는 사용 하기 쉬운, 다중 플랫폼, 수평 확장 된 푸시 메시지 인프라 모바일 플랫폼입니다.

때로는 tooregulatory 또는 보안 제약 조건 때문 응용 프로그램에서 hello 표준 푸시 알림 인프라를 통해 전송 될 수 없는 hello 알림 tooinclude를 할 수도 있습니다. 이 자습서에서는 tooachieve hello 클라이언트에 대 한 Android 장치 및 앱 백 엔드에서 hello 간에 안전 하 고 인증 된 연결을 통해 중요 한 정보를 전송 하 여 동일한 환경을 hello 하는 방법을 설명 합니다.

상위 수준 hello 흐름은 다음과 같습니다.

1. hello 앱 백 엔드에서:
   * 백 엔드 데이터베이스에 보안 페이로드를 저장합니다.
   * Hello ID (보안 정보 없음 전송)이 알림 toohello Android 장치에 보냅니다.
2. 응용 프로그램에 액세스 hello 알림을 받은 경우 hello 장치 hello:
   * hello Android 장치가 hello 백 엔드에서 요청 hello 보안 페이로드를 연결합니다.
   * hello 앱 hello 장치에 대 한 알림으로 hello 페이로드를 표시할 수 있습니다.

hello 사용자가 로그인 한 후 toonote 하의 hello 흐름 이전 (및이 자습서에서는) 가정 hello 장치 로컬 저장소에 인증 토큰을 저장 합니다. 이 hello 장치는이 토큰을 사용 하 여 hello 알림 보안 페이로드를 검색할 수 있는 완전히 원활한 환경을 보장 합니다. 응용 프로그램에서 hello 장치에서 인증 토큰을 저장 하지 않으면 또는 이러한 토큰을 만료 될 수 있습니다 하는 경우 hello 사용자 toolaunch hello 앱 메시지를 표시 하는 제네릭 알림 hello 푸시 알림을 받으면 hello 장치 응용 프로그램에 표시 됩니다. 그런 다음 hello 앱 hello 사용자를 인증 하 고 hello 알림 페이로드를 보여 줍니다.

이 자습서에서는 보안 toosend 푸시 알림 방법을 보여 줍니다. Hello에 기반 [사용자에 게 알림](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) 자습서에서 단계를 완료 해야 hello 해당 자습서에서는 먼저 아직 없는 경우 하도록 합니다.

> [!NOTE]
> 이 자습서에서는 [알림 허브 시작(Android)](notification-hubs-android-push-notification-google-gcm-get-started.md)에 설명된 대로 알림 허브를 만들고 구성했다고 가정합니다
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-android-project"></a>Hello Android 프로젝트를 수정 합니다.
앱 백 엔드에서 toosend 정당한 hello 수정 했으므로 *id* 푸시 알림의 있는 toochange 알림과 콜백을 백 엔드 tooretrieve hello 보안 메시지 toobe 표시 하 여 Android 앱 toohandle 합니다.
tooachieve이이 목표를 Android 앱 알고 있어야 toomake 있는 어떻게 tooauthenticate 자체 백 엔드 hello 푸시 알림의 받을 때 사용 합니다.

에서는 이제 hello를 수정 합니다 *로그인* hello 순서 toosave hello 인증 헤더 값의 흐름 공유 응용 프로그램의 기본 설정 합니다. 유사한 메커니즘 사용된 toostore 수 앱 hello 모든 인증 토큰 (예: OAuth 토큰)는 사용자 자격 증명을 요구 하지 않고 toouse 갖습니다.

1. Android 응용 프로그램 프로젝트에서 추가 상수 hello hello 맨 뒤 hello **MainActivity** 클래스:
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. Hello에 여전히 **MainActivity** 클래스, 업데이트 hello `getAuthorizationHeader()` 코드 다음 메서드 toocontain hello:
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. Hello 다음 추가 `import` hello 위쪽 hello에 문을 **MainActivity** 파일:
   
        import android.content.SharedPreferences;

이제 hello 알림이 수신 되 면 호출 되는 hello 처리기를 변경 합니다.

1. Hello에 **MyHandler** 클래스 변경 hello `OnReceive()` 메서드 toocontain:
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. 그런 다음 추가 hello `retrieveNotification()` hello 자리 표시자를 대체 하는 메서드를 `{back-end endpoint}` 백 엔드를 배포 하는 동안 가져온 hello 백 엔드 끝점을 사용:
   
        private void retrieveNotification(final String secureMessageId) {
            SharedPreferences sp = ctx.getSharedPreferences(MainActivity.NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            final String authorizationHeader = sp.getString(MainActivity.AUTHORIZATION_HEADER_PROPERTY, null);
   
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
                        HttpUriRequest request = new HttpGet("{back-end endpoint}/api/notifications/"+secureMessageId);
                        request.addHeader("Authorization", "Basic "+authorizationHeader);
                        HttpResponse response = new DefaultHttpClient().execute(request);
                        if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                            Log.e("MainActivity", "Error retrieving secure notification" + response.getStatusLine().getStatusCode());
                            throw new RuntimeException("Error retrieving secure notification");
                        }
                        String secureNotificationJSON = EntityUtils.toString(response.getEntity());
                        JSONObject secureNotification = new JSONObject(secureNotificationJSON);
                        sendNotification(secureNotification.getString("Payload"));
                    } catch (Exception e) {
                        Log.e("MainActivity", "Failed tooretrieve secure notification - " + e.getMessage());
                        return e;
                    }
                    return null;
                }
            }.execute(null, null, null);
        }

이 메서드는 앱 백 엔드 tooretrieve hello 알림이 기본 설정을 공유 하 고 일반 알림으로 표시 hello에 저장 된 hello 자격 증명을 사용 하 여 콘텐츠를 호출 합니다. hello 알림 다른 푸시 알림 똑같이 toohello 응용 프로그램 사용자를 찾습니다.

누락 된 인증 헤더 속성 또는 hello 백 엔드가 거부 된 것이 좋습니다 toohandle hello 경우 인지 note 합니다. 대상 사용자 경험에 대부분의이 경우 hello 특정 처리에 따라 달라 집니다. 한 가지 방법은 toodisplay hello 사용자 tooauthenticate tooretrieve hello 실제 알림에 대 한 제네릭 프롬프트로 알림입니다.

## <a name="run-hello-application"></a>Hello 응용 프로그램 실행
toorun hello 응용 프로그램, 다음 hello지 않습니다.

1. **AppBackend** 가 Azure에 배포되었는지 확인합니다. Visual Studio를 사용 하는 경우 실행 hello **AppBackend** Web API 응용 프로그램입니다. ASP.NET 웹 페이지가 표시됩니다.
2. Eclipse에서 실제 Android 장치 또는 hello 에뮬레이터의 hello 앱을 실행 합니다.
3. Hello Android 앱 UI를 사용자 이름 및 암호를 입력 합니다. 모든 문자열을 지정할 수 있습니다 이러한 있지만 해야만 해당 hello 동일한 값입니다.
4. Hello Android 앱 UI의에서 클릭 **로그인**합니다. 그리고 나서 **푸시 보내기**를 클릭합니다.

