<!--author=SharS last changed: 02/22/2016-->

### <a name="to-configure-and-register-the-device"></a><span data-ttu-id="71a6f-101">장치를 구성 및 등록하려면</span><span class="sxs-lookup"><span data-stu-id="71a6f-101">To configure and register the device</span></span>
1. <span data-ttu-id="71a6f-102">StorSimple 장치 직렬 콘솔에서 Windows PowerShell 인터페이스에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-102">Access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="71a6f-103">지침은 [장치 직렬 콘솔 연결에 PuTTY 사용](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="71a6f-103">See [Use PuTTY to connect to the device serial console](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="71a6f-104">**과정을 정확하게 따르지 않으면 콘솔에 액세스할 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="71a6f-104">**Be sure to follow the procedure exactly or you will not be able to access the console.**</span></span>
2. <span data-ttu-id="71a6f-105">열린 세션에서 Enter를 한 번 눌러 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-105">In the session that opens up, press Enter one time to get a command prompt.</span></span>
3. <span data-ttu-id="71a6f-106">장치에 설정하려는 언어를 선택하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-106">You will be prompted to choose the language that you would like to set for your device.</span></span> <span data-ttu-id="71a6f-107">언어를 지정하고 Enter를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-107">Specify the language, and then press Enter.</span></span>
   
    ![StorSimple 구성 및 등록 장치 1](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice1-gov-include.png)
4. <span data-ttu-id="71a6f-109">표시되는 직렬 콘솔 메뉴에서 모든 권한으로 로그온할 수 있는 옵션 1을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-109">In the serial console menu that is presented, choose option 1 to log on with full access.</span></span>
   
    ![StorSimple 등록 장치 2](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice2-gov-include.png)
5. <span data-ttu-id="71a6f-111">다음 단계를 수행하여 장치에 필요한 최소 네트워크 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-111">Perform the following steps to configure the minimum required network settings for your device.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="71a6f-112">이러한 구성 단계는 장치의 활성 컨트롤러에서 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-112">These configuration steps need to be performed on the active controller of the device.</span></span> <span data-ttu-id="71a6f-113">직렬 콘솔 메뉴는 배너 메시지에 컨트롤러 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-113">The serial console menu indicates the controller state in the banner message.</span></span> <span data-ttu-id="71a6f-114">활성 컨트롤러에 연결되지 않은 경우 연결을 끊은 다음 활성 컨트롤러에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-114">If you are not connect to the active controller, disconnect and then connect to the active controller.</span></span>
   > 
   > 
   
   1. <span data-ttu-id="71a6f-115">명령 프롬프트에 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-115">At the command prompt, type your password.</span></span> <span data-ttu-id="71a6f-116">기본 장치 암호는 **Password1**입니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-116">The default device password is **Password1**.</span></span>
   2. <span data-ttu-id="71a6f-117">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-117">Type the following command:</span></span>
      
        `Invoke-HcsSetupWizard`
   3. <span data-ttu-id="71a6f-118">장치에 대한 네트워크 설정 구성을 도와주는 설치 마법사가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-118">A setup wizard will appear to help you configure the network settings for the device.</span></span> <span data-ttu-id="71a6f-119">다음 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-119">Supply the following information:</span></span>
      
      * <span data-ttu-id="71a6f-120">데이터 0 네트워크 인터페이스의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="71a6f-120">IP address for DATA 0 network interface</span></span>
      * <span data-ttu-id="71a6f-121">서브넷 마스크</span><span class="sxs-lookup"><span data-stu-id="71a6f-121">Subnet mask</span></span>
      * <span data-ttu-id="71a6f-122">게이트웨이</span><span class="sxs-lookup"><span data-stu-id="71a6f-122">Gateway</span></span>
      * <span data-ttu-id="71a6f-123">주 DNS 서버의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="71a6f-123">IP address for Primary DNS server</span></span>
      * <span data-ttu-id="71a6f-124">주 NTP 서버의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="71a6f-124">IP address for Primary NTP server</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="71a6f-125">서브넷 마스크 및 DNS 설정을 적용하려면 몇 분간 대기해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-125">You may have to wait for a few minutes for the subnet mask and DNS settings to be applied.</span></span>
      > 
      > 
   4. <span data-ttu-id="71a6f-126">선택적으로 웹 프록시 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-126">Optionally, configure your web proxy server.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="71a6f-127">웹 프록시 구성은 선택 사항이지만 웹 프록시를 사용하면 여기서만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-127">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span> <span data-ttu-id="71a6f-128">자세한 내용은 [장치에 웹 프록시 구성](../articles/storsimple/storsimple-configure-web-proxy.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-128">For more information, go to [Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md).</span></span>
      > 
      > 
6. <span data-ttu-id="71a6f-129">설치 마법사를 끝내려면 Ctrl + C를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-129">Press Ctrl + C to exit the setup wizard.</span></span>
7. <span data-ttu-id="71a6f-130">다음과 같이 업데이트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-130">Install the updates as follows:</span></span>
   
   1. <span data-ttu-id="71a6f-131">두 컨트롤러에 IP를 설정하려면 다음 cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-131">Use the following cmdlet to set IPs on both the controllers:</span></span>
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. <span data-ttu-id="71a6f-132">명령 프롬프트에서 `Get-HcsUpdateAvailability`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-132">At the command prompt, run `Get-HcsUpdateAvailability`.</span></span> <span data-ttu-id="71a6f-133">업데이트를 사용할 수 있는지 알림을 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-133">You should be notified that updates are available.</span></span>
   3. <span data-ttu-id="71a6f-134">`Start-HcsUpdate`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-134">Run `Start-HcsUpdate`.</span></span> <span data-ttu-id="71a6f-135">모든 노드에서 이 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-135">You can run this command on any node.</span></span> <span data-ttu-id="71a6f-136">첫번째 컨트롤러에 업데이트가 적용되며, 컨트롤러는 장애 조치 이후 업데이트가 다른 컨트롤러에서 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-136">Updates will be applied on the first controller, the controller will fail over, and then the updates will be applied on the other controller.</span></span>
      
      <span data-ttu-id="71a6f-137">`Get-HcsUpdateStatus`을 실행하여 업데이트의 진행률을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-137">You can monitor the progress of the update by running `Get-HcsUpdateStatus`.</span></span>    
      
      <span data-ttu-id="71a6f-138">다음 샘플 출력에서는 진행 중인 업데이트를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-138">The following sample output shows the update in progress.</span></span>
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ````
      
      <span data-ttu-id="71a6f-139">다음 샘플 출력은 업데이트가 완료되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-139">The following sample output indicates that the update is finished.</span></span>
      
      ```
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ```
      
      <span data-ttu-id="71a6f-140">Windows 업데이트를 포함하여 모든 업데이트를 적용하려면 최대 11시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-140">It may take up to 11 hours to apply all the updates, including the Windows Updates.</span></span>
8. <span data-ttu-id="71a6f-141">장치가 Microsoft Azure Government 포털을 가리키도록 다음 cmdlet을 실행합니다(기본적으로 공용 Azure 클래식 포털을 가리키기 때문임).</span><span class="sxs-lookup"><span data-stu-id="71a6f-141">Run the following cmdlet to point the device to the Microsoft Azure Government portal (because it points to the public Azure classic portal by default).</span></span> <span data-ttu-id="71a6f-142">두 컨트롤러가 모두 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-142">This will restart both controllers.</span></span> <span data-ttu-id="71a6f-143">두 PuTTY 세션을 사용하여, 각 컨트롤러가 다시 시작되면 볼 수 있도록 두 컨트롤러에 동시에 연결하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-143">We recommend that you use two PuTTY sessions to simultaneously connect to both controllers so that you can see when each controller is restarted.</span></span>
   
    `Set-CloudPlatform -AzureGovt_US`
   
   <span data-ttu-id="71a6f-144">확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-144">You will see a confirmation message.</span></span> <span data-ttu-id="71a6f-145">기본값(**Y**)을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-145">Accept the default (**Y**).</span></span>
9. <span data-ttu-id="71a6f-146">설치를 다시 시작하려면 다음 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-146">Run the following cmdlet to resume setup:</span></span>
   
    `Invoke-HcsSetupWizard`
   
    ![설치 마법사 다시 시작](./media/storsimple-configure-and-register-device-gov-u2/HCS_ResumeSetup-gov-include.png)
   
   <span data-ttu-id="71a6f-148">설치를 다시 시작하는 경우 마법사는 업데이트 2 버전이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-148">When you resume setup, the wizard will be the Update 2 version.</span></span>
10. <span data-ttu-id="71a6f-149">네트워크 설정을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-149">Accept the network settings.</span></span> <span data-ttu-id="71a6f-150">각 설정에 동의하면 유효성 검사 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-150">You will see a validation message after you accept each setting.</span></span>
11. <span data-ttu-id="71a6f-151">보안상의 이유로 첫 번째 세션이 끝난 후 장치 관리자 암호가 만료되고 지금 암호를 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-151">For security reasons, the device administrator password expires after the first session, and you will need to change it now.</span></span> <span data-ttu-id="71a6f-152">메시지가 표시되면 장치 관리자 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-152">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="71a6f-153">유효한 장치 관리자 암호는 8자에서 15자 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-153">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="71a6f-154">암호는 소문자, 대문자, 숫자 및 특수 문자 중 세 유형을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-154">The password must contain three of the following: lowercase, uppercase, numeric, and special characters.</span></span>
    
    <br/>![StorSimple 등록 장치 5](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice5_gov-include.png)
12. <span data-ttu-id="71a6f-156">설치 마법사의 마지막 단계에서는 StorSimple 관리자 서비스에 장치를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-156">The final step in the setup wizard registers your device with the StorSimple Manager service.</span></span> <span data-ttu-id="71a6f-157">이 경우 [2단계: 서비스 등록 키 가져오기](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key)에서 얻은 서비스 등록 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-157">For this, you will need the service registration key that you obtained in [Step 2: Get the service registration key](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key).</span></span> <span data-ttu-id="71a6f-158">등록 키를 입력한 후 장치가 등록되려면 2~3분 정도 기다려야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-158">After you supply the registration key, you may need to wait for 2-3 minutes before the device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="71a6f-159">Ctrl + C를 눌러 언제든지 설치 마법사를 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-159">You can press Ctrl + C at any time to exit the setup wizard.</span></span> <span data-ttu-id="71a6f-160">모든 네트워크 설정(Data 0, 서브넷 마스크 및 게이트웨이 IP 주소)를 입력한 경우, 항목이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-160">If you have entered all the network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    > 
    > 
    
    ![StorSimple 등록 진행률](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegistrationProgress-gov-include.png)
13. <span data-ttu-id="71a6f-162">장치를 등록한 후 서비스 데이터 암호화 키가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-162">After the device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="71a6f-163">이 키를 복사하고 안전한 위치에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-163">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="71a6f-164">**이 키는 StorSimple 관리자 서비스로 추가 장치를 등록하기 위한 서비스 등록 키에 필요합니다.**</span><span class="sxs-lookup"><span data-stu-id="71a6f-164">**This key will be required with the service registration key to register additional devices with the StorSimple Manager service.**</span></span> <span data-ttu-id="71a6f-165">이 키에 대한 자세한 내용은 [StorSimple 보안](../articles/storsimple/storsimple-security.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="71a6f-165">Refer to [StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![StorSimple 등록 장치 7](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > <span data-ttu-id="71a6f-167">직렬 콘솔 창에서 텍스트를 복사하려면 해당 텍스트를 선택하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-167">To copy the text from the serial console window, simply select the text.</span></span> <span data-ttu-id="71a6f-168">그런 다음 클립보드 또는 임의의 텍스트 편집기에 붙여넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-168">You should then be able to paste it in the clipboard or any text editor.</span></span>
    > 
    > <span data-ttu-id="71a6f-169">Ctrl + C를 사용하여 서비스 데이터 암호화 키를 복사하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="71a6f-169">DO NOT use Ctrl + C to copy the service data encryption key.</span></span> <span data-ttu-id="71a6f-170">Ctrl + C를 사용하면 설치 마법사가 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-170">Using Ctrl + C will cause you to exit the setup wizard.</span></span> <span data-ttu-id="71a6f-171">결과적으로, 장치 관리자 암호는 변경되지 않으며 장치는 기본 암호로 되돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-171">As a result, the device administrator password will not be changed and the device will revert to the default password.</span></span>
    > 
    > 
14. <span data-ttu-id="71a6f-172">직렬 콘솔을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-172">Exit the serial console.</span></span>
15. <span data-ttu-id="71a6f-173">Azure Government 포털로 돌아가서 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-173">Return to the Azure Government Portal, and complete the following steps:</span></span>
    
    1. <span data-ttu-id="71a6f-174">StorSimple 관리자 서비스를 두 번 클릭하여 **퀵 스타트** 페이지에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-174">Double-click your StorSimple Manager service to access the **Quick Start** page.</span></span>
    2. <span data-ttu-id="71a6f-175">**연결된 장치 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-175">Click **View connected devices**.</span></span>
    3. <span data-ttu-id="71a6f-176">**장치** 페이지에서 상태를 조회하여 장치가 서비스에 성공적으로 연결되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-176">On the **Devices** page, verify that the device has successfully connected to the service by looking up the status.</span></span> <span data-ttu-id="71a6f-177">장치 상태는 **온라인**이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-177">The device status should be **Online**.</span></span>
       
        ![StorSimple 장치 페이지](./media/storsimple-configure-and-register-device-gov-u2/HCS_DeviceOnline-gov-include.png)
       
        <span data-ttu-id="71a6f-179">장치 상태가 **오프라인**이면 장치가 온라인 상태가 될 때까지 몇 분 정도 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-179">If the device status is **Offline**, wait for a couple of minutes for the device to come online.</span></span>
       
        <span data-ttu-id="71a6f-180">몇분 후 장치가 여전히 오프라인 상태인 경우, [StorSimple 장치에 대한 네트워킹 요구 사항](../articles/storsimple/storsimple-system-requirements.md)에 설명된 대로 방화벽 네트워크가 구성되었는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-180">If the device is still offline after a few minutes, then you need to make sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-system-requirements.md).</span></span>
       
        <span data-ttu-id="71a6f-181">9354 포트가 StorSimple Manager 서비스와 장치 간 통신용 서비스 버스에 의해 사용될 때 아웃바운드 통신을 위해 열리는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="71a6f-181">Verify that port 9354 is open for outbound communication as this is used by the service bus for StorSimple Manager Service-to-device communication.</span></span>

