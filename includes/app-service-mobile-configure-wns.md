
1. <span data-ttu-id="e7cc3-101">[Azure Portal](https://portal.azure.com/)에서 **모두 찾아보기** > **App Services** > Mobile Apps 백 엔드를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7cc3-101">In the [Azure portal](https://portal.azure.com/), click **Browse All** > **App Services**, and click your Mobile Apps back end.</span></span> <span data-ttu-id="e7cc3-102">**설정** 아래에서 **App Service 푸시**를 클릭한 후 알림 허브 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7cc3-102">Under **Settings**, click **App Service Push**, and then click your notification hub name.</span></span>
2. <span data-ttu-id="e7cc3-103">**Windows(WNS)**로 이동하고 Live 서비스 사이트에서 가져온 **보안 키**(클라이언트 암호) 및 **패키지 SID**를 입력한 후 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7cc3-103">Go to **Windows (WNS)**, enter the **Security key** (client secret) and **Package SID** that you obtained from the Live Services site, and then click **Save**.</span></span>

    ![포털에서 WNS 키 설정](./media/app-service-mobile-configure-wns/mobile-push-wns-credentials.png)

<span data-ttu-id="e7cc3-105">이제 백 엔드가 WNS를 사용하여 푸시 알림을 보내도록 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e7cc3-105">Your back end is now configured to use WNS to send push notifications.</span></span>
