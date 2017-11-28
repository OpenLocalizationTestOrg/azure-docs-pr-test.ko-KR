---
title: "Azure 알림 허브를 사용하여 보안 푸시 알림 보내기"
description: "Azure에서 Android 앱에 보안 푸시 알림을 보내는 방법에 대해 알아봅니다. 코드 샘플은 Java 및 C#으로 작성되었습니다."
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
ms.openlocfilehash: 29f8c516e611c13fb73c7edc15e7c52708c75bb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a><span data-ttu-id="ffa2a-105">Azure 알림 허브를 사용하여 보안 푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="ffa2a-105">Sending Secure Push Notifications with Azure Notification Hubs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ffa2a-106">Windows 범용</span><span class="sxs-lookup"><span data-stu-id="ffa2a-106">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="ffa2a-107">iOS</span><span class="sxs-lookup"><span data-stu-id="ffa2a-107">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="ffa2a-108">Android</span><span class="sxs-lookup"><span data-stu-id="ffa2a-108">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="ffa2a-109">개요</span><span class="sxs-lookup"><span data-stu-id="ffa2a-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ffa2a-110">이 자습서를 완료하려면 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-110">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="ffa2a-111">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ffa2a-112">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="ffa2a-113">Microsoft Azure의 푸시 알림 지원을 통해 사용하기 쉬운 다중 플랫폼 및 규모 확장 푸시 메시지 인프라에 액세스할 수 있어, 모바일 플랫폼용 소비자 응용 프로그램 및 엔터프라이즈 응용 프로그램 모두에 대한 푸시 알림을 매우 간단하게 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-113">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push message infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="ffa2a-114">규제나 보안 제약 조건 때문에 응용 프로그램의 알림에 표준 푸시 알림 인프라를 통해 전송할 수 없는 어떤 항목을 포함해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-114">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="ffa2a-115">이 자습서에서는 클라이언트 Android 장치와 앱 백 엔드 간에 인증된 보안 연결을 통해 중요한 정보를 전송하여 동일한 경험을 얻는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-115">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client Android device and the app backend.</span></span>

<span data-ttu-id="ffa2a-116">개략적으로 흐름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-116">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="ffa2a-117">앱 백 엔드:</span><span class="sxs-lookup"><span data-stu-id="ffa2a-117">The app back-end:</span></span>
   * <span data-ttu-id="ffa2a-118">백 엔드 데이터베이스에 보안 페이로드를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-118">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="ffa2a-119">이 알림의 ID를 Android 장치에 보냅니다(보안 정보는 전송되지 않음).</span><span class="sxs-lookup"><span data-stu-id="ffa2a-119">Sends the ID of this notification to the Android device (no secure information is sent).</span></span>
2. <span data-ttu-id="ffa2a-120">알림 수신 시 장치의 앱:</span><span class="sxs-lookup"><span data-stu-id="ffa2a-120">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="ffa2a-121">Android 장치가 보안 페이로드를 요청하는 백 엔드에 접속합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-121">The Android device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="ffa2a-122">앱이 장치에서 페이로드를 알림으로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-122">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="ffa2a-123">앞의 흐름과 이 자습서에서는 사용자가 로그인한 후 장치가 인증 토큰을 로컬 저장소에 저장한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-123">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="ffa2a-124">이렇게 하면 장치가 이 토큰을 사용하여 알림의 보안 페이로드를 검색할 수 있으므로 매우 원활한 환경이 보장됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-124">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="ffa2a-125">응용 프로그램이 인증 토큰을 장치에 저장하지 않거나 이 토큰이 만료될 수 없으면 푸시 알림 수신 시 장치 앱은 사용자에게 앱을 시작할지 묻는 메시지가 포함된 일반 알림을 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-125">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the push notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="ffa2a-126">그리고 나서 앱은 사용자를 인증하고 알림 페이로드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-126">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="ffa2a-127">이 자습서에서는 보안 푸시 알림을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-127">This tutorial shows how to send secure push notifications.</span></span> <span data-ttu-id="ffa2a-128">이 자습서는 [사용자에게 알림](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) 자습서를 기반으로 빌드되므로 해당 자습서의 단계를 아직 완료하지 않은 경우 먼저 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-128">It builds on the [Notify Users](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) tutorial, so you should complete the steps in that tutorial first if you haven't already.</span></span>

> [!NOTE]
> <span data-ttu-id="ffa2a-129">이 자습서에서는 [알림 허브 시작(Android)](notification-hubs-android-push-notification-google-gcm-get-started.md)에 설명된 대로 알림 허브를 만들고 구성했다고 가정합니다</span><span class="sxs-lookup"><span data-stu-id="ffa2a-129">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-android-project"></a><span data-ttu-id="ffa2a-130">Android 프로젝트 수정</span><span class="sxs-lookup"><span data-stu-id="ffa2a-130">Modify the Android project</span></span>
<span data-ttu-id="ffa2a-131">푸시 알림의 *id* 만 보내도록 앱 백 엔드를 수정했으므로 해당 알림을 처리하고 백 엔드를 콜백하여 표시할 보안 메시지를 검색하도록 Android 앱을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-131">Now that you modified your app back-end to send just the *id* of a push notification, you have to change your Android app to handle that notification and call back your back-end to retrieve the secure message to be displayed.</span></span>
<span data-ttu-id="ffa2a-132">이 목표를 달성하려면 Android 앱이 푸시 알림을 받을 때 백 엔드에 인증하는 방법을 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-132">To achieve this goal, you have to make sure that your Android app knows how to authenticate itself with your back-end when it receives the push notifications.</span></span>

<span data-ttu-id="ffa2a-133">이제 앱의 공유 기본 설정에서 인증 헤더 값을 저장하기 위해 *로그인* 흐름을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-133">We will now modify the *login* flow in order to save the authentication header value in the shared preferences of your app.</span></span> <span data-ttu-id="ffa2a-134">유사 메커니즘을 사용하여 사용자 앱에서 자격 증명 없이 사용해야 하는 인증 토큰(예: OAuth 토큰)을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-134">Analogous mechanisms can be used to store any authentication token (e.g. OAuth tokens) that the app will have to use without requiring user credentials.</span></span>

1. <span data-ttu-id="ffa2a-135">Android 앱 프로젝트에서 **MainActivity** 클래스의 맨 위에 다음 상수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-135">In your Android app project, add the following constants at the top of the **MainActivity** class:</span></span>
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. <span data-ttu-id="ffa2a-136">**MainActivity** 클래스에서 `getAuthorizationHeader()` 메서드를 업데이트하여 다음 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-136">Still in the **MainActivity** class, update the `getAuthorizationHeader()` method to contain the following code:</span></span>
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. <span data-ttu-id="ffa2a-137">**MainActivity** 파일의 맨 위에 다음 `import` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-137">Add the following `import` statements at the top of the **MainActivity** file:</span></span>
   
        import android.content.SharedPreferences;

<span data-ttu-id="ffa2a-138">이제 알림을 받을 때 호출되는 처리기를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-138">Now we will change the handler that is called when the notification is received.</span></span>

1. <span data-ttu-id="ffa2a-139">**MyHandler** 클래스에서 다음을 포함하도록 `OnReceive()` 메서드를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-139">In the **MyHandler** class change the `OnReceive()` method to contain:</span></span>
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. <span data-ttu-id="ffa2a-140">그런 다음 `retrieveNotification()` 메서드를 추가하고 자리 표시자 `{back-end endpoint}`를 백 엔드를 배포할 때 얻은 백 엔드 끝점으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-140">Then add the `retrieveNotification()` method, replacing the placeholder `{back-end endpoint}` with the back-end endpoint obtained while deploying your back-end:</span></span>
   
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
                        Log.e("MainActivity", "Failed to retrieve secure notification - " + e.getMessage());
                        return e;
                    }
                    return null;
                }
            }.execute(null, null, null);
        }

<span data-ttu-id="ffa2a-141">이 메서드는 앱 백 엔드를 호출하여 공유 기본 설정에 저장된 자격 증명을 통해 알림 콘텐츠를 검색하고 일반 알림으로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-141">This method calls your app back-end to retrieve the notification content using the credentials stored in the shared preferences and displays it as a normal notification.</span></span> <span data-ttu-id="ffa2a-142">이 알림은 앱 사용자에게 다른 푸시 알림과 똑같이 보입니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-142">The notification looks to the app user exactly like any other push notification.</span></span>

<span data-ttu-id="ffa2a-143">백 엔드에 의해 거부되거나 인증 헤더 속성이 누락되는 경우를 처리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-143">Note that it is preferable to handle the cases of missing authentication header property or rejection by the back-end.</span></span> <span data-ttu-id="ffa2a-144">이러한 경우의 특수 처리는 대부분 대상 사용자 환경에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-144">The specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="ffa2a-145">한 가지 옵션은 실제 알림을 검색하기 위해 사용자가 인증을 받도록 하는 일반 프롬프트가 포함된 알림을 표시하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-145">One option is to display a notification with a generic prompt for the user to authenticate to retrieve the actual notification.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="ffa2a-146">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="ffa2a-146">Run the Application</span></span>
<span data-ttu-id="ffa2a-147">응용 프로그램을 실행하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-147">To run the application, do the following:</span></span>

1. <span data-ttu-id="ffa2a-148">**AppBackend** 가 Azure에 배포되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-148">Make sure **AppBackend** is deployed in Azure.</span></span> <span data-ttu-id="ffa2a-149">Visual Studio를 사용할 경우 **AppBackend** Web API 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-149">If using Visual Studio, run the **AppBackend** Web API application.</span></span> <span data-ttu-id="ffa2a-150">ASP.NET 웹 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-150">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="ffa2a-151">Eclipse에서는 실제 Android 장치나 에뮬레이터에서 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-151">In Eclipse, run the app on a physical Android device or the emulator.</span></span>
3. <span data-ttu-id="ffa2a-152">Android 앱 UI에서 사용자 이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-152">In the Android app UI, enter a username and password.</span></span> <span data-ttu-id="ffa2a-153">이는 임의 문자열일 수 있지만 같은 값이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-153">These can be any string, but they must be the same value.</span></span>
4. <span data-ttu-id="ffa2a-154">Android 앱 UI에서 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-154">In the Android app UI, click **Log in**.</span></span> <span data-ttu-id="ffa2a-155">그리고 나서 **푸시 보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffa2a-155">Then click **Send push**.</span></span>

