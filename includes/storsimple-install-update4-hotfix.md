<!--author=alkohli last changed: 02/10/17-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="1b37e-101">toodownload 핫픽스</span><span class="sxs-lookup"><span data-stu-id="1b37e-101">toodownload hotfixes</span></span>

<span data-ttu-id="1b37e-102">Hello hello Microsoft Update 카탈로그에서에서 단계 toodownload hello 소프트웨어 업데이트를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-102">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="1b37e-103">Internet Explorer를 시작 하 고 탐색 너무[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="1b37e-104">Microsoft Update 카탈로그 hello를 사용 하 여이 컴퓨터에 처음으로 이면 클릭 **설치** 때 메시지 표시 tooinstall hello Microsoft Update 카탈로그 추가 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

    ![카탈로그 설치](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. <span data-ttu-id="1b37e-106">Hello Microsoft Update 카탈로그의 hello 검색 상자에 hello 기술 자료 (KB) 번호를 입력 hello 핫픽스의 원하는 toodownload, 예를 들어 **4011839**, 클릭 하 고 **검색**합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **4011839**, and then click **Search**.</span></span>
   
    <span data-ttu-id="1b37e-107">hello 핫픽스 목록이 표시 되 면 예를 들어 **StorSimple 8000 시리즈에 대 한 누적 소프트웨어 번들 업데이트 4.0**합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-107">hello hotfix listing appears, for example, **Cumulative Software Bundle Update 4.0 for StorSimple 8000 Series**.</span></span>
   
    ![카탈로그 검색](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)

4. <span data-ttu-id="1b37e-109">**다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-109">Click **Download**.</span></span> <span data-ttu-id="1b37e-110">지정 하거나 **찾아보기** tooa 로컬 위치 hello tooappear 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-110">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="1b37e-111">Hello 파일 클릭 toodownload toohello 위치 및 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-111">Click hello files toodownload toohello specified location and folder.</span></span> <span data-ttu-id="1b37e-112">hello 폴더 hello 장치에서 연결할 수 있는 tooa 복사한 네트워크 공유 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-112">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>
5. <span data-ttu-id="1b37e-113">위의 hello 표에 나열 된 모든 추가 핫픽스에 대 한 검색 (**4011841**), 및 hello 테이블 앞에 나열 된 toohello 특정 폴더에 파일 다운로드 hello에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-113">Search for any additional hotfixes listed in hello table above (**4011841**), and download hello corresponding files toohello specific folders as listed in hello preceding table.</span></span>

> [!NOTE]
> <span data-ttu-id="1b37e-114">hello 핫픽스 두 컨트롤러 toodetect hello 피어 컨트롤러에서 잠재적인 오류 메시지에서 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-114">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
>
> <span data-ttu-id="1b37e-115">hello 핫픽스 3 별도 폴더에 복사 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-115">hello hotfixes must be copied in 3 separate folders.</span></span> <span data-ttu-id="1b37e-116">예를 들어에 hello 장치 소프트웨어/Ci/MDS 에이전트 업데이트를 복사할 수 있습니다 _FirstOrderUpdate_ hello 모든 폴더를 다른 정기적인 업데이트 hello에 복사할 수 없습니다 _SecondOrderUpdate_ 폴더 및 유지 관리 모드 업데이트에서 복사한 _ThirdOrderUpdate_ 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-116">For example, hello device software/Cis/MDS agent update can be copied in _FirstOrderUpdate_ folder, all hello other non-disruptive updates could be copied in hello _SecondOrderUpdate_ folder, and maintenance mode updates copied in _ThirdOrderUpdate_ folder.</span></span>

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="1b37e-117">tooinstall 일반 모드 핫픽스를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-117">tooinstall and verify regular mode hotfixes</span></span>

<span data-ttu-id="1b37e-118">Hello 단계 tooinstall 다음을 수행 하 고 일반 모드 핫픽스를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-118">Perform hello following steps tooinstall and verify regular-mode hotfixes.</span></span> <span data-ttu-id="1b37e-119">이미 설치 하는 경우에 Azure 클래식 포털 hello를 사용 하 여 너무 건너 뛸[설치 하 고 유지 관리 모드 핫픽스 확인](#to-install-and-verify-maintenance-mode-hotfixes)합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-119">If you already installed them using hello Azure classic portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="1b37e-120">StorSimple 장치 직렬 콘솔에 액세스 hello Windows PowerShell 인터페이스 tooinstall hello 핫픽스 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-120">tooinstall hello hotfixes, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="1b37e-121">에 따라 hello에 필요한 세부 정보 [사용 PuTTy tooconnect toohello 직렬 콘솔](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-121">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="1b37e-122">Hello 명령 프롬프트에를 눌러 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-122">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="1b37e-123">선택 **옵션 1** toolog 전체 액세스 권한이 있는 toohello 장치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-123">Select **Option 1** toolog on toohello device with full access.</span></span> <span data-ttu-id="1b37e-124">Hello 핫픽스 hello 수동 컨트롤러에 먼저 설치 해야 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-124">We recommend that you install hello hotfix on hello passive controller first.</span></span>
3. <span data-ttu-id="1b37e-125">tooinstall hello 핫픽스, 형식 hello 명령 프롬프트에서:</span><span class="sxs-lookup"><span data-stu-id="1b37e-125">tooinstall hello hotfix, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="1b37e-126">명령 위에 hello 공유 경로에 DNS를 사용 하지 않고 IP를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-126">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="1b37e-127">hello credential 매개 변수는 인증 된 공유에 액세스 하는 경우에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-127">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="1b37e-128">Hello 자격 증명 매개 변수 tooaccess 공유를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-128">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="1b37e-129">열려 있는 너무 일반적으로 "everyone 이라는"도 공유 toounauthenticated 사용자 열.</span><span class="sxs-lookup"><span data-stu-id="1b37e-129">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
    <span data-ttu-id="1b37e-130">메시지가 표시 되 면 hello 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-130">Supply hello password when prompted.</span></span>
   
    <span data-ttu-id="1b37e-131">Hello 첫 번째 주문 업데이트를 설치 하기 위한 샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-131">A sample output for installing hello first order updates is shown below.</span></span> <span data-ttu-id="1b37e-132">첫 번째 주문 업데이트 hello toopoint toohello 특정 파일이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-132">For hello first order update, you need toopoint toohello specific file.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts hello hotfix installation and could reboot one or
        both of hello controllers. If hello device is serving I/Os, these will not
        be disrupted. Are you sure you want toocontinue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
4. <span data-ttu-id="1b37e-133">형식 **Y** 때 메시지 표시 tooconfirm hello 핫픽스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-133">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
5. <span data-ttu-id="1b37e-134">Hello를 사용 하 여 hello 업데이트를 모니터링할 `Get-HcsUpdateStatus` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1b37e-134">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="1b37e-135">hello 업데이트 hello 수동 컨트롤러에서 먼저 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-135">hello update will first complete on hello passive controller.</span></span> <span data-ttu-id="1b37e-136">Hello 수동 컨트롤러 업데이트 되, 장애 조치 됩니다 hello 업데이트 후에 적용 되 면 다른 컨트롤러를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-136">Once hello passive controller is updated, there will be a failover and hello update will then get applied on hello other controller.</span></span> <span data-ttu-id="1b37e-137">hello 컨트롤러를 모두 업데이트 하는 경우 hello 업데이트가 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-137">hello update is complete when both hello controllers are updated.</span></span>
   
    <span data-ttu-id="1b37e-138">hello 다음 샘플은 출력 hello 업데이트 진행 중에서입니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-138">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="1b37e-139">hello `RunInprogress` 됩니다 `True` hello 업데이트가 진행 중 설정 된 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-139">hello `RunInprogress` will be `True` when hello update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 02/03/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="1b37e-140">다음 샘플 출력 hello 해당 hello 업데이트가 완료 된 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-140">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="1b37e-141">hello `RunInProgress` 됩니다 `False` hello 업데이트 작업을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-141">hello `RunInProgress` will be `False` when hello update has completed.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 02/03/2017 9:15:55 AM
    LastUpdateTimestamp : 02/03/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="1b37e-142">경우에 따라서는 cmdlet 보고서 hello `False` hello 업데이트 중인 경우 계속 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-142">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="1b37e-143">핫픽스 hello tooensure 완료, 몇 분 정도 기다렸다가,이 명령을 다시 실행 및 해당 hello 확인 `RunInProgress` 은 `False`합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-143">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="1b37e-144">인 경우 hello 핫픽스 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-144">If it is, then hello hotfix has completed.</span></span>

6. <span data-ttu-id="1b37e-145">Hello 소프트웨어 업데이트가 완료 되 면 hello 시스템 소프트웨어 버전을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-145">After hello software update is complete, verify hello system software versions.</span></span> <span data-ttu-id="1b37e-146">형식:</span><span class="sxs-lookup"><span data-stu-id="1b37e-146">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="1b37e-147">다음 버전 hello를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-147">You should see hello following versions:</span></span>
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 4.0`
   *  `HcsSoftwareVersion: 6.3.9600.17820`
   
    <span data-ttu-id="1b37e-148">Hello 업데이트를 적용 한 후 hello 버전 번호가 변경 되지 않으면 해당 hello 핫픽스가 tooapply 못한 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-148">If hello version number does not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="1b37e-149">이 경우 추가 지원을 받으려면 [Microsoft 지원](../articles/storsimple/storsimple-contact-microsoft-support.md) 에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="1b37e-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="1b37e-150">Hello hello 통해 활성 컨트롤러를 다시 시작 해야 `Restart-HcsController` 적용 하기 전에 cmdlet hello 다음 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-150">You must restart hello active controller via hello `Restart-HcsController` cmdlet before applying hello next update.</span></span>
     
7. <span data-ttu-id="1b37e-151">3-5 tooinstall hello Ci/MDS 에이전트 다운로드 tooyour 단계를 반복 _FirstOrderUpdate_ 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-151">Repeat steps 3-5 tooinstall hello Cis/MDS agent downloaded tooyour _FirstOrderUpdate_ folder.</span></span> 
8. <span data-ttu-id="1b37e-152">3-5 단계 tooinstall hello 두 번째 주문 업데이트를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-152">Repeat steps 3-5 tooinstall hello second order updates.</span></span> <span data-ttu-id="1b37e-153">**두 번째 주문 업데이트에 대 한 여러 업데이트가 방금 hello를 실행 하 여 설치 수 `Start-HcsHotfix cmdlet` 및 두 번째 주문 업데이트 있는 포인팅 toohello 폴더. hello cmdlet hello 폴더에서 사용할 수 있는 모든 hello 업데이트 실행 됩니다.**</span><span class="sxs-lookup"><span data-stu-id="1b37e-153">**For second order updates, multiple updates can be installed by just running hello `Start-HcsHotfix cmdlet` and pointing toohello folder where second order updates are located. hello cmdlet will execute all hello updates available in hello folder.**</span></span> <span data-ttu-id="1b37e-154">업데이트가 이미 설치 되어 있는 경우 hello 업데이트 논리에서는 하는 검색 하 고 해당 업데이트를 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-154">If an update is already installed, hello update logic will detect that and not apply that update.</span></span> 

<span data-ttu-id="1b37e-155">Hello를 사용 하 여 모든 hello 핫픽스를 설치 했으면 `Get-HcsSystem` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1b37e-155">After all hello hotfixes are installed, use hello `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="1b37e-156">hello 버전 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-156">hello versions should be:</span></span>

   * `CisAgentVersion:  1.0.9441.0`
   * `MdsAgentVersion: 35.2.2.0`
   * `Lsisas2Version: 2.0.78.00`


#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="1b37e-157">tooinstall 유지 관리 모드 핫픽스를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-157">tooinstall and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="1b37e-158">KB4011837 tooinstall 디스크 펌웨어 업데이트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-158">Use KB4011837 tooinstall disk firmware updates.</span></span> <span data-ttu-id="1b37e-159">이러한 업데이트가 중단 되 고 약 30 분 toocomplete를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-159">These are disruptive updates and take around 30 minutes toocomplete.</span></span> <span data-ttu-id="1b37e-160">선택할 수 있습니다 tooinstall 계획 된 유지 관리 창에서 이러한 연결 toohello 장치 직렬 콘솔에서.</span><span class="sxs-lookup"><span data-stu-id="1b37e-160">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

<span data-ttu-id="1b37e-161">디스크 펌웨어 이미 최신 상태 이면 필요 없는 tooinstall 이러한 업데이트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-161">Note that if your disk firmware is already up-to-date, you won't need tooinstall these updates.</span></span> <span data-ttu-id="1b37e-162">Hello 실행 `Get-HcsUpdateAvailability` hello 장치 직렬 콘솔 toocheck 업데이트 사용할 수 있고 여부 hello에서 cmdlet은 중단 (유지 관리 모드) 또는 무중단 (일반 모드)를 업데이트 합니다. 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-162">Run hello `Get-HcsUpdateAvailability` cmdlet from hello device serial console toocheck if updates are available and whether hello updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="1b37e-163">tooinstall hello 디스크 펌웨어 업데이트 아래 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-163">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="1b37e-164">Hello 유지 관리 모드에서 hello 장치를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-164">Place hello device in hello maintenance mode.</span></span> <span data-ttu-id="1b37e-165">**참고 tooa 장치 유지 관리 모드에 연결할 때 Windows PowerShell 원격을 사용 하지 않아야 합니다. 대신 hello 장치 컨트롤러 hello 장치 직렬 콘솔을 통해 연결 된 경우에이 cmdlet을 실행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1b37e-165">**Note that you should not use Windows PowerShell remoting when connecting tooa device in maintenance mode. Instead run this cmdlet on hello device controller when connected through hello device serial console.**</span></span> <span data-ttu-id="1b37e-166">형식:</span><span class="sxs-lookup"><span data-stu-id="1b37e-166">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="1b37e-167">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-167">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8600
        Name: Update4-8600-mystorsimple
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="1b37e-168">두 hello 컨트롤러 유지 관리 모드로 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-168">Both hello controllers then restart into maintenance mode.</span></span>
2. <span data-ttu-id="1b37e-169">tooinstall hello 디스크 펌웨어 업데이트, 유형:</span><span class="sxs-lookup"><span data-stu-id="1b37e-169">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="1b37e-170">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-170">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="1b37e-171">Hello 설치 진행률 사용 하 여 모니터링 `Get-HcsUpdateStatus` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-171">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="1b37e-172">hello 업데이트가 완료 되 면 hello `RunInProgress` 쪽 변경`False`합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-172">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="1b37e-173">Hello 설치가 완료 되 면 유지 관리 모드 핫픽스가 설치 되어 있는 hello hello 컨트롤러 다시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-173">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="1b37e-174">모든 권한이 있는 옵션 1로 로그인 하 고 hello 디스크 펌웨어 버전을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-174">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="1b37e-175">형식:</span><span class="sxs-lookup"><span data-stu-id="1b37e-175">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="1b37e-176">hello는 디스크 펌웨어 버전이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-176">hello expected disk firmware versions are:</span></span>
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N002, 0106`
   
   <span data-ttu-id="1b37e-177">샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-177">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17820
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
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
   
    <span data-ttu-id="1b37e-178">Hello 실행 `Get-HcsFirmwareVersion` 소프트웨어 버전 hello 하는 hello 두 번째 컨트롤러 tooverify에 명령 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-178">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="1b37e-179">그런 다음 hello 유지 관리 모드를 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-179">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="1b37e-180">따라서 toodo 다음 각 장치 컨트롤러에 대 한 명령을 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-180">toodo so, type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`

5. <span data-ttu-id="1b37e-181">유지 관리 모드를 종료 하는 hello 컨트롤러 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-181">hello controllers restart when you exit maintenance mode.</span></span> <span data-ttu-id="1b37e-182">Hello 디스크 펌웨어 후 업데이트를 적용 하 고 hello 장치 반환 toohello Azure 클래식 포털의 유지 관리 모드 종료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-182">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure classic portal.</span></span> <span data-ttu-id="1b37e-183">Note 24 시간 동안 hello 유지 관리 모드 업데이트를 설치한 hello 포털이 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b37e-183">Note that hello portal might not show that you installed hello maintenance mode updates for 24 hours.</span></span>

