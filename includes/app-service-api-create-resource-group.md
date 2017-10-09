<span data-ttu-id="1a0ec-101">Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="1a0ec-101">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="1a0ec-102">hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *westeurope* 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a0ec-102">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="1a0ec-103">toosee hello 사용할 수 있는 위치, hello 실행 `az appservice list-locations` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="1a0ec-103">toosee hello available locations, run hello `az appservice list-locations` command.</span></span> <span data-ttu-id="1a0ec-104">일반적으로 사용자와 가까운 지역에서 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a0ec-104">You generally create resources in a region near you.</span></span>
