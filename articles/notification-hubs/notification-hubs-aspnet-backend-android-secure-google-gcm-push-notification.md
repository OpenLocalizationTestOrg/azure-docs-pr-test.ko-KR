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
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a><span data-ttu-id="2d68a-105">Azure 알림 허브를 사용하여 보안 푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="2d68a-105">Sending Secure Push Notifications with Azure Notification Hubs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2d68a-106">Windows 범용</span><span class="sxs-lookup"><span data-stu-id="2d68a-106">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="2d68a-107">iOS</span><span class="sxs-lookup"><span data-stu-id="2d68a-107">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="2d68a-108">Android</span><span class="sxs-lookup"><span data-stu-id="2d68a-108">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="2d68a-109">개요</span><span class="sxs-lookup"><span data-stu-id="2d68a-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2d68a-110">toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-110">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="2d68a-111">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2d68a-112">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d68a-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="2d68a-113">Microsoft Azure에서 푸시 알림 지원을 사용 하면 tooaccess 크게 간소화 됩니다. hello에 대 한 소비자 및 엔터프라이즈 응용 프로그램에서 푸시 알림 구현 하는 사용 하기 쉬운, 다중 플랫폼, 수평 확장 된 푸시 메시지 인프라 모바일 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-113">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push message infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="2d68a-114">때로는 tooregulatory 또는 보안 제약 조건 때문 응용 프로그램에서 hello 표준 푸시 알림 인프라를 통해 전송 될 수 없는 hello 알림 tooinclude를 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-114">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="2d68a-115">이 자습서에서는 tooachieve hello 클라이언트에 대 한 Android 장치 및 앱 백 엔드에서 hello 간에 안전 하 고 인증 된 연결을 통해 중요 한 정보를 전송 하 여 동일한 환경을 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-115">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client Android device and hello app backend.</span></span>

<span data-ttu-id="2d68a-116">상위 수준 hello 흐름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-116">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="2d68a-117">hello 앱 백 엔드에서:</span><span class="sxs-lookup"><span data-stu-id="2d68a-117">hello app back-end:</span></span>
   * <span data-ttu-id="2d68a-118">백 엔드 데이터베이스에 보안 페이로드를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-118">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="2d68a-119">Hello ID (보안 정보 없음 전송)이 알림 toohello Android 장치에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-119">Sends hello ID of this notification toohello Android device (no secure information is sent).</span></span>
2. <span data-ttu-id="2d68a-120">응용 프로그램에 액세스 hello 알림을 받은 경우 hello 장치 hello:</span><span class="sxs-lookup"><span data-stu-id="2d68a-120">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="2d68a-121">hello Android 장치가 hello 백 엔드에서 요청 hello 보안 페이로드를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-121">hello Android device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="2d68a-122">hello 앱 hello 장치에 대 한 알림으로 hello 페이로드를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-122">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="2d68a-123">hello 사용자가 로그인 한 후 toonote 하의 hello 흐름 이전 (및이 자습서에서는) 가정 hello 장치 로컬 저장소에 인증 토큰을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-123">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="2d68a-124">이 hello 장치는이 토큰을 사용 하 여 hello 알림 보안 페이로드를 검색할 수 있는 완전히 원활한 환경을 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-124">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="2d68a-125">응용 프로그램에서 hello 장치에서 인증 토큰을 저장 하지 않으면 또는 이러한 토큰을 만료 될 수 있습니다 하는 경우 hello 사용자 toolaunch hello 앱 메시지를 표시 하는 제네릭 알림 hello 푸시 알림을 받으면 hello 장치 응용 프로그램에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-125">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello push notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="2d68a-126">그런 다음 hello 앱 hello 사용자를 인증 하 고 hello 알림 페이로드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-126">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="2d68a-127">이 자습서에서는 보안 toosend 푸시 알림 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-127">This tutorial shows how toosend secure push notifications.</span></span> <span data-ttu-id="2d68a-128">Hello에 기반 [사용자에 게 알림](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) 자습서에서 단계를 완료 해야 hello 해당 자습서에서는 먼저 아직 없는 경우 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-128">It builds on hello [Notify Users](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) tutorial, so you should complete hello steps in that tutorial first if you haven't already.</span></span>

> [!NOTE]
> <span data-ttu-id="2d68a-129">이 자습서에서는 [알림 허브 시작(Android)](notification-hubs-android-push-notification-google-gcm-get-started.md)에 설명된 대로 알림 허브를 만들고 구성했다고 가정합니다</span><span class="sxs-lookup"><span data-stu-id="2d68a-129">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-android-project"></a><span data-ttu-id="2d68a-130">Hello Android 프로젝트를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-130">Modify hello Android project</span></span>
<span data-ttu-id="2d68a-131">앱 백 엔드에서 toosend 정당한 hello 수정 했으므로 *id* 푸시 알림의 있는 toochange 알림과 콜백을 백 엔드 tooretrieve hello 보안 메시지 toobe 표시 하 여 Android 앱 toohandle 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-131">Now that you modified your app back-end toosend just hello *id* of a push notification, you have toochange your Android app toohandle that notification and call back your back-end tooretrieve hello secure message toobe displayed.</span></span>
<span data-ttu-id="2d68a-132">tooachieve이이 목표를 Android 앱 알고 있어야 toomake 있는 어떻게 tooauthenticate 자체 백 엔드 hello 푸시 알림의 받을 때 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-132">tooachieve this goal, you have toomake sure that your Android app knows how tooauthenticate itself with your back-end when it receives hello push notifications.</span></span>

<span data-ttu-id="2d68a-133">에서는 이제 hello를 수정 합니다 *로그인* hello 순서 toosave hello 인증 헤더 값의 흐름 공유 응용 프로그램의 기본 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-133">We will now modify hello *login* flow in order toosave hello authentication header value in hello shared preferences of your app.</span></span> <span data-ttu-id="2d68a-134">유사한 메커니즘 사용된 toostore 수 앱 hello 모든 인증 토큰 (예: OAuth 토큰)는 사용자 자격 증명을 요구 하지 않고 toouse 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-134">Analogous mechanisms can be used toostore any authentication token (e.g. OAuth tokens) that hello app will have toouse without requiring user credentials.</span></span>

1. <span data-ttu-id="2d68a-135">Android 응용 프로그램 프로젝트에서 추가 상수 hello hello 맨 뒤 hello **MainActivity** 클래스:</span><span class="sxs-lookup"><span data-stu-id="2d68a-135">In your Android app project, add hello following constants at hello top of hello **MainActivity** class:</span></span>
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. <span data-ttu-id="2d68a-136">Hello에 여전히 **MainActivity** 클래스, 업데이트 hello `getAuthorizationHeader()` 코드 다음 메서드 toocontain hello:</span><span class="sxs-lookup"><span data-stu-id="2d68a-136">Still in hello **MainActivity** class, update hello `getAuthorizationHeader()` method toocontain hello following code:</span></span>
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. <span data-ttu-id="2d68a-137">Hello 다음 추가 `import` hello 위쪽 hello에 문을 **MainActivity** 파일:</span><span class="sxs-lookup"><span data-stu-id="2d68a-137">Add hello following `import` statements at hello top of hello **MainActivity** file:</span></span>
   
        import android.content.SharedPreferences;

<span data-ttu-id="2d68a-138">이제 hello 알림이 수신 되 면 호출 되는 hello 처리기를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-138">Now we will change hello handler that is called when hello notification is received.</span></span>

1. <span data-ttu-id="2d68a-139">Hello에 **MyHandler** 클래스 변경 hello `OnReceive()` 메서드 toocontain:</span><span class="sxs-lookup"><span data-stu-id="2d68a-139">In hello **MyHandler** class change hello `OnReceive()` method toocontain:</span></span>
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. <span data-ttu-id="2d68a-140">그런 다음 추가 hello `retrieveNotification()` hello 자리 표시자를 대체 하는 메서드를 `{back-end endpoint}` 백 엔드를 배포 하는 동안 가져온 hello 백 엔드 끝점을 사용:</span><span class="sxs-lookup"><span data-stu-id="2d68a-140">Then add hello `retrieveNotification()` method, replacing hello placeholder `{back-end endpoint}` with hello back-end endpoint obtained while deploying your back-end:</span></span>
   
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

<span data-ttu-id="2d68a-141">이 메서드는 앱 백 엔드 tooretrieve hello 알림이 기본 설정을 공유 하 고 일반 알림으로 표시 hello에 저장 된 hello 자격 증명을 사용 하 여 콘텐츠를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-141">This method calls your app back-end tooretrieve hello notification content using hello credentials stored in hello shared preferences and displays it as a normal notification.</span></span> <span data-ttu-id="2d68a-142">hello 알림 다른 푸시 알림 똑같이 toohello 응용 프로그램 사용자를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-142">hello notification looks toohello app user exactly like any other push notification.</span></span>

<span data-ttu-id="2d68a-143">누락 된 인증 헤더 속성 또는 hello 백 엔드가 거부 된 것이 좋습니다 toohandle hello 경우 인지 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-143">Note that it is preferable toohandle hello cases of missing authentication header property or rejection by hello back-end.</span></span> <span data-ttu-id="2d68a-144">대상 사용자 경험에 대부분의이 경우 hello 특정 처리에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-144">hello specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="2d68a-145">한 가지 방법은 toodisplay hello 사용자 tooauthenticate tooretrieve hello 실제 알림에 대 한 제네릭 프롬프트로 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-145">One option is toodisplay a notification with a generic prompt for hello user tooauthenticate tooretrieve hello actual notification.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="2d68a-146">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="2d68a-146">Run hello Application</span></span>
<span data-ttu-id="2d68a-147">toorun hello 응용 프로그램, 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-147">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="2d68a-148">**AppBackend** 가 Azure에 배포되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-148">Make sure **AppBackend** is deployed in Azure.</span></span> <span data-ttu-id="2d68a-149">Visual Studio를 사용 하는 경우 실행 hello **AppBackend** Web API 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-149">If using Visual Studio, run hello **AppBackend** Web API application.</span></span> <span data-ttu-id="2d68a-150">ASP.NET 웹 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-150">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="2d68a-151">Eclipse에서 실제 Android 장치 또는 hello 에뮬레이터의 hello 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-151">In Eclipse, run hello app on a physical Android device or hello emulator.</span></span>
3. <span data-ttu-id="2d68a-152">Hello Android 앱 UI를 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-152">In hello Android app UI, enter a username and password.</span></span> <span data-ttu-id="2d68a-153">모든 문자열을 지정할 수 있습니다 이러한 있지만 해야만 해당 hello 동일한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-153">These can be any string, but they must be hello same value.</span></span>
4. <span data-ttu-id="2d68a-154">Hello Android 앱 UI의에서 클릭 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-154">In hello Android app UI, click **Log in**.</span></span> <span data-ttu-id="2d68a-155">그리고 나서 **푸시 보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2d68a-155">Then click **Send push**.</span></span>

