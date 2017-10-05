---
title: "여러 사이트를 호스트하는 Application Gateway 만들기 | Microsoft Docs"
description: "이 페이지에서는 동일한 게이트웨이에서 여러 웹 응용 프로그램을 호스트하는 Azure 응용 프로그램 게이트웨이를 만들고 구성하는 지침을 제공합니다."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: b107d647-c9be-499f-8b55-809c4310c783
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/12/2016
ms.author: amsriva
ms.openlocfilehash: d42efa7d359f5c87c14afbfd138328b37c8ae6c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a>여러 웹 응용 프로그램을 호스트하는 응용 프로그램 게이트웨이 만들기

> [!div class="op_single_selector"]
> * [쉬운 테이블](application-gateway-create-multisite-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-multisite-azureresourcemanager-powershell.md)

다중 사이트 호스팅을 통해 둘 이상의 웹 응용 프로그램을 동일한 응용 프로그램 게이트웨이에 배포할 수 있습니다. 들어오는 HTTP 요청의 호스트 헤더 존재 여부에 따라 트래픽을 수신할 수신기가 결정됩니다. 그런 다음 수신기는 게이트웨이 규칙 정의에 구성된 대로 적절한 백 엔드 풀로 트래픽을 전달합니다. SSL 사용 웹 응용 프로그램에서 응용 프로그램 게이트웨이는 SNI(서버 이름 표시) 확장에 의존하여 웹 트래픽에 대한 올바른 수신기를 선택합니다. 다중 사이트 호스팅의 일반적인 용도는 여러 웹 도메인에 대한 요청의 부하를 여러 백 엔드 서버 풀에 분산하는 것입니다. 마찬가지로 같은 루트 도메인의 여러 하위 도메인을 동일한 응용 프로그램 게이트웨이에서 호스트할 수도 있습니다.

## <a name="scenario"></a>시나리오

다음 예제에서 응용 프로그램 게이트웨이는 두 개의 백 엔드 서버 풀(contoso 서버 풀 및 fabrikam 서버 풀)을 통해 contoso.com 및 fabrikam.com에 대한 트래픽을 처리합니다. 유사한 설정을 사용하여 app.contoso.com 및 blog.contoso.com과 같은 하위 도메인을 호스팅할 수 있습니다.

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a>시작하기 전에

1. 웹 플랫폼 설치 관리자를 사용하는 Azure PowerShell cmdlet의 최신 버전을 설치합니다. **다운로드 페이지** 의 [Windows PowerShell](https://azure.microsoft.com/downloads/)섹션에서 최신 버전을 다운로드하여 설치할 수 있습니다.
2. 응용 프로그램 게이트웨이를 사용하도록 백 엔드 풀에 추가된 서버가 존재하거나 별도의 서브넷에서 가상 네트워크에 또는 할당된 공용 IP/VIP와 함께 해당 끝점이 만들어져야 합니다.

## <a name="requirements"></a>요구 사항

* **백 엔드 서버 풀:** 백 엔드 서버의 IP 주소 목록입니다. 나열된 IP 주소는 가상 네트워크 서브넷에 속하거나 공용 IP/VIP이어야 합니다. FQDN을 사용할 수도 있습니다.
* **백 엔드 서버 풀 설정:** 모든 풀에는 포트, 프로토콜 및 쿠키 기반의 선호도와 같은 설정이 있습니다. 이러한 설정은 풀에 연결 및 풀 내의 모든 서버에 적용 됩니다.
* **프런트 엔드 포트:** 이 포트는 응용 프로그램 게이트웨이에 열려 있는 공용 포트입니다. 트래픽이 이 포트에 도달하면, 백 엔드 서버 중의 하나로 리디렉트됩니다.
* **수신기:** 수신기에는 프런트 엔드 포트, 프로토콜(Http 또는 Https, 이 값은 대/소문자 구분) 및 SSL 인증서 이름(SSL 오프로드를 구성하는 경우)이 있습니다. 다중 사이트 지원 응용 프로그램 게이트웨이의 경우 호스트 이름 및 SNI 표시도 추가됩니다.
* **규칙:** 규칙은 수신기와 백 엔드 서버 풀을 바인딩하고 특정 수신기에 도달했을 때 트래픽이 전달되어야 하는 백 엔드 서버 풀을 정의합니다. 규칙은 나열된 순서대로 처리되고 트래픽은 특이성에 관계없이 일치하는 첫 번째 규칙을 통해 전달됩니다. 예를 들어 기본 수신기를 사용하는 규칙과 다중 사이트 수신기를 사용하는 규칙이 둘 다 같은 포트에 있는 경우 다중 사이트 규칙이 예상대로 작동하려면 다중 사이트 수신기를 사용하는 규칙은 기본 수신기를 사용하는 규칙 앞에 나열되어야 합니다.

## <a name="create-an-application-gateway"></a>응용 프로그램 게이트웨이 만들기

다음은 Application Gateway를 만드는 데 필요한 단계입니다.

1. 리소스 관리자에 대한 리소스 그룹을 만듭니다.
2. 응용 프로그램 게이트웨이에 대한 가상 네트워크, 서브넷 및 공용 IP를 만듭니다.
3. 응용 프로그램 게이트웨이 구성 개체를 만듭니다.
4. 응용 프로그램 게이트웨이 리소스를 만듭니다.

## <a name="create-a-resource-group-for-resource-manager"></a>리소스 관리자에 대한 리소스 그룹 만들기

Azure PowerShell의 최신 버전을 사용하고 있는지 확인합니다. 자세한 내용은 [Resource Manager에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.

### <a name="step-1"></a>1단계

Azure에 로그인

```powershell
Login-AzureRmAccount
```
자격 증명을 사용하여 인증하라는 메시지가 표시됩니다.

### <a name="step-2"></a>2단계:

계정에 대한 구독을 확인합니다.

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a>3단계:

사용할 Azure 구독을 선택합니다.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>4단계:

리소스 그룹을 만듭니다. 기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛰세요.

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

또는 응용 프로그램 게이트웨이의 리소스 그룹에 대한 태그를 만들 수도 있습니다.

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다. 이 위치는 해당 리소스 그룹에서 리소스의 기본 위치로 사용됩니다. 응용 프로그램 게이트웨이를 만들기 위한 모든 명령이 동일한 리소스 그룹을 사용하는지 확인합니다.

위 예제에서는 **appgw-RG**라는 리소스 그룹과 **West US**라는 위치를 만들었습니다.

> [!NOTE]
> 응용 프로그램 게이트웨이에 사용자 지정 프로브를 구성해야 하는 경우 [PowerShell을 사용하여 사용자 지정 프로브로 응용 프로그램 게이트웨이 만들기](application-gateway-create-probe-ps.md)를 참조하세요. 자세한 내용은 [사용자 지정 프로브 및 상태 모니터링](application-gateway-probe-overview.md)으로 이동하세요.

## <a name="create-a-virtual-network-and-subnets"></a>가상 네트워크 및 서브넷 만들기

다음 예제에서는 리소스 관리자를 사용하여 가상 네트워크를 만드는 방법을 보여 줍니다. 이 단계에서는 두 개의 서브넷이 만들어집니다. 응용 프로그램 게이트웨이 자체에 대 한 첫 번째 서브넷입니다. 응용 프로그램 게이트웨이에서 자체 인스턴스를 보유하려면 자체 서브넷이 필요합니다. 다른 응용 프로그램 게이트웨이의 해당 서브넷에만 배포할 수 있습니다. 두 번째 서브넷은 응용 프로그램 백 엔드 서버를 보유하는 데 사용됩니다.

### <a name="step-1"></a>1단계

주소 범위 10.0.0.0/24를 응용 프로그램 게이트웨이를 보유하는 데 사용할 서브넷 변수에 할당합니다.

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a>2단계

주소 범위 10.0.1.0/24를 백엔드 풀에 사용할 서브넷2 변수에 할당합니다.

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a>3단계

접두사 10.0.0.0/16과 서브넷 10.0.0.0/24및 10.0.1.0/24를 사용하여 미국 서부 지역에 리소스 그룹 **appgw-rg**에서 **appgwvnet**이라는 가상 네트워크를 만듭니다.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a>4단계

응용 프로그램 게이트웨이를 만드는 다음 단계에 서브넷 변수를 할당합니다.

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a>프런트 엔드 구성에 대한 공용 IP 주소 만들기

미국 서부 지역에 리소스 그룹 **appgw-rg**에서 공용 IP 리소스 **publicIP01**을 만듭니다.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

서비스를 시작할 때 응용 프로그램 게이트웨이에 IP 주소가 할당됩니다.

## <a name="create-application-gateway-configuration"></a>응용 프로그램 게이트웨이 구성 만들기

응용 프로그램 게이트웨이를 만들기 전에 모든 구성 항목을 설정해야 합니다. 다음 단계 응용 프로그램 게이트웨이 리소스에 필요한 구성 항목을 만듭니다.

### <a name="step-1"></a>1단계:

**gatewayIP01**이라는 응용 프로그램 게이트웨이 IP 구성을 만듭니다. 응용 프로그램 게이트웨이는 시작되면 구성된 서브넷에서 IP 주소를 선택하고 백 엔드 IP 풀의 IP 주소로 네트워크 트래픽을 라우팅합니다. 인스턴스마다 하나의 IP 주소를 사용합니다.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a>2단계

IP 주소가 **134.170.185.46**, **134.170.188.221**, **134.170.185.50**인 **pool1**과 IP 주소가 **134.170.186.46**, **134.170.189.221**, **134.170.186.50**인 **pool2**로 백 엔드 IP 주소 풀, **pool01**과 **pool2**를 구성합니다.

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

이 예제에서는 요청된 사이트를 기반으로 네트워크 트래픽을 라우팅하는 두 개의 백 엔드 풀이 있습니다. 하나의 풀은 사이트 "contoso.com"에서 트래픽을 수신하고 또 다른 풀은 사이트 "fabrikam.com"에서 트래픽을 수신합니다. 사용자 고유의 응용 프로그램 IP 주소 끝점을 추가하려면 이전 IP 주소를 교체해야 합니다. 내부 IP 주소 대신 공용 IP 주소, FQDN 또는 VM의 NIC를 백 엔드 인스턴스에 사용할 수도 있습니다. PowerShell에서 IP 대신 FQDN을 지정하려면 "-BackendFQDNs" 매개 변수를 사용합니다.

### <a name="step-3"></a>3단계:

백 엔드 풀에서 부하가 분산된 네트워크 트래픽에 대해 Application Gateway 설정 **poolsetting01** 및 **poolsetting02**를 구성합니다. 이 예제에서는 백 엔드 풀에 대한 다른 백 엔드 풀 설정을 구성합니다. 각 백 엔드 풀에는 고유한 백 엔드 풀 설정이 있을 수 있습니다.

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a>4단계

공용 IP 끝점으로 프런트 엔드 IP를 구성합니다.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a>5단계

응용 프로그램 게이트웨이에 대한 프런트 엔드 포트를 구성합니다.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a>6단계

이 예제에서 지원하려는 두 웹 사이트에 대해 두 개의 SSL 인증서를 구성합니다. 인증서 하나는 contoso.com 트래픽용이고, 나머지는 fabrikam.com 트래픽용입니다. 이러한 인증서는 사용자 웹 사이트용으로 인증 기관에서 발급한 인증서여야 합니다. 자체 서명된 인증서는 지원되지만 프로덕션 트래픽에 권장되지 않습니다.

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a>7단계

이 예제의 두 웹 사이트에 대한 두 개의 수신기를 구성합니다. 이 단계에서는 들어오는 트래픽을 수신하는 데 사용되는 공용 IP 주소, 포트 및 호스트에 대한 수신기를 구성합니다. HostName 매개 변수는 다중 사이트 지원에 필요하며 트래픽이 수신되는 적절한 웹 사이트로 설정되어야 합니다. RequireServerNameIndication 매개 변수는 다중 호스트 시나리오에서 SSL 지원이 필요한 웹 사이트에 대해 true로 설정되어야 합니다. SSL 지원이 필요한 경우 해당 웹 응용 프로그램에 대한 트래픽의 보안을 유지하는 데 사용되는 SSL 인증서도 지정해야 합니다. FrontendIPConfiguration, FrontendPort 및 HostName의 조합은 수신기에 고유해야 합니다. 각 수신기는 하나의 인증서를 지원할 수 있습니다.

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a>8단계

이 예제의 두 웹 응용 프로그램에 대한 두 개의 규칙 설정을 만듭니다. 규칙은 수신기, 백 엔드 풀 및 http 설정을 연결합니다. 이 단계에서는 각 웹 사이트에 기본 라우팅 규칙을 사용하도록 응용 프로그램 게이트웨이를 구성합니다. 각 웹 사이트의 트래픽은 구성된 해당 수신기에서 수신된 후 BackendHttpSettings에 지정된 속성을 사용하여 구성된 해당 백 엔드 풀로 전송됩니다.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a>9단계

응용 프로그램 게이트웨이에 대한 크기 및 인스턴스 수를 구성합니다.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a>응용 프로그램 게이트웨이 만들기

이전 단계의 모든 구성 개체로 응용 프로그램 게이트웨이를 만듭니다.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> 응용 프로그램 게이트웨이 프로비전은 장기 실행 작업이며 완료하는 데 다소 시간이 걸릴 수 있습니다.
> 
> 

## <a name="get-application-gateway-dns-name"></a>응용 프로그램 게이트웨이 DNS 이름 가져오기

게이트웨이가 생성되면 다음 단계는 통신에 대한 프런트 엔드를 구성하는 것입니다. 공용 IP를 사용할 때 Application Gateway는 식별 이름이 아닌 동적으로 할당된 DNS 이름이 필요합니다. 최종 사용자가 Application Gateway를 누를 수 있도록 하려면 CNAME 레코드를 사용하여 Application Gateway의 공용 끝점을 가리키도록 합니다. [Azure에서 사용자 지정 도메인 이름 구성](../cloud-services/cloud-services-custom-domain-name-portal.md). 이 작업을 수행하려면 Application Gateway에 연결된 PublicIPAddress 요소를 사용하여 Application Gateway 및 관련 IP/DNS 이름에 대한 세부 정보를 검색합니다. 응용 프로그램 게이트웨이의 DNS 이름은 두 개의 웹 응용 프로그램을 이 DNS 이름으로 가리키는 CNAME 레코드를 만드는 데 사용됩니다. A 레코드를 사용할 경우 응용 프로그램 게이트웨이 다시 시작 시 VIP가 변경될 수 있으므로 이는 권장되지 않습니다.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a>다음 단계

[응용 프로그램 게이트웨이-웹 응용 프로그램 방화벽](application-gateway-webapplicationfirewall-overview.md)을 사용하여 웹 사이트를 보호하는 방법을 알아봅니다.

