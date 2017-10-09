<span data-ttu-id="af78c-101">VNet 대 VNet FAQ hello tooVPN 게이트웨이 연결을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="af78c-101">hello VNet-to-VNet FAQ applies tooVPN Gateway connections.</span></span> <span data-ttu-id="af78c-102">VNet 피어링을 찾으려면 [가상 네트워크 피어링](../articles/virtual-network/virtual-network-peering-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af78c-102">If you are looking for VNet Peering, see [Virtual Network Peering](../articles/virtual-network/virtual-network-peering-overview.md)</span></span>

### <a name="does-azure-charge-for-traffic-between-vnets"></a><span data-ttu-id="af78c-103">Azure는 VNet 간 트래픽에 요금을 청구하나요?</span><span class="sxs-lookup"><span data-stu-id="af78c-103">Does Azure charge for traffic between VNets?</span></span>

<span data-ttu-id="af78c-104">Hello 내에서 VNet 대 VNet 트래픽이 동일 지역은 VPN 게이트웨이 연결을 사용 하는 경우 양방향에 대 한 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="af78c-104">VNet-to-VNet traffic within hello same region is free for both directions when using a VPN gateway connection.</span></span> <span data-ttu-id="af78c-105">지역 VNet 대 VNet 송신 간 트래픽 hello 소스 지역을 기반으로 하는 hello 간 VNet 아웃 바운드 데이터 전송 속도 대금이 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af78c-105">Cross region VNet-to-VNet egress traffic is charged with hello outbound inter-VNet data transfer rates based on hello source regions.</span></span> <span data-ttu-id="af78c-106">Toohello 참조 [VPN 게이트웨이 가격 책정 페이지](https://azure.microsoft.com/pricing/details/vpn-gateway/) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="af78c-106">Refer toohello [VPN Gateway pricing page](https://azure.microsoft.com/pricing/details/vpn-gateway/) for details.</span></span> <span data-ttu-id="af78c-107">VNet 피어 링을 보다는 VPN 게이트웨이 사용 하 여 Vnet을 연결 하는 경우 참조 hello [가격 책정 페이지 가상 네트워크](https://azure.microsoft.com/pricing/details/virtual-network/)합니다.</span><span class="sxs-lookup"><span data-stu-id="af78c-107">If you are connecting your VNets using VNet Peering, rather than VPN Gateway, see hello [Virtual Network pricing page](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>

### <a name="does-vnet-to-vnet-traffic-travel-across-hello-internet"></a><span data-ttu-id="af78c-108">VNet 대 VNet 트래픽이 hello 인터넷 거쳐야가?</span><span class="sxs-lookup"><span data-stu-id="af78c-108">Does VNet-to-VNet traffic travel across hello Internet?</span></span>

<span data-ttu-id="af78c-109">아니요.</span><span class="sxs-lookup"><span data-stu-id="af78c-109">No.</span></span> <span data-ttu-id="af78c-110">VNet 대 VNet 트래픽이 hello backbone Microsoft Azure hello 인터넷 하지을 통과 합니다.</span><span class="sxs-lookup"><span data-stu-id="af78c-110">VNet-to-VNet traffic travels across hello Microsoft Azure backbone, not hello Internet.</span></span>

### <a name="is-vnet-to-vnet-traffic-secure"></a><span data-ttu-id="af78c-111">VNet 간 트래픽은 안전한가요?</span><span class="sxs-lookup"><span data-stu-id="af78c-111">Is VNet-to-VNet traffic secure?</span></span>

<span data-ttu-id="af78c-112">예, IPsec/IKE 암호화로 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="af78c-112">Yes, it is protected by IPsec/IKE encryption.</span></span>

### <a name="do-i-need-a-vpn-device-tooconnect-vnets-together"></a><span data-ttu-id="af78c-113">VPN 장치 tooconnect Vnet을 함께 필요 수행 합니까?</span><span class="sxs-lookup"><span data-stu-id="af78c-113">Do I need a VPN device tooconnect VNets together?</span></span>

<span data-ttu-id="af78c-114">아니요.</span><span class="sxs-lookup"><span data-stu-id="af78c-114">No.</span></span> <span data-ttu-id="af78c-115">크로스-프레미스 연결이 필요한 경우가 아니면 여러 Azure 가상 네트워크를 함께 연결할 때 VPN 장치는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af78c-115">Connecting multiple Azure virtual networks together doesn't require a VPN device unless cross-premises connectivity is required.</span></span>

### <a name="do-my-vnets-need-toobe-in-hello-same-region"></a><span data-ttu-id="af78c-116">Vnet 내 hello에 toobe 필요가 동일한 지역?</span><span class="sxs-lookup"><span data-stu-id="af78c-116">Do my VNets need toobe in hello same region?</span></span>

<span data-ttu-id="af78c-117">아니요.</span><span class="sxs-lookup"><span data-stu-id="af78c-117">No.</span></span> <span data-ttu-id="af78c-118">hello에 hello 가상 네트워크 수 같거나 다른 Azure 지역 (위치).</span><span class="sxs-lookup"><span data-stu-id="af78c-118">hello virtual networks can be in hello same or different Azure regions (locations).</span></span>

### <a name="if-hello-vnets-are-not-in-hello-same-subscription-do-hello-subscriptions-need-toobe-associated-with-hello-same-ad-tenant"></a><span data-ttu-id="af78c-119">Hello Vnet에는 없는 경우 hello 동일한 구독을 hello 구독 필요가 hello 동일한 AD 테 넌 트와 연결 된 toobe?</span><span class="sxs-lookup"><span data-stu-id="af78c-119">If hello VNets are not in hello same subscription, do hello subscriptions need toobe associated with hello same AD tenant?</span></span>

<span data-ttu-id="af78c-120">아니요.</span><span class="sxs-lookup"><span data-stu-id="af78c-120">No.</span></span>

### <a name="can-i-use-vnet-to-vnet-along-with-multi-site-connections"></a><span data-ttu-id="af78c-121">VNet간 연결을 멀티 사이트 연결과 함께 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="af78c-121">Can I use VNet-to-VNet along with multi-site connections?</span></span>

<span data-ttu-id="af78c-122">예.</span><span class="sxs-lookup"><span data-stu-id="af78c-122">Yes.</span></span> <span data-ttu-id="af78c-123">가상 네트워크 연결을 다중 사이트 VPN과 동시에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af78c-123">Virtual network connectivity can be used simultaneously with multi-site VPNs.</span></span>

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a><span data-ttu-id="af78c-124">하나의 가상 네트워크에 연결할 수 있는 온-프레미스 사이트 및 가상 네트워크 수는 어떻게 됩니까?</span><span class="sxs-lookup"><span data-stu-id="af78c-124">How many on-premises sites and virtual networks can one virtual network connect to?</span></span>

<span data-ttu-id="af78c-125">[게이트웨이 요구 사항](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements) 테이블을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af78c-125">See [Gateway requirements](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements) table.</span></span>

### <a name="can-i-use-vnet-to-vnet-tooconnect-vms-or-cloud-services-outside-of-a-vnet"></a><span data-ttu-id="af78c-126">VNet 대 VNet tooconnect Vm을 사용 하거나 클라우드 서비스는 VNet 외부에서 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="af78c-126">Can I use VNet-to-VNet tooconnect VMs or cloud services outside of a VNet?</span></span>

<span data-ttu-id="af78c-127">아니요.</span><span class="sxs-lookup"><span data-stu-id="af78c-127">No.</span></span> <span data-ttu-id="af78c-128">VNet 간 연결은 가상 네트워크 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="af78c-128">VNet-to-VNet supports connecting virtual networks.</span></span> <span data-ttu-id="af78c-129">가상 네트워크에 포함되어 있지 않은 가상 컴퓨터 또는 클라우드 서비스 연결은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af78c-129">It does not support connecting virtual machines or cloud services that are not in a virtual network.</span></span>

### <a name="can-a-cloud-service-or-a-load-balancing-endpoint-span-vnets"></a><span data-ttu-id="af78c-130">클라우드 서비스 또는 부하 분산 끝점이 VNet까지 이어지나요?</span><span class="sxs-lookup"><span data-stu-id="af78c-130">Can a cloud service or a load balancing endpoint span VNets?</span></span>

<span data-ttu-id="af78c-131">아니요.</span><span class="sxs-lookup"><span data-stu-id="af78c-131">No.</span></span> <span data-ttu-id="af78c-132">클라우드 서비스 또는 부하 분산 끝점은 연결되어 있더라도 여러 가상 네트워크에 분산될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="af78c-132">A cloud service or a load balancing endpoint can't span across virtual networks, even if they are connected together.</span></span>

### <a name="can-i-used-a-policybased-vpn-type-for-vnet-to-vnet-or-multi-site-connections"></a><span data-ttu-id="af78c-133">VNet 간 또는 멀티 사이트 연결에 PolicyBased VPN 유형을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="af78c-133">Can I used a PolicyBased VPN type for VNet-to-VNet or Multi-Site connections?</span></span>

<span data-ttu-id="af78c-134">아니요.</span><span class="sxs-lookup"><span data-stu-id="af78c-134">No.</span></span> <span data-ttu-id="af78c-135">VNet 간 연결 및 멀티 사이트 연결에는 RouteBased(이전 명칭: 동적 라우팅) VPN 유형의 Azure VPN 게이트웨이가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="af78c-135">VNet-to-VNet and Multi-Site connections require Azure VPN gateways with RouteBased (previously called Dynamic Routing) VPN types.</span></span>

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-tooanother-vnet-with-a-policybased-vpn-type"></a><span data-ttu-id="af78c-136">연결할 수 있습니까 VNet RouteBased VPN 유형을 tooanother VNet으로 PolicyBased VPN 형식과?</span><span class="sxs-lookup"><span data-stu-id="af78c-136">Can I connect a VNet with a RouteBased VPN Type tooanother VNet with a PolicyBased VPN type?</span></span>

<span data-ttu-id="af78c-137">아니요, 두 가상 네트워크는 모두 경로 기반(이전 명칭: 동적 라우팅) VPN을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af78c-137">No, both virtual networks MUST be using route-based (previously called Dynamic Routing) VPNs.</span></span>

### <a name="do-vpn-tunnels-share-bandwidth"></a><span data-ttu-id="af78c-138">VPN 터널은 대역폭을 공유하나요?</span><span class="sxs-lookup"><span data-stu-id="af78c-138">Do VPN tunnels share bandwidth?</span></span>

<span data-ttu-id="af78c-139">예.</span><span class="sxs-lookup"><span data-stu-id="af78c-139">Yes.</span></span> <span data-ttu-id="af78c-140">Hello 가상 네트워크의 모든 VPN 터널 hello hello Azure VPN 게이트웨이 사용 가능한 대역폭을 공유 하 고 Azure에서 동일한 VPN 게이트웨이 작동 시간 SLA hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="af78c-140">All VPN tunnels of hello virtual network share hello available bandwidth on hello Azure VPN gateway and hello same VPN gateway uptime SLA in Azure.</span></span>

### <a name="are-redundant-tunnels-supported"></a><span data-ttu-id="af78c-141">중복 터널이 지원되나요?</span><span class="sxs-lookup"><span data-stu-id="af78c-141">Are redundant tunnels supported?</span></span>

<span data-ttu-id="af78c-142">하나의 가상 네트워크 게이트웨이를 active-active로 구성하면 한 쌍의 가상 네트워크 사이의 중복 터널이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="af78c-142">Redundant tunnels between a pair of virtual networks are supported when one virtual network gateway is configured as active-active.</span></span>

### <a name="can-i-have-overlapping-address-spaces-for-vnet-to-vnet-configurations"></a><span data-ttu-id="af78c-143">VNet 간 구성에 대해 겹치는 주소 공간을 가질 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="af78c-143">Can I have overlapping address spaces for VNet-to-VNet configurations?</span></span>

<span data-ttu-id="af78c-144">아니요.</span><span class="sxs-lookup"><span data-stu-id="af78c-144">No.</span></span> <span data-ttu-id="af78c-145">겹치는 IP 주소 범위를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af78c-145">You can't have overlapping IP address ranges.</span></span>

### <a name="can-there-be-overlapping-address-spaces-among-connected-virtual-networks-and-on-premises-local-sites"></a><span data-ttu-id="af78c-146">연결된 가상 네트워크와 온-프레미스 로컬 사이트 사이에 겹치는 주소 공간이 있을 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="af78c-146">Can there be overlapping address spaces among connected virtual networks and on-premises local sites?</span></span>

<span data-ttu-id="af78c-147">아니요.</span><span class="sxs-lookup"><span data-stu-id="af78c-147">No.</span></span> <span data-ttu-id="af78c-148">겹치는 IP 주소 범위를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af78c-148">You can't have overlapping IP address ranges.</span></span>



