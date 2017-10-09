## <a name="route-tables"></a><span data-ttu-id="ee272-101">경로 테이블</span><span class="sxs-lookup"><span data-stu-id="ee272-101">Route tables</span></span>
<span data-ttu-id="ee272-102">경로 테이블 리소스에 사용 된 경로 toodefine 트래픽이 Azure 인프라 내에서 어떻게 이동 하는지 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee272-102">Route table resources contains routes used toodefine how traffic flows within your Azure infrastructure.</span></span> <span data-ttu-id="ee272-103">사용자 정의 경로 (UDR) toosend을 특정된 서브넷 tooa 가상 어플라이언스로 (ID)는 방화벽 또는 침입 감지 시스템 등의 모든 트래픽이 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee272-103">You can use user defined routes (UDR) toosend all traffic from a given subnet tooa virtual appliance, such as a firewall or intrusion detection system (IDS).</span></span> <span data-ttu-id="ee272-104">경로 테이블 toosubnets를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee272-104">You can associate a route table toosubnets.</span></span> 

<span data-ttu-id="ee272-105">경로 테이블 hello 다음과 같은 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee272-105">Route tables contain hello following properties.</span></span>

| <span data-ttu-id="ee272-106">속성</span><span class="sxs-lookup"><span data-stu-id="ee272-106">Property</span></span> | <span data-ttu-id="ee272-107">설명</span><span class="sxs-lookup"><span data-stu-id="ee272-107">Description</span></span> | <span data-ttu-id="ee272-108">샘플 값</span><span class="sxs-lookup"><span data-stu-id="ee272-108">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ee272-109">**routes**</span><span class="sxs-lookup"><span data-stu-id="ee272-109">**routes**</span></span> |<span data-ttu-id="ee272-110">Hello 경로 테이블의 경로 정의 하는 사용자의 컬렉션</span><span class="sxs-lookup"><span data-stu-id="ee272-110">Collection of user defined routes in hello route table</span></span> |<span data-ttu-id="ee272-111">[사용자 정의 경로](#User-defined-routes)</span><span class="sxs-lookup"><span data-stu-id="ee272-111">see [user defined routes](#User-defined-routes)</span></span> |
| <span data-ttu-id="ee272-112">**서브넷**</span><span class="sxs-lookup"><span data-stu-id="ee272-112">**subnets**</span></span> |<span data-ttu-id="ee272-113">서브넷 hello 경로 테이블의 컬렉션 너무 적용</span><span class="sxs-lookup"><span data-stu-id="ee272-113">Collection of subnets hello route table is applied too</span></span>|<span data-ttu-id="ee272-114">[서브넷](#Subnets)</span><span class="sxs-lookup"><span data-stu-id="ee272-114">see [subnets](#Subnets)</span></span> |

### <a name="user-defined-routes"></a><span data-ttu-id="ee272-115">사용자 정의 경로</span><span class="sxs-lookup"><span data-stu-id="ee272-115">User defined routes</span></span>
<span data-ttu-id="ee272-116">대상 주소에 기반 UDRs toospecify 트래픽를 보낼 위치를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee272-116">You can create UDRs toospecify where traffic should be sent to, based on its destination address.</span></span> <span data-ttu-id="ee272-117">Hello 기본 게이트웨이 정의 네트워크 패킷의 hello 대상 주소를 기반으로 하는 경로 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee272-117">You can think of a route as hello default gateway definition based on hello destination address of a network packet.</span></span>

<span data-ttu-id="ee272-118">UDRs hello 다음과 같은 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee272-118">UDRs contain hello following properties.</span></span> 

| <span data-ttu-id="ee272-119">속성</span><span class="sxs-lookup"><span data-stu-id="ee272-119">Property</span></span> | <span data-ttu-id="ee272-120">설명</span><span class="sxs-lookup"><span data-stu-id="ee272-120">Description</span></span> | <span data-ttu-id="ee272-121">샘플 값</span><span class="sxs-lookup"><span data-stu-id="ee272-121">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ee272-122">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="ee272-122">**addressPrefix**</span></span> |<span data-ttu-id="ee272-123">주소 접두사 또는 hello 대상에 대 한 전체 IP 주소</span><span class="sxs-lookup"><span data-stu-id="ee272-123">Address prefix, or full IP address for hello destination</span></span> |<span data-ttu-id="ee272-124">192.168.1.0/24, 192.168.1.101</span><span class="sxs-lookup"><span data-stu-id="ee272-124">192.168.1.0/24, 192.168.1.101</span></span> |
| <span data-ttu-id="ee272-125">**nextHopType**</span><span class="sxs-lookup"><span data-stu-id="ee272-125">**nextHopType**</span></span> |<span data-ttu-id="ee272-126">장치 hello 트래픽 종류에는 너무에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee272-126">Type of device hello traffic will be sent too</span></span>|<span data-ttu-id="ee272-127">VirtualAppliance, VPN 게이트웨이, 인터넷</span><span class="sxs-lookup"><span data-stu-id="ee272-127">VirtualAppliance, VPN Gateway, Internet</span></span> |
| <span data-ttu-id="ee272-128">**nextHopIpAddress**</span><span class="sxs-lookup"><span data-stu-id="ee272-128">**nextHopIpAddress**</span></span> |<span data-ttu-id="ee272-129">다음 홉 hello에 대 한 IP 주소</span><span class="sxs-lookup"><span data-stu-id="ee272-129">IP address for hello next hop</span></span> |<span data-ttu-id="ee272-130">192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="ee272-130">192.168.1.4</span></span> |

<span data-ttu-id="ee272-131">JSON 형식의 샘플 경로 테이블:</span><span class="sxs-lookup"><span data-stu-id="ee272-131">Sample route table in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="ee272-132">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="ee272-132">Additional resources</span></span>
* <span data-ttu-id="ee272-133">[UDR](../articles/virtual-network/virtual-networks-udr-overview.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="ee272-133">Get more information about [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).</span></span>
* <span data-ttu-id="ee272-134">읽기 hello [REST API 참조 설명서](https://msdn.microsoft.com/library/azure/mt502549.aspx) 경로 테이블에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee272-134">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502549.aspx) for route tables.</span></span>
* <span data-ttu-id="ee272-135">읽기 hello [REST API 참조 설명서](https://msdn.microsoft.com/library/azure/mt502539.aspx) 사용자에 대 한 경로 (UDRs)을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee272-135">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502539.aspx) for user defined routes (UDRs).</span></span>

