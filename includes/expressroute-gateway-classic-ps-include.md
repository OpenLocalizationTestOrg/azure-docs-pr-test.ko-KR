<span data-ttu-id="c1f0a-101">만들어야 VNet 및 게이트웨이 서브넷 먼저 작업 hello 다음 작업을 계속 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f0a-101">You must create a VNet and a gateway subnet first, before working on hello following tasks.</span></span> <span data-ttu-id="c1f0a-102">Hello 문서 참조 [hello 클래식 포털을 사용 하 여 가상 네트워크 구성](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f0a-102">See hello article [Configure a Virtual Network using hello classic portal](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) for more information.</span></span>   

## <a name="add-a-gateway"></a><span data-ttu-id="c1f0a-103">게이트웨이를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f0a-103">Add a gateway</span></span>
<span data-ttu-id="c1f0a-104">Toocreate 게이트웨이 아래 hello 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f0a-104">Use hello command below toocreate a gateway.</span></span> <span data-ttu-id="c1f0a-105">있는지 toosubstitute 자신만의 모든 값 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c1f0a-105">Be sure toosubstitute any values for your own.</span></span>

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-hello-gateway-was-created"></a><span data-ttu-id="c1f0a-106">Hello 게이트웨이가 생성 되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="c1f0a-106">Verify hello gateway was created</span></span>
<span data-ttu-id="c1f0a-107">게이트웨이 hello tooverify 아래 hello 명령은 사용 하 여 생성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c1f0a-107">Use hello command below tooverify that hello gateway has been created.</span></span> <span data-ttu-id="c1f0a-108">이 명령은 다른 작업에 필요한 hello 게이트웨이 ID를도 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f0a-108">This command also retrieves hello gateway ID, which you need for other operations.</span></span>

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a><span data-ttu-id="c1f0a-109">게이트웨이 크기 조정</span><span class="sxs-lookup"><span data-stu-id="c1f0a-109">Resize a gateway</span></span>
<span data-ttu-id="c1f0a-110">다양한 [게이트웨이 SKU](../articles/expressroute/expressroute-about-virtual-network-gateways.md)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1f0a-110">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="c1f0a-111">언제 든 지 명령 toochange hello 게이트웨이 SKU 다음 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1f0a-111">You can use hello following command toochange hello Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c1f0a-112">이 명령은 UltraPerformance 게이트웨이에는 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c1f0a-112">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="c1f0a-113">toochange 게이트웨이 tooan UltraPerformance 게이트웨이 먼저 hello 기존 express 경로 게이트웨이 제거 하 고 새 UltraPerformance 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c1f0a-113">toochange your gateway tooan UltraPerformance gateway, first remove hello existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="c1f0a-114">toodowngrade UltraPerformance 게이트웨이에서 게이트웨이 먼저 제거 UltraPerformance 게이트웨이 hello 한 다음 새 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c1f0a-114">toodowngrade your gateway from an UltraPerformance gateway, first remove hello UltraPerformance gateway, and then create a new gateway.</span></span> 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a><span data-ttu-id="c1f0a-115">게이트웨이 제거</span><span class="sxs-lookup"><span data-stu-id="c1f0a-115">Remove a gateway</span></span>
<span data-ttu-id="c1f0a-116">Tooremove 게이트웨이 아래 hello 명령을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c1f0a-116">Use hello command below tooremove a gateway</span></span>

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>