<!--author=alkohli last changed: 01/18/2017-->


#### <a name="to-configure-and-register-the-device"></a><span data-ttu-id="af3a8-101">장치를 구성 및 등록하려면</span><span class="sxs-lookup"><span data-stu-id="af3a8-101">To configure and register the device</span></span>

1. <span data-ttu-id="af3a8-102">StorSimple 장치 직렬 콘솔에서 Windows PowerShell 인터페이스에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-102">Access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="af3a8-103">지침은 [장치 직렬 콘솔 연결에 PuTTY 사용](#use-putty-to-connect-to-the-device-serial-console) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af3a8-103">See [Use PuTTY to connect to the device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="af3a8-104">**과정을 정확하게 따르지 않으면 콘솔에 액세스할 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="af3a8-104">**Be sure to follow the procedure exactly or you will not be able to access the console.**</span></span>

2. <span data-ttu-id="af3a8-105">열린 세션에서 **Enter**를 한 번 눌러 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-105">In the session that opens up, press **Enter** one time to get a command prompt.</span></span>

3. <span data-ttu-id="af3a8-106">장치에 설정하려는 언어를 선택하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-106">You will be prompted to choose the language that you would like to set for your device.</span></span> <span data-ttu-id="af3a8-107">언어를 지정하고 **Enter**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-107">Specify the language, and then press **Enter**.</span></span>

4. <span data-ttu-id="af3a8-108">표시되는 직렬 콘솔 메뉴에서 **l모든 권한으로 로그인**할 수 있는 옵션 1을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-108">In the serial console menu that is presented, choose option 1 to **log in with full access**.</span></span>
     <span data-ttu-id="af3a8-109">5~12단계를 완료하여 장치에 필요한 최소 네트워크 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-109">Complete steps 5-12 to configure the minimum required network settings for your device.</span></span> <span data-ttu-id="af3a8-110">**이러한 구성 단계는 장치의 활성 컨트롤러에서 수행해야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="af3a8-110">**These configuration steps need to be performed on the active controller of the device.**</span></span> <span data-ttu-id="af3a8-111">직렬 콘솔 메뉴는 배너 메시지에 컨트롤러 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-111">The serial console menu indicates the controller state in the banner message.</span></span> <span data-ttu-id="af3a8-112">활성 컨트롤러에 연결되지 않은 경우 연결을 끊고 활성 컨트롤러에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-112">If you are not connected to the active controller, disconnect and then connect to the active controller.</span></span>

5. <span data-ttu-id="af3a8-113">명령 프롬프트에 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-113">At the command prompt, type your password.</span></span> <span data-ttu-id="af3a8-114">기본 장치 암호는 **Password1**입니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-114">The default device password is **Password1**.</span></span>

6. <span data-ttu-id="af3a8-115">다음 명령을 입력합니다. `Invoke-HcsSetupWizard`</span><span class="sxs-lookup"><span data-stu-id="af3a8-115">Type the following command: `Invoke-HcsSetupWizard`.</span></span>

7. <span data-ttu-id="af3a8-116">장치에 대한 네트워크 설정 구성을 도와주는 설치 마법사가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-116">A setup wizard will appear to help you configure the network settings for the device.</span></span> <span data-ttu-id="af3a8-117">다음 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-117">Supply the the following information:</span></span>
   
   * <span data-ttu-id="af3a8-118">데이터 0 네트워크 인터페이스의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="af3a8-118">IP address for the DATA 0 network interface</span></span>
   * <span data-ttu-id="af3a8-119">서브넷 마스크</span><span class="sxs-lookup"><span data-stu-id="af3a8-119">Subnet mask</span></span>
   * <span data-ttu-id="af3a8-120">게이트웨이</span><span class="sxs-lookup"><span data-stu-id="af3a8-120">Gateway</span></span>
   * <span data-ttu-id="af3a8-121">주 DNS 서버의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="af3a8-121">IP address for Primary DNS server</span></span>

   <span data-ttu-id="af3a8-122">샘플 출력은 아래 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-122">A sample output is presented below.</span></span>

    ```
        ---------------------------------------------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: 8100-SHX0991003G44MT
        Software Version: 6.3.9600.17759
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Active
        ---------------------------------------------------------------

        Your device needs to be registered with the Microsoft Azure StorSimple Manager service. Please run 'Invoke-HcsSetupWizard' to set up your device.

        Controller0>Invoke-HcsSetupWizard

        Which IP address family would you like to configure on interface Data0?
        [4] IPv4 [6] IPv6 [B] Both (Default is "4"): 4

        Data0 IPv4 address:10.111.111.00
        Data0 IPv4 subnet: 255.255.252.0
        Data0 IPv4 gateway: 10.111.111.11

        IPv4 primary DNS server [10.222.118.154]:10.222.222.111
    ```

    <br>
    <span data-ttu-id="af3a8-123">이전 샘플 출력에서 프로세스의 각 단계가 완료될 때마다 시스템에서 네트워크 설정의 유효성을 검사하고 있음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-123">In the preceding sample output, you can see that the system is validating network settings after each step in the process.</span></span>

     > [!NOTE]
     > <span data-ttu-id="af3a8-124">서브넷 마스크 및 DNS 설정을 적용하려면 몇 분간 대기할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-124">You may have to wait for a few minutes for the subnet mask and the DNS settings to be applied.</span></span> <span data-ttu-id="af3a8-125">"데이터 0에 대한 네트워크 연결을 확인합니다." 오류 메시지를 받게되면, 활성 컨트롤러의 데이터 0 네트워크 인터페이스에서 실제 네트워크 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-125">If you get a "Check the network connectivity to Data 0" error message, check the physical network connection on the DATA 0 network interface of your active controller.</span></span>

8. <span data-ttu-id="af3a8-126">(선택 사항) 웹 프록시 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-126">(Optional) configure your web proxy server.</span></span> <span data-ttu-id="af3a8-127">웹 프록시 구성은 선택 사항이지만 **웹 프록시를 사용하면 여기서만 구성할 수 있습니다**.</span><span class="sxs-lookup"><span data-stu-id="af3a8-127">Although web proxy configuration is optional, **be aware that if you use a web proxy, you can only configure it here**.</span></span> <span data-ttu-id="af3a8-128">자세한 내용은 [장치에 웹 프록시 구성](../articles/storsimple/storsimple-8000-configure-web-proxy.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-128">For more information, go to [Configure web proxy for your device](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span></span>
9. <span data-ttu-id="af3a8-129">장치에 대한 기본 NTP 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-129">Configure a Primary NTP server for your device.</span></span> <span data-ttu-id="af3a8-130">클라우드 서비스 공급자와 인증할 수 있도록 장치 시간을 동기화해야 하는 것처럼 NTP 서버가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-130">NTP servers are required, as your device must synchronize time so that it can authenticate with your cloud service providers.</span></span> <span data-ttu-id="af3a8-131">네트워크에서 NTP 트래픽이 데이터 센터에서 인터넷으로 전달되도록 허용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-131">Ensure that your network allows NTP traffic to pass from your datacenter to the Internet.</span></span> <span data-ttu-id="af3a8-132">허용되지 않는 경우 내부 NTP 서버를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-132">If this is not possible, specify an internal NTP server.</span></span>

    <span data-ttu-id="af3a8-133">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-133">A sample output is shown below.</span></span>

    ```
        Would you like to configure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. <span data-ttu-id="af3a8-134">보안상의 이유로 첫 번째 세션이 끝난 후 장치 관리자 암호가 만료되고 지금 암호를 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-134">For security reasons, the device administrator password expires after the first session, and you will need to change it now.</span></span> <span data-ttu-id="af3a8-135">메시지가 표시되면 장치 관리자 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-135">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="af3a8-136">유효한 장치 관리자 암호는 8자에서 15자 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-136">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="af3a8-137">암호는 소문자, 대문자, 숫자 및 특수 문자 중 세 유형을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-137">The password must contain three of the following: lowercase, uppercase, numeric, and special characters.</span></span>

    ```
        The device administrator password must be between 8 and 15 characters. The password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. <span data-ttu-id="af3a8-138">설치 마법사의 마지막 단계에서는 StorSimple 장치 관리자 서비스에 장치를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-138">The final step in the setup wizard registers your device with the StorSimple Device Manager service.</span></span> <span data-ttu-id="af3a8-139">이 경우 2단계에서 얻은 서비스 등록 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-139">For this, you will need the service registration key that you obtained in step 2.</span></span> <span data-ttu-id="af3a8-140">등록 키를 입력한 후 장치가 등록되려면 2~3분 정도 기다려야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-140">After you supply the registration key, you may need to wait for 2-3 minutes before the device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="af3a8-141">Ctrl + C를 눌러 언제든지 설치 마법사를 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-141">You can press Ctrl + C at any time to exit the setup wizard.</span></span> <span data-ttu-id="af3a8-142">모든 네트워크 설정(Data 0, 서브넷 마스크 및 게이트웨이 IP 주소)를 입력한 경우, 항목이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-142">If you have entered all the network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    
    <span data-ttu-id="af3a8-143">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-143">A sample output is shown below.</span></span>

    ```
        The service registration key is available in the StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. <span data-ttu-id="af3a8-144">장치를 등록한 후 서비스 데이터 암호화 키가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-144">After the device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="af3a8-145">이 키를 복사하고 안전한 위치에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-145">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="af3a8-146">**이 키는 StorSimple 장치 관리자 서비스로 추가 장치를 등록하기 위한 서비스 등록 키에 필요합니다.**</span><span class="sxs-lookup"><span data-stu-id="af3a8-146">**This key will be required with the service registration key to register additional devices with the StorSimple Device Manager service.**</span></span> <span data-ttu-id="af3a8-147">이 키에 대한 자세한 내용은 [StorSimple 보안](../articles/storsimple/storsimple-security.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af3a8-147">Refer to [StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![StorSimple 등록 장치 7](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > <span data-ttu-id="af3a8-149">직렬 콘솔 창에서 텍스트를 복사하려면 해당 텍스트를 선택하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-149">To copy the text from the serial console window, simply select the text.</span></span> <span data-ttu-id="af3a8-150">그런 다음 클립보드 또는 임의의 텍스트 편집기에 붙여넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-150">You should then be able to paste it in the clipboard or any text editor.</span></span> <span data-ttu-id="af3a8-151">Ctrl + C를 사용하여 서비스 데이터 암호화 키를 복사하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="af3a8-151">DO NOT use Ctrl + C to copy the service data encryption key.</span></span> <span data-ttu-id="af3a8-152">Ctrl + C를 사용하면 설치 마법사가 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-152">Using Ctrl + C will cause you to exit the setup wizard.</span></span> <span data-ttu-id="af3a8-153">결과적으로, 장치 관리자 암호는 변경되지 않으며 장치는 기본 암호로 되돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-153">As a result, the device administrator password will not be changed and the device will revert to the default password.</span></span>
    
13. <span data-ttu-id="af3a8-154">직렬 콘솔을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-154">Exit the serial console.</span></span>
14. <span data-ttu-id="af3a8-155">Azure Portal로 돌아가 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-155">Return to the Azure portal, and complete the following steps:</span></span>
    
    1. <span data-ttu-id="af3a8-156">StorSimple 장치 관리자 서비스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-156">Go to your StorSimple Device Manager service.</span></span>
    2. <span data-ttu-id="af3a8-157">**장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-157">Click **Devices**.</span></span>
    3. <span data-ttu-id="af3a8-158">테이블 형식 장치 목록에서 상태를 조회하여 장치가 서비스에 성공적으로 연결되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-158">In the tabular listing of devices, verify that the device has successfully connected to the service by looking up the status.</span></span> <span data-ttu-id="af3a8-159">장치 상태는 **설정할 준비 완료**여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-159">The device status should be **Ready to set up**.</span></span>
       
        ![StorSimple 장치 페이지](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        <span data-ttu-id="af3a8-161">장치 상태가 **설정 준비 완료**로 변경되기까지 몇 분 동안 기다려야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-161">You may need to wait for a couple of minutes for the device status to change to **Ready to set up**.</span></span>
       
        <span data-ttu-id="af3a8-162">장치가 이 목록에 표시되지 않으면, [StorSimple 장치에 대한 네트워킹 요구 사항](../articles/storsimple/storsimple-8000-system-requirements.md)에 설명된 대로 방화벽 네트워크가 구성되었는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-162">If the device does not show up in this list, then you need to make sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-8000-system-requirements.md).</span></span> <span data-ttu-id="af3a8-163">9354 포트가 StorSimple 장치 관리자 서비스와 장치 간 통신을 위해 서비스 버스에서 사용되므로 아웃바운드 통신을 위해 이 포트가 열려 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="af3a8-163">Verify that port 9354 is open for outbound communication as this is used by the service bus for StorSimple Device Manager service-to-device communication.</span></span>

