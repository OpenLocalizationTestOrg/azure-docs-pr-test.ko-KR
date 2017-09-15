## <a name="virtual-network"></a><span data-ttu-id="7cbac-101">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="7cbac-101">Virtual Network</span></span>
<span data-ttu-id="7cbac-102">VNET(가상 네트워크)과 서브넷 리소스를 사용하여 Azure에서 실행 중인 워크로드에 대한 보안 경계를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cbac-102">Virtual Networks (VNET) and subnets resources help define a security boundary for workloads running in Azure.</span></span> <span data-ttu-id="7cbac-103">VNet은 주소 공간의 모임(CIDR 블록으로 정의됨)으로 특징지을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cbac-103">A VNet is characterized by a collection of address spaces, defined as CIDR blocks.</span></span> 

> [!NOTE]
> <span data-ttu-id="7cbac-104">네트워크 관리자는 CIDR 표기법에 익숙합니다.</span><span class="sxs-lookup"><span data-stu-id="7cbac-104">Network administrators are familiar with CIDR notation.</span></span> <span data-ttu-id="7cbac-105">CIDR을 잘 모르는 경우 [자세히 알아보세요](http://whatismyipaddress.com/cidr).</span><span class="sxs-lookup"><span data-stu-id="7cbac-105">If you are not familiar with CIDR, [learn more about it](http://whatismyipaddress.com/cidr).</span></span>
> 
> 

![다중 서브넷을 가진 VNet](./media/resource-groups-networking/Figure4.png)

<span data-ttu-id="7cbac-107">VNet에는 다음 속성이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cbac-107">VNets contain the following properties.</span></span>

| <span data-ttu-id="7cbac-108">속성</span><span class="sxs-lookup"><span data-stu-id="7cbac-108">Property</span></span> | <span data-ttu-id="7cbac-109">설명</span><span class="sxs-lookup"><span data-stu-id="7cbac-109">Description</span></span> | <span data-ttu-id="7cbac-110">샘플 값</span><span class="sxs-lookup"><span data-stu-id="7cbac-110">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7cbac-111">**addressSpace**</span><span class="sxs-lookup"><span data-stu-id="7cbac-111">**addressSpace**</span></span> |<span data-ttu-id="7cbac-112">CIDR 표기법에서 VNet을 구성하는 주소 접두사 컬렉션</span><span class="sxs-lookup"><span data-stu-id="7cbac-112">Collection of address prefixes that make up the VNet in CIDR notation</span></span> |<span data-ttu-id="7cbac-113">192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="7cbac-113">192.168.0.0/16</span></span> |
| <span data-ttu-id="7cbac-114">**서브넷**</span><span class="sxs-lookup"><span data-stu-id="7cbac-114">**subnets**</span></span> |<span data-ttu-id="7cbac-115">VNet을 구성하는 서브넷 컬렉션</span><span class="sxs-lookup"><span data-stu-id="7cbac-115">Collection of subnets that make up the VNet</span></span> |<span data-ttu-id="7cbac-116">아래 [서브넷](#Subnets) 참조</span><span class="sxs-lookup"><span data-stu-id="7cbac-116">see [subnets](#Subnets) below.</span></span> |
| <span data-ttu-id="7cbac-117">**ipAddress**</span><span class="sxs-lookup"><span data-stu-id="7cbac-117">**ipAddress**</span></span> |<span data-ttu-id="7cbac-118">개체에 할당된 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="7cbac-118">IP address assigned to object.</span></span> <span data-ttu-id="7cbac-119">읽기 전용 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="7cbac-119">This is a read-only property.</span></span> |<span data-ttu-id="7cbac-120">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="7cbac-120">104.42.233.77</span></span> |

### <a name="subnets"></a><span data-ttu-id="7cbac-121">서브넷</span><span class="sxs-lookup"><span data-stu-id="7cbac-121">Subnets</span></span>
<span data-ttu-id="7cbac-122">서브넷은 VNet의 자식 리소스이며, IP 주소 접두사를 사용하여 CIDR 블록 내의 주소 공간 세그먼트를 정의하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cbac-122">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="7cbac-123">NIC는 서브넷에 추가하고 VM에 연결하여 다양한 워크로드에 대한 연결을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cbac-123">NICs can be added to subnets, and connected to VMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="7cbac-124">서브넷에는 다음 속성이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cbac-124">Subnets contain the following properties.</span></span> 

| <span data-ttu-id="7cbac-125">속성</span><span class="sxs-lookup"><span data-stu-id="7cbac-125">Property</span></span> | <span data-ttu-id="7cbac-126">설명</span><span class="sxs-lookup"><span data-stu-id="7cbac-126">Description</span></span> | <span data-ttu-id="7cbac-127">샘플 값</span><span class="sxs-lookup"><span data-stu-id="7cbac-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7cbac-128">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="7cbac-128">**addressPrefix**</span></span> |<span data-ttu-id="7cbac-129">CIDR 표기법에서 서브넷을 구성하는 단일 주소 접두사</span><span class="sxs-lookup"><span data-stu-id="7cbac-129">Single address prefix that make up the subnet in CIDR notation</span></span> |<span data-ttu-id="7cbac-130">192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="7cbac-130">192.168.1.0/24</span></span> |
| <span data-ttu-id="7cbac-131">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="7cbac-131">**networkSecurityGroup**</span></span> |<span data-ttu-id="7cbac-132">서브넷에 적용된 NSG</span><span class="sxs-lookup"><span data-stu-id="7cbac-132">NSG applied to the subnet</span></span> |<span data-ttu-id="7cbac-133">아래 [NSG](#Network-Security-Group)</span><span class="sxs-lookup"><span data-stu-id="7cbac-133">see [NSGs](#Network-Security-Group)</span></span> |
| <span data-ttu-id="7cbac-134">**routeTable**</span><span class="sxs-lookup"><span data-stu-id="7cbac-134">**routeTable**</span></span> |<span data-ttu-id="7cbac-135">서브넷에 적용된 경로 테이블</span><span class="sxs-lookup"><span data-stu-id="7cbac-135">Route table applied to the subnet</span></span> |<span data-ttu-id="7cbac-136">아래 [UDR](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="7cbac-136">see [UDR](#Route-table)</span></span> |
| <span data-ttu-id="7cbac-137">**ipConfigurations**</span><span class="sxs-lookup"><span data-stu-id="7cbac-137">**ipConfigurations**</span></span> |<span data-ttu-id="7cbac-138">서브넷에 연결된 NIC에 사용된 IP 구성 개체 컬렉션</span><span class="sxs-lookup"><span data-stu-id="7cbac-138">Collection of IP configruation objects used by NICs connected to the subnet</span></span> |<span data-ttu-id="7cbac-139">아래 [UDR](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="7cbac-139">see [UDR](#Route-table)</span></span> |

<span data-ttu-id="7cbac-140">JSON 형식의 샘플 VNet:</span><span class="sxs-lookup"><span data-stu-id="7cbac-140">Sample VNet in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="7cbac-141">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="7cbac-141">Additional resources</span></span>
* <span data-ttu-id="7cbac-142">[VNet](../articles/virtual-network/virtual-networks-overview.md)에 대한 자세한 정보를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7cbac-142">Get more information about [VNet](../articles/virtual-network/virtual-networks-overview.md).</span></span>
* <span data-ttu-id="7cbac-143">VNet에 대한 [REST API 참조 설명서](https://msdn.microsoft.com/library/azure/mt163650.aspx) 를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="7cbac-143">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163650.aspx) for VNets.</span></span>
* <span data-ttu-id="7cbac-144">서브넷에 대한 [REST API 참조 설명서](https://msdn.microsoft.com/library/azure/mt163618.aspx) 를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="7cbac-144">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163618.aspx) for Subnets.</span></span>

