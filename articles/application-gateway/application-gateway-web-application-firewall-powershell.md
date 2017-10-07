---
title: "aaaConfigure 웹 응용 프로그램 방화벽 Azure 응용 프로그램 게이트웨이 | Microsoft Docs"
description: "이 문서는 어떻게 toostart 웹를 사용 하는 기존 또는 새 응용 프로그램 게이트웨이에 응용 프로그램 방화벽에 지침을 제공 합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: bd2a69901f0ec0d6551d633e2588b74c3ab59a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a>새 또는 기존 Application Gateway에 웹 응용 프로그램 방화벽 구성

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Azure CLI](application-gateway-web-application-firewall-cli.md)

웹 응용 프로그램 방화벽 tooan 기존 응용 프로그램 게이트웨이 추가 하거나 toocreate 웹 응용 프로그램 방화벽에서 응용 프로그램 게이트웨이 사용 하는 방법을 알아봅니다.

hello 웹 응용 프로그램 방화벽 (WAF)에서 Azure 응용 프로그램 게이트웨이 SQL 삽입 같은 일반적인 웹 기반 공격, 사이트 간 스크립팅 공격이 및 도용 하는 세션에서 웹 응용 프로그램을 보호합니다.

Azure Application Gateway는 계층 7 부하 분산 장치입니다. 장애 조치의 경우 서로 다른 서버 간에 HTTP 요청 성능 라우팅 hello 클라우드 또는 온-프레미스에 있는지 여부를 제공 합니다. Application Gateway는 HTTP 부하 분산, 쿠키 기반 세션 선호도, SSL(Secure Sockets Layer) 오프로드, 사용자 지정 상태 프로브, 다중 사이트 지원 및 기타 여러 기능을 포함하여 다양한 ADC(Application Delivery Controller)를 제공합니다. 지원 되는 기능의 전체 목록은 toofind 방문: [응용 프로그램 게이트웨이 개요](application-gateway-introduction.md)합니다.

hello 다음 문서에서는 어떻게 너무[응용 프로그램 게이트웨이 기존 웹 응용 프로그램 방화벽 tooan 추가](#add-web-application-firewall-to-an-existing-application-gateway) 및 [웹 응용 프로그램 방화벽을 사용 하 여 응용 프로그램 게이트웨이 만들](#create-an-application-gateway-with-web-application-firewall)합니다.

![시나리오 이미지][scenario]

## <a name="waf-configuration-differences"></a>WAF 구성 차이

읽기 있으면 [PowerShell과 함께 응용 프로그램 게이트웨이 만들](application-gateway-create-gateway-arm.md), 응용 프로그램 게이트웨이 만들 때 hello SKU 설정 tooconfigure 이해 합니다. WAF는 hello SKU 응용 프로그램 게이트웨이를 구성 하는 경우 추가 설정을 toodefine를 제공 합니다. 추가 변경 된 사항이 없습니다 hello 응용 프로그램 게이트웨이 자체에서 설정한 합니다.

| **설정** | **세부 정보**
|---|---|
|**SKU** |WAF가 없는 일반 Application Gateway는 **Standard\_Small**, **Standard\_Medium** 및 **Standard\_Large** 크기를 지원합니다. WAF의 hello 도입으로 두 개의 추가 Sku는 **WAF\_보통** 및 **WAF\_Large**합니다. 소형 Application Gateway에는 WAF가 지원되지 않습니다.|
|**계층** | hello 사용 가능한 값은 **표준** 또는 **WAF**합니다. 웹 응용 프로그램 방화벽을 사용하는 경우 **WAF**를 선택해야 합니다.|
|**모드** | 이 설정은 WAF의 hello 모드입니다. 허용되는 값은 **검색** 및 **방지**입니다. WAF를 검색 모드로 설정하면 모든 위협이 로그 파일에 저장됩니다. 방지 모드에서 이벤트는 여전히 로깅되지만 hello 공격자가 응용 프로그램 게이트웨이 hello에서 403 권한 없는 응답을 받습니다.|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a>웹 응용 프로그램 방화벽 tooan 기존 응용 프로그램 게이트웨이 추가 합니다.

Hello 최신 버전의 Azure PowerShell을 사용 하 고 있는지 확인 합니다. 자세한 내용은 [Resource Manager에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.

1. Tooyour Azure 계정에에서 로그인 합니다.

    ```powershell
    Login-AzureRmAccount
    ```

2. 이 시나리오에 대 한 구독 toouse hello를 선택 합니다.

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. 웹 응용 프로그램 방화벽에 추가 하는 hello 게이트웨이 검색 합니다.

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. Hello 웹 응용 프로그램 방화벽 sku를 구성 합니다. hello 사용 가능한 크기는 **WAF\_Large** 및 **WAF\_보통**합니다. 웹 응용 프로그램 방화벽 사용 되 면 hello 계층 야 **WAF**, hello sku를 설정할 때 hello 용량을 확인 해야 합니다.

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. 다음 예제는 hello에 정의 된 대로 WAF hello 설정을 구성 합니다.

   에 대 한 **FirewallMode**, hello 사용 가능한 값은 검색 및 방지 합니다.

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. Hello 단계 이전에 정의 된 hello 설정을 사용 하 여 hello 응용 프로그램 게이트웨이 업데이트 합니다.

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

이 명령은 웹 응용 프로그램 방화벽으로 hello 응용 프로그램 게이트웨이 업데이트합니다. 방문 [응용 프로그램 게이트웨이 진단](application-gateway-diagnostics.md) toounderstand tooview 응용 프로그램 게이트웨이 기록 하는 방법입니다. WAF에서는 toohello 보안 이기 때문 로그 필요 toobe toounderstand 웹 응용 프로그램의 보안 상태를 hello 정기적으로 검토 합니다.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>웹 응용 프로그램 방화벽이 있는 Application Gateway 만들기

hello 다음 단계 이동에서 웹 응용 프로그램 방화벽을 사용 하 여 응용 프로그램 게이트웨이 만들기에 대 한 시작 tooend hello 전체 프로세스를 통해.

Hello 최신 버전의 Azure PowerShell을 사용 하 고 있는지 확인 합니다. 자세한 내용은 [Resource Manager에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.

1. TooAzure를 실행 하 여 로그인 `Login-AzureRmAccount`, 자격 증명으로 증명된 tooauthenticate 됩니다.

1. 실행 하 여 hello 계정에 대 한 hello 구독을 확인 합니다.`Get-AzureRmSubscription`

1. Azure 구독 toouse 선택 합니다.

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a>리소스 그룹 만들기

응용 프로그램 게이트웨이 hello에 대 한 리소스 그룹을 만듭니다.

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다. 이 위치는 해당 리소스 그룹의 리소스에 대 한 hello 기본 위치로 사용 됩니다. 모든 명령을 사용 하 여 응용 프로그램 게이트웨이는 toocreate hello 동일한 리소스 그룹이 있는지 확인 합니다.

앞 예제는 hello, "appgw RG" 및 위치 "West US." 라는 리소스 그룹 생성

> [!NOTE]
> 응용 프로그램 게이트웨이에 대 한 사용자 지정 프로브 tooconfigure 해야 할 경우 참조 [PowerShell을 사용 하 여 사용자 지정 프로브 사용 하 여 응용 프로그램 게이트웨이 만들](application-gateway-create-probe-ps.md)합니다. 자세한 내용은 [사용자 지정 프로브 및 상태 모니터링](application-gateway-probe-overview.md) 을 확인합니다.

### <a name="configure-virtual-network"></a>가상 네트워크 구성

Application Gateway에는 자체 서브넷이 필요합니다. 이 단계에서는 응용 프로그램 게이트웨이 hello 및 백 엔드 풀 멤버에 대 한 10.0.0.0/16 및 두 서브넷의 주소 공간을 사용 하 여 가상 네트워크를 만듭니다.

```powershell
# Create a subnet configuration object for hello Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in hello subnet for Application Gateway instances. With a smaller subnet, you may not be able tooadd more instance of your Application Gateway in hello future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for hello backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create hello virtual network with hello previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a>공용 IP 주소 구성

주문 toohandle 외부 요청 응용 프로그램 게이트웨이 공용 IP 주소를 필요합니다. 이 공용 IP 주소가 없어야는 `DomainNameLabel` hello 응용 프로그램 게이트웨이 사용한 toobe를 정의 합니다.

```powershell
# Create a public IP address for use with hello Application Gateway. Defining hello domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-hello-application-gateway"></a>Hello 응용 프로그램 게이트웨이 구성 합니다.

```powershell
# Create a IP configuration. This configures what subnet hello Application Gateway uses. When Application Gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool toohold hello addresses or NICs for hello application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload hello authenication certificate that will be used toocommunicate with hello backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path too.cer file>

# Conifugre hello backend HTTP settings toobe used toodefine how traffic is routed toohello backend pool. hello authenication certificate used in hello previous step is added toohello backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port toobe used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration tooassociate hello public IP address with hello Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure hello certificate for hello Application Gateway. This certificate is used toodecrypt and re-encrypt hello traffic on hello Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>

# Create hello HTTP listener for hello Application Gateway. Assign hello front-end ip configuration, port, and ssl certificate toouse.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures hello load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU of hello Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define hello SSL policy toouse
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure hello waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create hello Application Gateway utilizing all hello previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> Hello 기본 웹 응용 프로그램 방화벽 구성을 사용 하 여 만든 응용 프로그램 게이트웨이 보호 기능에 대 한 CRS 3.0으로 구성 됩니다.

## <a name="get-application-gateway-dns-name"></a>Application Gateway DNS 이름 가져오기

Hello 게이트웨이가 생성 된 hello 다음 단계는 통신을 위해 tooconfigure hello 프런트 엔드입니다. 공용 IP를 사용할 때 Application Gateway는 친근한 이름이 아닌 동적으로 할당된 DNS 이름이 필요합니다. tooensure 최종 사용자가 응용 프로그램 게이트웨이 hello 적중할 수, CNAME 레코드를 사용 하는 toopoint toohello 공용 끝점의 응용 프로그램 게이트웨이 hello 될 수 있습니다. [Azure에서 사용자 지정 도메인 이름 구성](../cloud-services/cloud-services-custom-domain-name-portal.md). 별칭을 tooconfigure hello 응용 프로그램 게이트웨이 및 연결 된 hello PublicIPAddress 연결 요소 toohello 응용 프로그램 게이트웨이 사용 하 여 해당 IP/DNS 이름 세부 정보를 검색 합니다. hello 응용 프로그램 게이트웨이 DNS 이름이 사용 되는 toocreate CNAME 레코드는 포인트 hello 두 웹 응용 프로그램 toothis DNS 이름 이어야 합니다. A 레코드의 hello 사용 hello VIP는 응용 프로그램 게이트웨이 다시 시작으로 변동 될 수 있으므로 권장 되지 않습니다.

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

자세한 내용은 방법 tooconfigure 진단 로깅 toolog hello 되거나 되는 이벤트 검색 방문 하 여 웹 응용 프로그램 방화벽을 모두 방지할 [응용 프로그램 게이트웨이 진단](application-gateway-diagnostics.md)

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
