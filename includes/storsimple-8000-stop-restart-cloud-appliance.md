#### <a name="toostop-and-start-a-cloud-appliance"></a><span data-ttu-id="47be8-101">toostop 및 클라우드 어플라이언스에 시작</span><span class="sxs-lookup"><span data-stu-id="47be8-101">toostop and start a cloud appliance</span></span>

1. <span data-ttu-id="47be8-102">클라우드 어플라이언스에 toostop toohello VM 클라우드 장비에 대 한 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="47be8-102">toostop a cloud appliance, go toohello VM for your cloud appliance.</span></span>
    <span data-ttu-id="47be8-103">![StorSimple Cloud Appliance 가상 컴퓨터](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span><span class="sxs-lookup"><span data-stu-id="47be8-103">![StorSimple Cloud Appliance Virtual Machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span></span>

2. <span data-ttu-id="47be8-104">Hello 명령 모음에서 클릭 **중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="47be8-104">From hello command bar, click **Stop**.</span></span>

    ![StorSimple Cloud Appliance 가상 컴퓨터](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. <span data-ttu-id="47be8-106">확인하라는 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47be8-106">When prompted for confirmation, click **Yes**.</span></span>

    ![StorSimple Cloud Appliance 가상 컴퓨터](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. <span data-ttu-id="47be8-108">VM을 중지하면 할당 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="47be8-108">When you stop a VM, it gets deallocated.</span></span> <span data-ttu-id="47be8-109">상태는 hello 클라우드 장비를 중지 하는 동안 **Deallocating**합니다.</span><span class="sxs-lookup"><span data-stu-id="47be8-109">While hello cloud appliance is stopping, its status is **Deallocating**.</span></span> <span data-ttu-id="47be8-110">Hello 클라우드 어플라이언스에 중지 된 후에 상태가 **중지 됨 (할당 취소 됨)**합니다.</span><span class="sxs-lookup"><span data-stu-id="47be8-110">After hello cloud appliance is stopped, its status is **Stopped (deallocated)**.</span></span>

    ![StorSimple Cloud Appliance 가상 컴퓨터](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. <span data-ttu-id="47be8-112">VM 중지 되 고 나면 클릭 **시작** (단추를 사용할 수) toostart hello VM입니다.</span><span class="sxs-lookup"><span data-stu-id="47be8-112">Once a VM is stopped, click **Start** (button becomes available) toostart hello VM.</span></span> <span data-ttu-id="47be8-113">Hello 클라우드 장비 시작 된 후에 상태가 **Started**합니다.</span><span class="sxs-lookup"><span data-stu-id="47be8-113">After hello cloud appliance has started up, its status is **Started**.</span></span>

    ![StorSimple Cloud Appliance 가상 컴퓨터](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

<span data-ttu-id="47be8-115">다음 cmdlet toostop hello를 사용 하 고 클라우드 장비를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="47be8-115">Use hello following cmdlets toostop and start a cloud appliance.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-cloud-appliance"></a><span data-ttu-id="47be8-116">클라우드 어플라이언스에 toorestart</span><span class="sxs-lookup"><span data-stu-id="47be8-116">toorestart a cloud appliance</span></span>

<span data-ttu-id="47be8-117">클라우드 어플라이언스에 toorestart toohello VM 클라우드 장비에 대 한 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="47be8-117">toorestart a cloud appliance, go toohello VM for your cloud appliance.</span></span> <span data-ttu-id="47be8-118">Hello 명령 모음에서 클릭 **다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="47be8-118">From hello command bar, click **Restart**.</span></span> <span data-ttu-id="47be8-119">메시지가 표시 되 면 hello를 다시 시작을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="47be8-119">When prompted, confirm hello restart.</span></span> <span data-ttu-id="47be8-120">상태는 hello 클라우드 어플라이언스에 toouse 있습니다에 대 한 준비 되 면 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="47be8-120">When hello cloud appliance is ready for you toouse, its status is **Running**.</span></span>

![StorSimple Cloud Appliance 가상 컴퓨터](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

<span data-ttu-id="47be8-122">다음 cmdlet toorestart 클라우드 어플라이언스에 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="47be8-122">Use hello following cmdlet toorestart a cloud appliance.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

