<span data-ttu-id="f4890-101">다음 작업을 수행하기 전에 VNet과 게이트웨이 서브넷을 먼저 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4890-101">You must create a VNet and a gateway subnet first, before working on the following tasks.</span></span> <span data-ttu-id="f4890-102">자세한 내용은 [클래식 포털을 사용하여 가상 네트워크 구성](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4890-102">See the article [Configure a Virtual Network using the classic portal](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) for more information.</span></span>   

## <a name="add-a-gateway"></a><span data-ttu-id="f4890-103">게이트웨이를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f4890-103">Add a gateway</span></span>
<span data-ttu-id="f4890-104">다음 명령을 사용하여 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4890-104">Use the command below to create a gateway.</span></span> <span data-ttu-id="f4890-105">모든 값을 자신의 고유한 값으로 대체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4890-105">Be sure to substitute any values for your own.</span></span>

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-the-gateway-was-created"></a><span data-ttu-id="f4890-106">게이트웨이가 만들어졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f4890-106">Verify the gateway was created</span></span>
<span data-ttu-id="f4890-107">아래 명령을 사용하여 게이트웨이가 만들어졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f4890-107">Use the command below to verify that the gateway has been created.</span></span> <span data-ttu-id="f4890-108">또한 이 명령은 다른 작업에 필요한 게이트웨이 ID를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f4890-108">This command also retrieves the gateway ID, which you need for other operations.</span></span>

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a><span data-ttu-id="f4890-109">게이트웨이 크기 조정</span><span class="sxs-lookup"><span data-stu-id="f4890-109">Resize a gateway</span></span>
<span data-ttu-id="f4890-110">다양한 [게이트웨이 SKU](../articles/expressroute/expressroute-about-virtual-network-gateways.md)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4890-110">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="f4890-111">다음 명령을 사용하여 언제든지 게이트웨이 SKU를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f4890-111">You can use the following command to change the Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f4890-112">이 명령은 UltraPerformance 게이트웨이에는 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4890-112">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="f4890-113">게이트웨이를 UltraPerformance 게이트웨이로 변경하려면 먼저 기존 Express 경로 게이트웨이를 제거한 다음 새 UltraPerformance 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4890-113">To change your gateway to an UltraPerformance gateway, first remove the existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="f4890-114">게이트웨이를 UltraPerformance 게이트웨이에서 다운그레이드하려면 먼저 UltraPerformance 게이트웨이를 제거한 후 새 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4890-114">To downgrade your gateway from an UltraPerformance gateway, first remove the UltraPerformance gateway, and then create a new gateway.</span></span> 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a><span data-ttu-id="f4890-115">게이트웨이 제거</span><span class="sxs-lookup"><span data-stu-id="f4890-115">Remove a gateway</span></span>
<span data-ttu-id="f4890-116">다음 명령을 사용하여 게이트웨이를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f4890-116">Use the command below to remove a gateway</span></span>

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>