


<span data-ttu-id="a7873-101">가용성 집합을 사용하면 유지 관리 중과 같은 가동 중지 시간 동안에도 가상 컴퓨터를 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-101">An availability set helps keep your virtual machines available during downtime, such as during maintenance.</span></span> <span data-ttu-id="a7873-102">가용성 집합 내에 비슷하게 구성된 둘 이상의 가상 컴퓨터를 배치하면 가상 컴퓨터가 실행하는 서비스나 응용 프로그램의 가용성을 유지하는 데 필요한 중복성이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-102">Placing two or more similarly configured virtual machines in an availability set creates the redundancy needed to maintain availability of the applications or services that your virtual machine runs.</span></span> <span data-ttu-id="a7873-103">이 기능이 작동하는 방식에 대한 자세한 내용은 [가상 컴퓨터의 가용성 관리][Manage the availability of virtual machines]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7873-103">For details about how this works, see [Manage the availability of virtual machines][Manage the availability of virtual machines].</span></span>

<span data-ttu-id="a7873-104">응용 프로그램을 항상 사용 가능한 상태로 유지하고 효과적으로 실행하려면 가용성 집합과 부하 분산 끝점을 함께 사용하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-104">It's a best practice to use both availability sets and load-balancing endpoints to help ensure that your application is always available and running efficiently.</span></span> <span data-ttu-id="a7873-105">부하가 분산된 끝점에 대한 자세한 내용은 [Azure 인프라 서비스를 위한 부하 분산][Load balancing for Azure infrastructure services]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7873-105">For details about load-balanced endpoints, see [Load balancing for Azure infrastructure services][Load balancing for Azure infrastructure services].</span></span>

<span data-ttu-id="a7873-106">다음 두 옵션 중 하나를 사용하여 클래식 가상 컴퓨터를 가용성 집합에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-106">You can add classic virtual machines into an availability set by using one of two options:</span></span>

* <span data-ttu-id="a7873-107">[옵션 1: 동시에 가상 컴퓨터 및 가용성 집합 만들기][Option 1: Create a virtual machine and an availability set at the same time]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7873-107">[Option 1: Create a virtual machine and an availability set at the same time][Option 1: Create a virtual machine and an availability set at the same time].</span></span> <span data-ttu-id="a7873-108">그런 다음 새 가상 컴퓨터를 만들 때 집합에 가상 컴퓨터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-108">Then, add new virtual machines to the set when you create those virtual machines.</span></span>
* <span data-ttu-id="a7873-109">[옵션 2: 기존 가상 컴퓨터를 가용성 집합에 추가][Option 2: Add an existing virtual machine to an availability set]</span><span class="sxs-lookup"><span data-stu-id="a7873-109">[Option 2: Add an existing virtual machine to an availability set][Option 2: Add an existing virtual machine to an availability set].</span></span>

> [!NOTE]
> <span data-ttu-id="a7873-110">클래식 모델에서는 같은 가용성 집합에 배치할 가상 컴퓨터는 같은 클라우드 서비스에 속해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-110">In the classic model, virtual machines that you want to put in the same availability set must belong to the same cloud service.</span></span>
> 
> 

## <span data-ttu-id="a7873-111"><a id="createset"> </a>옵션 1: 동시에 가상 컴퓨터 및 가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="a7873-111"><a id="createset"> </a>Option 1: Create a virtual machine and an availability set at the same time</span></span>
<span data-ttu-id="a7873-112">Azure 포털 또는 Azure PowerShell 명령을 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-112">You can use either the Azure portal or Azure PowerShell commands to do this.</span></span>

<span data-ttu-id="a7873-113">Azure 포털을 사용하려면</span><span class="sxs-lookup"><span data-stu-id="a7873-113">To use the Azure portal:</span></span>

1. <span data-ttu-id="a7873-114">아직 로그인하지 않은 경우 [Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-114">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a7873-115">허브 메뉴에서 **+ 새로 만들기**를 클릭한 다음 **가상 컴퓨터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-115">On the hub menu, click **+ New**, and then click **Virtual Machine**.</span></span>
   
    ![대체 이미지 텍스트](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. <span data-ttu-id="a7873-117">사용하려는 마켓플레이스 가상 컴퓨터 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-117">Select the Marketplace virtual machine image you wish to use.</span></span> <span data-ttu-id="a7873-118">Linux 또는 Windows 가상 컴퓨터를 만들도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-118">You can choose to create a Linux or Windows virtual machine.</span></span>
4. <span data-ttu-id="a7873-119">선택한 가상 컴퓨터에 대해 배포 모델이 **클래식**으로 설정되어 있는지 확인한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-119">For the selected virtual machine, verify that the deployment model is set to **Classic** and then click **Create**</span></span>
   
    ![대체 이미지 텍스트](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. <span data-ttu-id="a7873-121">가상 컴퓨터 이름, 사용자 이름 및 암호(Window 컴퓨터) 또는 SSH 공개 키(Linux 컴퓨터)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-121">Enter a virtual machine name, user name and password (for Windows machines) or SSH public key (for Linux machines).</span></span> 
6. <span data-ttu-id="a7873-122">VM 크기를 선택하고 **선택** 을 클릭하여 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-122">Choose the VM size and then click **Select** to continue.</span></span>
7. <span data-ttu-id="a7873-123">**선택적 구성 > 가용성 집합**을 선택하고 가상 컴퓨터를 추가하려는 가용성 집합을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-123">Choose **Optional Configuration > Availability set**, and select the availability set you wish to add the virtual machine to.</span></span>
   
    ![대체 이미지 텍스트](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. <span data-ttu-id="a7873-125">구성 설정을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-125">Review your configuration settings.</span></span> <span data-ttu-id="a7873-126">완료하면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-126">When you're done, click **Create**.</span></span>
9. <span data-ttu-id="a7873-127">Azure에서 가상 컴퓨터를 만드는 동안 허브 메뉴의 **가상 컴퓨터** 에서 진행 상황을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-127">While Azure creates your virtual machine, you can track the progress under **Virtual Machines** in the hub menu.</span></span>

<span data-ttu-id="a7873-128">Azure PowerShell 명령을 사용하여 Azure 가상 컴퓨터를 만들고 새로운 또는 기존 가용성 집합에 추가하려면 [Azure PowerShell을 사용하여 Windows 기반 가상 컴퓨터 만들기 및 미리 구성](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="a7873-128">To use Azure PowerShell commands to create an Azure virtual machine and add it to a new or existing availability set, see [Use Azure PowerShell to create and preconfigure Windows-based virtual machines](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="a7873-129"><a id="addmachine"> </a>옵션 2: 기존 가상 컴퓨터를 가용성 집합에 추가</span><span class="sxs-lookup"><span data-stu-id="a7873-129"><a id="addmachine"> </a>Option 2: Add an existing virtual machine to an availability set</span></span>
<span data-ttu-id="a7873-130">Azure 포털에서 기존 클래식 가상 컴퓨터를 기존 가용성 집합에 추가하거나 가상 컴퓨터용으로 새 가용성 집합을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-130">In the Azure portal, you can add existing classic virtual machines to an existing availability set or create a new one for them.</span></span> <span data-ttu-id="a7873-131">동일한 가용성 집합의 가상 컴퓨터는 같은 클라우드 서비스에 속해야 합니다. 이 옵션에서도 단계는 거의 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-131">(Keep in mind that the virtual machines in the same availability set must belong to the same cloud service.) The steps are almost the same.</span></span> <span data-ttu-id="a7873-132">Azure PowerShell에서 기존 가용성 집합에 가상 컴퓨터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-132">With Azure PowerShell, you can add the virtual machine to an existing availability set.</span></span>

1. <span data-ttu-id="a7873-133">아직 로그인하지 않은 경우 [Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-133">If you have not already done so, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a7873-134">허브 메뉴에서 **가상 컴퓨터(클래식)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-134">On the Hub menu, click **Virtual Machines (classic)**.</span></span>
   
    ![대체 이미지 텍스트](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. <span data-ttu-id="a7873-136">가상 컴퓨터 목록에서 집합에 추가할 가상 컴퓨터 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-136">From the list of virtual machines, select the name of the virtual machine that you want to add to the set.</span></span>
4. <span data-ttu-id="a7873-137">가상 컴퓨터 **설정**에서 **가용성 집합**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-137">Choose **Availability set** from the virtual machine **Settings**.</span></span>
   
    ![대체 이미지 텍스트](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. <span data-ttu-id="a7873-139">가상 컴퓨터를 추가하려는 가용성 집합을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-139">Select the availability set you wish to add the virtual machine to.</span></span> <span data-ttu-id="a7873-140">가상 컴퓨터는 가용성 집합과 동일한 클라우드 서비스에 속해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-140">The virtual machine must belong to the same cloud service as the availability set.</span></span>
   
    ![대체 이미지 텍스트](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. <span data-ttu-id="a7873-142">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-142">Click **Save**.</span></span>

<span data-ttu-id="a7873-143">Azure PowerShell 명령을 사용하려면 관리자 수준의 Azure PowerShell 세션을 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-143">To use Azure PowerShell commands, open an administrator-level Azure PowerShell session and run the following command.</span></span> <span data-ttu-id="a7873-144">자리 표시자(예: &lt;VmCloudServiceName&gt;)의 경우 < 및 > 문자를 포함하여 따옴표 안의 모든 항목을 올바른 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-144">For the placeholders (such as &lt;VmCloudServiceName&gt;), replace everything within the quotes, including the < and > characters, with the correct names.</span></span>

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> <span data-ttu-id="a7873-145">가용성 집합에 추가하는 작업을 완료하기 위해 가상 컴퓨터를 다시 시작해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7873-145">The virtual machine might have to be restarted to finish adding it to the availability set.</span></span>
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at the same time]: #createset
[Option 2: Add an existing virtual machine to an availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage the availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

