---
title: "Azure 응용 프로그램 게이트웨이-PowerShell에서 aaaConfigure SSL 정책 | Microsoft Docs"
description: "이 페이지에서는 Azure 응용 프로그램 게이트웨이에 지침 tooconfigure SSL 정책"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 7802ad3d3191a2fe9d88dddcb7c65bc4a70a419c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-policy-versions-and-cipher-suites-on-application-gateway"></a>Application Gateway에서 SSL 정책 버전 및 암호 그룹 구성

자세한 내용은 방법 tooconfigure SSL 정책 버전 암호 그룹에 응용 프로그램 게이트웨이 및 합니다. SSL 정책 버전의 다른 구성을 포함하고 암호 그룹을 사용하도록 설정하는 [미리 정의된 정책 목록](#predefined-ssl-policies)을 선택할 수 있습니다. Hello 기능 toodefine 있습니다는 [사용자 지정 SSL 정책](#configure-a-custom-ssl-policy) 요구 사항을 기반으로 합니다.

## <a name="get-available-ssl-options"></a>사용 가능한 SSL 옵션 가져오기

hello `Get-AzureRMApplicationGatewayAvailableSslOptions` cmdlet은 사용 가능한 미리 정의 된 정책, 사용할 수 있는 암호 그룹 및 구성할 수 있는 프로토콜 버전의 목록을 제공 합니다. hello 다음 예제에서는 hello cmdlet을 실행의 출력 예

```
DefaultPolicy: AppGwSslPolicy20150501
PredefinedPolicies:
    /subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups//providers/Microsoft.Network/ApplicationGatewayAvailableSslOptions/default/Applic
ationGatewaySslPredefinedPolicy/AppGwSslPolicy20150501
    /subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups//providers/Microsoft.Network/ApplicationGatewayAvailableSslOptions/default/Applic
ationGatewaySslPredefinedPolicy/AppGwSslPolicy20170401
    /subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups//providers/Microsoft.Network/ApplicationGatewayAvailableSslOptions/default/Applic
ationGatewaySslPredefinedPolicy/AppGwSslPolicy20170401S

AvailableCipherSuites:
    TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
    TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_DHE_RSA_WITH_AES_256_CBC_SHA
    TLS_DHE_RSA_WITH_AES_128_CBC_SHA
    TLS_RSA_WITH_AES_256_GCM_SHA384
    TLS_RSA_WITH_AES_128_GCM_SHA256
    TLS_RSA_WITH_AES_256_CBC_SHA256
    TLS_RSA_WITH_AES_128_CBC_SHA256
    TLS_RSA_WITH_AES_256_CBC_SHA
    TLS_RSA_WITH_AES_128_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
    TLS_DHE_DSS_WITH_AES_256_CBC_SHA256
    TLS_DHE_DSS_WITH_AES_128_CBC_SHA256
    TLS_DHE_DSS_WITH_AES_256_CBC_SHA
    TLS_DHE_DSS_WITH_AES_128_CBC_SHA
    TLS_RSA_WITH_3DES_EDE_CBC_SHA
    TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA

AvailableProtocols:
    TLSv1_0
    TLSv1_1
    TLSv1_2
```

## <a name="list-pre-defined-ssl-policies"></a>미리 정의된 SSL 정책 나열

Application Gateway는 사용할 수 있는 미리 정의된 3가지 정책을 함께 제공합니다. hello `Get-AzureRmApplicationGatewaySslPredefinedPolicy` cmdlet 이러한 정책을 검색 합니다. 각 정책에는 다른 프로토콜 버전 및 암호 그룹을 사용 하도록 설정했습니다. 이러한 미리 정의 된 정책을 사용할 수 있습니다 tooquickly 응용 프로그램 게이트웨이에 대 한 SSL 정책을 구성 합니다. 기본적으로 **AppGwSslPolicy20170401**은 특정 SSL 정책이 정의되지 않은 경우에 선택됩니다.

hello 다음은 실행의 예가 `Get-AzureRmApplicationGatewaySslPredefinedPolicy`합니다.

```
Name: AppGwSslPolicy20150501
MinProtocolVersion: TLSv1_0
CipherSuites:
    TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
    TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_DHE_RSA_WITH_AES_256_CBC_SHA
    TLS_DHE_RSA_WITH_AES_128_CBC_SHA
    TLS_RSA_WITH_AES_256_GCM_SHA384
 ...
Name: AppGwSslPolicy20170401
MinProtocolVersion: TLSv1_1
CipherSuites:
    TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
...
```

## <a name="configure-a-custom-ssl-policy"></a>사용자 지정 SSL 정책 구성

다음 예제는 hello 응용 프로그램 게이트웨이 사용자 지정 SSL 정책을 설정 합니다. Hello 최소 프로토콜 버전을 너무 설정`TLSv1_1` 활성화 hello 암호 그룹에 따라:

* TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
* TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256

> [!IMPORTANT]
> 사용자 지정 SSL 정책을 구성할 때 hello 다음 목록에서에서 하나 이상의 암호 그룹을 선택 해야 합니다. Application Gateway는 백 엔드 관리를 위해 RSA SHA256 암호 그룹을 사용합니다.
> * TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 
> * TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
> * TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
> * TLS_RSA_WITH_AES_128_GCM_SHA256
> * TLS_RSA_WITH_AES_256_CBC_SHA256
> * TLS_RSA_WITH_AES_128_CBC_SHA256

```powershell
# get an application gateway resource
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroup AdatumAppGatewayRG

# set hello SSL policy on hello application gateway
Set-AzureRmApplicationGatewaySslPolicy -ApplicationGateway $gw -PolicyType Custom -MinProtocolVersion TLSv1_1 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-an-application-gateway-with-a-pre-defined-ssl-policy"></a>미리 정의된 SSL 정책을 사용하여 Application Gateway 만들기

hello 다음 예제에서는 새 응용 프로그램 게이트웨이 미리 정의 된 SSL 정책을 사용 하 여

```powershell
# Create a resource group
$rg = New-AzureRmResourceGroup -Name ContosoRG -Location "East US"
# Create a subnet for hello application gateway
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
# Create a virtual network with a 10.0.0.0/16 address space
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName $rg.ResourceGroupName -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
# Retrieve hello subnet object for later use
$subnet = $vnet.Subnets[0]
# Create a public IP address
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName $rg.ResourceGroupName -name publicIP01 -location "East US" -AllocationMethod Dynamic
# Create a ip configuration object
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
# Create a backend pool for backend web servers
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
# Define hello backend http settings toobe used.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
# Create a new port for SSL
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
# Upload an existing pfx certificate for SSL offload
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile C:\folder\contoso.pfx -Password "P@ssw0rd"
# Create a frontend IP configuration for hello public IP address
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
# Create a new listener with hello certificate, port, and frontend ip.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
# Create a new rule for backend traffic routing
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
# Define hello size of hello application gateway
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
# Configure hello SSL policy toouse a different pre-defined policy
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
# Create hello application gateway.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName $rg.ResourceGroupName -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

## <a name="next-steps"></a>다음 단계

방문 [응용 프로그램 게이트웨이 리디렉션 개요](application-gateway-redirect-overview.md) toolearn 어떻게 tooredirect HTTP 트래픽을 tooa HTTPS 끝점입니다.
