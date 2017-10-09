---
title: "aaaConfigure 부하 분산 장치 TCP 유휴 시간 제한 | Microsoft Docs"
description: "분산 장치 TCP 유휴 시간 제한 구성"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 4625c6a8-5725-47ce-81db-4fa3bd055891
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 2bf0704b891f708e0a5bd7aa827441930f51cfaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a>Azure Load Balancer에 대한 TCP 유휴 시간 제한 설정 구성

기본 구성에서 Azure 부하 분산 장치의 '유휴 시간 제한' 설정은 4분입니다. 일정 시간 동안 hello 시간 제한 값 보다 긴 경우 TCP hello 되지는 또는 HTTP 세션 hello 클라이언트와 클라우드 서비스 간에 유지 됩니다.

클라이언트 응용 프로그램 hello 다음과 같은 오류 메시지가 나타날 수 hello 연결이 닫히면: "hello 기본 연결이 닫혔습니다: 연결을 활성 상태로 유지 toobe hello 서버에 의해 닫혔습니다."

일반적인 방법은 toouse TCP 연결 유지 합니다. 이 방법은 더 긴 기간에 대 한 hello 연결을 활성 상태로 유지 합니다. 자세한 내용은 이러한 [.NET 예제](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx)를 참조하세요. 와 연결 유지 하 고 사용 하도록 설정, 사용 하지 않는 hello 연결 하는 동안 패킷이 전송 합니다. 이러한 연결 유지 패킷이 확인 hello 유휴 시간 제한 값에 도달 하지 않습니다 hello 연결은 긴 기간 동안 유지 됩니다.

이 설정은 인바운드 연결에서만 작동합니다. 무시 되 hello 연결 tooavoid hello 유휴 제한 시간 설정 또는 증가 hello 유휴 시간 제한 값 보다 작은 간격으로 hello TCP 연결 유지를 구성 해야 합니다. toosupport 이러한 시나리오에 대 한 구성 가능한 유휴 시간 제한 지원이 추가 되었습니다. 이제 4 too30 분 기간에 대해 설정할 수 있습니다.

TCP 연결 유지는 배터리 수명에 대한 제약이 없는 시나리오에 적합합니다. 모바일 응용 프로그램에는 권장되지 않습니다. TCP 연결 유지 모바일 응용 프로그램에서을 사용 하 여 hello 장치 배터리를 더 빠르게 드레이닝 할 수 있습니다.

![TCP 시간 제한](./media/load-balancer-tcp-idle-timeout/image1.png)

다음 섹션 hello toochange이 유휴 가상 컴퓨터의 시간 제한 설정 하 고 클라우드 서비스 하는 방법을 설명 합니다.

## <a name="configure-hello-tcp-timeout-for-your-instance-level-public-ip-too15-minutes"></a>사용자 인스턴스 수준 공용 IP too15 분에 대 한 hello TCP 시간 제한 값 구성

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

`IdleTimeoutInMinutes` 는 선택 사항입니다. 설정 되지 않은 경우 기본 시간 제한을 hello 4 분입니다. hello 허용 가능한 제한 시간 범위는 4 too30 분입니다.

## <a name="set-hello-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a>가상 컴퓨터에서 Azure 끝점을 만드는 경우 hello 유휴 제한 시간을 설정 합니다.

toochange hello 끝점에 대해 설정 하는 시간 제한, hello 다음을 사용 하 여:

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

tooretrieve 유휴 제한 시간 구성에 다음 명령을 사용 하 여 hello:

    PS C:\> Get-AzureVM -ServiceName "MyService" -Name "MyVM" | Get-AzureEndpoint
    VERBOSE: 6:43:50 PM - Completed Operation: Get Deployment
    LBSetName : MyLoadBalancedSet
    LocalPort : 80
    Name : HTTP
    Port : 80
    Protocol : tcp
    Vip : 65.52.xxx.xxx
    ProbePath :
    ProbePort : 80
    ProbeProtocol : tcp
    ProbeIntervalInSeconds : 15
    ProbeTimeoutInSeconds : 31
    EnableDirectServerReturn : False
    Acl : {}
    InternalLoadBalancerName :
    IdleTimeoutInMinutes : 15

## <a name="set-hello-tcp-timeout-on-a-load-balanced-endpoint-set"></a>부하 분산 끝점 집합에 hello TCP 제한 시간을 설정 합니다.

끝점에 부하 분산 끝점 집합에 속해 있다면 hello TCP 시간 제한 값 hello 부하 분산 끝점 집합에 대해 설정 되어야 합니다. 예:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a>클라우드 서비스에 대한 시간 제한 설정 변경

Hello Azure SDK tooupdate 클라우드 서비스를 사용할 수 있습니다. Hello.csdef 파일에서 클라우드 서비스에 대 한 끝점 설정 하면 됩니다. 클라우드 서비스의 배포에 대 한 hello TCP 시간 제한 값을 업데이트 하려면 배포 업그레이드 합니다. 예외는 hello TCP 시간 제한 값 공용 IP에 대해서만 지정 됩니다. 공용 IP 설정을 hello.cscfg 파일에 있으며 배포 업데이트 및 업그레이드를 통해 업데이트할 수 있습니다.

hello.csdef 끝점 설정에 대 한 변경이합니다.

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

공용 Ip에서 hello 제한 시간 설정에 대 한 hello.cscfg 변경은 다음과 같습니다.

```xml
<NetworkConfiguration>
    <VirtualNetworkSite name="VNet"/>
    <AddressAssignments>
    <InstanceAddress roleName="VMRolePersisted">
    <PublicIPs>
        <PublicIP name="public-ip-name" idleTimeoutInMinutes="timeout-in-minutes"/>
    </PublicIPs>
    </InstanceAddress>
    </AddressAssignments>
</NetworkConfiguration>
```

## <a name="rest-api-example"></a>Rest API 예제

Hello 서비스 관리 API를 사용 하 여 hello TCP 유휴 시간 제한 값을 구성할 수 있습니다. 해당 hello 있는지 확인 `x-ms-version` 헤더가 tooversion 설정 되어 `2014-06-01` 이상. Hello의 hello 구성 업데이트는 배포의 모든 가상 컴퓨터에서 부하 분산 된 입력된 끝점을 지정합니다.

### <a name="request"></a>요청

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a>응답

```xml
<LoadBalancedEndpointList xmlns="http://schemas.microsoft.com/windowsazure" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <InputEndpoint>
    <LoadBalancedEndpointSetName>endpoint-set-name</LoadBalancedEndpointSetName>
    <LocalPort>local-port-number</LocalPort>
    <Port>external-port-number</Port>
    <LoadBalancerProbe>
        <Path>path-of-probe</Path>
        <Port>port-assigned-to-probe</Port>
        <Protocol>probe-protocol</Protocol>
        <IntervalInSeconds>interval-of-probe</IntervalInSeconds>
        <TimeoutInSeconds>timeout-for-probe</TimeoutInSeconds>
    </LoadBalancerProbe>
    <LoadBalancerName>name-of-internal-loadbalancer</LoadBalancerName>
    <Protocol>endpoint-protocol</Protocol>
    <IdleTimeoutInMinutes>15</IdleTimeoutInMinutes>
    <EnableDirectServerReturn>enable-direct-server-return</EnableDirectServerReturn>
    <EndpointACL>
        <Rules>
        <Rule>
            <Order>priority-of-the-rule</Order>
            <Action>permit-rule</Action>
            <RemoteSubnet>subnet-of-the-rule</RemoteSubnet>
            <Description>description-of-the-rule</Description>
        </Rule>
        </Rules>
    </EndpointACL>
    </InputEndpoint>
</LoadBalancedEndpointList>
```

## <a name="next-steps"></a>다음 단계

[내부 부하 분산 장치 개요](load-balancer-internal-overview.md)

[인터넷 연결 부하 분산 장치 구성 시작](load-balancer-get-started-internet-arm-ps.md)

[부하 분산 장치 배포 모드 구성](load-balancer-distribution-mode.md)
