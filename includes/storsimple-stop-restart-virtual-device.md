#### <a name="toostop-and-start-a-virtual-device"></a><span data-ttu-id="8b213-101">toostop 및 가상 장치 시작</span><span class="sxs-lookup"><span data-stu-id="8b213-101">toostop and start a virtual device</span></span>
<span data-ttu-id="8b213-102">가상 장치 toostop 해당 이름을 클릭 하 고 클릭 **종료**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b213-102">toostop a virtual device, click its name, and then click **Shutdown**.</span></span> <span data-ttu-id="8b213-103">상태는 hello 가상 장치를 종료 하는 동안 **중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b213-103">While hello virtual device is shutting down, its status is **Stopping**.</span></span> <span data-ttu-id="8b213-104">가상 장치 hello 중지 된 후에 상태가 **Stopped**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b213-104">After hello virtual device is stopped, its status is **Stopped**.</span></span>

<span data-ttu-id="8b213-105">다음 cmdlet toostop hello를 사용 하 고 가상 장치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b213-105">Use hello following cmdlets toostop and start a virtual device.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-virtual-device"></a><span data-ttu-id="8b213-106">toorestart 가상 장치</span><span class="sxs-lookup"><span data-stu-id="8b213-106">toorestart a virtual device</span></span>
<span data-ttu-id="8b213-107">가상 장치가 실행 되 고 toorestart 원하는 해당 이름을 클릭 한 다음 클릭 **다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b213-107">When a virtual device is running and you want toorestart it, click its name, and then click **Restart**.</span></span> <span data-ttu-id="8b213-108">상태는 hello 가상 장치를 다시 시작 하는 동안 **를 다시 설치 하면**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b213-108">While hello virtual device is restarting, its status is **Restarting**.</span></span> <span data-ttu-id="8b213-109">상태는 hello 가상 장치 toouse 있습니다에 대 한 준비 되 면 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b213-109">When hello virtual device is ready for you toouse, its status is **Running**.</span></span>

<span data-ttu-id="8b213-110">다음 cmdlet toorestart 가상 장치 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b213-110">Use hello following cmdlet toorestart a virtual device.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

