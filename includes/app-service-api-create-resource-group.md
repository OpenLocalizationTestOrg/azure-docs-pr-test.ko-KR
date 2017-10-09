Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다.

[!INCLUDE [resource group intro text](resource-group.md)]

hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *westeurope* 위치 합니다.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

toosee hello 사용할 수 있는 위치, hello 실행 `az appservice list-locations` 명령입니다. 일반적으로 사용자와 가까운 지역에서 리소스를 만듭니다.
