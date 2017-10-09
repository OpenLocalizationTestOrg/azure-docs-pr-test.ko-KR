만들어야 VNet 및 게이트웨이 서브넷 먼저 작업 hello 다음 작업을 계속 해야 합니다. Hello 문서 참조 [hello 클래식 포털을 사용 하 여 가상 네트워크 구성](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) 자세한 정보에 대 한 합니다.   

## <a name="add-a-gateway"></a>게이트웨이를 추가합니다.
Toocreate 게이트웨이 아래 hello 명령을 사용 합니다. 있는지 toosubstitute 자신만의 모든 값 수입니다.

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-hello-gateway-was-created"></a>Hello 게이트웨이가 생성 되었는지 확인
게이트웨이 hello tooverify 아래 hello 명령은 사용 하 여 생성 되었습니다. 이 명령은 다른 작업에 필요한 hello 게이트웨이 ID를도 검색 합니다.

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a>게이트웨이 크기 조정
다양한 [게이트웨이 SKU](../articles/expressroute/expressroute-about-virtual-network-gateways.md)가 있습니다. 언제 든 지 명령 toochange hello 게이트웨이 SKU 다음 hello를 사용할 수 있습니다.

> [!IMPORTANT]
> 이 명령은 UltraPerformance 게이트웨이에는 작동하지 않습니다. toochange 게이트웨이 tooan UltraPerformance 게이트웨이 먼저 hello 기존 express 경로 게이트웨이 제거 하 고 새 UltraPerformance 게이트웨이 만듭니다. toodowngrade UltraPerformance 게이트웨이에서 게이트웨이 먼저 제거 UltraPerformance 게이트웨이 hello 한 다음 새 게이트웨이 만듭니다. 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a>게이트웨이 제거
Tooremove 게이트웨이 아래 hello 명령을 사용 하 여

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>