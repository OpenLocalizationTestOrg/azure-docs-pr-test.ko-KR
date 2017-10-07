---
title: "Azure 응용 프로그램 게이트웨이에 있는 내부 부하 분산 장치-PowerShell aaaUsing | Microsoft Docs"
description: "이 페이지에서는 toocreate, 구성, 시작 및 Azure 리소스 관리자에 대 한 내부 부하 분산 장치 (ILB)와 Azure 응용 프로그램 게이트웨이 삭제 하는 지침을 제공 합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 75cfd5a2-e378-4365-99ee-a2b2abda2e0d
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: dd0d7e954b1fa219ae6ebe42cb4b479dbcf08653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a>Azure 리소스 관리자를 사용하여 ILB(내부 부하 분산 장치)에서 응용 프로그램 게이트웨이 만들기

> [!div class="op_single_selector"]
> * [Azure 클래식 PowerShell](application-gateway-ilb.md)
> * [Azure Resource Manager PowerShell](application-gateway-ilb-arm.md)

Azure 응용 프로그램 게이트웨이 인터넷 연결 VIP 또는 내부 끝점 노출된 toohello 인터넷으로 알려진 내부 부하 분산 장치 (ILB) 끝점을 구성할 수 있습니다. 구성 hello 게이트웨이 ilb 노출된 toohello 인터넷 되지 않은 내부 기간 업무 응용 프로그램에 유용 합니다. 서비스에도 유용 하 고 다중 계층 응용 프로그램 내에서 노출 된 toohello 인터넷 하지 않은 보안 경계에 앉아 하지만 여전히 필요 하는 라운드 로빈 계층 로드 배포, 세션 인력 또는 Secure Sockets Layer (SSL) 종료 합니다.

이 문서에서는 hello 단계 tooconfigure ilb는 응용 프로그램 게이트웨이 안내합니다.

## <a name="before-you-begin"></a>시작하기 전에

1. Hello 웹 플랫폼 설치 관리자를 사용 하 여 hello 최신 버전의 hello Azure PowerShell cmdlet 설치 합니다. 다운로드 하 고 hello에서 hello 최신 버전을 설치할 수 **Windows PowerShell** hello 섹션 [다운로드 페이지](https://azure.microsoft.com/downloads/)합니다.
2. 응용 프로그램 게이트웨이에 대한 가상 네트워크 및 서브넷을 만듭니다. 가상 컴퓨터 또는 클라우드 배포 없습니다 hello 서브넷 사용 하 고 있는지 확인 합니다. 응용 프로그램 게이트웨이는 가상 네트워크 서브넷에서 단독이어야 합니다.
3. toouse hello 응용 프로그램 게이트웨이 구성 하는 hello 서버에 존재 해야 하거나 또는 hello 가상 네트워크에서 공용 IP/VIP와 만든 끝점을 할당 합니다.

## <a name="what-is-required-toocreate-an-application-gateway"></a>필요한 toocreate 응용 프로그램 게이트웨이 란?

* **백 엔드 서버 풀:** hello hello 백 엔드 서버의 IP 주소 목록입니다. hello 나열 된 IP 주소 중 하나에 속해야 합니다 toohello 가상 네트워크 하지만 응용 프로그램 게이트웨이 hello에 대 한 다른 서브넷 또는 공용 IP/VIP 이어야 합니다.
* **백 엔드 서버 풀 설정:** 모든 풀에는 포트, 프로토콜 및 쿠키 기반의 선호도와 같은 설정이 있습니다. 이러한 설정은 동률된 tooa 풀 및 hello 풀 내에서 적용 된 tooall 서버입니다.
* **프런트 엔드 포트:** 이 포트는 hello 응용 프로그램 게이트웨이에 열려 있는 hello 공용 포트입니다. 트래픽이이 포트에 도달 하 고 가져옵니다 hello 백 엔드 서버의 tooone 리디렉션됩니다.
* **수신기:** hello 수신기에는 프런트 엔드 포트 프로토콜 (Http 또는 Https의 경우,이 대/소문자 구분), 및 hello SSL 인증서 이름 (오프 로드 SSL 구성) 하는 경우.
* **규칙:** hello 규칙 hello 수신기 및 hello 백 엔드 서버 풀 바인딩하고 정의 백 엔드 서버 풀 hello 트래픽을 특정 수신기 페이로드만 directed toowhen 이어야 합니다. 현재만 hello *기본* 규칙 지원 됩니다. hello *기본* 규칙은 라운드 로빈 부하 분산 합니다.

## <a name="create-an-application-gateway"></a>응용 프로그램 게이트웨이 만들기

hello Azure 클래식 및 Azure 리소스 관리자를 사용 하는 차이점은 hello 응용 프로그램 게이트웨이 및 toobe 구성 해야 하는 hello 항목을 만들 있는 hello 순서입니다.
리소스 관리자와 응용 프로그램 게이트웨이 구성 하는 모든 항목 개별적으로 구성 되 고 다음 조립 toocreate hello 응용 프로그램 게이트웨이 리소스입니다.

필요한 toocreate 응용 프로그램 게이트웨이 hello 단계는 다음과 같습니다.

1. 리소스 관리자에 대한 리소스 그룹 만들기
2. 가상 네트워크 및 서브넷을 hello 응용 프로그램 게이트웨이 만들기
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

새 리소스 그룹을 만듭니다. 기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛰세요.

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다. 이것은 해당 리소스 그룹의 리소스에 대 한 hello 기본 위치로 사용 됩니다. 응용 프로그램 게이트웨이 사용 하 여 모든 명령을 toocreate hello 동일 하 고 있는지 확인 리소스 그룹입니다.

앞 예제는 hello, "appgw rg" 및 위치 "West US" 라는 리소스 그룹을 만들었습니다.

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>가상 네트워크 및 서브넷을 hello 응용 프로그램 게이트웨이 만들기

hello 방법을 예제와 다음 toocreate 리소스 관리자를 사용 하 여 가상 네트워크:

### <a name="step-1"></a>1단계

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

이 단계는 hello 주소 범위 10.0.0.0/24 tooa 서브넷 사용 되는 변수 toobe toocreate 가상 네트워크를 할당합니다.

### <a name="step-2"></a>2단계

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

이 단계에서 리소스 그룹 "appgw-rg" hello 미국 서 부 지역 서브넷 10.0.0.0/24 hello 접두사 10.0.0.0/16 사용에 대 한 "appgwvnet" 이라는 가상 네트워크를 만듭니다.

### <a name="step-3"></a>3단계

```powershell
$subnet = $vnet.subnets[0]
```

이 단계는 hello 다음 단계에 대 한 hello 서브넷 개체 toovariable $subnet을 할당합니다.

## <a name="create-an-application-gateway-configuration-object"></a>응용 프로그램 게이트웨이 구성 개체 만들기

### <a name="step-1"></a>1단계:

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

이 단계에서는 "gatewayIP01"이라는 응용 프로그램 게이트웨이 IP 구성을 만듭니다. 응용 프로그램 게이트웨이 시작할 때 구성 hello 서브넷에서 IP 주소를 선택 하 고 hello 백 엔드 IP 풀의 네트워크 트래픽을 toohello IP 주소를 라우팅합니다. 인스턴스마다 하나의 IP 주소를 사용합니다.

### <a name="step-2"></a>2단계

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

이 단계에서는 이라는 hello 백 엔드 IP 주소 풀을 구성 "10.1.1.8, 10.1.1.9, 10.1.1.10" "pool01" ip 주소입니다. Hello 프런트 엔드 IP 끝점에서 제공 되는 hello 네트워크 트래픽을 수신 하는 hello IP 주소 모두입니다. 사용자 고유의 응용 프로그램의 IP 주소 끝점 IP 주소 tooadd 앞 hello를 대체 합니다.

### <a name="step-3"></a>3단계

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

이 단계에서는 hello 백 엔드 풀의 응용 프로그램 게이트웨이 설정 "poolsetting01" hello 부하 분산 된 네트워크 트래픽을 구성 합니다.

### <a name="step-4"></a>4단계

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

이 단계에서는 ILB hello에 대 한 "frontendport01" 라는 hello 프런트 엔드 IP 포트를 구성 합니다.

### <a name="step-5"></a>5단계

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

이 단계는 hello 프런트 엔드 IP 구성 "fipconfig01" 라는 만들고 hello 현재 가상 네트워크 서브넷의 개인 IP와 연결 합니다.

### <a name="step-6"></a>6단계

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

이 단계 "listener01" 라는 hello 수신기를 만들고 hello 프런트 엔드 포트 toohello 프런트 엔드 IP 구성에 연결 합니다.

### <a name="step-7"></a>7단계

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

이 단계는 hello 부하 분산 장치 라우팅 규칙 "rule01" hello 부하 분산 장치 동작을 구성 하는 호출을 만듭니다.

### <a name="step-8"></a>8단계

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

이 단계는 hello 인스턴스 크기의 hello 응용 프로그램 게이트웨이 구성합니다.

> [!NOTE]
> 기본값에 대 한 hello *InstanceCount* 최대 값이 10 인 2입니다. 에 대 한 기본값을 hello *GatewaySize* 보통입니다. Standard_Small, Standard_Medium 및 Standard_Large 간에 선택할 수 있습니다.

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a>New-AzureApplicationGateway를 사용하여 응용 프로그램 게이트웨이 만들기

Hello 이전 단계에서에서 구성 항목을 모두 사용 응용 프로그램 게이트웨이 만듭니다. 이 예제에서는 hello 응용 프로그램 게이트웨이 "appgwtest" 라고 합니다.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

이 단계는 hello 이전 단계에서에서 모든 구성 항목과 응용 프로그램 게이트웨이 만듭니다. Hello 예제 hello 응용 프로그램 게이트웨이 "appgwtest" 라고 합니다.

## <a name="delete-an-application-gateway"></a>응용 프로그램 게이트웨이 삭제

응용 프로그램 게이트웨이 toodelete toodo hello 순서에 단계를 수행 해야 합니다.

1. 사용 하 여 hello `Stop-AzureRmApplicationGateway` cmdlet toostop hello 게이트웨이 합니다.
2. 사용 하 여 hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello 게이트웨이 합니다.
3. Hello를 사용 하 여 해당 hello 게이트웨이에 제거 되었는지 확인 `Get-AzureApplicationGateway` cmdlet.

### <a name="step-1"></a>1단계

Hello 응용 프로그램 게이트웨이 개체를 가져오고 tooa "$getgw" 변수를 연결 합니다.

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a>2단계

사용 하 여 `Stop-AzureRmApplicationGateway` toostop hello 응용 프로그램 게이트웨이 합니다. 이 샘플은 hello `Stop-AzureRmApplicationGateway` hello 첫 번째 줄에는 cmdlet hello 출력이 차례로 표시 합니다.

```powershell
Stop-AzureRmApplicationGateway -ApplicationGateway $getgw  
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

중지 된 상태에 hello 응용 프로그램 게이트웨이 사용 하 여 hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello 서비스입니다.

```powershell
Remove-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Force
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

> [!NOTE]
> hello **-강제로** 스위치 사용된 toosuppress hello 제거 확인 메시지를 수 있습니다.

서비스 hello tooverify 제거 된 hello를 사용할 수 있습니다, `Get-AzureRmApplicationGateway` cmdlet. 이 단계는 필요 하지 않습니다.

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
```

## <a name="next-steps"></a>다음 단계

SSL 오프 로드 tooconfigure 참조 [SSL 오프 로드에 대 한 응용 프로그램 게이트웨이 구성](application-gateway-ssl.md)합니다.

ilb는 응용 프로그램 게이트웨이 toouse tooconfigure 참조 [내부 부하 분산 장치 (ILB) 응용 프로그램 게이트웨이 만들](application-gateway-ilb.md)합니다.

보다 자세한 내용을 원한다면 일반적 부하 분산 옵션을 참조:

* [Azure 부하 분산 장치](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

