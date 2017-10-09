<span data-ttu-id="e27e1-101">가상 네트워크 게이트웨이 만들 때 toospecify hello 게이트웨이 SKU toouse 되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e27e1-101">When you create a virtual network gateway, you need toospecify hello gateway SKU that you want toouse.</span></span> <span data-ttu-id="e27e1-102">작업 부하, 처리량, 기능 및 Sla의 hello 유형을 기반으로 하는 요구 사항을 충족 하는 hello Sku를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e27e1-102">Select hello SKUs that satisfy your requirements based on hello types of workloads, throughputs, features, and SLAs.</span></span>

[!INCLUDE [classic SKU](./vpn-gateway-classic-sku-support-include.md)]

[!INCLUDE [Aggregated throughput by SKU](./vpn-gateway-table-gwtype-aggtput-include.md)]

###  <span data-ttu-id="e27e1-103"><a name="workloads"></a>프로덕션 *vs.* 개발=테스트 워크로드</span><span class="sxs-lookup"><span data-stu-id="e27e1-103"><a name="workloads"></a>Production *vs.* Dev-Test Workloads</span></span>

<span data-ttu-id="e27e1-104">프로덕션에 대 한 Sku 다음 hello Sla 및 기능 집합, toohello 차이 때문 권장 *비교* 개발 테스트:</span><span class="sxs-lookup"><span data-stu-id="e27e1-104">Due toohello differences in SLAs and feature sets, we recommend hello following SKUs for production *vs.* dev-test:</span></span>

| <span data-ttu-id="e27e1-105">**워크로드**</span><span class="sxs-lookup"><span data-stu-id="e27e1-105">**Workload**</span></span>                       | <span data-ttu-id="e27e1-106">**SKU**</span><span class="sxs-lookup"><span data-stu-id="e27e1-106">**SKUs**</span></span>               |
| ---                                | ---                    |
| <span data-ttu-id="e27e1-107">**프로덕션, 중요한 워크로드**</span><span class="sxs-lookup"><span data-stu-id="e27e1-107">**Production, critical workloads**</span></span> | <span data-ttu-id="e27e1-108">VpnGw1, VpnGw2, VpnGw3</span><span class="sxs-lookup"><span data-stu-id="e27e1-108">VpnGw1, VpnGw2, VpnGw3</span></span> |
| <span data-ttu-id="e27e1-109">**개발-테스트 또는 개념 증명**</span><span class="sxs-lookup"><span data-stu-id="e27e1-109">**Dev-test or proof of concept**</span></span>   | <span data-ttu-id="e27e1-110">Basic</span><span class="sxs-lookup"><span data-stu-id="e27e1-110">Basic</span></span>                  |
|                                    |                        |

<span data-ttu-id="e27e1-111">이전 hello를 사용 하는 표준 및 HighPerformance Sku Sku, hello 프로덕션 SKU 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e27e1-111">If you are using hello old SKUs, hello production SKU recommendations are Standard and HighPerformance SKUs.</span></span> <span data-ttu-id="e27e1-112">Hello에 대 한 내용은 이전 Sku 참조 [게이트웨이 Sku (레거시 Sku)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e27e1-112">For information on hello old SKUs, see [Gateway SKUs (legacy SKUs)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).</span></span>

###  <span data-ttu-id="e27e1-113"><a name="feature"></a>게이트웨이 SKU 기능 집합</span><span class="sxs-lookup"><span data-stu-id="e27e1-113"><a name="feature"></a>Gateway SKU feature sets</span></span>

<span data-ttu-id="e27e1-114">hello 새로운 게이트웨이 Sku 약식 hello 기능 집합이 제공 hello 게이트웨이:</span><span class="sxs-lookup"><span data-stu-id="e27e1-114">hello new gateway SKUs streamline hello feature sets offered on hello gateways:</span></span>

| <span data-ttu-id="e27e1-115">**SKU**</span><span class="sxs-lookup"><span data-stu-id="e27e1-115">**SKU**</span></span>| <span data-ttu-id="e27e1-116">**기능**</span><span class="sxs-lookup"><span data-stu-id="e27e1-116">**Features**</span></span>|
| ---    | ---         |
|<span data-ttu-id="e27e1-117">**Basic**</span><span class="sxs-lookup"><span data-stu-id="e27e1-117">**Basic**</span></span>   | <span data-ttu-id="e27e1-118">**경로 기반 VPN**: P2S를 사용하는 10개의 터널</span><span class="sxs-lookup"><span data-stu-id="e27e1-118">**Route-based VPN**: 10 tunnels with P2S</span></span><br><br><span data-ttu-id="e27e1-119">**정책 기반 VPN**: (IKEv1): 1개의 터널. P2S 없음</span><span class="sxs-lookup"><span data-stu-id="e27e1-119">**Policy-based VPN**: (IKEv1): 1 tunnel; no P2S</span></span>|
| <span data-ttu-id="e27e1-120">**VpnGw1, VpnGw2 및 VpnGw3**</span><span class="sxs-lookup"><span data-stu-id="e27e1-120">**VpnGw1, VpnGw2, and VpnGw3**</span></span> | <span data-ttu-id="e27e1-121">**경로 기반 VPN**: P2S, BGP, too30 터널 (*)을 활성-활성, 사용자 지정 IPsec/IKE 정책, ExpressRoute/v p N 공존</span><span class="sxs-lookup"><span data-stu-id="e27e1-121">**Route-based VPN**: up too30 tunnels (*), P2S, BGP, active-active, custom IPsec/IKE policy, ExpressRoute/VPN co-existence</span></span> |
|        |             |

<span data-ttu-id="e27e1-122">(*) "PolicyBasedTrafficSelectors" tooconnect는 경로 기반 VPN 게이트웨이 (VpnGw1, VpnGw2, VpnGw3) toomultiple 온-프레미스 방화벽 정책 기반 장치를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e27e1-122">(*) You can configure "PolicyBasedTrafficSelectors" tooconnect a route-based VPN gateway (VpnGw1, VpnGw2, VpnGw3) toomultiple on-premises policy-based firewall devices.</span></span> <span data-ttu-id="e27e1-123">너무 참조[연결 VPN 게이트웨이 toomultiple 온-프레미스 PowerShell을 사용 하 여 정책 기반 VPN 장치](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="e27e1-123">Refer too[Connect VPN gateways toomultiple on-premises policy-based VPN devices using PowerShell](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) for details.</span></span>

###  <span data-ttu-id="e27e1-124"><a name="resize"></a>게이트웨이 SKU 크기 조정</span><span class="sxs-lookup"><span data-stu-id="e27e1-124"><a name="resize"></a>Resizing gateway SKUs</span></span>

1. <span data-ttu-id="e27e1-125">VpnGw1, VpnGw2와 VpnGw3 SKU 간에 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e27e1-125">You can resize between VpnGw1, VpnGw2, and VpnGw3 SKUs.</span></span>
2. <span data-ttu-id="e27e1-126">Hello 오래 된 게이트웨이 Sku 사용할 때는 Basic, Standard 및 HighPerformance Sku 간에 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e27e1-126">When working with hello old gateway SKUs, you can resize between Basic, Standard, and HighPerformance SKUs.</span></span>
2. <span data-ttu-id="e27e1-127">하면 **없습니다** HighPerformance/Standard/Basic Sku toohello에서 크기 조정 새 VpnGw1/VpnGw2/VpnGw3 Sku입니다.</span><span class="sxs-lookup"><span data-stu-id="e27e1-127">You **cannot** resize from Basic/Standard/HighPerformance SKUs toohello new VpnGw1/VpnGw2/VpnGw3 SKUs.</span></span> <span data-ttu-id="e27e1-128">대신, 해야 [마이그레이션할](#migrate) toohello 새 Sku입니다.</span><span class="sxs-lookup"><span data-stu-id="e27e1-128">You must, instead, [migrate](#migrate) toohello new SKUs.</span></span>

###  <span data-ttu-id="e27e1-129"><a name="migrate"></a>이전 Sku toohello에서 마이그레이션 새 Sku</span><span class="sxs-lookup"><span data-stu-id="e27e1-129"><a name="migrate"></a>Migrating from old SKUs toohello new SKUs</span></span>

[!INCLUDE [Migrate SKU](./vpn-gateway-migrate-legacy-sku-include.md)]
