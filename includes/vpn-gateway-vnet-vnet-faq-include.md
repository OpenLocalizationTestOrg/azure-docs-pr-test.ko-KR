<span data-ttu-id="3e923-101">VNet 간 FAQ는 VPN Gateway 연결에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e923-101">The VNet-to-VNet FAQ applies to VPN Gateway connections.</span></span> <span data-ttu-id="3e923-102">VNet 피어링을 찾으려면 [가상 네트워크 피어링](../articles/virtual-network/virtual-network-peering-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e923-102">If you are looking for VNet Peering, see [Virtual Network Peering](../articles/virtual-network/virtual-network-peering-overview.md)</span></span>

### <a name="does-azure-charge-for-traffic-between-vnets"></a><span data-ttu-id="3e923-103">Azure는 VNet 간 트래픽에 요금을 청구하나요?</span><span class="sxs-lookup"><span data-stu-id="3e923-103">Does Azure charge for traffic between VNets?</span></span>

<span data-ttu-id="3e923-104">VPN 게이트웨이 연결을 사용하는 경우 동일한 지역 내의 VNet 간 트래픽은 양방향 모두에 대해 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="3e923-104">VNet-to-VNet traffic within the same region is free for both directions when using a VPN gateway connection.</span></span> <span data-ttu-id="3e923-105">지역 전체 VNet 간 송신 트래픽은 원본 지역을 기반으로 아웃바운드 VNet 간 데이터 전송 요금으로 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e923-105">Cross region VNet-to-VNet egress traffic is charged with the outbound inter-VNet data transfer rates based on the source regions.</span></span> <span data-ttu-id="3e923-106">자세한 내용은 [VPN Gateway 가격 책정 페이지](https://azure.microsoft.com/pricing/details/vpn-gateway/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e923-106">Refer to the [VPN Gateway pricing page](https://azure.microsoft.com/pricing/details/vpn-gateway/) for details.</span></span> <span data-ttu-id="3e923-107">VPN Gateway 대신 VNet 피어링을 사용하여 VNet을 연결하는 경우 [Virtual Network 가격 책정 페이지](https://azure.microsoft.com/pricing/details/virtual-network/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e923-107">If you are connecting your VNets using VNet Peering, rather than VPN Gateway, see the [Virtual Network pricing page](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>

### <a name="does-vnet-to-vnet-traffic-travel-across-the-internet"></a><span data-ttu-id="3e923-108">VNet 간 트래픽은 인터넷을 거쳐서 이동하나요?</span><span class="sxs-lookup"><span data-stu-id="3e923-108">Does VNet-to-VNet traffic travel across the Internet?</span></span>

<span data-ttu-id="3e923-109">아니요.</span><span class="sxs-lookup"><span data-stu-id="3e923-109">No.</span></span> <span data-ttu-id="3e923-110">VNet 간 트래픽은 인터넷이 아닌 Microsoft Azure 백본을 거쳐서 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3e923-110">VNet-to-VNet traffic travels across the Microsoft Azure backbone, not the Internet.</span></span>

### <a name="is-vnet-to-vnet-traffic-secure"></a><span data-ttu-id="3e923-111">VNet 간 트래픽은 안전한가요?</span><span class="sxs-lookup"><span data-stu-id="3e923-111">Is VNet-to-VNet traffic secure?</span></span>

<span data-ttu-id="3e923-112">예, IPsec/IKE 암호화로 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e923-112">Yes, it is protected by IPsec/IKE encryption.</span></span>

### <a name="do-i-need-a-vpn-device-to-connect-vnets-together"></a><span data-ttu-id="3e923-113">VNet을 함께 연결하려면 VPN 장치가 필요한가요?</span><span class="sxs-lookup"><span data-stu-id="3e923-113">Do I need a VPN device to connect VNets together?</span></span>

<span data-ttu-id="3e923-114">아니요.</span><span class="sxs-lookup"><span data-stu-id="3e923-114">No.</span></span> <span data-ttu-id="3e923-115">크로스-프레미스 연결이 필요한 경우가 아니면 여러 Azure 가상 네트워크를 함께 연결할 때 VPN 장치는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e923-115">Connecting multiple Azure virtual networks together doesn't require a VPN device unless cross-premises connectivity is required.</span></span>

### <a name="do-my-vnets-need-to-be-in-the-same-region"></a><span data-ttu-id="3e923-116">VNet이 동일한 지역에 있어야 하나요?</span><span class="sxs-lookup"><span data-stu-id="3e923-116">Do my VNets need to be in the same region?</span></span>

<span data-ttu-id="3e923-117">아니요.</span><span class="sxs-lookup"><span data-stu-id="3e923-117">No.</span></span> <span data-ttu-id="3e923-118">가상 네트워크는 같은 Azure 지역(위치)에 있을 수도 있고 다른 Azure 지역(위치)에 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e923-118">The virtual networks can be in the same or different Azure regions (locations).</span></span>

### <a name="if-the-vnets-are-not-in-the-same-subscription-do-the-subscriptions-need-to-be-associated-with-the-same-ad-tenant"></a><span data-ttu-id="3e923-119">VNet이 동일한 구독에 없으면 구독이 동일한 AD 테넌트와 연결되어야 하나요?</span><span class="sxs-lookup"><span data-stu-id="3e923-119">If the VNets are not in the same subscription, do the subscriptions need to be associated with the same AD tenant?</span></span>

<span data-ttu-id="3e923-120">번호</span><span class="sxs-lookup"><span data-stu-id="3e923-120">No.</span></span>

### <a name="can-i-use-vnet-to-vnet-along-with-multi-site-connections"></a><span data-ttu-id="3e923-121">VNet간 연결을 멀티 사이트 연결과 함께 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="3e923-121">Can I use VNet-to-VNet along with multi-site connections?</span></span>

<span data-ttu-id="3e923-122">예.</span><span class="sxs-lookup"><span data-stu-id="3e923-122">Yes.</span></span> <span data-ttu-id="3e923-123">가상 네트워크 연결을 다중 사이트 VPN과 동시에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e923-123">Virtual network connectivity can be used simultaneously with multi-site VPNs.</span></span>

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a><span data-ttu-id="3e923-124">하나의 가상 네트워크에 연결할 수 있는 온-프레미스 사이트 및 가상 네트워크 수는 어떻게 됩니까?</span><span class="sxs-lookup"><span data-stu-id="3e923-124">How many on-premises sites and virtual networks can one virtual network connect to?</span></span>

<span data-ttu-id="3e923-125">[게이트웨이 요구 사항](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements) 테이블을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3e923-125">See [Gateway requirements](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements) table.</span></span>

### <a name="can-i-use-vnet-to-vnet-to-connect-vms-or-cloud-services-outside-of-a-vnet"></a><span data-ttu-id="3e923-126">VNet 간 연결을 사용하여 VNet 외부의 VM 또는 클라우드 서비스를 연결할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="3e923-126">Can I use VNet-to-VNet to connect VMs or cloud services outside of a VNet?</span></span>

<span data-ttu-id="3e923-127">아니요.</span><span class="sxs-lookup"><span data-stu-id="3e923-127">No.</span></span> <span data-ttu-id="3e923-128">VNet 간 연결은 가상 네트워크 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3e923-128">VNet-to-VNet supports connecting virtual networks.</span></span> <span data-ttu-id="3e923-129">가상 네트워크에 포함되어 있지 않은 가상 컴퓨터 또는 클라우드 서비스 연결은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e923-129">It does not support connecting virtual machines or cloud services that are not in a virtual network.</span></span>

### <a name="can-a-cloud-service-or-a-load-balancing-endpoint-span-vnets"></a><span data-ttu-id="3e923-130">클라우드 서비스 또는 부하 분산 끝점이 VNet까지 이어지나요?</span><span class="sxs-lookup"><span data-stu-id="3e923-130">Can a cloud service or a load balancing endpoint span VNets?</span></span>

<span data-ttu-id="3e923-131">아니요.</span><span class="sxs-lookup"><span data-stu-id="3e923-131">No.</span></span> <span data-ttu-id="3e923-132">클라우드 서비스 또는 부하 분산 끝점은 연결되어 있더라도 여러 가상 네트워크에 분산될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3e923-132">A cloud service or a load balancing endpoint can't span across virtual networks, even if they are connected together.</span></span>

### <a name="can-i-used-a-policybased-vpn-type-for-vnet-to-vnet-or-multi-site-connections"></a><span data-ttu-id="3e923-133">VNet 간 또는 멀티 사이트 연결에 PolicyBased VPN 유형을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="3e923-133">Can I used a PolicyBased VPN type for VNet-to-VNet or Multi-Site connections?</span></span>

<span data-ttu-id="3e923-134">아니요.</span><span class="sxs-lookup"><span data-stu-id="3e923-134">No.</span></span> <span data-ttu-id="3e923-135">VNet 간 연결 및 멀티 사이트 연결에는 RouteBased(이전 명칭: 동적 라우팅) VPN 유형의 Azure VPN 게이트웨이가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3e923-135">VNet-to-VNet and Multi-Site connections require Azure VPN gateways with RouteBased (previously called Dynamic Routing) VPN types.</span></span>

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-to-another-vnet-with-a-policybased-vpn-type"></a><span data-ttu-id="3e923-136">PolicyBased VPN 형식을 가진 VNet을 다른 RouteBased VPN 형식을 가진 VNet과 연결할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="3e923-136">Can I connect a VNet with a RouteBased VPN Type to another VNet with a PolicyBased VPN type?</span></span>

<span data-ttu-id="3e923-137">아니요, 두 가상 네트워크는 모두 경로 기반(이전 명칭: 동적 라우팅) VPN을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e923-137">No, both virtual networks MUST be using route-based (previously called Dynamic Routing) VPNs.</span></span>

### <a name="do-vpn-tunnels-share-bandwidth"></a><span data-ttu-id="3e923-138">VPN 터널은 대역폭을 공유하나요?</span><span class="sxs-lookup"><span data-stu-id="3e923-138">Do VPN tunnels share bandwidth?</span></span>

<span data-ttu-id="3e923-139">예.</span><span class="sxs-lookup"><span data-stu-id="3e923-139">Yes.</span></span> <span data-ttu-id="3e923-140">가상 네트워크의 모든 VPN 터널은 Azure VPN 게이트웨이의 사용 가능한 대역폭 및 Azure의 동일 VPN 게이트웨이 작동 시간 SLA를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="3e923-140">All VPN tunnels of the virtual network share the available bandwidth on the Azure VPN gateway and the same VPN gateway uptime SLA in Azure.</span></span>

### <a name="are-redundant-tunnels-supported"></a><span data-ttu-id="3e923-141">중복 터널이 지원되나요?</span><span class="sxs-lookup"><span data-stu-id="3e923-141">Are redundant tunnels supported?</span></span>

<span data-ttu-id="3e923-142">하나의 가상 네트워크 게이트웨이를 active-active로 구성하면 한 쌍의 가상 네트워크 사이의 중복 터널이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e923-142">Redundant tunnels between a pair of virtual networks are supported when one virtual network gateway is configured as active-active.</span></span>

### <a name="can-i-have-overlapping-address-spaces-for-vnet-to-vnet-configurations"></a><span data-ttu-id="3e923-143">VNet 간 구성에 대해 겹치는 주소 공간을 가질 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="3e923-143">Can I have overlapping address spaces for VNet-to-VNet configurations?</span></span>

<span data-ttu-id="3e923-144">아니요.</span><span class="sxs-lookup"><span data-stu-id="3e923-144">No.</span></span> <span data-ttu-id="3e923-145">겹치는 IP 주소 범위를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e923-145">You can't have overlapping IP address ranges.</span></span>

### <a name="can-there-be-overlapping-address-spaces-among-connected-virtual-networks-and-on-premises-local-sites"></a><span data-ttu-id="3e923-146">연결된 가상 네트워크와 온-프레미스 로컬 사이트 사이에 겹치는 주소 공간이 있을 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="3e923-146">Can there be overlapping address spaces among connected virtual networks and on-premises local sites?</span></span>

<span data-ttu-id="3e923-147">아니요.</span><span class="sxs-lookup"><span data-stu-id="3e923-147">No.</span></span> <span data-ttu-id="3e923-148">겹치는 IP 주소 범위를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e923-148">You can't have overlapping IP address ranges.</span></span>



