<!--author=SharS last changed: 9/17/15-->

#### <a name="to-install-regular-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="c5a18-101">StorSimple용 Windows PowerShell을 통해 정기적인 핫픽스를 설치하려면</span><span class="sxs-lookup"><span data-stu-id="c5a18-101">To install regular hotfixes via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="c5a18-102">장치 직렬 콘솔에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a18-102">Connect to the device serial console.</span></span> <span data-ttu-id="c5a18-103">자세한 내용은 [1단계: 직렬 콘솔에 연결](../articles/storsimple/storsimple-update-device.md#step1)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5a18-103">For more information, see [Step 1: Connect to the serial console](../articles/storsimple/storsimple-update-device.md#step1).</span></span>
2. <span data-ttu-id="c5a18-104">직렬 콘솔 메뉴에서 옵션 1, **모든 권한으로 로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a18-104">In the serial console menu, select option 1, **Log in with full access**.</span></span> <span data-ttu-id="c5a18-105">암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a18-105">Type the password.</span></span> <span data-ttu-id="c5a18-106">기본 암호는 **Password1**입니다.</span><span class="sxs-lookup"><span data-stu-id="c5a18-106">The default password is **Password1**.</span></span>
3. <span data-ttu-id="c5a18-107">명령 프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a18-107">At the command prompt, type:</span></span>
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > <span data-ttu-id="c5a18-108">이 명령은 정기적인 핫픽스에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5a18-108">This command applies only to regular hotfixes.</span></span> <span data-ttu-id="c5a18-109">컨트롤러 하나에서만 이 명령을 실행하면 두 컨트롤러가 모두 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5a18-109">You run this command on only one controller, but both controllers will be updated.</span></span>
    > <span data-ttu-id="c5a18-110">업데이트 프로세스 중에 컨트롤러 장애 조치(failover)가 수행되지만 시스템 가용성이나 작업에는 영향이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c5a18-110">You may notice a controller failover during the update process; however, the failover will not affect system availability or operation.</span></span>

4. <span data-ttu-id="c5a18-111">메시지가 표시되면 핫픽스 파일이 포함된 네트워크 공유 폴더의 경로를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a18-111">When prompted, supply the path to the network shared folder that contains the hotfix files.</span></span>
5. <span data-ttu-id="c5a18-112">확인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5a18-112">You will be prompted for confirmation.</span></span> <span data-ttu-id="c5a18-113">**Y** 를 입력하여 핫픽스 설치를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5a18-113">Type **Y** to proceed with the hotfix installation.</span></span>

