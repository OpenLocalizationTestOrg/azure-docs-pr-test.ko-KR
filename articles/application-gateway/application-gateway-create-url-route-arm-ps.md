---
title: "URL 라우팅을 사용 하 여 응용 프로그램 게이트웨이 규칙 aaaCreate | Microsoft Docs"
description: "이 페이지에서는 지침 toocreate, URL 라우팅 규칙을 사용 하 여 Azure 응용 프로그램 게이트웨이 구성 합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d141cfbb-320a-4fc9-9125-10001c6fa4cf
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 54fcccc39e48a933576968ce3d8160518c0d0b7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a>경로 기반 라우팅을 사용하여 응용 프로그램 게이트웨이 만들기

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-create-url-route-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-url-route-arm-ps.md)
> * [Azure CLI 2.0](application-gateway-create-url-route-cli.md)

URL 라우팅 경로 기반 있습니다 tooassociate 경로 Http 요청의 hello URL 경로에 따라 수 있습니다. 응용 프로그램 게이트웨이 hello에 제공 된 hello URL에 대해 구성 하는 경로 tooa 백 엔드 풀 인지 확인 합니다. 그런 다음 hello 네트워크 트래픽 toohello 백 엔드 풀 정의 보냅니다. URL 기반 라우팅에 대 한 일반적인 용도는 서로 다른 내용 유형 toodifferent 백 엔드 서버 풀에 대 한 tooload 잔액 요청입니다.

URL 기반 라우팅 새 규칙 유형 tooapplication 게이트웨이 소개합니다. 응용 프로그램 게이트웨이에는 두 가지 규칙 형식(기본 및 PathBasedRouting)이 있습니다. 기본 규칙 종류는 hello 백 엔드에 대 한 라운드 로빈 서비스 PathBasedRouting 하면서 또한 tooround 로빈 배포 풀, 고려 hello 요청 URL의 경로 패턴 hello 백 엔드 풀을 선택 하는 동안를 제공 합니다.

## <a name="scenario"></a>시나리오

다음 예제는 hello에서 응용 프로그램 게이트웨이 백 엔드 서버 풀 두으로 contoso.com에 대 한 트래픽을 제공: 비디오 서버 풀 및 이미지 서버 풀입니다.

요청 http://contoso.com/image * 라우팅되에 tooimage 서버 풀 (pool1) 및 http://contoso.com/video * 라우팅되 toovideo 서버 풀 (pool2). hello 경로 패턴 일치 하는, 기본 서버 풀 (pool1)을 선택 합니다.

![url 경로](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a>시작하기 전에

1. Hello 웹 플랫폼 설치 관리자를 사용 하 여 hello 최신 버전의 hello Azure PowerShell cmdlet 설치 합니다. 다운로드 하 고 hello에서 hello 최신 버전을 설치할 수 **Windows PowerShell** hello 섹션 [다운로드 페이지](https://azure.microsoft.com/downloads/)합니다.
2. Application Gateway에 대한 가상 네트워크 및 서브넷을 만듭니다. 가상 컴퓨터 또는 클라우드 배포 없습니다 hello 서브넷 사용 하 고 있는지 확인 합니다. hello 응용 프로그램 게이트웨이 자체 가상 네트워크 서브넷에 있어야 합니다.
3. hello 서버 toohello 백 엔드 풀 toouse hello 응용 프로그램 게이트웨이 있어야 하거나 끝점 만든 hello 가상 네트워크 또는 할당 된 공용 IP/VIP와 추가 합니다.

## <a name="what-is-required-toocreate-an-application-gateway"></a>필요한 toocreate 응용 프로그램 게이트웨이 란?

* **백 엔드 서버 풀:** hello hello 백 엔드 서버의 IP 주소 목록입니다. 나열 된 hello IP 주소 하거나 toohello 가상 네트워크 서브넷에 속해야 하거나 공용 IP/VIP가 있어야 합니다.
* **백 엔드 서버 풀 설정:** 모든 풀에는 포트, 프로토콜 및 쿠키 기반의 선호도와 같은 설정이 있습니다. 이러한 설정은 동률된 tooa 풀 및 hello 풀 내에서 적용 된 tooall 서버입니다.
* **프런트 엔드 포트:** 이 포트는 hello 응용 프로그램 게이트웨이에 열려 있는 hello 공용 포트입니다. 트래픽이이 포트에 도달 하 고 가져옵니다 hello 백 엔드 서버의 tooone 리디렉션됩니다.
* **수신기:** hello 수신기에는 프런트 엔드 포트 프로토콜 (Http 또는 Https의 경우, 이러한 값은 대/소문자 구분), 및 hello SSL 인증서 이름 (오프 로드 SSL 구성) 하는 경우.
* **규칙:** hello 규칙 hello 수신기를 hello 백 엔드 서버 풀에 바인딩하고 정의 백 엔드 서버 풀 hello 트래픽을 특정 수신기 페이로드만 directed toowhen 이어야 합니다.

## <a name="create-an-application-gateway"></a>응용 프로그램 게이트웨이 만들기

hello Azure 클래식 및 Azure 리소스 관리자를 사용 하는 차이점은 hello 응용 프로그램 게이트웨이 및 toobe 구성 해야 하는 hello 항목을 만들 있는 hello 순서입니다.

리소스 관리자와 응용 프로그램 게이트웨이 구성 하는 모든 항목은 개별적으로 구성 하 고 다음 조립 toocreate hello 응용 프로그램 게이트웨이 리소스입니다.

필요한 toocreate 응용 프로그램 게이트웨이 hello 단계는 다음과 같습니다.

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

사용자가 입력 정보 요청된 tooauthenticate 자격 증명입니다.<BR>

### <a name="step-2"></a>2단계

Hello 계정에 대 한 hello 구독을 확인 합니다.

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a>3단계

Azure 구독 toouse 선택 합니다. <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>4단계

리소스 그룹을 만듭니다. 기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛰세요.

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

또는 응용 프로그램 게이트웨이의 리소스 그룹에 대한 태그를 만들 수도 있습니다.

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다. 이 리소스 그룹은 해당 리소스 그룹의 리소스에 대 한 hello 기본 위치로 사용 됩니다. 모든 명령을 toocreate 응용 프로그램 게이트웨이 사용 하 여 hello 확인 동일한 리소스 그룹입니다.

Hello 위의 예에서 "appgw RG" 및 "West US" 위치 라는 리소스 그룹을 만들었습니다.

> [!NOTE]
> 응용 프로그램 게이트웨이에 대 한 사용자 지정 프로브 tooconfigure 해야 할 경우 참조 [PowerShell을 사용 하 여 사용자 지정 프로브 사용 하 여 응용 프로그램 게이트웨이 만들](application-gateway-create-probe-ps.md)합니다. 자세한 내용은 [사용자 지정 프로브 및 상태 모니터링](application-gateway-probe-overview.md) 을 확인합니다.
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>가상 네트워크 및 서브넷을 hello 응용 프로그램 게이트웨이 만들기

hello 방법을 예제와 다음 toocreate 리소스 관리자를 사용 하 여 가상 네트워크입니다. 이 예제는 hello 응용 프로그램 게이트웨이 용 VNET을 만듭니다. 응용 프로그램 게이트웨이 응용 프로그램 게이트웨이 hello에 대 한 작성 hello 서브넷 hello VNET 주소 공간 보다 작습니다. 따라서 자체 서브넷이 필요 합니다. 이 통해 다른 리소스에 포함 되지만 hello에서 제한 되지 tooweb 서버 toobe 구성 동일한 VNET입니다.

### <a name="step-1"></a>1단계

Hello 주소 범위 10.0.0.0/24 toohello 서브넷 사용 되는 변수 toobe toocreate 가상 네트워크를 할당 합니다.  Hello 다음 예제에 사용 되는 응용 프로그램 게이트웨이 hello에 대 한 hello 서브넷 configuration 개체를 만듭니다.

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a>2단계

명명 된 가상 네트워크 만들기 **appgwvnet** 리소스 그룹에 **appgw rg** hello 미국 서 부 지역 서브넷 10.0.0.0/24 hello 접두사 10.0.0.0/16 사용에 대 한 합니다. 이 응용 프로그램 게이트웨이 tooreside hello에 대 한 단일 서브넷 hello VNET의 hello 구성을 완료합니다.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a>3단계

다음 단계 hello에 대 한 hello 서브넷 변수 할당을 toohello 전달이 `New-AzureRMApplicationGateway` cmdlet는 향후 단계에 있습니다.

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Hello 프런트 엔드 구성에 대 한 공용 IP 주소 만들기

공용 IP 리소스 만들기 **publicIP01** 리소스 그룹에 **appgw rg** hello 미국 서 부 지역에 대 한 합니다. 응용 프로그램 게이트웨이 부하 분산에 대 한 공용 IP 주소를, 내부 IP 주소 또는 tooreceive 요청 모두 사용할 수 있습니다.  이 예제에서는 공용 IP 주소만 사용합니다. 다음 예제는 hello, DNS 이름이 없는 hello 공용 IP 주소를 만들기 위한 구성 됩니다.  Application Gateway는 공용 IP 주소에서 사용자 지정 DNS 이름을 지원하지 않습니다.  사용자 지정 이름을 hello 공용 끝점에 대 한 필요한 경우 toopoint toohello 자동으로 생성 된 DNS 이름 hello 공용 IP 주소에 대 한 CNAME 레코드를 만들어야 합니다.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

IP 주소는 hello 서비스가 시작 될 때 toohello 응용 프로그램 게이트웨이 할당 됩니다.

## <a name="create-application-gateway-configuration"></a>응용 프로그램 게이트웨이 구성 만들기

Hello 응용 프로그램 게이트웨이 만들기 전에 모든 구성 항목 설정 해야 합니다. hello 다음 단계 hello 구성 항목을 만드는 응용 프로그램 게이트웨이 리소스에 대 한 필요 합니다.

### <a name="step-1"></a>1단계

**gatewayIP01**이라는 응용 프로그램 게이트웨이 IP 구성을 만듭니다. 응용 프로그램 게이트웨이 시작할 때 구성 hello 서브넷에서 IP 주소를 선택 하 고 hello 백 엔드 IP 풀의 네트워크 트래픽을 toohello IP 주소를 라우팅합니다. 인스턴스마다 하나의 IP 주소를 사용합니다.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a>2단계

명명 된 hello 백 엔드 IP 주소 풀을 구성 **pool01** 및 **pool2** 에 대 한 IP 주소와 **pool1** 및 **pool2**합니다. 이러한 IP 주소는 hello 웹 응용 프로그램 toobe hello 응용 프로그램 게이트웨이 의해 보호를 호스트 하는 hello 리소스의 hello IP 주소입니다. 이러한 백 엔드 풀 멤버는 기본 프로브 또는 사용자 지정 프로브 모든 유효성이 검사 된 toobe 프로브 정상는입니다.  트래픽 라우팅됩니다 toothem 요청 hello 응용 프로그램 게이트웨이에 도달 합니다. 즉, 한 백 엔드 풀 동일 hello에 상주 하는 여러 웹 응용 프로그램에 사용 될 수는 hello 응용 프로그램 게이트웨이 내에서 여러 규칙에서 백 엔드 풀을 사용할 수 호스트 합니다.

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

이 예제에서는 hello URL 경로에 따라 두 개의 백 엔드 풀 tooroute 네트워크 트래픽이 있습니다. 하나의 풀은 URL 경로 "/video"에서 트래픽을 수신하고 또 다른 풀은 경로 "/image"에서 트래픽을 수신합니다. 사용자 고유의 응용 프로그램의 IP 주소 끝점 IP 주소 tooadd 앞 hello를 대체 합니다. 

### <a name="step-3"></a>3단계

응용 프로그램 게이트웨이 설정 구성 **poolsetting01** 및 **poolsetting02** hello 백 엔드 풀의 hello 부하 분산 된 네트워크 트래픽에 대 한 합니다. 이 예제에서는 hello 백 엔드 풀에 대 한 다른 백 엔드 풀 설정을 구성할 수 있습니다. 각 백 엔드 풀에는 고유한 백 엔드 풀 설정이 있을 수 있습니다.  백 엔드 HTTP 설정 규칙 tooroute 트래픽 toohello 올바른 백 엔드 풀 멤버에서 사용 합니다. Hello 프로토콜 및 백 엔드 풀 멤버가 toohello 트래픽을 보낼 때 사용 되는 포트를 결정 합니다. 쿠키 기반 세션 hello 백 엔드 HTTP 설정에 따라 결정 됩니다.  쿠키 기반 세션 선호도 트래픽 toohello 보냅니다 설정 된 경우 각 패킷에 대 한 이전 요청으로 동일한 백 엔드 합니다.

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a>4단계

공용 IP 끝점으로 hello 프런트 엔드 IP를 구성 합니다. hello 프런트 엔드 IP 구성 개체 연결 hello 수신기와 함께 IP 주소 바깥쪽 수신기 toorelate hello에서 사용 됩니다.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a>5단계

Hello 프런트 엔드 포트에 대 한 응용 프로그램 게이트웨이 구성 합니다. hello 프런트 엔드 포트 구성 개체는 hello 수신기에서 트래픽을 hello 응용 프로그램 게이트웨이 수신 포트 기능 수신기 toodefine에서 사용 됩니다.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a>6단계

Hello 수신기를 구성 합니다. 이 단계 hello 공용 IP 주소에 대 한 hello 수신기를 구성 하 고 포트 tooreceive 들어오는 네트워크 트래픽을 사용 됩니다. 다음 예제는 hello hello 이전에 구성 된 프런트 엔드 IP 구성, 프런트 엔드 포트 구성 및 프로토콜 (http 또는 https)을 사용 하 고 hello 수신기를 구성 합니다. 이 예제에서는 hello 수신기 tooHTTP 트래픽을 이전 작성 된 hello 공용 IP 주소에 포트 80에서 수신 합니다.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a>7단계

Hello 백 엔드 풀에 대 한 규칙 경로 URL을 구성 합니다. 이 단계는 응용 프로그램 게이트웨이에서 사용 하는 hello 상대 경로 구성 하 고 hello URL 경로 toohandle hello 들어오는 트래픽을 할당 된 hello 백 엔드 풀 간의 hello 매핑을 정의 합니다.

> [!IMPORTANT]
> 각 경로로 시작 해야 / hello만 장소는 "\*" hello 끝에를 허용 합니다. 사용 가능한 예는 /xyz, /xyz* 또는 /xyz/*입니다. hello toohello 경로 검색 도구를 공급 하는 문자열을 다루지 않습니다 텍스트 hello 후 처음 "?" 또는 "#", 및 이러한 문자는 허용 되지 않습니다. 

hello 다음 예제에서는 두 개의 규칙을 만듭니다: tooback 엔드 "pool1" 및 "/" (비디오/간 tooback "pool2" 트래픽 라우팅 경로 대 한 다른 하나의 "/" (이미지/경로 라우팅에 대 한 트래픽 이러한 규칙 url 각 집합에 대 한 트래픽이 라우팅된 toohello 백 엔드 인지 확인 합니다. 예를 들어 http://contoso.com/image/figure1.jpg toopool1 들어가고 http://contoso.com/video/example.mp4 toopool2 이동 됩니다.

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

Hello 경로 hello 미리 정의 된 경로 규칙이 일치 하지 않으면, hello 규칙 경로 맵 구성도 기본 백 엔드 주소 풀을 구성 합니다. 예를 들어 http://contoso.com/shoppingcart/test.html가 일치 하지 않는 트래픽에 대 한 hello 기본 풀으로 정의 된 대로 toopool1를 이동 합니다.

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a>8단계

규칙 설정을 만듭니다. 이 단계에서는 hello 응용 프로그램 게이트웨이 toouse URL 경로 기반 라우팅을 구성 합니다. hello `$urlPathMap` 정의 된 변수 hello에 이전 단계는 현재 사용 되는 toocreate hello 경로 기반 규칙입니다. 이 단계에서는 앞에서 만든 hello url 경로 매핑 수신기와 hello 규칙을 연결 합니다.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a>9단계

Hello 인스턴스 수 및 크기 hello 응용 프로그램 게이트웨이를 구성 합니다.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a>Application Gateway 만들기

Hello 이전 단계에서에서 모든 구성 개체를 응용 프로그램 게이트웨이 만듭니다.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a>응용 프로그램 게이트웨이 DNS 이름 가져오기

Hello 게이트웨이가 생성 된 hello 다음 단계는 통신을 위해 tooconfigure hello 프런트 엔드입니다. 공용 IP를 사용할 때 Application Gateway는 식별 이름이 아닌 동적으로 할당된 DNS 이름이 필요합니다. tooensure 최종 사용자가 hello 응용 프로그램 게이트웨이 적중할 수, CNAME 레코드를 사용 하는 toopoint toohello hello 응용 프로그램 게이트웨이의 공용 끝점 수 있습니다. [Azure에서 사용자 지정 도메인 이름 구성](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure hello 프런트 엔드 IP CNAME 레코드는 hello 응용 프로그램 게이트웨이 및 연결 된 해당 IP/DNS 이름 hello PublicIPAddress 요소 toohello 연결 된 응용 프로그램 게이트웨이 사용 하 여 세부 정보를 검색 합니다. hello 응용 프로그램 게이트웨이 DNS 이름이 사용 되는 toocreate CNAME 레코드를 이어야 합니다. A 레코드의 hello 사용 hello VIP는 응용 프로그램 게이트웨이 다시 시작으로 변동 될 수 있으므로 권장 되지 않습니다.

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

Secure Sockets Layer (SSL)를 오프 로드 toolearn 참조 [SSL 오프 로드에 대 한 응용 프로그램 게이트웨이 구성](application-gateway-ssl-arm.md)합니다.

