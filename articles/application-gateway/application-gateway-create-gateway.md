---
title: "aaaCreate, 시작 또는 응용 프로그램 게이트웨이 삭제 합니다. | Microsoft Docs"
description: "이 페이지에서는 toocreate, 구성, 시작 및 Azure 응용 프로그램 게이트웨이 삭제 하는 지침을 제공 합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 577054ca-8368-4fbf-8d53-a813f29dc3bc
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3efef5b49880c9efdafad8b88d4bce5b749b82af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a>PowerShell을 사용하여 Application Gateway 만들기, 시작 또는 삭제 

> [!div class="op_single_selector"]
> * [Azure 포털](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure 클래식 PowerShell](application-gateway-create-gateway.md)
> * [Azure Resource Manager 템플릿](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI](application-gateway-create-gateway-cli.md)

Azure Application Gateway는 계층 7 부하 분산 장치입니다. 장애 조치의 경우 서로 다른 서버 간에 HTTP 요청 성능 라우팅 hello 클라우드 또는 온-프레미스에 있는지 여부를 제공 합니다. 응용 프로그램 게이트웨이는 HTTP 부하 분산, 쿠키 기반 세션 선호도, SSL(Secure Sockets Layer) 오프로드, 사용자 지정 상태 프로브, 다중 사이트 지원 및 기타를 포함하여 많은 ADC(Application Delivery Controller)를 제공합니다. 지원 되는 기능의 전체 목록은 toofind 방문 [응용 프로그램 게이트웨이 개요](application-gateway-introduction.md)

이 문서 단계별로 hello 단계 toocreate, 구성, 시작 및 응용 프로그램 게이트웨이 삭제 합니다.

## <a name="before-you-begin"></a>시작하기 전에

1. Hello 웹 플랫폼 설치 관리자를 사용 하 여 hello 최신 버전의 hello Azure PowerShell cmdlet 설치 합니다. 다운로드 하 고 hello에서 hello 최신 버전을 설치할 수 **Windows PowerShell** hello 섹션 [다운로드 페이지](https://azure.microsoft.com/downloads/)합니다.
2. 기존 가상 네트워크를 사용 하도록 설정한 경우 기존 빈 서브넷을 선택 하거나 hello 응용 프로그램 게이트웨이에서 사용 하기 위해서만 하려면 기존 가상 네트워크에서 새 서브넷을 만듭니다. Hello 응용 프로그램 게이트웨이 tooa 다른 가상 네트워크를 배포할 수 없습니다 hello 리소스 보다 하려는 hello 응용 프로그램 게이트웨이 뒤 toodeploy vnet 피어 링을 사용 합니다. toolearn 더 방문 [Vnet 피어 링](../virtual-network/virtual-network-peering-overview.md)
3. 유효한 서브넷과 작업 가상 네트워크가 있는지 확인합니다. 가상 컴퓨터 또는 클라우드 배포 없습니다 hello 서브넷 사용 하 고 있는지 확인 합니다. hello 응용 프로그램 게이트웨이 자체 가상 네트워크 서브넷에 있어야 합니다.
4. toouse hello 응용 프로그램 게이트웨이 구성 하는 hello 서버에 존재 해야 하거나 또는 hello 가상 네트워크에서 공용 IP/VIP와 만든 끝점을 할당 합니다.

## <a name="what-is-required-toocreate-an-application-gateway"></a>필요한 toocreate 응용 프로그램 게이트웨이 란?

Hello를 사용 하는 경우 `New-AzureApplicationGateway` 명령 toocreate hello 응용 프로그램 게이트웨이 구성 없이 시점에서 설정 되 고 hello 새로 만든 리소스 구성 된 XML 또는 구성 개체를 사용 하 여 합니다.

hello 값은 같습니다.

* **백 엔드 서버 풀:** hello hello 백 엔드 서버의 IP 주소 목록입니다. 나열 된 hello IP 주소 하거나 toohello 가상 네트워크 서브넷에 속해야 하거나 공용 IP/VIP가 있어야 합니다.
* **백 엔드 서버 풀 설정:** 모든 풀에는 포트, 프로토콜 및 쿠키 기반의 선호도와 같은 설정이 있습니다. 이러한 설정은 동률된 tooa 풀 및 hello 풀 내에서 적용 된 tooall 서버입니다.
* **프런트 엔드 포트:** 이 포트는 hello 응용 프로그램 게이트웨이에 열려 있는 hello 공용 포트입니다. 트래픽이이 포트에 도달 하 고 가져옵니다 hello 백 엔드 서버의 tooone 리디렉션됩니다.
* **수신기:** hello 수신기에는 프런트 엔드 포트 프로토콜 (Http 또는 Https의 경우, 이러한 값은 대/소문자 구분), 및 hello SSL 인증서 이름 (오프 로드 SSL 구성) 하는 경우.
* **규칙:** hello 규칙 hello 수신기 및 hello 백 엔드 서버 풀 바인딩하고 정의 백 엔드 서버 풀 hello 트래픽을 특정 수신기 페이로드만 directed toowhen 이어야 합니다.

## <a name="create-an-application-gateway"></a>응용 프로그램 게이트웨이 만들기

응용 프로그램 게이트웨이 toocreate:

1. 응용 프로그램 게이트웨이 리소스를 만듭니다.
2. 구성 XML 파일 또는 구성 개체를 만듭니다.
3. 새로 만든 응용 프로그램 게이트웨이 리소스 hello 구성 toohello를 커밋하십시오.

> [!NOTE]
> 응용 프로그램 게이트웨이에 대 한 사용자 지정 프로브 tooconfigure 해야 할 경우 참조 [PowerShell을 사용 하 여 사용자 지정 프로브 사용 하 여 응용 프로그램 게이트웨이 만들](application-gateway-create-probe-classic-ps.md)합니다. 자세한 내용은 [사용자 지정 프로브 및 상태 모니터링](application-gateway-probe-overview.md) 을 확인합니다.

![예제 시나리오][scenario]

### <a name="create-an-application-gateway-resource"></a>응용 프로그램 게이트웨이 리소스 만들기

toocreate hello 게이트웨이 사용 하 여 hello `New-AzureApplicationGateway` cmdlet, 사용자의 정보로 hello 값을 대체 합니다. 게이트웨이 hello에 대 한 청구가 시점에서 시작 되지 않습니다. 청구는 hello 게이트웨이 성공적으로 시작 하는 경우 이후 단계에서 시작 합니다.

hello 다음 만드는 예제 응용 프로그램 게이트웨이 "testvnet1"과 "서브넷-1" 이라는 서브넷 이라는 가상 네트워크를 사용 하 여:

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

*Description*, *InstanceCount* 및 *GatewaySize*는 선택적 매개 변수입니다.

게이트웨이 hello toovalidate 만들어진 hello를 사용할 수 있습니다, `Get-AzureApplicationGateway` cmdlet.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Stopped
VirtualIPs    : {}
DnsName       :
```

> [!NOTE]
> 기본값에 대 한 hello *InstanceCount* 최대 값이 10 인 2입니다. 에 대 한 기본값을 hello *GatewaySize* 보통입니다. 작게, 보통 및 크게를 선택할 수 있습니다.

*Virtualip* 및 *DnsName* hello 게이트웨이가 아직 시작 되지 않았습니다. 때문에 출력이 빈 값으로 표시 됩니다. Hello 게이트웨이 hello 실행 중 상태에에서 있으면 만들어집니다.

## <a name="configure-hello-application-gateway"></a>Hello 응용 프로그램 게이트웨이 구성 합니다.

XML 또는 구성 개체를 사용 하 여 hello 응용 프로그램 게이트웨이 구성할 수 있습니다.

### <a name="configure-hello-application-gateway-by-using-xml"></a>XML을 사용 하 여 hello 응용 프로그램 게이트웨이 구성 합니다.

다음 예제는 hello, 모든 응용 프로그램 게이트웨이 설정 XML 파일 tooconfigure를 사용 하 고 응용 프로그램 게이트웨이 리소스 toohello 커밋하기 합니다.  

#### <a name="step-1"></a>1단계

다음 텍스트 tooNotepad hello를 복사 합니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>(name-of-your-frontend-port)</Name>
            <Port>(port number)</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>(name-of-your-backend-pool)</Name>
            <IPAddresses>
                <IPAddress>(your-IP-address-for-backend-pool)</IPAddress>
                <IPAddress>(your-second-IP-address-for-backend-pool)</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>(backend-setting-name-to-configure-rule)</Name>
            <Port>80</Port>
            <Protocol>[Http|Https]</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>(name-of-the-listener)</Name>
            <FrontendPort>(name-of-your-frontend-port)</FrontendPort>
            <Protocol>[Http|Https]</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>(name-of-load-balancing-rule)</Name>
            <Type>basic</Type>
            <BackendHttpSettings>(backend-setting-name-to-configure-rule)</BackendHttpSettings>
            <Listener>(name-of-the-listener)</Listener>
            <BackendAddressPool>(name-of-your-backend-pool)</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

Hello hello 구성 항목에 대 한 hello 괄호 사이 값을 편집 합니다. Hello 파일 확장명이.xml으로 저장 합니다.

> [!IMPORTANT]
> Http 또는 Https hello 프로토콜 항목은 대/소문자 구분입니다.

다음 예제는 hello toouse 구성 파일 tooset hello 응용 프로그램 게이트웨이를 보여 줍니다. hello 예제에서는 로드 된 공용 포트 80의 HTTP 트래픽을 분산 시키고 후 tooback 끝 포트 80에서 두 개의 IP 주소 간의 네트워크 트래픽을 보냅니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
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

#### <a name="step-2"></a>2단계

다음으로 hello 응용 프로그램 게이트웨이 설정 합니다. 사용 하 여 hello `Set-AzureApplicationGatewayConfig` 구성 XML 파일을 사용 하 여 cmdlet.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-hello-application-gateway-by-using-a-configuration-object"></a>구성 개체를 사용 하 여 hello 응용 프로그램 게이트웨이 구성

다음 예제는 hello tooconfigure 구성 개체를 사용 하 여 응용 프로그램 게이트웨이 hello 하는 방법을 보여 줍니다. 모든 구성 항목을 개별적으로 구성 되며 다음 추가 해야 tooan 응용 프로그램 게이트웨이 구성 개체입니다. Hello를 사용 하면 hello 구성 개체를 만든 후 `Set-AzureApplicationGateway` 명령 toocommit hello 구성 toohello 이전에 응용 프로그램 게이트웨이 리소스를 생성 합니다.

> [!NOTE]
> 값 tooeach 구성 개체를 할당 하기 전에 필요한 toodeclare PowerShell가 어떤 종류의 개체 저장을 위해 사용 합니다. hello 첫 번째 toocreate hello 개별 품목 대상을 정의 `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` 사용 됩니다.

#### <a name="step-1"></a>1단계

모든 개별 구성 항목을 만듭니다.

다음 예제는 hello와 같이 hello 프런트 엔드 IP를 만듭니다.

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

다음 예제는 hello와 같이 hello 프런트 엔드 포트를 만듭니다.

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

Hello 백 엔드 서버 풀을 만듭니다.

Hello 다음 예제와 같이 toohello 백 엔드 서버 풀에 추가 된 hello IP 주소를 정의 합니다.

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

Hello $server 개체 tooadd hello 값 toohello 백 엔드 풀 개체 ($pool)를 사용 합니다.

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

Hello 백 엔드 서버 풀 설정을 만듭니다.

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

Hello 수신기를 만듭니다.

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

Hello 규칙을 만듭니다.

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a>2단계

모든 개별 구성 항목 tooan 응용 프로그램 게이트웨이 구성 개체 ($appgwconfig)를 할당 합니다.

Hello 프런트 엔드 IP toohello 구성을 추가 합니다.

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

Hello 프런트 엔드 포트 toohello 구성을 추가 합니다.

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
Hello 백 엔드 서버 풀 toohello 구성을 추가 합니다.

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

Hello 백 엔드 풀 설정을 toohello 구성을 추가 합니다.

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

Hello 수신기 toohello 구성을 추가 합니다.

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

Hello 규칙 toohello 구성을 추가 합니다.

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a>3단계
Hello 구성 개체 toohello 응용 프로그램 게이트웨이 리소스를 사용 하 여 커밋 `Set-AzureApplicationGatewayConfig`합니다.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-hello-gateway"></a>Hello 게이트웨이 시작

Hello를 사용 하 여 hello 게이트웨이 구성한 후 `Start-AzureApplicationGateway` cmdlet toostart hello 게이트웨이 합니다. 응용 프로그램 게이트웨이 대 한 청구 hello 게이트웨이 성공적으로 시작 된 후 시작 합니다.

> [!NOTE]
> hello `Start-AzureApplicationGateway` cmdlet toofinish too15 20 분이 걸릴 수도 있습니다.

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a>Hello 게이트웨이 상태를 확인 합니다.

사용 하 여 hello `Get-AzureApplicationGateway` hello 게이트웨이의 cmdlet toocheck hello 상태입니다. 경우 `Start-AzureApplicationGateway` hello 이전 단계에서 성공한 *상태* 실행 해야 하 고 *Vip* 및 *DnsName* 유효한 항목 있어야 합니다.

hello 다음 예제에서는 최대, 실행 되는 응용 프로그램 게이트웨이 및 대상이 지정 되었으며 준비 tootake 트래픽 `http://<generated-dns-name>.cloudapp.net`합니다.

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
Vip           : 138.91.170.26
DnsName       : appgw-1b8402e8-3e0d-428d-b661-289c16c82101.cloudapp.net
```

## <a name="delete-hello-application-gateway"></a>Hello 응용 프로그램 게이트웨이 삭제 합니다.

toodelete hello 응용 프로그램 게이트웨이:

1. 사용 하 여 hello `Stop-AzureApplicationGateway` cmdlet toostop hello 게이트웨이 합니다.
2. 사용 하 여 hello `Remove-AzureApplicationGateway` cmdlet tooremove hello 게이트웨이 합니다.
3. Hello를 사용 하 여 해당 hello 게이트웨이에 제거 되었는지 확인 `Get-AzureApplicationGateway` cmdlet.

hello 다음 예제에서는 hello `Stop-AzureApplicationGateway` hello 첫 번째 줄에는 cmdlet hello 출력이 차례로 표시 합니다.

```powershell
Stop-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

중지 된 상태에 hello 응용 프로그램 게이트웨이 사용 하 여 hello `Remove-AzureApplicationGateway` cmdlet tooremove hello 서비스입니다.

```powershell
Remove-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

서비스 hello tooverify 제거 된 hello를 사용할 수 있습니다, `Get-AzureApplicationGateway` cmdlet. 이 단계는 필요 하지 않습니다.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
.....
```

## <a name="next-steps"></a>다음 단계

SSL 오프 로드 tooconfigure 참조 [SSL 오프 로드에 대 한 응용 프로그램 게이트웨이 구성](application-gateway-ssl.md)합니다.

내부 부하 분산 장치는 응용 프로그램 게이트웨이 toouse tooconfigure 참조 [내부 부하 분산 장치 (ILB) 응용 프로그램 게이트웨이 만들](application-gateway-ilb.md)합니다.

보다 자세한 내용을 원한다면 일반적 부하 분산 옵션을 참조:

* [Azure 부하 분산 장치](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
