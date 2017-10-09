Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다.

[!INCLUDE [resource group intro text](resource-group.md)]

hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *westeurope* 위치 합니다.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

일반적으로 리소스 그룹 및 hello의 리소스를 만들 가까운 지역입니다. hello 실행 되는 Azure 웹 앱에 대 한 모든 지원 toosee 위치 `az appservice list-locations` 명령입니다. 
