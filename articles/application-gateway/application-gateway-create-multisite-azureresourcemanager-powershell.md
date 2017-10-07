---
title: "여러 사이트를 호스팅하는 응용 프로그램 게이트웨이 aaaCreate | Microsoft Docs"
description: "이 페이지에서는 지침 toocreate hello에서 여러 웹 응용 프로그램에 대 한 Azure 응용 프로그램 게이트웨이 구성, 동일한 게이트웨이에 합니다."
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
ms.openlocfilehash: bad9a76be0a73a7026a770630fa7156f6e5940c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a>여러 웹 응용 프로그램을 호스트하는 응용 프로그램 게이트웨이 만들기

> [!div class="op_single_selector"]
> * [쉬운 테이블](application-gateway-create-multisite-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-multisite-azureresourcemanager-powershell.md)

여러 사이트 호스팅 사용 하면 하나의 웹 응용 프로그램 둘 이상의 toodeploy hello에 동일한 응용 프로그램 게이트웨이 합니다. Hello 들어오는 HTTP 요청에는 수신기가 트래픽을 받게 toodetermine 호스트 헤더의 존재 여부에 의존 합니다. hello 수신기는 다음 트래픽 tooappropriate 백 엔드 풀의 hello 게이트웨이 hello 규칙 정의에 구성 된 대로 지시 합니다. SSL 사용한 웹 응용 프로그램에서 응용 프로그램 게이트웨이 hello SNI 서버 이름 표시 () 확장 toochoose hello 올바른 수신기 hello 웹 트래픽에 대 한 사용합니다. 여러 사이트 호스팅에 대 한 일반적인 용도는 다른 웹 도메인 toodifferent 백 엔드 서버 풀에 대 한 tooload 잔액 요청입니다. 마찬가지로 여러 하위 도메인의 hello에 동일한 루트 도메인을 호스팅할 수 또한 동일한 응용 프로그램 게이트웨이 hello 합니다.

## <a name="scenario"></a>시나리오

다음 예제는 hello에서 응용 프로그램 게이트웨이으로 두 개의 백 엔드 서버 풀 contoso.com과 fabrikam.com을에 대 한 트래픽을 제공: contoso 서버 풀 및 fabrikam 서버 풀입니다. 유사한 설정을 app.contoso.com 및 blog.contoso.com와 같은 하위 도메인을 사용 하는 toohost 될 수 있습니다.

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a>시작하기 전에

1. Hello 웹 플랫폼 설치 관리자를 사용 하 여 hello 최신 버전의 hello Azure PowerShell cmdlet 설치 합니다. 다운로드 하 고 hello에서 hello 최신 버전을 설치할 수 **Windows PowerShell** hello 섹션 [다운로드 페이지](https://azure.microsoft.com/downloads/)합니다.
2. hello 서버 toohello 백 엔드 풀 toouse hello 응용 프로그램 게이트웨이 있어야 하거나 끝점 만든 hello 할당 된 공용 IP/VIP를 사용 하거나 별도 서브넷에서 가상 네트워크에 추가 합니다.

## <a name="requirements"></a>요구 사항

* **백 엔드 서버 풀:** hello hello 백 엔드 서버의 IP 주소 목록입니다. 나열 된 hello IP 주소 하거나 toohello 가상 네트워크 서브넷에 속해야 하거나 공용 IP/VIP가 있어야 합니다. FQDN을 사용할 수도 있습니다.
* **백 엔드 서버 풀 설정:** 모든 풀에는 포트, 프로토콜 및 쿠키 기반의 선호도와 같은 설정이 있습니다. 이러한 설정은 동률된 tooa 풀 및 hello 풀 내에서 적용 된 tooall 서버입니다.
* **프런트 엔드 포트:** 이 포트는 hello 응용 프로그램 게이트웨이에 열려 있는 hello 공용 포트입니다. 트래픽이이 포트에 도달 하 고 가져옵니다 hello 백 엔드 서버의 tooone 리디렉션됩니다.
* **수신기:** hello 수신기에는 프런트 엔드 포트 프로토콜 (Http 또는 Https의 경우, 이러한 값은 대/소문자 구분), 및 hello SSL 인증서 이름 (오프 로드 SSL 구성) 하는 경우. 다중 사이트 지원 응용 프로그램 게이트웨이의 경우 호스트 이름 및 SNI 표시도 추가됩니다.
* **규칙:** hello 규칙 hello 수신기를 hello 백 엔드 서버 풀에 바인딩하고 정의 백 엔드 서버 풀 hello 트래픽을 특정 수신기 페이로드만 directed toowhen 이어야 합니다. 트래픽 구체적인 정도 관계 없이 일치 하는 hello 첫 번째 규칙을 통해 이동 됩니다 및 규칙 나열 된 hello 순서로 처리 됩니다. 예를 들어 기본 수신기를 사용 하 여 규칙과 동일한 포트를 사용 하는 hello 규칙 hello에서 모두 다중 사이트 수신기를 사용 하 여 규칙을 설정한 경우 hello 다중 사이트 수신기 해야 보다 먼저 나열 되어야 hello 규칙으로 다중 사이트 규칙 toofunction hello에 대 한 순서 대로 기본 수신기 hello와 가 필요합니다.

## <a name="create-an-application-gateway"></a>응용 프로그램 게이트웨이 만들기

hello 다음은 위해 필요한 응용 프로그램 게이트웨이 toocreate hello 단계입니다.

1. 리소스 관리자에 대한 리소스 그룹을 만듭니다.
2. 가상 네트워크, 서브넷 및 응용 프로그램 게이트웨이 hello에 대 한 공용 IP를 만듭니다.
3. 응용 프로그램 게이트웨이 구성 개체를 만듭니다.
4. 응용 프로그램 게이트웨이 리소스를 만듭니다.

## <a name="create-a-resource-group-for-resource-manager"></a>리소스 관리자에 대한 리소스 그룹 만들기

Hello 최신 버전의 Azure PowerShell을 사용 하 고 있는지 확인 합니다. 자세한 내용은 [Resource Manager에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.

### <a name="step-1"></a>1단계

TooAzure 로그인

```powershell
Login-AzureRmAccount
```
사용자가 입력 정보 요청된 tooauthenticate 자격 증명입니다.

### <a name="step-2"></a>2단계

Hello 계정에 대 한 hello 구독을 확인 합니다.

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a>3단계

Azure 구독 toouse 선택 합니다.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>4단계

리소스 그룹을 만듭니다. 기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛰세요.

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

또는 응용 프로그램 게이트웨이의 리소스 그룹에 대한 태그를 만들 수도 있습니다.

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다. 이 위치는 해당 리소스 그룹의 리소스에 대 한 hello 기본 위치로 사용 됩니다. 모든 명령을 toocreate 응용 프로그램 게이트웨이 사용 하 여 hello 확인 동일한 리소스 그룹입니다.

리소스 그룹이 위의 hello 예제에서 만든 **appgw RG** 의 위치와 **West US**합니다.

> [!NOTE]
> 응용 프로그램 게이트웨이에 대 한 사용자 지정 프로브 tooconfigure 해야 할 경우 참조 [PowerShell을 사용 하 여 사용자 지정 프로브 사용 하 여 응용 프로그램 게이트웨이 만들](application-gateway-create-probe-ps.md)합니다. 자세한 내용은 [사용자 지정 프로브 및 상태 모니터링](application-gateway-probe-overview.md)으로 이동하세요.

## <a name="create-a-virtual-network-and-subnets"></a>가상 네트워크 및 서브넷 만들기

hello 방법을 예제와 다음 toocreate 리소스 관리자를 사용 하 여 가상 네트워크입니다. 이 단계에서는 두 개의 서브넷이 만들어집니다. 첫 번째 서브넷 hello hello 응용 프로그램 게이트웨이 자체입니다. 응용 프로그램 게이트웨이 해당 인스턴스는 자체 서브넷 toohold를 필요합니다. 다른 응용 프로그램 게이트웨이의 해당 서브넷에만 배포할 수 있습니다. hello 두 번째 서브넷이 사용 되는 toohold hello 응용 프로그램 백 엔드 서버.

### <a name="step-1"></a>1단계

Hello 주소 범위 10.0.0.0/24 toohello 서브넷 변수 toobe 사용 되는 toohold hello 응용 프로그램 게이트웨이 할당 합니다.

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a>2단계

Hello 주소 범위 10.0.1.0/24 toohello e t 2 변수 toobe hello 백 엔드 풀에 사용 되는 할당 합니다.

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a>3단계

명명 된 가상 네트워크 만들기 **appgwvnet** 리소스 그룹에 **appgw rg** hello 미국 서 부 지역 서브넷 10.0.0.0/24 hello 접두사 10.0.0.0/16 사용에 대 한 및 10.0.1.0/24 합니다.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a>4단계

응용 프로그램 게이트웨이 만드는 hello 다음 단계에 대 한 서브넷 변수를 할당 합니다.

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Hello 프런트 엔드 구성에 대 한 공용 IP 주소 만들기

공용 IP 리소스 만들기 **publicIP01** 리소스 그룹에 **appgw rg** hello 미국 서 부 지역에 대 한 합니다.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

IP 주소는 hello 서비스가 시작 될 때 toohello 응용 프로그램 게이트웨이 할당 됩니다.

## <a name="create-application-gateway-configuration"></a>응용 프로그램 게이트웨이 구성 만들기

Hello 응용 프로그램 게이트웨이 만들기 전에 모든 구성 항목을 tooset을 해야 합니다. hello 다음 단계 hello 구성 항목을 만드는 응용 프로그램 게이트웨이 리소스에 대 한 필요 합니다.

### <a name="step-1"></a>1단계

**gatewayIP01**이라는 응용 프로그램 게이트웨이 IP 구성을 만듭니다. 응용 프로그램 게이트웨이 시작할 때 구성 hello 서브넷에서 IP 주소를 선택 하 고 hello 백 엔드 IP 풀의 네트워크 트래픽을 toohello IP 주소를 라우팅합니다. 인스턴스마다 하나의 IP 주소를 사용합니다.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a>2단계

명명 된 hello 백 엔드 IP 주소 풀을 구성 **pool01** 및 **pool2** IP 주소와 **134.170.185.46**, **134.170.188.221**, **134.170.185.50** 에 대 한 **pool1** 및 **134.170.186.46**, **134.170.189.221**, **134.170.186.50**  에 대 한 **pool2**합니다.

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

이 예제는 hello 요청 된 사이트에 따라 두 개의 백 엔드 풀 tooroute 네트워크 트래픽의 합니다. 하나의 풀은 사이트 "contoso.com"에서 트래픽을 수신하고 또 다른 풀은 사이트 "fabrikam.com"에서 트래픽을 수신합니다. 사용자 고유의 응용 프로그램의 IP 주소 끝점 IP 주소 tooadd 앞 tooreplace hello를 해야 합니다. 내부 IP 주소 대신 공용 IP 주소, FQDN 또는 VM의 NIC를 백 엔드 인스턴스에 사용할 수도 있습니다. PowerShell 사용에 대신 Ip Fqdn toospecify "-BackendFQDNs" 매개 변수입니다.

### <a name="step-3"></a>3단계

응용 프로그램 게이트웨이 설정 구성 **poolsetting01** 및 **poolsetting02** hello 백 엔드 풀의 hello 부하 분산 된 네트워크 트래픽에 대 한 합니다. 이 예제에서는 hello 백 엔드 풀에 대 한 다른 백 엔드 풀 설정을 구성할 수 있습니다. 각 백 엔드 풀에는 고유한 백 엔드 풀 설정이 있을 수 있습니다.

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a>4단계

공용 IP 끝점으로 hello 프런트 엔드 IP를 구성 합니다.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a>5단계

Hello 프런트 엔드 포트에 대 한 응용 프로그램 게이트웨이 구성 합니다.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a>6단계

SSL 인증서를 두 개의 구성 hello 두 웹 사이트에 대 한이 예에서 toosupport는 것입니다. 인증서가 두 개는 contoso.com 트래픽 이며 다른 hello fabrikam.com 트래픽에 대 한 합니다. 이러한 인증서는 사용자 웹 사이트용으로 인증 기관에서 발급한 인증서여야 합니다. 자체 서명된 인증서는 지원되지만 프로덕션 트래픽에 권장되지 않습니다.

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a>7단계

이 예에서 hello 두 개의 웹 사이트에 대 한 두 가지 수신기를 구성 합니다. 이 단계에서는 사용 되는 tooreceive 들어오는 트래픽의 공용 IP 주소, 포트 및 호스트 hello 수신기를 구성 합니다. HostName 매개 변수는 여러 사이트 지원에 대 한 필요 하며 집합 toohello 적절 한 웹 사이트는 hello에 대 한 트래픽을 수신 이어야 합니다. Requireservernameindication이 매개 변수는 여러 호스트 시나리오에서 SSL에 대 한 지원이 필요로 하는 웹 사이트에 대 한 tootrue를 설정 되어야 합니다. SSL 지원이 필요한 경우 또한 해야 toospecify hello SSL 인증서 사용 되는 toosecure 트래픽이 해당 웹 응용 프로그램에 대 한 합니다. FrontendIPConfiguration, FrontendPort, 및 호스트 이름 조합을 hello 고유 tooa 수신기 이어야 합니다. 각 수신기는 하나의 인증서를 지원할 수 있습니다.

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a>8단계

이 예제에서 두 개의 웹 응용 프로그램을 hello에 대 한 설정 하는 두 개의 규칙을 만듭니다. 규칙은 수신기, 백 엔드 풀 및 http 설정을 연결합니다. 이 단계에서는 hello 응용 프로그램 게이트웨이 toouse 기본 라우팅 규칙을 각 웹 사이트에 대 한 구성 합니다. 트래픽 tooeach 웹 사이트는 해당 구성 된 수신기에서 수신 및 tooits 구성 BackendHttpSettings hello에 지정 된 hello 속성을 사용 하 여 백 엔드 풀을 향합니다.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a>9단계

Hello 인스턴스 수 및 크기 hello 응용 프로그램 게이트웨이를 구성 합니다.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a>응용 프로그램 게이트웨이 만들기

Hello 이전 단계에서에서 모든 구성 개체를 응용 프로그램 게이트웨이 만듭니다.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> 응용 프로그램 게이트웨이 프로 비전 장기 실행 작업으로 일부 시간 toocomplete 걸릴 수 있습니다.
> 
> 

## <a name="get-application-gateway-dns-name"></a>응용 프로그램 게이트웨이 DNS 이름 가져오기

Hello 게이트웨이가 생성 된 hello 다음 단계는 통신을 위해 tooconfigure hello 프런트 엔드입니다. 공용 IP를 사용할 때 Application Gateway는 식별 이름이 아닌 동적으로 할당된 DNS 이름이 필요합니다. tooensure 최종 사용자가 hello 응용 프로그램 게이트웨이 적중할 수, CNAME 레코드를 사용 하는 toopoint toohello hello 응용 프로그램 게이트웨이의 공용 끝점 수 있습니다. [Azure에서 사용자 지정 도메인 이름 구성](../cloud-services/cloud-services-custom-domain-name-portal.md). toodo hello 응용 프로그램 게이트웨이 및 연결 된 해당 IP/DNS 이름 hello PublicIPAddress 요소 toohello 연결 된 응용 프로그램 게이트웨이 사용 하 여이 검색 세부 정보입니다. hello 응용 프로그램 게이트웨이 DNS 이름이 사용 되는 toocreate CNAME 레코드는 포인트 hello 두 웹 응용 프로그램 toothis DNS 이름 이어야 합니다. A 레코드의 hello 사용 hello VIP는 응용 프로그램 게이트웨이 다시 시작으로 변동 될 수 있으므로 권장 되지 않습니다.

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

자세한 내용은 방법 tooprotect와 웹 사이트 [응용 프로그램 게이트웨이-웹 응용 프로그램 방화벽](application-gateway-webapplicationfirewall-overview.md)

