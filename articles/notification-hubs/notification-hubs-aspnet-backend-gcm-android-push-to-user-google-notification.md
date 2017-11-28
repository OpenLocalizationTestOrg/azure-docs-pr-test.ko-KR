---
title: ".NET 백 엔드와 aaaAzure Android 용 알림 허브 알릴 사용자"
description: "Azure에서 toosend 알림 toousers 강제 하는 방법에 대해 알아봅니다. Android용 Java로 작성된 코드 샘플"
documentationcenter: android
services: notification-hubs
author: ysxu
manager: erikre
editor: 
ms.assetid: ae0e17a8-9d2b-496e-afd2-baa151370c25
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: b042d2e6fb7f7c861c378526a8a0d59ab75beef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-for-android-with-net-backend"></a><span data-ttu-id="58675-104">.NET 백 엔드를 통한 Azure 알림 허브의 Android 사용자 알림</span><span class="sxs-lookup"><span data-stu-id="58675-104">Azure Notification Hubs Notify Users for Android with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="58675-105">개요</span><span class="sxs-lookup"><span data-stu-id="58675-105">Overview</span></span>
<span data-ttu-id="58675-106">Azure의 푸시 알림 지원을 사용 하면 tooaccess는 사용 하기 쉬운, 다중 플랫폼, 및 수평 확장형 푸시 인프라를 모바일 앱을 위해 소비자 및 엔터프라이즈 응용 프로그램에 대 한 푸시 알림 hello 구현이 크게 간소화 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="58675-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="58675-107">이 자습서에서는 toouse Azure 알림 허브 toosend 특정 장치에서 알림을 tooa 특정 응용 프로그램 사용자를 강제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="58675-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="58675-108">ASP.NET WebAPI 백 엔드는 사용 되는 tooauthenticate 클라이언트 및 toogenerate 알림 hello 지침 항목에 나와 있는 것 처럼 [앱 백 엔드에서 등록](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend)합니다.</span><span class="sxs-lookup"><span data-stu-id="58675-108">An ASP.NET WebAPI backend is used tooauthenticate clients and toogenerate notifications, as shown in hello guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span> <span data-ttu-id="58675-109">Hello에서 만든 hello 알림 허브를 기반으로 한이 자습서 [(Android) 알림 허브 시작](notification-hubs-android-push-notification-google-gcm-get-started.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="58675-109">This tutorial builds on hello notification hub that you created in hello [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="58675-110">이 자습서에서는 [알림 허브 시작(Android)](notification-hubs-android-push-notification-google-gcm-get-started.md)에 설명된 대로 알림 허브를 만들고 구성했다고 가정합니다</span><span class="sxs-lookup"><span data-stu-id="58675-110">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="create-hello-android-project"></a><span data-ttu-id="58675-111">Hello Android 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="58675-111">Create hello Android Project</span></span>
<span data-ttu-id="58675-112">hello 다음 단계 toocreate hello Android 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="58675-112">hello next step is toocreate hello Android application.</span></span>

1. <span data-ttu-id="58675-113">Hello에 따라 [(Android) 알림 허브 시작](notification-hubs-android-push-notification-google-gcm-get-started.md) 자습서 toocreate 및 GCM에서 응용 프로그램 tooreceive 푸시 알림을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="58675-113">Follow hello [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial toocreate and configure your app tooreceive push notifications from GCM.</span></span>
2. <span data-ttu-id="58675-114">Open 프로그램 **res/layout/activity_main.xml** 파일, hello hello 콘텐츠 정의 다음으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="58675-114">Open your **res/layout/activity_main.xml** file, replace hello with hello following content definitions.</span></span>
   
    <span data-ttu-id="58675-115">그러면 사용자로 로그인할 수 있는 새 EditText 컨트롤이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="58675-115">This adds new EditText controls for logging in as a user.</span></span> <span data-ttu-id="58675-116">또한 보내는 알림의 일부가 될 사용자 이름 태그 필드가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="58675-116">Also a field is added for a username tag that will be part of notifications you send:</span></span>
   
        <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"
            android:layout_height="match_parent" android:paddingLeft="@dimen/activity_horizontal_margin"
            android:paddingRight="@dimen/activity_horizontal_margin"
            android:paddingTop="@dimen/activity_vertical_margin"
            android:paddingBottom="@dimen/activity_vertical_margin" tools:context=".MainActivity">
   
        <EditText
            android:id="@+id/usernameText"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:ems="10"
            android:hint="@string/usernameHint"
            android:layout_above="@+id/passwordText"
            android:layout_alignParentEnd="true" />
        <EditText
            android:id="@+id/passwordText"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:ems="10"
            android:hint="@string/passwordHint"
            android:inputType="textPassword"
            android:layout_above="@+id/buttonLogin"
            android:layout_alignParentEnd="true" />
        <Button
            android:id="@+id/buttonLogin"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/loginButton"
            android:onClick="login"
            android:layout_above="@+id/toggleButtonGCM"
            android:layout_centerHorizontal="true"
            android:layout_marginBottom="24dp" />
        <ToggleButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textOn="WNS on"
            android:textOff="WNS off"
            android:id="@+id/toggleButtonWNS"
            android:layout_toLeftOf="@id/toggleButtonGCM"
            android:layout_centerVertical="true" />
        <ToggleButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textOn="GCM on"
            android:textOff="GCM off"
            android:id="@+id/toggleButtonGCM"
            android:checked="true"
            android:layout_centerHorizontal="true"
            android:layout_centerVertical="true" />
        <ToggleButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textOn="APNS on"
            android:textOff="APNS off"
            android:id="@+id/toggleButtonAPNS"
            android:layout_toRightOf="@id/toggleButtonGCM"
            android:layout_centerVertical="true" />
        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/editTextNotificationMessageTag"
            android:layout_below="@id/toggleButtonGCM"
            android:layout_centerHorizontal="true"
            android:hint="@string/notification_message_tag_hint" />
        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/editTextNotificationMessage"
            android:layout_below="@+id/editTextNotificationMessageTag"
            android:layout_centerHorizontal="true"
            android:hint="@string/notification_message_hint" />
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/send_button"
            android:id="@+id/sendbutton"
            android:onClick="sendNotificationButtonOnClick"
            android:layout_below="@+id/editTextNotificationMessage"
            android:layout_centerHorizontal="true" />
        </RelativeLayout>
3. <span data-ttu-id="58675-117">Open 프로그램 **res/values/strings.xml** hello를 바꾸고 파일 `send_button` hello 다음과 같이 정의 줄 hello에 대 한 해당 재정의 hello 문자열 `send_button` hello에 대 한 문자열을 다른 컨트롤 추가 및:</span><span class="sxs-lookup"><span data-stu-id="58675-117">Open your **res/values/strings.xml** file and replace hello `send_button` definition with hello following lines that redefine hello string for hello `send_button` and add strings for hello other controls:</span></span>
   
        <string name="usernameHint">Username</string>
        <string name="passwordHint">Password</string>
        <string name="loginButton">1. Log in</string>
        <string name="send_button">2. Send Notification</string>
        <string name="notification_message_tag_hint">
            Recipient username tag
        </string>
   
    <span data-ttu-id="58675-118">main_activity.xml 그래픽 레이아웃은 다음과 같이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58675-118">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
4. <span data-ttu-id="58675-119">이라는 새 클래스를 만들 **RegisterClient** 패키징하여 동일 hello에 프로그램 `MainActivity` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="58675-119">Create a new class named **RegisterClient** in hello same package as your `MainActivity` class.</span></span> <span data-ttu-id="58675-120">아래 hello 코드를 사용 하 여 hello 새 클래스 파일에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="58675-120">Use hello code below for hello new class file.</span></span>
   
        import java.io.IOException;
        import java.io.UnsupportedEncodingException;
        import java.util.Set;
   
        import org.apache.http.HttpResponse;
        import org.apache.http.HttpStatus;
        import org.apache.http.client.ClientProtocolException;
        import org.apache.http.client.HttpClient;
        import org.apache.http.client.methods.HttpPost;
        import org.apache.http.client.methods.HttpPut;
        import org.apache.http.client.methods.HttpUriRequest;
        import org.apache.http.entity.StringEntity;
        import org.apache.http.impl.client.DefaultHttpClient;
        import org.apache.http.util.EntityUtils;
        import org.json.JSONArray;
        import org.json.JSONException;
        import org.json.JSONObject;
   
        import android.content.Context;
        import android.content.SharedPreferences;
        import android.util.Log;
   
        public class RegisterClient {
            private static final String PREFS_NAME = "ANHSettings";
            private static final String REGID_SETTING_NAME = "ANHRegistrationId";
            private String Backend_Endpoint;
            SharedPreferences settings;
            protected HttpClient httpClient;
            private String authorizationHeader;
   
            public RegisterClient(Context context, String backendEnpoint) {
                super();
                this.settings = context.getSharedPreferences(PREFS_NAME, 0);
                httpClient =  new DefaultHttpClient();
                Backend_Endpoint = backendEnpoint + "/api/register";
            }
   
            public String getAuthorizationHeader() {
                return authorizationHeader;
            }
   
            public void setAuthorizationHeader(String authorizationHeader) {
                this.authorizationHeader = authorizationHeader;
            }
   
            public void register(String handle, Set<String> tags) throws ClientProtocolException, IOException, JSONException {
                String registrationId = retrieveRegistrationIdOrRequestNewOne(handle);
   
                JSONObject deviceInfo = new JSONObject();
                deviceInfo.put("Platform", "gcm");
                deviceInfo.put("Handle", handle);
                deviceInfo.put("Tags", new JSONArray(tags));
   
                int statusCode = upsertRegistration(registrationId, deviceInfo);
   
                if (statusCode == HttpStatus.SC_OK) {
                    return;
                } else if (statusCode == HttpStatus.SC_GONE){
                    settings.edit().remove(REGID_SETTING_NAME).commit();
                    registrationId = retrieveRegistrationIdOrRequestNewOne(handle);
                    statusCode = upsertRegistration(registrationId, deviceInfo);
                    if (statusCode != HttpStatus.SC_OK) {
                        Log.e("RegisterClient", "Error upserting registration: " + statusCode);
                        throw new RuntimeException("Error upserting registration");
                    }
                } else {
                    Log.e("RegisterClient", "Error upserting registration: " + statusCode);
                    throw new RuntimeException("Error upserting registration");
                }
            }
   
            private int upsertRegistration(String registrationId, JSONObject deviceInfo)
                    throws UnsupportedEncodingException, IOException,
                    ClientProtocolException {
                HttpPut request = new HttpPut(Backend_Endpoint+"/"+registrationId);
                request.setEntity(new StringEntity(deviceInfo.toString()));
                request.addHeader("Authorization", "Basic "+authorizationHeader);
                request.addHeader("Content-Type", "application/json");
                HttpResponse response = httpClient.execute(request);
                int statusCode = response.getStatusLine().getStatusCode();
                return statusCode;
            }
   
            private String retrieveRegistrationIdOrRequestNewOne(String handle) throws ClientProtocolException, IOException {
                if (settings.contains(REGID_SETTING_NAME))
                    return settings.getString(REGID_SETTING_NAME, null);
   
                HttpUriRequest request = new HttpPost(Backend_Endpoint+"?handle="+handle);
                request.addHeader("Authorization", "Basic "+authorizationHeader);
                HttpResponse response = httpClient.execute(request);
                if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                    Log.e("RegisterClient", "Error creating registrationId: " + response.getStatusLine().getStatusCode());
                    throw new RuntimeException("Error creating Notification Hubs registrationId");
                }
                String registrationId = EntityUtils.toString(response.getEntity());
                registrationId = registrationId.substring(1, registrationId.length()-1);
   
                settings.edit().putString(REGID_SETTING_NAME, registrationId).commit();
   
                return registrationId;
            }
        }
   
    <span data-ttu-id="58675-121">이 구성 요소는 hello REST 호출 필요한 toocontact hello 앱 백 순서 tooregister 푸시 알림을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="58675-121">This component implements hello REST calls required toocontact hello app backend, in order tooregister for push notifications.</span></span> <span data-ttu-id="58675-122">또한 로컬로 hello 저장 *registrationIds* 알림 허브에 설명 된 대로 hello에서 만든 [앱 백 엔드에서 등록](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend)합니다.</span><span class="sxs-lookup"><span data-stu-id="58675-122">It also locally stores hello *registrationIds* created by hello Notification Hub as detailed in [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span> <span data-ttu-id="58675-123">Hello를 클릭할 때 로컬 저장소에 저장 하는 권한 부여 토큰을 사용 하 여 참고 **로그인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="58675-123">Note that it uses an authorization token stored in local storage when you click hello **Log in** button.</span></span>
5. <span data-ttu-id="58675-124">사용자 `MainActivity` 클래스를 제거 하거나 주석 처리에 대 한 개인 필드 `NotificationHub`, hello에 대 한 필드를 추가 하 고 `RegisterClient` 클래스 및 ASP.NET 백 엔드의 끝점에 대 한 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="58675-124">In your `MainActivity` class remove or comment out your private field for `NotificationHub`, and add a field for hello `RegisterClient` class and a string for your ASP.NET backend's endpoint.</span></span> <span data-ttu-id="58675-125">수 있는지 tooreplace `<Enter Your Backend Endpoint>` hello로 실제 백 엔드 끝점 이전에 얻은 합니다.</span><span class="sxs-lookup"><span data-stu-id="58675-125">Be sure tooreplace `<Enter Your Backend Endpoint>` with hello your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="58675-126">예: `http://mybackend.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="58675-126">For example, `http://mybackend.azurewebsites.net`.</span></span>

        //private NotificationHub hub;
        private RegisterClient registerClient;
        private static final String BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";


1. <span data-ttu-id="58675-127">사용자 `MainActivity` hello에 클래스 `onCreate` 메서드를 제거 하거나 주석으로 hello hello 초기화 `hub` 필드와 hello 호출 toohello `registerWithNotificationHubs` 메서드.</span><span class="sxs-lookup"><span data-stu-id="58675-127">In your `MainActivity` class, in hello `onCreate` method, remove or comment out hello initialization of hello `hub` field and hello call toohello `registerWithNotificationHubs` method.</span></span> <span data-ttu-id="58675-128">다음 코드 tooinitialize hello의 인스턴스를 추가할 `RegisterClient` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="58675-128">Then add code tooinitialize an instance of hello `RegisterClient` class.</span></span> <span data-ttu-id="58675-129">hello 메서드 hello 다음 줄을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58675-129">hello method should contain hello following lines:</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
   
            MyHandler.mainActivity = this;
            NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);
            gcm = GoogleCloudMessaging.getInstance(this);
   
            //hub = new NotificationHub(HubName, HubListenConnectionString, this);
            //registerWithNotificationHubs();
   
            registerClient = new RegisterClient(this, BACKEND_ENDPOINT);
   
            setContentView(R.layout.activity_main);
        }
2. <span data-ttu-id="58675-130">사용자 `MainActivity` 클래스, 삭제 또는 전체 hello 주석 `registerWithNotificationHubs` 메서드.</span><span class="sxs-lookup"><span data-stu-id="58675-130">In your `MainActivity` class, delete or comment out hello entire `registerWithNotificationHubs` method.</span></span> <span data-ttu-id="58675-131">이는 이 자습서에서는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58675-131">It will not be used in this tutorial.</span></span>
3. <span data-ttu-id="58675-132">Hello 다음 추가 `import` 문 tooyour **MainActivity.java** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="58675-132">Add hello following `import` statements tooyour **MainActivity.java** file.</span></span>
   
        import android.widget.Button;
        import java.io.UnsupportedEncodingException;
        import android.content.Context;
        import java.util.HashSet;
        import android.widget.Toast;
        import org.apache.http.client.ClientProtocolException;
        import java.io.IOException;
        import org.apache.http.HttpStatus;
4. <span data-ttu-id="58675-133">그런 다음 hello 메서드 toohandle hello 다음 추가 **로그인** 단추 클릭 이벤트 및 푸시 알림을 보내는 합니다.</span><span class="sxs-lookup"><span data-stu-id="58675-133">Then, add hello following methods toohandle hello **Log in** button click event and sending push notifications.</span></span>
   
        @Override
        protected void onStart() {
            super.onStart();
            Button sendPush = (Button) findViewById(R.id.sendbutton);
            sendPush.setEnabled(false);
        }
   
        public void login(View view) throws UnsupportedEncodingException {
            this.registerClient.setAuthorizationHeader(getAuthorizationHeader());
   
            final Context context = this;
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
                        String regid = gcm.register(SENDER_ID);
                        registerClient.register(regid, new HashSet<String>());
                    } catch (Exception e) {
                        DialogNotify("MainActivity - Failed tooregister", e.getMessage());
                        return e;
                    }
                    return null;
                }
   
                protected void onPostExecute(Object result) {
                    Button sendPush = (Button) findViewById(R.id.sendbutton);
                    sendPush.setEnabled(true);
                    Toast.makeText(context, "Logged in and registered.",
                            Toast.LENGTH_LONG).show();
                }
            }.execute(null, null, null);
        }
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
            return basicAuthHeader;
        }
   
        /**
         * This method calls hello ASP.NET WebAPI backend toosend hello notification message
         * toohello platform notification service based on hello pns parameter.
         *
         * @param pns     hello platform notification service toosend hello notification message to. Must
         *                be one of hello following ("wns", "gcm", "apns").
         * @param userTag hello tag for hello user who will receive hello notification message. This string
         *                must not contain spaces or special characters.
         * @param message hello notification message string. This string must include hello double quotes
         *                toobe used as JSON content.
         */
        public void sendPush(final String pns, final String userTag, final String message)
                throws ClientProtocolException, IOException {
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
   
                        String uri = BACKEND_ENDPOINT + "/api/notifications";
                        uri += "?pns=" + pns;
                        uri += "&to_tag=" + userTag;
   
                        HttpPost request = new HttpPost(uri);
                        request.addHeader("Authorization", "Basic "+ getAuthorizationHeader());
                        request.setEntity(new StringEntity(message));
                        request.addHeader("Content-Type", "application/json");
   
                        HttpResponse response = new DefaultHttpClient().execute(request);
   
                        if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                            DialogNotify("MainActivity - Error sending " + pns + " notification",
                                response.getStatusLine().toString());
                            throw new RuntimeException("Error sending notification");
                        }
                    } catch (Exception e) {
                        DialogNotify("MainActivity - Failed toosend " + pns + " notification ", e.getMessage());
                        return e;
                    }
   
                    return null;
                }
            }.execute(null, null, null);
        }

    <span data-ttu-id="58675-134">hello `login` hello에 대 한 처리기 **로그인** 단추는 기본 인증 사용 하 여 토큰에 사용자 이름이 입력된 하는 hello 및 암호 (참고가는 인증 체계를 사용 하는 모든 토큰)를 생성 한 다음 사용하여`RegisterClient`toocall hello 백 엔드 등록에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="58675-134">hello `login` handler for hello **Log in** button generates a basic authentication token using on hello input username and password (note that this represents any token your authentication scheme uses), then it uses `RegisterClient` toocall hello backend for registration.</span></span>

    <span data-ttu-id="58675-135">hello `sendPush` 메서드 hello 백 엔드 tootrigger hello 사용자 태그에 따라 보안 알림 toohello 사용자를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="58675-135">hello `sendPush` method calls hello backend tootrigger a secure notification toohello user based on hello user tag.</span></span> <span data-ttu-id="58675-136">hello 플랫폼 알림 서비스에 `sendPush` 대상 hello에 따라 달라 집니다 `pns` 문자열이 전달 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="58675-136">hello platform notification service that `sendPush` targets depends on hello `pns` string passed in.</span></span>

1. <span data-ttu-id="58675-137">사용자 `MainActivity` 클래스, 업데이트 hello `sendNotificationButtonOnClick` 메서드 toocall hello `sendPush` hello 사용자와 방법을 다음과 같은 플랫폼 알림 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="58675-137">In your `MainActivity` class, update hello `sendNotificationButtonOnClick` method toocall hello `sendPush` method with hello user's selected platform notification services as follows.</span></span>
   
       /**
        * Send Notification button click handler. This method sends hello push notification
        * message tooeach platform selected.
        *
        * @param v hello view
        */
       public void sendNotificationButtonOnClick(View v)
               throws ClientProtocolException, IOException {
   
           String nhMessageTag = ((EditText) findViewById(R.id.editTextNotificationMessageTag))
                   .getText().toString();
           String nhMessage = ((EditText) findViewById(R.id.editTextNotificationMessage))
                   .getText().toString();
   
           // JSON String
           nhMessage = "\"" + nhMessage + "\"";
   
           if (((ToggleButton)findViewById(R.id.toggleButtonWNS)).isChecked())
           {
               sendPush("wns", nhMessageTag, nhMessage);
           }
           if (((ToggleButton)findViewById(R.id.toggleButtonGCM)).isChecked())
           {
               sendPush("gcm", nhMessageTag, nhMessage);
           }
           if (((ToggleButton)findViewById(R.id.toggleButtonAPNS)).isChecked())
           {
               sendPush("apns", nhMessageTag, nhMessage);
           }
       }

## <a name="run-hello-application"></a><span data-ttu-id="58675-138">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="58675-138">Run hello Application</span></span>
1. <span data-ttu-id="58675-139">장치 또는 Android Studio를 사용 하 여 에뮬레이터 hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="58675-139">Run hello application on a device or an emulator using Android Studio.</span></span>
2. <span data-ttu-id="58675-140">Hello Android 앱에서 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="58675-140">In hello Android app, enter a username and password.</span></span> <span data-ttu-id="58675-141">여야 hello 동일한 문자열 값 있으며 없어야 공백이 나 특수 문자.</span><span class="sxs-lookup"><span data-stu-id="58675-141">They must both be hello same string value and they must not contain spaces or special characters.</span></span>
3. <span data-ttu-id="58675-142">Hello Android 앱에서 클릭 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="58675-142">In hello Android app, click **Log in**.</span></span> <span data-ttu-id="58675-143">**Logged in and registered**를 나타내는 알림 메시지를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="58675-143">Wait for a toast message that states **Logged in and registered**.</span></span> <span data-ttu-id="58675-144">이렇게 하면 hello **알림 보내기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="58675-144">This will enable hello **Send Notification** button.</span></span>
   
    ![][A2]
4. <span data-ttu-id="58675-145">Hello 토글 단추 tooenable 클릭 수 있는 모든 플랫폼 hello 앱을 실행 하 고 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="58675-145">Click hello toggle buttons tooenable all platforms where you have ran hello app and registered a user.</span></span>
5. <span data-ttu-id="58675-146">Hello 알림 메시지를 수신할 hello 사용자의 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="58675-146">Enter hello user's name that will receive hello notification message.</span></span> <span data-ttu-id="58675-147">해당 사용자는 장치를 대상으로 하는 hello에 대 한 알림을 등록 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58675-147">That user must be registered for notifications on hello target devices.</span></span>
6. <span data-ttu-id="58675-148">푸시 알림 메시지로 사용자 tooreceive hello에 대 한 메시지를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="58675-148">Enter a message for hello user tooreceive as a push notification message.</span></span>
7. <span data-ttu-id="58675-149">**Send Notification**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58675-149">Click **Send Notification**.</span></span>  <span data-ttu-id="58675-150">Hello 일치 하는 사용자 이름 태그로 등록에는 각 장치 hello 푸시 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58675-150">Each device that has a registration with hello matching username tag will receive hello push notification.</span></span>

[A1]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users.png
[A2]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users-enter-password.png
