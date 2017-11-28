
1. <span data-ttu-id="bd739-101">[Google 클라우드 콘솔](https://console.developers.google.com/project)로 이동하고 Google 계정 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bd739-101">Navigate to the [Google Cloud Console](https://console.developers.google.com/project), sign in with your Google account credentials.</span></span> 
2. <span data-ttu-id="bd739-102">**프로젝트 만들기**를 클릭하고 프로젝트 이름을 입력한 후에 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd739-102">Click **Create Project**, type a project name, then click **Create**.</span></span> <span data-ttu-id="bd739-103">요청된 경우 SMS 확인을 수행하고 **Create** 를 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd739-103">If requested, carry out the SMS Verification, and click **Create** again.</span></span>
   
    ![새 프로젝트 만들기](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     <span data-ttu-id="bd739-105">새 **프로젝트 이름**을 입력하고 **프로젝트 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd739-105">Type in your new **Project name** and click **Create project**.</span></span>
3. <span data-ttu-id="bd739-106">**유틸리티 및 기타** 단추를 클릭한 다음 **프로젝트 정보**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd739-106">Click the **Utilities and More** button and then click **Project Information**.</span></span> <span data-ttu-id="bd739-107">**프로젝트 번호**를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="bd739-107">Make a note of the **Project Number**.</span></span> <span data-ttu-id="bd739-108">이 값을 클라이언트 앱의 `SenderId` 변수로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd739-108">You will need to set this value as the `SenderId` variable in the client app.</span></span>
   
    ![유틸리티 및 기타 정보](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. <span data-ttu-id="bd739-110">프로젝트 대시보드의 **모바일 API**에서 **Google Cloud Messaging**을 클릭하고 다음 페이지에서 **Enable API**를 클릭하고 서비스 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="bd739-110">In the project dashboard, under **Mobile APIs**, click **Google Cloud Messaging**, then on the next page click **Enable API** and accept the terms of service.</span></span> 
   
    ![GCM 사용 설정](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![GCM 사용 설정](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. <span data-ttu-id="bd739-113">프로젝트 대시보드에서 **자격 증명** > **자격 증명 만들기** > **API 키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd739-113">In the project dashboard, Click **Credentials** > **Create Credential** > **API Key**.</span></span> 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. <span data-ttu-id="bd739-114">**새 키 만들기**에서 **서버 키**를 클릭하고 사용자의 키에 대한 이름을 입력한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd739-114">In **Create a new key**, click **Server key**, type a name for your key, then click **Create**.</span></span>
7. <span data-ttu-id="bd739-115">**API key** 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="bd739-115">Make a note of the **API KEY** value.</span></span>
   
    <span data-ttu-id="bd739-116">이 API 키를 사용하여 Azure 에서 GCM에 인증하고 앱 대신 푸시 알림을 보낼 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd739-116">You will use this API key value to enable Azure to authenticate with GCM and send push notifications on behalf of your app.</span></span>

