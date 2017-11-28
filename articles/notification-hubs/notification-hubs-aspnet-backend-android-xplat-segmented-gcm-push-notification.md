---
title: "aaaNotification 허브 주요 속보 자습서-Android"
description: "자세한 방법을 toouse Azure 서비스 버스 알림 허브 toosend 뉴스 알림 tooAndroid 장치를 중단 합니다."
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 3c23cb80-9d35-4dde-b26d-a7bfd4cb8f81
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: e6eb41bec95c67d7dc059f560194966d04400494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="fce11-103">알림 허브 toosend 최신 뉴스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="fce11-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="fce11-104">개요</span><span class="sxs-lookup"><span data-stu-id="fce11-104">Overview</span></span>
<span data-ttu-id="fce11-105">이 항목에서는 toouse Azure 알림 허브 toobroadcast 주요 뉴스 알림 tooan Android 앱.</span><span class="sxs-lookup"><span data-stu-id="fce11-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooan Android app.</span></span> <span data-ttu-id="fce11-106">완료 되 면에 관심이 있는 뉴스 범주 파괴 수 tooregister 수 및 해당 범주에 대 한 푸시 알림을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-106">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="fce11-107">이 시나리오는 알림을 그 예: RSS 수집기, 음악 팬 속도 등에 대 한 앱에 대 한 관심 선언 이전에 사용자의 전송 toobe toogroups 있는 많은 응용 프로그램에 대 한 일반적인 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-107">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="fce11-108">브로드캐스트 시나리오 하나 이상 포함 하 여 설정 된 *태그* hello 알림 허브의 등록을 만들 때.</span><span class="sxs-lookup"><span data-stu-id="fce11-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="fce11-109">알림을 tooa 태그를 보내면 hello 태그에 대 한 모든 장치를 등록 한 hello 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-109">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="fce11-110">태그는 단순히 문자열을 하기 때문에 미리 프로 비전 toobe를 갖지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-110">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="fce11-111">태그에 대 한 자세한 내용은 참조 너무[알림 허브 라우팅 및 태그 식](notification-hubs-tags-segment-push-message.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-111">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fce11-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fce11-112">Prerequisites</span></span>
<span data-ttu-id="fce11-113">이 항목에서는에서 만든 hello 앱 [알림 허브 시작][get-started]합니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-113">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="fce11-114">이 자습서를 시작하기 전에 먼저 [Notification Hubs 시작][get-started]을 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="fce11-115">범주 선택 toohello 앱 추가</span><span class="sxs-lookup"><span data-stu-id="fce11-115">Add category selection toohello app</span></span>
<span data-ttu-id="fce11-116">hello 첫 번째 단계는 tooadd hello UI 요소 tooyour 기존 기본 활동 hello 사용자 tooselect 범주 tooregister 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-116">hello first step is tooadd hello UI elements tooyour existing main activity that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="fce11-117">사용자가 선택한 hello 범주 hello 장치에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-117">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="fce11-118">Hello 앱이 시작 되 면 태그로 hello 선택한 범주와 알림 허브에 장치 등록이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-118">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="fce11-119">Res/layout/activity_main.xml 파일을 열고 hello 다음과 같이 hello 콘텐츠를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-119">Open your res/layout/activity_main.xml file, and substitute hello content with hello following:</span></span>
   
        <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:tools="http://schemas.android.com/tools"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:paddingBottom="@dimen/activity_vertical_margin"
            android:paddingLeft="@dimen/activity_horizontal_margin"
            android:paddingRight="@dimen/activity_horizontal_margin"
            android:paddingTop="@dimen/activity_vertical_margin"
            tools:context="com.example.breakingnews.MainActivity"
            android:orientation="vertical">
   
                <CheckBox
                    android:id="@+id/worldBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_world" />
                <CheckBox
                    android:id="@+id/politicsBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_politics" />
                <CheckBox
                    android:id="@+id/businessBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_business" />
                <CheckBox
                    android:id="@+id/technologyBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_technology" />
                <CheckBox
                    android:id="@+id/scienceBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_science" />
                <CheckBox
                    android:id="@+id/sportsBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_sports" />
                <Button
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:onClick="subscribe"
                    android:text="@string/button_subscribe" />
        </LinearLayout>
2. <span data-ttu-id="fce11-120">Res/values/strings.xml 파일을 열고 hello 다음 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-120">Open your res/values/strings.xml file and add hello following lines:</span></span>
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    <span data-ttu-id="fce11-121">main_activity.xml 그래픽 레이아웃은 다음과 같이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-121">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
3. <span data-ttu-id="fce11-122">이제 클래스를 만들 **알림** 패키징하여 동일 hello에 프로그램 **MainActivity** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-122">Now create a class **Notifications** in hello same package as your **MainActivity** class.</span></span>
   
        import java.util.HashSet;
        import java.util.Set;
   
        import android.content.Context;
        import android.content.SharedPreferences;
        import android.os.AsyncTask;
        import android.util.Log;
        import android.widget.Toast;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class Notifications {
            private static final String PREFS_NAME = "BreakingNewsCategories";
            private GoogleCloudMessaging gcm;
            private NotificationHub hub;
            private Context context;
            private String senderId;
   
            public Notifications(Context context, String senderId, String hubName, 
                                    String listenConnectionString) {
                this.context = context;
                this.senderId = senderId;
   
                gcm = GoogleCloudMessaging.getInstance(context);
                hub = new NotificationHub(hubName, listenConnectionString, context);
            }
   
            public void storeCategoriesAndSubscribe(Set<String> categories)
            {
                SharedPreferences settings = context.getSharedPreferences(PREFS_NAME, 0);
                settings.edit().putStringSet("categories", categories).commit();
                subscribeToCategories(categories);
            }
   
            public Set<String> retrieveCategories() {
                SharedPreferences settings = context.getSharedPreferences(PREFS_NAME, 0);
                return settings.getStringSet("categories", new HashSet<String>());
            }
   
            public void subscribeToCategories(final Set<String> categories) {
                new AsyncTask<Object, Object, Object>() {
                    @Override
                    protected Object doInBackground(Object... params) {
                        try {
                            String regid = gcm.register(senderId);
   
                            String templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";
   
                            hub.registerTemplate(regid,"simpleGCMTemplate", templateBodyGCM, 
                                categories.toArray(new String[categories.size()]));
                        } catch (Exception e) {
                            Log.e("MainActivity", "Failed tooregister - " + e.getMessage());
                            return e;
                        }
                        return null;
                    }
   
                    protected void onPostExecute(Object result) {
                        String message = "Subscribed for categories: "
                                + categories.toString();
                        Toast.makeText(context, message,
                                Toast.LENGTH_LONG).show();
                    }
                }.execute(null, null, null);
            }
   
        }
   
    <span data-ttu-id="fce11-123">이 클래스는이 장치에는 tooreceive 뉴스의 hello toostore hello 범주를 로컬 저장소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-123">This class uses hello local storage toostore hello categories of news that this device has tooreceive.</span></span> <span data-ttu-id="fce11-124">또한 이러한 범주에 대 한 메서드 tooregister 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-124">It also contains methods tooregister for these categories.</span></span>
4. <span data-ttu-id="fce11-125">**MainActivity** 클래스에서 **NotificationHub** 및 **GoogleCloudMessaging**에 대한 Private 필드를 제거하고 **Notifications**에 대한 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-125">In your **MainActivity** class remove your private fields for **NotificationHub** and **GoogleCloudMessaging**, and add a field for **Notifications**:</span></span>
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. <span data-ttu-id="fce11-126">그런 다음, hello **onCreate** 메서드, remove hello 초기화 hello **허브** 필드와 hello **registerWithNotificationHubs** 메서드.</span><span class="sxs-lookup"><span data-stu-id="fce11-126">Then, in hello **onCreate** method, remove hello initialization of hello **hub** field and hello **registerWithNotificationHubs** method.</span></span> <span data-ttu-id="fce11-127">그런 다음 위의 삼각형 hello의 인스턴스를 초기화 하는 hello를 추가 **알림** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-127">Then add hello following lines which initialize an instance of hello **Notifications** class.</span></span> 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    <span data-ttu-id="fce11-128">`HubName`및 `HubListenConnectionString` hello로 이미 설정 되어 있어야 `<hub name>` 및 `<connection string with listen access>` 와 알림 허브 이름 및 hello 연결 문자열에 대 한 자리 표시자 *DefaultListenSharedAccessSignature* 가져온 이전 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-128">`HubName` and `HubListenConnectionString` should already be set with hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>

    > [AZURE.NOTE] <span data-ttu-id="fce11-129">클라이언트 응용 프로그램과 함께 배포 되는 자격 증명에 일반적으로 안전 하지 않으므로 클라이언트 응용 프로그램과 함께 수신 액세스에 대 한 hello 키만 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-129">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="fce11-130">알림, 하지만 기존 등록에 대 한 응용 프로그램 tooregister 프로그램을 수정할 수 없는 액세스 활성화를 수신 하 고 알림을 보낼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-130">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="fce11-131">hello 전체 액세스 키를 사용 하 여 보안 된 백 엔드 서비스 알림을 전송 하 고 기존 등록을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-131">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>


1. <span data-ttu-id="fce11-132">그런 다음 다음 hello 가져오기를 추가 및 `subscribe` 메서드 toohandle hello 구독 단추 클릭 이벤트:</span><span class="sxs-lookup"><span data-stu-id="fce11-132">Then, add hello following imports and `subscribe` method toohandle hello subscribe button click event:</span></span>
   
        import android.widget.CheckBox;
        import java.util.HashSet;
        import java.util.Set;
   
        public void subscribe(View sender) {
            final Set<String> categories = new HashSet<String>();
   
            CheckBox world = (CheckBox) findViewById(R.id.worldBox);
            if (world.isChecked())
                categories.add("world");
            CheckBox politics = (CheckBox) findViewById(R.id.politicsBox);
            if (politics.isChecked())
                categories.add("politics");
            CheckBox business = (CheckBox) findViewById(R.id.businessBox);
            if (business.isChecked())
                categories.add("business");
            CheckBox technology = (CheckBox) findViewById(R.id.technologyBox);
            if (technology.isChecked())
                categories.add("technology");
            CheckBox science = (CheckBox) findViewById(R.id.scienceBox);
            if (science.isChecked())
                categories.add("science");
            CheckBox sports = (CheckBox) findViewById(R.id.sportsBox);
            if (sports.isChecked())
                categories.add("sports");
   
            notifications.storeCategoriesAndSubscribe(categories);
        }
   
    <span data-ttu-id="fce11-133">이 메서드가 만드는 범주 및 사용 하 여 hello 목록이 **알림** toostore hello 목록 hello 로컬 저장소에 클래스 및 해당 태그 hello 알림 허브에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-133">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="fce11-134">범주 변경 되 면 hello 등록 hello 새 범주와 다시 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-134">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="fce11-135">앱은 hello 장치의 로컬 저장소에 수 toostore 범주 집합에 포함 되었습니다 및 hello 사용자 변경 내용을 hello 범주의 선택 될 때마다 hello 알림 허브에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-135">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="fce11-136">알림 등록</span><span class="sxs-lookup"><span data-stu-id="fce11-136">Register for notifications</span></span>
<span data-ttu-id="fce11-137">이러한 단계는 시작할 때 로컬 저장소에 저장 된 hello 범주를 사용 하 여 hello 알림 허브를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-137">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="fce11-138">Google 클라우드 메시징 (GCM)에서 할당 된 hello registrationId 언제 든 지 변경할 수 있습니다, 때문에 등록 해야 알림에 대 한 자주 tooavoid 알림 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-138">Because hello registrationId assigned by Google Cloud Messaging (GCM) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="fce11-139">이 예제에서는 hello 이러한 앱이 시작 될 때마다 알림을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-139">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="fce11-140">자주 실행 되는 응용 프로그램의 경우 하루에 한 번 이상 건너뛸 수 있습니다 아마도 등록 toopreserve 대역폭 hello 이전 등록 이후 1 일 미만 경과한 경우.</span><span class="sxs-lookup"><span data-stu-id="fce11-140">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="fce11-141">Hello 코드 hello의 hello 끝에 다음 추가 **onCreate** hello에 대 한 메서드 **MainActivity** 클래스:</span><span class="sxs-lookup"><span data-stu-id="fce11-141">Add hello following code at hello end of hello **onCreate** method in hello **MainActivity** class:</span></span>
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    <span data-ttu-id="fce11-142">이렇게 하면 hello 앱 시작 될 때마다 로컬 저장소에서 검색 하는 hello 범주를 이러한 범주에 대 한 등록을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-142">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registeration for these categories.</span></span> 
2. <span data-ttu-id="fce11-143">Hello를 업데이트할 `onStart()` hello 방식의 `MainActivity` 클래스를 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-143">Then update hello `onStart()` method of hello `MainActivity` class as follows:</span></span>
   
    <span data-ttu-id="fce11-144">@Override  protected void onStart() {</span><span class="sxs-lookup"><span data-stu-id="fce11-144">@Override  protected void onStart() {</span></span>
   
        super.onStart();
        isVisible = true;
   
        Set<String> categories = notifications.retrieveCategories();
   
        CheckBox world = (CheckBox) findViewById(R.id.worldBox);
        world.setChecked(categories.contains("world"));
        CheckBox politics = (CheckBox) findViewById(R.id.politicsBox);
        politics.setChecked(categories.contains("politics"));
        CheckBox business = (CheckBox) findViewById(R.id.businessBox);
        business.setChecked(categories.contains("business"));
        CheckBox technology = (CheckBox) findViewById(R.id.technologyBox);
        technology.setChecked(categories.contains("technology"));
        CheckBox science = (CheckBox) findViewById(R.id.scienceBox);
        science.setChecked(categories.contains("science"));
        CheckBox sports = (CheckBox) findViewById(R.id.sportsBox);
        sports.setChecked(categories.contains("sports"));
    <span data-ttu-id="fce11-145">}</span><span class="sxs-lookup"><span data-stu-id="fce11-145">}</span></span>
   
    <span data-ttu-id="fce11-146">이전에 저장 된 범주의 hello 상태에 따라 hello 기본 활동을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-146">This updates hello main activity based on hello status of previously saved categories.</span></span>

<span data-ttu-id="fce11-147">hello 앱 완료 되며 hello 사용자 변경 내용을 hello 범주의 선택 될 때마다 hello 알림 허브와 장치 사용 되는 로컬 저장소 tooregister hello 범주 집합을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-147">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="fce11-148">다음으로, 알림 toothis 앱 범주를 보낼 수 있는 백 엔드를 정의 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-148">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="fce11-149">태그가 지정된 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="fce11-149">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="fce11-150">Hello 앱을 실행 하 고 알림 생성</span><span class="sxs-lookup"><span data-stu-id="fce11-150">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="fce11-151">Android Studio에서 hello 앱을 빌드하고 장치 또는 에뮬레이터에서 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-151">In Android Studio, build hello app and start it on a device or emulator.</span></span>
   
    <span data-ttu-id="fce11-152">참고 hello 앱 UI의 집합을 제공 하는 설정/해제를 hello 범주 toosubscribe를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-152">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="fce11-153">하나 이상의 범주 토글을 사용하도록 설정한 후 **구독**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-153">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="fce11-154">hello 앱 태그에 hello 선택한 범주를 변환 하 고 hello 알림 허브에서 선택 하는 hello 태그에 대 한 새 장치 등록을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-154">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="fce11-155">hello 등록 된 범주는 반환 된 없으며 알림 메시지에에서 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-155">hello registered categories are returned and displayed in a toast notification.</span></span>
3. <span data-ttu-id="fce11-156">Hello.NET 콘솔 응용 프로그램을 실행 하 여 새 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-156">Send a new notification by running hello .NET Console app.</span></span>  <span data-ttu-id="fce11-157">Hello 알림 허브의 hello 디버그 탭을 사용 하는 태그가 지정 된 템플릿 알림을 보낼 수 또는 [Azure 클래식 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-157">Alternatively, you can send tagged template notifications using hello debug tab of your notification hub in hello [Azure Classic Portal].</span></span>
   
    <span data-ttu-id="fce11-158">알림 메시지 hello 선택한 범주에 대 한 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-158">Notifications for hello selected categories appear as toast notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fce11-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fce11-159">Next steps</span></span>
<span data-ttu-id="fce11-160">이 자습서에서는 이전에 배운 것 어떻게 toobroadcast 최신 뉴스 범주별으로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-160">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="fce11-161">기타 고급 알림 허브 시나리오를 강조 표시 하는 자습서를 따라 hello 중 하나를 완료 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-161">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="fce11-162">[알림 허브 지역화 toobroadcast 주요 뉴스를 사용 하 여]</span><span class="sxs-lookup"><span data-stu-id="fce11-162">[Use Notification Hubs toobroadcast localized breaking news]</span></span>
  
    <span data-ttu-id="fce11-163">뉴스 앱 tooenable 보내는 주요 tooexpand hello 알림을 지역화 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fce11-163">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

<!-- Images. -->
[A1]: ./media/notification-hubs-aspnet-backend-android-breaking-news/android-breaking-news1.PNG

<!-- URLs.-->
[get-started]: notification-hubs-android-push-notification-google-gcm-get-started.md
[알림 허브 지역화 toobroadcast 주요 뉴스를 사용 하 여]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Azure 클래식 포털]: https://manage.windowsazure.com
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
