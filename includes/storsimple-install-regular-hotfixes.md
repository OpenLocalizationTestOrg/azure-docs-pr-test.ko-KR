<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-regular-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="618ec-101">StorSimple 용 Windows PowerShell을 통해 tooinstall 정기적인 핫픽스</span><span class="sxs-lookup"><span data-stu-id="618ec-101">tooinstall regular hotfixes via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="618ec-102">Toohello 장치 직렬 콘솔을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="618ec-102">Connect toohello device serial console.</span></span> <span data-ttu-id="618ec-103">자세한 내용은 참조 [1 단계: toohello 직렬 콘솔 연결](../articles/storsimple/storsimple-update-device.md#step1)합니다.</span><span class="sxs-lookup"><span data-stu-id="618ec-103">For more information, see [Step 1: Connect toohello serial console](../articles/storsimple/storsimple-update-device.md#step1).</span></span>
2. <span data-ttu-id="618ec-104">Hello 직렬 콘솔 메뉴에서 옵션 1, 선택 **전체 권한으로 로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="618ec-104">In hello serial console menu, select option 1, **Log in with full access**.</span></span> <span data-ttu-id="618ec-105">Hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="618ec-105">Type hello password.</span></span> <span data-ttu-id="618ec-106">hello 기본 암호는 **Password1**합니다.</span><span class="sxs-lookup"><span data-stu-id="618ec-106">hello default password is **Password1**.</span></span>
3. <span data-ttu-id="618ec-107">Hello 명령 프롬프트에서 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="618ec-107">At hello command prompt, type:</span></span>
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > <span data-ttu-id="618ec-108">이 명령은 tooregular 핫픽스만을 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="618ec-108">This command applies only tooregular hotfixes.</span></span> <span data-ttu-id="618ec-109">컨트롤러 하나에서만 이 명령을 실행하면 두 컨트롤러가 모두 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="618ec-109">You run this command on only one controller, but both controllers will be updated.</span></span>
    > <span data-ttu-id="618ec-110">컨트롤러 장애 조치 hello 업데이트 과정; 표시 될 수도 있습니다. 그러나 시스템 가용성이 나 작동 hello 장애 조치 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="618ec-110">You may notice a controller failover during hello update process; however, hello failover will not affect system availability or operation.</span></span>

4. <span data-ttu-id="618ec-111">메시지가 표시 되 면 hello 경로 toohello 네트워크 공유 폴더 hello 핫픽스 파일이 포함 된를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="618ec-111">When prompted, supply hello path toohello network shared folder that contains hello hotfix files.</span></span>
5. <span data-ttu-id="618ec-112">확인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="618ec-112">You will be prompted for confirmation.</span></span> <span data-ttu-id="618ec-113">형식 **Y** tooproceed hello 핫픽스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="618ec-113">Type **Y** tooproceed with hello hotfix installation.</span></span>

