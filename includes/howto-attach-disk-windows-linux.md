


## <a name="attach-an-empty-disk"></a><span data-ttu-id="3b2c3-101">빈 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="3b2c3-101">Attach an empty disk</span></span>
<span data-ttu-id="3b2c3-102">Azure가 .vhd 파일을 자동으로 만들어 저장소 계정에 저장하므로, 빈 디스크를 연결하는 것이 데이터 디스크를 추가하는 간단한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-102">Attaching an empty disk is a simple way to add a data disk, because Azure creates the .vhd file for you and stores it in the storage account.</span></span>

1. <span data-ttu-id="3b2c3-103">**가상 컴퓨터(클래식)**를 클릭한 다음 적절한 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-103">Click **Virtual Machines (classic)**, and then select the appropriate VM.</span></span>

2. <span data-ttu-id="3b2c3-104">설정 메뉴에서 **디스크**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-104">In the Settings menu, click **Disks**.</span></span>

   ![새로운 빈 디스크 연결](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. <span data-ttu-id="3b2c3-106">명령 모음에서 **새 연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-106">On the command bar, click **Attach new**.</span></span>  
    <span data-ttu-id="3b2c3-107">**새 디스크 연결** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-107">The **Attach new disk** dialog box appears.</span></span>

    ![새 디스크 연결](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    <span data-ttu-id="3b2c3-109">다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-109">Fill in the following information:</span></span>
    - <span data-ttu-id="3b2c3-110">**파일 이름**에서 기본 이름을 그대로 사용하거나 .vhd 파일에 대한 다른 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-110">In **File Name**, accept the default name or type another one for the .vhd file.</span></span> <span data-ttu-id="3b2c3-111">.vhd 파일용으로 다른 이름을 입력하는 경우에도 데이터 디스크는 자동으로 생성된 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-111">The data disk uses an automatically generated name, even if you type another name for the .vhd file.</span></span>
    - <span data-ttu-id="3b2c3-112">데이터 디스크의 **유형**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-112">Select the **Type** of the data disk.</span></span> <span data-ttu-id="3b2c3-113">모든 가상 컴퓨터에서 표준 디스크를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-113">All virtual machines support standard disks.</span></span> <span data-ttu-id="3b2c3-114">많은 가상 컴퓨터에서 프리미엄 디스크도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-114">Many virtual machines also support premium disks.</span></span>
    - <span data-ttu-id="3b2c3-115">데이터 디스크의 **크기(GB)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-115">Select the **Size (GB)** of the data disk.</span></span>
    - <span data-ttu-id="3b2c3-116">**호스트 캐싱**에 대해 없음 또는 읽기 전용을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-116">For **Host caching**, choose none or Read Only.</span></span>
    - <span data-ttu-id="3b2c3-117">[확인]을 클릭하여 마칩니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-117">Click OK to finish.</span></span>

4. <span data-ttu-id="3b2c3-118">데이터 디스크가 생성되어 연결된 후에는 VM의 디스크 섹션에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-118">After the data disk is created and attached, it's listed in the disks section of the VM.</span></span>

   ![새 빈 데이터 디스크가 성공적으로 연결됨](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> <span data-ttu-id="3b2c3-120">데이터 디스크를 추가한 후 VM에 로그온하여 디스크를 사용할 수 있도록 초기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-120">After you add a data disk, you need to log on to the VM and initialize the disk so that it can be used.</span></span>

## <a name="how-to-attach-an-existing-disk"></a><span data-ttu-id="3b2c3-121">방법: 기존 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="3b2c3-121">How to: Attach an existing disk</span></span>
<span data-ttu-id="3b2c3-122">기존 디스크를 연결하려면 저장소 계정에 사용 가능한 .vhd가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-122">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span> <span data-ttu-id="3b2c3-123">[Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet을 사용하여 .vhd 파일을 저장소 계정에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-123">Use the [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet to upload the .vhd file to the storage account.</span></span> <span data-ttu-id="3b2c3-124">.vhd 파일을 만들어 업로드한 후에는 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-124">After you've created and uploaded the .vhd file, you can attach it to a VM.</span></span>

1. <span data-ttu-id="3b2c3-125">**가상 컴퓨터(클래식)**를 클릭하고 해당 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-125">Click **Virtual Machines (classic)**, and then select the appropriate virtual machine.</span></span>

2. <span data-ttu-id="3b2c3-126">설정 메뉴에서 **디스크**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-126">In the Settings menu, click **Disks**.</span></span>

3. <span data-ttu-id="3b2c3-127">명령 모음에서 **기존 디스크 연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-127">On the command bar, click **Attach existing**.</span></span>

    ![데이터 디스크 연결](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. <span data-ttu-id="3b2c3-129">**위치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-129">Click **Location**.</span></span> <span data-ttu-id="3b2c3-130">사용 가능한 저장소 계정이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-130">The available storage accounts display.</span></span> <span data-ttu-id="3b2c3-131">다음으로 목록에서 해당 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-131">Next, select an appropriate storage account from those listed.</span></span>

    ![디스크 저장소 계정 제공](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. <span data-ttu-id="3b2c3-133">**저장소 계정**은 디스크 드라이브(vhds)가 있는 하나 이상의 컨테이너를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-133">A **Storage account** holds one or more containers that contain disk drives (vhds).</span></span> <span data-ttu-id="3b2c3-134">목록에서 해당 컨테이너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-134">Select the appropriate container from those listed.</span></span>

    ![virtual-machines-windows의 컨테이너 제공](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. <span data-ttu-id="3b2c3-136">**vhds** 패널에는 컨테이너에 있는 디스크 드라이브가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-136">The **vhds** panel lists the disk drives held in the container.</span></span> <span data-ttu-id="3b2c3-137">디스크 중 하나를 클릭한 후 [선택]을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-137">Click one of the disks, and then click Select.</span></span>

    ![virtual-machines-windows의 디스크 이미지 제공](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. <span data-ttu-id="3b2c3-139">저장소 계정, 컨테이너 및 가상 컴퓨터에 추가할 특정 하드 디스크(vhd)가 포함된 위치와 함께 **기존 디스크 연결** 패널이 다시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-139">The **Attach existing disk** panel displays again, with the location containing the storage account, container, and selected hard disk (vhd) to add to the virtual machine.</span></span>

  <span data-ttu-id="3b2c3-140">**호스트 캐싱**을 없음 또는 읽기 전용으로 설정한 후 [확인]을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c3-140">Set **Host caching** to none or Read only, then click OK.</span></span>

    ![데이터 디스크 연결됨](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
