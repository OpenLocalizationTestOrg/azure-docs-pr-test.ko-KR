<span data-ttu-id="57d97-101">tooadd 태그 tooa 리소스 그룹을 사용 하 여 **으로 azure 그룹 집합**합니다.</span><span class="sxs-lookup"><span data-stu-id="57d97-101">tooadd a tag tooa resource group, use **azure group set**.</span></span> <span data-ttu-id="57d97-102">Hello 리소스 그룹에는 기존 태그 hello 태그에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57d97-102">If hello resource group does not have any existing tags, pass in hello tag.</span></span>

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

<span data-ttu-id="57d97-103">태그는 전체적으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="57d97-103">Tags are updated as a whole.</span></span> <span data-ttu-id="57d97-104">Tooadd 기존 태그 된 태그 tooa 리소스 그룹을 사용 하도록 하려는 경우 모든 hello 태그를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="57d97-104">If you want tooadd a tag tooa resource group that has existing tags, pass all hello tags.</span></span> 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

<span data-ttu-id="57d97-105">태그는 리소스 그룹에 있는 리소스에 의해 상속되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57d97-105">Tags are not inherited by resources in a resource group.</span></span> <span data-ttu-id="57d97-106">tooadd 태그 tooa 리소스를 사용 하 여 **azure 리소스 집합**합니다.</span><span class="sxs-lookup"><span data-stu-id="57d97-106">tooadd a tag tooa resource, use **azure resource set**.</span></span> <span data-ttu-id="57d97-107">Hello hello 태그를 추가 하는 hello 리소스 유형에 대 한 API 버전 번호를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="57d97-107">Pass hello API version number for hello resource type that you are adding hello tag to.</span></span> <span data-ttu-id="57d97-108">Tooretrieve hello API 버전을 해야 하는 경우 다음 설정 하는 hello 형식에 대 한 hello 리소스 공급자와 명령을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="57d97-108">If you need tooretrieve hello API version, use hello following command with hello resource provider for hello type you are setting:</span></span>

```azurecli
azure provider show -n Microsoft.Storage --json
```

<span data-ttu-id="57d97-109">Hello 결과에서 원하는 hello 리소스 종류를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="57d97-109">In hello results, look for hello resource type you want.</span></span>

```azurecli
"resourceTypes": [
{
  "resourceType": "storageAccounts",
  ...
  "apiVersions": [
    "2016-01-01",
    "2015-06-15",
    "2015-05-01-preview"
  ]
}
...
```

<span data-ttu-id="57d97-110">이제 API 버전, 리소스 그룹 이름, 리소스 이름, 리소스 유형 및 태그 값을 매개 변수로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="57d97-110">Now, provide that API version, resource group name, resource name, resource type, and tag value as parameters.</span></span>

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

<span data-ttu-id="57d97-111">태그는 리소스 및 리소스 그룹에 직접 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="57d97-111">Tags exist directly on resources and resource groups.</span></span> <span data-ttu-id="57d97-112">리소스 그룹을 사용 하 여 해당 리소스 toosee hello 기존 태그 가져오기 **으로 azure 그룹 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="57d97-112">toosee hello existing tags, get a resource group and its resources with **azure group show**.</span></span>

```azurecli
azure group show -n tag-demo-group --json
```

<span data-ttu-id="57d97-113">모든 태그가 적용 tooit 포함 hello 리소스 그룹에 대 한 메타 데이터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="57d97-113">Which returns metadata about hello resource group, including any tags applied tooit.</span></span>

```azurecli
{
  "id": "/subscriptions/4705409c-9372-42f0-914c-64a504530837/resourceGroups/tag-demo-group",
  "name": "tag-demo-group",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "location": "southcentralus",
  "tags": {
    "Dept": "Finance",
    "Environment": "Production",
    "Project": "Upgrade"
  },
  ...
}
```

<span data-ttu-id="57d97-114">사용 하 여 특정 리소스에 대 한 hello 태그를 보면 **azure 리소스 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="57d97-114">You view hello tags for a particular resource by using **azure resource show**.</span></span>

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

<span data-ttu-id="57d97-115">tooretrieve 모든 hello 리소스 태그 값으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="57d97-115">tooretrieve all hello resources with a tag value, use:</span></span>

```azurecli
azure resource list -t Dept=Finance --json
```

<span data-ttu-id="57d97-116">tooretrieve 태그 값을 가진 모든 hello 리소스 그룹을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="57d97-116">tooretrieve all hello resource groups with a tag value, use:</span></span>

```azurecli
azure group list -t Dept=Finance
```

<span data-ttu-id="57d97-117">다음 명령을 hello로 구독에 기존 태그 hello를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57d97-117">You can view hello existing tags in your subscription with hello following command:</span></span>

```azurecli
azure tag list
```
