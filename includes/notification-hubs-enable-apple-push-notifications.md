

## <a name="generate-the-certificate-signing-request-file"></a><span data-ttu-id="e7872-101">인증서 서명 요청 파일 생성</span><span class="sxs-lookup"><span data-stu-id="e7872-101">Generate the Certificate Signing Request file</span></span>
<span data-ttu-id="e7872-102">APNS(Apple Push Notification Service)는 인증서를 사용하여 푸시 알림을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-102">The Apple Push Notification Service (APNS) uses certificates to authenticate your push notifications.</span></span> <span data-ttu-id="e7872-103">알림을 보내고 받는 데 필요한 푸시 인증서를 만들려면 다음 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="e7872-103">Follow these instructions to create the necessary push certificate to send and receive notifications.</span></span> <span data-ttu-id="e7872-104">이러한 개념에 대한 자세한 내용은 [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) 공식 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7872-104">For more information on these concepts see the official [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentation.</span></span>

<span data-ttu-id="e7872-105">서명된 푸시 인증서를 생성하기 위해 Apple에서 사용하는 CSR(인증서 서명 요청) 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-105">Generate the Certificate Signing Request (CSR) file, which is used by Apple to generate a signed push certificate.</span></span>

1. <span data-ttu-id="e7872-106">Mac에서 Keychain Access 도구를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-106">On your Mac, run the Keychain Access tool.</span></span> <span data-ttu-id="e7872-107">**Utilities** 폴더 또는 **Other** 폴더에서 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-107">It can be opened from the **Utilities** folder or the **Other** folder on the launch pad.</span></span>
2. <span data-ttu-id="e7872-108">**Keychain Access**를 클릭하고 **Certificate Assistant**를 확장한 다음 **Request a Certificate from a Certificate Authority...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-108">Click **Keychain Access**, expand **Certificate Assistant**, then click **Request a Certificate from a Certificate Authority...**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. <span data-ttu-id="e7872-109">**User Email Address**와 **Common Name**을 선택하고, **Saved to disk**가 선택되어 있는지 확인한 후 **Continue**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-109">Select your **User Email Address** and **Common Name** , make sure that **Saved to disk** is selected, and then click **Continue**.</span></span> <span data-ttu-id="e7872-110">**CA Email Address** 필드는 필요하지 않으므로 비워둡니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-110">Leave the **CA Email Address** field blank as it is not required.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. <span data-ttu-id="e7872-111">**Save As**에 CSR(인증서 서명 요청) 파일의 이름을 입력하고, **Where**에서 위치를 선택한 후 **Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-111">Type a name for the Certificate Signing Request (CSR) file in **Save As**, select the location in **Where**, then click **Save**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      <span data-ttu-id="e7872-112">CSR 파일이 선택한 위치에 저장됩니다. 기본 위치는 바탕 화면입니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-112">This saves the CSR file in the selected location; the default location is in the Desktop.</span></span> <span data-ttu-id="e7872-113">이 파일을 저장한 위치를 기억해두세요.</span><span class="sxs-lookup"><span data-stu-id="e7872-113">Remember the location chosen for this file.</span></span>

<span data-ttu-id="e7872-114">이제 Apple에 앱을 등록하고, 푸시 알림을 사용하도록 설정하고, 내보낸 CSR을 업로드하여 푸시 인증서를 만들 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-114">Next, you will register your app with Apple, enable push notifications, and upload this exported CSR to create a push certificate.</span></span>

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="e7872-115">푸시 알림에 대해 앱 등록</span><span class="sxs-lookup"><span data-stu-id="e7872-115">Register your app for push notifications</span></span>
<span data-ttu-id="e7872-116">iOS 앱으로 푸시 알림을 보내려면 Apple에 응용 프로그램을 등록하고 푸시 알림도 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-116">To be able to send push notifications to an iOS app, you must register your application with Apple and also register for push notifications.</span></span>  

1. <span data-ttu-id="e7872-117">아직 앱을 등록하지 않은 경우 Apple Developer Center의 <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a>로 이동하여 Apple ID로 로그온하고 **Identifiers**와 **App IDs**를 클릭한 다음에 **+** 기호를 클릭하여 새 앱을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-117">If you have not already registered your app, navigate to the <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a> at the Apple Developer Center, log on with your Apple ID, click **Identifiers**, then click **App IDs**, and finally click on the **+** sign to register a new app.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. <span data-ttu-id="e7872-118">새 앱에 다음과 같은 세 개의 필드를 업데이트한 다음 **Continue**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-118">Update the following three fields for your new app and then click **Continue**:</span></span>
   
   * <span data-ttu-id="e7872-119">**Name**: **App ID Description** 섹션의 **Name** 필드에서 앱에 대한 설명이 포함된 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-119">**Name**: Type a descriptive name for your app in the **Name** field in the **App ID Description** section.</span></span>
   * <span data-ttu-id="e7872-120">**번들 식별자**: **명시적 앱 ID** 섹션에 [앱 배포 가이드](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8)에 설명된 대로 `<Organization Identifier>.<Product Name>` 형식으로 **번들 식별자**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-120">**Bundle Identifier**: Under the **Explicit App ID** section, enter a **Bundle Identifier** in the form `<Organization Identifier>.<Product Name>` as mentioned in the [App Distribution Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span></span> <span data-ttu-id="e7872-121">사용하는 *Organization Identifier* 및 *Product Name*은 XCode 프로젝트를 만들 때 사용할 조직 식별자 및 제품 이름과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-121">The *Organization Identifier* and *Product Name* you use must match the organization identifier and product name you will use when you create your XCode project.</span></span> <span data-ttu-id="e7872-122">아래 스크린샷에서는 조직 식별자로 *NotificationHubs*가 사용되고 제품 이름으로 *GetStarted*가 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-122">In the screeshot below *NotificationHubs* is used as a organization idenitifier and *GetStarted* is used as the product name.</span></span> <span data-ttu-id="e7872-123">이 값이 XCode 프로젝트에서 사용할 값과 일치하면 XCode에서 올바른 게시 프로필을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-123">Making sure this matches the values you will use in your XCode project will allow you to use the correct publishing profile with XCode.</span></span> 
   * <span data-ttu-id="e7872-124">**푸시 알림**: **App Services** 섹션에서 **푸시 알림** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-124">**Push Notifications**: Check the **Push Notifications** option in the **App Services** section, .</span></span>
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      <span data-ttu-id="e7872-125">그러면 앱 ID가 생성되고 정보를 확인하라는 요청이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-125">This generates your App ID and requests you to confirm the information.</span></span> <span data-ttu-id="e7872-126">**등록** 을 클릭하여 새 앱 ID를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-126">Click **Register** to confirm the new App ID.</span></span>
     
      <span data-ttu-id="e7872-127">**등록**을 클릭하면 아래와 같은 **등록 완료** 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-127">Once you click **Register**, you will see the **Registration complete** screen, as shown below.</span></span> <span data-ttu-id="e7872-128">**Done**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-128">Click **Done**.</span></span>
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. <span data-ttu-id="e7872-129">개발자 센터의 앱 ID에서 방금 만든 앱 ID를 찾아 해당 행을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-129">In the Developer Center, under App IDs, locate the app ID that you just created, and click on its row.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      <span data-ttu-id="e7872-130">앱 ID를 클릭하면 앱 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-130">Clicking on the app ID will display the app details.</span></span> <span data-ttu-id="e7872-131">아래쪽에 있는 **Edit** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-131">Click the **Edit** button at the bottom.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. <span data-ttu-id="e7872-132">화면 아래로 스크롤하여 **Development Push SSL Certificate** 섹션에서 **Create Certificate...** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-132">Scroll to the bottom of the screen, and click the **Create Certificate...** button under the section **Development Push SSL Certificate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      <span data-ttu-id="e7872-133">"Add iOS Certificate" assistant가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-133">This displays the "Add iOS Certificate" assistant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e7872-134">이 자습서에서는 개발 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-134">This tutorial uses a development certificate.</span></span> <span data-ttu-id="e7872-135">프로덕션 인증서를 등록할 때에도 동일한 프로세스가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-135">The same process is used when registering a production certificate.</span></span> <span data-ttu-id="e7872-136">알림을 보낼 때 동일한 인증서 유형을 사용하는지만 확인하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-136">Just make sure that you use the same certificate type when sending notifications.</span></span>
   > 
   > 
3. <span data-ttu-id="e7872-137">**Choose File**을 클릭하고, 첫 번째 작업에서 만든 CSR 파일이 저장된 위치로 이동하여 파일을 선택하고, **Generate**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-137">Click **Choose File**, browse to the location where you saved the CSR file that you created in the first task, then click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. <span data-ttu-id="e7872-138">포털에서 인증서가 생성되면 **Download** 단추를 클릭하고 **Done**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-138">After the certificate is created by the portal, click the **Download** button, and click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      <span data-ttu-id="e7872-139">인증서가 다운로드되어 컴퓨터의 다운로드 폴더에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-139">This downloads the certificate and saves it to your computer in your Downloads folder.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > <span data-ttu-id="e7872-140">기본적으로 다운로드된 개발 인증서 파일은 이름이 **aps_development.cer**로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-140">By default, the downloaded file a development certificate is named **aps_development.cer**.</span></span>
   > 
   > 
5. <span data-ttu-id="e7872-141">다운로드한 푸시 인증서 **aps_development.cer**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-141">Double-click the downloaded push certificate **aps_development.cer**.</span></span>
   
      <span data-ttu-id="e7872-142">아래와 같이 새 인증서가 Keychain에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-142">This installs the new certificate in the Keychain, as shown below:</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > <span data-ttu-id="e7872-143">인증서의 이름은 다를 수 있지만 **Apple Development iOS Push Services:**가 앞에 옵니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-143">The name in your certificate might be different, but it will be prefixed with **Apple Development iOS Push Services:**.</span></span>
   > 
   > 
6. <span data-ttu-id="e7872-144">Keychain Access에서는 **인증서** 범주에서 만든 새 푸시 인증서를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-144">In Keychain Access, right-click the new push certificate that you created in the **Certificates** category.</span></span> <span data-ttu-id="e7872-145">**내보내기**를 클릭하고 파일의 이름을 지정한 후 **.p12** 형식을 선택하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-145">Click **Export**, name the file, select the **.p12** format, and then click **Save**.</span></span>
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    <span data-ttu-id="e7872-146">내보낸 .p12 인증서의 파일 이름과 위치를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-146">Make a note of the file name and location of the exported .p12 certificate.</span></span> <span data-ttu-id="e7872-147">APNS을 이용한 인증을 사용하도록 설정하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-147">It will be used to enable authentication with APNS.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e7872-148">이 자습서에서는 QuickStart.p12 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-148">This tutorial creates a QuickStart.p12 file.</span></span> <span data-ttu-id="e7872-149">Your file name and location might be different.</span><span class="sxs-lookup"><span data-stu-id="e7872-149">Your file name and location might be different.</span></span>
   > 
   > 

## <a name="create-a-provisioning-profile-for-the-app"></a><span data-ttu-id="e7872-150">앱용 프로비저닝 프로필 만들기</span><span class="sxs-lookup"><span data-stu-id="e7872-150">Create a provisioning profile for the app</span></span>
1. <span data-ttu-id="e7872-151"><a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a>로 돌아가서 **Provisioning Profiles**와 **All**을 차례로 선택하고 **+** 단추를 클릭하여 새 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-151">Back in the <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a>, select **Provisioning Profiles**, select **All**, and then click the **+** button to create a new profile.</span></span> <span data-ttu-id="e7872-152">**Add iOS Provisioning Profile** 마법사가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-152">This launches the **Add iOS Provisiong Profile** Wizard</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. <span data-ttu-id="e7872-153">**Development**에서 프로비저닝 프로필 유형으로 **iOS App Development**를 선택하고 **Continue**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-153">Select **iOS App Development** under **Development** as the provisiong profile type, and click **Continue**.</span></span> 
3. <span data-ttu-id="e7872-154">**App ID** 드롭다운 목록에서 방금 만든 앱 ID를 선택하고 **Continue**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-154">Next, select the app ID you just created from the **App ID** drop-down list, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. <span data-ttu-id="e7872-155">**Select certificates** 화면에서 코드 서명에 사용되는 일반적인 개발 인증서를 선택하고 **Continue**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-155">In the **Select certificates** screen, select your usual development certificate used for code signing, and click **Continue**.</span></span> <span data-ttu-id="e7872-156">이는 방금 만든 푸시 인증서가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-156">This is not the push certificate you just created.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. <span data-ttu-id="e7872-157">테스트에 사용할 **Devices**를 선택하고 **Continue**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-157">Next, select the **Devices** to use for testing, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. <span data-ttu-id="e7872-158">마지막으로, **Profile Name**에서 프로필의 이름을 선택하고 **Generate**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-158">Finally, pick a name for the profile in **Profile Name**, click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. <span data-ttu-id="e7872-159">새 프로비전 프로필이 만들어질 때 다운로드를 클릭하고 Xcode 개발 컴퓨터에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-159">When the new provisioning profile is created click to download it and install it on your Xcode development machine.</span></span> <span data-ttu-id="e7872-160">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7872-160">Then click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)
