

1. <span data-ttu-id="cce5e-101">[Firebase 콘솔](https://firebase.google.com/console/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="cce5e-101">Sign in to the [Firebase console](https://firebase.google.com/console/).</span></span> <span data-ttu-id="cce5e-102">아직 없는 경우 새 Firebase 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cce5e-102">Create a new Firebase project if you don't already have one.</span></span>
2. <span data-ttu-id="cce5e-103">프로젝트를 만든 후에 **Android 앱에 Firebase 추가**를 클릭하고 제공된 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="cce5e-103">After your project is created, click **Add Firebase to your Android app** and follow the instructions provided.</span></span>

    ![](./media/notification-hubs-enable-firebase-cloud-messaging/notification-hubs-add-firebase-to-android-app.png)
3. <span data-ttu-id="cce5e-104">Firebase 콘솔에서 프로젝트에 대한 톱니바퀴를 클릭한 다음 **프로젝트 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cce5e-104">In the Firebase console, click the cog for your project and then click **Project Settings**.</span></span>

    ![](./media/notification-hubs-enable-firebase-cloud-messaging/notification-hubs-firebase-console-project-settings.png)
4. <span data-ttu-id="cce5e-105">프로젝트 설정에서 **클라우드 메시징** 탭을 클릭하고 **서버 키** 및 **보낸 사람 ID**의 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="cce5e-105">Click the **Cloud Messaging** tab in your project settings, and copy the value of the **Server key** and **Sender ID**.</span></span> <span data-ttu-id="cce5e-106">나중에 앱에서 알림 허브 액세스 정책 및 알림 처리기를 구성하는 데 이러한 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cce5e-106">These values will be used later to configure the notification hub access policy, and your notification handler in the app.</span></span>
