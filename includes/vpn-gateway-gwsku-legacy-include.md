<span data-ttu-id="d9f99-101">레거시(이전) VPN 게이트웨이 SKU는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d9f99-101">The legacy (old) VPN gateway SKUs are:</span></span>

* <span data-ttu-id="d9f99-102">Basic</span><span class="sxs-lookup"><span data-stu-id="d9f99-102">Basic</span></span>
* <span data-ttu-id="d9f99-103">Standard</span><span class="sxs-lookup"><span data-stu-id="d9f99-103">Standard</span></span>
* <span data-ttu-id="d9f99-104">HighPerformance</span><span class="sxs-lookup"><span data-stu-id="d9f99-104">HighPerformance</span></span>

<span data-ttu-id="d9f99-105">VPN Gateway는 UltraPerformance 게이트웨이 SKU를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d9f99-105">VPN Gateway does not use the UltraPerformance gateway SKU.</span></span> <span data-ttu-id="d9f99-106">UltraPerformance SKU에 대한 내용은 [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9f99-106">For information about the UltraPerformance SKU, see the [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) documentation.</span></span>

<span data-ttu-id="d9f99-107">이전 SKU를 사용할 경우 다음 사항을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f99-107">When working with the legacy SKUs, consider the following:</span></span>

* <span data-ttu-id="d9f99-108">정책 기반 VPN 유형을 사용하려는 경우 기본 SKU를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f99-108">If you want to use a PolicyBased VPN type, you must use the Basic SKU.</span></span> <span data-ttu-id="d9f99-109">정책 기반 VPN(이전에는 정적 라우팅이라고 함)은 다른 SKU에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d9f99-109">PolicyBased VPNs (previously called Static Routing) are not supported on any other SKU.</span></span>
* <span data-ttu-id="d9f99-110">BGP는 기본 SKU에 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d9f99-110">BGP is not supported on the Basic SKU.</span></span>
* <span data-ttu-id="d9f99-111">ExpressRoute-VPN Gateway 공존 구성은 기본 SKU에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d9f99-111">ExpressRoute-VPN Gateway coexist configurations are not supported on the Basic SKU.</span></span>
* <span data-ttu-id="d9f99-112">활성-활성 S2S VPN Gateway 연결은 HighPerformance SKU에서만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9f99-112">Active-active S2S VPN Gateway connections can be configured on the HighPerformance SKU only.</span></span>