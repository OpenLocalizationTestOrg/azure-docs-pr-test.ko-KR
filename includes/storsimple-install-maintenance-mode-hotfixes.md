<!--author=SharS last changed: 9/17/15-->

#### <a name="to-install-maintenance-mode-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="ffd61-101">StorSimple용 Windows PowerShell을 통해 유지 관리 모드 핫픽스를 설치하려면</span><span class="sxs-lookup"><span data-stu-id="ffd61-101">To install Maintenance mode hotfixes via Windows PowerShell for StorSimple</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ffd61-102">유지 관리 모드에서는 핫픽스를 각 컨트롤러에 차례대로 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd61-102">In Maintenance mode, you need to apply the hotfix first on one controller and then on the other controller.</span></span>
> 
> 

1. <span data-ttu-id="ffd61-103">장치를 유지 관리 모드로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd61-103">Place the device into Maintenance mode.</span></span> <span data-ttu-id="ffd61-104">유지 관리 모드로 전환하는 방법에 대한 지침은 [2단계: 유지 관리 모드 전환](../articles/storsimple/storsimple-update-device.md#step2) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffd61-104">See [Step 2: Enter Maintenance mode](../articles/storsimple/storsimple-update-device.md#step2) for instructions on how to enter Maintenance mode.</span></span>
2. <span data-ttu-id="ffd61-105">핫픽스를 적용하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd61-105">To apply the hotfix, type:</span></span>
   
     `Start-HcsHotfix` 
3. <span data-ttu-id="ffd61-106">메시지가 표시되면 핫픽스 파일이 포함된 네트워크 공유 폴더의 경로를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd61-106">When prompted, supply the path to the network shared folder that contains the hotfix files.</span></span>
4. <span data-ttu-id="ffd61-107">확인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffd61-107">You will be prompted for confirmation.</span></span> <span data-ttu-id="ffd61-108">**Y** 를 입력하여 핫픽스 설치를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd61-108">Type **Y** to proceed with the hotfix installation.</span></span>
5. <span data-ttu-id="ffd61-109">컨트롤러 하나에 핫픽스를 적용한 후 다른 컨트롤러에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd61-109">After you have applied the hotfix on one controller, log on to the other controller.</span></span> <span data-ttu-id="ffd61-110">이전 컨트롤러에서와 같이 핫픽스를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd61-110">Apply the hotfix as you did for the previous controller.</span></span>
6. <span data-ttu-id="ffd61-111">핫픽스를 적용한 후 유지 관리 모드를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd61-111">After the hotfixes are applied, exit Maintenance mode.</span></span> <span data-ttu-id="ffd61-112">지침은 [4단계: 유지 관리 모드 종료](../articles/storsimple/storsimple-update-device.md#step4) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffd61-112">See [Step 4: Exit Maintenance mode](../articles/storsimple/storsimple-update-device.md#step4) for instructions.</span></span>

