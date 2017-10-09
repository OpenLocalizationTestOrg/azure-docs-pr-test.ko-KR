## <a name="network-security-group"></a><span data-ttu-id="1bca8-101">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="1bca8-101">Network Security Group</span></span>
<span data-ttu-id="1bca8-102">NSG 리소스 작업에 대 한 보안 경계 hello 만들 수 있음, 구현 하 여 허용 및 거부 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="1bca8-102">An NSG resource enables hello creation of security boundary for workloads, by implementing allow and deny rules.</span></span> <span data-ttu-id="1bca8-103">이러한 규칙 될 수 있습니다 tooa VM, 서브넷 또는 NIC를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bca8-103">Such rules can be applied tooa VM, a NIC, or a subnet.</span></span>

| <span data-ttu-id="1bca8-104">속성</span><span class="sxs-lookup"><span data-stu-id="1bca8-104">Property</span></span> | <span data-ttu-id="1bca8-105">설명</span><span class="sxs-lookup"><span data-stu-id="1bca8-105">Description</span></span> | <span data-ttu-id="1bca8-106">샘플 값</span><span class="sxs-lookup"><span data-stu-id="1bca8-106">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1bca8-107">**서브넷**</span><span class="sxs-lookup"><span data-stu-id="1bca8-107">**subnets**</span></span> |<span data-ttu-id="1bca8-108">서브넷 id hello NSG의 목록에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bca8-108">List of subnet ids hello NSG is applied to.</span></span> |<span data-ttu-id="1bca8-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span><span class="sxs-lookup"><span data-stu-id="1bca8-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span></span> |
| <span data-ttu-id="1bca8-110">**securityRules**</span><span class="sxs-lookup"><span data-stu-id="1bca8-110">**securityRules**</span></span> |<span data-ttu-id="1bca8-111">Hello NSG 구성 하는 보안 규칙의 목록</span><span class="sxs-lookup"><span data-stu-id="1bca8-111">List of security rules that make up hello NSG</span></span> |<span data-ttu-id="1bca8-112">아래 [보안 규칙](#Security-rule) 참조</span><span class="sxs-lookup"><span data-stu-id="1bca8-112">See [Security rule](#Security-rule) below</span></span> |
| <span data-ttu-id="1bca8-113">**defaultSecurityRules**</span><span class="sxs-lookup"><span data-stu-id="1bca8-113">**defaultSecurityRules**</span></span> |<span data-ttu-id="1bca8-114">모든 NSG에 있는 기본 보안 규칙 목록</span><span class="sxs-lookup"><span data-stu-id="1bca8-114">List of default security rules present in every NSG</span></span> |<span data-ttu-id="1bca8-115">아래 [기본 보안 규칙](#Default-security-rules) 참조</span><span class="sxs-lookup"><span data-stu-id="1bca8-115">See [Default security rules](#Default-security-rules) below</span></span> |

* <span data-ttu-id="1bca8-116">**보안 규칙** - NSG에 대해 여러 보안 규칙을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bca8-116">**Security rule** - An NSG can have multiple security rules defined.</span></span> <span data-ttu-id="1bca8-117">각 규칙은 서로 다른 유형의 트래픽을 허용하거나 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bca8-117">Each rule can allow or deny different types of traffic.</span></span>

### <a name="security-rule"></a><span data-ttu-id="1bca8-118">보안 규칙</span><span class="sxs-lookup"><span data-stu-id="1bca8-118">Security rule</span></span>
<span data-ttu-id="1bca8-119">보안 규칙은 nsg 아래의 hello 속성을 포함 하는 자식 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="1bca8-119">A security rule is a child resource of an NSG containing hello properties below.</span></span>

| <span data-ttu-id="1bca8-120">속성</span><span class="sxs-lookup"><span data-stu-id="1bca8-120">Property</span></span> | <span data-ttu-id="1bca8-121">설명</span><span class="sxs-lookup"><span data-stu-id="1bca8-121">Description</span></span> | <span data-ttu-id="1bca8-122">샘플 값</span><span class="sxs-lookup"><span data-stu-id="1bca8-122">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1bca8-123">**description**</span><span class="sxs-lookup"><span data-stu-id="1bca8-123">**description**</span></span> |<span data-ttu-id="1bca8-124">Hello 규칙에 대 한 설명</span><span class="sxs-lookup"><span data-stu-id="1bca8-124">Description for hello rule</span></span> |<span data-ttu-id="1bca8-125">서브넷 X에서 모든 VM에 인바운드 트래픽 허용</span><span class="sxs-lookup"><span data-stu-id="1bca8-125">Allow inbound traffic for all VMs in subnet X</span></span> |
| <span data-ttu-id="1bca8-126">**protocol**</span><span class="sxs-lookup"><span data-stu-id="1bca8-126">**protocol**</span></span> |<span data-ttu-id="1bca8-127">Hello 규칙에 대 한 프로토콜 toomatch</span><span class="sxs-lookup"><span data-stu-id="1bca8-127">Protocol toomatch for hello rule</span></span> |<span data-ttu-id="1bca8-128">TCP, UDP, 또는 *</span><span class="sxs-lookup"><span data-stu-id="1bca8-128">TCP, UDP, or *</span></span> |
| <span data-ttu-id="1bca8-129">**sourcePortRange**</span><span class="sxs-lookup"><span data-stu-id="1bca8-129">**sourcePortRange**</span></span> |<span data-ttu-id="1bca8-130">원본 포트 범위 toomatch hello 규칙에 대 한</span><span class="sxs-lookup"><span data-stu-id="1bca8-130">Source port range toomatch for hello rule</span></span> |<span data-ttu-id="1bca8-131">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="1bca8-131">80, 100-200, *</span></span> |
| <span data-ttu-id="1bca8-132">**destinationPortRange**</span><span class="sxs-lookup"><span data-stu-id="1bca8-132">**destinationPortRange**</span></span> |<span data-ttu-id="1bca8-133">대상 포트 범위 toomatch hello 규칙에 대 한</span><span class="sxs-lookup"><span data-stu-id="1bca8-133">Destination port range toomatch for hello rule</span></span> |<span data-ttu-id="1bca8-134">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="1bca8-134">80, 100-200, *</span></span> |
| <span data-ttu-id="1bca8-135">**sourceAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="1bca8-135">**sourceAddressPrefix**</span></span> |<span data-ttu-id="1bca8-136">소스 주소 접두사 toomatch hello 규칙에 대 한</span><span class="sxs-lookup"><span data-stu-id="1bca8-136">Source address prefix toomatch for hello rule</span></span> |<span data-ttu-id="1bca8-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="1bca8-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="1bca8-138">**destinationAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="1bca8-138">**destinationAddressPrefix**</span></span> |<span data-ttu-id="1bca8-139">대상 주소 접두사 toomatch hello 규칙에 대 한</span><span class="sxs-lookup"><span data-stu-id="1bca8-139">Destination address prefix toomatch for hello rule</span></span> |<span data-ttu-id="1bca8-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="1bca8-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="1bca8-141">**direction**</span><span class="sxs-lookup"><span data-stu-id="1bca8-141">**direction**</span></span> |<span data-ttu-id="1bca8-142">Hello 규칙에 대 한 트래픽 toomatch의 방향</span><span class="sxs-lookup"><span data-stu-id="1bca8-142">Direction of traffic toomatch for hello rule</span></span> |<span data-ttu-id="1bca8-143">인바운드 또는 아웃바운드</span><span class="sxs-lookup"><span data-stu-id="1bca8-143">inbound or outbound</span></span> |
| <span data-ttu-id="1bca8-144">**우선 순위**</span><span class="sxs-lookup"><span data-stu-id="1bca8-144">**priority**</span></span> |<span data-ttu-id="1bca8-145">Hello 규칙에 대 한 우선 순위입니다.</span><span class="sxs-lookup"><span data-stu-id="1bca8-145">Priority for hello rule.</span></span> <span data-ttu-id="1bca8-146">규칙은 우선 순위대로 검사되고, 규칙이 적용된 후에는 일치 여부를 알기 위해 규칙이 더 이상 테스트되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1bca8-146">Rules are checked int he order of priority, once a rule applies, no more rules are tested for matching.</span></span> |<span data-ttu-id="1bca8-147">10, 100, 65000</span><span class="sxs-lookup"><span data-stu-id="1bca8-147">10, 100, 65000</span></span> |
| <span data-ttu-id="1bca8-148">**access**</span><span class="sxs-lookup"><span data-stu-id="1bca8-148">**access**</span></span> |<span data-ttu-id="1bca8-149">유형의 액세스 tooapply hello 규칙과 일치 하는 경우</span><span class="sxs-lookup"><span data-stu-id="1bca8-149">Type of access tooapply if hello rule matches</span></span> |<span data-ttu-id="1bca8-150">허용 또는 거부</span><span class="sxs-lookup"><span data-stu-id="1bca8-150">allow or deny</span></span> |

<span data-ttu-id="1bca8-151">JSON 형식의 샘플 NSG:</span><span class="sxs-lookup"><span data-stu-id="1bca8-151">Sample NSG in JSON format:</span></span>

    {
        "name": "NSG-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkSecurityGroups",
        "location": "westus",
        "tags": {
            "displayName": "NSG - Front End"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "securityRules": [
                {
                    "name": "rdp-rule",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/rdp-rule",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "description": "Allow RDP",
                        "protocol": "Tcp",
                        "sourcePortRange": "*",
                        "destinationPortRange": "3389",
                        "sourceAddressPrefix": "Internet",
                        "destinationAddressPrefix": "*",
                        "access": "Allow",
                        "priority": 100,
                        "direction": "Inbound"
                    }
                }
            ],
            "defaultSecurityRules": [
                { [...],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                }
            ]
        }
    }

### <a name="default-security-rules"></a><span data-ttu-id="1bca8-152">기본 보안 규칙</span><span class="sxs-lookup"><span data-stu-id="1bca8-152">Default security rules</span></span>

<span data-ttu-id="1bca8-153">기본 보안 규칙 hello는 보안 규칙에서 사용할 수 있는 동일한 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bca8-153">Default security rules have hello same properties available in security rules.</span></span> <span data-ttu-id="1bca8-154">이러한 적용할 Nsg toothem 않은 리소스 간의 기본 연결 tooprovide 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bca8-154">They exist tooprovide basic connectivity between resources that have NSGs applied toothem.</span></span> <span data-ttu-id="1bca8-155">어떤 [기본 보안 규칙](../articles/virtual-network/virtual-networks-nsg.md#default-rules) 이 있는지 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bca8-155">Make sure you know which [default security rules](../articles/virtual-network/virtual-networks-nsg.md#default-rules) exist.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="1bca8-156">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1bca8-156">Additional resources</span></span>
* <span data-ttu-id="1bca8-157">[NSG](../articles/virtual-network/virtual-networks-nsg.md)에 대한 자세한 정보를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1bca8-157">Get more information about [NSGs](../articles/virtual-network/virtual-networks-nsg.md).</span></span>
* <span data-ttu-id="1bca8-158">읽기 hello [REST API 참조 설명서](https://msdn.microsoft.com/library/azure/mt163615.aspx) Nsg에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bca8-158">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163615.aspx) for NSGs.</span></span>
* <span data-ttu-id="1bca8-159">읽기 hello [REST API 참조 설명서](https://msdn.microsoft.com/library/azure/mt163580.aspx) 보안 규칙에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bca8-159">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163580.aspx) for security rules.</span></span>
