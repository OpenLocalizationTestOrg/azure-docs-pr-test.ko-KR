<!--author=SharS last changed: 11/18/16-->

#### <a name="to-install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="3f609-101">StorSimple용 Windows PowerShell을 통해 정기적인 업데이트를 설치하려면</span><span class="sxs-lookup"><span data-stu-id="3f609-101">To install regular updates via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="3f609-102">장치 직렬 콘솔을 열고 옵션 1, **모든 권한으로 로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f609-102">Open the device serial console and select option 1, **Log in with full access**.</span></span> <span data-ttu-id="3f609-103">암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3f609-103">Type the password.</span></span> <span data-ttu-id="3f609-104">기본 암호는 *Password1*입니다.</span><span class="sxs-lookup"><span data-stu-id="3f609-104">The default password is *Password1*.</span></span> 
2. <span data-ttu-id="3f609-105">명령 프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3f609-105">At the command prompt, type:</span></span>
   
     `Get-HcsUpdateAvailability`
   
    <span data-ttu-id="3f609-106">업데이트가 사용 가능한지 여부 및 업데이트 시 장치를 중단해야 하는지 여부에 대한 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f609-106">You will be notified if updates are available and whether the updates are disruptive or non-disruptive.</span></span>
3. <span data-ttu-id="3f609-107">명령 프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3f609-107">At the command prompt, type:</span></span>
   
     `Start-HcsUpdate`
   
    <span data-ttu-id="3f609-108">업데이트 프로세스가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f609-108">The update process will start.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="3f609-109">이 명령은 정기적인 업데이트에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f609-109">This command applies only to regular updates.</span></span> <span data-ttu-id="3f609-110">컨트롤러 하나에서만 이 명령을 실행하면 두 컨트롤러가 모두 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f609-110">You run this command on only one controller, but both controllers will be updated.</span></span> 
> * <span data-ttu-id="3f609-111">업데이트 프로세스 중에 컨트롤러 장애 조치(failover)가 수행되지만 시스템 가용성이나 작업에는 영향이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3f609-111">You may notice a controller failover during the update process; however, the failover will not affect system availability or operation.</span></span>
> 
> 

