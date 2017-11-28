### <span data-ttu-id="3f418-101"><a name="gwipnoconnection"></a> 로컬 네트워크 게이트웨이 'GatewayIpAddress'를 수정하려면 - 게이트웨이 연결 없음</span><span class="sxs-lookup"><span data-stu-id="3f418-101"><a name="gwipnoconnection"></a> To modify the local network gateway 'GatewayIpAddress' - no gateway connection</span></span>

<span data-ttu-id="3f418-102">연결하려는 VPN 장치의 공용 IP 주소가 변경된 경우 해당 변경 내용을 반영하도록 로컬 네트워크 게이트웨이를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f418-102">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="3f418-103">예제를 사용하여 게이트웨이 연결이 없는 로컬 네트워크 게이트웨이를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f418-103">Use the example to modify a local network gateway that does not have a gateway connection.</span></span>

<span data-ttu-id="3f418-104">이 값을 수정할 때 주소 접두사를 함께 수정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f418-104">When modifying this value, you can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="3f418-105">현재 설정을 덮어쓰려면 로컬 네트워크 게이트웨이의 기존 이름을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f418-105">Be sure to use the existing name of your local network gateway in order to overwrite the current settings.</span></span> <span data-ttu-id="3f418-106">다른 이름을 사용하면 기존 게이트웨이를 덮어쓰지 않고 새 로컬 네트워크 게이트웨이를 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f418-106">If you use a different name, you create a new local network gateway, instead of overwriting the existing one.</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <span data-ttu-id="3f418-107"><a name="gwipwithconnection"></a>로컬 네트워크 게이트웨이 'GatewayIpAddress'를 수정하려면 - 기존 게이트웨이 연결</span><span class="sxs-lookup"><span data-stu-id="3f418-107"><a name="gwipwithconnection"></a>To modify the local network gateway 'GatewayIpAddress' - existing gateway connection</span></span>

<span data-ttu-id="3f418-108">연결하려는 VPN 장치의 공용 IP 주소가 변경된 경우 해당 변경 내용을 반영하도록 로컬 네트워크 게이트웨이를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f418-108">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="3f418-109">게이트웨이 연결이 이미 있는 경우 먼저 연결을 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f418-109">If a gateway connection already exists, you first need to remove the connection.</span></span> <span data-ttu-id="3f418-110">연결을 제거한 후 게이트웨이 IP 주소를 수정하고 새 연결을 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f418-110">After the connection is removed, you can modify the gateway IP address and recreate a new connection.</span></span> <span data-ttu-id="3f418-111">이와 동시에 주소 접두사를 수정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f418-111">You can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="3f418-112">이로 인해 VPN 연결에 약간의 가동 중지 시간이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="3f418-112">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="3f418-113">게이트웨이 IP 주소를 수정할 때 VPN Gateway를 삭제할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3f418-113">When modifying the gateway IP address, you don't need to delete the VPN gateway.</span></span> <span data-ttu-id="3f418-114">연결만 제거하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f418-114">You only need to remove the connection.</span></span>
 

1. <span data-ttu-id="3f418-115">연결을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="3f418-115">Remove the connection.</span></span> <span data-ttu-id="3f418-116">'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet을 사용하여 연결 이름을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f418-116">You can find the name of your connection by using the 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="3f418-117">'GatewayIpAddress' 값을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f418-117">Modify the 'GatewayIpAddress' value.</span></span> <span data-ttu-id="3f418-118">이와 동시에 주소 접두사를 수정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f418-118">You can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="3f418-119">로컬 네트워크 게이트웨이의 기존 이름으로 현재 설정을 덮어써야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f418-119">Be sure to use the existing name of your local network gateway to overwrite the current settings.</span></span> <span data-ttu-id="3f418-120">이렇게 하지 않으면 기존 게이트웨이를 덮어쓰지 않고 새 로컬 네트워크 게이트웨이를 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f418-120">If you don't, you create a new local network gateway, instead of overwriting the existing one.</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. <span data-ttu-id="3f418-121">연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f418-121">Create the connection.</span></span> <span data-ttu-id="3f418-122">이 예제에서는 IPsec 연결 형식을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3f418-122">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="3f418-123">연결을 다시 만들 때 구성에 대해 지정된 연결 유형을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3f418-123">When you recreate your connection, use the connection type that is specified for your configuration.</span></span> <span data-ttu-id="3f418-124">추가 연결 형식은 [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f418-124">For additional connection types, see the [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>  <span data-ttu-id="3f418-125">VirtualNetworkGateway 이름을 가져오려면 'Get-AzureRmVirtualNetworkGateway' cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f418-125">To obtain the VirtualNetworkGateway name, you can run the 'Get-AzureRmVirtualNetworkGateway' cmdlet.</span></span>
   
    <span data-ttu-id="3f418-126">변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f418-126">Set the variables.</span></span>

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    <span data-ttu-id="3f418-127">연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f418-127">Create the connection.</span></span>

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```