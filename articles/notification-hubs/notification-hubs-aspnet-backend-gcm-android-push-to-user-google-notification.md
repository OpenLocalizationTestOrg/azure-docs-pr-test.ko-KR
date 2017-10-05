---
title: ".NET 백 엔드를 통한 Azure 알림 허브의 Android 사용자 알림"
description: "Azure에서 사용자에게 푸시 알림을 보내는 방법에 대해 알아봅니다. Android용 Java로 작성된 코드 샘플"
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
ms.openlocfilehash: 418a4b638dfaa3fee33a7a7242433699205c79f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-notify-users-for-android-with-net-backend"></a><span data-ttu-id="350e2-104">.NET 백 엔드를 통한 Azure 알림 허브의 Android 사용자 알림</span><span class="sxs-lookup"><span data-stu-id="350e2-104">Azure Notification Hubs Notify Users for Android with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="350e2-105">개요</span><span class="sxs-lookup"><span data-stu-id="350e2-105">Overview</span></span>
<span data-ttu-id="350e2-106">Azure의 푸시 알림 지원을 통해 사용하기 쉬운 다중 플랫폼 및 규모 확장 푸시 인프라에 액세스할 수 있어, 모바일 플랫폼용 소비자 응용 프로그램 및 엔터프라이즈 응용 프로그램 모두에 대한 푸시 알림을 매우 간단하게 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-106">Push notification support in Azure enables you to access an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="350e2-107">이 자습서에서는 Azure 알림 허브를 사용하여 특정 장치에서 특정 앱 사용자에게 푸시 알림을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-107">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a specific app user on a specific device.</span></span> <span data-ttu-id="350e2-108">[앱 백 엔드에서 등록](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) 지침 항목에 나와 있는 대로 ASP.NET WebAPI 백 엔드는 클라이언트를 인증하고 알림을 생성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-108">An ASP.NET WebAPI backend is used to authenticate clients and to generate notifications, as shown in the guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span> <span data-ttu-id="350e2-109">이 자습서는 [알림 허브 시작(Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) 자습서에서 만든 알림 허브를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-109">This tutorial builds on the notification hub that you created in the [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="350e2-110">이 자습서에서는 [알림 허브 시작(Android)](notification-hubs-android-push-notification-google-gcm-get-started.md)에 설명된 대로 알림 허브를 만들고 구성했다고 가정합니다</span><span class="sxs-lookup"><span data-stu-id="350e2-110">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="create-the-android-project"></a><span data-ttu-id="350e2-111">Android 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="350e2-111">Create the Android Project</span></span>
<span data-ttu-id="350e2-112">다음은 Android 응용 프로그램을 만드는 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-112">The next step is to create the Android application.</span></span>

1. <span data-ttu-id="350e2-113">[알림 허브 시작(Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) 자습서에 따라 앱을 만들고 GCM에서 푸시 알림을 받도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-113">Follow the [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial to create and configure your app to receive push notifications from GCM.</span></span>
2. <span data-ttu-id="350e2-114">**res/layout/activity_main.xml** 파일을 열고 다음 콘텐츠 정의로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-114">Open your **res/layout/activity_main.xml** file, replace the with the following content definitions.</span></span>
   
    <span data-ttu-id="350e2-115">그러면 사용자로 로그인할 수 있는 새 EditText 컨트롤이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-115">This adds new EditText controls for logging in as a user.</span></span> <span data-ttu-id="350e2-116">또한 보내는 알림의 일부가 될 사용자 이름 태그 필드가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-116">Also a field is added for a username tag that will be part of notifications you send:</span></span>
   
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
3. <span data-ttu-id="350e2-117">**res/values/strings.xml** 파일을 열고 `send_button` 정의를 다음 줄로 바꿉니다. 그러면 `send_button`에 대한 문자열이 다시 정의되고 다른 컨트롤에 대한 문자열이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-117">Open your **res/values/strings.xml** file and replace the `send_button` definition with the following lines that redefine the string for the `send_button` and add strings for the other controls:</span></span>
   
        <string name="usernameHint">Username</string>
        <string name="passwordHint">Password</string>
        <string name="loginButton">1. Log in</string>
        <string name="send_button">2. Send Notification</string>
        <string name="notification_message_tag_hint">
            Recipient username tag
        </string>
   
    <span data-ttu-id="350e2-118">main_activity.xml 그래픽 레이아웃은 다음과 같이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-118">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
4. <span data-ttu-id="350e2-119">`MainActivity` 클래스와 동일한 패키지에서 **RegisterClient**라는 새 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-119">Create a new class named **RegisterClient** in the same package as your `MainActivity` class.</span></span> <span data-ttu-id="350e2-120">새 클래스 파일에 아래 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-120">Use the code below for the new class file.</span></span>
   
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
   
    <span data-ttu-id="350e2-121">이 구성 요소는 푸시 알림을 등록하기 위해 앱 백 엔드에 접속하는 데 필요한 REST 호출을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-121">This component implements the REST calls required to contact the app backend, in order to register for push notifications.</span></span> <span data-ttu-id="350e2-122">또한 *앱 백 엔드에서 등록* 에 설명된 대로 알림 허브에서 생성된 [registrationId](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend)를 로컬로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-122">It also locally stores the *registrationIds* created by the Notification Hub as detailed in [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span> <span data-ttu-id="350e2-123">이 구성 요소는 **로그인** 단추를 클릭할 때 로컬 저장소에 저장된 인증 토큰을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-123">Note that it uses an authorization token stored in local storage when you click the **Log in** button.</span></span>
5. <span data-ttu-id="350e2-124">`MainActivity` 클래스에서 `NotificationHub`에 대한 전용 필드를 제거하거나 주석 처리하고 `RegisterClient` 클래스에 대한 필드 및 ASP.NET 백 엔드의 끝점에 대한 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-124">In your `MainActivity` class remove or comment out your private field for `NotificationHub`, and add a field for the `RegisterClient` class and a string for your ASP.NET backend's endpoint.</span></span> <span data-ttu-id="350e2-125">`<Enter Your Backend Endpoint>` 을 이전에 얻은 실제 백 엔드 끝점으로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-125">Be sure to replace `<Enter Your Backend Endpoint>` with the your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="350e2-126">예: `http://mybackend.azurewebsites.net`</span><span class="sxs-lookup"><span data-stu-id="350e2-126">For example, `http://mybackend.azurewebsites.net`.</span></span>

        //private NotificationHub hub;
        private RegisterClient registerClient;
        private static final String BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";


1. <span data-ttu-id="350e2-127">`MainActivity` 클래스의 `onCreate` 메서드에서 `hub` 필드의 초기화를 제거하거나 주석 처리하고 `registerWithNotificationHubs` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-127">In your `MainActivity` class, in the `onCreate` method, remove or comment out the initialization of the `hub` field and the call to the `registerWithNotificationHubs` method.</span></span> <span data-ttu-id="350e2-128">그런 다음 `RegisterClient` 클래스의 인스턴스를 초기화할 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-128">Then add code to initialize an instance of the `RegisterClient` class.</span></span> <span data-ttu-id="350e2-129">메서드에는 다음 줄이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-129">The method should contain the following lines:</span></span>
   
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
2. <span data-ttu-id="350e2-130">`MainActivity` 클래스에서 전체 `registerWithNotificationHubs` 메서드를 삭제하거나 주석 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-130">In your `MainActivity` class, delete or comment out the entire `registerWithNotificationHubs` method.</span></span> <span data-ttu-id="350e2-131">이는 이 자습서에서는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-131">It will not be used in this tutorial.</span></span>
3. <span data-ttu-id="350e2-132">다음 `import` 문을 **MainActivity.java** 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-132">Add the following `import` statements to your **MainActivity.java** file.</span></span>
   
        import android.widget.Button;
        import java.io.UnsupportedEncodingException;
        import android.content.Context;
        import java.util.HashSet;
        import android.widget.Toast;
        import org.apache.http.client.ClientProtocolException;
        import java.io.IOException;
        import org.apache.http.HttpStatus;
4. <span data-ttu-id="350e2-133">그런 다음 **로그인** 단추 클릭 이벤트를 처리하고 푸시 알림을 보내는 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-133">Then, add the following methods to handle the **Log in** button click event and sending push notifications.</span></span>
   
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
                        DialogNotify("MainActivity - Failed to register", e.getMessage());
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
         * This method calls the ASP.NET WebAPI backend to send the notification message
         * to the platform notification service based on the pns parameter.
         *
         * @param pns     The platform notification service to send the notification message to. Must
         *                be one of the following ("wns", "gcm", "apns").
         * @param userTag The tag for the user who will receive the notification message. This string
         *                must not contain spaces or special characters.
         * @param message The notification message string. This string must include the double quotes
         *                to be used as JSON content.
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
                        DialogNotify("MainActivity - Failed to send " + pns + " notification ", e.getMessage());
                        return e;
                    }
   
                    return null;
                }
            }.execute(null, null, null);
        }

    <span data-ttu-id="350e2-134">**로그인** 단추에 대한 `login` 처리기는 입력 사용자 이름과 암호(이는 인증 체계에서 사용하는 모든 토큰을 나타냄)를 사용하여 기본 인증 토큰을 생성하고 `RegisterClient`를 사용하여 등록을 위한 백 엔드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-134">The `login` handler for the **Log in** button generates a basic authentication token using on the input username and password (note that this represents any token your authentication scheme uses), then it uses `RegisterClient` to call the backend for registration.</span></span>

    <span data-ttu-id="350e2-135">`sendPush` 메서드는 사용자 태그를 기반으로 사용자에 대한 보안 알림을 트리거하는 백 엔드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-135">The `sendPush` method calls the backend to trigger a secure notification to the user based on the user tag.</span></span> <span data-ttu-id="350e2-136">`sendPush`에서 대상으로 하는 플랫폼 알림 서비스는 전달되는 `pns` 문자열에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-136">The platform notification service that `sendPush` targets depends on the `pns` string passed in.</span></span>

1. <span data-ttu-id="350e2-137">다음과 같이 `MainActivity` 클래스에서 사용자가 선택한 플랫폼 알림 서비스를 사용하여 `sendPush` 메서드를 호출하도록 `sendNotificationButtonOnClick` 메서드를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-137">In your `MainActivity` class, update the `sendNotificationButtonOnClick` method to call the `sendPush` method with the user's selected platform notification services as follows.</span></span>
   
       /**
        * Send Notification button click handler. This method sends the push notification
        * message to each platform selected.
        *
        * @param v The view
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

## <a name="run-the-application"></a><span data-ttu-id="350e2-138">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="350e2-138">Run the Application</span></span>
1. <span data-ttu-id="350e2-139">Android Studio를 사용하여 장치 또는 에뮬레이터에서 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-139">Run the application on a device or an emulator using Android Studio.</span></span>
2. <span data-ttu-id="350e2-140">Android 앱에서 사용자 이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-140">In the Android app, enter a username and password.</span></span> <span data-ttu-id="350e2-141">둘 다 동일한 문자열 값이어야 하며 공백이나 특수 문자를 포함해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-141">They must both be the same string value and they must not contain spaces or special characters.</span></span>
3. <span data-ttu-id="350e2-142">Android 앱에서 **Log in**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-142">In the Android app, click **Log in**.</span></span> <span data-ttu-id="350e2-143">**Logged in and registered**를 나타내는 알림 메시지를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-143">Wait for a toast message that states **Logged in and registered**.</span></span> <span data-ttu-id="350e2-144">이 메시지가 나타나면 **Send Notification** 단추가 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-144">This will enable the **Send Notification** button.</span></span>
   
    ![][A2]
4. <span data-ttu-id="350e2-145">토글 단추를 클릭하여 앱을 실행하고 사용자를 등록한 모든 플랫폼을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-145">Click the toggle buttons to enable all platforms where you have ran the app and registered a user.</span></span>
5. <span data-ttu-id="350e2-146">알림 메시지를 받을 사용자의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-146">Enter the user's name that will receive the notification message.</span></span> <span data-ttu-id="350e2-147">대상 장치에 이 사용자에 대한 알림이 등록되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-147">That user must be registered for notifications on the target devices.</span></span>
6. <span data-ttu-id="350e2-148">사용자가 푸시 알림 메시지로 받을 메시지를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-148">Enter a message for the user to receive as a push notification message.</span></span>
7. <span data-ttu-id="350e2-149">**Send Notification**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-149">Click **Send Notification**.</span></span>  <span data-ttu-id="350e2-150">일치하는 사용자 이름 태그로 등록된 각 장치에 푸시 알림이 수신됩니다.</span><span class="sxs-lookup"><span data-stu-id="350e2-150">Each device that has a registration with the matching username tag will receive the push notification.</span></span>

[A1]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users.png
[A2]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users-enter-password.png
