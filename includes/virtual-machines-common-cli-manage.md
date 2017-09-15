<span data-ttu-id="29cfc-101">Azure CLI 2.0을 사용하면 macOS, Linux 및 Windows에서 Azure 리소스를 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-101">The Azure CLI 2.0 allows you to create and manage your Azure resources on macOS, Linux, and Windows.</span></span> <span data-ttu-id="29cfc-102">이 문서에서는 VM(가상 컴퓨터)을 만들고 관리하는 가장 일반적인 몇 가지 명령에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-102">This article details some of the most common commands to create and manage virtual machines (VMs).</span></span>

<span data-ttu-id="29cfc-103">이 문서에는 Azure CLI 버전 2.0.4 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-103">This article requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="29cfc-104">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-104">Run `az --version` to find the version.</span></span> <span data-ttu-id="29cfc-105">업그레이드해야 하는 경우 [Azure CLI 2.0 설치](/cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29cfc-105">If you need to upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="29cfc-106">브라우저에서 [Cloud Shell](/azure/cloud-shell/quickstart)을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-106">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a><span data-ttu-id="29cfc-107">Azure CLI의 기본 Azure Resource Manager 명령</span><span class="sxs-lookup"><span data-stu-id="29cfc-107">Basic Azure Resource Manager commands in Azure CLI</span></span>
<span data-ttu-id="29cfc-108">특정 명령줄 스위치와 옵션에 대해 자세한 도움말은 `az <command> <subcommand> --help`를 입력하여 온라인 명령 도움말과 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29cfc-108">For more detailed help with specific command line switches and options, you can use the online command help and options by typing `az <command> <subcommand> --help`.</span></span>

### <a name="create-vms"></a><span data-ttu-id="29cfc-109">VM 만들기</span><span class="sxs-lookup"><span data-stu-id="29cfc-109">Create VMs</span></span>
| <span data-ttu-id="29cfc-110">작업</span><span class="sxs-lookup"><span data-stu-id="29cfc-110">Task</span></span> | <span data-ttu-id="29cfc-111">Azure CLI 명령</span><span class="sxs-lookup"><span data-stu-id="29cfc-111">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="29cfc-112">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="29cfc-112">Create a resource group</span></span> | `az group create --name myResourceGroup --location eastus` |
| <span data-ttu-id="29cfc-113">Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="29cfc-113">Create a Linux VM</span></span> | `az vm create --resource-group myResourceGroup --name myVM --image ubuntults` |
| <span data-ttu-id="29cfc-114">Windows VM 만들기</span><span class="sxs-lookup"><span data-stu-id="29cfc-114">Create a Windows VM</span></span> | `az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter` |

### <a name="manage-vm-state"></a><span data-ttu-id="29cfc-115">VM 상태 관리</span><span class="sxs-lookup"><span data-stu-id="29cfc-115">Manage VM state</span></span>
| <span data-ttu-id="29cfc-116">작업</span><span class="sxs-lookup"><span data-stu-id="29cfc-116">Task</span></span> | <span data-ttu-id="29cfc-117">Azure CLI 명령</span><span class="sxs-lookup"><span data-stu-id="29cfc-117">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="29cfc-118">VM 시작</span><span class="sxs-lookup"><span data-stu-id="29cfc-118">Start a VM</span></span> | `az vm start --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="29cfc-119">VM 중지</span><span class="sxs-lookup"><span data-stu-id="29cfc-119">Stop a VM</span></span> | `az vm stop --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="29cfc-120">VM 할당 취소</span><span class="sxs-lookup"><span data-stu-id="29cfc-120">Deallocate a VM</span></span> | `az vm deallocate --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="29cfc-121">VM 다시 시작</span><span class="sxs-lookup"><span data-stu-id="29cfc-121">Restart a VM</span></span> | `az vm restart --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="29cfc-122">VM 재배포</span><span class="sxs-lookup"><span data-stu-id="29cfc-122">Redeploy a VM</span></span> | `az vm redeploy --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="29cfc-123">VM 삭제</span><span class="sxs-lookup"><span data-stu-id="29cfc-123">Delete a VM</span></span> | `az vm delete --resource-group myResourceGroup --name myVM` |

### <a name="get-vm-info"></a><span data-ttu-id="29cfc-124">VM 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="29cfc-124">Get VM info</span></span>
| <span data-ttu-id="29cfc-125">작업</span><span class="sxs-lookup"><span data-stu-id="29cfc-125">Task</span></span> | <span data-ttu-id="29cfc-126">Azure CLI 명령</span><span class="sxs-lookup"><span data-stu-id="29cfc-126">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="29cfc-127">VM 나열</span><span class="sxs-lookup"><span data-stu-id="29cfc-127">List VMs</span></span> | `az vm list` |
| <span data-ttu-id="29cfc-128">VM 관련 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="29cfc-128">Get information about a VM</span></span> | `az vm show --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="29cfc-129">VM 리소스 사용</span><span class="sxs-lookup"><span data-stu-id="29cfc-129">Get usage of VM resources</span></span> | `az vm list-usage --location eastus` |
| <span data-ttu-id="29cfc-130">모든 사용 가능한 VM 크기 가져오기</span><span class="sxs-lookup"><span data-stu-id="29cfc-130">Get all available VM sizes</span></span> | `az vm list-sizes --location eastus` |

## <a name="disks-and-images"></a><span data-ttu-id="29cfc-131">디스크 및 이미지</span><span class="sxs-lookup"><span data-stu-id="29cfc-131">Disks and images</span></span>
| <span data-ttu-id="29cfc-132">작업</span><span class="sxs-lookup"><span data-stu-id="29cfc-132">Task</span></span> | <span data-ttu-id="29cfc-133">Azure CLI 명령</span><span class="sxs-lookup"><span data-stu-id="29cfc-133">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="29cfc-134">VM에 데이터 디스크 추가</span><span class="sxs-lookup"><span data-stu-id="29cfc-134">Add a data disk to a VM</span></span> | `az vm disk attach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk --size-gb 128 --new ` |
| <span data-ttu-id="29cfc-135">VM에서 데이터 디스크 제거</span><span class="sxs-lookup"><span data-stu-id="29cfc-135">Remove a data disk from a VM</span></span> | `az vm disk detach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk` |
| <span data-ttu-id="29cfc-136">디스크 크기 조정</span><span class="sxs-lookup"><span data-stu-id="29cfc-136">Resize a disk</span></span> | `az disk update --resource-group myResourceGroup --name myDataDisk --size-gb 256` |
| <span data-ttu-id="29cfc-137">디스크 스냅숏</span><span class="sxs-lookup"><span data-stu-id="29cfc-137">Snapshot a disk</span></span> | `az snapshot create --resource-group myResourceGroup --name mySnapshot --source myDataDisk` |
| <span data-ttu-id="29cfc-138">VM 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="29cfc-138">Create image of a VM</span></span> | `az image create --resource-group myResourceGroup --source myVM --name myImage` |
| <span data-ttu-id="29cfc-139">이미지에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="29cfc-139">Create VM from image</span></span> | `az vm create --resource-group myResourceGroup --name myNewVM --image myImage` |


## <a name="next-steps"></a><span data-ttu-id="29cfc-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="29cfc-140">Next steps</span></span>
<span data-ttu-id="29cfc-141">CLI 명령의 추가 예제는 [Azure CLI를 사용하여 Linux VM 만들기 및 관리](../articles/virtual-machines/linux/tutorial-manage-vm.md) 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29cfc-141">For additional examples of the CLI commands, see the [Create and Manage Linux VMs with the Azure CLI](../articles/virtual-machines/linux/tutorial-manage-vm.md) tutorial.</span></span>

