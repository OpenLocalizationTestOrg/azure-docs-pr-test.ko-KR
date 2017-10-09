<span data-ttu-id="b0471-101">Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b0471-101">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="b0471-102">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *westeurope* 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0471-102">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="b0471-103">일반적으로 리소스 그룹 및 hello의 리소스를 만들 가까운 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="b0471-103">You generally create your resource group and hello resources in a region near you.</span></span> <span data-ttu-id="b0471-104">hello 실행 되는 Azure 웹 앱에 대 한 모든 지원 toosee 위치 `az appservice list-locations` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b0471-104">toosee all supported locations for Azure Web Apps, run hello `az appservice list-locations` command.</span></span> 
