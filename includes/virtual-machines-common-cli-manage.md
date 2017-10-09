<span data-ttu-id="50949-101">hello Azure CLI 2.0 toocreate 있으며 macOS, Linux 및 Windows에서 Azure 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="50949-101">hello Azure CLI 2.0 allows you toocreate and manage your Azure resources on macOS, Linux, and Windows.</span></span> <span data-ttu-id="50949-102">이 문서는 가장 일반적인 명령 toocreate hello 중 일부에 대해 자세히 설명 하 고 가상 컴퓨터 (Vm)를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="50949-102">This article details some of hello most common commands toocreate and manage virtual machines (VMs).</span></span>

<span data-ttu-id="50949-103">이 문서는 hello Azure CLI 버전 2.0.4 필요 이상.</span><span class="sxs-lookup"><span data-stu-id="50949-103">This article requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="50949-104">실행 `az --version` toofind hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="50949-104">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="50949-105">Tooupgrade 필요한 경우 참조 [Azure CLI 2.0 설치](/cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="50949-105">If you need tooupgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="50949-106">또한 브라우저에서 [Cloud Shell](/azure/cloud-shell/quickstart)을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50949-106">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a><span data-ttu-id="50949-107">Azure CLI의 기본 Azure Resource Manager 명령</span><span class="sxs-lookup"><span data-stu-id="50949-107">Basic Azure Resource Manager commands in Azure CLI</span></span>
<span data-ttu-id="50949-108">Hello 온라인 명령 도움말 및 옵션을 입력 하 여 사용할 수 특정 명령줄 스위치 및 옵션에 대 한 도움 자세한 `az <command> <subcommand> --help`합니다.</span><span class="sxs-lookup"><span data-stu-id="50949-108">For more detailed help with specific command line switches and options, you can use hello online command help and options by typing `az <command> <subcommand> --help`.</span></span>

### <a name="create-vms"></a><span data-ttu-id="50949-109">VM 만들기</span><span class="sxs-lookup"><span data-stu-id="50949-109">Create VMs</span></span>
| <span data-ttu-id="50949-110">작업</span><span class="sxs-lookup"><span data-stu-id="50949-110">Task</span></span> | <span data-ttu-id="50949-111">Azure CLI 명령</span><span class="sxs-lookup"><span data-stu-id="50949-111">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="50949-112">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="50949-112">Create a resource group</span></span> | `az group create --name myResourceGroup --location eastus` |
| <span data-ttu-id="50949-113">Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="50949-113">Create a Linux VM</span></span> | `az vm create --resource-group myResourceGroup --name myVM --image ubuntults` |
| <span data-ttu-id="50949-114">Windows VM 만들기</span><span class="sxs-lookup"><span data-stu-id="50949-114">Create a Windows VM</span></span> | `az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter` |

### <a name="manage-vm-state"></a><span data-ttu-id="50949-115">VM 상태 관리</span><span class="sxs-lookup"><span data-stu-id="50949-115">Manage VM state</span></span>
| <span data-ttu-id="50949-116">작업</span><span class="sxs-lookup"><span data-stu-id="50949-116">Task</span></span> | <span data-ttu-id="50949-117">Azure CLI 명령</span><span class="sxs-lookup"><span data-stu-id="50949-117">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="50949-118">VM 시작</span><span class="sxs-lookup"><span data-stu-id="50949-118">Start a VM</span></span> | `az vm start --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="50949-119">VM 중지</span><span class="sxs-lookup"><span data-stu-id="50949-119">Stop a VM</span></span> | `az vm stop --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="50949-120">VM 할당 취소</span><span class="sxs-lookup"><span data-stu-id="50949-120">Deallocate a VM</span></span> | `az vm deallocate --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="50949-121">VM 다시 시작</span><span class="sxs-lookup"><span data-stu-id="50949-121">Restart a VM</span></span> | `az vm restart --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="50949-122">VM 재배포</span><span class="sxs-lookup"><span data-stu-id="50949-122">Redeploy a VM</span></span> | `az vm redeploy --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="50949-123">VM 삭제</span><span class="sxs-lookup"><span data-stu-id="50949-123">Delete a VM</span></span> | `az vm delete --resource-group myResourceGroup --name myVM` |

### <a name="get-vm-info"></a><span data-ttu-id="50949-124">VM 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="50949-124">Get VM info</span></span>
| <span data-ttu-id="50949-125">작업</span><span class="sxs-lookup"><span data-stu-id="50949-125">Task</span></span> | <span data-ttu-id="50949-126">Azure CLI 명령</span><span class="sxs-lookup"><span data-stu-id="50949-126">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="50949-127">VM 나열</span><span class="sxs-lookup"><span data-stu-id="50949-127">List VMs</span></span> | `az vm list` |
| <span data-ttu-id="50949-128">VM 관련 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="50949-128">Get information about a VM</span></span> | `az vm show --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="50949-129">VM 리소스 사용</span><span class="sxs-lookup"><span data-stu-id="50949-129">Get usage of VM resources</span></span> | `az vm list-usage --location eastus` |
| <span data-ttu-id="50949-130">모든 사용 가능한 VM 크기 가져오기</span><span class="sxs-lookup"><span data-stu-id="50949-130">Get all available VM sizes</span></span> | `az vm list-sizes --location eastus` |

## <a name="disks-and-images"></a><span data-ttu-id="50949-131">디스크 및 이미지</span><span class="sxs-lookup"><span data-stu-id="50949-131">Disks and images</span></span>
| <span data-ttu-id="50949-132">작업</span><span class="sxs-lookup"><span data-stu-id="50949-132">Task</span></span> | <span data-ttu-id="50949-133">Azure CLI 명령</span><span class="sxs-lookup"><span data-stu-id="50949-133">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="50949-134">데이터 디스크 tooa VM 추가</span><span class="sxs-lookup"><span data-stu-id="50949-134">Add a data disk tooa VM</span></span> | `az vm disk attach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk --size-gb 128 --new ` |
| <span data-ttu-id="50949-135">VM에서 데이터 디스크 제거</span><span class="sxs-lookup"><span data-stu-id="50949-135">Remove a data disk from a VM</span></span> | `az vm disk detach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk` |
| <span data-ttu-id="50949-136">디스크 크기 조정</span><span class="sxs-lookup"><span data-stu-id="50949-136">Resize a disk</span></span> | `az disk update --resource-group myResourceGroup --name myDataDisk --size-gb 256` |
| <span data-ttu-id="50949-137">디스크 스냅숏</span><span class="sxs-lookup"><span data-stu-id="50949-137">Snapshot a disk</span></span> | `az snapshot create --resource-group myResourceGroup --name mySnapshot --source myDataDisk` |
| <span data-ttu-id="50949-138">VM 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="50949-138">Create image of a VM</span></span> | `az image create --resource-group myResourceGroup --source myVM --name myImage` |
| <span data-ttu-id="50949-139">이미지에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="50949-139">Create VM from image</span></span> | `az vm create --resource-group myResourceGroup --name myNewVM --image myImage` |


## <a name="next-steps"></a><span data-ttu-id="50949-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="50949-140">Next steps</span></span>
<span data-ttu-id="50949-141">Hello CLI 명령의 추가 예 참조 hello [만들기 및 Azure CLI hello로 Linux Vm 관리](../articles/virtual-machines/linux/tutorial-manage-vm.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="50949-141">For additional examples of hello CLI commands, see hello [Create and Manage Linux VMs with hello Azure CLI](../articles/virtual-machines/linux/tutorial-manage-vm.md) tutorial.</span></span>

