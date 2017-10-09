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
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a><span data-ttu-id="5fe0c-103">Azure Load Balancer에 대한 TCP 유휴 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="5fe0c-103">Configure TCP idle timeout settings for Azure Load Balancer</span></span>

<span data-ttu-id="5fe0c-104">기본 구성에서 Azure 부하 분산 장치의 '유휴 시간 제한' 설정은 4분입니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-104">In its default configuration, Azure Load Balancer has an idle timeout setting of 4 minutes.</span></span> <span data-ttu-id="5fe0c-105">일정 시간 동안 hello 시간 제한 값 보다 긴 경우 TCP hello 되지는 또는 HTTP 세션 hello 클라이언트와 클라우드 서비스 간에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-105">If a period of inactivity is longer than hello timeout value, there's no guarantee that hello TCP or HTTP session is maintained between hello client and your cloud service.</span></span>

<span data-ttu-id="5fe0c-106">클라이언트 응용 프로그램 hello 다음과 같은 오류 메시지가 나타날 수 hello 연결이 닫히면: "hello 기본 연결이 닫혔습니다: 연결을 활성 상태로 유지 toobe hello 서버에 의해 닫혔습니다."</span><span class="sxs-lookup"><span data-stu-id="5fe0c-106">When hello connection is closed, your client application may receive hello following error message: "hello underlying connection was closed: A connection that was expected toobe kept alive was closed by hello server."</span></span>

<span data-ttu-id="5fe0c-107">일반적인 방법은 toouse TCP 연결 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-107">A common practice is toouse a TCP keep-alive.</span></span> <span data-ttu-id="5fe0c-108">이 방법은 더 긴 기간에 대 한 hello 연결을 활성 상태로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-108">This practice keeps hello connection active for a longer period.</span></span> <span data-ttu-id="5fe0c-109">자세한 내용은 이러한 [.NET 예제](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-109">For more information, see these [.NET examples](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span></span> <span data-ttu-id="5fe0c-110">와 연결 유지 하 고 사용 하도록 설정, 사용 하지 않는 hello 연결 하는 동안 패킷이 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-110">With keep-alive enabled, packets are sent during periods of inactivity on hello connection.</span></span> <span data-ttu-id="5fe0c-111">이러한 연결 유지 패킷이 확인 hello 유휴 시간 제한 값에 도달 하지 않습니다 hello 연결은 긴 기간 동안 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-111">These keep-alive packets ensure that hello idle timeout value is never reached and hello connection is maintained for a long period.</span></span>

<span data-ttu-id="5fe0c-112">이 설정은 인바운드 연결에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-112">This setting works for inbound connections only.</span></span> <span data-ttu-id="5fe0c-113">무시 되 hello 연결 tooavoid hello 유휴 제한 시간 설정 또는 증가 hello 유휴 시간 제한 값 보다 작은 간격으로 hello TCP 연결 유지를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-113">tooavoid losing hello connection, you must configure hello TCP keep-alive with an interval less than hello idle timeout setting or increase hello idle timeout value.</span></span> <span data-ttu-id="5fe0c-114">toosupport 이러한 시나리오에 대 한 구성 가능한 유휴 시간 제한 지원이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-114">toosupport such scenarios, we've added support for a configurable idle timeout.</span></span> <span data-ttu-id="5fe0c-115">이제 4 too30 분 기간에 대해 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-115">You can now set it for a duration of 4 too30 minutes.</span></span>

<span data-ttu-id="5fe0c-116">TCP 연결 유지는 배터리 수명에 대한 제약이 없는 시나리오에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-116">TCP keep-alive works well for scenarios where battery life is not a constraint.</span></span> <span data-ttu-id="5fe0c-117">모바일 응용 프로그램에는 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-117">It is not recommended for mobile applications.</span></span> <span data-ttu-id="5fe0c-118">TCP 연결 유지 모바일 응용 프로그램에서을 사용 하 여 hello 장치 배터리를 더 빠르게 드레이닝 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-118">Using a TCP keep-alive in a mobile application can drain hello device battery faster.</span></span>

![TCP 시간 제한](./media/load-balancer-tcp-idle-timeout/image1.png)

<span data-ttu-id="5fe0c-120">다음 섹션 hello toochange이 유휴 가상 컴퓨터의 시간 제한 설정 하 고 클라우드 서비스 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-120">hello following sections describe how toochange idle timeout settings in virtual machines and cloud services.</span></span>

## <a name="configure-hello-tcp-timeout-for-your-instance-level-public-ip-too15-minutes"></a><span data-ttu-id="5fe0c-121">사용자 인스턴스 수준 공용 IP too15 분에 대 한 hello TCP 시간 제한 값 구성</span><span class="sxs-lookup"><span data-stu-id="5fe0c-121">Configure hello TCP timeout for your instance-level public IP too15 minutes</span></span>

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

<span data-ttu-id="5fe0c-122">`IdleTimeoutInMinutes` 는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-122">`IdleTimeoutInMinutes` is optional.</span></span> <span data-ttu-id="5fe0c-123">설정 되지 않은 경우 기본 시간 제한을 hello 4 분입니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-123">If it is not set, hello default timeout is 4 minutes.</span></span> <span data-ttu-id="5fe0c-124">hello 허용 가능한 제한 시간 범위는 4 too30 분입니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-124">hello acceptable timeout range is 4 too30 minutes.</span></span>

## <a name="set-hello-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a><span data-ttu-id="5fe0c-125">가상 컴퓨터에서 Azure 끝점을 만드는 경우 hello 유휴 제한 시간을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-125">Set hello idle timeout when creating an Azure endpoint on a virtual machine</span></span>

<span data-ttu-id="5fe0c-126">toochange hello 끝점에 대해 설정 하는 시간 제한, hello 다음을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="5fe0c-126">toochange hello timeout setting for an endpoint, use hello following:</span></span>

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

<span data-ttu-id="5fe0c-127">tooretrieve 유휴 제한 시간 구성에 다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="5fe0c-127">tooretrieve your idle timeout configuration, use hello following command:</span></span>

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

## <a name="set-hello-tcp-timeout-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="5fe0c-128">부하 분산 끝점 집합에 hello TCP 제한 시간을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-128">Set hello TCP timeout on a load-balanced endpoint set</span></span>

<span data-ttu-id="5fe0c-129">끝점에 부하 분산 끝점 집합에 속해 있다면 hello TCP 시간 제한 값 hello 부하 분산 끝점 집합에 대해 설정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-129">If endpoints are part of a load-balanced endpoint set, hello TCP timeout must be set on hello load-balanced endpoint set.</span></span> <span data-ttu-id="5fe0c-130">예:</span><span class="sxs-lookup"><span data-stu-id="5fe0c-130">For example:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a><span data-ttu-id="5fe0c-131">클라우드 서비스에 대한 시간 제한 설정 변경</span><span class="sxs-lookup"><span data-stu-id="5fe0c-131">Change timeout settings for cloud services</span></span>

<span data-ttu-id="5fe0c-132">Hello Azure SDK tooupdate 클라우드 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-132">You can use hello Azure SDK tooupdate your cloud service.</span></span> <span data-ttu-id="5fe0c-133">Hello.csdef 파일에서 클라우드 서비스에 대 한 끝점 설정 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-133">You make endpoint settings for cloud services in hello .csdef file.</span></span> <span data-ttu-id="5fe0c-134">클라우드 서비스의 배포에 대 한 hello TCP 시간 제한 값을 업데이트 하려면 배포 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-134">Updating hello TCP timeout for deployment of a cloud service requires a deployment upgrade.</span></span> <span data-ttu-id="5fe0c-135">예외는 hello TCP 시간 제한 값 공용 IP에 대해서만 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-135">An exception is if hello TCP timeout is specified only for a public IP.</span></span> <span data-ttu-id="5fe0c-136">공용 IP 설정을 hello.cscfg 파일에 있으며 배포 업데이트 및 업그레이드를 통해 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-136">Public IP settings are in hello .cscfg file, and you can update them through deployment update and upgrade.</span></span>

<span data-ttu-id="5fe0c-137">hello.csdef 끝점 설정에 대 한 변경이합니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-137">hello .csdef changes for endpoint settings are:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="5fe0c-138">공용 Ip에서 hello 제한 시간 설정에 대 한 hello.cscfg 변경은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-138">hello .cscfg changes for hello timeout setting on public IPs are:</span></span>

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

## <a name="rest-api-example"></a><span data-ttu-id="5fe0c-139">Rest API 예제</span><span class="sxs-lookup"><span data-stu-id="5fe0c-139">REST API example</span></span>

<span data-ttu-id="5fe0c-140">Hello 서비스 관리 API를 사용 하 여 hello TCP 유휴 시간 제한 값을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-140">You can configure hello TCP idle timeout by using hello service management API.</span></span> <span data-ttu-id="5fe0c-141">해당 hello 있는지 확인 `x-ms-version` 헤더가 tooversion 설정 되어 `2014-06-01` 이상.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-141">Make sure that hello `x-ms-version` header is set tooversion `2014-06-01` or later.</span></span> <span data-ttu-id="5fe0c-142">Hello의 hello 구성 업데이트는 배포의 모든 가상 컴퓨터에서 부하 분산 된 입력된 끝점을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5fe0c-142">Update hello configuration of hello specified load-balanced input endpoints on all virtual machines in a deployment.</span></span>

### <a name="request"></a><span data-ttu-id="5fe0c-143">요청</span><span class="sxs-lookup"><span data-stu-id="5fe0c-143">Request</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a><span data-ttu-id="5fe0c-144">응답</span><span class="sxs-lookup"><span data-stu-id="5fe0c-144">Response</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5fe0c-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5fe0c-145">Next steps</span></span>

[<span data-ttu-id="5fe0c-146">내부 부하 분산 장치 개요</span><span class="sxs-lookup"><span data-stu-id="5fe0c-146">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="5fe0c-147">인터넷 연결 부하 분산 장치 구성 시작</span><span class="sxs-lookup"><span data-stu-id="5fe0c-147">Get started configuring an Internet-facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="5fe0c-148">부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="5fe0c-148">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)
