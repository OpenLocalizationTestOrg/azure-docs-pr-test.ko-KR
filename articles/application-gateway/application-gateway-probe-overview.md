---
title: "Azure Application Gateway에 대한 상태 모니터링 개요 | Microsoft Docs"
description: "Azure 응용 프로그램 게이트웨이의 모니터링 기능에 대해 알아봅니다."
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7eeba328-bb2d-4d3e-bdac-7552e7900b7f
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 899115d213e626f17e58c2e5f01313f760f9e7f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="application-gateway-health-monitoring-overview"></a><span data-ttu-id="4f6f6-103">응용 프로그램 게이트웨이 상태 모니터링 개요</span><span class="sxs-lookup"><span data-stu-id="4f6f6-103">Application Gateway health monitoring overview</span></span>

<span data-ttu-id="4f6f6-104">Azure 응용 프로그램 게이트웨이는 기본적으로 백 엔드 풀의 모든 리소스 상태를 모니터링하고 풀에서 비정상으로 간주한 모든 리소스를 자동으로 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-104">Azure Application Gateway by default monitors the health of all resources in its back-end pool and automatically removes any resource considered unhealthy from the pool.</span></span> <span data-ttu-id="4f6f6-105">Application Gateway는 비정상 인스턴스를 계속 모니터링하며 사용할 수 있게 되고 상태 프로브에 응답하게 되면 정상 백 엔드 풀에 다시 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-105">Application Gateway continues to monitor the unhealthy instances and adds them back to the healthy back-end pool once they become available and respond to health probes.</span></span> <span data-ttu-id="4f6f6-106">응용 프로그램 게이트웨이에서 상태 프로브를 백 엔드 HTTP 설정에 정의된 동일한 포트와 함께 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-106">Application gateway sends the health probes with the same port that is defined in the back-end HTTP settings.</span></span> <span data-ttu-id="4f6f6-107">이 구성으로 프로브에서 사용자가 백 엔드에 연결하는 데 사용하는 것과 동일한 포트를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-107">This configuration ensures that the probe is testing the same port that customers would be using to connect to the backend.</span></span>

![Application Gateway 프로브 예제][1]

<span data-ttu-id="4f6f6-109">기본 상태 프로브 모니터링 사용 외에도 응용 프로그램의 요구 사항에 맞게 상태 프로브를 사용자 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-109">In addition to using default health probe monitoring, you can also customize the health probe to suit your application's requirements.</span></span> <span data-ttu-id="4f6f6-110">이 문서에서는 기본 및 사용자 지정 상태 프로브를 모두 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-110">In this article, both default and custom health probes are covered.</span></span>

> [!NOTE]
> <span data-ttu-id="4f6f6-111">Application Gateway 서브넷에 NSG가 있는 경우 인바운드 트래픽을 위해 Application Gateway 서브넷에서 포트 범위 65503-65534를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-111">If there is an NSG on Application Gateway subnet, port ranges 65503-65534 should be opened on the Application Gateway subnet for Inbound traffic.</span></span> <span data-ttu-id="4f6f6-112">이러한 포트는 백 엔드 상태 API가 제대로 작동하기 위해 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-112">These ports are required for the backend health API to work.</span></span>

## <a name="default-health-probe"></a><span data-ttu-id="4f6f6-113">기본 상태 프로브</span><span class="sxs-lookup"><span data-stu-id="4f6f6-113">Default health probe</span></span>

<span data-ttu-id="4f6f6-114">응용 프로그램 게이트웨이는 사용자 지정 프로브 구성을 설정하지 않는 경우 기본 상태 프로브를 자동으로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-114">An application gateway automatically configures a default health probe when you don't set up any custom probe configuration.</span></span> <span data-ttu-id="4f6f6-115">모니터링 동작은 백 엔드 풀에 대해 구성된 IP 주소에 대한 HTTP 요청을 만들어 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-115">The monitoring behavior works by making an HTTP request to the IP addresses configured for the back-end pool.</span></span> <span data-ttu-id="4f6f6-116">기본 프로브의 경우 백 엔드 http 설정이 HTTPS에 대해 구성되면 프로브는 HTTPS를 사용하고 백엔드의 상태를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-116">For default probes if the backend http settings are configured for HTTPS, the probe uses HTTPS as well to test health of the backends.</span></span>

<span data-ttu-id="4f6f6-117">예: 포트 80에서 HTTP 네트워크 트래픽을 수신할 백 엔드 서버 A, B, C를 사용하도록 응용 프로그램 게이트웨이를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-117">For example: You configure your application gateway to use back-end servers A, B, and C to receive HTTP network traffic on port 80.</span></span> <span data-ttu-id="4f6f6-118">기본 상태 모니터링은 정상 HTTP 응답에 대해 3개의 서버를 30초마다 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-118">The default health monitoring tests the three servers every 30 seconds for a healthy HTTP response.</span></span> <span data-ttu-id="4f6f6-119">정상 HTTP 응답은 [상태 코드](https://msdn.microsoft.com/library/aa287675.aspx) 200에서 399 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-119">A healthy HTTP response has a [status code](https://msdn.microsoft.com/library/aa287675.aspx) between 200 and 399.</span></span>

<span data-ttu-id="4f6f6-120">서버 A에 대한 기본 프로브 확인이 실패하면 응용 프로그램 게이트웨이가 백 엔드 풀에서 이를 제거하고 네트워크 트래픽이 이 서버로 이동되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-120">If the default probe check fails for server A, the application gateway removes it from its back-end pool, and network traffic stops flowing to this server.</span></span> <span data-ttu-id="4f6f6-121">기본 프로브는 서버 A에 대해 30초마다 계속 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-121">The default probe still continues to check for server A every 30 seconds.</span></span> <span data-ttu-id="4f6f6-122">서버 A가 기본 상태 프로브에서 하나의 요청에 대해 성공적으로 응답하는 경우 백 엔드 풀에 정상으로 다시 추가되고 트래픽이 이 서버로 다시 이동하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-122">When server A responds successfully to one request from a default health probe, it is added back as healthy to the back-end pool, and traffic starts flowing to the server again.</span></span>

### <a name="default-health-probe-settings"></a><span data-ttu-id="4f6f6-123">기본 상태 프로브 설정</span><span class="sxs-lookup"><span data-stu-id="4f6f6-123">Default health probe settings</span></span>

| <span data-ttu-id="4f6f6-124">프로브 속성</span><span class="sxs-lookup"><span data-stu-id="4f6f6-124">Probe property</span></span> | <span data-ttu-id="4f6f6-125">값</span><span class="sxs-lookup"><span data-stu-id="4f6f6-125">Value</span></span> | <span data-ttu-id="4f6f6-126">설명</span><span class="sxs-lookup"><span data-stu-id="4f6f6-126">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4f6f6-127">프로브 URL</span><span class="sxs-lookup"><span data-stu-id="4f6f6-127">Probe URL</span></span> |<span data-ttu-id="4f6f6-128">http://127.0.0.1:\<port\>/</span><span class="sxs-lookup"><span data-stu-id="4f6f6-128">http://127.0.0.1:\<port\>/</span></span> |<span data-ttu-id="4f6f6-129">URL 경로</span><span class="sxs-lookup"><span data-stu-id="4f6f6-129">URL path</span></span> |
| <span data-ttu-id="4f6f6-130">간격</span><span class="sxs-lookup"><span data-stu-id="4f6f6-130">Interval</span></span> |<span data-ttu-id="4f6f6-131">30</span><span class="sxs-lookup"><span data-stu-id="4f6f6-131">30</span></span> |<span data-ttu-id="4f6f6-132">프로브 간격(초)</span><span class="sxs-lookup"><span data-stu-id="4f6f6-132">Probe interval in seconds</span></span> |
| <span data-ttu-id="4f6f6-133">시간 제한</span><span class="sxs-lookup"><span data-stu-id="4f6f6-133">Time-out</span></span> |<span data-ttu-id="4f6f6-134">30</span><span class="sxs-lookup"><span data-stu-id="4f6f6-134">30</span></span> |<span data-ttu-id="4f6f6-135">프로브 시간 제한(초)</span><span class="sxs-lookup"><span data-stu-id="4f6f6-135">Probe time-out in seconds</span></span> |
| <span data-ttu-id="4f6f6-136">비정상 임계값</span><span class="sxs-lookup"><span data-stu-id="4f6f6-136">Unhealthy threshold</span></span> |<span data-ttu-id="4f6f6-137">3</span><span class="sxs-lookup"><span data-stu-id="4f6f6-137">3</span></span> |<span data-ttu-id="4f6f6-138">프로브 재시도 횟수.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-138">Probe retry count.</span></span> <span data-ttu-id="4f6f6-139">연속된 프로브 실패 횟수가 비정상 임계값에 도달하면 백 엔드 서버가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-139">The back-end server is marked down after the consecutive probe failure count reaches the unhealthy threshold.</span></span> |

> [!NOTE]
> <span data-ttu-id="4f6f6-140">포트는 백 엔드 HTTP 설정과 동일한 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-140">The port is the same port as the back-end HTTP settings.</span></span>

<span data-ttu-id="4f6f6-141">기본 프로브는 상태를 확인하는 데 http://127.0.0.1:\<port\>만 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-141">The default probe looks only at http://127.0.0.1:\<port\> to determine health status.</span></span> <span data-ttu-id="4f6f6-142">사용자 지정 URL로 이동하거나 다른 모든 설정을 수정하도록 상태 프로브를 구성하려면 다음 단계에 설명된 대로 사용자 지정 프로브를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-142">If you need to configure the health probe to go to a custom URL or modify any other settings, you must use custom probes as described in the following steps:</span></span>

## <a name="custom-health-probe"></a><span data-ttu-id="4f6f6-143">사용자 지정 상태 프로브</span><span class="sxs-lookup"><span data-stu-id="4f6f6-143">Custom health probe</span></span>

<span data-ttu-id="4f6f6-144">사용자 지정 프로브를 통해 상태 모니터링을 보다 세부적으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-144">Custom probes allow you to have a more granular control over the health monitoring.</span></span> <span data-ttu-id="4f6f6-145">사용자 지정 프로브를 사용하는 경우 프로브 간격, 테스트할 URL 및 경로, 백 엔드 풀 인스턴스를 비정상으로 표시하기 전에 허용할 실패 응답 횟수를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-145">When using custom probes, you can configure the probe interval, the URL and path to test, and how many failed responses to accept before marking the back-end pool instance as unhealthy.</span></span>

### <a name="custom-health-probe-settings"></a><span data-ttu-id="4f6f6-146">사용자 지정 상태 프로브 설정</span><span class="sxs-lookup"><span data-stu-id="4f6f6-146">Custom health probe settings</span></span>

<span data-ttu-id="4f6f6-147">다음 표에는 사용자 지정 상태 프로브의 속성을 위한 정의가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-147">The following table provides definitions for the properties of a custom health probe.</span></span>

| <span data-ttu-id="4f6f6-148">프로브 속성</span><span class="sxs-lookup"><span data-stu-id="4f6f6-148">Probe property</span></span> | <span data-ttu-id="4f6f6-149">설명</span><span class="sxs-lookup"><span data-stu-id="4f6f6-149">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4f6f6-150">Name</span><span class="sxs-lookup"><span data-stu-id="4f6f6-150">Name</span></span> |<span data-ttu-id="4f6f6-151">프로브 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-151">Name of the probe.</span></span> <span data-ttu-id="4f6f6-152">이 이름은 백 엔드 HTTP 설정에서 프로브를 참조하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-152">This name is used to refer to the probe in back-end HTTP settings.</span></span> |
| <span data-ttu-id="4f6f6-153">프로토콜</span><span class="sxs-lookup"><span data-stu-id="4f6f6-153">Protocol</span></span> |<span data-ttu-id="4f6f6-154">프로브를 보내는 데 사용하는 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-154">Protocol used to send the probe.</span></span> <span data-ttu-id="4f6f6-155">프로브는 백 엔드 HTTP 설정에 정의된 프로토콜을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-155">The probe uses the protocol defined in the back-end HTTP settings</span></span> |
| <span data-ttu-id="4f6f6-156">호스트</span><span class="sxs-lookup"><span data-stu-id="4f6f6-156">Host</span></span> |<span data-ttu-id="4f6f6-157">프로브에 보낼 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-157">Host name to send the probe.</span></span> <span data-ttu-id="4f6f6-158">다중 사이트를 Application Gateway에 구성하는 경우에만 적용할 수 있습니다. 그렇지 않으면 '127.0.0.1'을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-158">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span></span> <span data-ttu-id="4f6f6-159">이 값은 VM 호스트 이름과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-159">This value is different from VM host name.</span></span> |
| <span data-ttu-id="4f6f6-160">Path</span><span class="sxs-lookup"><span data-stu-id="4f6f6-160">Path</span></span> |<span data-ttu-id="4f6f6-161">프로브의 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-161">Relative path of the probe.</span></span> <span data-ttu-id="4f6f6-162">올바른 경로는 '/'부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-162">The valid path starts from '/'.</span></span> |
| <span data-ttu-id="4f6f6-163">간격</span><span class="sxs-lookup"><span data-stu-id="4f6f6-163">Interval</span></span> |<span data-ttu-id="4f6f6-164">프로브 간격(초).</span><span class="sxs-lookup"><span data-stu-id="4f6f6-164">Probe interval in seconds.</span></span> <span data-ttu-id="4f6f6-165">이 값은 연속된 두 프로브 사이의 시간 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-165">This value is the time interval between two consecutive probes.</span></span> |
| <span data-ttu-id="4f6f6-166">시간 제한</span><span class="sxs-lookup"><span data-stu-id="4f6f6-166">Time-out</span></span> |<span data-ttu-id="4f6f6-167">프로브 시간 제한(초)</span><span class="sxs-lookup"><span data-stu-id="4f6f6-167">Probe time-out in seconds.</span></span> <span data-ttu-id="4f6f6-168">이 시간 제한 기간 내에 올바른 응답을 받지 못하면 프로브는 실패로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-168">If a valid response is not received within this time-out period, the probe is marked as failed.</span></span>  |
| <span data-ttu-id="4f6f6-169">비정상 임계값</span><span class="sxs-lookup"><span data-stu-id="4f6f6-169">Unhealthy threshold</span></span> |<span data-ttu-id="4f6f6-170">프로브 재시도 횟수.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-170">Probe retry count.</span></span> <span data-ttu-id="4f6f6-171">연속된 프로브 실패 횟수가 비정상 임계값에 도달하면 백 엔드 서버가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-171">The back-end server is marked down after the consecutive probe failure count reaches the unhealthy threshold.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="4f6f6-172">응용 프로그램 게이트웨이가 단일 사이트에 대해 구성된 경우 기본적으로 호스트 이름은 '127.0.0.1'로 지정해야 합니다. 그렇지 않으면 사용자 지정 프로브에서 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-172">If Application Gateway is configured for a single site, by default the Host name should be specified as '127.0.0.1', unless otherwise configured in custom probe.</span></span>
> <span data-ttu-id="4f6f6-173">참고로 사용자 지정 프로브는 \<protocol\>://\<host\>:\<port\>\<path\>로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-173">For reference a custom probe is sent to \<protocol\>://\<host\>:\<port\>\<path\>.</span></span> <span data-ttu-id="4f6f6-174">사용된 포트는 항상 백 엔드 HTTP 설정에 정의된 것과 동일한 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-174">The port used will be the same port as defined in the back-end HTTP settings.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f6f6-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4f6f6-175">Next steps</span></span>
<span data-ttu-id="4f6f6-176">Application Gateway 상태 모니터링에 대해 알아본 후에 PowerShell 및 Azure Resource Manager 배포 모델을 사용하여 Azure Portal의 [사용자 지정 상태 프로브](application-gateway-create-probe-portal.md) 또는 [사용자 지정 상태 프로브](application-gateway-create-probe-ps.md)를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6f6-176">After learning about Application Gateway health monitoring, you can configure a [custom health probe](application-gateway-create-probe-portal.md) in the Azure portal or a [custom health probe](application-gateway-create-probe-ps.md) using PowerShell and the Azure Resource Manager deployment model.</span></span>

[1]: ./media/application-gateway-probe-overview/appgatewayprobe.png
