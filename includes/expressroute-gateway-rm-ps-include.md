이 작업 사용 하 여 VNet에 대 한 hello 단계 hello 구성 참조 목록 다음의 hello 값에 기반 합니다. 추가 설정 및 이름도 이 목록에 설명되어 있습니다. 이 목록에 hello 값에 기반 하 여 변수 추가 수행 하지만 hello 단계 중 하나에서 직접이 목록을 사용 하지 마십시오 했습니다. 자신의 hello 값 대체를 참조로 hello 목록 toouse을 복사할 수 있습니다.

**구성 참조 목록**

* 가상 네트워크 이름 = "TestVNet"
* 가상 네트워크 주소 공간: 192.168.0.0/16
* 리소스 그룹: "TestRG"
* Subnet1 이름 = "FrontEnd" 
* Subnet1 주소 공간 = "192.168.1.0/24"
* 게이트웨이 서브넷 이름: "GatewaySubnet" 게이트웨이 서브넷의 이름을 항상 *GatewaySubnet*으로 지정해야 합니다.
* 게이트웨이 서브넷 주소 공간 = "192.168.200.0/26"
* 지역 = "미국 동부"
* 게이트웨이 이름 = "GW"
* 게이트웨이 IP 이름 = "GWIP"
* 게이트웨이 IP 구성 이름 = "gwipconf"
* 유형 = "ExpressRoute" 이 유형이 Express 경로 구성에 필요합니다.
* 게이트웨이 공용 IP 이름 = "gwpip"

## <a name="add-a-gateway"></a>게이트웨이를 추가합니다.
1. Tooyour Azure 구독을 연결 합니다.

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. 이 연습에 대한 변수를 선언합니다. 있는지 tooedit hello 샘플 tooreflect hello 설정을 toouse 원하는 수 있습니다.

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. 변수로 hello 가상 네트워크 개체를 저장 합니다.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. 게이트웨이 서브넷 tooyour 가상 네트워크를 추가 합니다. "GatewaySubnet" hello 게이트웨이 서브넷에 이름을 지정 해야 합니다. /27 이상(/26, /25 등)인 게이트웨이 서브넷을 만들어야 합니다.

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. Hello 구성을 설정 합니다.

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. 변수로 hello 게이트웨이 서브넷을 저장 합니다.

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. 공용 IP 주소를 요청합니다. hello 게이트웨이 만들기 전에 hello IP 주소가 요청 합니다. 원하는 toouse; hello IP 주소를 지정할 수 없습니다. 동적으로 할당 됩니다. Hello 다음 구성 섹션에이 IP 주소를 사용 합니다. hello AllocationMethod 동적 이어야 합니다.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. 게이트웨이에 대 한 hello 구성을 만듭니다. hello 게이트웨이 구성 hello 서브넷과 공용 IP 주소 toouse hello 정의합니다. 이 단계에서는 hello 게이트웨이 만들 때 사용 됨 hello 구성을 지정 됩니다. 이 단계 실제로 hello 게이트웨이 개체를 만들지 않습니다. 게이트웨이 구성 toocreate 아래 hello 샘플을 사용 합니다.

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. Hello 게이트웨이 만듭니다. 이 단계에서는 hello **-GatewayType** 는 특히 중요 합니다. Hello 값을 사용 해야 **ExpressRoute**합니다. 이러한 cmdlet을 실행 한 후 45 분 또는 자세한 toocreate hello 게이트웨이 걸릴 수 있습니다.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-hello-gateway-was-created"></a>Hello 게이트웨이가 생성 되었는지 확인
게이트웨이 hello tooverify 만든 명령 뒤 hello를 사용 합니다.

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a>게이트웨이 크기 조정
다양한 [게이트웨이 SKU](../articles/expressroute/expressroute-about-virtual-network-gateways.md)가 있습니다. 언제 든 지 명령 toochange hello 게이트웨이 SKU 다음 hello를 사용할 수 있습니다.

> [!IMPORTANT]
> 이 명령은 UltraPerformance 게이트웨이에는 작동하지 않습니다. toochange 게이트웨이 tooan UltraPerformance 게이트웨이 먼저 hello 기존 express 경로 게이트웨이 제거 하 고 새 UltraPerformance 게이트웨이 만듭니다. toodowngrade UltraPerformance 게이트웨이에서 게이트웨이 먼저 제거 UltraPerformance 게이트웨이 hello 한 다음 새 게이트웨이 만듭니다.
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a>게이트웨이 제거
다음 명령 tooremove 게이트웨이 hello를 사용 합니다.

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```