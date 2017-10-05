---
title: "Azure Application Gateway 502 잘못된 게이트웨이 오류 문제 해결 | Microsoft Docs"
description: "응용 프로그램 게이트웨이 502 오류를 해결하는 방법을 알아봅니다"
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
ms.openlocfilehash: cbf9c552c4818b3925f449081539f1db6d61918e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a><span data-ttu-id="00788-103">응용 프로그램 게이트웨이의 잘못된 게이트웨이 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="00788-103">Troubleshooting bad gateway errors in Application Gateway</span></span>

<span data-ttu-id="00788-104">응용 프로그램 게이트웨이를 사용할 때 받은 502 잘못된 게이트웨이 오류 문제를 해결하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="00788-104">Learn how to troubleshoot bad gateway (502) errors received when using application gateway.</span></span>

## <a name="overview"></a><span data-ttu-id="00788-105">개요</span><span class="sxs-lookup"><span data-stu-id="00788-105">Overview</span></span>

<span data-ttu-id="00788-106">응용 프로그램 게이트웨이를 구성한 후에 발생할 수 있는 오류 중 하나는 "서버 오류: 502 - 웹 서버가 게이트웨이 또는 프록시 서버 역할을 하는 동안 잘못된 응답을 받았습니다."입니다.</span><span class="sxs-lookup"><span data-stu-id="00788-106">After configuring an application gateway, one of the errors that users may encounter is "Server Error: 502 - Web server received an invalid response while acting as a gateway or proxy server".</span></span> <span data-ttu-id="00788-107">이 오류는 다음과 같은 주요 이유로 인해 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00788-107">This error may happen due to the following main reasons:</span></span>

* <span data-ttu-id="00788-108">Azure Application Gateway의 [백 엔드 풀은 구성되어 있지 않거나 비어 있습니다](#empty-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="00788-108">Azure Application Gateway's [back-end pool is not configured or empty](#empty-backendaddresspool).</span></span>
* <span data-ttu-id="00788-109">VM Scale Set의 VM 또는 인스턴스가 [모두 정상이 아닙니다](#unhealthy-instances-in-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="00788-109">None of the VMs or instances in [VM Scale Set are healthy](#unhealthy-instances-in-backendaddresspool).</span></span>
* <span data-ttu-id="00788-110">VM Scale Set의 백 엔드 VM 또는 인스턴스가 [기본 상태 프로브에 응답하지 않습니다](#problems-with-default-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="00788-110">Back-end VMs or instances of VM Scale Set are [not responding to the default health probe](#problems-with-default-health-probe.md).</span></span>
* <span data-ttu-id="00788-111">사용자 지정 상태 프로브의 구성이 [잘못되었거나 부적절합니다](#problems-with-custom-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="00788-111">Invalid or improper [configuration of custom health probes](#problems-with-custom-health-probe.md).</span></span>
* <span data-ttu-id="00788-112">사용자 요청과 관련된 [요청 시간 초과 또는 연결 문제입니다](#request-time-out).</span><span class="sxs-lookup"><span data-stu-id="00788-112">[Request time out or connectivity issues](#request-time-out) with user requests.</span></span>

## <a name="empty-backendaddresspool"></a><span data-ttu-id="00788-113">비어 있는 BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="00788-113">Empty BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="00788-114">원인</span><span class="sxs-lookup"><span data-stu-id="00788-114">Cause</span></span>

<span data-ttu-id="00788-115">Application Gateway에 백 엔드 주소 풀에 구성된 VM 또는 VM 크기 조정 설정이 없는 경우 고객의 요청을 라우팅할 수 없고 잘못된 게이트웨이 오류를 throw할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="00788-115">If the Application Gateway has no VMs or VM Scale Set configured in the back-end address pool, it cannot route any customer request and throws a bad gateway error.</span></span>

### <a name="solution"></a><span data-ttu-id="00788-116">해결 방법</span><span class="sxs-lookup"><span data-stu-id="00788-116">Solution</span></span>

<span data-ttu-id="00788-117">백 엔드 주소 풀이 비어 있지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-117">Ensure that the back-end address pool is not empty.</span></span> <span data-ttu-id="00788-118">PowerShell, CLI 또는 포털을 통해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00788-118">This can be done either via PowerShell, CLI, or portal.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

<span data-ttu-id="00788-119">앞의 cmdlet에서 출력은 비어 있지 않은 백 엔드 주소 풀을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-119">The output from the preceding cmdlet should contain non-empty back-end address pool.</span></span> <span data-ttu-id="00788-120">다음은 백 엔드 VM에 대한 FQDN 또는 IP 주소로 구성된 두 개의 풀을 반환하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="00788-120">Following is an example where two pools are returned which are configured with FQDN or IP addresses for backend VMs.</span></span> <span data-ttu-id="00788-121">BackendAddressPool의 상태를 프로비전하는 작업은 '성공'해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-121">The provisioning state of the BackendAddressPool must be 'Succeeded'.</span></span>

<span data-ttu-id="00788-122">BackendAddressPoolsText:</span><span class="sxs-lookup"><span data-stu-id="00788-122">BackendAddressPoolsText:</span></span>

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

## <a name="unhealthy-instances-in-backendaddresspool"></a><span data-ttu-id="00788-123">BackendAddressPool의 비정상 인스턴스</span><span class="sxs-lookup"><span data-stu-id="00788-123">Unhealthy instances in BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="00788-124">원인</span><span class="sxs-lookup"><span data-stu-id="00788-124">Cause</span></span>

<span data-ttu-id="00788-125">BackendAddressPool의 모든 인스턴스가 정상이 아닌 경우 Application Gateway에는 사용자 요청을 라우팅할 백 엔드가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="00788-125">If all the instances of BackendAddressPool are unhealthy, then Application Gateway would not have any back-end to route user request to.</span></span> <span data-ttu-id="00788-126">백 엔드 인스턴스가 정상이지만 필요한 응용 프로그램이 배포되지 않은 경우일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00788-126">This could also be the case when back-end instances are healthy but do not have the required application deployed.</span></span>

### <a name="solution"></a><span data-ttu-id="00788-127">해결 방법</span><span class="sxs-lookup"><span data-stu-id="00788-127">Solution</span></span>

<span data-ttu-id="00788-128">인스턴스가 정상이고 응용 프로그램이 올바르게 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-128">Ensure that the instances are healthy and the application is properly configured.</span></span> <span data-ttu-id="00788-129">백 엔드 인스턴스가 동일한 VNet의 다른 VM에서 ping에 응답할 수 있는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-129">Check if the back-end instances are able to respond to a ping from another VM in the same VNet.</span></span> <span data-ttu-id="00788-130">공용 끝점으로 구성된 경우 웹 응용 프로그램에 대한 브라우저 요청을 서비스할 수 있는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-130">If configured with a public end point, ensure that a browser request to the web application is serviceable.</span></span>

## <a name="problems-with-default-health-probe"></a><span data-ttu-id="00788-131">기본 상태 검색의 문제</span><span class="sxs-lookup"><span data-stu-id="00788-131">Problems with default health probe</span></span>

### <a name="cause"></a><span data-ttu-id="00788-132">원인</span><span class="sxs-lookup"><span data-stu-id="00788-132">Cause</span></span>

<span data-ttu-id="00788-133">502 오류는 종종 기본 상태 프로브가 백 엔드 VM에 연결할 수 없다는 지표일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00788-133">502 errors can also be frequent indicators that the default health probe is not able to reach back-end VMs.</span></span> <span data-ttu-id="00788-134">응용 프로그램 게이트웨이 인스턴스를 프로비전할 경우 BackendHttpSetting의 속성을 사용하여 각 BackendAddressPool에 대한 기본 상태 프로브를 자동으로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-134">When an Application Gateway instance is provisioned, it automatically configures a default health probe to each BackendAddressPool using properties of the BackendHttpSetting.</span></span> <span data-ttu-id="00788-135">이 프로브를 설정하기 위해 사용자 입력이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00788-135">No user input is required to set this probe.</span></span> <span data-ttu-id="00788-136">특히, 부하 분산 규칙을 구성한 경우 BackendHttpSetting와 BackendAddressPool 간에 연결이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="00788-136">Specifically, when a load balancing rule is configured, an association is made between a BackendHttpSetting and BackendAddressPool.</span></span> <span data-ttu-id="00788-137">기본 검색이 다음 연결 각각에 대해 구성되고 응용 프로그램 게이트웨이가 BackendHttpSetting 요소에 지정된 포트에서 BackendAddressPool의 각 인스턴스에 대한 정기 상태 검사 연결을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-137">A default probe is configured for each of these associations and Application Gateway initiates a periodic health check connection to each instance in the BackendAddressPool at the port specified in the BackendHttpSetting element.</span></span> <span data-ttu-id="00788-138">다음 테이블에서는 기본 상태 프로브로 연결된 값을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-138">Following table lists the values associated with the default health probe.</span></span>

| <span data-ttu-id="00788-139">프로브 속성</span><span class="sxs-lookup"><span data-stu-id="00788-139">Probe property</span></span> | <span data-ttu-id="00788-140">값</span><span class="sxs-lookup"><span data-stu-id="00788-140">Value</span></span> | <span data-ttu-id="00788-141">설명</span><span class="sxs-lookup"><span data-stu-id="00788-141">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="00788-142">프로브 URL</span><span class="sxs-lookup"><span data-stu-id="00788-142">Probe URL</span></span> |<span data-ttu-id="00788-143">http://127.0.0.1/</span><span class="sxs-lookup"><span data-stu-id="00788-143">http://127.0.0.1/</span></span> |<span data-ttu-id="00788-144">URL 경로</span><span class="sxs-lookup"><span data-stu-id="00788-144">URL path</span></span> |
| <span data-ttu-id="00788-145">간격</span><span class="sxs-lookup"><span data-stu-id="00788-145">Interval</span></span> |<span data-ttu-id="00788-146">30</span><span class="sxs-lookup"><span data-stu-id="00788-146">30</span></span> |<span data-ttu-id="00788-147">프로브 간격(초)</span><span class="sxs-lookup"><span data-stu-id="00788-147">Probe interval in seconds</span></span> |
| <span data-ttu-id="00788-148">시간 제한</span><span class="sxs-lookup"><span data-stu-id="00788-148">Time-out</span></span> |<span data-ttu-id="00788-149">30</span><span class="sxs-lookup"><span data-stu-id="00788-149">30</span></span> |<span data-ttu-id="00788-150">프로브 시간 제한(초)</span><span class="sxs-lookup"><span data-stu-id="00788-150">Probe time-out in seconds</span></span> |
| <span data-ttu-id="00788-151">비정상 임계값</span><span class="sxs-lookup"><span data-stu-id="00788-151">Unhealthy threshold</span></span> |<span data-ttu-id="00788-152">3</span><span class="sxs-lookup"><span data-stu-id="00788-152">3</span></span> |<span data-ttu-id="00788-153">프로브 재시도 횟수.</span><span class="sxs-lookup"><span data-stu-id="00788-153">Probe retry count.</span></span> <span data-ttu-id="00788-154">연속된 프로브 실패 횟수가 비정상 임계값에 도달하면 백 엔드 서버가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00788-154">The back-end server is marked down after the consecutive probe failure count reaches the unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="00788-155">해결 방법</span><span class="sxs-lookup"><span data-stu-id="00788-155">Solution</span></span>

* <span data-ttu-id="00788-156">기본 사이트를 구성하고 127.0.0.1에서 수신 대기 중인지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-156">Ensure that a default site is configured and is listening at 127.0.0.1.</span></span>
* <span data-ttu-id="00788-157">BackendHttpSetting이 포트 80이 아닌 다른 포트를 지정하는 경우 기본 사이트는 해당 포트에서 수신하도록 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-157">If BackendHttpSetting specifies a port other than 80, the default site should be configured to listen at that port.</span></span>
* <span data-ttu-id="00788-158">http://127.0.0.1:port에 대한 호출은 HTTP 결과 코드 200을 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-158">The call to http://127.0.0.1:port should return an HTTP result code of 200.</span></span> <span data-ttu-id="00788-159">30초 제한 시간 내에 반환되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-159">This should be returned within the 30 sec time-out period.</span></span>
* <span data-ttu-id="00788-160">구성된 포트가 열려 있고 방화벽 규칙 또는 Azure 네트워크 보안 그룹이 없는지를 확인합니다. 여기서 구성된 포트에서 들어오거나 나가는 트래픽을 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-160">Ensure that port configured is open and that there are no firewall rules or Azure Network Security Groups, which block incoming or outgoing traffic on the port configured.</span></span>
* <span data-ttu-id="00788-161">Azure 클래식 VM 또는 클라우드 서비스를 FQDN 또는 공용 IP와 사용하는 경우 해당 [끝점](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) 이 열려 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-161">If Azure classic VMs or Cloud Service is used with FQDN or Public IP, ensure that the corresponding [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) is opened.</span></span>
* <span data-ttu-id="00788-162">VM이 Azure Resource Manager를 통해 구성되고 응용 프로그램 게이트웨이가 배포된 VNet의 외부에 있는 경우 [네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md) 을 원하는 포트에 대한 액세스를 허용하도록 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-162">If the VM is configured via Azure Resource Manager and is outside the VNet where Application Gateway is deployed, [Network Security Group](../virtual-network/virtual-networks-nsg.md) must be configured to allow access on the desired port.</span></span>

## <a name="problems-with-custom-health-probe"></a><span data-ttu-id="00788-163">사용자 지정 상태 검색의 문제</span><span class="sxs-lookup"><span data-stu-id="00788-163">Problems with custom health probe</span></span>

### <a name="cause"></a><span data-ttu-id="00788-164">원인</span><span class="sxs-lookup"><span data-stu-id="00788-164">Cause</span></span>

<span data-ttu-id="00788-165">사용자 지정 상태 프로브를 사용하면 기본 검사 동작에 추가적인 유연성을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00788-165">Custom health probes allow additional flexibility to the default probing behavior.</span></span> <span data-ttu-id="00788-166">사용자 지정 프로브를 사용하는 경우 사용자는 프로브 간격, 테스트할 URL 및 경로, 백 엔드 풀 인스턴스를 비정상으로 표시하기 전에 허용할 실패 응답 횟수를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00788-166">When using custom probes, users can configure the probe interval, the URL, and path to test, and how many failed responses to accept before marking the back-end pool instance as unhealthy.</span></span> <span data-ttu-id="00788-167">다음과 같은 추가 속성이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="00788-167">The following additional properties are added.</span></span>

| <span data-ttu-id="00788-168">프로브 속성</span><span class="sxs-lookup"><span data-stu-id="00788-168">Probe property</span></span> | <span data-ttu-id="00788-169">설명</span><span class="sxs-lookup"><span data-stu-id="00788-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="00788-170">Name</span><span class="sxs-lookup"><span data-stu-id="00788-170">Name</span></span> |<span data-ttu-id="00788-171">프로브 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="00788-171">Name of the probe.</span></span> <span data-ttu-id="00788-172">이 이름은 백 엔드 HTTP 설정에서 프로브를 참조하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="00788-172">This name is used to refer to the probe in back-end HTTP settings.</span></span> |
| <span data-ttu-id="00788-173">프로토콜</span><span class="sxs-lookup"><span data-stu-id="00788-173">Protocol</span></span> |<span data-ttu-id="00788-174">프로브를 보내는 데 사용하는 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="00788-174">Protocol used to send the probe.</span></span> <span data-ttu-id="00788-175">프로브는 백 엔드 HTTP 설정에 정의된 프로토콜을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-175">The probe uses the protocol defined in the back-end HTTP settings</span></span> |
| <span data-ttu-id="00788-176">호스트</span><span class="sxs-lookup"><span data-stu-id="00788-176">Host</span></span> |<span data-ttu-id="00788-177">프로브에 보낼 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="00788-177">Host name to send the probe.</span></span> <span data-ttu-id="00788-178">다중 사이트를 응용 프로그램 게이트웨이에 구성하는 경우에만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00788-178">Applicable only when multi-site is configured on Application Gateway.</span></span> <span data-ttu-id="00788-179">VM 호스트 이름과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="00788-179">This is different from VM host name.</span></span> |
| <span data-ttu-id="00788-180">Path</span><span class="sxs-lookup"><span data-stu-id="00788-180">Path</span></span> |<span data-ttu-id="00788-181">프로브의 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="00788-181">Relative path of the probe.</span></span> <span data-ttu-id="00788-182">올바른 경로는 '/'부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-182">The valid path starts from '/'.</span></span> <span data-ttu-id="00788-183">프로브는 \<protocol\>://\<host\>:\<port\>\<path\>로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="00788-183">The probe is sent to \<protocol\>://\<host\>:\<port\>\<path\></span></span> |
| <span data-ttu-id="00788-184">간격</span><span class="sxs-lookup"><span data-stu-id="00788-184">Interval</span></span> |<span data-ttu-id="00788-185">프로브 간격(초).</span><span class="sxs-lookup"><span data-stu-id="00788-185">Probe interval in seconds.</span></span> <span data-ttu-id="00788-186">연속된 두 프로브 사이의 시간 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="00788-186">This is the time interval between two consecutive probes.</span></span> |
| <span data-ttu-id="00788-187">시간 제한</span><span class="sxs-lookup"><span data-stu-id="00788-187">Time-out</span></span> |<span data-ttu-id="00788-188">프로브 시간 제한(초)</span><span class="sxs-lookup"><span data-stu-id="00788-188">Probe time-out in seconds.</span></span> <span data-ttu-id="00788-189">이 시간 제한 기간 내에 올바른 응답을 받지 못하면 프로브는 실패로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00788-189">If a valid response is not received within this time-out period, the probe is marked as failed.</span></span> |
| <span data-ttu-id="00788-190">비정상 임계값</span><span class="sxs-lookup"><span data-stu-id="00788-190">Unhealthy threshold</span></span> |<span data-ttu-id="00788-191">프로브 재시도 횟수.</span><span class="sxs-lookup"><span data-stu-id="00788-191">Probe retry count.</span></span> <span data-ttu-id="00788-192">연속된 프로브 실패 횟수가 비정상 임계값에 도달하면 백 엔드 서버가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00788-192">The back-end server is marked down after the consecutive probe failure count reaches the unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="00788-193">해결 방법</span><span class="sxs-lookup"><span data-stu-id="00788-193">Solution</span></span>

<span data-ttu-id="00788-194">앞의 테이블처럼 사용자 지정 상태 프로브를 올바르게 구성했는지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-194">Validate that the Custom Health Probe is configured correctly as the preceding table.</span></span> <span data-ttu-id="00788-195">앞의 문제 해결 단계 외에도 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-195">In addition to the preceding troubleshooting steps, also ensure the following:</span></span>

* <span data-ttu-id="00788-196">프로브가 [가이드](application-gateway-create-probe-ps.md)를 기준으로 올바르게 지정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-196">Ensure that the probe is correctly specified as per the [guide](application-gateway-create-probe-ps.md).</span></span>
* <span data-ttu-id="00788-197">응용 프로그램 게이트웨이가 단일 사이트에 대해 구성된 경우 기본적으로 호스트 이름은 '127.0.0.1'로 지정해야 합니다. 그렇지 않으면 사용자 지정 프로브에서 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-197">If Application Gateway is configured for a single site, by default the Host name should be specified as '127.0.0.1', unless otherwise configured in custom probe.</span></span>
* <span data-ttu-id="00788-198">http://\<host\>:\<port\>\<path\>에 대한 호출은 HTTP 결과 코드 200을 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-198">Ensure that a call to http://\<host\>:\<port\>\<path\> returns an HTTP result code of 200.</span></span>
* <span data-ttu-id="00788-199">간격, 제한 시간 및 UnhealtyThreshold이 허용 가능한 범위 내에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-199">Ensure that Interval, Time-out and UnhealtyThreshold are within the acceptable ranges.</span></span>
* <span data-ttu-id="00788-200">HTTPS 프로브를 사용하는 경우 백 엔드 서버 자체에서 대체(fallback) 인증서를 구성하여 백 엔드 서버에 SNI가 필요하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-200">If using an HTTPS probe, make sure that the backend server doesn't require SNI by configuring a fallback certificate on the backend server itself.</span></span> 
* <span data-ttu-id="00788-201">간격, 제한 시간 및 UnhealtyThreshold이 허용 가능한 범위 내에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-201">Ensure that Interval, Time-out, and UnhealtyThreshold are within the acceptable ranges.</span></span>

## <a name="request-time-out"></a><span data-ttu-id="00788-202">요청 시간 초과</span><span class="sxs-lookup"><span data-stu-id="00788-202">Request time out</span></span>

### <a name="cause"></a><span data-ttu-id="00788-203">원인</span><span class="sxs-lookup"><span data-stu-id="00788-203">Cause</span></span>

<span data-ttu-id="00788-204">사용자 요청이 수신되면 Application Gateway가 요청에 구성된 규칙을 적용하고 백 엔드 풀 인스턴스를 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="00788-204">When a user request is received, Application Gateway applies the configured rules to the request and routes it to a back-end pool instance.</span></span> <span data-ttu-id="00788-205">백 엔드 인스턴스의 응답에 대해 구성 가능한 시간 간격을 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="00788-205">It waits for a configurable interval of time for a response from the back-end instance.</span></span> <span data-ttu-id="00788-206">기본적으로 이 간격은 **30초**입니다.</span><span class="sxs-lookup"><span data-stu-id="00788-206">By default, this interval is **30 seconds**.</span></span> <span data-ttu-id="00788-207">Application Gateway가 이 간격에서 백 엔드 응용 프로그램의 응답을 수신하지 않으면 사용자 요청에 502 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00788-207">If Application Gateway does not receive a response from back-end application in this interval, user request would see a 502 error.</span></span>

### <a name="solution"></a><span data-ttu-id="00788-208">해결 방법</span><span class="sxs-lookup"><span data-stu-id="00788-208">Solution</span></span>

<span data-ttu-id="00788-209">Application Gateway를 사용하면 사용자가 다른 풀에 적용할 수 있는 BackendHttpSetting을 통해 이 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00788-209">Application Gateway allows users to configure this setting via BackendHttpSetting, which can be then applied to different pools.</span></span> <span data-ttu-id="00788-210">다른 백 엔드 풀에서는 다른 BackendHttpSetting 및 다른 요청 시간 초과를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00788-210">Different back-end pools can have different BackendHttpSetting and hence different request time out configured.</span></span>

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a><span data-ttu-id="00788-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="00788-211">Next steps</span></span>

<span data-ttu-id="00788-212">앞의 단계에서 문제가 해결되지 않으면 [지원 티켓](https://azure.microsoft.com/support/options/)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="00788-212">If the preceding steps do not resolve the issue, open a [support ticket](https://azure.microsoft.com/support/options/).</span></span>

