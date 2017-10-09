### <span data-ttu-id="00c0a-101"><a name="gwipnoconnection"></a>toomodify hello 로컬 네트워크 게이트웨이 'GatewayIpAddress'-게이트웨이 연결 없음</span><span class="sxs-lookup"><span data-stu-id="00c0a-101"><a name="gwipnoconnection"></a> toomodify hello local network gateway 'GatewayIpAddress' - no gateway connection</span></span>

<span data-ttu-id="00c0a-102">원하는 tooconnect toohas hello VPN 장치에 공용 IP 주소 변경 된 경우 toomodify hello 로컬 네트워크 게이트웨이 tooreflect 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00c0a-102">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="00c0a-103">Hello 예제 toomodify 게이트웨이 연결 되어 있지 않은 로컬 네트워크 게이트웨이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="00c0a-103">Use hello example toomodify a local network gateway that does not have a gateway connection.</span></span>

<span data-ttu-id="00c0a-104">이 값을 수정할 때는 hello 주소 접두사 hello에도 수정할 수 있습니다 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="00c0a-104">When modifying this value, you can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="00c0a-105">로컬 네트워크 게이트웨이의 순서 toooverwrite hello에 대 한 현재 설정에 있는지 toouse hello 기존 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00c0a-105">Be sure toouse hello existing name of your local network gateway in order toooverwrite hello current settings.</span></span> <span data-ttu-id="00c0a-106">다른 이름을 사용 하는 경우 새 로컬 네트워크 게이트웨이 만들을 덮어쓰지 않고 기존 hello 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00c0a-106">If you use a different name, you create a new local network gateway, instead of overwriting hello existing one.</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <span data-ttu-id="00c0a-107"><a name="gwipwithconnection"></a>toomodify hello 로컬 네트워크 게이트웨이 'GatewayIpAddress'-기존 게이트웨이 연결</span><span class="sxs-lookup"><span data-stu-id="00c0a-107"><a name="gwipwithconnection"></a>toomodify hello local network gateway 'GatewayIpAddress' - existing gateway connection</span></span>

<span data-ttu-id="00c0a-108">원하는 tooconnect toohas hello VPN 장치에 공용 IP 주소 변경 된 경우 toomodify hello 로컬 네트워크 게이트웨이 tooreflect 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00c0a-108">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="00c0a-109">게이트웨이 연결을 이미 있는 경우 먼저 tooremove hello 연결을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00c0a-109">If a gateway connection already exists, you first need tooremove hello connection.</span></span> <span data-ttu-id="00c0a-110">Hello 연결을 제거한 후 hello 게이트웨이 IP 주소를 수정할 수 있으며 새 연결을 다시 만드십시오.</span><span class="sxs-lookup"><span data-stu-id="00c0a-110">After hello connection is removed, you can modify hello gateway IP address and recreate a new connection.</span></span> <span data-ttu-id="00c0a-111">Hello에 hello 주소 접두사를 수정할 수도 있습니다 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="00c0a-111">You can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="00c0a-112">이로 인해 VPN 연결에 약간의 가동 중지 시간이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="00c0a-112">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="00c0a-113">Hello 게이트웨이 IP 주소를 수정할 때 toodelete hello VPN 게이트웨이 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="00c0a-113">When modifying hello gateway IP address, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="00c0a-114">Tooremove hello 연결을 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00c0a-114">You only need tooremove hello connection.</span></span>
 

1. <span data-ttu-id="00c0a-115">Hello 연결을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="00c0a-115">Remove hello connection.</span></span> <span data-ttu-id="00c0a-116">' Get AzureRmVirtualNetworkGatewayConnection' hello cmdlet을 사용 하 여 연결의 hello 이름임을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00c0a-116">You can find hello name of your connection by using hello 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="00c0a-117">Hello 'GatewayIpAddress' 값을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00c0a-117">Modify hello 'GatewayIpAddress' value.</span></span> <span data-ttu-id="00c0a-118">Hello에 hello 주소 접두사를 수정할 수도 있습니다 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="00c0a-118">You can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="00c0a-119">로컬 네트워크 게이트웨이 toooverwrite hello 현재 설정의 있는지 toouse hello 기존 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00c0a-119">Be sure toouse hello existing name of your local network gateway toooverwrite hello current settings.</span></span> <span data-ttu-id="00c0a-120">이렇게 하지 않으면 새 로컬 네트워크 게이트웨이 만들을 덮어쓰지 않고 기존 hello 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00c0a-120">If you don't, you create a new local network gateway, instead of overwriting hello existing one.</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. <span data-ttu-id="00c0a-121">Hello 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00c0a-121">Create hello connection.</span></span> <span data-ttu-id="00c0a-122">이 예제에서는 IPsec 연결 형식을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="00c0a-122">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="00c0a-123">연결을 다시 만들 때 지정 된 hello 연결 형식 구성에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="00c0a-123">When you recreate your connection, use hello connection type that is specified for your configuration.</span></span> <span data-ttu-id="00c0a-124">추가 연결 형식에 대 한 참조 hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) 페이지.</span><span class="sxs-lookup"><span data-stu-id="00c0a-124">For additional connection types, see hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>  <span data-ttu-id="00c0a-125">tooobtain hello VirtualNetworkGateway 이름 hello ' Get AzureRmVirtualNetworkGateway' cmdlet을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00c0a-125">tooobtain hello VirtualNetworkGateway name, you can run hello 'Get-AzureRmVirtualNetworkGateway' cmdlet.</span></span>
   
    <span data-ttu-id="00c0a-126">Hello 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00c0a-126">Set hello variables.</span></span>

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    <span data-ttu-id="00c0a-127">Hello 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00c0a-127">Create hello connection.</span></span>

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```