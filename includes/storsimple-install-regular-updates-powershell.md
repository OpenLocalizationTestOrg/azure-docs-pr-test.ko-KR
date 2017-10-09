<!--author=SharS last changed: 11/18/16-->

#### <a name="tooinstall-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="f2613-101">StorSimple 용 Windows PowerShell을 통해 tooinstall 정기적으로 업데이트</span><span class="sxs-lookup"><span data-stu-id="f2613-101">tooinstall regular updates via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="f2613-102">Hello 장치 직렬 콘솔을 열고 선택 옵션 1, **전체 권한으로 로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2613-102">Open hello device serial console and select option 1, **Log in with full access**.</span></span> <span data-ttu-id="f2613-103">Hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2613-103">Type hello password.</span></span> <span data-ttu-id="f2613-104">hello 기본 암호는 *Password1*합니다.</span><span class="sxs-lookup"><span data-stu-id="f2613-104">hello default password is *Password1*.</span></span> 
2. <span data-ttu-id="f2613-105">Hello 명령 프롬프트에서 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2613-105">At hello command prompt, type:</span></span>
   
     `Get-HcsUpdateAvailability`
   
    <span data-ttu-id="f2613-106">사용 가능한 업데이트가 있으면 및 중단 또는 중단 없는 hello 업데이트 되는지 여부를 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f2613-106">You will be notified if updates are available and whether hello updates are disruptive or non-disruptive.</span></span>
3. <span data-ttu-id="f2613-107">Hello 명령 프롬프트에서 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2613-107">At hello command prompt, type:</span></span>
   
     `Start-HcsUpdate`
   
    <span data-ttu-id="f2613-108">hello 업데이트 프로세스가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2613-108">hello update process will start.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="f2613-109">이 명령은 tooregular 업데이트에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2613-109">This command applies only tooregular updates.</span></span> <span data-ttu-id="f2613-110">컨트롤러 하나에서만 이 명령을 실행하면 두 컨트롤러가 모두 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2613-110">You run this command on only one controller, but both controllers will be updated.</span></span> 
> * <span data-ttu-id="f2613-111">컨트롤러 장애 조치 hello 업데이트 과정; 표시 될 수도 있습니다. 그러나 시스템 가용성이 나 작동 hello 장애 조치 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2613-111">You may notice a controller failover during hello update process; however, hello failover will not affect system availability or operation.</span></span>
> 
> 

