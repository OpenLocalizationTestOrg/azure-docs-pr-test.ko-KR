<span data-ttu-id="c5c7d-101">이 작업 사용 하 여 VNet에 대 한 hello 단계 hello 구성 참조 목록 다음의 hello 값에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-101">hello steps for this task use a VNet based on hello values in hello following configuration reference list.</span></span> <span data-ttu-id="c5c7d-102">추가 설정 및 이름도 이 목록에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-102">Additional settings and names are also outlined in this list.</span></span> <span data-ttu-id="c5c7d-103">이 목록에 hello 값에 기반 하 여 변수 추가 수행 하지만 hello 단계 중 하나에서 직접이 목록을 사용 하지 마십시오 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-103">We don't use this list directly in any of hello steps, although we do add variables based on hello values in this list.</span></span> <span data-ttu-id="c5c7d-104">자신의 hello 값 대체를 참조로 hello 목록 toouse을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-104">You can copy hello list toouse as a reference, replacing hello values with your own.</span></span>

<span data-ttu-id="c5c7d-105">**구성 참조 목록**</span><span class="sxs-lookup"><span data-stu-id="c5c7d-105">**Configuration reference list**</span></span>

* <span data-ttu-id="c5c7d-106">가상 네트워크 이름 = "TestVNet"</span><span class="sxs-lookup"><span data-stu-id="c5c7d-106">Virtual Network Name = "TestVNet"</span></span>
* <span data-ttu-id="c5c7d-107">가상 네트워크 주소 공간: 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="c5c7d-107">Virtual Network address space = 192.168.0.0/16</span></span>
* <span data-ttu-id="c5c7d-108">리소스 그룹: "TestRG"</span><span class="sxs-lookup"><span data-stu-id="c5c7d-108">Resource Group = "TestRG"</span></span>
* <span data-ttu-id="c5c7d-109">Subnet1 이름 = "FrontEnd"</span><span class="sxs-lookup"><span data-stu-id="c5c7d-109">Subnet1 Name = "FrontEnd"</span></span> 
* <span data-ttu-id="c5c7d-110">Subnet1 주소 공간 = "192.168.1.0/24"</span><span class="sxs-lookup"><span data-stu-id="c5c7d-110">Subnet1 address space = "192.168.1.0/24"</span></span>
* <span data-ttu-id="c5c7d-111">게이트웨이 서브넷 이름: "GatewaySubnet" 게이트웨이 서브넷의 이름을 항상 *GatewaySubnet*으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-111">Gateway Subnet name: "GatewaySubnet" You must always name a gateway subnet *GatewaySubnet*.</span></span>
* <span data-ttu-id="c5c7d-112">게이트웨이 서브넷 주소 공간 = "192.168.200.0/26"</span><span class="sxs-lookup"><span data-stu-id="c5c7d-112">Gateway Subnet address space = "192.168.200.0/26"</span></span>
* <span data-ttu-id="c5c7d-113">지역 = "미국 동부"</span><span class="sxs-lookup"><span data-stu-id="c5c7d-113">Region = "East US"</span></span>
* <span data-ttu-id="c5c7d-114">게이트웨이 이름 = "GW"</span><span class="sxs-lookup"><span data-stu-id="c5c7d-114">Gateway Name = "GW"</span></span>
* <span data-ttu-id="c5c7d-115">게이트웨이 IP 이름 = "GWIP"</span><span class="sxs-lookup"><span data-stu-id="c5c7d-115">Gateway IP Name = "GWIP"</span></span>
* <span data-ttu-id="c5c7d-116">게이트웨이 IP 구성 이름 = "gwipconf"</span><span class="sxs-lookup"><span data-stu-id="c5c7d-116">Gateway IP configuration Name = "gwipconf"</span></span>
* <span data-ttu-id="c5c7d-117">유형 = "ExpressRoute" 이 유형이 Express 경로 구성에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-117">Type = "ExpressRoute" This type is required for an ExpressRoute configuration.</span></span>
* <span data-ttu-id="c5c7d-118">게이트웨이 공용 IP 이름 = "gwpip"</span><span class="sxs-lookup"><span data-stu-id="c5c7d-118">Gateway Public IP Name = "gwpip"</span></span>

## <a name="add-a-gateway"></a><span data-ttu-id="c5c7d-119">게이트웨이를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-119">Add a gateway</span></span>
1. <span data-ttu-id="c5c7d-120">Tooyour Azure 구독을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-120">Connect tooyour Azure Subscription.</span></span>

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="c5c7d-121">이 연습에 대한 변수를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-121">Declare your variables for this exercise.</span></span> <span data-ttu-id="c5c7d-122">있는지 tooedit hello 샘플 tooreflect hello 설정을 toouse 원하는 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-122">Be sure tooedit hello sample tooreflect hello settings that you want toouse.</span></span>

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. <span data-ttu-id="c5c7d-123">변수로 hello 가상 네트워크 개체를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-123">Store hello virtual network object as a variable.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. <span data-ttu-id="c5c7d-124">게이트웨이 서브넷 tooyour 가상 네트워크를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-124">Add a gateway subnet tooyour Virtual Network.</span></span> <span data-ttu-id="c5c7d-125">"GatewaySubnet" hello 게이트웨이 서브넷에 이름을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-125">hello gateway subnet must be named "GatewaySubnet".</span></span> <span data-ttu-id="c5c7d-126">/27 이상(/26, /25 등)인 게이트웨이 서브넷을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-126">You should create a gateway subnet that is /27 or larger (/26, /25, etc.).</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. <span data-ttu-id="c5c7d-127">Hello 구성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-127">Set hello configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="c5c7d-128">변수로 hello 게이트웨이 서브넷을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-128">Store hello gateway subnet as a variable.</span></span>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. <span data-ttu-id="c5c7d-129">공용 IP 주소를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-129">Request a public IP address.</span></span> <span data-ttu-id="c5c7d-130">hello 게이트웨이 만들기 전에 hello IP 주소가 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-130">hello IP address is requested before creating hello gateway.</span></span> <span data-ttu-id="c5c7d-131">원하는 toouse; hello IP 주소를 지정할 수 없습니다. 동적으로 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-131">You cannot specify hello IP address that you want toouse; it’s dynamically allocated.</span></span> <span data-ttu-id="c5c7d-132">Hello 다음 구성 섹션에이 IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-132">You'll use this IP address in hello next configuration section.</span></span> <span data-ttu-id="c5c7d-133">hello AllocationMethod 동적 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-133">hello AllocationMethod must be Dynamic.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. <span data-ttu-id="c5c7d-134">게이트웨이에 대 한 hello 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-134">Create hello configuration for your gateway.</span></span> <span data-ttu-id="c5c7d-135">hello 게이트웨이 구성 hello 서브넷과 공용 IP 주소 toouse hello 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-135">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="c5c7d-136">이 단계에서는 hello 게이트웨이 만들 때 사용 됨 hello 구성을 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-136">In this step, you are specifying hello configuration that will be used when you create hello gateway.</span></span> <span data-ttu-id="c5c7d-137">이 단계 실제로 hello 게이트웨이 개체를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-137">This step does not actually create hello gateway object.</span></span> <span data-ttu-id="c5c7d-138">게이트웨이 구성 toocreate 아래 hello 샘플을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-138">Use hello sample below toocreate your gateway configuration.</span></span>

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. <span data-ttu-id="c5c7d-139">Hello 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-139">Create hello gateway.</span></span> <span data-ttu-id="c5c7d-140">이 단계에서는 hello **-GatewayType** 는 특히 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-140">In this step, hello **-GatewayType** is especially important.</span></span> <span data-ttu-id="c5c7d-141">Hello 값을 사용 해야 **ExpressRoute**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-141">You must use hello value **ExpressRoute**.</span></span> <span data-ttu-id="c5c7d-142">이러한 cmdlet을 실행 한 후 45 분 또는 자세한 toocreate hello 게이트웨이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-142">After running these cmdlets, hello gateway can take 45 minutes or more toocreate.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-hello-gateway-was-created"></a><span data-ttu-id="c5c7d-143">Hello 게이트웨이가 생성 되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="c5c7d-143">Verify hello gateway was created</span></span>
<span data-ttu-id="c5c7d-144">게이트웨이 hello tooverify 만든 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-144">Use hello following commands tooverify that hello gateway has been created:</span></span>

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a><span data-ttu-id="c5c7d-145">게이트웨이 크기 조정</span><span class="sxs-lookup"><span data-stu-id="c5c7d-145">Resize a gateway</span></span>
<span data-ttu-id="c5c7d-146">다양한 [게이트웨이 SKU](../articles/expressroute/expressroute-about-virtual-network-gateways.md)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-146">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="c5c7d-147">언제 든 지 명령 toochange hello 게이트웨이 SKU 다음 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-147">You can use hello following command toochange hello Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c5c7d-148">이 명령은 UltraPerformance 게이트웨이에는 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-148">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="c5c7d-149">toochange 게이트웨이 tooan UltraPerformance 게이트웨이 먼저 hello 기존 express 경로 게이트웨이 제거 하 고 새 UltraPerformance 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-149">toochange your gateway tooan UltraPerformance gateway, first remove hello existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="c5c7d-150">toodowngrade UltraPerformance 게이트웨이에서 게이트웨이 먼저 제거 UltraPerformance 게이트웨이 hello 한 다음 새 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-150">toodowngrade your gateway from an UltraPerformance gateway, first remove hello UltraPerformance gateway, and then create a new gateway.</span></span>
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a><span data-ttu-id="c5c7d-151">게이트웨이 제거</span><span class="sxs-lookup"><span data-stu-id="c5c7d-151">Remove a gateway</span></span>
<span data-ttu-id="c5c7d-152">다음 명령 tooremove 게이트웨이 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5c7d-152">Use hello following command tooremove a gateway:</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```