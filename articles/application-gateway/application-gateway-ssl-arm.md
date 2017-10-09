---
title: "-Azure 응용 프로그램 게이트웨이-PowerShell aaaConfigure SSL 오프 로드를 | Microsoft Docs"
description: "이 페이지에서는 Azure 리소스 관리자를 사용 하 여 응용 프로그램 게이트웨이 ssl 오프 로드 하는 지침 toocreate 제공"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 3c3681e0-f928-4682-9d97-567f8e278e13
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: c2855d8d3caaa97ec05475c67ff0f8dce72ef2a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a>Azure Resource Manager를 사용하여 SSL 오프로드에 대한 응용 프로그램 게이트웨이 구성

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-ssl-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-ssl-arm.md)
> * [Azure 클래식 PowerShell](application-gateway-ssl.md)
> * [Azure CLI 2.0](application-gateway-ssl-cli.md)

Azure 응용 프로그램 게이트웨이 hello 게이트웨이 tooavoid 비용이 많이 드는 SSL 암호 해독 작업 toohappen hello 웹 팜에서에 구성 된 tooterminate hello (SECURE Sockets Layer) 세션 수 있습니다. SSL 오프 로드 hello 프런트 엔드 서버 설치 및 hello 웹 응용 프로그램 관리를 단순화합니다.

## <a name="before-you-begin"></a>시작하기 전에

1. Hello 웹 플랫폼 설치 관리자를 사용 하 여 hello 최신 버전의 hello Azure PowerShell cmdlet 설치 합니다. 다운로드 하 고 hello에서 hello 최신 버전을 설치할 수 **Windows PowerShell** hello 섹션 [다운로드 페이지](https://azure.microsoft.com/downloads/)합니다.
2. 가상 네트워크 및 서브넷을 hello 응용 프로그램 게이트웨이 만듭니다. 가상 컴퓨터 또는 클라우드 배포 없습니다 hello 서브넷 사용 하 고 있는지 확인 합니다. 응용 프로그램 게이트웨이는 가상 네트워크 서브넷에서 단독이어야 합니다.
3. toouse hello 응용 프로그램 게이트웨이 구성 하는 hello 서버 있어야 하거나 끝점 만든 hello 가상 네트워크 또는 할당 된 공용 IP/VIP와 합니다.

## <a name="what-is-required-toocreate-an-application-gateway"></a>필요한 toocreate 응용 프로그램 게이트웨이 란?

* **백 엔드 서버 풀:** hello hello 백 엔드 서버의 IP 주소 목록입니다. 나열 된 hello IP 주소 하거나 toohello 가상 네트워크 서브넷에 속해야 하거나 공용 IP/VIP가 있어야 합니다.
* **백 엔드 서버 풀 설정:** 모든 풀에는 포트, 프로토콜 및 쿠키 기반의 선호도와 같은 설정이 있습니다. 이러한 설정은 동률된 tooa 풀 및 hello 풀 내에서 적용 된 tooall 서버입니다.
* **프런트 엔드 포트:** 이 포트는 hello 응용 프로그램 게이트웨이에 열려 있는 hello 공용 포트입니다. 트래픽이이 포트에 도달 하 고 가져옵니다 hello 백 엔드 서버의 tooone 리디렉션됩니다.
* **수신기:** hello 수신기에는 프런트 엔드 포트 프로토콜 (Http 또는 Https의 경우, 이러한 설정은 대/소문자 구분) 및 hello SSL 인증서 이름 (오프 로드 SSL 구성) 하는 경우.
* **규칙:** hello 규칙 hello 수신기 및 hello 백 엔드 서버 풀 바인딩하고 정의 백 엔드 서버 풀 hello 트래픽을 특정 수신기 페이로드만 directed toowhen 이어야 합니다. 현재만 hello *기본* 규칙 지원 됩니다. hello *기본* 규칙은 라운드 로빈 부하 분산 합니다.

**추가 구성 정보**

SSL 인증서 구성에 대 한 프로토콜에서 hello **HttpListener** 도 변경 해야*Https* (대/소문자 구분). hello **SslCertificate** 요소가 너무 추가**HttpListener** hello SSL 인증서에 대해 구성 하는 hello 변수 값으로. hello 프런트 엔드 포트에는 업데이트 된 too443 해야 합니다.

**tooenable 쿠키 기반 선호도**: 응용 프로그램 게이트웨이 클라이언트 세션에서 요청은 항상 방향이 지정 된 toohello 구성된 tooensure 수 hello 웹 팜의 동일한 VM입니다. 이 시나리오는 hello 게이트웨이 toodirect 트래픽을 적절 하 게 허용 하는 세션 쿠키의 삽입으로 수행 됩니다. tooenable 쿠키 기반 선호도 설정 **CookieBasedAffinity** 너무*Enabled* hello에 **BackendHttpSettings** 요소입니다.

## <a name="create-an-application-gateway"></a>응용 프로그램 게이트웨이 만들기

hello hello Azure 클래식 배포 모델 및 Azure 리소스 관리자를 사용 하는 차이점은 toobe 구성 해야 하는 응용 프로그램 게이트웨이와 hello 항목이 만드는 hello 순서입니다.

리소스 관리자와 응용 프로그램 게이트웨이의 모든 구성 요소는 개별적으로 구성 하 고 다음 관리 함께 toocreate 응용 프로그램 게이트웨이 리소스입니다.

응용 프로그램 게이트웨이 hello 필요한 단계 toocreate 키를 같습니다.

1. 리소스 관리자에 대한 리소스 그룹 만들기
2. 가상 네트워크, 서브넷 및 응용 프로그램 게이트웨이 hello에 대 한 공용 IP 만들기
3. 응용 프로그램 게이트웨이 구성 개체 만들기
4. 응용 프로그램 게이트웨이 리소스 만들기

## <a name="create-a-resource-group-for-resource-manager"></a>리소스 관리자에 대한 리소스 그룹 만들기

PowerShell 모드 toouse hello Azure 리소스 관리자 cmdlet을 전환 하면 있는지 확인 합니다. 자세한 내용은 [Resource Manager에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.

### <a name="step-1"></a>1단계

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>2단계

Hello 계정에 대 한 hello 구독을 확인 합니다.

```powershell
Get-AzureRmSubscription
```

사용자가 입력 정보 요청된 tooauthenticate 자격 증명입니다.

### <a name="step-3"></a>3단계

Azure 구독 toouse 선택 합니다.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>4단계

리소스 그룹을 만듭니다. 기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛰세요.

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다. 이 설정은 해당 리소스 그룹의 리소스에 대 한 hello 기본 위치로 사용 됩니다. 응용 프로그램 게이트웨이 사용 하 여 모든 명령을 toocreate hello 동일 하 고 있는지 확인 리소스 그룹입니다.

리소스 그룹이 위의 hello 예제에서 만든 **appgw RG** 및 위치 **West US**합니다.

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>가상 네트워크 및 서브넷을 hello 응용 프로그램 게이트웨이 만들기

hello 방법을 예제와 다음 toocreate 리소스 관리자를 사용 하 여 가상 네트워크:

### <a name="step-1"></a>1단계

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

이 샘플 hello 주소 범위 10.0.0.0/24 tooa 서브넷 사용 되는 변수 toobe toocreate 가상 네트워크를 할당합니다.

### <a name="step-2"></a>2단계

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

이 샘플 이라는 가상 네트워크를 만들어 **appgwvnet** 리소스 그룹에 **appgw rg** hello 미국 서 부 지역 서브넷 10.0.0.0/24 hello 접두사 10.0.0.0/16 사용에 대 한 합니다.

### <a name="step-3"></a>3단계

```powershell
$subnet = $vnet.Subnets[0]
```

이 샘플에는 hello 서브넷 개체 toovariable $subnet hello 다음 단계에 대 한 할당합니다.

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Hello 프런트 엔드 구성에 대 한 공용 IP 주소 만들기

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

이 샘플에서는 공용 IP 리소스 **publicIP01** 리소스 그룹에 **appgw rg** hello 미국 서 부 지역에 대 한 합니다.

## <a name="create-an-application-gateway-configuration-object"></a>응용 프로그램 게이트웨이 구성 개체 만들기

### <a name="step-1"></a>1단계

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

이 샘플은 **gatewayIP01**이라는 Application Gateway IP 구성을 만듭니다. 응용 프로그램 게이트웨이 시작할 때 구성 hello 서브넷에서 IP 주소를 선택 하 고 hello 백 엔드 IP 풀의 네트워크 트래픽을 toohello IP 주소를 라우팅합니다. 인스턴스마다 하나의 IP 주소를 사용합니다.

### <a name="step-2"></a>2단계

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

이 샘플에서는 이라는 hello 백 엔드 IP 주소 풀을 구성 **pool01** IP 주소와 **134.170.185.46**, **134.170.188.221**, **134.170.185.50** . 이러한 값은 hello 프런트 엔드 IP 끝점에서 제공 되는 hello 네트워크 트래픽을 수신 하는 hello IP 주소입니다. Hello hello IP 주소와 웹 응용 프로그램 끝점의 예를 앞에서 hello IP 주소를 대체 합니다.

### <a name="step-3"></a>3단계

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

이 샘플에서는 응용 프로그램 게이트웨이 설정 구성 **poolsetting01** hello 백 엔드 풀에서 네트워크 트래픽을 tooload 분산 합니다.

### <a name="step-4"></a>4단계

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

이 샘플에서는 명명 된 hello 프런트 엔드 IP 포트 구성 **frontendport01** hello 공용 IP 끝점에 대 한 합니다.

### <a name="step-5"></a>5단계

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

이 샘플에서는 SSL 연결에 사용 되는 hello 인증서를 구성 합니다. hello 인증서.pfx 형식에서 toobe 하며 hello 암호 4 too12 자 사이 여야 합니다.

### <a name="step-6"></a>6단계

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

이 샘플에서는 라는 hello 프런트 엔드 IP 구성을 만듭니다. **fipconfig01** associates hello hello 프런트 엔드 IP 구성 사용 하 여 공용 IP 주소 및 합니다.

### <a name="step-7"></a>7단계

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

이 샘플에서는 수신기 이름을 hello 만듭니다 **listener01** 프런트 엔드 포트 toohello 프런트 엔드 IP 구성 및 인증서 associates hello 및 합니다.

### <a name="step-8"></a>8단계

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

이 샘플에서는 hello 부하 분산 장치 라우팅 규칙 이라는 만듭니다 **rule01** hello 부하 분산 장치 동작을 구성 하는 합니다.

### <a name="step-9"></a>9단계

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

이 샘플에서는 hello 인스턴스 크기의 hello 응용 프로그램 게이트웨이 구성 합니다.

> [!NOTE]
> 기본값에 대 한 hello *InstanceCount* 최대 값이 10 인 2입니다. 에 대 한 기본값을 hello *GatewaySize* 보통입니다. Standard_Small, Standard_Medium 및 Standard_Large 간에 선택할 수 있습니다.

### <a name="step-10"></a>10단계

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

이 단계는 hello 응용 프로그램 게이트웨이에 hello SSL 정책 toouse를 정의합니다. 방문 [SSL 구성 정책 버전 및 응용 프로그램 게이트웨이에 암호 그룹](application-gateway-configure-ssl-policy-powershell.md) toolearn 더 합니다.

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a>New-AzureApplicationGateway를 사용하여 응용 프로그램 게이트웨이 만들기

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

이 샘플에서는 hello 이전 단계에서에서 모든 구성 항목을 포함 한 응용 프로그램 게이트웨이 만듭니다. Hello 예제에서는 응용 프로그램 게이트웨이 hello 라고 **appgwtest**합니다.

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

내부 부하 분산 장치 ILB ()는 응용 프로그램 게이트웨이 toouse tooconfigure 참조 [내부 부하 분산 장치 (ILB) 응용 프로그램 게이트웨이 만들](application-gateway-ilb.md)합니다.

보다 자세한 내용을 원한다면 일반적 부하 분산 옵션을 참조:

* [Azure 부하 분산 장치](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

