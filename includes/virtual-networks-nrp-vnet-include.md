## <a name="virtual-network"></a><span data-ttu-id="310ee-101">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="310ee-101">Virtual Network</span></span>
<span data-ttu-id="310ee-102">VNET(가상 네트워크)과 서브넷 리소스를 사용하여 Azure에서 실행 중인 워크로드에 대한 보안 경계를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="310ee-102">Virtual Networks (VNET) and subnets resources help define a security boundary for workloads running in Azure.</span></span> <span data-ttu-id="310ee-103">VNet은 주소 공간의 모임(CIDR 블록으로 정의됨)으로 특징지을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="310ee-103">A VNet is characterized by a collection of address spaces, defined as CIDR blocks.</span></span> 

> [!NOTE]
> <span data-ttu-id="310ee-104">네트워크 관리자는 CIDR 표기법에 익숙합니다.</span><span class="sxs-lookup"><span data-stu-id="310ee-104">Network administrators are familiar with CIDR notation.</span></span> <span data-ttu-id="310ee-105">CIDR을 잘 모르는 경우 [자세히 알아보세요](http://whatismyipaddress.com/cidr).</span><span class="sxs-lookup"><span data-stu-id="310ee-105">If you are not familiar with CIDR, [learn more about it](http://whatismyipaddress.com/cidr).</span></span>
> 
> 

![다중 서브넷을 가진 VNet](./media/resource-groups-networking/Figure4.png)

<span data-ttu-id="310ee-107">Vnet hello 다음과 같은 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="310ee-107">VNets contain hello following properties.</span></span>

| <span data-ttu-id="310ee-108">속성</span><span class="sxs-lookup"><span data-stu-id="310ee-108">Property</span></span> | <span data-ttu-id="310ee-109">설명</span><span class="sxs-lookup"><span data-stu-id="310ee-109">Description</span></span> | <span data-ttu-id="310ee-110">샘플 값</span><span class="sxs-lookup"><span data-stu-id="310ee-110">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="310ee-111">**addressSpace**</span><span class="sxs-lookup"><span data-stu-id="310ee-111">**addressSpace**</span></span> |<span data-ttu-id="310ee-112">CIDR 표기법에 hello VNet 구성 하는 주소 접두사의 컬렉션</span><span class="sxs-lookup"><span data-stu-id="310ee-112">Collection of address prefixes that make up hello VNet in CIDR notation</span></span> |<span data-ttu-id="310ee-113">192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="310ee-113">192.168.0.0/16</span></span> |
| <span data-ttu-id="310ee-114">**서브넷**</span><span class="sxs-lookup"><span data-stu-id="310ee-114">**subnets**</span></span> |<span data-ttu-id="310ee-115">서브넷 hello VNet 구성 하는 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="310ee-115">Collection of subnets that make up hello VNet</span></span> |<span data-ttu-id="310ee-116">아래 [서브넷](#Subnets) 참조</span><span class="sxs-lookup"><span data-stu-id="310ee-116">see [subnets](#Subnets) below.</span></span> |
| <span data-ttu-id="310ee-117">**ipAddress**</span><span class="sxs-lookup"><span data-stu-id="310ee-117">**ipAddress**</span></span> |<span data-ttu-id="310ee-118">IP 주소 할당 tooobject 합니다.</span><span class="sxs-lookup"><span data-stu-id="310ee-118">IP address assigned tooobject.</span></span> <span data-ttu-id="310ee-119">읽기 전용 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="310ee-119">This is a read-only property.</span></span> |<span data-ttu-id="310ee-120">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="310ee-120">104.42.233.77</span></span> |

### <a name="subnets"></a><span data-ttu-id="310ee-121">서브넷</span><span class="sxs-lookup"><span data-stu-id="310ee-121">Subnets</span></span>
<span data-ttu-id="310ee-122">서브넷은 VNet의 자식 리소스이며, IP 주소 접두사를 사용하여 CIDR 블록 내의 주소 공간 세그먼트를 정의하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="310ee-122">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="310ee-123">Nic는 toosubnets, 및 다양 한 작업에 대 한 연결을 제공 하는 연결 된 tooVMs를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="310ee-123">NICs can be added toosubnets, and connected tooVMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="310ee-124">서브넷 hello 다음과 같은 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="310ee-124">Subnets contain hello following properties.</span></span> 

| <span data-ttu-id="310ee-125">속성</span><span class="sxs-lookup"><span data-stu-id="310ee-125">Property</span></span> | <span data-ttu-id="310ee-126">설명</span><span class="sxs-lookup"><span data-stu-id="310ee-126">Description</span></span> | <span data-ttu-id="310ee-127">샘플 값</span><span class="sxs-lookup"><span data-stu-id="310ee-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="310ee-128">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="310ee-128">**addressPrefix**</span></span> |<span data-ttu-id="310ee-129">CIDR 표기법에서 hello 서브넷 구성 하는 단일 주소 접두사</span><span class="sxs-lookup"><span data-stu-id="310ee-129">Single address prefix that make up hello subnet in CIDR notation</span></span> |<span data-ttu-id="310ee-130">192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="310ee-130">192.168.1.0/24</span></span> |
| <span data-ttu-id="310ee-131">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="310ee-131">**networkSecurityGroup**</span></span> |<span data-ttu-id="310ee-132">NSG 적용 toohello 서브넷</span><span class="sxs-lookup"><span data-stu-id="310ee-132">NSG applied toohello subnet</span></span> |<span data-ttu-id="310ee-133">아래 [NSG](#Network-Security-Group)</span><span class="sxs-lookup"><span data-stu-id="310ee-133">see [NSGs](#Network-Security-Group)</span></span> |
| <span data-ttu-id="310ee-134">**routeTable**</span><span class="sxs-lookup"><span data-stu-id="310ee-134">**routeTable**</span></span> |<span data-ttu-id="310ee-135">경로 테이블 toohello 서브넷 적용</span><span class="sxs-lookup"><span data-stu-id="310ee-135">Route table applied toohello subnet</span></span> |<span data-ttu-id="310ee-136">아래 [UDR](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="310ee-136">see [UDR](#Route-table)</span></span> |
| <span data-ttu-id="310ee-137">**ipConfigurations**</span><span class="sxs-lookup"><span data-stu-id="310ee-137">**ipConfigurations**</span></span> |<span data-ttu-id="310ee-138">Nic 연결 된 toohello 서브넷에서 사용 되는 IP 구성 개체의 컬렉션</span><span class="sxs-lookup"><span data-stu-id="310ee-138">Collection of IP configruation objects used by NICs connected toohello subnet</span></span> |<span data-ttu-id="310ee-139">아래 [UDR](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="310ee-139">see [UDR](#Route-table)</span></span> |

<span data-ttu-id="310ee-140">JSON 형식의 샘플 VNet:</span><span class="sxs-lookup"><span data-stu-id="310ee-140">Sample VNet in JSON format:</span></span>

    {
        "name": "TestVNet",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/virtualNetworks",
        "location": "westus",
        "tags": {
            "displayName": "VNet"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "addressSpace": {
                "addressPrefixes": [
                    "192.168.0.0/16"
                ]
            },
            "subnets": [
                {
                    "name": "FrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "networkSecurityGroup": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "routeTable": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                        },
                        "ipConfigurations": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                            },
                            ...]
                    }
                },
                ...]
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="310ee-141">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="310ee-141">Additional resources</span></span>
* <span data-ttu-id="310ee-142">[VNet](../articles/virtual-network/virtual-networks-overview.md)에 대한 자세한 정보를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="310ee-142">Get more information about [VNet](../articles/virtual-network/virtual-networks-overview.md).</span></span>
* <span data-ttu-id="310ee-143">읽기 hello [REST API 참조 설명서](https://msdn.microsoft.com/library/azure/mt163650.aspx) Vnet에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="310ee-143">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163650.aspx) for VNets.</span></span>
* <span data-ttu-id="310ee-144">읽기 hello [REST API 참조 설명서](https://msdn.microsoft.com/library/azure/mt163618.aspx) 서브넷에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="310ee-144">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163618.aspx) for Subnets.</span></span>

