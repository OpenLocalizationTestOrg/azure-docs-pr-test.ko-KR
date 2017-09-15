#### <a name="to-stop-and-start-a-cloud-appliance"></a><span data-ttu-id="57321-101">클라우드 어플라이언스를 중지 및 시작하려면</span><span class="sxs-lookup"><span data-stu-id="57321-101">To stop and start a cloud appliance</span></span>

1. <span data-ttu-id="57321-102">클라우드 어플라이언스를 중지하려면 클라우드 어플라이언스에 대한 VM으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="57321-102">To stop a cloud appliance, go to the VM for your cloud appliance.</span></span>
    <span data-ttu-id="57321-103">![StorSimple Cloud Appliance 가상 컴퓨터](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span><span class="sxs-lookup"><span data-stu-id="57321-103">![StorSimple Cloud Appliance Virtual Machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span></span>

2. <span data-ttu-id="57321-104">명령 모음에서 **중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57321-104">From the command bar, click **Stop**.</span></span>

    ![StorSimple Cloud Appliance 가상 컴퓨터](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. <span data-ttu-id="57321-106">확인하라는 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57321-106">When prompted for confirmation, click **Yes**.</span></span>

    ![StorSimple Cloud Appliance 가상 컴퓨터](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. <span data-ttu-id="57321-108">VM을 중지하면 할당 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="57321-108">When you stop a VM, it gets deallocated.</span></span> <span data-ttu-id="57321-109">클라우드 어플라이언스를 중지하는 동안에는 상태가 **할당 취소 중**입니다.</span><span class="sxs-lookup"><span data-stu-id="57321-109">While the cloud appliance is stopping, its status is **Deallocating**.</span></span> <span data-ttu-id="57321-110">클라우드 어플라이언스를 중지한 후에는 상태가 **중지됨(할당 취소됨)**입니다.</span><span class="sxs-lookup"><span data-stu-id="57321-110">After the cloud appliance is stopped, its status is **Stopped (deallocated)**.</span></span>

    ![StorSimple Cloud Appliance 가상 컴퓨터](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. <span data-ttu-id="57321-112">VM이 중지되면 **시작**(단추를 사용할 수 있게 됨)을 클릭하여 VM을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="57321-112">Once a VM is stopped, click **Start** (button becomes available) to start the VM.</span></span> <span data-ttu-id="57321-113">클라우드 어플라이언스가 시작되면 상태는 **시작됨**입니다.</span><span class="sxs-lookup"><span data-stu-id="57321-113">After the cloud appliance has started up, its status is **Started**.</span></span>

    ![StorSimple Cloud Appliance 가상 컴퓨터](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

<span data-ttu-id="57321-115">다음 cmdlet을 사용하여 클라우드 어플라이언스를 중지했다가 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="57321-115">Use the following cmdlets to stop and start a cloud appliance.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="to-restart-a-cloud-appliance"></a><span data-ttu-id="57321-116">클라우드 어플라이언스를 다시 시작하려면</span><span class="sxs-lookup"><span data-stu-id="57321-116">To restart a cloud appliance</span></span>

<span data-ttu-id="57321-117">클라우드 어플라이언스를 다시 시작하려면 클라우드 어플라이언스에 대한 VM으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="57321-117">To restart a cloud appliance, go to the VM for your cloud appliance.</span></span> <span data-ttu-id="57321-118">명령 모음에서 **다시 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57321-118">From the command bar, click **Restart**.</span></span> <span data-ttu-id="57321-119">메시지가 표시되면 다시 시작을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="57321-119">When prompted, confirm the restart.</span></span> <span data-ttu-id="57321-120">클라우드 어플라이언스를 사용할 준비가 되면 상태는 **실행 중**입니다.</span><span class="sxs-lookup"><span data-stu-id="57321-120">When the cloud appliance is ready for you to use, its status is **Running**.</span></span>

![StorSimple Cloud Appliance 가상 컴퓨터](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

<span data-ttu-id="57321-122">다음 cmdlet을 사용하여 클라우드 어플라이언스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="57321-122">Use the following cmdlet to restart a cloud appliance.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

