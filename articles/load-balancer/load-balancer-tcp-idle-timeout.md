---
title: "부하 분산 장치 TCP 유휴 시간 제한 구성 | Microsoft Docs"
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
ms.openlocfilehash: d040fe6580b8ae777aecc9dd385ed33861530c38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a><span data-ttu-id="7946d-103">Azure Load Balancer에 대한 TCP 유휴 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="7946d-103">Configure TCP idle timeout settings for Azure Load Balancer</span></span>

<span data-ttu-id="7946d-104">기본 구성에서 Azure 부하 분산 장치의 '유휴 시간 제한' 설정은 4분입니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-104">In its default configuration, Azure Load Balancer has an idle timeout setting of 4 minutes.</span></span> <span data-ttu-id="7946d-105">비활성 기간이 시간 제한 값보다 긴 경우 클라이언트와 클라우드 서비스 간의 TCP 또는 HTTP 세션이 유지되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-105">If a period of inactivity is longer than the timeout value, there's no guarantee that the TCP or HTTP session is maintained between the client and your cloud service.</span></span>

<span data-ttu-id="7946d-106">연결이 닫히면 클라이언트 응용 프로그램에 "기본 연결이 닫혔습니다. 활성 상태로 유지될 것으로 예상된 연결이 서버에서 닫혔습니다."와 같은 오류 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-106">When the connection is closed, your client application may receive the following error message: "The underlying connection was closed: A connection that was expected to be kept alive was closed by the server."</span></span>

<span data-ttu-id="7946d-107">일반적인 방법은 TCP 연결 유지를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-107">A common practice is to use a TCP keep-alive.</span></span> <span data-ttu-id="7946d-108">이 방법은 더 오랜 기간 동안 연결을 활성 상태로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-108">This practice keeps the connection active for a longer period.</span></span> <span data-ttu-id="7946d-109">자세한 내용은 이러한 [.NET 예제](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7946d-109">For more information, see these [.NET examples](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span></span> <span data-ttu-id="7946d-110">연결 유지를 사용하면 연결 비활성화 기간 동안 패킷이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-110">With keep-alive enabled, packets are sent during periods of inactivity on the connection.</span></span> <span data-ttu-id="7946d-111">이러한 연결 유지 패킷은 유휴 시간 제한 값에 도달하지 않도록 하고 연결이 장기간 유지되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-111">These keep-alive packets ensure that the idle timeout value is never reached and the connection is maintained for a long period.</span></span>

<span data-ttu-id="7946d-112">이 설정은 인바운드 연결에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-112">This setting works for inbound connections only.</span></span> <span data-ttu-id="7946d-113">연결 끊김을 방지하려면 유휴 시간 제한 설정보다 낮은 간격으로 TCP 연결 유지를 구성하거나 유휴 시간 제한 값을 증가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-113">To avoid losing the connection, you must configure the TCP keep-alive with an interval less than the idle timeout setting or increase the idle timeout value.</span></span> <span data-ttu-id="7946d-114">이러한 시나리오를 지원하기 위해 구성 가능한 유휴 시간 제한에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-114">To support such scenarios, we've added support for a configurable idle timeout.</span></span> <span data-ttu-id="7946d-115">이제 4분에서 30분 사이의 기간으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-115">You can now set it for a duration of 4 to 30 minutes.</span></span>

<span data-ttu-id="7946d-116">TCP 연결 유지는 배터리 수명에 대한 제약이 없는 시나리오에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-116">TCP keep-alive works well for scenarios where battery life is not a constraint.</span></span> <span data-ttu-id="7946d-117">모바일 응용 프로그램에는 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-117">It is not recommended for mobile applications.</span></span> <span data-ttu-id="7946d-118">모바일 응용 프로그램에서 TCP 연결 유지를 사용하면 장치 배터리가 더 빨리 방전될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-118">Using a TCP keep-alive in a mobile application can drain the device battery faster.</span></span>

![TCP 시간 제한](./media/load-balancer-tcp-idle-timeout/image1.png)

<span data-ttu-id="7946d-120">다음 섹션에서는 가상 컴퓨터 및 클라우드 서비스의 유휴 시간 제한 설정을 변경하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-120">The following sections describe how to change idle timeout settings in virtual machines and cloud services.</span></span>

## <a name="configure-the-tcp-timeout-for-your-instance-level-public-ip-to-15-minutes"></a><span data-ttu-id="7946d-121">인스턴스 수준 공용 IP의 TCP 시간 제한을 15분으로 구성</span><span class="sxs-lookup"><span data-stu-id="7946d-121">Configure the TCP timeout for your instance-level public IP to 15 minutes</span></span>

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

<span data-ttu-id="7946d-122">`IdleTimeoutInMinutes` 는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-122">`IdleTimeoutInMinutes` is optional.</span></span> <span data-ttu-id="7946d-123">설정하지 않은 경우 기본 시간 제한은 4분입니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-123">If it is not set, the default timeout is 4 minutes.</span></span> <span data-ttu-id="7946d-124">허용되는 시간 제한 범위는 4분에서 30분 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-124">The acceptable timeout range is 4 to 30 minutes.</span></span>

## <a name="set-the-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a><span data-ttu-id="7946d-125">가상 컴퓨터에서 Azure 끝점을 만들 때 유휴 시간 제한 설정</span><span class="sxs-lookup"><span data-stu-id="7946d-125">Set the idle timeout when creating an Azure endpoint on a virtual machine</span></span>

<span data-ttu-id="7946d-126">끝점에 대한 시간 제한 설정을 변경하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-126">To change the timeout setting for an endpoint, use the following:</span></span>

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

<span data-ttu-id="7946d-127">유휴 시간 제한 구성을 검색하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-127">To retrieve your idle timeout configuration, use the following command:</span></span>

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

## <a name="set-the-tcp-timeout-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="7946d-128">부하 분산된 끝점 집합에 대한 TCP 시간 제한 설정</span><span class="sxs-lookup"><span data-stu-id="7946d-128">Set the TCP timeout on a load-balanced endpoint set</span></span>

<span data-ttu-id="7946d-129">부하 분산된 끝점 집합에 끝점이 포함되어 있으면 부하 분산된 끝점 집합에 대해 TCP 시간 제한을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-129">If endpoints are part of a load-balanced endpoint set, the TCP timeout must be set on the load-balanced endpoint set.</span></span> <span data-ttu-id="7946d-130">예:</span><span class="sxs-lookup"><span data-stu-id="7946d-130">For example:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a><span data-ttu-id="7946d-131">클라우드 서비스에 대한 시간 제한 설정 변경</span><span class="sxs-lookup"><span data-stu-id="7946d-131">Change timeout settings for cloud services</span></span>

<span data-ttu-id="7946d-132">Azure SDK를 사용하여 클라우드 서비스를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-132">You can use the Azure SDK to update your cloud service.</span></span> <span data-ttu-id="7946d-133">.csdef 파일에서 클라우드 서비스용 끝점 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-133">You make endpoint settings for cloud services in the .csdef file.</span></span> <span data-ttu-id="7946d-134">클라우드 서비스의 배포에 대한 TCP 시간 제한을 업데이트하려면 배포를 업그레이드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-134">Updating the TCP timeout for deployment of a cloud service requires a deployment upgrade.</span></span> <span data-ttu-id="7946d-135">단, 공용 IP에 대해서만 TCP 시간 제한을 지정하는 경우는 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-135">An exception is if the TCP timeout is specified only for a public IP.</span></span> <span data-ttu-id="7946d-136">공용 IP 설정은 .cscfg에 포함되어 있으므로 배포 업데이트 및 업그레이드를 통해 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-136">Public IP settings are in the .cscfg file, and you can update them through deployment update and upgrade.</span></span>

<span data-ttu-id="7946d-137">아래에 .csdef에서 끝점 설정을 변경하는 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-137">The .csdef changes for endpoint settings are:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="7946d-138">공용 IP의 시간 제한 설정에 대한 .cscfg 변경 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-138">The .cscfg changes for the timeout setting on public IPs are:</span></span>

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

## <a name="rest-api-example"></a><span data-ttu-id="7946d-139">Rest API 예제</span><span class="sxs-lookup"><span data-stu-id="7946d-139">REST API example</span></span>

<span data-ttu-id="7946d-140">Service Management API를 사용하여 TCP 유휴 시간 제한을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-140">You can configure the TCP idle timeout by using the service management API.</span></span> <span data-ttu-id="7946d-141">`x-ms-version` 헤더가 `2014-06-01` 버전 이상으로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-141">Make sure that the `x-ms-version` header is set to version `2014-06-01` or later.</span></span> <span data-ttu-id="7946d-142">배포의 모든 가상 컴퓨터에서 지정한 부하 분산된 입력 끝점의 구성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7946d-142">Update the configuration of the specified load-balanced input endpoints on all virtual machines in a deployment.</span></span>

### <a name="request"></a><span data-ttu-id="7946d-143">요청</span><span class="sxs-lookup"><span data-stu-id="7946d-143">Request</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a><span data-ttu-id="7946d-144">응답</span><span class="sxs-lookup"><span data-stu-id="7946d-144">Response</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7946d-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7946d-145">Next steps</span></span>

[<span data-ttu-id="7946d-146">내부 부하 분산 장치 개요</span><span class="sxs-lookup"><span data-stu-id="7946d-146">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="7946d-147">인터넷 연결 부하 분산 장치 구성 시작</span><span class="sxs-lookup"><span data-stu-id="7946d-147">Get started configuring an Internet-facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="7946d-148">부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="7946d-148">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)
