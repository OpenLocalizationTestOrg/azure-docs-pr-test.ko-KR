
### <a name="cacheskuname"></a><span data-ttu-id="d41da-101">cacheSKUName</span><span class="sxs-lookup"><span data-stu-id="d41da-101">cacheSKUName</span></span>
<span data-ttu-id="d41da-102">새 Azure Redis 캐시 hello hello의 가격 책정 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="d41da-102">hello pricing tier of hello new Azure Redis Cache.</span></span>

    "cacheSKUName": {
      "type": "string",
      "allowedValues": [
        "Basic",
        "Standard"
      ],
      "defaultValue": "Basic",
      "metadata": {
        "description": "hello pricing tier of hello new Azure Redis Cache."
      }
    },

<span data-ttu-id="d41da-103">hello 서식 파일은이 매개 변수 (기본 또는 표준)에 대 한 허용 되며 값을 지정 하는 경우 기본값 (기본)을 할당 하는 hello 값을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d41da-103">hello template defines hello values that are permitted for this parameter (Basic or Standard), and assigns a default value (Basic) if no value is specified.</span></span> <span data-ttu-id="d41da-104">Basic는 too53 GB를 사용할 수 있는 여러 크기와 단일 노드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d41da-104">Basic provides a single node with multiple sizes available up too53 GB.</span></span>
<span data-ttu-id="d41da-105">표준은은 too53 GB 인데 99.9 %SLA 사용할 수 있는 여러 크기와 주/복제본 2 개 노드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d41da-105">Standard provides two-node Primary/Replica with multiple sizes available up too53 GB and 99.9% SLA.</span></span>

### <a name="cacheskufamily"></a><span data-ttu-id="d41da-106">cacheSKUFamily</span><span class="sxs-lookup"><span data-stu-id="d41da-106">cacheSKUFamily</span></span>
<span data-ttu-id="d41da-107">hello sku에 대 한 hello 패밀리입니다.</span><span class="sxs-lookup"><span data-stu-id="d41da-107">hello family for hello sku.</span></span>

    "cacheSKUFamily": {
      "type": "string",
      "allowedValues": [
        "C"
      ],
      "defaultValue": "C",
      "metadata": {
        "description": "hello family for hello sku."
      }
    },


### <a name="cacheskucapacity"></a><span data-ttu-id="d41da-108">cacheSKUCapacity</span><span class="sxs-lookup"><span data-stu-id="d41da-108">cacheSKUCapacity</span></span>
<span data-ttu-id="d41da-109">새 Azure Redis Cache 인스턴스 hello의 hello 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="d41da-109">hello size of hello new Azure Redis Cache instance.</span></span> 

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
        "description": "hello size of hello new Azure Redis Cache instance. "
      }
    }


<span data-ttu-id="d41da-110">hello 서식 파일 (0, 1, 2, 3, 4, 5 또는 6),이 매개 변수에 대해 허용 되는 hello 값을 정의 하 고 값을 지정 하는 경우 기본값 (1)를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="d41da-110">hello template defines hello values that are permitted for this parameter (0, 1, 2, 3, 4, 5 or 6), and assigns a default value (1) if no value is specified.</span></span> <span data-ttu-id="d41da-111">Toofollowing 캐시 크기를 해당 하는 숫자: 0 = 250, 1 = 1 g B, 2 = 2.5 g B, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span><span class="sxs-lookup"><span data-stu-id="d41da-111">Those numbers correspond toofollowing cache sizes: 0 = 250 MB, 1 = 1 GB, 2 = 2.5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span></span>

