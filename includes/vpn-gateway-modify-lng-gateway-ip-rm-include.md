### <a name="gwipnoconnection"></a>toomodify hello 로컬 네트워크 게이트웨이 'GatewayIpAddress'-게이트웨이 연결 없음

원하는 tooconnect toohas hello VPN 장치에 공용 IP 주소 변경 된 경우 toomodify hello 로컬 네트워크 게이트웨이 tooreflect 변경 해야 합니다. Hello 예제 toomodify 게이트웨이 연결 되어 있지 않은 로컬 네트워크 게이트웨이 사용 합니다.

이 값을 수정할 때는 hello 주소 접두사 hello에도 수정할 수 있습니다 동시 합니다. 로컬 네트워크 게이트웨이의 순서 toooverwrite hello에 대 한 현재 설정에 있는지 toouse hello 기존 이름 이어야 합니다. 다른 이름을 사용 하는 경우 새 로컬 네트워크 게이트웨이 만들을 덮어쓰지 않고 기존 hello 있습니다.

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <a name="gwipwithconnection"></a>toomodify hello 로컬 네트워크 게이트웨이 'GatewayIpAddress'-기존 게이트웨이 연결

원하는 tooconnect toohas hello VPN 장치에 공용 IP 주소 변경 된 경우 toomodify hello 로컬 네트워크 게이트웨이 tooreflect 변경 해야 합니다. 게이트웨이 연결을 이미 있는 경우 먼저 tooremove hello 연결을 해야 합니다. Hello 연결을 제거한 후 hello 게이트웨이 IP 주소를 수정할 수 있으며 새 연결을 다시 만드십시오. Hello에 hello 주소 접두사를 수정할 수도 있습니다 동시 합니다. 이로 인해 VPN 연결에 약간의 가동 중지 시간이 발생합니다. Hello 게이트웨이 IP 주소를 수정할 때 toodelete hello VPN 게이트웨이 필요는 없습니다. Tooremove hello 연결을 하기만 하면 됩니다.
 

1. Hello 연결을 제거 합니다. ' Get AzureRmVirtualNetworkGatewayConnection' hello cmdlet을 사용 하 여 연결의 hello 이름임을 찾을 수 있습니다.

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. Hello 'GatewayIpAddress' 값을 수정 합니다. Hello에 hello 주소 접두사를 수정할 수도 있습니다 동시 합니다. 로컬 네트워크 게이트웨이 toooverwrite hello 현재 설정의 있는지 toouse hello 기존 이름 이어야 합니다. 이렇게 하지 않으면 새 로컬 네트워크 게이트웨이 만들을 덮어쓰지 않고 기존 hello 있습니다.

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. Hello 연결을 만듭니다. 이 예제에서는 IPsec 연결 형식을 구성합니다. 연결을 다시 만들 때 지정 된 hello 연결 형식 구성에 사용 합니다. 추가 연결 형식에 대 한 참조 hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) 페이지.  tooobtain hello VirtualNetworkGateway 이름 hello ' Get AzureRmVirtualNetworkGateway' cmdlet을 실행할 수 있습니다.
   
    Hello 변수를 설정 합니다.

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    Hello 연결을 만듭니다.

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```