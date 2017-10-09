<span data-ttu-id="7ab76-101">배포 중 리소스 tootag 추가 hello `tags` 배포 하는 요소 toohello 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="7ab76-101">tootag a resource during deployment, add hello `tags` element toohello resource you are deploying.</span></span> <span data-ttu-id="7ab76-102">Hello 태그 이름 및 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab76-102">Provide hello tag name and value.</span></span>

### <a name="apply-a-literal-value-toohello-tag-name"></a><span data-ttu-id="7ab76-103">리터럴 값 toohello 태그 이름을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab76-103">Apply a literal value toohello tag name</span></span>
<span data-ttu-id="7ab76-104">hello 다음 예제에서는 두 개의 태그를 사용 하는 저장소 계정 (`Dept` 및 `Environment`) tooliteral 값을 설정 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="7ab76-104">hello following example shows a storage account with two tags (`Dept` and `Environment`) that are set tooliteral values:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

### <a name="apply-an-object-toohello-tag-element"></a><span data-ttu-id="7ab76-105">개체 toohello 태그 요소를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab76-105">Apply an object toohello tag element</span></span>
<span data-ttu-id="7ab76-106">여러 태그를 저장 하는 개체 매개 변수를 정의할 수 있으며 해당 개체 toohello 태그 요소를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab76-106">You can define an object parameter that stores several tags, and apply that object toohello tag element.</span></span> <span data-ttu-id="7ab76-107">Hello 개체의 각 속성에는 hello 리소스에 대 한 별도 태그 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab76-107">Each property in hello object becomes a separate tag for hello resource.</span></span> <span data-ttu-id="7ab76-108">hello 다음 예제는 명명 된 매개 변수가 `tagValues` 즉 적용 된 toohello 태그 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="7ab76-108">hello following example has a parameter named `tagValues` that is applied toohello tag element.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "tagValues": {
      "type": "object",
      "defaultValue": {
        "Dept": "Finance",
        "Environment": "Production"
      }
    }
  },
  "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": "[parameters('tagValues')]",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": {}
    }
  ]
}
```

### <a name="apply-a-json-string-toohello-tag-name"></a><span data-ttu-id="7ab76-109">JSON 문자열 toohello 태그 이름을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab76-109">Apply a JSON string toohello tag name</span></span>

<span data-ttu-id="7ab76-110">toostore을 단일 태그에 값이 많은 hello 값을 나타내는 JSON 문자열로 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab76-110">toostore many values in a single tag, apply a JSON string that represents hello values.</span></span> <span data-ttu-id="7ab76-111">전체 JSON 문자열 hello 256 자를 초과할 수 없으며 한 태그로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab76-111">hello entire JSON string is stored as one tag that cannot exceed 256 characters.</span></span> <span data-ttu-id="7ab76-112">hello 다음 예제는 명명 된 단일 태그로 `CostCenter` JSON 문자열에서 여러 값이 포함 된:</span><span class="sxs-lookup"><span data-stu-id="7ab76-112">hello following example has a single tag named `CostCenter` that contains several values from a JSON string:</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": {
        "CostCenter": "{\"Dept\":\"Finance\",\"Environment\":\"Production\"}"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```