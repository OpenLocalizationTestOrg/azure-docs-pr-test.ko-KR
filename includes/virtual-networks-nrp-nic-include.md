## <a name="nic"></a><span data-ttu-id="90040-101">NIC</span><span class="sxs-lookup"><span data-stu-id="90040-101">NIC</span></span>
<span data-ttu-id="90040-102">네트워크 인터페이스 카드 (NIC) 리소스 VNet 리소스의 네트워크 연결 tooan 기존 서브넷을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="90040-102">A network interface card (NIC) resource provides network connectivity tooan existing subnet in a VNet resource.</span></span> <span data-ttu-id="90040-103">Tooassociate 독립 실행형 개체로 NIC를 만들 수 있지만 필요한 것 tooanother 개체 tooactually 연결을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="90040-103">Although you can create a NIC as a stand alone object, you need tooassociate it tooanother object tooactually provide connectivity.</span></span> <span data-ttu-id="90040-104">NIC VM tooa 서브넷, 공용 IP 주소 또는 부하 분산 장치 사용된 tooconnect를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90040-104">A NIC can be used tooconnect a VM tooa subnet, a public IP address, or a load balancer.</span></span>  

| <span data-ttu-id="90040-105">속성</span><span class="sxs-lookup"><span data-stu-id="90040-105">Property</span></span> | <span data-ttu-id="90040-106">설명</span><span class="sxs-lookup"><span data-stu-id="90040-106">Description</span></span> | <span data-ttu-id="90040-107">샘플 값</span><span class="sxs-lookup"><span data-stu-id="90040-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="90040-108">**virtualMachine**</span><span class="sxs-lookup"><span data-stu-id="90040-108">**virtualMachine**</span></span> |<span data-ttu-id="90040-109">VM hello NIC에 연결 된입니다.</span><span class="sxs-lookup"><span data-stu-id="90040-109">VM hello NIC is associated with.</span></span> |<span data-ttu-id="90040-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span><span class="sxs-lookup"><span data-stu-id="90040-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span></span> |
| <span data-ttu-id="90040-111">**macAddress**</span><span class="sxs-lookup"><span data-stu-id="90040-111">**macAddress**</span></span> |<span data-ttu-id="90040-112">NIC hello에 대 한 MAC 주소</span><span class="sxs-lookup"><span data-stu-id="90040-112">MAC address for hello NIC</span></span> |<span data-ttu-id="90040-113">4와 30 사이의 임의 값</span><span class="sxs-lookup"><span data-stu-id="90040-113">any value between 4 and 30</span></span> |
| <span data-ttu-id="90040-114">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="90040-114">**networkSecurityGroup**</span></span> |<span data-ttu-id="90040-115">연결 된 NSG toohello NIC</span><span class="sxs-lookup"><span data-stu-id="90040-115">NSG associated toohello NIC</span></span> |<span data-ttu-id="90040-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span><span class="sxs-lookup"><span data-stu-id="90040-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span></span> |
| <span data-ttu-id="90040-117">**dnsSettings**</span><span class="sxs-lookup"><span data-stu-id="90040-117">**dnsSettings**</span></span> |<span data-ttu-id="90040-118">NIC hello에 대 한 DNS 설정</span><span class="sxs-lookup"><span data-stu-id="90040-118">DNS settings for hello NIC</span></span> |<span data-ttu-id="90040-119">[PIP](#Public-IP-address)</span><span class="sxs-lookup"><span data-stu-id="90040-119">see [PIP](#Public-IP-address)</span></span> |

<span data-ttu-id="90040-120">네트워크 인터페이스 카드 또는 NIC를 관련된 tooa 가상 컴퓨터 (VM) 일 수 있는 네트워크 인터페이스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="90040-120">A Network Interface Card, or NIC, represents a network interface that can be associated tooa virtual machine (VM).</span></span> <span data-ttu-id="90040-121">VM은 NIC를 하나 이상 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90040-121">A VM can have one or more NICs.</span></span>

![단일 VM의 NIC](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a><span data-ttu-id="90040-123">IP 구성</span><span class="sxs-lookup"><span data-stu-id="90040-123">IP configurations</span></span>
<span data-ttu-id="90040-124">Nic가 명명 된 자식 개체 **ipConfigurations** hello 다음과 같은 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="90040-124">NICs have a child object named **ipConfigurations** containing hello following properties:</span></span>

| <span data-ttu-id="90040-125">속성</span><span class="sxs-lookup"><span data-stu-id="90040-125">Property</span></span> | <span data-ttu-id="90040-126">설명</span><span class="sxs-lookup"><span data-stu-id="90040-126">Description</span></span> | <span data-ttu-id="90040-127">샘플 값</span><span class="sxs-lookup"><span data-stu-id="90040-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="90040-128">**subnet**</span><span class="sxs-lookup"><span data-stu-id="90040-128">**subnet**</span></span> |<span data-ttu-id="90040-129">서브넷 hello NIC에 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90040-129">Subnet hello NIC is onnected to.</span></span> |<span data-ttu-id="90040-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span><span class="sxs-lookup"><span data-stu-id="90040-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span></span> |
| <span data-ttu-id="90040-131">**privateIPAddress**</span><span class="sxs-lookup"><span data-stu-id="90040-131">**privateIPAddress**</span></span> |<span data-ttu-id="90040-132">Hello 서브넷의 NIC hello에 대 한 IP 주소</span><span class="sxs-lookup"><span data-stu-id="90040-132">IP address for hello NIC in hello subnet</span></span> |<span data-ttu-id="90040-133">10.0.0.8</span><span class="sxs-lookup"><span data-stu-id="90040-133">10.0.0.8</span></span> |
| <span data-ttu-id="90040-134">**privateIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="90040-134">**privateIPAllocationMethod**</span></span> |<span data-ttu-id="90040-135">IP 할당 방법</span><span class="sxs-lookup"><span data-stu-id="90040-135">IP allocation method</span></span> |<span data-ttu-id="90040-136">동적 또는 정적</span><span class="sxs-lookup"><span data-stu-id="90040-136">Dynamic or Static</span></span> |
| <span data-ttu-id="90040-137">**enableIPForwarding**</span><span class="sxs-lookup"><span data-stu-id="90040-137">**enableIPForwarding**</span></span> |<span data-ttu-id="90040-138">라우팅에 대 한 hello NIC를 사용할 수 있는지 여부</span><span class="sxs-lookup"><span data-stu-id="90040-138">Whether hello NIC can be used for routing</span></span> |<span data-ttu-id="90040-139">true 또는 false</span><span class="sxs-lookup"><span data-stu-id="90040-139">true or false</span></span> |
| <span data-ttu-id="90040-140">**primary**</span><span class="sxs-lookup"><span data-stu-id="90040-140">**primary**</span></span> |<span data-ttu-id="90040-141">Hello NIC 인지 hello hello VM에 대 한 기본 NIC</span><span class="sxs-lookup"><span data-stu-id="90040-141">Whether hello NIC is hello primary NIC for hello VM</span></span> |<span data-ttu-id="90040-142">true 또는 false</span><span class="sxs-lookup"><span data-stu-id="90040-142">true or false</span></span> |
| <span data-ttu-id="90040-143">**publicIPAddress**</span><span class="sxs-lookup"><span data-stu-id="90040-143">**publicIPAddress**</span></span> |<span data-ttu-id="90040-144">Hello NIC와 관련 된 PIP</span><span class="sxs-lookup"><span data-stu-id="90040-144">PIP associated with hello NIC</span></span> |<span data-ttu-id="90040-145">[DNS 설정](#DNS-settings)</span><span class="sxs-lookup"><span data-stu-id="90040-145">see [DNS Settings](#DNS-settings)</span></span> |
| <span data-ttu-id="90040-146">**loadBalancerBackendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="90040-146">**loadBalancerBackendAddressPools**</span></span> |<span data-ttu-id="90040-147">끝 주소 풀 hello NIC와 연결 된 백업</span><span class="sxs-lookup"><span data-stu-id="90040-147">Back end address pools hello NIC is associated with</span></span> | |
| <span data-ttu-id="90040-148">**loadBalancerInboundNatRules**</span><span class="sxs-lookup"><span data-stu-id="90040-148">**loadBalancerInboundNatRules**</span></span> |<span data-ttu-id="90040-149">부하 분산 장치 NAT 규칙 hello NIC와 연결 된 인바운드</span><span class="sxs-lookup"><span data-stu-id="90040-149">Inbound load balancer NAT rules hello NIC is associated with</span></span> | |

<span data-ttu-id="90040-150">JSON 형식의 샘플 공용 IP 주소:</span><span class="sxs-lookup"><span data-stu-id="90040-150">Sample public IP address in JSON format:</span></span>

    {
        "name": "lb-nic1-be",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkInterfaces",
        "location": "eastus",
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "ipConfigurations": [
                {
                    "name": "NIC-config",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/NIC-config",
                    "etag": "W/\"0027f1a2-3ac8-49de-b5d5-fd46550500b1\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "privateIPAddress": "10.0.0.4",
                        "privateIPAllocationMethod": "Dynamic",
                        "subnet": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet"
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1"
                            }
                        ]
                    }
                }
            ],
            "dnsSettings": { ... },
            "macAddress": "00-0D-3A-10-F1-29",
            "enableIPForwarding": false,
            "primary": true,
            "virtualMachine": {
                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Compute/virtualMachines/web1"
            }
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="90040-151">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="90040-151">Additional resources</span></span>
* <span data-ttu-id="90040-152">읽기 hello [REST API 참조 설명서](https://msdn.microsoft.com/library/azure/mt163579.aspx) Nic에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="90040-152">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163579.aspx) for NICs.</span></span>

