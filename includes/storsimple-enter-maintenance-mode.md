<!--author=SharS last changed: 12/01/15-->

#### <a name="to-enter-maintenance-mode"></a><span data-ttu-id="a88e3-101">유지 관리 모드를 설정하려면</span><span class="sxs-lookup"><span data-stu-id="a88e3-101">To enter Maintenance mode</span></span>
1. <span data-ttu-id="a88e3-102">직렬 콘솔 메뉴에서 옵션 1, **모든 권한으로 로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a88e3-102">In the serial console menu, choose option 1, **Log in with full access**.</span></span>
2. <span data-ttu-id="a88e3-103">암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a88e3-103">Type the password.</span></span> <span data-ttu-id="a88e3-104">기본 암호는 **Password1**입니다.</span><span class="sxs-lookup"><span data-stu-id="a88e3-104">The default password is **Password1**.</span></span>
3. <span data-ttu-id="a88e3-105">명령 프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a88e3-105">At the command prompt, type</span></span>
   
     `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="a88e3-106">유지 관리 모드에서는 모든 I/O 요청이 중단되며 Azure 클래식 포털에 대한 연결이 끊어짐을 알리는 경고 메시지와 확인 요청 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a88e3-106">You will see a warning message telling you that Maintenance mode will disrupt all I/O requests and sever the connection to the Azure classic portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="a88e3-107">**Y** 를 입력하여 유지 관리 모드를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a88e3-107">Type **Y** to enter Maintenance mode.</span></span>
   
    <span data-ttu-id="a88e3-108">두 컨트롤러가 모두 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="a88e3-108">Both controllers will restart.</span></span> <span data-ttu-id="a88e3-109">다시 시작이 완료되면 장치가 유지 관리 모드임을 나타내는 다른 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a88e3-109">When the restart is complete, another message will appear indicating that the device is in Maintenance mode.</span></span>

