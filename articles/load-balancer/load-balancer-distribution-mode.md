---
title: "부하 분산 장치 배포 모드 aaaConfigure | Microsoft Docs"
description: "어떻게 tooconfigure Azure 부하 분산 장치 배포 모드 toosupport 원본 IP 선호도"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 7df27a4d-67a8-47d6-b73e-32c0c6206e6e
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: e745240b733ffc07928d8ed0ae097785ad4f412e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-distribution-mode-for-load-balancer"></a>부하 분산 장치에 대 한 hello 배포 모드를 구성 합니다.

## <a name="hash-based-distribution-mode"></a>해시 기반 배포 모드

hello 기본 배포 알고리즘은 5-튜플 (원본 IP, 원본 포트 대상 IP, 대상 포트 프로토콜 유형) toomap 트래픽 tooavailable 서버 해시 합니다. 전송 세션 내에서만 연결이 유지됩니다. 동일한 세션 됩니다 hello 패킷에 toohello hello 부하 분산 된 끝점 뒤에 동일한 데이터 센터 IP (DIP) 인스턴스를 이동 합니다. Hello 클라이언트 시작 될 때 새 세션에서 동일한 원본 IP hello, hello 원본 포트 변경 하 고 hello 트래픽 toogo tooa 다른 DIP 끝점 발생 합니다.

![해시 기반 부하 분산 장치](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

그림 1 - 5개 튜플 배포

## <a name="source-ip-affinity-mode"></a>소스 IP 선호도 모드

원본 IP 선호도(세션 선호도 또는 클라이언트 IP 선호도라고도 함)라는 다른 배포 모드가 있습니다. 3-튜플 (원본 IP, 대상 IP, 프로토콜) toomap 트래픽 toohello 사용 가능한 서버 또는 azure 부하 분산 장치 구성된 toouse는 2-튜플 (원본 IP, 대상 IP)를 수 있습니다. 원본 IP 선호도 사용 하 여 연결에서에서 시작 된 hello 동일한 클라이언트 컴퓨터 라인 toohello 동일한 DIP 끝점입니다.

hello 다이어그램을 다음에 2 튜플 구성을 보여 줍니다. 컴퓨터를 통해 hello 부하 분산 장치 toovirtual 1 (VM1) 다음 v m 2와 VM3으로 백업 되는 hello 2-튜플 실행 하는 방법을 확인 합니다.

![세션 선호도](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

그림 2 - 2개 튜플 배포

원본 IP 선호도 hello Azure 부하 분산 장치 및 RD (원격 데스크톱) 게이트웨이 간의 비 호환성을 해결합니다. 이제 단일 클라우드 서비스에서 RD 게이트웨이 팜을 빌드할 수 있습니다.

다른 사용 사례 시나리오는 미디어 업로드 여기서 hello 데이터 업로드 UDP를 통해 수행 되지만 hello 제어 평면 TCP를 통해 이루어집니다.

* 먼저 클라이언트 toohello 부하가 공용 주소 TCP 세션을 시작, 특정 DIP,이 채널은 방향이 지정 된 tooa 왼쪽된 활성 toomonitor hello 연결 상태를 가져옵니다.
* 동일한 클라이언트 컴퓨터는 hello에서 새 UDP 세션이 시작 toohello 동일한 부하 분산 된 공용 끝점, hello 여기가이 연결 directed toohello 이기도 hello 이전 TCP 연결으로 동일한 DIP 끝점을 미디어 업로드 될 수 있습니다 또한 TCP 통해 컨트롤 채널을 유지 하면서 높은 처리량에서 실행 합니다.

> [!NOTE]
> 부하 분산 집합 변경 (추가 또는 제거 된 가상 컴퓨터), 되 면 클라이언트 요청의 hello 배포 다시 계산 됩니다. 종료 hello 동일한 기존 클라이언트 로부터의 새 연결에 종속 될 수 없도록 서버. 또한 원본 IP 선호도를 사용하는 경우 트래픽이 불규칙하게 배포될 수 있습니다. 프록시 뒤에서 실행되는 클라이언트는 하나의 고유한 클라이언트 응용 프로그램으로 표시될 수 있습니다.

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a>부하 분산 장치에 대한 원본 IP 선호도 설정 구성

가상 컴퓨터에 대 한 PowerShell toochange 제한 시간 설정을 사용할 수 있습니다.

Azure 끝점 tooa 가상 컴퓨터를 추가 하 고 부하 분산 장치 배포 모드 설정

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

2-튜플 (원본 IP, 대상 IP) 부하 분산을 위한, sourceIPProtocol 3-튜플 (원본 IP, 대상 IP, 프로토콜) 부하 분산 또는 none에 대해 5-튜플 부하 분산의 hello 기본 동작을 원하는 경우 toosourceIP LoadBalancerDistribution은 설정할 수 있습니다.

Tooretrieve 끝점 부하 분산 장치 배포 모드 구성에 따라 hello를 사용 합니다.

    PS C:\> Get-AzureVM –ServiceName MyService –Name MyVM | Get-AzureEndpoint

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
    LoadBalancerDistribution : sourceIP

Hello LoadBalancerDistribution 요소가 없으면 hello Azure 부하 분산 장치 hello 기본 5-튜플 알고리즘을 사용 합니다.

### <a name="set-hello-distribution-mode-on-a-load-balanced-endpoint-set"></a>부하 분산 끝점 집합에 사용 되는 hello 배포 모드 설정

끝점에 부하 분산 끝점 집합에 속해 있다면 hello 부하 분산 끝점 집합에 hello 배포 모드를 설정 해야 합니다.

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-toochange-distribution-mode"></a>클라우드 서비스 구성 toochange 배포 모드

Hello Azure SDK for.NET 2.5 (11 월에 릴리스된 toobe) 활용할 수 있는 tooupdate 클라우드 서비스입니다. 클라우드 서비스에 대 한 끝점 설정은 hello.csdef에서 이루어집니다. 순서 tooupdate hello 부하 분산 장치 배포 모드에서 클라우드 서비스 배포에 대 한 배포 업그레이드는 필수입니다.
아래에 .csdef에서 끝점 설정을 변경하는 예제가 나와 있습니다.

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancerDistribution="sourceIP" />
    </Endpoints>
</WorkerRole>
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

## <a name="api-example"></a>API 예제

Hello 서비스 관리 API를 사용 하 여 hello 부하 분산 장치 배포를 구성할 수 있습니다. 있는지 tooadd hello 확인 `x-ms-version` 헤더가 tooversion 설정 되어 `2014-09-01` 이상.

### <a name="update-hello-configuration-of-hello-specified-load-balanced-set-in-a-deployment"></a>Hello의 hello 구성 업데이트 배포의 부하 분산 집합 지정

#### <a name="request-example"></a>요청 예제

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>?comp=UpdateLbSet   x-ms-version: 2014-09-01
    Content-Type: application/xml

    <LoadBalancedEndpointList xmlns="http://schemas.microsoft.com/windowsazure" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
      <InputEndpoint>
        <LoadBalancedEndpointSetName> endpoint-set-name </LoadBalancedEndpointSetName>
        <LocalPort> local-port-number </LocalPort>
        <Port> external-port-number </Port>
        <LoadBalancerProbe>
          <Port> port-assigned-to-probe </Port>
          <Protocol> probe-protocol </Protocol>
          <IntervalInSeconds> interval-of-probe </IntervalInSeconds>
          <TimeoutInSeconds> timeout-for-probe </TimeoutInSeconds>
        </LoadBalancerProbe>
        <Protocol> endpoint-protocol </Protocol>
        <EnableDirectServerReturn> enable-direct-server-return </EnableDirectServerReturn>
        <IdleTimeoutInMinutes>idle-time-out</IdleTimeoutInMinutes>
        <LoadBalancerDistribution>sourceIP</LoadBalancerDistribution>
      </InputEndpoint>
    </LoadBalancedEndpointList>

hello LoadBalancerDistribution의 값일 수 sourceIP 2 튜플 선호도, sourceIPProtocol 선호도 3-튜플 또는 none (선호도 없음. 5개 튜플이 사용됨).

#### <a name="response"></a>응답

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a>다음 단계

[내부 부하 분산 장치 개요](load-balancer-internal-overview.md)

[인터넷 연결 부하 분산 장치 구성 시작](load-balancer-get-started-internet-arm-ps.md)

[부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성](load-balancer-tcp-idle-timeout.md)
