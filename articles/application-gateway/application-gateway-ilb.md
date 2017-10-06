---
title: "내부 부하 분산 장치와 Azure 응용 프로그램 게이트웨이 aaaUsing | Microsoft Docs"
description: "이 페이지에서는 내부 부하 분산 된 끝점이 있는 Azure 응용 프로그램 게이트웨이 tooconfigure 지침 제공"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 7403d28e-909f-46a2-b282-43a8e942f53c
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 272ef84a02f92a8521c35aad6f1d9f9bf1675718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a>내부 부하 분산 장치 (ILB)를 사용하여 응용 프로그램 게이트웨이 만들기

> [!div class="op_single_selector"]
> * [Azure 클래식 PowerShell](application-gateway-ilb.md)
> * [Azure Resource Manager PowerShell](application-gateway-ilb-arm.md)

가상 IP 인터넷 또는 내부 끝점을 노출 되지 toohello 응용 프로그램 게이트웨이 구성할 수 있습니다 인터넷, 부하 분산 장치 ILB (내부) 끝점 라고도 합니다. ilb 구성 hello 게이트웨이 toointernet 노출 되지 않는 내부 기간 업무 응용 프로그램에 유용합니다. 또한 서비스/계층에서 보안 경계 노출 되지 toointernet 하지만 여전히 라운드 로빈 부하 분산, 세션 인력 또는 SSL 종료를 필요한 다중 계층 응용 프로그램 내에서도 유용 합니다. 이 문서에서는 hello 단계 tooconfigure ilb는 응용 프로그램 게이트웨이 안내합니다.

## <a name="before-you-begin"></a>시작하기 전에

1. 최신 버전의 hello 웹 플랫폼 설치 관리자를 사용 하 여 hello Azure PowerShell cmdlet 설치 합니다. 다운로드 하 고 hello에서 hello 최신 버전을 설치할 수 **Windows PowerShell** hello 섹션 [다운로드 페이지](https://azure.microsoft.com/downloads/)합니다.
2. 유효한 서브넷과 작업 가상 네트워크가 있는지 확인합니다.
3. Hello 가상 네트워크 또는 할당 된 공용 IP/VIP와 백 엔드 서버 있는지 확인 합니다.

응용 프로그램 게이트웨이 toocreate hello 순서 대로 단계를 수행 하는 hello를 수행 합니다. 

1. [응용 프로그램 게이트웨이 만들기](#create-a-new-application-gateway)
2. [Hello 게이트웨이 구성](#configure-the-gateway)
3. [Hello 게이트웨이 구성 설정](#set-the-gateway-configuration)
4. [Hello 게이트웨이 시작](#start-the-gateway)
5. [Hello 게이트웨이 확인](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a>응용 프로그램 게이트웨이를 만듭니다.

**toocreate hello 게이트웨이**, hello를 사용 하 여 `New-AzureApplicationGateway` cmdlet, 사용자의 정보로 hello 값을 대체 합니다. Note hello 게이트웨이에 대 한 청구가 시점에서 시작 되지 않습니다. 청구는 hello 게이트웨이 성공적으로 시작 하는 경우 이후 단계에서 시작 합니다.

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

```
VERBOSE: 4:31:35 PM - Begin Operation: New-AzureApplicationGateway 
VERBOSE: 4:32:37 PM - Completed Operation: New-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   55ef0460-825d-2981-ad20-b9a8af41b399
```

**toovalidate** hello 게이트웨이 만든, hello를 사용할 수 있습니다 `Get-AzureApplicationGateway` cmdlet. 

Hello 샘플에서 *설명*, *InstanceCount*, 및 *GatewaySize* 는 선택적 매개 변수입니다. 기본값에 대 한 hello *InstanceCount* 최대 값이 10 인 2입니다. 에 대 한 기본값을 hello *GatewaySize* 보통입니다. 크고 작은 다른 사용 가능한 값이 됩니다. *Vip* 및 *DnsName* hello 게이트웨이가 아직 시작 되지 않았습니다. 때문에 출력이 빈 값으로 표시 됩니다. Hello 게이트웨이 hello 실행 중 상태에에서 있으면 만들어집니다. 

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 4:39:39 PM - Begin Operation:
Get-AzureApplicationGateway VERBOSE: 4:39:40 PM - Completed 
Operation: Get-AzureApplicationGateway
Name: AppGwTest    
Description: 
VnetName: testvnet1 
Subnets: {Subnet-1} 
InstanceCount: 2 
GatewaySize: Medium 
State: Stopped 
VirtualIPs: 
DnsName:
```

## <a name="configure-hello-gateway"></a>Hello 게이트웨이 구성
응용 프로그램 게이트웨이는 여러 값으로 구성됩니다. hello 값이 연결 될 수 함께 tooconstruct hello 구성 합니다.

hello 값은 같습니다.

* **백 엔드 서버 풀:** hello hello 백 엔드 서버의 IP 주소 목록입니다. 나열 된 IP 주소를 hello toohello VNet 서브넷에 속해야 하거나 또는 공용 IP/VIP 이어야 합니다. 
* **백 엔드 서버 풀 설정:** 모든 풀에는 포트, 프로토콜 및 쿠키 기반의 선호도와 같은 설정이 있습니다. 이러한 설정은 동률된 tooa 풀 및 hello 풀 내에서 적용 된 tooall 서버입니다.
* **프런트 엔드 포트:** 이 포트는 hello 공용 포트 hello 응용 프로그램 게이트웨이에서 열립니다. 트래픽이이 포트에 도달 하 고 hello 백 엔드 서버의 리디렉션된 tooone 가져옵니다.
* **수신기:** hello 수신기에 프런트 엔드 포트, 프로토콜 (Http 또는 Https의 경우,이 대/소문자 구분), 및 hello SSL 인증서 이름 (오프 로드 SSL 구성) 하는 경우. 
* **규칙:** hello 규칙 hello 수신기 및 hello 백 엔드 서버 풀 바인딩하고 정의 백 엔드 서버 풀 hello 트래픽을 특정 수신기 페이로드만 directed toowhen 이어야 합니다. 현재만 hello *기본* 규칙 지원 됩니다. hello *기본* 규칙은 라운드 로빈 부하 분산 합니다.

구성 개체를 만들거나, 구성 XML 파일을 사용하여 구성을 생성할 수 있습니다. 아래 샘플 구성 XML 파일을 사용 하 여 hello를 사용 하 여 구성을 tooconstruct 합니다.

참고 hello 다음.

* hello *frontendipconfigurations가* 요소는 ILB를 사용 하 여 응용 프로그램 게이트웨이 구성 하는 것에 대 한 관련 된 hello ILB 세부 정보를 설명 합니다. 
* hello 프런트 엔드 IP *형식* too'Private 설정할지 '
* hello *StaticIPAddress* 원하는 toohello는 hello 게이트웨이 트래픽을 수신 하는 내부 IP 설정 해야 합니다. 해당 hello 참고 *StaticIPAddress* 요소는 선택 사항입니다. 그렇지 않으면 집합에 배포 된 hello 서브넷에서 사용할 수 있는 내부 IP 선택 됩니다. 
* 값의 hello hello *이름* 요소에 지정 된 *FrontendIPConfiguration* hello HTTPListener의에서 사용 해야 *FrontendIP* toorefer toohello 요소 FrontendIPConfiguration 합니다.
  
  **구성 XML 샘플**
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations>
        <FrontendIPConfiguration>
            <Name>fip1</Name> 
            <Type>Private</Type> 
            <StaticIPAddress>10.0.0.10</StaticIPAddress> 
        </FrontendIPConfiguration>
    </FrontendIPConfigurations>
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendIP>fip1</FrontendIP>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```


## <a name="set-hello-gateway-configuration"></a>Hello 게이트웨이 구성 설정
다음으로 hello 응용 프로그램 게이트웨이 설정 합니다. Hello를 사용할 수 있습니다 `Set-AzureApplicationGatewayConfig` cmdlet는 구성 개체 또는 구성 XML 파일입니다. 

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

```
VERBOSE: 7:54:59 PM - Begin Operation: Set-AzureApplicationGatewayConfig 
VERBOSE: 7:55:32 PM - Completed Operation: Set-AzureApplicationGatewayConfig
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   9b995a09-66fe-2944-8b67-9bb04fcccb9d
```

## <a name="start-hello-gateway"></a>Hello 게이트웨이 시작

Hello를 사용 하 여 hello 게이트웨이 구성한 후 `Start-AzureApplicationGateway` cmdlet toostart hello 게이트웨이 합니다. 응용 프로그램 게이트웨이 대 한 청구 hello 게이트웨이 성공적으로 시작 된 후 시작 합니다. 

> [!NOTE]
> hello `Start-AzureApplicationGateway` cmdlet toocomplete too15 20 분이 걸릴 수도 있습니다. 
> 
> 

```powershell
Start-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 7:59:16 PM - Begin Operation: Start-AzureApplicationGateway 
VERBOSE: 8:05:52 PM - Completed Operation: Start-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   fc592db8-4c58-2c8e-9a1d-1c97880f0b9b
```

## <a name="verify-hello-gateway-status"></a>Hello 게이트웨이 상태를 확인 합니다.

사용 하 여 hello `Get-AzureApplicationGateway` 게이트웨이의 cmdlet toocheck hello 상태입니다. 경우 `Start-AzureApplicationGateway` hello 이전 단계에서 성공한 hello 상태 여야 합니다 *실행*, Vip hello 및 DnsName 유효한 항목 있어야 합니다. 이 hello 출력 다음 샘플에서는 hello 첫 번째 줄에 hello cmdlet을 보여 줍니다. 이 샘플에서는 hello 게이트웨이가 실행 되 고 준비 tootake 트래픽입니다. 

> [!NOTE]
> hello 응용 프로그램 게이트웨이 구성 된 hello에서 tooaccept 트래픽을이 예에서 10.0.0.10의 ILB 끝점을 구성 합니다.

```powershell
Get-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway 
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   : 
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {10.0.0.10}
DnsName       : appgw-b2a11563-2b3a-4172-a4aa-226ee4c23eed.cloudapp.net
```

## <a name="next-steps"></a>다음 단계
보다 자세한 내용을 원한다면 일반적 부하 분산 옵션을 참조:

* [Azure 부하 분산 장치](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

