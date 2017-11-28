
1. <span data-ttu-id="8983b-101">[Azure Portal](https://portal.azure.com/)에서 **모두 찾아보기** > **App Services** > Mobile Apps 백 엔드를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8983b-101">In the [Azure portal](https://portal.azure.com/), click **Browse All** > **App Services**, and then click your Mobile Apps back end.</span></span> <span data-ttu-id="8983b-102">**설정** 아래에서 **App Service 푸시**를 클릭한 후 알림 허브 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8983b-102">Under **Settings**, click **App Service Push**, and then click your notification hub name.</span></span>
2. <span data-ttu-id="8983b-103">**Google(GCM)**로 이동하고, 이전 절차에서 Firebase로부터 얻은 **Server Key** 값을 입력한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8983b-103">Go to **Google (GCM)**, enter the **Server Key** value that you obtained from Firebase in the previous procedure, and then click **Save**.</span></span>

    ![포털에서 GCM API 키 설정하기](./media/app-service-mobile-android-configure-push/mobile-push-api-key.png)

<span data-ttu-id="8983b-105">이제 Mobile Apps 백 엔드가 Firebase Cloud Messaging을 사용하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="8983b-105">The Mobile Apps back end is now configured to use Firebase Cloud Messaging.</span></span> <span data-ttu-id="8983b-106">알림 허브를 사용하여 Android 장치에서 실행 중인 앱에 푸시 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8983b-106">This enables you to send push notifications to your app running on an Android device, by using the notification hub.</span></span>

<!-- URLs. -->


<!-- images -->
