## <a name="route-tables"></a><span data-ttu-id="12e06-101">경로 테이블</span><span class="sxs-lookup"><span data-stu-id="12e06-101">Route tables</span></span>
<span data-ttu-id="12e06-102">경로 테이블 리소스는 Azure 인프라 내에서 트래픽의 흐름 방식을 정의하는 데 사용되는 경로를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="12e06-102">Route table resources contains routes used to define how traffic flows within your Azure infrastructure.</span></span> <span data-ttu-id="12e06-103">UDR(사용자 정의 경로)을 사용하여 제공된 서브넷의 모든 트래픽을 방화벽 또는 IDS(침입 검색 시스템)와 같은 가상 어플라이언스로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12e06-103">You can use user defined routes (UDR) to send all traffic from a given subnet to a virtual appliance, such as a firewall or intrusion detection system (IDS).</span></span> <span data-ttu-id="12e06-104">경로 테이블은 서브넷에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12e06-104">You can associate a route table to subnets.</span></span> 

<span data-ttu-id="12e06-105">경로 테이블에는 다음 속성이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12e06-105">Route tables contain the following properties.</span></span>

| <span data-ttu-id="12e06-106">속성</span><span class="sxs-lookup"><span data-stu-id="12e06-106">Property</span></span> | <span data-ttu-id="12e06-107">설명</span><span class="sxs-lookup"><span data-stu-id="12e06-107">Description</span></span> | <span data-ttu-id="12e06-108">샘플 값</span><span class="sxs-lookup"><span data-stu-id="12e06-108">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="12e06-109">**routes**</span><span class="sxs-lookup"><span data-stu-id="12e06-109">**routes**</span></span> |<span data-ttu-id="12e06-110">경로 테이블의 사용자 정의 경로 컬렉션</span><span class="sxs-lookup"><span data-stu-id="12e06-110">Collection of user defined routes in the route table</span></span> |<span data-ttu-id="12e06-111">[사용자 정의 경로](#User-defined-routes)</span><span class="sxs-lookup"><span data-stu-id="12e06-111">see [user defined routes](#User-defined-routes)</span></span> |
| <span data-ttu-id="12e06-112">**서브넷**</span><span class="sxs-lookup"><span data-stu-id="12e06-112">**subnets**</span></span> |<span data-ttu-id="12e06-113">경로 테이블이 적용되는 서브넷의 컬렉션</span><span class="sxs-lookup"><span data-stu-id="12e06-113">Collection of subnets the route table is applied to</span></span> |<span data-ttu-id="12e06-114">[서브넷](#Subnets)</span><span class="sxs-lookup"><span data-stu-id="12e06-114">see [subnets](#Subnets)</span></span> |

### <a name="user-defined-routes"></a><span data-ttu-id="12e06-115">사용자 정의 경로</span><span class="sxs-lookup"><span data-stu-id="12e06-115">User defined routes</span></span>
<span data-ttu-id="12e06-116">UDR을 만들어 대상 주소에 따라 트래픽을 보낼 위치를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12e06-116">You can create UDRs to specify where traffic should be sent to, based on its destination address.</span></span> <span data-ttu-id="12e06-117">경로를 네트워크 패킷의 대상 주소에 기반한 기본 게이트웨이 정의로 간주해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12e06-117">You can think of a route as the default gateway definition based on the destination address of a network packet.</span></span>

<span data-ttu-id="12e06-118">UDR에는 다음 속성이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12e06-118">UDRs contain the following properties.</span></span> 

| <span data-ttu-id="12e06-119">속성</span><span class="sxs-lookup"><span data-stu-id="12e06-119">Property</span></span> | <span data-ttu-id="12e06-120">설명</span><span class="sxs-lookup"><span data-stu-id="12e06-120">Description</span></span> | <span data-ttu-id="12e06-121">샘플 값</span><span class="sxs-lookup"><span data-stu-id="12e06-121">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="12e06-122">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="12e06-122">**addressPrefix**</span></span> |<span data-ttu-id="12e06-123">대상의 주소 접두사 또는 전체 IP 주소</span><span class="sxs-lookup"><span data-stu-id="12e06-123">Address prefix, or full IP address for the destination</span></span> |<span data-ttu-id="12e06-124">192.168.1.0/24, 192.168.1.101</span><span class="sxs-lookup"><span data-stu-id="12e06-124">192.168.1.0/24, 192.168.1.101</span></span> |
| <span data-ttu-id="12e06-125">**nextHopType**</span><span class="sxs-lookup"><span data-stu-id="12e06-125">**nextHopType**</span></span> |<span data-ttu-id="12e06-126">트래픽을 보낼 장치의 유형</span><span class="sxs-lookup"><span data-stu-id="12e06-126">Type of device the traffic will be sent to</span></span> |<span data-ttu-id="12e06-127">VirtualAppliance, VPN 게이트웨이, 인터넷</span><span class="sxs-lookup"><span data-stu-id="12e06-127">VirtualAppliance, VPN Gateway, Internet</span></span> |
| <span data-ttu-id="12e06-128">**nextHopIpAddress**</span><span class="sxs-lookup"><span data-stu-id="12e06-128">**nextHopIpAddress**</span></span> |<span data-ttu-id="12e06-129">다음 홉에 대한 IP 주소</span><span class="sxs-lookup"><span data-stu-id="12e06-129">IP address for the next hop</span></span> |<span data-ttu-id="12e06-130">192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="12e06-130">192.168.1.4</span></span> |

<span data-ttu-id="12e06-131">JSON 형식의 샘플 경로 테이블:</span><span class="sxs-lookup"><span data-stu-id="12e06-131">Sample route table in JSON format:</span></span>

    {
        "name": "UDR-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/routeTables",
        "location": "westus",
        "properties": {
            "provisioningState": "Succeeded",
            "routes": [
                {
                    "name": "RouteToFrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd/routes/RouteToFrontEnd",
                    "etag": "W/\"v\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "nextHopType": "VirtualAppliance",
                        "nextHopIpAddress": "192.168.0.4"
                    }
                }
            ],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd"
                }
            ]
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="12e06-132">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="12e06-132">Additional resources</span></span>
* <span data-ttu-id="12e06-133">[UDR](../articles/virtual-network/virtual-networks-udr-overview.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="12e06-133">Get more information about [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).</span></span>
* <span data-ttu-id="12e06-134">경로 테이블에 대한 [REST API 참조 설명서](https://msdn.microsoft.com/library/azure/mt502549.aspx) 를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="12e06-134">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502549.aspx) for route tables.</span></span>
* <span data-ttu-id="12e06-135">UDR(사용자 정의 경로)에 대한 [REST API 참조 설명서](https://msdn.microsoft.com/library/azure/mt502539.aspx) 를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="12e06-135">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502539.aspx) for user defined routes (UDRs).</span></span>

