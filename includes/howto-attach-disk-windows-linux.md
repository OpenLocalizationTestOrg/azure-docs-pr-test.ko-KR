


## <a name="attach-an-empty-disk"></a><span data-ttu-id="e9819-101">빈 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="e9819-101">Attach an empty disk</span></span>
<span data-ttu-id="e9819-102">Azure hello.vhd 파일을 만들어 드립니다 및 hello 저장소 계정에 저장 하기 때문에 데이터 디스크는 간단한 방법을 tooadd를은 빈 디스크를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-102">Attaching an empty disk is a simple way tooadd a data disk, because Azure creates hello .vhd file for you and stores it in hello storage account.</span></span>

1. <span data-ttu-id="e9819-103">클릭 **가상 컴퓨터 (클래식)**, 다음 선택 hello 적절 한 VM 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-103">Click **Virtual Machines (classic)**, and then select hello appropriate VM.</span></span>

2. <span data-ttu-id="e9819-104">Hello 설정 메뉴를 클릭 **디스크**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-104">In hello Settings menu, click **Disks**.</span></span>

   ![새로운 빈 디스크 연결](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. <span data-ttu-id="e9819-106">Hello 명령 모음에서 **새 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-106">On hello command bar, click **Attach new**.</span></span>  
    <span data-ttu-id="e9819-107">hello **새 디스크 연결** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-107">hello **Attach new disk** dialog box appears.</span></span>

    ![새 디스크 연결](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    <span data-ttu-id="e9819-109">Hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-109">Fill in hello following information:</span></span>
    - <span data-ttu-id="e9819-110">**파일 이름**hello 기본 이름을 그대로 사용 하거나 hello.vhd 파일에 대해 다른 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-110">In **File Name**, accept hello default name or type another one for hello .vhd file.</span></span> <span data-ttu-id="e9819-111">hello 데이터 디스크는 hello.vhd 파일에 다른 이름을 입력 하는 경우에 자동으로 생성 된 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-111">hello data disk uses an automatically generated name, even if you type another name for hello .vhd file.</span></span>
    - <span data-ttu-id="e9819-112">선택 hello **형식** hello 데이터 디스크의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-112">Select hello **Type** of hello data disk.</span></span> <span data-ttu-id="e9819-113">모든 가상 컴퓨터에서 표준 디스크를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-113">All virtual machines support standard disks.</span></span> <span data-ttu-id="e9819-114">많은 가상 컴퓨터에서 프리미엄 디스크도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-114">Many virtual machines also support premium disks.</span></span>
    - <span data-ttu-id="e9819-115">선택 hello **크기 (GB)** hello 데이터 디스크의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-115">Select hello **Size (GB)** of hello data disk.</span></span>
    - <span data-ttu-id="e9819-116">**호스트 캐싱**에 대해 없음 또는 읽기 전용을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-116">For **Host caching**, choose none or Read Only.</span></span>
    - <span data-ttu-id="e9819-117">Toofinish 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-117">Click OK toofinish.</span></span>

4. <span data-ttu-id="e9819-118">Hello 데이터 디스크를 만들고 연결 된 후 hello VM의 hello 디스크 섹션에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-118">After hello data disk is created and attached, it's listed in hello disks section of hello VM.</span></span>

   ![새 빈 데이터 디스크가 성공적으로 연결됨](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> <span data-ttu-id="e9819-120">데이터 디스크를 추가한 후 toolog toohello VM에 필요 하 고 사용할 수 있도록 hello 디스크를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-120">After you add a data disk, you need toolog on toohello VM and initialize hello disk so that it can be used.</span></span>

## <a name="how-to-attach-an-existing-disk"></a><span data-ttu-id="e9819-121">방법: 기존 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="e9819-121">How to: Attach an existing disk</span></span>
<span data-ttu-id="e9819-122">기존 디스크를 연결하려면 저장소 계정에 사용 가능한 .vhd가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-122">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span> <span data-ttu-id="e9819-123">사용 하 여 hello [Add-azurevhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet tooupload hello.vhd 파일 toohello 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-123">Use hello [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet tooupload hello .vhd file toohello storage account.</span></span> <span data-ttu-id="e9819-124">만든 hello.vhd 파일을 업로드 한 후 VM tooa를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-124">After you've created and uploaded hello .vhd file, you can attach it tooa VM.</span></span>

1. <span data-ttu-id="e9819-125">클릭 **가상 컴퓨터 (클래식)**, 다음 선택 hello 적절 한 가상 컴퓨터 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-125">Click **Virtual Machines (classic)**, and then select hello appropriate virtual machine.</span></span>

2. <span data-ttu-id="e9819-126">Hello 설정 메뉴를 클릭 **디스크**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-126">In hello Settings menu, click **Disks**.</span></span>

3. <span data-ttu-id="e9819-127">Hello 명령 모음에서 **연결 기존**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-127">On hello command bar, click **Attach existing**.</span></span>

    ![데이터 디스크 연결](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. <span data-ttu-id="e9819-129">**위치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-129">Click **Location**.</span></span> <span data-ttu-id="e9819-130">hello 사용 가능한 저장소 계정을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-130">hello available storage accounts display.</span></span> <span data-ttu-id="e9819-131">다음으로 목록에서 해당 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-131">Next, select an appropriate storage account from those listed.</span></span>

    ![디스크 저장소 계정 제공](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. <span data-ttu-id="e9819-133">**저장소 계정**은 디스크 드라이브(vhds)가 있는 하나 이상의 컨테이너를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-133">A **Storage account** holds one or more containers that contain disk drives (vhds).</span></span> <span data-ttu-id="e9819-134">나열 된 hello 적절 한 컨테이너를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-134">Select hello appropriate container from those listed.</span></span>

    ![virtual-machines-windows의 컨테이너 제공](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. <span data-ttu-id="e9819-136">hello **vhd** 패널 hello 컨테이너에서 hello 디스크 드라이브를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-136">hello **vhds** panel lists hello disk drives held in hello container.</span></span> <span data-ttu-id="e9819-137">Hello 디스크 중 하나를 클릭 하 고 선택을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-137">Click one of hello disks, and then click Select.</span></span>

    ![virtual-machines-windows의 디스크 이미지 제공](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. <span data-ttu-id="e9819-139">hello **기존 디스크 연결** hello 저장소 계정, 컨테이너 및 선택한 하드 디스크 (vhd) tooadd toohello 가상 컴퓨터를 포함 하는 hello 위치와 패널 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-139">hello **Attach existing disk** panel displays again, with hello location containing hello storage account, container, and selected hard disk (vhd) tooadd toohello virtual machine.</span></span>

  <span data-ttu-id="e9819-140">설정 **호스트 캐싱** toonone 또는 읽기 전용 다음 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9819-140">Set **Host caching** toonone or Read only, then click OK.</span></span>

    ![데이터 디스크 연결됨](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
