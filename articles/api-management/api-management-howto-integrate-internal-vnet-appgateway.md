---
title: "aaaHow toouse 응용 프로그램 게이트웨이 사용 하 여 가상 네트워크에서 Azure API 관리 | Microsoft Docs"
description: "자세한 내용은 방법 toosetup 및 내부 가상 네트워크와 응용 프로그램 게이트웨이 (WAF) 프런트 엔드로의 Azure API 관리 구성"
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: antonba
ms.assetid: a8c982b2-bca5-4312-9367-4a0bbc1082b1
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2017
ms.author: sasolank
ms.openlocfilehash: 74303a2ee8a10db633ab1740ec7267728eacb473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a>내부 VNET에서 Application Gateway와 API Management 통합 

##<a name="overview"> </a> 개요
 
hello 가상 네트워크 내 에서만 액세스할 수 있도록 내부 모드에서 가상 네트워크의 hello API 관리 서비스를 구성할 수 있습니다. Azure Application Gateway는 계층 7 부하 분산 장치를 제공하는 PAAS 서비스입니다. 역방향 프록시 서비스 역할을 하고 제품에 WAF(웹 응용 프로그램 방화벽)를 제공합니다.

Hello 다음 시나리오를 활성화 hello 응용 프로그램 게이트웨이 프런트엔드와 내부는 VNET에 사용자를 프로 비전 하는 API 관리를 결합 합니다.

* 사용 하 여 hello 동일한 API 관리 리소스 소비자가 내부 및 외부 소비자가 사용할 수 있도록 합니다.
* 단일 API Management 리소스를 사용하며 외부 소비자가 사용할 수 있는 API Management에서 정의된 API의 하위 집합을 갖습니다.
* Hello에서 턴키 방식으로 tooswitch 액세스 tooAPI 관리 제공 공용 인터넷 켜고 끕니다. 

##<a name="scenario"> </a> 시나리오
이 문서는 내부 및 외부 소비자에 대 한 toouse 단일 API 관리 서비스 하는 방법을 설명 하 고 두 온-프레미스에 대 한 단일 프런트엔드로 역할 및 Api 클라우드를 쉽게 됩니다. 살펴보면 어떻게 tooexpose hello 예에서는 녹색으로 강조 표시 된 Api의 하위 집합만을 통해 외부 응용 프로그램 게이트웨이에서 사용할 수 있는 hello PathBasedRouting 기능을 사용 하 여 합니다.

첫 번째 설치 예제 hello에에서 모든 Api 가상 네트워크 내 에서만 관리 됩니다. 내부 소비자(주황색으로 강조 표시됨)는 모든 내부 및 외부 API에 액세스할 수 있습니다. 트래픽은은 Express 경로 회로 통해 전달 되는 고성능 tooInternet 아웃 되지 전송 됩니다.

![url 경로](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <a name="before-you-begin"> </a> 시작하기 전에

1. Hello 웹 플랫폼 설치 관리자를 사용 하 여 hello 최신 버전의 hello Azure PowerShell cmdlet 설치 합니다. 다운로드 하 고 hello에서 hello 최신 버전을 설치할 수 **Windows PowerShell** hello 섹션 [다운로드 페이지](https://azure.microsoft.com/downloads/)합니다.
2. Virtual Network를 만들고 API Management 및 Application Gateway에 대한 별도 서브넷을 만듭니다. 
3. Toocreate hello 가상 네트워크에 대 한 사용자 지정 DNS 서버를 가져오려는 경우 그렇게 hello 배포를 시작 하기 전에. Hello 가상 네트워크에서에서 새 서브넷에서 만든 가상 컴퓨터에서 작동 하는 이중 확인 해결 하 고 모든 Azure 서비스 끝점에 액세스할 수 있습니다.

## <a name="what-is-required-toocreate-an-integration-between-api-management-and-application-gateway"></a>필요한 toocreate API 관리와 응용 프로그램 게이트웨이 간의 통합 이란?

* **백 엔드 서버 풀:** hello 내부 가상 IP 주소를 hello API 관리 서비스입니다.
* **백 엔드 서버 풀 설정:** 모든 풀에는 포트, 프로토콜 및 쿠키 기반의 선호도와 같은 설정이 있습니다. 이러한 설정은 hello 풀 내에서 적용 된 tooall 서버에 설명 합니다.
* **프런트 엔드 포트:** hello 응용 프로그램 게이트웨이에 열려 있는 hello 공용 포트입니다. 것에 도달 하는 트래픽이 리디렉션된 tooone hello의 백 엔드 서버를 가져옵니다.
* **수신기:** hello 수신기에는 프런트 엔드 포트 프로토콜 (Http 또는 Https의 경우, 이러한 값은 대/소문자 구분), 및 hello SSL 인증서 이름 (오프 로드 SSL 구성) 하는 경우.
* **규칙:** hello 규칙 수신기 tooa 백 엔드 서버 풀에 바인딩합니다.
* **사용자 정의 상태 검사:** 응용 프로그램 게이트웨이 기본적으로 사용 하 여 IP 주소 기반 프로브 toofigure BackendAddressPool 어떤 서버 hello에 활성화 됩니다. hello API 관리 서비스에만 toorequests hello 올바른 호스트 헤더를 포함 하는 응답, 따라서 hello 기본 프로브 실패 합니다. 사용자 지정 상태 프로브 필요한 toobe 정의 toohelp 응용 프로그램 게이트웨이 지 여부를 확인할 hello 서비스는 활성 상태 요청을 전달 해야 합니다.
* **사용자 지정 도메인 인증서:** hello에서 API 관리 tooaccess 인터넷 toocreate 해당 이름의 호스트 이름 toohello 응용 프로그램 게이트웨이 프런트 엔드 DNS의 CNAME 매핑이 필요 합니다. 이렇게 하면 hello hostname 헤더 및 보낸 인증서 tooApplication tooAPI 전달 되는 게이트웨이 관리 하나 임을 APIM 유효한 것으로 인식할 수 있습니다.

## <a name="overview-steps"> </a> API Management 및 Application Gateway 통합에 필요한 단계 

1. 리소스 관리자에 대한 리소스 그룹을 만듭니다.
2. 가상 네트워크, 서브넷 및 응용 프로그램 게이트웨이 hello에 대 한 공용 IP를 만듭니다. API Management에 대한 다른 서브넷을 만듭니다.
3. 위에서 만든 hello VNET 서브넷 내에 API 관리 서비스를 만들고 hello 내부 모드를 사용 하 여 확인 합니다.
4. API 관리 서비스 hello에 hello 사용자 지정 도메인 이름을 설정 합니다.
5. Application Gateway 구성 개체를 만듭니다.
6. Application Gateway 리소스를 만듭니다.
7. API 관리 프록시 호스트 이름 hello 응용 프로그램 게이트웨이 toohello의 hello 공용 DNS 이름에서 CNAME을 만들어야 합니다.

## <a name="create-a-resource-group-for-resource-manager"></a>리소스 관리자에 대한 리소스 그룹 만들기

Hello 최신 버전의 Azure PowerShell을 사용 하 고 있는지 확인 합니다. 자세한 내용은 [Resource Manager에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.

### <a name="step-1"></a>1단계

TooAzure 로그인

```powershell
Login-AzureRmAccount
```

자격 증명을 사용하여 인증합니다.<BR>

### <a name="step-2"></a>2단계

Hello 계정에 대 한 hello 구독을 확인 하 고 선택 합니다.

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a>3단계

리소스 그룹을 만듭니다. 기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛰세요.

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다. 이것은 해당 리소스 그룹의 리소스에 대 한 hello 기본 위치로 사용 됩니다. 모든 명령을 toocreate 응용 프로그램 게이트웨이 사용 하 여 hello 확인 동일한 리소스 그룹입니다.

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>가상 네트워크 및 서브넷을 hello 응용 프로그램 게이트웨이 만들기

다음 예제는 hello toocreate 사용 하 여 가상 네트워크에서 리소스 관리자를 hello 하는 방법을 보여 줍니다.

### <a name="step-1"></a>1단계

Hello 주소 범위 10.0.0.0/24 toohello 서브넷 변수 toobe 가상 네트워크를 만드는 동안 응용 프로그램 게이트웨이에 대 한 사용을 할당 합니다.

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a>2단계

Hello 주소 범위 10.0.1.0/24 toohello 서브넷 변수 toobe API 관리에 대 한 가상 네트워크를 만드는 동안 사용 되는 할당 합니다.

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a>3단계

명명 된 가상 네트워크 만들기 **appgwvnet** 리소스 그룹에 **apim-appGw-RG** 접두사 10.0.0.0/16 hello를 사용 하 여 hello 미국 서 부 지역에 대 한 서브넷 10.0.0.0/24 및 10.0.1.0/24 합니다.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a>4단계

Hello 다음 단계에 대 한 서브넷 변수 할당

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a>내부 모드로 구성된 VNET 내에서 API Management 서비스 만들기

hello 다음 예제에서는 어떻게 toocreate VNET에 있는 API 관리 서비스에 액세스 하도록 구성 내부만

### <a name="step-1"></a>1단계
위에서 만든 $apimsubnetdata hello 서브넷을 사용 하 여 API 관리 가상 네트워크 개체를 만듭니다.

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a>2단계
Hello 가상 네트워크 내에 API 관리 서비스를 만듭니다.

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
성공 하면 명령 위에 hello 너무 참조[DNS 구성이 필요 tooaccess 내부 VNET API 관리 서비스](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess 것입니다.

## <a name="set-up-a-custom-domain-name-in-api-management"></a>API Management에서 사용자 지정 도메인 이름 설정

### <a name="step-1"></a>1단계
Hello 도메인에 대 한 개인 키가 있는 hello 인증서를 업로드 합니다. 이 예에서는 `*.contoso.net`입니다. 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path too.pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a>2단계
Hello 인증서를 업로드 한 후 hello 프록시에 대 한 호스트 이름 구성 개체의 호스트 이름을 만들 `api.contoso.net`hello 예제 인증서 hello에 대 한 권한을 제공 하는 대로 `*.contoso.net` 도메인입니다. 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Hello 프런트 엔드 구성에 대 한 공용 IP 주소 만들기

공용 IP 리소스 만들기 **publicIP01** 리소스 그룹에 **apim-appGw-RG** hello 미국 서 부 지역에 대 한 합니다.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

IP 주소는 hello 서비스가 시작 될 때 toohello 응용 프로그램 게이트웨이 할당 됩니다.

## <a name="create-application-gateway-configuration"></a>응용 프로그램 게이트웨이 구성 만들기

Hello 응용 프로그램 게이트웨이 만들기 전에 모든 구성 항목 설정 해야 합니다. hello 다음 단계 hello 구성 항목을 만드는 응용 프로그램 게이트웨이 리소스에 대 한 필요 합니다.

### <a name="step-1"></a>1단계

**gatewayIP01**이라는 응용 프로그램 게이트웨이 IP 구성을 만듭니다. 응용 프로그램 게이트웨이 시작할 때 구성 hello 서브넷에서 IP 주소를 선택 하 고 hello 백 엔드 IP 풀의 네트워크 트래픽을 toohello IP 주소를 라우팅합니다. 인스턴스마다 하나의 IP 주소를 사용합니다.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a>2단계

Hello hello 공용 IP 끝점에 대 한 프런트 엔드 IP 포트를 구성 합니다. 이 포트는 최종 사용자에 연결 하는 hello 포트입니다.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a>3단계

공용 IP 끝점으로 hello 프런트 엔드 IP를 구성 합니다.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a>4단계

Hello 응용 프로그램 게이트웨이 사용 되는 toodecrypt hello 인증서를 구성 하 고 통과 hello 트래픽을 다시 암호화 합니다.

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a>5단계

응용 프로그램 게이트웨이 hello에 대 한 hello HTTP 수신기를 만듭니다. Hello 프런트 엔드 IP 구성, 포트 및 ssl 인증서 tooit 할당 합니다.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a>6단계

사용자 지정 프로브 toohello API 관리 서비스 만들기 `ContosoApi` 프록시 도메인 끝점입니다. hello 경로 `/status-0123456789abcdef` 모든 hello API 관리 서비스에서 호스팅되는 기본 상태 끝점이 있습니다. 설정 `api.contoso.net` 사용자 지정 프로브 hostname toosecure로 사용 하 여 SSL 인증서입니다.

> [!NOTE]
> 호스트 이름 hello `contosoapi.azure-api.net` 서비스 라는 hello 기본 프록시 호스트 이름이 구성 되어 `contosoapi` 공용 Azure에서 만든 합니다. 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a>7단계

Toobe hello SSL 사용 가능 백 엔드 풀 리소스에 사용 하는 hello 인증서를 업로드 합니다. 이 hello 위의 4 단계에서에서 제공 하는 동일한 인증서입니다.

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path too.cer file>
```

### <a name="step-8"></a>8단계

응용 프로그램 게이트웨이 hello에 대 한 HTTP 백 엔드 설정을 구성 합니다. 해당 설정이 취소된 후에 백 엔드 요청에 대한 제한 시간을 설정합니다. 이 값은 hello 프로브 시간 초과와에서 다릅니다.

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a>9단계

명명 된 백 엔드 IP 주소 풀을 구성 **apimbackend** hello 내부 가상 ip 주소 hello API 관리 서비스의 위에서 만든 합니다.

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a>10단계

더미(존재하지 않는) 백 엔드에 대한 설정을 만듭니다. 요청 tooAPI 경로 tooexpose 응용 프로그램 게이트웨이 통해 API 관리에서 원하지 않는 것이 백 엔드를 404 반환 됩니다.

Hello 더미 백 엔드에 대 한 HTTP 설정을 구성 합니다.

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

더미 백 엔드 구성 **dummyBackendPool**, tooa FQDN 주소가 가리키는 **dummybackend.com**합니다. 이 FQDN 주소가 hello 가상 네트워크에 존재 하지 않습니다.

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

응용 프로그램 게이트웨이 toohello 존재 하지 않는 백 엔드를 가리키는 기본적으로 사용 하는 해당 hello를 설정 하는 규칙을 만들 **dummybackend.com** hello 가상 네트워크에에서 있습니다.

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a>11단계

Hello 백 엔드 풀에 대 한 규칙 경로 URL을 구성 합니다. 이 통해 toohello 공개 노출 되기 위한 hello API 관리에서 Api의 일부에 선택 합니다. 예를 들어 `Echo API` (/echo/), `Calculator API` (/calc/) 등이 있으면 인터넷에서 `Echo API`에만 액세스할 수 있도록 합니다. 

hello 다음 예제에서는 hello "/ 에코 /" 경로 라우팅 트래픽 toohello 백 엔드 "apimProxyBackendPool"에 대 한 간단한 규칙

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

Hello 경로 tooenable 경로 맵 구성에는 또한 라는 기본 백 엔드 주소 풀을 구성 하는 hello 규칙, API 관리에서 원하는 규칙 hello 경로 일치 하지 않으면 **dummyBackendPool**합니다. 예를 들어 http://api.contoso.net/calc/ * 라인 너무**dummyBackendPool** 일치 하지 않는 트래픽에 대 한 hello 기본 풀으로 정의 된 대로 합니다.

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

단계 위에 hello만 hello 경로 대 한 요청을 사용 하면 "/ echo" hello 응용 프로그램 게이트웨이 통해 허용 됩니다. API 관리에서 구성 된 Api 요청 tooother hello 인터넷에서에서 액세스할 때 응용 프로그램 게이트웨이에서 404 오류를 throw 합니다. 

### <a name="step-12"></a>12단계

Hello 응용 프로그램 게이트웨이 toouse URL 경로 기반 라우팅에 대 한 규칙 설정을 만듭니다.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a>13단계

Hello 인스턴스 수 및 크기 hello 응용 프로그램 게이트웨이를 구성 합니다. 여기서 사용 하 여 hello [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) hello API 관리 리소스의 보안을 강화 합니다.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a>14단계

WAF toobe "방지" 모드에서 구성 합니다.
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a>Application Gateway 만들기

Hello 이전 단계에서에서 hello 구성 개체를 모두 포함 된 응용 프로그램 게이트웨이 만들기

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-hello-api-management-proxy-hostname-toohello-public-dns-name-of-hello-application-gateway-resource"></a>CNAME hello API 관리 프록시 호스트 이름 toohello의 공용 DNS 이름 hello 응용 프로그램 게이트웨이 리소스

Hello 게이트웨이가 생성 된 hello 다음 단계는 통신을 위해 tooconfigure hello 프런트 엔드입니다. 공용 IP를 사용할 때 응용 프로그램 게이트웨이 하지 않을 수 있는 쉬운 toouse 동적으로 할당 된 DNS 이름이 필요 합니다. 

hello 응용 프로그램 게이트웨이 DNS 이름 이어야 합니다 hello APIM 프록시 호스트 이름을 가리키는 CNAME 레코드를 사용 하는 toocreate (예: `api.contoso.net` 위의 hello 예에) toothis DNS 이름입니다. tooconfigure hello 프런트 엔드 IP CNAME 레코드의 응용 프로그램 게이트웨이 hello hello 세부 정보 및 hello PublicIPAddress 요소를 사용 하 여 연결 된 IP/DNS 이름을 검색 합니다. hello VIP 수 변하기 때문에 게이트웨이 다시 시작 hello를 사용 하 여 A 레코드의 권장 되지 않습니다.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<a name="summary"> </a> 요약
VNET에 구성 된 azure API 관리 호스트 된 온-프레미스가 든 상관 없이 또는 hello 클라우드의 모든 구성 된 Api에 대 한 단일 게이트웨이 인터페이스를 제공 합니다. API 관리 응용 프로그램 게이트웨이 통합 프런트 엔드 tooyour API 관리 인스턴스로 웹 응용 프로그램 방화벽 제공 수 있을 뿐만 아니라 특정 Api toobe hello 인터넷에서 액세스할 수 있는지를 선택적으로 사용의 hello 유연성을 제공 합니다.

##<a name="next-steps"> </a> 다음 단계
* Azure Application Gateway에 대한 자세한 정보
  * [응용 프로그램 게이트웨이 개요](../application-gateway/application-gateway-introduction.md)
  * [Application Gateway 웹 응용 프로그램 방화벽](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [경로 기반 라우팅을 사용하는 Application Gateway](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* API Management 및 VNET에 대한 자세한 정보
  * [Hello VNET 내 에서만 사용할 수 있는 API 관리를 사용 하 여](api-management-using-with-internal-vnet.md)
  * [VNET에서 API Management 사용](api-management-using-with-vnet.md)
