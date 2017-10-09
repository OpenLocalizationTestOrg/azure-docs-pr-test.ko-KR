## <a name="create-a-resource-group"></a><span data-ttu-id="728ea-101">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="728ea-101">Create a resource group</span></span>

<span data-ttu-id="728ea-102">Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="728ea-102">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="728ea-103">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="728ea-103">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="728ea-104">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="728ea-104">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="728ea-105">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="728ea-105">Create a virtual machine</span></span>

<span data-ttu-id="728ea-106">Hello로 VM을 만들 [az vm 만들기](/cli/azure/vm#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="728ea-106">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="728ea-107">hello 다음 예제에서는 V *myVM* 하 고 기본 키 위치에 이미 존재 하지 않는 경우 SSH 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="728ea-107">hello following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="728ea-108">toouse 특정 키의 집합, hello를 사용 하 여 `--ssh-key-value` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="728ea-108">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="728ea-109">Hello VM을 만든 hello Azure CLI 정보 비슷한 toohello 다음 예제에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="728ea-109">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="728ea-110">Hello를 메모해 `publicIpAddress`합니다.</span><span class="sxs-lookup"><span data-stu-id="728ea-110">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="728ea-111">이 주소는 사용 되는 tooaccess hello VM입니다.</span><span class="sxs-lookup"><span data-stu-id="728ea-111">This address is used tooaccess hello VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```



## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="728ea-112">웹 트래픽에 대해 포트 80 열기</span><span class="sxs-lookup"><span data-stu-id="728ea-112">Open port 80 for web traffic</span></span> 

<span data-ttu-id="728ea-113">기본적으로 Azure에 배포된 Linux VM에는 SSH 연결만이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="728ea-113">By default, only SSH connections are allowed into Linux VMs deployed in Azure.</span></span> <span data-ttu-id="728ea-114">Hello에서 tooopen 포트 80을 때문에이 VM은 웹 서버 toobe 해야 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="728ea-114">Because this VM is going toobe a web server, you need tooopen port 80 from hello internet.</span></span> <span data-ttu-id="728ea-115">사용 하 여 hello [az vm-포트를 열](/cli/azure/vm#open-port) 명령 tooopen hello 원하는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="728ea-115">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a><span data-ttu-id="728ea-116">VM에 SSH 수행</span><span class="sxs-lookup"><span data-stu-id="728ea-116">SSH into your VM</span></span>


<span data-ttu-id="728ea-117">VM의 공용 IP 주소를 hello, hello 실행 이미 알고 하지 않는 경우 [az 네트워크 공개 ip 목록](/cli/azure/network/public-ip#list) 명령:</span><span class="sxs-lookup"><span data-stu-id="728ea-117">If you don't already know hello public IP address of your VM, run hello [az network public-ip list](/cli/azure/network/public-ip#list) command:</span></span>


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

<span data-ttu-id="728ea-118">사용 하 여 hello 다음 명령은 toocreate hello 가상 컴퓨터와의 SSH 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="728ea-118">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="728ea-119">Hello 올바른 공용 IP 주소를 가상 컴퓨터를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="728ea-119">Substitute hello correct public IP address of your virtual machine.</span></span> <span data-ttu-id="728ea-120">이 예제에서는 hello IP 주소는 *40.68.254.142*합니다.</span><span class="sxs-lookup"><span data-stu-id="728ea-120">In this example, hello IP address is *40.68.254.142*.</span></span>

```bash
ssh azureuser@40.68.254.142
```

