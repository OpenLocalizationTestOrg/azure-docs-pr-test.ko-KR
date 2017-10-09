### <span data-ttu-id="ab5dd-101"><a name="noconnection"></a>toomodify 로컬 네트워크 게이트웨이 IP 주소 접두사 게이트웨이 연결 없음</span><span class="sxs-lookup"><span data-stu-id="ab5dd-101"><a name="noconnection"></a>toomodify local network gateway IP address prefixes - no gateway connection</span></span>

<span data-ttu-id="ab5dd-102">tooadd 추가 주소 접두사:</span><span class="sxs-lookup"><span data-stu-id="ab5dd-102">tooadd additional address prefixes:</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

<span data-ttu-id="ab5dd-103">tooremove 주소 접두사:</span><span class="sxs-lookup"><span data-stu-id="ab5dd-103">tooremove address prefixes:</span></span><br>
<span data-ttu-id="ab5dd-104">더 이상 필요 없는 hello 접두사를 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-104">Leave out hello prefixes that you no longer need.</span></span> <span data-ttu-id="ab5dd-105">이 예제에서는 더 이상 필요 접두사 20.0.0.0/24 hello 이전 예제) (에서 hello 로컬 네트워크 게이트웨이 업데이트 하므로 제외 하 고 해당 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-105">In this example, we no longer need prefix 20.0.0.0/24 (from hello previous example), so we update hello local network gateway, excluding that prefix.</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <span data-ttu-id="ab5dd-106"><a name="withconnection"></a>toomodify 로컬 네트워크 게이트웨이 IP 주소 접두사-기존 게이트웨이 연결</span><span class="sxs-lookup"><span data-stu-id="ab5dd-106"><a name="withconnection"></a>toomodify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="ab5dd-107">게이트웨이 연결 하 고 원하는 tooadd 또는 로컬 네트워크 게이트웨이에 포함 된 hello IP 주소 접두사를 제거 하는 경우 toodo hello 순서에 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-107">If you have a gateway connection and want tooadd or remove hello IP address prefixes contained in your local network gateway, you need toodo hello following steps, in order.</span></span> <span data-ttu-id="ab5dd-108">이로 인해 VPN 연결에 약간의 가동 중지 시간이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-108">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="ab5dd-109">IP 주소 접두사를 수정할 때 toodelete hello VPN 게이트웨이 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-109">When modifying IP address prefixes, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="ab5dd-110">Tooremove hello 연결을 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-110">You only need tooremove hello connection.</span></span>


1. <span data-ttu-id="ab5dd-111">Hello 연결을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-111">Remove hello connection.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="ab5dd-112">로컬 네트워크 게이트웨이에 대 한 hello 주소 접두사를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-112">Modify hello address prefixes for your local network gateway.</span></span>
   
  <span data-ttu-id="ab5dd-113">LocalNetworkGateway hello에 대 한 hello 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-113">Set hello variable for hello LocalNetworkGateway.</span></span>

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="ab5dd-114">Hello 접두사를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-114">Modify hello prefixes.</span></span>
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. <span data-ttu-id="ab5dd-115">Hello 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-115">Create hello connection.</span></span> <span data-ttu-id="ab5dd-116">이 예제에서는 IPsec 연결 형식을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-116">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="ab5dd-117">연결을 다시 만들 때 지정 된 hello 연결 형식 구성에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-117">When you recreate your connection, use hello connection type that is specified for your configuration.</span></span> <span data-ttu-id="ab5dd-118">추가 연결 형식에 대 한 참조 hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) 페이지.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-118">For additional connection types, see hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>
   
  <span data-ttu-id="ab5dd-119">VirtualNetworkGateway hello에 대 한 hello 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-119">Set hello variable for hello VirtualNetworkGateway.</span></span>

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="ab5dd-120">Hello 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-120">Create hello connection.</span></span> <span data-ttu-id="ab5dd-121">이 예제에서는 hello $local 2 단계에서 설정한 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab5dd-121">This example uses hello variable $local that you set in step 2.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```