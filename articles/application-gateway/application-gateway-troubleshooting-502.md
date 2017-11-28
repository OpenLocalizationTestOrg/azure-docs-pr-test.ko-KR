---
title: "Azure 응용 프로그램 게이트웨이 잘못 된 게이트웨이 (502) 오류 aaaTroubleshoot | Microsoft Docs"
description: "자세한 방법을 응용 프로그램 게이트웨이 502 tootroubleshoot 오류"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 1d431ead-d318-47d8-b3ad-9c69f7e08813
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: a50f736ac157256a53f6fbe3a208f0c11dd58f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a><span data-ttu-id="d595f-103">응용 프로그램 게이트웨이의 잘못된 게이트웨이 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="d595f-103">Troubleshooting bad gateway errors in Application Gateway</span></span>

<span data-ttu-id="d595f-104">응용 프로그램 게이트웨이 사용 하는 경우 tootroubleshoot 잘못 된 게이트웨이 (502) 오류 수신 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-104">Learn how tootroubleshoot bad gateway (502) errors received when using application gateway.</span></span>

## <a name="overview"></a><span data-ttu-id="d595f-105">개요</span><span class="sxs-lookup"><span data-stu-id="d595f-105">Overview</span></span>

<span data-ttu-id="d595f-106">응용 프로그램 게이트웨이 구성한 후 사용자가 발생할 수 있는 hello 오류 중 하나는 "서버 오류: 502-웹 서버는 게이트웨이 또는 프록시 서버 역할을 하는 동안 잘못 된 응답을 받았습니다"입니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-106">After configuring an application gateway, one of hello errors that users may encounter is "Server Error: 502 - Web server received an invalid response while acting as a gateway or proxy server".</span></span> <span data-ttu-id="d595f-107">이 오류는 toohello 다음 인해 발생할 수 있습니다는 주요 이유:</span><span class="sxs-lookup"><span data-stu-id="d595f-107">This error may happen due toohello following main reasons:</span></span>

* <span data-ttu-id="d595f-108">Azure Application Gateway의 [백 엔드 풀은 구성되어 있지 않거나 비어 있습니다](#empty-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="d595f-108">Azure Application Gateway's [back-end pool is not configured or empty](#empty-backendaddresspool).</span></span>
* <span data-ttu-id="d595f-109">Hello Vm 또는에서 인스턴스 [정상은 VM 크기 집합](#unhealthy-instances-in-backendaddresspool)합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-109">None of hello VMs or instances in [VM Scale Set are healthy](#unhealthy-instances-in-backendaddresspool).</span></span>
* <span data-ttu-id="d595f-110">백 엔드 Vm 또는 VM 크기 집합의 인스턴스는 [응답 하지 않는 toohello 기본 상태 프로브](#problems-with-default-health-probe.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-110">Back-end VMs or instances of VM Scale Set are [not responding toohello default health probe](#problems-with-default-health-probe.md).</span></span>
* <span data-ttu-id="d595f-111">사용자 지정 상태 프로브의 구성이 [잘못되었거나 부적절합니다](#problems-with-custom-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="d595f-111">Invalid or improper [configuration of custom health probes](#problems-with-custom-health-probe.md).</span></span>
* <span data-ttu-id="d595f-112">사용자 요청과 관련된 [요청 시간 초과 또는 연결 문제입니다](#request-time-out).</span><span class="sxs-lookup"><span data-stu-id="d595f-112">[Request time out or connectivity issues](#request-time-out) with user requests.</span></span>

## <a name="empty-backendaddresspool"></a><span data-ttu-id="d595f-113">비어 있는 BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="d595f-113">Empty BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="d595f-114">원인</span><span class="sxs-lookup"><span data-stu-id="d595f-114">Cause</span></span>

<span data-ttu-id="d595f-115">응용 프로그램 게이트웨이 hello에 Vm이 없는 경우 hello 백 엔드 주소 풀에 구성 된 VM 크기 집합, 모든 고객의 요청을 라우팅할 수 없으면 하 고 잘못 된 게이트웨이 오류를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-115">If hello Application Gateway has no VMs or VM Scale Set configured in hello back-end address pool, it cannot route any customer request and throws a bad gateway error.</span></span>

### <a name="solution"></a><span data-ttu-id="d595f-116">해결 방법</span><span class="sxs-lookup"><span data-stu-id="d595f-116">Solution</span></span>

<span data-ttu-id="d595f-117">Hello 백 엔드 주소 풀이 비어 있지 않은지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d595f-117">Ensure that hello back-end address pool is not empty.</span></span> <span data-ttu-id="d595f-118">PowerShell, CLI 또는 포털을 통해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-118">This can be done either via PowerShell, CLI, or portal.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

<span data-ttu-id="d595f-119">hello 출력 hello cmdlet 앞에서 비어 있지 않은 백 엔드 주소 풀을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-119">hello output from hello preceding cmdlet should contain non-empty back-end address pool.</span></span> <span data-ttu-id="d595f-120">다음은 백 엔드 VM에 대한 FQDN 또는 IP 주소로 구성된 두 개의 풀을 반환하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-120">Following is an example where two pools are returned which are configured with FQDN or IP addresses for backend VMs.</span></span> <span data-ttu-id="d595f-121">프로비저닝 상태입니다. hello BackendAddressPool hello 해야 ' 성공 ' 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-121">hello provisioning state of hello BackendAddressPool must be 'Succeeded'.</span></span>

<span data-ttu-id="d595f-122">BackendAddressPoolsText:</span><span class="sxs-lookup"><span data-stu-id="d595f-122">BackendAddressPoolsText:</span></span>

```json
[{
    "BackendAddresses": [{
        "ipAddress": "10.0.0.10",
        "ipAddress": "10.0.0.11"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool01",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool01"
}, {
    "BackendAddresses": [{
        "Fqdn": "xyx.cloudapp.net",
        "Fqdn": "abc.cloudapp.net"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool02",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool02"
}]
```

## <a name="unhealthy-instances-in-backendaddresspool"></a><span data-ttu-id="d595f-123">BackendAddressPool의 비정상 인스턴스</span><span class="sxs-lookup"><span data-stu-id="d595f-123">Unhealthy instances in BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="d595f-124">원인</span><span class="sxs-lookup"><span data-stu-id="d595f-124">Cause</span></span>

<span data-ttu-id="d595f-125">모든 hello 인스턴스의 BackendAddressPool 요소가 비정상적인 경우 응용 프로그램 게이트웨이 백 엔드 tooroute 사용자 요청을 없을 것.</span><span class="sxs-lookup"><span data-stu-id="d595f-125">If all hello instances of BackendAddressPool are unhealthy, then Application Gateway would not have any back-end tooroute user request to.</span></span> <span data-ttu-id="d595f-126">백 엔드 인스턴스 올바르게 작동 하지만 hello 필요한 응용 프로그램을 배포 하지 않은 경우에이 hello 사례 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-126">This could also be hello case when back-end instances are healthy but do not have hello required application deployed.</span></span>

### <a name="solution"></a><span data-ttu-id="d595f-127">해결 방법</span><span class="sxs-lookup"><span data-stu-id="d595f-127">Solution</span></span>

<span data-ttu-id="d595f-128">Hello 인스턴스 정상이 고 hello 올바르게 구성 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-128">Ensure that hello instances are healthy and hello application is properly configured.</span></span> <span data-ttu-id="d595f-129">검사는 hello 백 엔드 인스턴스 수 toorespond tooa ping 내 다른 VM에는 동일한 VNet hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-129">Check if hello back-end instances are able toorespond tooa ping from another VM in hello same VNet.</span></span> <span data-ttu-id="d595f-130">공용 끝점을 구성 하는 경우 브라우저 요청 toohello 웹 응용 프로그램 서비스 가능 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-130">If configured with a public end point, ensure that a browser request toohello web application is serviceable.</span></span>

## <a name="problems-with-default-health-probe"></a><span data-ttu-id="d595f-131">기본 상태 검색의 문제</span><span class="sxs-lookup"><span data-stu-id="d595f-131">Problems with default health probe</span></span>

### <a name="cause"></a><span data-ttu-id="d595f-132">원인</span><span class="sxs-lookup"><span data-stu-id="d595f-132">Cause</span></span>

<span data-ttu-id="d595f-133">502 오류는 또한 기본 상태 프로브 hello 부당한 수 없는 상태 tooreach 백 엔드 Vm은 합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-133">502 errors can also be frequent indicators that hello default health probe is not able tooreach back-end VMs.</span></span> <span data-ttu-id="d595f-134">응용 프로그램 게이트웨이 인스턴스를 프로 비전 되 면 자동으로 구성 기본 상태 프로브 tooeach BackendAddressPool hello BackendHttpSetting의 속성을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-134">When an Application Gateway instance is provisioned, it automatically configures a default health probe tooeach BackendAddressPool using properties of hello BackendHttpSetting.</span></span> <span data-ttu-id="d595f-135">사용자 입력은 필수 tooset이이 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-135">No user input is required tooset this probe.</span></span> <span data-ttu-id="d595f-136">특히, 부하 분산 규칙을 구성한 경우 BackendHttpSetting와 BackendAddressPool 간에 연결이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-136">Specifically, when a load balancing rule is configured, an association is made between a BackendHttpSetting and BackendAddressPool.</span></span> <span data-ttu-id="d595f-137">기본 검색 이러한 연결 및 응용 프로그램 게이트웨이 시작 하에서 정기 상태 검사 연결 tooeach 인스턴스 hello BackendAddressPool hello BackendHttpSetting 요소에 지정 된 hello 포트에서 각각에 대해 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-137">A default probe is configured for each of these associations and Application Gateway initiates a periodic health check connection tooeach instance in hello BackendAddressPool at hello port specified in hello BackendHttpSetting element.</span></span> <span data-ttu-id="d595f-138">다음 표에서 hello 기본 상태 프로브와 관련 된 hello 값을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-138">Following table lists hello values associated with hello default health probe.</span></span>

| <span data-ttu-id="d595f-139">프로브 속성</span><span class="sxs-lookup"><span data-stu-id="d595f-139">Probe property</span></span> | <span data-ttu-id="d595f-140">값</span><span class="sxs-lookup"><span data-stu-id="d595f-140">Value</span></span> | <span data-ttu-id="d595f-141">설명</span><span class="sxs-lookup"><span data-stu-id="d595f-141">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d595f-142">프로브 URL</span><span class="sxs-lookup"><span data-stu-id="d595f-142">Probe URL</span></span> |<span data-ttu-id="d595f-143">http://127.0.0.1/</span><span class="sxs-lookup"><span data-stu-id="d595f-143">http://127.0.0.1/</span></span> |<span data-ttu-id="d595f-144">URL 경로</span><span class="sxs-lookup"><span data-stu-id="d595f-144">URL path</span></span> |
| <span data-ttu-id="d595f-145">간격</span><span class="sxs-lookup"><span data-stu-id="d595f-145">Interval</span></span> |<span data-ttu-id="d595f-146">30</span><span class="sxs-lookup"><span data-stu-id="d595f-146">30</span></span> |<span data-ttu-id="d595f-147">프로브 간격(초)</span><span class="sxs-lookup"><span data-stu-id="d595f-147">Probe interval in seconds</span></span> |
| <span data-ttu-id="d595f-148">시간 제한</span><span class="sxs-lookup"><span data-stu-id="d595f-148">Time-out</span></span> |<span data-ttu-id="d595f-149">30</span><span class="sxs-lookup"><span data-stu-id="d595f-149">30</span></span> |<span data-ttu-id="d595f-150">프로브 시간 제한(초)</span><span class="sxs-lookup"><span data-stu-id="d595f-150">Probe time-out in seconds</span></span> |
| <span data-ttu-id="d595f-151">비정상 임계값</span><span class="sxs-lookup"><span data-stu-id="d595f-151">Unhealthy threshold</span></span> |<span data-ttu-id="d595f-152">3</span><span class="sxs-lookup"><span data-stu-id="d595f-152">3</span></span> |<span data-ttu-id="d595f-153">프로브 재시도 횟수.</span><span class="sxs-lookup"><span data-stu-id="d595f-153">Probe retry count.</span></span> <span data-ttu-id="d595f-154">hello 연속 프로브 오류 발생 횟수 hello 비정상 임계값에 도달 하면 hello 백 엔드 서버가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-154">hello back-end server is marked down after hello consecutive probe failure count reaches hello unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="d595f-155">해결 방법</span><span class="sxs-lookup"><span data-stu-id="d595f-155">Solution</span></span>

* <span data-ttu-id="d595f-156">기본 사이트를 구성하고 127.0.0.1에서 수신 대기 중인지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-156">Ensure that a default site is configured and is listening at 127.0.0.1.</span></span>
* <span data-ttu-id="d595f-157">BackendHttpSetting 80 이외의 포트를 지정 하는 경우 hello 기본 사이트에 해당 포트에서 구성 된 toolisten 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-157">If BackendHttpSetting specifies a port other than 80, hello default site should be configured toolisten at that port.</span></span>
* <span data-ttu-id="d595f-158">hello 호출 toohttp://127.0.0.1:port 반환 해야 HTTP 결과 코드는 200 합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-158">hello call toohttp://127.0.0.1:port should return an HTTP result code of 200.</span></span> <span data-ttu-id="d595f-159">이 hello 30 초 제한 시간 내 반환 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-159">This should be returned within hello 30 sec time-out period.</span></span>
* <span data-ttu-id="d595f-160">구성 된 포트가 열려 있고 Azure 네트워크 보안 그룹 구성 된 hello 포트에서 들어오거나 나가는 트래픽을 차단 없거나 방화벽 규칙은 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-160">Ensure that port configured is open and that there are no firewall rules or Azure Network Security Groups, which block incoming or outgoing traffic on hello port configured.</span></span>
* <span data-ttu-id="d595f-161">Azure 클래식 Vm 이나 클라우드 서비스 공용 IP 또는 FQDN을 사용 하는 경우 해당 하는 hello 확인 [끝점](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-161">If Azure classic VMs or Cloud Service is used with FQDN or Public IP, ensure that hello corresponding [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) is opened.</span></span>
* <span data-ttu-id="d595f-162">Hello VM Azure Resource Manager를 통해 구성 된 응용 프로그램 게이트웨이 배포 하는 VNet hello 외부 경우 [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md) 구성 해야 tooallow 액세스 hello에 필요한 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-162">If hello VM is configured via Azure Resource Manager and is outside hello VNet where Application Gateway is deployed, [Network Security Group](../virtual-network/virtual-networks-nsg.md) must be configured tooallow access on hello desired port.</span></span>

## <a name="problems-with-custom-health-probe"></a><span data-ttu-id="d595f-163">사용자 지정 상태 검색의 문제</span><span class="sxs-lookup"><span data-stu-id="d595f-163">Problems with custom health probe</span></span>

### <a name="cause"></a><span data-ttu-id="d595f-164">원인</span><span class="sxs-lookup"><span data-stu-id="d595f-164">Cause</span></span>

<span data-ttu-id="d595f-165">사용자 지정 상태 검색이 허용 유연성이 toohello 기본 동작을 조사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-165">Custom health probes allow additional flexibility toohello default probing behavior.</span></span> <span data-ttu-id="d595f-166">사용자 지정 프로브를 사용할 경우 사용자는 hello 백 엔드 풀 인스턴스 비정상으로 표시 하기 전에 hello 프로브 간격, hello URL 및 경로 tootest 및 개수 실패 응답 tooaccept 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-166">When using custom probes, users can configure hello probe interval, hello URL, and path tootest, and how many failed responses tooaccept before marking hello back-end pool instance as unhealthy.</span></span> <span data-ttu-id="d595f-167">다음과 같은 추가 속성 hello 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-167">hello following additional properties are added.</span></span>

| <span data-ttu-id="d595f-168">프로브 속성</span><span class="sxs-lookup"><span data-stu-id="d595f-168">Probe property</span></span> | <span data-ttu-id="d595f-169">설명</span><span class="sxs-lookup"><span data-stu-id="d595f-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d595f-170">이름</span><span class="sxs-lookup"><span data-stu-id="d595f-170">Name</span></span> |<span data-ttu-id="d595f-171">Hello 검색의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-171">Name of hello probe.</span></span> <span data-ttu-id="d595f-172">이 이름은 백 엔드 HTTP 설정에 사용 되는 toorefer toohello 프로브입니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-172">This name is used toorefer toohello probe in back-end HTTP settings.</span></span> |
| <span data-ttu-id="d595f-173">프로토콜</span><span class="sxs-lookup"><span data-stu-id="d595f-173">Protocol</span></span> |<span data-ttu-id="d595f-174">프로토콜은 toosend hello 프로브를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-174">Protocol used toosend hello probe.</span></span> <span data-ttu-id="d595f-175">hello 백 엔드 HTTP 설정에 정의 된 hello 프로토콜을 사용 하는 hello 프로브</span><span class="sxs-lookup"><span data-stu-id="d595f-175">hello probe uses hello protocol defined in hello back-end HTTP settings</span></span> |
| <span data-ttu-id="d595f-176">호스트</span><span class="sxs-lookup"><span data-stu-id="d595f-176">Host</span></span> |<span data-ttu-id="d595f-177">호스트 이름 toosend hello 프로브</span><span class="sxs-lookup"><span data-stu-id="d595f-177">Host name toosend hello probe.</span></span> <span data-ttu-id="d595f-178">다중 사이트를 응용 프로그램 게이트웨이에 구성하는 경우에만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-178">Applicable only when multi-site is configured on Application Gateway.</span></span> <span data-ttu-id="d595f-179">VM 호스트 이름과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-179">This is different from VM host name.</span></span> |
| <span data-ttu-id="d595f-180">Path</span><span class="sxs-lookup"><span data-stu-id="d595f-180">Path</span></span> |<span data-ttu-id="d595f-181">Hello 프로브의 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-181">Relative path of hello probe.</span></span> <span data-ttu-id="d595f-182">hello 유효한 경로가에서 시작 하 고 '/'입니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-182">hello valid path starts from '/'.</span></span> <span data-ttu-id="d595f-183">hello 프로브 너무 보내집니다\<프로토콜\>://\<호스트\>:\<포트\>\<경로\></span><span class="sxs-lookup"><span data-stu-id="d595f-183">hello probe is sent too\<protocol\>://\<host\>:\<port\>\<path\></span></span> |
| <span data-ttu-id="d595f-184">간격</span><span class="sxs-lookup"><span data-stu-id="d595f-184">Interval</span></span> |<span data-ttu-id="d595f-185">프로브 간격(초).</span><span class="sxs-lookup"><span data-stu-id="d595f-185">Probe interval in seconds.</span></span> <span data-ttu-id="d595f-186">두 개의 연속 프로브 사이의 hello 시간 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-186">This is hello time interval between two consecutive probes.</span></span> |
| <span data-ttu-id="d595f-187">시간 제한</span><span class="sxs-lookup"><span data-stu-id="d595f-187">Time-out</span></span> |<span data-ttu-id="d595f-188">프로브 시간 제한(초)</span><span class="sxs-lookup"><span data-stu-id="d595f-188">Probe time-out in seconds.</span></span> <span data-ttu-id="d595f-189">이 시간 제한 기간 내에서 유효한 응답 받지 hello 프로브 실패로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-189">If a valid response is not received within this time-out period, hello probe is marked as failed.</span></span> |
| <span data-ttu-id="d595f-190">비정상 임계값</span><span class="sxs-lookup"><span data-stu-id="d595f-190">Unhealthy threshold</span></span> |<span data-ttu-id="d595f-191">프로브 재시도 횟수.</span><span class="sxs-lookup"><span data-stu-id="d595f-191">Probe retry count.</span></span> <span data-ttu-id="d595f-192">hello 연속 프로브 오류 발생 횟수 hello 비정상 임계값에 도달 하면 hello 백 엔드 서버가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-192">hello back-end server is marked down after hello consecutive probe failure count reaches hello unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="d595f-193">해결 방법</span><span class="sxs-lookup"><span data-stu-id="d595f-193">Solution</span></span>

<span data-ttu-id="d595f-194">Hello 테이블 앞으로 올바르게 구성 된 사용자 지정 상태 프로브 해당 hello 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-194">Validate that hello Custom Health Probe is configured correctly as hello preceding table.</span></span> <span data-ttu-id="d595f-195">또한 이전 toohello hello 다음 확인 문제 해결 단계:</span><span class="sxs-lookup"><span data-stu-id="d595f-195">In addition toohello preceding troubleshooting steps, also ensure hello following:</span></span>

* <span data-ttu-id="d595f-196">해당 hello 프로브 hello를 기준으로 올바르게 지정 되어 확인 [가이드](application-gateway-create-probe-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-196">Ensure that hello probe is correctly specified as per hello [guide](application-gateway-create-probe-ps.md).</span></span>
* <span data-ttu-id="d595f-197">응용 프로그램 게이트웨이 단일 사이트에 대해 구성 된 경우 기본 hello 호스트에서 이름은로 지정 해야 '127.0.0.1', 그렇지 않으면 사용자 지정 프로브를 구성 하지 않는 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-197">If Application Gateway is configured for a single site, by default hello Host name should be specified as '127.0.0.1', unless otherwise configured in custom probe.</span></span>
* <span data-ttu-id="d595f-198">호출 toohttp 확인: / /\<호스트\>:\<포트\>\<경로\> HTTP 결과 코드 200 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-198">Ensure that a call toohttp://\<host\>:\<port\>\<path\> returns an HTTP result code of 200.</span></span>
* <span data-ttu-id="d595f-199">제한 시간 간격과 UnhealtyThreshold hello 허용 가능한 범위 이내 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-199">Ensure that Interval, Time-out and UnhealtyThreshold are within hello acceptable ranges.</span></span>
* <span data-ttu-id="d595f-200">프로브는 HTTPS를 사용 하는 경우 해당 hello 백 엔드 서버 hello 백 엔드 서버 자체에 fallback 인증서를 구성 하 여 SNI 필요가 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-200">If using an HTTPS probe, make sure that hello backend server doesn't require SNI by configuring a fallback certificate on hello backend server itself.</span></span> 
* <span data-ttu-id="d595f-201">제한 시간 간격과 UnhealtyThreshold hello 허용 가능한 범위 이내 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-201">Ensure that Interval, Time-out, and UnhealtyThreshold are within hello acceptable ranges.</span></span>

## <a name="request-time-out"></a><span data-ttu-id="d595f-202">요청 시간 초과</span><span class="sxs-lookup"><span data-stu-id="d595f-202">Request time out</span></span>

### <a name="cause"></a><span data-ttu-id="d595f-203">원인</span><span class="sxs-lookup"><span data-stu-id="d595f-203">Cause</span></span>

<span data-ttu-id="d595f-204">사용자 요청을 받으면 응용 프로그램 게이트웨이 구성 hello 규칙 toohello 요청을 적용 하 고 tooa 백 엔드 풀 인스턴스 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-204">When a user request is received, Application Gateway applies hello configured rules toohello request and routes it tooa back-end pool instance.</span></span> <span data-ttu-id="d595f-205">구성 가능한 간격의 시간에 hello 백 엔드 인스턴스의 응답을에서 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-205">It waits for a configurable interval of time for a response from hello back-end instance.</span></span> <span data-ttu-id="d595f-206">기본적으로 이 간격은 **30초**입니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-206">By default, this interval is **30 seconds**.</span></span> <span data-ttu-id="d595f-207">Application Gateway가 이 간격에서 백 엔드 응용 프로그램의 응답을 수신하지 않으면 사용자 요청에 502 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-207">If Application Gateway does not receive a response from back-end application in this interval, user request would see a 502 error.</span></span>

### <a name="solution"></a><span data-ttu-id="d595f-208">해결 방법</span><span class="sxs-lookup"><span data-stu-id="d595f-208">Solution</span></span>

<span data-ttu-id="d595f-209">응용 프로그램 게이트웨이 사용 하면 사용자 tooconfigure이이 설정을 통해 BackendHttpSetting toodifferent 풀 적용 된 다음 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-209">Application Gateway allows users tooconfigure this setting via BackendHttpSetting, which can be then applied toodifferent pools.</span></span> <span data-ttu-id="d595f-210">다른 백 엔드 풀에서는 다른 BackendHttpSetting 및 다른 요청 시간 초과를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-210">Different back-end pools can have different BackendHttpSetting and hence different request time out configured.</span></span>

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a><span data-ttu-id="d595f-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d595f-211">Next steps</span></span>

<span data-ttu-id="d595f-212">Hello 앞의 단계 문제가 해결 되지 않으면 hello를 열고는 [지원 티켓](https://azure.microsoft.com/support/options/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d595f-212">If hello preceding steps do not resolve hello issue, open a [support ticket](https://azure.microsoft.com/support/options/).</span></span>

