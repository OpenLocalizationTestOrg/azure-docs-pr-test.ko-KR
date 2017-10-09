### <a name="noconnection"></a>toomodify 로컬 네트워크 게이트웨이 IP 주소 접두사 게이트웨이 연결 없음

tooadd 추가 주소 접두사:

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

tooremove 주소 접두사:<br>
더 이상 필요 없는 hello 접두사를 생략 합니다. 이 예제에서는 더 이상 필요 접두사 20.0.0.0/24 hello 이전 예제) (에서 hello 로컬 네트워크 게이트웨이 업데이트 하므로 제외 하 고 해당 접두사입니다.

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <a name="withconnection"></a>toomodify 로컬 네트워크 게이트웨이 IP 주소 접두사-기존 게이트웨이 연결

게이트웨이 연결 하 고 원하는 tooadd 또는 로컬 네트워크 게이트웨이에 포함 된 hello IP 주소 접두사를 제거 하는 경우 toodo hello 순서에 단계를 수행 해야 합니다. 이로 인해 VPN 연결에 약간의 가동 중지 시간이 발생합니다. IP 주소 접두사를 수정할 때 toodelete hello VPN 게이트웨이 필요는 없습니다. Tooremove hello 연결을 하기만 하면 됩니다.


1. Hello 연결을 제거 합니다.

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. 로컬 네트워크 게이트웨이에 대 한 hello 주소 접두사를 수정 합니다.
   
  LocalNetworkGateway hello에 대 한 hello 변수를 설정 합니다.

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  Hello 접두사를 수정 합니다.
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. Hello 연결을 만듭니다. 이 예제에서는 IPsec 연결 형식을 구성합니다. 연결을 다시 만들 때 지정 된 hello 연결 형식 구성에 사용 합니다. 추가 연결 형식에 대 한 참조 hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) 페이지.
   
  VirtualNetworkGateway hello에 대 한 hello 변수를 설정 합니다.

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  Hello 연결을 만듭니다. 이 예제에서는 hello $local 2 단계에서 설정한 변수를 사용 합니다.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```