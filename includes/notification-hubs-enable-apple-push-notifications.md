

## <a name="generate-hello-certificate-signing-request-file"></a><span data-ttu-id="6c795-101">Hello 인증서 서명 요청 파일 생성</span><span class="sxs-lookup"><span data-stu-id="6c795-101">Generate hello Certificate Signing Request file</span></span>
<span data-ttu-id="6c795-102">인증서 tooauthenticate 푸시 알림을 사용 하는 hello 푸시 알림 서비스 APNS (Apple) 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-102">hello Apple Push Notification Service (APNS) uses certificates tooauthenticate your push notifications.</span></span> <span data-ttu-id="6c795-103">이러한 지침은 toocreate hello 필요한 푸시 인증서 toosend 따르고 알림을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-103">Follow these instructions toocreate hello necessary push certificate toosend and receive notifications.</span></span> <span data-ttu-id="6c795-104">이러한 개념에 대 한 자세한 내용은 참조 hello 공식 [Apple 푸시 알림 서비스](http://go.microsoft.com/fwlink/p/?LinkId=272584) 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-104">For more information on these concepts see hello official [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentation.</span></span>

<span data-ttu-id="6c795-105">hello 요청 CSR (인증서 서명) 파일을 생성에서 사용 하는 Apple toogenerate 서명 된 푸시 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-105">Generate hello Certificate Signing Request (CSR) file, which is used by Apple toogenerate a signed push certificate.</span></span>

1. <span data-ttu-id="6c795-106">Mac에서 hello 키 집합 액세스 도구를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-106">On your Mac, run hello Keychain Access tool.</span></span> <span data-ttu-id="6c795-107">Hello에서 열 수 있는 **유틸리티** 폴더 또는 hello **다른** hello 실행 패드에서 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-107">It can be opened from hello **Utilities** folder or hello **Other** folder on hello launch pad.</span></span>
2. <span data-ttu-id="6c795-108">**Keychain Access**를 클릭하고 **Certificate Assistant**를 확장한 다음 **Request a Certificate from a Certificate Authority...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-108">Click **Keychain Access**, expand **Certificate Assistant**, then click **Request a Certificate from a Certificate Authority...**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. <span data-ttu-id="6c795-109">선택 하면 **사용자 전자 메일 주소** 및 **일반 이름** , 있는지 확인 **toodisk 저장** 을 선택한 다음 클릭 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-109">Select your **User Email Address** and **Common Name** , make sure that **Saved toodisk** is selected, and then click **Continue**.</span></span> <span data-ttu-id="6c795-110">Hello 둡니다 **CA 전자 메일 주소** 필드를 비워은 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-110">Leave hello **CA Email Address** field blank as it is not required.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. <span data-ttu-id="6c795-111">Hello 요청 CSR (인증서 서명) 파일에 대 한 이름을 입력 **다른 이름으로 저장**에서 hello 위치를 선택 **여기서**, 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-111">Type a name for hello Certificate Signing Request (CSR) file in **Save As**, select hello location in **Where**, then click **Save**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      <span data-ttu-id="6c795-112">선택한 hello location;에 hello CSR 파일을 저장이 hello 데스크톱 hello 기본 위치가입니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-112">This saves hello CSR file in hello selected location; hello default location is in hello Desktop.</span></span> <span data-ttu-id="6c795-113">이 파일에 대해 선택한 hello 위치를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-113">Remember hello location chosen for this file.</span></span>

<span data-ttu-id="6c795-114">다음으로 앱을 Apple에 등록, 푸시 알림을 사용 하도록 설정 하 고이 내보낸된 CSR toocreate 푸시 인증서를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-114">Next, you will register your app with Apple, enable push notifications, and upload this exported CSR toocreate a push certificate.</span></span>

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="6c795-115">푸시 알림에 대해 앱 등록</span><span class="sxs-lookup"><span data-stu-id="6c795-115">Register your app for push notifications</span></span>
<span data-ttu-id="6c795-116">toobe 수 toosend 푸시 알림을 tooan iOS 앱을 Apple 및 레지스터를 푸시 알림을 사용 하 여 응용 프로그램을 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-116">toobe able toosend push notifications tooan iOS app, you must register your application with Apple and also register for push notifications.</span></span>  

1. <span data-ttu-id="6c795-117">이미 앱을 등록 하지 않은 경우 탐색 toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS 프로 비전 포털</a> hello Apple 개발자 센터를 Apple ID로, 로그온 클릭 **식별자**, 클릭 **의 앱 Id** , 마지막으로 hello에서을 클릭 하 고  **+**  tooregister 새 앱을 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-117">If you have not already registered your app, navigate toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a> at hello Apple Developer Center, log on with your Apple ID, click **Identifiers**, then click **App IDs**, and finally click on hello **+** sign tooregister a new app.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. <span data-ttu-id="6c795-118">새 응용 프로그램에 대 한 세 개의 필드가 다음 hello를 업데이트 한 다음 클릭 **계속**:</span><span class="sxs-lookup"><span data-stu-id="6c795-118">Update hello following three fields for your new app and then click **Continue**:</span></span>
   
   * <span data-ttu-id="6c795-119">**이름**: hello에 앱에 대 한 설명이 포함 된 이름을 입력 **이름** 필드 hello에 **응용 프로그램 ID 설명** 섹션.</span><span class="sxs-lookup"><span data-stu-id="6c795-119">**Name**: Type a descriptive name for your app in hello **Name** field in hello **App ID Description** section.</span></span>
   * <span data-ttu-id="6c795-120">**번들 식별자**: hello에서 **명시적 앱 ID** 섹션을 입력 한 **번들 식별자** hello 형태로 `<Organization Identifier>.<Product Name>` hello에 설명 된 대로 [앱 배포 가이드](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8)합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-120">**Bundle Identifier**: Under hello **Explicit App ID** section, enter a **Bundle Identifier** in hello form `<Organization Identifier>.<Product Name>` as mentioned in hello [App Distribution Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span></span> <span data-ttu-id="6c795-121">hello *조직 식별자* 및 *제품 이름* 합니다를 사용 하 여 hello 조직 식별자 및 XCode 프로젝트를 만들 때 사용할 제품 이름과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-121">hello *Organization Identifier* and *Product Name* you use must match hello organization identifier and product name you will use when you create your XCode project.</span></span> <span data-ttu-id="6c795-122">Hello screeshot 아래에서 *NotificationHubs* 조직 식별자로 사용 되 고 *GetStarted* hello 제품 이름으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-122">In hello screeshot below *NotificationHubs* is used as a organization idenitifier and *GetStarted* is used as hello product name.</span></span> <span data-ttu-id="6c795-123">이때 XCode 프로젝트에서 사용할 hello 값이 일치 해야 하면 toouse hello 올바른 게시 프로필 xcode를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-123">Making sure this matches hello values you will use in your XCode project will allow you toouse hello correct publishing profile with XCode.</span></span> 
   * <span data-ttu-id="6c795-124">**푸시 알림**: 검사 hello **푸시 알림을** hello에 대 한 옵션 **응용 프로그램 서비스** 섹션.</span><span class="sxs-lookup"><span data-stu-id="6c795-124">**Push Notifications**: Check hello **Push Notifications** option in hello **App Services** section, .</span></span>
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      <span data-ttu-id="6c795-125">이 응용 프로그램 ID를 생성 하 고 tooconfirm hello 정보를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-125">This generates your App ID and requests you tooconfirm hello information.</span></span> <span data-ttu-id="6c795-126">클릭 **등록** tooconfirm hello 새 응용 프로그램 id입니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-126">Click **Register** tooconfirm hello new App ID.</span></span>
     
      <span data-ttu-id="6c795-127">클릭 한 후 **등록**, hello 나타납니다 **등록이 완료** 화면에서 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-127">Once you click **Register**, you will see hello **Registration complete** screen, as shown below.</span></span> <span data-ttu-id="6c795-128">**Done**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-128">Click **Done**.</span></span>
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. <span data-ttu-id="6c795-129">Hello App Id에서 개발자 센터에서에서 방금 만든 하 고 해당 행을 클릭 하는 hello 응용 프로그램 ID를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-129">In hello Developer Center, under App IDs, locate hello app ID that you just created, and click on its row.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      <span data-ttu-id="6c795-130">Hello 앱 ID를 클릭 하는 hello 응용 프로그램 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-130">Clicking on hello app ID will display hello app details.</span></span> <span data-ttu-id="6c795-131">Hello 클릭 **편집** hello 아래쪽 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-131">Click hello **Edit** button at hello bottom.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. <span data-ttu-id="6c795-132">Toohello hello 화면 아래쪽을 스크롤하여 클릭 hello **인증서 만들기...**  hello 섹션에 따라 단추 **개발 푸시 SSL 인증서**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-132">Scroll toohello bottom of hello screen, and click hello **Create Certificate...** button under hello section **Development Push SSL Certificate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      <span data-ttu-id="6c795-133">Hello "iOS 인증서 추가" 도우미를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-133">This displays hello "Add iOS Certificate" assistant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6c795-134">이 자습서에서는 개발 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-134">This tutorial uses a development certificate.</span></span> <span data-ttu-id="6c795-135">프로덕션 인증서를 등록할 때 동일한 프로세스를 사용 하는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-135">hello same process is used when registering a production certificate.</span></span> <span data-ttu-id="6c795-136">Hello를 사용 하는 있는지만 알림을 보낼 때 동일한 인증서 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-136">Just make sure that you use hello same certificate type when sending notifications.</span></span>
   > 
   > 
3. <span data-ttu-id="6c795-137">클릭 **파일 선택**hello 첫 번째 작업에서 만든 hello CSR 파일을 저장 한 toohello 위치를 찾은 다음 클릭, **생성**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-137">Click **Choose File**, browse toohello location where you saved hello CSR file that you created in hello first task, then click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. <span data-ttu-id="6c795-138">Hello 인증서 hello 포털에서 만들어지면 클릭 hello **다운로드** 단추를 클릭 하 고 **수행**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-138">After hello certificate is created by hello portal, click hello **Download** button, and click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      <span data-ttu-id="6c795-139">이 hello 인증서를 다운로드 하 고 tooyour 컴퓨터 Downloads 폴더에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-139">This downloads hello certificate and saves it tooyour computer in your Downloads folder.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > <span data-ttu-id="6c795-140">기본적으로 hello 개발 인증서 라는 파일을 다운로드 **aps_development.cer**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-140">By default, hello downloaded file a development certificate is named **aps_development.cer**.</span></span>
   > 
   > 
5. <span data-ttu-id="6c795-141">Hello 다운로드 된 푸시 인증서를 두 번 클릭 **aps_development.cer**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-141">Double-click hello downloaded push certificate **aps_development.cer**.</span></span>
   
      <span data-ttu-id="6c795-142">이 아래와 같이 hello, 키 집합에에서 새 hello 인증서 설치:</span><span class="sxs-lookup"><span data-stu-id="6c795-142">This installs hello new certificate in hello Keychain, as shown below:</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > <span data-ttu-id="6c795-143">인증서에 hello 이름이 서로 다를 수 있지만와 접두사가 **개발 Apple iOS 푸시 서비스:**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-143">hello name in your certificate might be different, but it will be prefixed with **Apple Development iOS Push Services:**.</span></span>
   > 
   > 
6. <span data-ttu-id="6c795-144">키 집합 접근 hello에서 만든 hello 새 푸시 인증서 마우스 오른쪽 단추로 클릭 **인증서** 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-144">In Keychain Access, right-click hello new push certificate that you created in hello **Certificates** category.</span></span> <span data-ttu-id="6c795-145">클릭 **내보내기**, hello 파일의 이름을, 선택, hello **.p12** 서식을 지정 하 고 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-145">Click **Export**, name hello file, select hello **.p12** format, and then click **Save**.</span></span>
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    <span data-ttu-id="6c795-146">Hello 파일 이름 메모 및 hello 내보낸된.p12 인증서의 위치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-146">Make a note of hello file name and location of hello exported .p12 certificate.</span></span> <span data-ttu-id="6c795-147">Apns 사용된 tooenable 인증 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-147">It will be used tooenable authentication with APNS.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6c795-148">이 자습서에서는 QuickStart.p12 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-148">This tutorial creates a QuickStart.p12 file.</span></span> <span data-ttu-id="6c795-149">Your file name and location might be different.</span><span class="sxs-lookup"><span data-stu-id="6c795-149">Your file name and location might be different.</span></span>
   > 
   > 

## <a name="create-a-provisioning-profile-for-hello-app"></a><span data-ttu-id="6c795-150">Hello 앱 용 프로비저닝 프로필 만들기</span><span class="sxs-lookup"><span data-stu-id="6c795-150">Create a provisioning profile for hello app</span></span>
1. <span data-ttu-id="6c795-151">Hello에 다시 <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS 프로 비전 포털</a>선택, **프로 비전 프로필**선택, **모든**, hello를 클릭 한 다음  **+**  단추 toocreate 새 프로필입니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-151">Back in hello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a>, select **Provisioning Profiles**, select **All**, and then click hello **+** button toocreate a new profile.</span></span> <span data-ttu-id="6c795-152">그러면 hello **iOS Provisiong 프로필 추가** 마법사</span><span class="sxs-lookup"><span data-stu-id="6c795-152">This launches hello **Add iOS Provisiong Profile** Wizard</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. <span data-ttu-id="6c795-153">선택 **iOS 응용 프로그램 개발** 아래 **개발** hello provisiong 프로필 유형 및 클릭 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-153">Select **iOS App Development** under **Development** as hello provisiong profile type, and click **Continue**.</span></span> 
3. <span data-ttu-id="6c795-154">다음으로, hello에서 방금 만든 hello 앱 ID를 선택 **앱 ID** 드롭 다운 목록 및 클릭 **계속**</span><span class="sxs-lookup"><span data-stu-id="6c795-154">Next, select hello app ID you just created from hello **App ID** drop-down list, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. <span data-ttu-id="6c795-155">Hello에 **인증서 선택** 화면 코드 서명에 사용 된 일반적인 개발 인증서를 선택 하 고 클릭 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-155">In hello **Select certificates** screen, select your usual development certificate used for code signing, and click **Continue**.</span></span> <span data-ttu-id="6c795-156">방금 만든 hello 푸시 인증서 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-156">This is not hello push certificate you just created.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. <span data-ttu-id="6c795-157">다음으로, 선택 hello **장치** 테스트 및 클릭에 대 한 toouse **계속**</span><span class="sxs-lookup"><span data-stu-id="6c795-157">Next, select hello **Devices** toouse for testing, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. <span data-ttu-id="6c795-158">마지막으로 hello 프로필에 대 한 이름을 선택 **프로필 이름**, 클릭 **생성**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-158">Finally, pick a name for hello profile in **Profile Name**, click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. <span data-ttu-id="6c795-159">새 프로비저닝 프로필 hello를 만들 때 클릭 toodownload 하 고 설치 Xcode 개발 컴퓨터에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-159">When hello new provisioning profile is created click toodownload it and install it on your Xcode development machine.</span></span> <span data-ttu-id="6c795-160">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c795-160">Then click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)
