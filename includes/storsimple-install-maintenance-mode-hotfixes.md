<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="49e5b-101">StorSimple 용 Windows PowerShell을 통해 유지 관리 모드 핫픽스 tooinstall</span><span class="sxs-lookup"><span data-stu-id="49e5b-101">tooinstall Maintenance mode hotfixes via Windows PowerShell for StorSimple</span></span>
> [!IMPORTANT]
> <span data-ttu-id="49e5b-102">유지 관리 모드에서 tooapply hello 핫픽스를 먼저 컨트롤러 하나에 필요 하 고에 다른 컨트롤러를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e5b-102">In Maintenance mode, you need tooapply hello hotfix first on one controller and then on hello other controller.</span></span>
> 
> 

1. <span data-ttu-id="49e5b-103">유지 관리 모드로 hello 장치를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e5b-103">Place hello device into Maintenance mode.</span></span> <span data-ttu-id="49e5b-104">참조 [2 단계: 입력 유지 관리 모드](../articles/storsimple/storsimple-update-device.md#step2) 방법에 대 한 지침은 tooenter 유지 관리 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="49e5b-104">See [Step 2: Enter Maintenance mode](../articles/storsimple/storsimple-update-device.md#step2) for instructions on how tooenter Maintenance mode.</span></span>
2. <span data-ttu-id="49e5b-105">형식 tooapply hello 핫픽스:</span><span class="sxs-lookup"><span data-stu-id="49e5b-105">tooapply hello hotfix, type:</span></span>
   
     `Start-HcsHotfix` 
3. <span data-ttu-id="49e5b-106">메시지가 표시 되 면 hello 경로 toohello 네트워크 공유 폴더 hello 핫픽스 파일이 포함 된를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e5b-106">When prompted, supply hello path toohello network shared folder that contains hello hotfix files.</span></span>
4. <span data-ttu-id="49e5b-107">확인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="49e5b-107">You will be prompted for confirmation.</span></span> <span data-ttu-id="49e5b-108">형식 **Y** tooproceed hello 핫픽스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e5b-108">Type **Y** tooproceed with hello hotfix installation.</span></span>
5. <span data-ttu-id="49e5b-109">후 다른 컨트롤러 toohello 로그온 컨트롤러 하나에 hello 핫픽스를 적용 한 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49e5b-109">After you have applied hello hotfix on one controller, log on toohello other controller.</span></span> <span data-ttu-id="49e5b-110">Hello 이전 컨트롤러에 대해 수행한 것 처럼 hello 핫픽스를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e5b-110">Apply hello hotfix as you did for hello previous controller.</span></span>
6. <span data-ttu-id="49e5b-111">Hello 핫픽스를 적용 한 후 유지 관리 모드를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="49e5b-111">After hello hotfixes are applied, exit Maintenance mode.</span></span> <span data-ttu-id="49e5b-112">지침은 [4단계: 유지 관리 모드 종료](../articles/storsimple/storsimple-update-device.md#step4) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49e5b-112">See [Step 4: Exit Maintenance mode](../articles/storsimple/storsimple-update-device.md#step4) for instructions.</span></span>

