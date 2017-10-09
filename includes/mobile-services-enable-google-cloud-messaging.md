
1. <span data-ttu-id="7a959-101">Toohello 이동 [Google 클라우드 콘솔](https://console.developers.google.com/project), Google 계정 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a959-101">Navigate toohello [Google Cloud Console](https://console.developers.google.com/project), sign in with your Google account credentials.</span></span> 
2. <span data-ttu-id="7a959-102">**프로젝트 만들기**를 클릭하고 프로젝트 이름을 입력한 후에 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a959-102">Click **Create Project**, type a project name, then click **Create**.</span></span> <span data-ttu-id="7a959-103">요청 된 경우 hello SMS 확인을 수행 하 고 클릭 **만들기** 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a959-103">If requested, carry out hello SMS Verification, and click **Create** again.</span></span>
   
    ![새 프로젝트 만들기](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     <span data-ttu-id="7a959-105">새 **프로젝트 이름**을 입력하고 **프로젝트 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a959-105">Type in your new **Project name** and click **Create project**.</span></span>
3. <span data-ttu-id="7a959-106">Hello 클릭 **유틸리티 등** 단추를 선택한 다음 클릭 **프로젝트 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="7a959-106">Click hello **Utilities and More** button and then click **Project Information**.</span></span> <span data-ttu-id="7a959-107">Hello 메모 **프로젝트 번호**합니다.</span><span class="sxs-lookup"><span data-stu-id="7a959-107">Make a note of hello **Project Number**.</span></span> <span data-ttu-id="7a959-108">Tooset hello로이 값이 필요한 합니다 `SenderId` hello 클라이언트 앱에서 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="7a959-108">You will need tooset this value as hello `SenderId` variable in hello client app.</span></span>
   
    ![유틸리티 및 기타 정보](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. <span data-ttu-id="7a959-110">Hello, 대시보드를 아래에서 프로젝트 **모바일 Api**, 클릭 **Google Cloud Messaging**, hello 다음 페이지에서 클릭 **API 사용** hello 서비스 약관에 동의 하 고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a959-110">In hello project dashboard, under **Mobile APIs**, click **Google Cloud Messaging**, then on hello next page click **Enable API** and accept hello terms of service.</span></span> 
   
    ![GCM 사용 설정](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![GCM 사용 설정](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. <span data-ttu-id="7a959-113">Hello 프로젝트 대시보드 클릭 **자격 증명** > **Create Credential** > **API 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="7a959-113">In hello project dashboard, Click **Credentials** > **Create Credential** > **API Key**.</span></span> 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. <span data-ttu-id="7a959-114">**새 키 만들기**에서 **서버 키**를 클릭하고 사용자의 키에 대한 이름을 입력한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a959-114">In **Create a new key**, click **Server key**, type a name for your key, then click **Create**.</span></span>
7. <span data-ttu-id="7a959-115">Hello 메모 **API 키** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7a959-115">Make a note of hello **API KEY** value.</span></span>
   
    <span data-ttu-id="7a959-116">이 API 키 값 tooenable Azure tooauthenticate GCM과 함께 사용 되 고 응용 프로그램을 대신 하 여 푸시 알림을 보낼 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a959-116">You will use this API key value tooenable Azure tooauthenticate with GCM and send push notifications on behalf of your app.</span></span>

