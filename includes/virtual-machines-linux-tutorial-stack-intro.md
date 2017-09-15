## <a name="create-a-resource-group"></a><span data-ttu-id="03827-101">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="03827-101">Create a resource group</span></span>

<span data-ttu-id="03827-102">[az group create](/cli/azure/group#create) 명령을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03827-102">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="03827-103">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="03827-103">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="03827-104">다음 예제에서는 *eastus* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03827-104">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="03827-105">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="03827-105">Create a virtual machine</span></span>

<span data-ttu-id="03827-106">[az vm create](/cli/azure/vm#create) 명령을 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03827-106">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="03827-107">다음 예제에서는 *myVM*이라는 VM을 만들고 기본 키 위치에 SSH 키가 없는 경우 이 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03827-107">The following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="03827-108">특정 키 집합을 사용하려면 `--ssh-key-value` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="03827-108">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="03827-109">VM을 만든 경우 Azure CLI는 다음 예제와 비슷한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="03827-109">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="03827-110">`publicIpAddress`을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="03827-110">Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="03827-111">이 주소는 VM에 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="03827-111">This address is used to access the VM.</span></span>

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



## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="03827-112">웹 트래픽에 대해 포트 80 열기</span><span class="sxs-lookup"><span data-stu-id="03827-112">Open port 80 for web traffic</span></span> 

<span data-ttu-id="03827-113">기본적으로 Azure에 배포된 Linux VM에는 SSH 연결만이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="03827-113">By default, only SSH connections are allowed into Linux VMs deployed in Azure.</span></span> <span data-ttu-id="03827-114">이 VM이 웹 서버가 되기 때문에 인터넷에서 포트 80을 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03827-114">Because this VM is going to be a web server, you need to open port 80 from the internet.</span></span> <span data-ttu-id="03827-115">[az vm open-port](/cli/azure/vm#open-port) 명령을 사용하여 원하는 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="03827-115">Use the [az vm open-port](/cli/azure/vm#open-port) command to open the desired port.</span></span>  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a><span data-ttu-id="03827-116">VM에 SSH 수행</span><span class="sxs-lookup"><span data-stu-id="03827-116">SSH into your VM</span></span>


<span data-ttu-id="03827-117">VM의 공용 IP 주소를 알고 있는 경우 [az network public-ip list](/cli/azure/network/public-ip#list) 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="03827-117">If you don't already know the public IP address of your VM, run the [az network public-ip list](/cli/azure/network/public-ip#list) command:</span></span>


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

<span data-ttu-id="03827-118">다음 명령을 사용하여 가상 컴퓨터와의 SSH 세션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03827-118">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="03827-119">가상 컴퓨터의 올바른 공용 IP 주소로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="03827-119">Substitute the correct public IP address of your virtual machine.</span></span> <span data-ttu-id="03827-120">이 예제에서 IP 주소는 *40.68.254.142*입니다.</span><span class="sxs-lookup"><span data-stu-id="03827-120">In this example, the IP address is *40.68.254.142*.</span></span>

```bash
ssh azureuser@40.68.254.142
```

