<span data-ttu-id="0441b-101">가상 네트워크 게이트웨이를 만들 때 사용하려는 게이트웨이 SKU를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0441b-101">When you create a virtual network gateway, you need to specify the gateway SKU that you want to use.</span></span> <span data-ttu-id="0441b-102">작업 부하, 처리량, 기능 및 SLA의 종류를 기반으로 하는 요구 사항을 충족하는 SKU를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0441b-102">Select the SKUs that satisfy your requirements based on the types of workloads, throughputs, features, and SLAs.</span></span>

[!INCLUDE [classic SKU](./vpn-gateway-classic-sku-support-include.md)]

[!INCLUDE [Aggregated throughput by SKU](./vpn-gateway-table-gwtype-aggtput-include.md)]

###  <span data-ttu-id="0441b-103"><a name="workloads"></a>프로덕션 *vs.* 개발=테스트 워크로드</span><span class="sxs-lookup"><span data-stu-id="0441b-103"><a name="workloads"></a>Production *vs.* Dev-Test Workloads</span></span>

<span data-ttu-id="0441b-104">SLA 및 기능 집합의 차이로 인해 프로덕션 *vs.* 개발-테스트에 다음과 같은 SKU를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0441b-104">Due to the differences in SLAs and feature sets, we recommend the following SKUs for production *vs.* dev-test:</span></span>

| <span data-ttu-id="0441b-105">**워크로드**</span><span class="sxs-lookup"><span data-stu-id="0441b-105">**Workload**</span></span>                       | <span data-ttu-id="0441b-106">**SKU**</span><span class="sxs-lookup"><span data-stu-id="0441b-106">**SKUs**</span></span>               |
| ---                                | ---                    |
| <span data-ttu-id="0441b-107">**프로덕션, 중요한 워크로드**</span><span class="sxs-lookup"><span data-stu-id="0441b-107">**Production, critical workloads**</span></span> | <span data-ttu-id="0441b-108">VpnGw1, VpnGw2, VpnGw3</span><span class="sxs-lookup"><span data-stu-id="0441b-108">VpnGw1, VpnGw2, VpnGw3</span></span> |
| <span data-ttu-id="0441b-109">**개발-테스트 또는 개념 증명**</span><span class="sxs-lookup"><span data-stu-id="0441b-109">**Dev-test or proof of concept**</span></span>   | <span data-ttu-id="0441b-110">Basic</span><span class="sxs-lookup"><span data-stu-id="0441b-110">Basic</span></span>                  |
|                                    |                        |

<span data-ttu-id="0441b-111">이전 SKU를 사용하는 경우 프로덕션 SKU 권장 사항은 표준 및 HighPerformance SKU입니다.</span><span class="sxs-lookup"><span data-stu-id="0441b-111">If you are using the old SKUs, the production SKU recommendations are Standard and HighPerformance SKUs.</span></span> <span data-ttu-id="0441b-112">이전 SKU에 대한 정보는 [게이트웨이 SKU(이전 SKU)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0441b-112">For information on the old SKUs, see [Gateway SKUs (legacy SKUs)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).</span></span>

###  <span data-ttu-id="0441b-113"><a name="feature"></a>게이트웨이 SKU 기능 집합</span><span class="sxs-lookup"><span data-stu-id="0441b-113"><a name="feature"></a>Gateway SKU feature sets</span></span>

<span data-ttu-id="0441b-114">새 게이트웨이 SKU는 게이트웨이에서 제공한 기능 집합을 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="0441b-114">The new gateway SKUs streamline the feature sets offered on the gateways:</span></span>

| <span data-ttu-id="0441b-115">**SKU**</span><span class="sxs-lookup"><span data-stu-id="0441b-115">**SKU**</span></span>| <span data-ttu-id="0441b-116">**기능**</span><span class="sxs-lookup"><span data-stu-id="0441b-116">**Features**</span></span>|
| ---    | ---         |
|<span data-ttu-id="0441b-117">**Basic**</span><span class="sxs-lookup"><span data-stu-id="0441b-117">**Basic**</span></span>   | <span data-ttu-id="0441b-118">**경로 기반 VPN**: P2S를 사용하는 10개의 터널</span><span class="sxs-lookup"><span data-stu-id="0441b-118">**Route-based VPN**: 10 tunnels with P2S</span></span><br><br><span data-ttu-id="0441b-119">**정책 기반 VPN**: (IKEv1): 1개의 터널. P2S 없음</span><span class="sxs-lookup"><span data-stu-id="0441b-119">**Policy-based VPN**: (IKEv1): 1 tunnel; no P2S</span></span>|
| <span data-ttu-id="0441b-120">**VpnGw1, VpnGw2 및 VpnGw3**</span><span class="sxs-lookup"><span data-stu-id="0441b-120">**VpnGw1, VpnGw2, and VpnGw3**</span></span> | <span data-ttu-id="0441b-121">**경로 기반 VPN**: 최대 30개의 터널(*),P2S, BGP, 활성-활성, 사용자 지정 IPsec/IKE 정책, ExpressRoute/VPN 공존</span><span class="sxs-lookup"><span data-stu-id="0441b-121">**Route-based VPN**: up to 30 tunnels (*), P2S, BGP, active-active, custom IPsec/IKE policy, ExpressRoute/VPN co-existence</span></span> |
|        |             |

<span data-ttu-id="0441b-122">(*) 경로 기반 VPN 게이트웨이(VpnGw1, VpnGw2, VpnGw3)를 여러 온-프레미스 정책 기반 방화벽 장치에 연결하도록 "PolicyBasedTrafficSelectors"를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0441b-122">(*) You can configure "PolicyBasedTrafficSelectors" to connect a route-based VPN gateway (VpnGw1, VpnGw2, VpnGw3) to multiple on-premises policy-based firewall devices.</span></span> <span data-ttu-id="0441b-123">자세한 내용은 [PowerShell을 사용하여 VPN Gateway를 여러 온-프레미스 정책 기반 VPN 장치에 연결](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0441b-123">Refer to [Connect VPN gateways to multiple on-premises policy-based VPN devices using PowerShell](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) for details.</span></span>

###  <span data-ttu-id="0441b-124"><a name="resize"></a>게이트웨이 SKU 크기 조정</span><span class="sxs-lookup"><span data-stu-id="0441b-124"><a name="resize"></a>Resizing gateway SKUs</span></span>

1. <span data-ttu-id="0441b-125">VpnGw1, VpnGw2와 VpnGw3 SKU 간에 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0441b-125">You can resize between VpnGw1, VpnGw2, and VpnGw3 SKUs.</span></span>
2. <span data-ttu-id="0441b-126">이전 게이트웨이 SKU로 작동하는 경우 Basic, Standard 및 HighPerformance SKU 간에 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0441b-126">When working with the old gateway SKUs, you can resize between Basic, Standard, and HighPerformance SKUs.</span></span>
2. <span data-ttu-id="0441b-127">Basic/Standard/HighPerformance SKU에서 새 VpnGw1/VpnGw2/VpnGw3 SKU까지 크기를 조정할 수 **없습니다**.</span><span class="sxs-lookup"><span data-stu-id="0441b-127">You **cannot** resize from Basic/Standard/HighPerformance SKUs to the new VpnGw1/VpnGw2/VpnGw3 SKUs.</span></span> <span data-ttu-id="0441b-128">대신 새 SKU으로 [마이그레이션](#migrate)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0441b-128">You must, instead, [migrate](#migrate) to the new SKUs.</span></span>

###  <span data-ttu-id="0441b-129"><a name="migrate"></a>이전 SKU에서 새 SKU로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="0441b-129"><a name="migrate"></a>Migrating from old SKUs to the new SKUs</span></span>

[!INCLUDE [Migrate SKU](./vpn-gateway-migrate-legacy-sku-include.md)]
