<!--author=alkohli last changed: 05/19/16-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="eada1-101">핫픽스를 다운로드하려면</span><span class="sxs-lookup"><span data-stu-id="eada1-101">To download hotfixes</span></span>
<span data-ttu-id="eada1-102">Microsoft 업데이트 카탈로그에서 소프트웨어 업데이트를 다운로드하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="eada1-103">Internet Explorer를 시작하고 [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="eada1-104">이 컴퓨터에서 Microsoft 업데이트 카탈로그를 처음 사용하는 경우 Microsoft 업데이트 카탈로그 추가 기능을 설치하라는 메시지가 나타나면 **설치** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="eada1-105">![카탈로그 설치](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="eada1-105">![Install catalog](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="eada1-106">Microsoft 업데이트 카탈로그의 검색 상자에 다운로드하려는 핫픽스의 KB(기술 자료) 번호(예: **3179904**)를 입력하고 **Search**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **3179904**, and then click **Search**.</span></span>
   
    <span data-ttu-id="eada1-107">핫픽스 목록이 나타납니다(예: **StorSimple 8000 시리즈용 누적 소프트웨어 번들 업데이트 2.2**).</span><span class="sxs-lookup"><span data-stu-id="eada1-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 2.2 for StorSimple 8000 Series**.</span></span>
   
    ![카탈로그 검색](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="eada1-109">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-109">Click **Add**.</span></span> <span data-ttu-id="eada1-110">업데이트는 장바구니에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-110">The update is added to the basket.</span></span>
5. <span data-ttu-id="eada1-111">위의 표에 나열된 추가적인 핫픽스(**3103616**, **3146621**)를 검색하고 각각 바구니에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-111">Search for any additional hotfixes listed in the table above (**3103616**, **3146621**), and add each to the basket.</span></span>
6. <span data-ttu-id="eada1-112">**바구니 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="eada1-113">**다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-113">Click **Download**.</span></span> <span data-ttu-id="eada1-114">다운로드를 표시할 로컬 위치를 지정하거나 **검색합니다** .</span><span class="sxs-lookup"><span data-stu-id="eada1-114">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="eada1-115">업데이트를 지정된 위치에 다운로드하고 업데이트와 같은 이름의 하위 폴더에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-115">The updates are downloaded to the specified location and placed in a sub-folder with the same name as the update.</span></span> <span data-ttu-id="eada1-116">장치에서 연결할 수 있는 네트워크 공유에 폴더도 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-116">The folder can also be copied to a network share that is reachable from the device.</span></span>

> [!NOTE]
> <span data-ttu-id="eada1-117">피어 컨트롤러의 잠재적 오류 메시지를 검색하려면 컨트롤러 둘 다에서 핫픽스에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
> 
> 

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="eada1-118">일반 모드 핫픽스를 설치 및 확인하려면</span><span class="sxs-lookup"><span data-stu-id="eada1-118">To install and verify regular mode hotfixes</span></span>
<span data-ttu-id="eada1-119">일반 모드 핫픽스를 설치 및 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-119">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="eada1-120">이미 Azure 포털을 사용하여 설치한 경우 [유지 관리 모드 핫픽스 설치 및 확인](#to-install-and-verify-maintenance-mode-hotfixes)으로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-120">If you already installed them using the Azure Portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="eada1-121">핫픽스를 설치하려면 StorSimple 장치 직렬 콘솔에서 Windows PowerShell 인터페이스에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-121">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="eada1-122">[PuTTy를 사용하여 직렬 콘솔에 연결](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)에서 자세한 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="eada1-122">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="eada1-123">명령 프롬프트에서 **Enter**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-123">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="eada1-124">**옵션 1** 을 선택하여 모든 권한으로 장치에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-124">Select **Option 1** to log on to the device with full access.</span></span> <span data-ttu-id="eada1-125">먼저 수동 컨트롤러에 핫픽스를 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-125">We recommend that you install the hotfix on the passive controller first.</span></span>
3. <span data-ttu-id="eada1-126">핫픽스를 설치하려면 명령 프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-126">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="eada1-127">위 명령에서 공유 경로에 DNS 대신 IP를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-127">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="eada1-128">자격 증명 매개 변수는 인증된 공유에 액세스하는 경우에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-128">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="eada1-129">자격 증명 매개 변수를 사용하여 공유에 액세스하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-129">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="eada1-130">일반적으로 "모든 사용자"에게 개방된 공유도 인증되지 않은 사용자에게는 개방되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-130">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="eada1-131">메시지가 표시되면 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-131">Supply the password when prompted.</span></span>
   
    <span data-ttu-id="eada1-132">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-132">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts the hotfix installation and could reboot one or
    both of the controllers. If the device is serving I/Os, these will not
    be disrupted. Are you sure you want to continue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. <span data-ttu-id="eada1-133">핫픽스 설치를 확인하라는 메시지가 표시되면 **Y** 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-133">Type **Y** when prompted to confirm the hotfix installation.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="eada1-134">업데이트 2.2를 설치하는 경우 'all-hcsmdssoftwareudpate'가 붙은 이진 파일만 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-134">If installing Update 2.2, only install the binary file prefaced with 'all-hcsmdssoftwareudpate'.</span></span> <span data-ttu-id="eada1-135">all-cismdsagentupdatebundle이 앞에 붙은 Ci 및 MDS 에이전트 업데이트를 설치하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="eada1-135">Do not install the Cis and the MDS agent update prefaced with all-cismdsagentupdatebundle.</span></span> <span data-ttu-id="eada1-136">이렇게 하지 않으면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-136">Failure to do so will result in an error.</span></span> 

5. <span data-ttu-id="eada1-137">`Get-HcsUpdateStatus` cmdlet을 사용하여 업데이트를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-137">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="eada1-138">업데이트가 수동 컨트롤러에서 먼저 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-138">The update will first complete on the passive controller.</span></span> <span data-ttu-id="eada1-139">수동 컨트롤러가 업데이트되면 장애 조치(failover)된 다음 업데이트가 다른 컨트롤러에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-139">Once the passive controller is updated, there will be a failover and the update will then get applied on the other controller.</span></span> <span data-ttu-id="eada1-140">두 컨트롤러가 모두 업데이트되면 업데이트가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-140">The update is complete when both the controllers are updated.</span></span>
   
    <span data-ttu-id="eada1-141">다음 샘플 출력에서는 진행 중인 업데이트를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-141">The following sample output shows the update in progress.</span></span> <span data-ttu-id="eada1-142">업데이트가 진행 중이면 `RunInprogress`가 `True`입니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-142">The `RunInprogress` will be `True` when the update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 5/5/2016 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="eada1-143">다음 샘플 출력은 업데이트가 완료되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-143">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="eada1-144">업데이트가 완료되면 `RunInProgress`가 `False`입니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-144">The `RunInProgress` will be `False` when the update has completed.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 5/17/2016 9:15:55 AM
    LastUpdateTimestamp : 5/17/2016 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="eada1-145">업데이트가 진행 중일 때 cmdlet에서 `False`를 보고하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-145">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="eada1-146">핫픽스가 완료되었는지 확인하려면 몇 분 동안 기다린 후 이 명령을 다시 실행하고 `RunInProgress`가 `False`인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-146">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="eada1-147">맞으면 핫픽스가 완료된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-147">If it is, then the hotfix has completed.</span></span>

1. <span data-ttu-id="eada1-148">소프트웨어 업데이트가 완료된 후 시스템 소프트웨어 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-148">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="eada1-149">형식:</span><span class="sxs-lookup"><span data-stu-id="eada1-149">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="eada1-150">다음 버전이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-150">You should see the following versions:</span></span>
   
   * `HcsSoftwareVersion: 6.3.9600.17708`
   * `CisAgentVersion: 1.0.9299.0`
   * `MdsAgentVersion: 30.0.4698.16` 
     
     <span data-ttu-id="eada1-151">업데이트를 적용한 후 버전 번호가 변경되지 않으면 핫픽스를 적용하지 못한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-151">If the version numbers do not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="eada1-152">이 경우 추가 지원을 받으려면 [Microsoft 지원](../articles/storsimple/storsimple-contact-microsoft-support.md) 에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="eada1-152">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="eada1-153">나머지 업데이트를 적용하기 전에 `Restart-HcsController` cmdlet을 통해 활성 컨트롤러를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-153">You must restart the active controller via the `Restart-HcsController` cmdlet before applying the remaining updates.</span></span> 
     > 
     > 
2. <span data-ttu-id="eada1-154">나머지 일반 모드 핫픽스를 설치하려면 3-5단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-154">Repeat steps 3-5 to install the remaining regular-mode hotfixes.</span></span>
   
   * <span data-ttu-id="eada1-155">ISCSI 업데이트 KB3146621</span><span class="sxs-lookup"><span data-stu-id="eada1-155">The iSCSI update KB3146621</span></span>
   * <span data-ttu-id="eada1-156">WMI 업데이트 KB3103616</span><span class="sxs-lookup"><span data-stu-id="eada1-156">The WMI update KB3103616</span></span>
3. <span data-ttu-id="eada1-157">업데이트 2에서 업데이트하는 경우에는 이 단계를 건너뛰세요.</span><span class="sxs-lookup"><span data-stu-id="eada1-157">Skip this step if you are updating from Update 2.</span></span> <span data-ttu-id="eada1-158">업데이트 2 이전 버전에서 업데이트하는 경우에도 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-158">If you are updating from a version prior to Update 2, you will also need to download:</span></span>

    - <span data-ttu-id="eada1-159">LSI 드라이버 KB3121900</span><span class="sxs-lookup"><span data-stu-id="eada1-159">The LSI driver KB3121900</span></span>

    - <span data-ttu-id="eada1-160">Spaceport 업데이트 KB3090322</span><span class="sxs-lookup"><span data-stu-id="eada1-160">The Spaceport update KB3090322</span></span>

    - <span data-ttu-id="eada1-161">Storport 업데이트 KB3080728</span><span class="sxs-lookup"><span data-stu-id="eada1-161">The Storport update KB3080728</span></span>

#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="eada1-162">유지 관리 모드 핫픽스를 설치 및 확인하려면</span><span class="sxs-lookup"><span data-stu-id="eada1-162">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="eada1-163">KB3121899를 사용하여 디스크 펌웨어 업데이트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-163">Use KB3121899 to install disk firmware updates.</span></span> <span data-ttu-id="eada1-164">작업 중단 업데이트이며 완료하는 데 약 30분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-164">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="eada1-165">장치 직렬 콘솔에 연결하여 계획된 유지 관리 기간에 설치하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-165">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="eada1-166">디스크 펌웨어가 이미 최신 상태인 경우 이러한 업데이트를 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-166">Note that if your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="eada1-167">장치 일련 번호 콘솔에서 `Get-HcsUpdateAvailability` cmdlet을 실행하여 업데이트가 사용 가능한지 여부와 업데이트가 중단(유지 관리 모드) 또는 비중단(일반 모드)인지에 대해 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-167">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="eada1-168">디스크 펌웨어 업데이트를 설치하려면 아래 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-168">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="eada1-169">장치를 유지 관리 모드로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-169">Place the device in the Maintenance mode.</span></span> <span data-ttu-id="eada1-170">유지 관리 모드에서 장치에 연결할 때는 Windows PowerShell 원격을 사용해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-170">Note that you should not use Windows PowerShell remoting when connecting to a device in Maintenance mode.</span></span> <span data-ttu-id="eada1-171">장치 직렬 콘솔을 통해 연결된 경우에는 장치 컨트롤러에서 이 cmdlet을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-171">Instead run this cmdlet on the device controller when connected through the device serial console.</span></span> <span data-ttu-id="eada1-172">형식:</span><span class="sxs-lookup"><span data-stu-id="eada1-172">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="eada1-173">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-173">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76673
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="eada1-174">두 컨트롤러 모두 유지 관리 모드로 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-174">Both the controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="eada1-175">디스크 펌웨어 업데이트를 설치하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-175">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="eada1-176">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-176">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="eada1-177">`Get-HcsUpdateStatus` 명령을 사용하여 설치 진행률을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-177">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="eada1-178">`RunInProgress`가 `False`로 변경되면 업데이트가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-178">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="eada1-179">설치가 완료된 후에 유지 관리 모드 핫픽스가 설치된 컨트롤러가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-179">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="eada1-180">모든 권한이 있는 옵션 1로 로그인하고 디스크 펌웨어 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-180">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="eada1-181">형식:</span><span class="sxs-lookup"><span data-stu-id="eada1-181">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="eada1-182">예상된 디스크 펌웨어 버전은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-182">The expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="eada1-183">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-183">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17705
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected to Controller1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
         ActiveBIOS:0.45.0006
         BackupBIOS:0.45.0008
         MainCPLD:17.0.0005
         ActiveBMCRoot:2.0.000E
         BackupBMCRoot:2.0.000E
         BMCBoot:2.0.0001
         LsiFirmware:19.00.00.00
         LsiBios:07.37.00.00
         Battery1Firmware:06.29
         Battery2Firmware:06.29
         DomFirmware:X231600
         CanisterFirmware:3.5.0.32
         CanisterBootloader:5.03
         CanisterConfigCRC:0xD1B030A4
         CanisterVPDStructure:0x06
         CanisterGEMCPLD:0x17
         CanisterVPDCRC:0xEE3504B4
         MidplaneVPDStructure:0x0C
         MidplaneVPDCRC:0xA6BD4F64
         MidplaneCPLD:0x10
         PCM1Firmware:1.00|1.05
         PCM1VPDStructure:0x05
         PCM1VPDCRC:0x41BEF99C
         PCM2Firmware:1.00|1.05
         PCM2VPDStructure:0x05
         PCM2VPDCRC:0x41BEF99C
   
         DisksFirmware
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
   
    <span data-ttu-id="eada1-184">두 번째 컨트롤러에서 `Get-HcsFirmwareVersion` 명령을 실행하여 해당 소프트웨어 버전이 업데이트되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-184">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="eada1-185">그런 다음 유지 관리 모드를 끝낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-185">You can then exit the maintenance mode.</span></span> <span data-ttu-id="eada1-186">이렇게 하려면 각 장치 컨트롤러에 대해 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-186">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="eada1-187">유지 관리 모드를 종료하면 컨트롤러가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-187">The controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="eada1-188">디스크 펌웨어 업데이트가 성공적으로 적용되고 장치가 유지 관리 모드를 종료한 후 Azure 클래식 포털로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-188">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="eada1-189">유지 관리 모드 업데이트가 설치되었는지 24시간 동안 포털에 표시되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eada1-189">Note that the portal might not show that you installed the Maintenance mode updates for 24 hours.</span></span>

