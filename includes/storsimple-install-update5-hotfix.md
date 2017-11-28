<!--author=alkohli last changed: 08/21/17-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="6ba26-101">핫픽스를 다운로드하려면</span><span class="sxs-lookup"><span data-stu-id="6ba26-101">To download hotfixes</span></span>

<span data-ttu-id="6ba26-102">Microsoft 업데이트 카탈로그에서 소프트웨어 업데이트를 다운로드하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="6ba26-103">Internet Explorer를 시작하고 [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="6ba26-104">이 컴퓨터에서 Microsoft 업데이트 카탈로그를 처음 사용하는 경우 Microsoft 업데이트 카탈로그 추가 기능을 설치하라는 메시지가 나타나면 **설치** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

    ![카탈로그 설치](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. <span data-ttu-id="6ba26-106">Microsoft 업데이트 카탈로그의 검색 상자에 다운로드하려는 핫픽스의 KB(기술 자료) 번호(예: **4037264**)를 입력하고 **검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **4037264**, and then click **Search**.</span></span>
   
    <span data-ttu-id="6ba26-107">핫픽스 목록이 나타납니다(예: **StorSimple 8000 시리즈용 누적 소프트웨어 번들 업데이트 5.0**).</span><span class="sxs-lookup"><span data-stu-id="6ba26-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 5.0 for StorSimple 8000 Series**.</span></span>
   
    ![카탈로그 검색](./media/storsimple-install-update5-hotfix/update-catalog-search.png)

4. <span data-ttu-id="6ba26-109">**다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-109">Click **Download**.</span></span> <span data-ttu-id="6ba26-110">다운로드를 표시할 로컬 위치를 지정하거나 **검색** 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-110">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="6ba26-111">파일을 클릭하여 지정된 위치 및 폴더로 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-111">Click the files to download to the specified location and folder.</span></span> <span data-ttu-id="6ba26-112">장치에서 연결할 수 있는 네트워크 공유에 폴더도 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-112">The folder can also be copied to a network share that is reachable from the device.</span></span>
5. <span data-ttu-id="6ba26-113">위의 표에 나열된 추가 핫픽스(**4037266**)를 검색하고 해당 파일을 이전 표에 나열된 대로 특정 폴더에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-113">Search for any additional hotfixes listed in the table above (**4037266**), and download the corresponding files to the specific folders as listed in the preceding table.</span></span>

> [!NOTE]
> <span data-ttu-id="6ba26-114">피어 컨트롤러의 잠재적 오류 메시지를 검색하려면 컨트롤러 둘 다에서 핫픽스에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-114">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
>
> <span data-ttu-id="6ba26-115">핫픽스는 3개의 별도 폴더에 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-115">The hotfixes must be copied in 3 separate folders.</span></span> <span data-ttu-id="6ba26-116">예를 들어, 장치 소프트웨어/Cis/MDS 에이전트 업데이트는 _FirstOrderUpdate_ 폴더에 복사할 수 있으며, 다른 정기적인 업데이트는 모두 _SecondOrderUpdate_ 폴더에 복사되고, 유지 관리 모드 업데이트는 _ThirdOrderUpdate_ 폴더에 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-116">For example, the device software/Cis/MDS agent update can be copied in _FirstOrderUpdate_ folder, all the other non-disruptive updates could be copied in the _SecondOrderUpdate_ folder, and maintenance mode updates copied in _ThirdOrderUpdate_ folder.</span></span>

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="6ba26-117">일반 모드 핫픽스를 설치 및 확인하려면</span><span class="sxs-lookup"><span data-stu-id="6ba26-117">To install and verify regular mode hotfixes</span></span>

<span data-ttu-id="6ba26-118">일반 모드 핫픽스를 설치 및 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-118">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="6ba26-119">이미 Azure Portal을 사용하여 설치한 경우 [유지 관리 모드 핫픽스 설치 및 확인](#to-install-and-verify-maintenance-mode-hotfixes)으로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-119">If you already installed them using the Azure portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="6ba26-120">핫픽스를 설치하려면 StorSimple 장치 직렬 콘솔에서 Windows PowerShell 인터페이스에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-120">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="6ba26-121">[PuTTy를 사용하여 직렬 콘솔에 연결](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)에서 자세한 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="6ba26-121">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="6ba26-122">명령 프롬프트에서 **Enter**키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-122">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="6ba26-123">**옵션 1** 을 선택하여 모든 권한으로 장치에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-123">Select **Option 1** to log on to the device with full access.</span></span> <span data-ttu-id="6ba26-124">먼저 수동 컨트롤러에 핫픽스를 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-124">We recommend that you install the hotfix on the passive controller first.</span></span>
3. <span data-ttu-id="6ba26-125">핫픽스를 설치하려면 명령 프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-125">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="6ba26-126">위 명령에서 공유 경로에 DNS 대신 IP를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-126">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="6ba26-127">자격 증명 매개 변수는 인증된 공유에 액세스하는 경우에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-127">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="6ba26-128">자격 증명 매개 변수를 사용하여 공유에 액세스하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-128">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="6ba26-129">일반적으로 "모든 사용자"에게 개방된 공유도 인증되지 않은 사용자에게는 개방되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-129">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
4. <span data-ttu-id="6ba26-130">메시지가 표시되면 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-130">Supply the password when prompted.</span></span> <span data-ttu-id="6ba26-131">첫 번째 주문 업데이트를 설치하기 위한 샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-131">A sample output for installing the first order updates is shown below.</span></span> <span data-ttu-id="6ba26-132">첫 번째 주문 업데이트의 경우 특정 파일을 가리키도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-132">For the first order update, you need to point to the specific file.</span></span>

    >[!NOTE] 
    > <span data-ttu-id="6ba26-133">먼저 _HcsSoftwareUpdate.exe_를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-133">You should install the _HcsSoftwareUpdate.exe_ first.</span></span> <span data-ttu-id="6ba26-134">이 설치가 완료된 후에 _CisMdsAgentUpdate.exe_를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-134">After this install has completed, then install _CisMdsAgentUpdate.exe_.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts the hotfix installation and could reboot one or
        both of the controllers. If the device is serving I/Os, these will not
        be disrupted. Are you sure you want to continue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
5. <span data-ttu-id="6ba26-135">핫픽스 설치를 확인하라는 메시지가 표시되면 **Y** 를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-135">Type **Y** when prompted to confirm the hotfix installation.</span></span>
6. <span data-ttu-id="6ba26-136">`Get-HcsUpdateStatus` cmdlet을 사용하여 업데이트를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-136">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="6ba26-137">업데이트가 수동 컨트롤러에서 먼저 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-137">The update will first complete on the passive controller.</span></span> <span data-ttu-id="6ba26-138">수동 컨트롤러가 업데이트되면 장애 조치(failover)된 다음 업데이트가 다른 컨트롤러에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-138">Once the passive controller is updated, there will be a failover and the update will then get applied on the other controller.</span></span> <span data-ttu-id="6ba26-139">두 컨트롤러가 모두 업데이트되면 업데이트가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-139">The update is complete when both the controllers are updated.</span></span>
   
    <span data-ttu-id="6ba26-140">다음 샘플 출력에서는 진행 중인 업데이트를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-140">The following sample output shows the update in progress.</span></span> <span data-ttu-id="6ba26-141">업데이트가 진행 중이면 `RunInprogress`가 `True`입니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-141">The `RunInprogress` is `True` when the update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 07/28/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="6ba26-142">다음 샘플 출력은 업데이트가 완료되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-142">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="6ba26-143">업데이트가 완료되면 `RunInProgress`가 `False`입니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-143">The `RunInProgress` is `False` when the update is complete.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 07/28/2017 9:15:55 AM
    LastUpdateTimestamp : 07/28/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="6ba26-144">업데이트가 진행 중일 때 cmdlet에서 `False`를 보고하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-144">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="6ba26-145">핫픽스가 완료되었는지 확인하려면 몇 분 동안 기다린 후 이 명령을 다시 실행하고 `RunInProgress`가 `False`인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-145">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="6ba26-146">맞으면 핫픽스가 완료된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-146">If it is, then the hotfix has completed.</span></span>

7. <span data-ttu-id="6ba26-147">소프트웨어 업데이트가 완료된 후 시스템 소프트웨어 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-147">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="6ba26-148">형식:</span><span class="sxs-lookup"><span data-stu-id="6ba26-148">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="6ba26-149">다음 버전이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-149">You should see the following versions:</span></span>
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 5.0`
   *  `HcsSoftwareVersion: 6.3.9600.17845`
   
    <span data-ttu-id="6ba26-150">업데이트를 적용한 후 버전 번호가 변경되지 않으면 핫픽스를 적용하지 못한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-150">If the version number does not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="6ba26-151">이 경우 추가 지원을 받으려면 [Microsoft 지원](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) 에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="6ba26-151">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) for further assistance.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="6ba26-152">다음 업데이트를 적용하기 전에 `Restart-HcsController` cmdlet을 통해 활성 컨트롤러를 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-152">You must restart the active controller via the `Restart-HcsController` cmdlet before applying the next update.</span></span>
     
8. <span data-ttu-id="6ba26-153">_FirstOrderUpdate_ 폴더에 다운로드한 _CisMDSAgentupdate.exe_ 에이전트를 설치하려면 3~6단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-153">Repeat steps 3-6 to install the _CisMDSAgentupdate.exe_ agent downloaded to your _FirstOrderUpdate_ folder.</span></span>
8. <span data-ttu-id="6ba26-154">두 번째 주문 업데이트를 설치하려면 3~6단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-154">Repeat steps 3-6 to install the second order updates.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="6ba26-155">두 번째 주문 업데이트의 경우 `Start-HcsHotfix cmdlet`을 실행하고 두 번째 주문 업데이트가 있는 폴더를 가리키면 여러 업데이트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-155">For second order updates, multiple updates can be installed by just running the `Start-HcsHotfix cmdlet` and pointing to the folder where second order updates are located.</span></span> <span data-ttu-id="6ba26-156">이 cmdlet은 폴더에서 사용할 수 있는 모든 업데이트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-156">The cmdlet will execute all the updates available in the folder.</span></span> <span data-ttu-id="6ba26-157">업데이트가 이미 설치되어 경우 업데이트 논리를 감지하고 해당 업데이트를 적용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-157">If an update is already installed, the update logic will detect that and not apply that update.</span></span>

    <span data-ttu-id="6ba26-158">핫픽스를 모두 설치한 후 `Get-HcsSystem` cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-158">After all the hotfixes are installed, use the `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="6ba26-159">버전은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-159">The versions should be:</span></span>
    
    * `CisAgentVersion:  1.0.9724.0`
    * `MdsAgentVersion: 35.2.2.0`
    * `Lsisas2Version: 2.0.78.00`


#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="6ba26-160">유지 관리 모드 핫픽스를 설치 및 확인하려면</span><span class="sxs-lookup"><span data-stu-id="6ba26-160">To install and verify maintenance mode hotfixes</span></span>

<span data-ttu-id="6ba26-161">KB4037263을 사용하여 디스크 펌웨어 업데이트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-161">Use KB4037263 to install disk firmware updates.</span></span> <span data-ttu-id="6ba26-162">작업 중단 업데이트이며 완료하는 데 약 30분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-162">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="6ba26-163">장치 직렬 콘솔에 연결하여 계획된 유지 관리 기간에 설치하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-163">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

> [!NOTE] 
> <span data-ttu-id="6ba26-164">디스크 펌웨어가 이미 최신 상태인 경우 이러한 업데이트를 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-164">If your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="6ba26-165">장치 일련 번호 콘솔에서 `Get-HcsUpdateAvailability` cmdlet을 실행하여 업데이트가 사용 가능한지 여부와 업데이트가 중단(유지 관리 모드) 또는 비중단(일반 모드)인지에 대해 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-165">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="6ba26-166">디스크 펌웨어 업데이트를 설치하려면 아래 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-166">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="6ba26-167">장치를 유지 관리 모드로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-167">Place the device in the maintenance mode.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="6ba26-168">유지 관리 모드에서 장치에 연결할 때는 Windows PowerShell 원격을 사용해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-168">Do not use Windows PowerShell remoting when connecting to a device in maintenance mode.</span></span> <span data-ttu-id="6ba26-169">장치 직렬 콘솔을 통해 연결된 경우에는 장치 컨트롤러에서 이 cmdlet을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-169">Instead run this cmdlet on the device controller when connected through the device serial console.</span></span>

    <span data-ttu-id="6ba26-170">컨트롤러를 유지 관리 모드로 배치하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-170">To place the controller in maintenance mode, type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="6ba26-171">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-171">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8600
        Name: Update4-8600-mystorsimple
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="6ba26-172">두 컨트롤러 모두 유지 관리 모드로 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-172">Both the controllers then restart into maintenance mode.</span></span>
2. <span data-ttu-id="6ba26-173">디스크 펌웨어 업데이트를 설치하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-173">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="6ba26-174">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-174">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="6ba26-175">`Get-HcsUpdateStatus` 명령을 사용하여 설치 진행률을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-175">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="6ba26-176">`RunInProgress`가 `False`로 변경되면 업데이트가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-176">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="6ba26-177">설치가 완료된 후에 유지 관리 모드 핫픽스가 설치된 컨트롤러가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-177">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="6ba26-178">모든 권한이 있는 옵션 1로 로그인하고 디스크 펌웨어 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-178">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="6ba26-179">형식:</span><span class="sxs-lookup"><span data-stu-id="6ba26-179">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="6ba26-180">예상된 디스크 펌웨어 버전은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-180">The expected disk firmware versions are:</span></span>
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N003, 0107`
   
   <span data-ttu-id="6ba26-181">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-181">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17845
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected to Controller1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
           ActiveBIOS:0.45.0010
              BackupBIOS:0.45.0006
              MainCPLD:17.0.000b
              ActiveBMCRoot:2.0.001F
              BackupBMCRoot:2.0.001F
              BMCBoot:2.0.0002
              LsiFirmware:20.00.04.00
              LsiBios:07.37.00.00
              Battery1Firmware:06.2C
              Battery2Firmware:06.2C
              DomFirmware:X231600
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0x9134777A
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x19
              CanisterVPDCRC:0x142F7DC2
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:1.00|1.05
              PCM1VPDStructure:0x05
              PCM1VPDCRC:0x41BEF99C
              PCM2Firmware:1.00|1.05
              PCM2VPDStructure:0x05
              PCM2VPDCRC:0x41BEF99C

           EbodFirmware
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0xB23150F8
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x14
              CanisterVPDCRC:0xBAA55828
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:3.11
              PCM1VPDStructure:0x03
              PCM1VPDCRC:0x6B58AD13
              PCM2Firmware:3.11
              PCM2VPDStructure:0x03
              PCM2VPDCRC:0x6B58AD13

           DisksFirmware
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
   
    <span data-ttu-id="6ba26-182">두 번째 컨트롤러에서 `Get-HcsFirmwareVersion` 명령을 실행하여 해당 소프트웨어 버전이 업데이트되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-182">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="6ba26-183">그런 다음 유지 관리 모드를 끝낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-183">You can then exit the maintenance mode.</span></span> <span data-ttu-id="6ba26-184">이렇게 하려면 각 장치 컨트롤러에 대해 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-184">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`

5. <span data-ttu-id="6ba26-185">유지 관리 모드를 종료하면 컨트롤러가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-185">The controllers restart when you exit maintenance mode.</span></span> <span data-ttu-id="6ba26-186">디스크 펌웨어 업데이트가 성공적으로 적용되고 장치가 유지 관리 모드를 종료한 후 Azure Portal로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-186">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure portal.</span></span> <span data-ttu-id="6ba26-187">유지 관리 모드 업데이트가 설치되었는지 24시간 동안 포털에 표시되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ba26-187">Note that the portal might not show that you installed the maintenance mode updates for 24 hours.</span></span>

