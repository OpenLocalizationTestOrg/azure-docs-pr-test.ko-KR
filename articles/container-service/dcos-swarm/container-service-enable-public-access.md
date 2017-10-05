---
title: "Azure DC/OS 컨테이너 앱에 대한 액세스 허용 | Microsoft Docs"
description: "Azure Container Service에서 DC/OS 컨테이너에 대해 공용 액세스를 사용하도록 설정하는 방법입니다."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Docker, 컨테이너, 마이크로 서비스, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: c9ef5913859cf3a55a2de2107a9304f1d28a4829
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="enable-public-access-to-an-azure-container-service-application"></a><span data-ttu-id="89313-104">Azure Container Service 응용 프로그램에 공용 액세스를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="89313-104">Enable public access to an Azure Container Service application</span></span>
<span data-ttu-id="89313-105">ACS [공용 에이전트 풀](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) 의 모든 DC/OS 컨테이너가 인터넷에 자동으로 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="89313-105">Any DC/OS container in the ACS [public agent pool](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) is automatically exposed to the internet.</span></span> <span data-ttu-id="89313-106">기본적으로 포트 **80**, **443**, **8080**이 열리며 이러한 포트에서 수신 대기하는 모든 (공용) 컨테이너에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89313-106">By default, ports **80**, **443**, **8080** are opened, and any (public) container listening on those ports are accessible.</span></span> <span data-ttu-id="89313-107">이 문서에서는 Azure Container Service의 응용 프로그램에 대해 더 많은 포트를 여는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="89313-107">This article shows you how to open more ports for your applications in Azure Container Service.</span></span>

## <a name="open-a-port-portal"></a><span data-ttu-id="89313-108">포트 열기(포털)</span><span class="sxs-lookup"><span data-stu-id="89313-108">Open a port (portal)</span></span>
<span data-ttu-id="89313-109">먼저 원하는 포트를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89313-109">First, we need to open the port we want.</span></span>

1. <span data-ttu-id="89313-110">포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="89313-110">Log in to the portal.</span></span>
2. <span data-ttu-id="89313-111">Azure Container Service를 배포한 리소스 그룹을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="89313-111">Find the resource group that you deployed the Azure Container Service to.</span></span>
3. <span data-ttu-id="89313-112">에이전트 부하 분산 장치( **XXXX-agent-lb-XXXX**와 유사하게 이름 지정됨)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="89313-112">Select the agent load balancer (which is named similar to **XXXX-agent-lb-XXXX**).</span></span>
   
    ![Azure Container Service 부하 분산 장치](./media/container-service-enable-public-access/agent-load-balancer.png)
4. <span data-ttu-id="89313-114">**프로브**를 클릭한 후 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89313-114">Click **Probes** and then **Add**.</span></span>
   
    ![Azure Container Service 부하 분산 장치 프로브](./media/container-service-enable-public-access/add-probe.png)
5. <span data-ttu-id="89313-116">프로브 양식을 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89313-116">Fill out the probe form and click **OK**.</span></span>
   
   | <span data-ttu-id="89313-117">필드</span><span class="sxs-lookup"><span data-stu-id="89313-117">Field</span></span> | <span data-ttu-id="89313-118">설명</span><span class="sxs-lookup"><span data-stu-id="89313-118">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="89313-119">이름</span><span class="sxs-lookup"><span data-stu-id="89313-119">Name</span></span> |<span data-ttu-id="89313-120">프로브에 대한 설명이 포함된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="89313-120">A descriptive name of the probe.</span></span> |
   | <span data-ttu-id="89313-121">포트</span><span class="sxs-lookup"><span data-stu-id="89313-121">Port</span></span> |<span data-ttu-id="89313-122">테스트할 컨테이너의 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="89313-122">The port of the container to test.</span></span> |
   | <span data-ttu-id="89313-123">Path</span><span class="sxs-lookup"><span data-stu-id="89313-123">Path</span></span> |<span data-ttu-id="89313-124">(HTTP 모드에 있는 경우) 프로브에 대한 상대 웹 사이트 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="89313-124">(When in HTTP mode) The relative website path to probe.</span></span> <span data-ttu-id="89313-125">HTTPS는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89313-125">HTTPS not supported.</span></span> |
   | <span data-ttu-id="89313-126">간격</span><span class="sxs-lookup"><span data-stu-id="89313-126">Interval</span></span> |<span data-ttu-id="89313-127">프로브 시도 간격(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="89313-127">The amount of time between probe attempts, in seconds.</span></span> |
   | <span data-ttu-id="89313-128">비정상 임계값</span><span class="sxs-lookup"><span data-stu-id="89313-128">Unhealthy threshold</span></span> |<span data-ttu-id="89313-129">몇 번의 연속 프로브 시도 후 컨테이너를 비정상으로 간주할지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="89313-129">Number of consecutive probe attempts before considering the container unhealthy.</span></span> |
6. <span data-ttu-id="89313-130">에이전트 부하 분산 장치 속성으로 돌아가 **부하 분산 규칙**을 클릭한 후 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89313-130">Back at the properties of the agent load balancer, click **Load balancing rules** and then **Add**.</span></span>
   
    ![Azure Container Service 부하 분산 장치 규칙](./media/container-service-enable-public-access/add-balancer-rule.png)
7. <span data-ttu-id="89313-132">부하 분산 장치 양식을 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89313-132">Fill out the load balancer form and click **OK**.</span></span>
   
   | <span data-ttu-id="89313-133">필드</span><span class="sxs-lookup"><span data-stu-id="89313-133">Field</span></span> | <span data-ttu-id="89313-134">설명</span><span class="sxs-lookup"><span data-stu-id="89313-134">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="89313-135">이름</span><span class="sxs-lookup"><span data-stu-id="89313-135">Name</span></span> |<span data-ttu-id="89313-136">부하 분산 장치에 대한 설명이 포함된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="89313-136">A descriptive name of the load balancer.</span></span> |
   | <span data-ttu-id="89313-137">포트</span><span class="sxs-lookup"><span data-stu-id="89313-137">Port</span></span> |<span data-ttu-id="89313-138">공용 수신 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="89313-138">The public incoming port.</span></span> |
   | <span data-ttu-id="89313-139">백 엔드 포트</span><span class="sxs-lookup"><span data-stu-id="89313-139">Backend port</span></span> |<span data-ttu-id="89313-140">트래픽을 라우팅할 컨테이너의 내부 공용 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="89313-140">The internal-public port of the container to route traffic to.</span></span> |
   | <span data-ttu-id="89313-141">백 엔드 풀</span><span class="sxs-lookup"><span data-stu-id="89313-141">Backend pool</span></span> |<span data-ttu-id="89313-142">이 풀에 있는 컨테이너가 이 부하 분산 장치의 대상이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89313-142">The containers in this pool will be the target for this load balancer.</span></span> |
   | <span data-ttu-id="89313-143">프로브</span><span class="sxs-lookup"><span data-stu-id="89313-143">Probe</span></span> |<span data-ttu-id="89313-144">프로브는 **백 엔드 풀** 의 대상이 정상인지 확인하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="89313-144">The probe used to determine if a target in the **Backend pool** is healthy.</span></span> |
   | <span data-ttu-id="89313-145">세션 지속성</span><span class="sxs-lookup"><span data-stu-id="89313-145">Session persistence</span></span> |<span data-ttu-id="89313-146">세션 기간 동안 클라이언트의 트래픽을 처리하는 방식을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="89313-146">Determines how traffic from a client should be handled for the duration of the session.</span></span><br><br><span data-ttu-id="89313-147">**없음**: 동일한 클라이언트의 후속 요청은 컨테이너에 의해 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89313-147">**None**: Successive requests from the same client can be handled by any container.</span></span><br><span data-ttu-id="89313-148">**클라이언트 IP**: 동일한 클라이언트 IP의 후속 요청은 동일한 컨테이너에 의해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="89313-148">**Client IP**: Successive requests from the same client IP are handled by the same container.</span></span><br><span data-ttu-id="89313-149">**클라이언트 IP 및 프로토콜**: 동일한 클라이언트 IP 및 프로토콜 조합의 후속 요청은 동일한 컨테이너로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="89313-149">**Client IP and protocol**: Successive requests from the same client IP and protocol combination are handled by the same container.</span></span> |
   | <span data-ttu-id="89313-150">유휴 상태 시간 제한</span><span class="sxs-lookup"><span data-stu-id="89313-150">Idle timeout</span></span> |<span data-ttu-id="89313-151">(TCP 전용) *keep-alive* 메시지에 의존하지 않고 TCP/HTTP를 열기 상태로 유지하는 시간(분)입니다.</span><span class="sxs-lookup"><span data-stu-id="89313-151">(TCP only) In minutes, the time to keep a TCP/HTTP client open without relying on *keep-alive* messages.</span></span> |

## <a name="add-a-security-rule-portal"></a><span data-ttu-id="89313-152">보안 규칙 추가(포털)</span><span class="sxs-lookup"><span data-stu-id="89313-152">Add a security rule (portal)</span></span>
<span data-ttu-id="89313-153">다음으로, 트래픽을 열린 포트에서 방화벽을 통과하도록 라우팅하는 보안 규칙을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89313-153">Next, we need to add a security rule that routes traffic from our opened port through the firewall.</span></span>

1. <span data-ttu-id="89313-154">포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="89313-154">Log in to the portal.</span></span>
2. <span data-ttu-id="89313-155">Azure Container Service를 배포한 리소스 그룹을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="89313-155">Find the resource group that you deployed the Azure Container Service to.</span></span>
3. <span data-ttu-id="89313-156">**공용** 에이전트 네트워크 보안 그룹을 선택합니다(이름은 **XXXX-agent-public-nsg-XXXX**와 유사).</span><span class="sxs-lookup"><span data-stu-id="89313-156">Select the **public** agent network security group (which is named similar to **XXXX-agent-public-nsg-XXXX**).</span></span>
   
    ![Azure Container Service 네트워크 보안 그룹](./media/container-service-enable-public-access/agent-nsg.png)
4. <span data-ttu-id="89313-158">**인바운드 보안 규칙**을 선택한 후 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="89313-158">Select **Inbound security rules** and then **Add**.</span></span>
   
    ![Azure Container Service 네트워크 보안 그룹 규칙](./media/container-service-enable-public-access/add-firewall-rule.png)
5. <span data-ttu-id="89313-160">공용 포트를 허용하도록 방화벽 규칙을 채우고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="89313-160">Fill out the firewall rule to allow your public port and click **OK**.</span></span>
   
   | <span data-ttu-id="89313-161">필드</span><span class="sxs-lookup"><span data-stu-id="89313-161">Field</span></span> | <span data-ttu-id="89313-162">설명</span><span class="sxs-lookup"><span data-stu-id="89313-162">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="89313-163">이름</span><span class="sxs-lookup"><span data-stu-id="89313-163">Name</span></span> |<span data-ttu-id="89313-164">방화벽 규칙에 대한 설명이 포함된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="89313-164">A descriptive name of the firewall rule.</span></span> |
   | <span data-ttu-id="89313-165">우선 순위</span><span class="sxs-lookup"><span data-stu-id="89313-165">Priority</span></span> |<span data-ttu-id="89313-166">규칙에 대한 우선순위입니다.</span><span class="sxs-lookup"><span data-stu-id="89313-166">Priority rank for the rule.</span></span> <span data-ttu-id="89313-167">번호가 낮을수록 우선순위가 높습니다.</span><span class="sxs-lookup"><span data-stu-id="89313-167">The lower the number the higher the priority.</span></span> |
   | <span data-ttu-id="89313-168">원본</span><span class="sxs-lookup"><span data-stu-id="89313-168">Source</span></span> |<span data-ttu-id="89313-169">이 규칙에 의해 허용 또는 거부될 IP 주소 범위를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="89313-169">Restrict the incoming IP address range to be allowed or denied by this rule.</span></span> <span data-ttu-id="89313-170">제한을 지정하지 않으려면 **모두** 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="89313-170">Use **Any** to not specify a restriction.</span></span> |
   | <span data-ttu-id="89313-171">부여</span><span class="sxs-lookup"><span data-stu-id="89313-171">Service</span></span> |<span data-ttu-id="89313-172">이 보안 규칙을 위한 미리 정의된 서비스 집합을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="89313-172">Select a set of predefined services this security rule is for.</span></span> <span data-ttu-id="89313-173">그렇지 않으면 **사용자 지정** 을 사용하여 직접 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="89313-173">Otherwise use **Custom** to create your own.</span></span> |
   | <span data-ttu-id="89313-174">프로토콜</span><span class="sxs-lookup"><span data-stu-id="89313-174">Protocol</span></span> |<span data-ttu-id="89313-175">**TCP** 또는 **UDP**에 따라 트래픽을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="89313-175">Restrict traffic based on **TCP** or **UDP**.</span></span> <span data-ttu-id="89313-176">제한을 지정하지 않으려면 **모두** 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="89313-176">Use **Any** to not specify a restriction.</span></span> |
   | <span data-ttu-id="89313-177">포트 범위</span><span class="sxs-lookup"><span data-stu-id="89313-177">Port range</span></span> |<span data-ttu-id="89313-178">**서비스**가 **사용자 지정**인 경우 이 규칙의 영향을 받는 포트 범위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="89313-178">When **Service** is **Custom**, specifies the range of ports that this rule affects.</span></span> <span data-ttu-id="89313-179">**80**과 같은 단일 포트 또는 **1024-1500**과 같은 범위를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89313-179">You can use a single port, such as **80**, or a range like **1024-1500**.</span></span> |
   | <span data-ttu-id="89313-180">작업</span><span class="sxs-lookup"><span data-stu-id="89313-180">Action</span></span> |<span data-ttu-id="89313-181">조건과 일치하는 트래픽을 허용 또는 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="89313-181">Allow or deny traffic that meets the criteria.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="89313-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="89313-182">Next steps</span></span>
<span data-ttu-id="89313-183">[공용 및 개인 DC/OS 에이전트](container-service-dcos-agents.md)의 차이점에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="89313-183">Learn about the difference between [public and private DC/OS agents](container-service-dcos-agents.md).</span></span>

<span data-ttu-id="89313-184">[DC/OS 컨테이너 관리](container-service-mesos-marathon-ui.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="89313-184">Read more information about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

