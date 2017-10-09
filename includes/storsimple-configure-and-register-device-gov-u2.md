<!--author=SharS last changed: 02/22/2016-->

### <a name="tooconfigure-and-register-hello-device"></a><span data-ttu-id="041dc-101">tooconfigure 및 레지스터 hello 장치</span><span class="sxs-lookup"><span data-stu-id="041dc-101">tooconfigure and register hello device</span></span>
1. <span data-ttu-id="041dc-102">StorSimple 장치 직렬 콘솔에 hello Windows PowerShell 인터페이스에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-102">Access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="041dc-103">참조 [PuTTY를 사용 하 여 장치 직렬 콘솔 tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-103">See [Use PuTTY tooconnect toohello device serial console](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="041dc-104">**있는지 toofollow hello 절차를 정확 하 게 것인지 수 tooaccess hello 콘솔 됩니다.**</span><span class="sxs-lookup"><span data-stu-id="041dc-104">**Be sure toofollow hello procedure exactly or you will not be able tooaccess hello console.**</span></span>
2. <span data-ttu-id="041dc-105">가 열리면 hello 세션에서 입력 한 시간 tooget 명령 프롬프트를 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-105">In hello session that opens up, press Enter one time tooget a command prompt.</span></span>
3. <span data-ttu-id="041dc-106">싶다는 의사를 tooset 장치에 대 한 증명된 toochoose hello 언어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-106">You will be prompted toochoose hello language that you would like tooset for your device.</span></span> <span data-ttu-id="041dc-107">Hello 언어를 지정 하 고 enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-107">Specify hello language, and then press Enter.</span></span>
   
    ![StorSimple 구성 및 등록 장치 1](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice1-gov-include.png)
4. <span data-ttu-id="041dc-109">제공 되는 hello 직렬 콘솔 메뉴에서 옵션 1 toolog에 대 한 모든 권한을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-109">In hello serial console menu that is presented, choose option 1 toolog on with full access.</span></span>
   
    ![StorSimple 등록 장치 2](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice2-gov-include.png)
5. <span data-ttu-id="041dc-111">Hello 장치에 대 한 단계 tooconfigure hello 필요한 최소 네트워크 설정을 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-111">Perform hello following steps tooconfigure hello minimum required network settings for your device.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="041dc-112">이러한 구성 단계 toobe hello hello 장치의 활성 컨트롤러에서 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-112">These configuration steps need toobe performed on hello active controller of hello device.</span></span> <span data-ttu-id="041dc-113">hello 직렬 콘솔 메뉴 hello 배너 메시지에 hello 컨트롤러 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-113">hello serial console menu indicates hello controller state in hello banner message.</span></span> <span data-ttu-id="041dc-114">Toohello 활성 컨트롤러를 연결 하지는 끊고 toohello 활성 컨트롤러를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-114">If you are not connect toohello active controller, disconnect and then connect toohello active controller.</span></span>
   > 
   > 
   
   1. <span data-ttu-id="041dc-115">Hello 명령 프롬프트에서 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-115">At hello command prompt, type your password.</span></span> <span data-ttu-id="041dc-116">hello 기본 장치 암호는 **Password1**합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-116">hello default device password is **Password1**.</span></span>
   2. <span data-ttu-id="041dc-117">Hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-117">Type hello following command:</span></span>
      
        `Invoke-HcsSetupWizard`
   3. <span data-ttu-id="041dc-118">설치 마법사는 hello 장치에 대 한 hello 네트워크 설정을 구성 하는 toohelp 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-118">A setup wizard will appear toohelp you configure hello network settings for hello device.</span></span> <span data-ttu-id="041dc-119">Hello 다음 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-119">Supply hello following information:</span></span>
      
      * <span data-ttu-id="041dc-120">데이터 0 네트워크 인터페이스의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="041dc-120">IP address for DATA 0 network interface</span></span>
      * <span data-ttu-id="041dc-121">서브넷 마스크</span><span class="sxs-lookup"><span data-stu-id="041dc-121">Subnet mask</span></span>
      * <span data-ttu-id="041dc-122">게이트웨이</span><span class="sxs-lookup"><span data-stu-id="041dc-122">Gateway</span></span>
      * <span data-ttu-id="041dc-123">주 DNS 서버의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="041dc-123">IP address for Primary DNS server</span></span>
      * <span data-ttu-id="041dc-124">주 NTP 서버의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="041dc-124">IP address for Primary NTP server</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="041dc-125">Hello 서브넷 마스크 및 DNS 설정이 toobe 적용에 대 일 분 동안 toowait이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-125">You may have toowait for a few minutes for hello subnet mask and DNS settings toobe applied.</span></span>
      > 
      > 
   4. <span data-ttu-id="041dc-126">선택적으로 웹 프록시 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-126">Optionally, configure your web proxy server.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="041dc-127">웹 프록시 구성은 선택 사항이지만 웹 프록시를 사용하면 여기서만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-127">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span> <span data-ttu-id="041dc-128">자세한 내용은 이동 너무[장치에 대 한 웹 프록시 구성](../articles/storsimple/storsimple-configure-web-proxy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-128">For more information, go too[Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md).</span></span>
      > 
      > 
6. <span data-ttu-id="041dc-129">Ctrl + C를 눌러 tooexit hello 설정 마법사입니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-129">Press Ctrl + C tooexit hello setup wizard.</span></span>
7. <span data-ttu-id="041dc-130">다음과 같이 hello 업데이트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-130">Install hello updates as follows:</span></span>
   
   1. <span data-ttu-id="041dc-131">Hello cmdlet tooset Ip 두 hello 컨트롤러에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-131">Use hello following cmdlet tooset IPs on both hello controllers:</span></span>
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. <span data-ttu-id="041dc-132">Hello 명령 프롬프트에서 실행 `Get-HcsUpdateAvailability`합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-132">At hello command prompt, run `Get-HcsUpdateAvailability`.</span></span> <span data-ttu-id="041dc-133">업데이트를 사용할 수 있는지 알림을 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-133">You should be notified that updates are available.</span></span>
   3. <span data-ttu-id="041dc-134">`Start-HcsUpdate`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-134">Run `Start-HcsUpdate`.</span></span> <span data-ttu-id="041dc-135">모든 노드에서 이 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-135">You can run this command on any node.</span></span> <span data-ttu-id="041dc-136">Hello 첫 번째 컨트롤러에서 업데이트가 적용 됩니다, hello 컨트롤러 조치 실패 하 고에 업데이트가 적용 되며 hello hello 다른 컨트롤러.</span><span class="sxs-lookup"><span data-stu-id="041dc-136">Updates will be applied on hello first controller, hello controller will fail over, and then hello updates will be applied on hello other controller.</span></span>
      
      <span data-ttu-id="041dc-137">실행 하 여 hello hello 업데이트 진행률을 모니터링할 수 있습니다 `Get-HcsUpdateStatus`합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-137">You can monitor hello progress of hello update by running `Get-HcsUpdateStatus`.</span></span>    
      
      <span data-ttu-id="041dc-138">hello 다음 샘플은 출력 hello 업데이트 진행 중에서입니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-138">hello following sample output shows hello update in progress.</span></span>
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ````
      
      <span data-ttu-id="041dc-139">다음 샘플 출력 hello 해당 hello 업데이트가 완료 된 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-139">hello following sample output indicates that hello update is finished.</span></span>
      
      ```
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ```
      
      <span data-ttu-id="041dc-140">업데이트를 포함 하 여 hello 모든 tooapply hello Windows 업데이트 too11 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-140">It may take up too11 hours tooapply all hello updates, including hello Windows Updates.</span></span>
8. <span data-ttu-id="041dc-141">(기본적으로 toohello 공용 Azure 클래식 포털을 가리킴) 이므로 cmdlet toopoint hello 장치 toohello Microsoft Azure Government 포털 다음 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-141">Run hello following cmdlet toopoint hello device toohello Microsoft Azure Government portal (because it points toohello public Azure classic portal by default).</span></span> <span data-ttu-id="041dc-142">두 컨트롤러가 모두 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-142">This will restart both controllers.</span></span> <span data-ttu-id="041dc-143">각 컨트롤러 다시 시작 되 면 볼 수 있도록 toosimultaneously tooboth 컨트롤러를 연결 하는 두 개의 PuTTY 세션을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-143">We recommend that you use two PuTTY sessions toosimultaneously connect tooboth controllers so that you can see when each controller is restarted.</span></span>
   
    `Set-CloudPlatform -AzureGovt_US`
   
   <span data-ttu-id="041dc-144">확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-144">You will see a confirmation message.</span></span> <span data-ttu-id="041dc-145">Hello 기본값을 그대로 (**Y**).</span><span class="sxs-lookup"><span data-stu-id="041dc-145">Accept hello default (**Y**).</span></span>
9. <span data-ttu-id="041dc-146">다음과 같은 cmdlet tooresume 설정이 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-146">Run hello following cmdlet tooresume setup:</span></span>
   
    `Invoke-HcsSetupWizard`
   
    ![설치 마법사 다시 시작](./media/storsimple-configure-and-register-device-gov-u2/HCS_ResumeSetup-gov-include.png)
   
   <span data-ttu-id="041dc-148">설치 프로그램을 다시 시작할 때 hello 마법사는 hello 업데이트 2 버전 됩니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-148">When you resume setup, hello wizard will be hello Update 2 version.</span></span>
10. <span data-ttu-id="041dc-149">Hello 네트워크 설정을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-149">Accept hello network settings.</span></span> <span data-ttu-id="041dc-150">각 설정에 동의하면 유효성 검사 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-150">You will see a validation message after you accept each setting.</span></span>
11. <span data-ttu-id="041dc-151">보안상의 이유로 hello 첫 번째 세션 후 hello 장치 관리자 암호가 만료 되어 toochange 해야 it 이제 합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-151">For security reasons, hello device administrator password expires after hello first session, and you will need toochange it now.</span></span> <span data-ttu-id="041dc-152">메시지가 표시되면 장치 관리자 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-152">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="041dc-153">유효한 장치 관리자 암호는 8자에서 15자 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-153">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="041dc-154">hello 암호에 포함 해야 hello 다음의 3 개: 소문자, 대문자, 숫자 및 특수 문자.</span><span class="sxs-lookup"><span data-stu-id="041dc-154">hello password must contain three of hello following: lowercase, uppercase, numeric, and special characters.</span></span>
    
    <br/>![StorSimple 등록 장치 5](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice5_gov-include.png)
12. <span data-ttu-id="041dc-156">hello hello 설치 마법사의 마지막 단계는 hello StorSimple Manager 서비스와 장치를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-156">hello final step in hello setup wizard registers your device with hello StorSimple Manager service.</span></span> <span data-ttu-id="041dc-157">이렇게 하면 됩니다 필요 hello에서 얻은 서비스 등록 키 [2 단계: Get hello 서비스 등록 키](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key)합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-157">For this, you will need hello service registration key that you obtained in [Step 2: Get hello service registration key](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key).</span></span> <span data-ttu-id="041dc-158">Hello 등록 키를 제공한 후 toowait hello 장치를 등록 하기 전에 2-3 분 동안 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-158">After you supply hello registration key, you may need toowait for 2-3 minutes before hello device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="041dc-159">모든 시간 tooexit hello 설치 마법사에서 Ctrl + C를 눌러 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-159">You can press Ctrl + C at any time tooexit hello setup wizard.</span></span> <span data-ttu-id="041dc-160">모든 hello 네트워크 설정 (Data 0, 서브넷 마스크 및 게이트웨이 IP 주소)를 입력 하면 입력 한 내용을 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-160">If you have entered all hello network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    > 
    > 
    
    ![StorSimple 등록 진행률](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegistrationProgress-gov-include.png)
13. <span data-ttu-id="041dc-162">Hello 장치를 등록 한 후에 서비스 데이터 암호화 키가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-162">After hello device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="041dc-163">이 키를 복사하고 안전한 위치에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-163">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="041dc-164">**이 키는 hello 서비스 등록 키 tooregister 추가 장치를 StorSimple Manager 서비스 hello 함께 해야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="041dc-164">**This key will be required with hello service registration key tooregister additional devices with hello StorSimple Manager service.**</span></span> <span data-ttu-id="041dc-165">너무 참조[StorSimple 보안](../articles/storsimple/storsimple-security.md) 이 키에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-165">Refer too[StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![StorSimple 등록 장치 7](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > <span data-ttu-id="041dc-167">hello 직렬 콘솔 창에서 toocopy hello 텍스트 hello 텍스트를 선택 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-167">toocopy hello text from hello serial console window, simply select hello text.</span></span> <span data-ttu-id="041dc-168">Toopaste 수 있어야 다음 hello 클립보드 또는 텍스트 편집기에서.</span><span class="sxs-lookup"><span data-stu-id="041dc-168">You should then be able toopaste it in hello clipboard or any text editor.</span></span>
    > 
    > <span data-ttu-id="041dc-169">Ctrl 키를 사용 하지 않는 + C toocopy hello 서비스 데이터 암호화 키입니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-169">DO NOT use Ctrl + C toocopy hello service data encryption key.</span></span> <span data-ttu-id="041dc-170">Ctrl + C를 사용 하면 tooexit hello 설치 마법사를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-170">Using Ctrl + C will cause you tooexit hello setup wizard.</span></span> <span data-ttu-id="041dc-171">결과적으로, hello 장치 관리자 암호가 변경 되지 않습니다 및 hello 장치 toohello 기본 암호 되돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-171">As a result, hello device administrator password will not be changed and hello device will revert toohello default password.</span></span>
    > 
    > 
14. <span data-ttu-id="041dc-172">Hello 직렬 콘솔을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-172">Exit hello serial console.</span></span>
15. <span data-ttu-id="041dc-173">Toohello Azure Government 포털을 반환 하 고 hello 다음 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-173">Return toohello Azure Government Portal, and complete hello following steps:</span></span>
    
    1. <span data-ttu-id="041dc-174">두 번 클릭 하 여 StorSimple Manager 서비스 tooaccess hello **빠른 시작** 페이지.</span><span class="sxs-lookup"><span data-stu-id="041dc-174">Double-click your StorSimple Manager service tooaccess hello **Quick Start** page.</span></span>
    2. <span data-ttu-id="041dc-175">**연결된 장치 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-175">Click **View connected devices**.</span></span>
    3. <span data-ttu-id="041dc-176">Hello에 **장치** 페이지에서 해당 hello 장치 성공적으로 hello 상태를 조회 하 여 toohello 서비스 연결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-176">On hello **Devices** page, verify that hello device has successfully connected toohello service by looking up hello status.</span></span> <span data-ttu-id="041dc-177">hello 장치 상태가 **온라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-177">hello device status should be **Online**.</span></span>
       
        ![StorSimple 장치 페이지](./media/storsimple-configure-and-register-device-gov-u2/HCS_DeviceOnline-gov-include.png)
       
        <span data-ttu-id="041dc-179">Hello 장치 상태 이면 **오프 라인**, 몇 분까지 hello 장치 toocome 온라인 정도 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-179">If hello device status is **Offline**, wait for a couple of minutes for hello device toocome online.</span></span>
       
        <span data-ttu-id="041dc-180">몇 분 후 hello 장치는 계속 오프 라인 상태 경우 toomake에 설명 된 대로 방화벽 네트워크가 구성 되어 있는지 필요 [네트워킹 StorSimple 장치에 대 한 요구 사항이](../articles/storsimple/storsimple-system-requirements.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-180">If hello device is still offline after a few minutes, then you need toomake sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-system-requirements.md).</span></span>
       
        <span data-ttu-id="041dc-181">Hello 서비스 버스 StorSimple Manager 서비스-장치 통신에 사용이 포트 9354를 아웃 바운드 통신을 위해 열려 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="041dc-181">Verify that port 9354 is open for outbound communication as this is used by hello service bus for StorSimple Manager Service-to-device communication.</span></span>

