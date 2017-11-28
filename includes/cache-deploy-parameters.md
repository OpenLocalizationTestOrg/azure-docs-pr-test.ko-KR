
### <a name="cacheskuname"></a><span data-ttu-id="8c231-101">cacheSKUName</span><span class="sxs-lookup"><span data-stu-id="8c231-101">cacheSKUName</span></span>
<span data-ttu-id="8c231-102">새 Azure Redis Cache의 가격 책정 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="8c231-102">The pricing tier of the new Azure Redis Cache.</span></span>

    "cacheSKUName": {
      "type": "string",
      "allowedValues": [
        "Basic",
        "Standard"
      ],
      "defaultValue": "Basic",
      "metadata": {
        "description": "The pricing tier of the new Azure Redis Cache."
      }
    },

<span data-ttu-id="8c231-103">이 매개 변수에 허용되는 값(Basic 또는 Standard)을 정의하고, 값이 지정되지 않은 경우에는 기본값(Basic)을 할당하는 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="8c231-103">The template defines the values that are permitted for this parameter (Basic or Standard), and assigns a default value (Basic) if no value is specified.</span></span> <span data-ttu-id="8c231-104">Basic은 최대 53GB를 사용할 수 있는 다양한 크기의 단일 노드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8c231-104">Basic provides a single node with multiple sizes available up to 53 GB.</span></span>
<span data-ttu-id="8c231-105">Standard는 최대 53GB를 사용할 수 있으며 99.9%의 SLA를 제공하는 다양한 크기의 2-노드 주/복제본을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8c231-105">Standard provides two-node Primary/Replica with multiple sizes available up to 53 GB and 99.9% SLA.</span></span>

### <a name="cacheskufamily"></a><span data-ttu-id="8c231-106">cacheSKUFamily</span><span class="sxs-lookup"><span data-stu-id="8c231-106">cacheSKUFamily</span></span>
<span data-ttu-id="8c231-107">SKU 제품군입니다.</span><span class="sxs-lookup"><span data-stu-id="8c231-107">The family for the sku.</span></span>

    "cacheSKUFamily": {
      "type": "string",
      "allowedValues": [
        "C"
      ],
      "defaultValue": "C",
      "metadata": {
        "description": "The family for the sku."
      }
    },


### <a name="cacheskucapacity"></a><span data-ttu-id="8c231-108">cacheSKUCapacity</span><span class="sxs-lookup"><span data-stu-id="8c231-108">cacheSKUCapacity</span></span>
<span data-ttu-id="8c231-109">새 Azure Redis Cache 인스턴스의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="8c231-109">The size of the new Azure Redis Cache instance.</span></span> 

    "cacheSKUCapacity": {
      "type": "int",
      "allowedValues": [
        0,
        1,
        2,
        3,
        4,
        5,
        6
      ],
      "defaultValue": 0,
      "metadata": {
        "description": "The size of the new Azure Redis Cache instance. "
      }
    }


<span data-ttu-id="8c231-110">이 매개 변수에 허용되는 값(0, 1, 2, 3, 4, 5 또는 6)을 정의하고, 값이 지정되지 않은 경우에는 기본값(1)을 할당하는 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="8c231-110">The template defines the values that are permitted for this parameter (0, 1, 2, 3, 4, 5 or 6), and assigns a default value (1) if no value is specified.</span></span> <span data-ttu-id="8c231-111">이러한 숫자는 다음 캐시 크기에 해당합니다. 0 = 250MB, 1 = 1GB, 2 = 2.5GB, 3 = 6GB, 4 = 13GB, 5 = 26GB, 6 = 53GB</span><span class="sxs-lookup"><span data-stu-id="8c231-111">Those numbers correspond to following cache sizes: 0 = 250 MB, 1 = 1 GB, 2 = 2.5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span></span>

