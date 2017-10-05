---
title: "알림 허브 속보 자습서 - Android"
description: "Azure 서비스 버스 알림 허브를 사용하여 Android 장치에 최신 뉴스 알림을 보내는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 76ec01c874fceedab7d76b2ef58e4b45b5489f58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="adf5c-103">알림 허브를 사용하여 속보 보내기</span><span class="sxs-lookup"><span data-stu-id="adf5c-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="adf5c-104">개요</span><span class="sxs-lookup"><span data-stu-id="adf5c-104">Overview</span></span>
<span data-ttu-id="adf5c-105">이 항목에서는 Azure 알림 허브를 사용하여 Android 앱에 속보 알림을 브로드캐스트하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to an Android app.</span></span> <span data-ttu-id="adf5c-106">완료하면, 관심이 있는 속보 범주를 등록하고 해당 범주의 푸시 알림만 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-106">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="adf5c-107">이 시나리오는 RSS 수집기, 음악 애호가를 위한 앱 등 이전에 관심을 보인 사용자 그룹에 알림을 보내야 하는 많은 앱에 공통된 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-107">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="adf5c-108">브로드캐스트 시나리오를 사용하려면 알림 허브에서 등록을 만들 때 하나 이상의 *태그*를 포함하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="adf5c-109">태그에 알림이 전송되면 태그에 대해 등록된 모든 장치에서 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-109">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="adf5c-110">태그는 단순히 문자열이므로 사전에 프로비전해야 할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-110">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="adf5c-111">태그에 대한 자세한 내용은 [알림 허브 라우팅 및 태그 식](notification-hubs-tags-segment-push-message.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="adf5c-111">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="adf5c-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="adf5c-112">Prerequisites</span></span>
<span data-ttu-id="adf5c-113">이 항목은 [Notification Hubs 시작][get-started]에서 만든 앱을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-113">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="adf5c-114">이 자습서를 시작하기 전에 먼저 [Notification Hubs 시작][get-started]을 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="adf5c-115">앱에 범주 선택 추가</span><span class="sxs-lookup"><span data-stu-id="adf5c-115">Add category selection to the app</span></span>
<span data-ttu-id="adf5c-116">첫 번째 단계는 기존의 기본 활동에 사용자가 등록할 범주를 선택할 수 있도록 하는 UI 요소를 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-116">The first step is to add the UI elements to your existing main activity that enable the user to select categories to register.</span></span> <span data-ttu-id="adf5c-117">사용자가 선택한 범주는 장치에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-117">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="adf5c-118">앱을 시작하면 장치 등록이 선택한 범주와 함께 태그로서 알림 허브에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-118">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="adf5c-119">res/layout/activity_main.xml 파일을 열고 콘텐츠를 다음으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-119">Open your res/layout/activity_main.xml file, and substitute the content with the following:</span></span>
   
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
2. <span data-ttu-id="adf5c-120">res/values/strings.xml 파일을 열고 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-120">Open your res/values/strings.xml file and add the following lines:</span></span>
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    <span data-ttu-id="adf5c-121">main_activity.xml 그래픽 레이아웃은 다음과 같이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-121">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
3. <span data-ttu-id="adf5c-122">이제 **MainActivity** 클래스와 같은 패키지에서 **Notifications** 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-122">Now create a class **Notifications** in the same package as your **MainActivity** class.</span></span>
   
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
                            Log.e("MainActivity", "Failed to register - " + e.getMessage());
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
   
    <span data-ttu-id="adf5c-123">이 클래스는 로컬 저장소를 사용하여, 이 장치에서 받아야 할 뉴스의 범주를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-123">This class uses the local storage to store the categories of news that this device has to receive.</span></span> <span data-ttu-id="adf5c-124">이러한 범주를 등록하기 위한 메서드도 이 클래스에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-124">It also contains methods to register for these categories.</span></span>
4. <span data-ttu-id="adf5c-125">**MainActivity** 클래스에서 **NotificationHub** 및 **GoogleCloudMessaging**에 대한 Private 필드를 제거하고 **Notifications**에 대한 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-125">In your **MainActivity** class remove your private fields for **NotificationHub** and **GoogleCloudMessaging**, and add a field for **Notifications**:</span></span>
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. <span data-ttu-id="adf5c-126">**onCreate** 메서드에서 **hub** 필드 및 **registerWithNotificationHubs** 메서드의 초기화를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-126">Then, in the **onCreate** method, remove the initialization of the **hub** field and the **registerWithNotificationHubs** method.</span></span> <span data-ttu-id="adf5c-127">**Notifications** 클래스 인스턴스를 초기화하는 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-127">Then add the following lines which initialize an instance of the **Notifications** class.</span></span> 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    <span data-ttu-id="adf5c-128">`HubName`과 `HubListenConnectionString`은 이미 `<hub name>` 및 `<connection string with listen access>` 자리 표시자를 알림 허브 이름과 앞서 얻었던 *DefaultListenSharedAccessSignature*의 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-128">`HubName` and `HubListenConnectionString` should already be set with the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>

    > [AZURE.NOTE] <span data-ttu-id="adf5c-129">클라이언트 앱과 함께 배포되는 자격 증명은 일반적으로 안전하지 않기 때문에 클라이언트 앱과 함께 listen access용 키만 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-129">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="adf5c-130">Listen access를 통해 앱에서 알림을 등록할 수 있지만, 기존 등록을 수정할 수 없으며 알림을 전송할 수도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-130">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="adf5c-131">안전한 백 엔드 서비스에서 알림을 보내고 기존 등록을 변경하는 데에는 모든 권한 키가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-131">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>


1. <span data-ttu-id="adf5c-132">그런 후 다음 가져오기와 `subscribe` 메서드를 추가하여 구독 단추 클릭 이벤트를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-132">Then, add the following imports and `subscribe` method to handle the subscribe button click event:</span></span>
   
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
   
    <span data-ttu-id="adf5c-133">이 메서드는 범주 목록을 만들고 **Notifications** 클래스를 사용하여, 로컬 저장소에 목록을 저장하고 알림 허브에 해당 태그를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-133">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="adf5c-134">범주가 변경되면 새 범주로 등록이 다시 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-134">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="adf5c-135">이제 사용자가 범주 선택을 변경할 때마다 앱은 범주 집합을 장치의 로컬 저장소에 저장하고 알림 허브에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-135">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="adf5c-136">알림 등록</span><span class="sxs-lookup"><span data-stu-id="adf5c-136">Register for notifications</span></span>
<span data-ttu-id="adf5c-137">다음 단계에서는 로컬 저장소에 저장된 범주를 사용하여 시작 시 알림 허브에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-137">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="adf5c-138">GCM(Google Cloud Messaging)에서 할당하는 registrationId는 언제든지 변경될 수 있으므로 알림 실패를 피하려면 알림을 자주 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-138">Because the registrationId assigned by Google Cloud Messaging (GCM) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="adf5c-139">이 예제에서는 앱이 시작될 때마다 알림을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-139">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="adf5c-140">자주(하루 두 번 이상) 실행되는 앱에서는 이전 등록 이후 만 하루가 지나지 않은 경우 대역폭 유지를 위한 등록을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-140">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="adf5c-141">**MainActivity** 클래스에서 **onCreate** 메서드의 끝에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-141">Add the following code at the end of the **onCreate** method in the **MainActivity** class:</span></span>
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    <span data-ttu-id="adf5c-142">이제 앱이 시작될 때마다 로컬 저장소에서 범주를 검색하고, 이러한 범주에 대한 등록을 요청하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-142">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registeration for these categories.</span></span> 
2. <span data-ttu-id="adf5c-143">그런 후 다음과 같이 `MainActivity` 클래스의 `onStart()` 메서드를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-143">Then update the `onStart()` method of the `MainActivity` class as follows:</span></span>
   
    <span data-ttu-id="adf5c-144">@Override  protected void onStart() {</span><span class="sxs-lookup"><span data-stu-id="adf5c-144">@Override  protected void onStart() {</span></span>
   
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
    <span data-ttu-id="adf5c-145">}</span><span class="sxs-lookup"><span data-stu-id="adf5c-145">}</span></span>
   
    <span data-ttu-id="adf5c-146">전에 저장한 범주의 상태를 기반으로 기본 활동이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-146">This updates the main activity based on the status of previously saved categories.</span></span>

<span data-ttu-id="adf5c-147">이제 앱이 완료되며, 사용자가 범주 선택을 변경할 때마다 알림 허브 등록에 사용된 장치의 로컬 저장소에 범주 집합을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-147">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="adf5c-148">다음에는 범주 알림을 이 앱에 보낼 수 있는 백 엔드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-148">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="adf5c-149">태그가 지정된 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="adf5c-149">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="adf5c-150">앱 실행 및 알림 생성</span><span class="sxs-lookup"><span data-stu-id="adf5c-150">Run the app and generate notifications</span></span>
1. <span data-ttu-id="adf5c-151">Android Studio에서는 앱을 빌드하고 장치나 에뮬레이터에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-151">In Android Studio, build the app and start it on a device or emulator.</span></span>
   
    <span data-ttu-id="adf5c-152">앱 UI는 구독할 범주를 선택하도록 하는 토글 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-152">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="adf5c-153">하나 이상의 범주 토글을 사용하도록 설정한 후 **구독**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-153">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="adf5c-154">앱은 선택한 범주를 태그로 변환하고 알림 허브에서 선택한 태그에 대한 새로운 장치 등록을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-154">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="adf5c-155">등록된 범주가 반환되어 알림 메시지에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-155">The registered categories are returned and displayed in a toast notification.</span></span>
3. <span data-ttu-id="adf5c-156">.NET 콘솔 앱을 실행하여 새 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-156">Send a new notification by running the .NET Console app.</span></span>  <span data-ttu-id="adf5c-157">또는 [Azure 클래식 포털]에 있는 알림 허브의 디버그 탭을 사용하여 태그가 지정된 템플릿 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-157">Alternatively, you can send tagged template notifications using the debug tab of your notification hub in the [Azure Classic Portal].</span></span>
   
    <span data-ttu-id="adf5c-158">선택한 범주에 대한 알림이 알림 메시지로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-158">Notifications for the selected categories appear as toast notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="adf5c-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="adf5c-159">Next steps</span></span>
<span data-ttu-id="adf5c-160">이 자습서에서는 범주별로 속보를 브로드캐스트하는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="adf5c-160">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="adf5c-161">이제 기타 고급 알림 허브 시나리오를 다루는 다음 자습서 중 하나를 완료해 보세요.</span><span class="sxs-lookup"><span data-stu-id="adf5c-161">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="adf5c-162">[알림 허브를 사용하여 지역화된 속보 브로드캐스트]</span><span class="sxs-lookup"><span data-stu-id="adf5c-162">[Use Notification Hubs to broadcast localized breaking news]</span></span>
  
    <span data-ttu-id="adf5c-163">지역화된 알림을 보낼 수 있도록 속보 앱을 확장하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="adf5c-163">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

<!-- Images. -->
[A1]: ./media/notification-hubs-aspnet-backend-android-breaking-news/android-breaking-news1.PNG

<!-- URLs.-->
[get-started]: notification-hubs-android-push-notification-google-gcm-get-started.md
<span data-ttu-id="adf5c-164">[알림 허브를 사용하여 지역화된 속보 브로드캐스트]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span><span class="sxs-lookup"><span data-stu-id="adf5c-164">[Use Notification Hubs to broadcast localized breaking news]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span></span>
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
<span data-ttu-id="adf5c-165">[Azure 클래식 포털]: https://manage.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="adf5c-165">[Azure Classic Portal]: https://manage.windowsazure.com</span></span>
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
