---
title: "DC/OS 컨테이너 응용 프로그램 aaaEnable 액세스 tooAzure | Microsoft Docs"
description: "Tooenable 공용 tooDC/OS 컨테이너 Azure 컨테이너 서비스에 액세스 하는 방법입니다."
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
ms.openlocfilehash: 1ba251ba5a176a6a5e1c7831655164e380a62b27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-public-access-tooan-azure-container-service-application"></a><span data-ttu-id="183af-104">공용 액세스 tooan Azure 컨테이너 서비스 응용 프로그램을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="183af-104">Enable public access tooan Azure Container Service application</span></span>
<span data-ttu-id="183af-105">Hello ACS의에서 모든 DC/OS 컨테이너 [공용 에이전트 풀](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) 은 자동으로 노출 된 toohello 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-105">Any DC/OS container in hello ACS [public agent pool](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) is automatically exposed toohello internet.</span></span> <span data-ttu-id="183af-106">기본적으로 포트 **80**, **443**, **8080**이 열리며 이러한 포트에서 수신 대기하는 모든 (공용) 컨테이너에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="183af-106">By default, ports **80**, **443**, **8080** are opened, and any (public) container listening on those ports are accessible.</span></span> <span data-ttu-id="183af-107">이 문서에서는 tooopen Azure 컨테이너 서비스에서 응용 프로그램에 더 포트 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-107">This article shows you how tooopen more ports for your applications in Azure Container Service.</span></span>

## <a name="open-a-port-portal"></a><span data-ttu-id="183af-108">포트 열기(포털)</span><span class="sxs-lookup"><span data-stu-id="183af-108">Open a port (portal)</span></span>
<span data-ttu-id="183af-109">먼저 tooopen hello 포트 주시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="183af-109">First, we need tooopen hello port we want.</span></span>

1. <span data-ttu-id="183af-110">Toohello 포털에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-110">Log in toohello portal.</span></span>
2. <span data-ttu-id="183af-111">찾기 hello 리소스 그룹 배포 된 hello Azure 컨테이너 서비스를 합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-111">Find hello resource group that you deployed hello Azure Container Service to.</span></span>
3. <span data-ttu-id="183af-112">Hello 에이전트에 대 한 부하 분산 장치를 선택 (라는 비슷한 너무**XXXX 에이전트-lb XXXX**).</span><span class="sxs-lookup"><span data-stu-id="183af-112">Select hello agent load balancer (which is named similar too**XXXX-agent-lb-XXXX**).</span></span>
   
    ![Azure Container Service 부하 분산 장치](./media/container-service-enable-public-access/agent-load-balancer.png)
4. <span data-ttu-id="183af-114">**프로브**를 클릭한 후 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-114">Click **Probes** and then **Add**.</span></span>
   
    ![Azure Container Service 부하 분산 장치 프로브](./media/container-service-enable-public-access/add-probe.png)
5. <span data-ttu-id="183af-116">Hello 프로브 양식을 작성 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-116">Fill out hello probe form and click **OK**.</span></span>
   
   | <span data-ttu-id="183af-117">필드</span><span class="sxs-lookup"><span data-stu-id="183af-117">Field</span></span> | <span data-ttu-id="183af-118">설명</span><span class="sxs-lookup"><span data-stu-id="183af-118">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="183af-119">이름</span><span class="sxs-lookup"><span data-stu-id="183af-119">Name</span></span> |<span data-ttu-id="183af-120">Hello 프로브의 설명이 포함 된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="183af-120">A descriptive name of hello probe.</span></span> |
   | <span data-ttu-id="183af-121">포트</span><span class="sxs-lookup"><span data-stu-id="183af-121">Port</span></span> |<span data-ttu-id="183af-122">hello 컨테이너 tootest의 hello 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="183af-122">hello port of hello container tootest.</span></span> |
   | <span data-ttu-id="183af-123">Path</span><span class="sxs-lookup"><span data-stu-id="183af-123">Path</span></span> |<span data-ttu-id="183af-124">(HTTP 모드의 경우) 상대 웹 사이트 경로 tooprobe hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-124">(When in HTTP mode) hello relative website path tooprobe.</span></span> <span data-ttu-id="183af-125">HTTPS는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="183af-125">HTTPS not supported.</span></span> |
   | <span data-ttu-id="183af-126">간격</span><span class="sxs-lookup"><span data-stu-id="183af-126">Interval</span></span> |<span data-ttu-id="183af-127">hello 프로브 시간 간격 (초)에서 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-127">hello amount of time between probe attempts, in seconds.</span></span> |
   | <span data-ttu-id="183af-128">비정상 임계값</span><span class="sxs-lookup"><span data-stu-id="183af-128">Unhealthy threshold</span></span> |<span data-ttu-id="183af-129">Hello 컨테이너를 비정상으로 간주 되기 전에 시도 하는 연속 프로브 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="183af-129">Number of consecutive probe attempts before considering hello container unhealthy.</span></span> |
6. <span data-ttu-id="183af-130">Hello 속성 hello 에이전트에 대 한 부하 분산 장치에서 다시 **부하 분산 규칙** 차례로 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-130">Back at hello properties of hello agent load balancer, click **Load balancing rules** and then **Add**.</span></span>
   
    ![Azure Container Service 부하 분산 장치 규칙](./media/container-service-enable-public-access/add-balancer-rule.png)
7. <span data-ttu-id="183af-132">Hello 부하 분산 장치 양식을 작성 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-132">Fill out hello load balancer form and click **OK**.</span></span>
   
   | <span data-ttu-id="183af-133">필드</span><span class="sxs-lookup"><span data-stu-id="183af-133">Field</span></span> | <span data-ttu-id="183af-134">설명</span><span class="sxs-lookup"><span data-stu-id="183af-134">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="183af-135">이름</span><span class="sxs-lookup"><span data-stu-id="183af-135">Name</span></span> |<span data-ttu-id="183af-136">부하 분산 장치 hello의 설명이 포함 된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="183af-136">A descriptive name of hello load balancer.</span></span> |
   | <span data-ttu-id="183af-137">포트</span><span class="sxs-lookup"><span data-stu-id="183af-137">Port</span></span> |<span data-ttu-id="183af-138">hello 공용 수신 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="183af-138">hello public incoming port.</span></span> |
   | <span data-ttu-id="183af-139">백 엔드 포트</span><span class="sxs-lookup"><span data-stu-id="183af-139">Backend port</span></span> |<span data-ttu-id="183af-140">hello 컨테이너 tooroute 트래픽을 hello public이 내부 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="183af-140">hello internal-public port of hello container tooroute traffic to.</span></span> |
   | <span data-ttu-id="183af-141">백 엔드 풀</span><span class="sxs-lookup"><span data-stu-id="183af-141">Backend pool</span></span> |<span data-ttu-id="183af-142">이 풀에 있는 hello 컨테이너에는이 부하 분산 장치에 대 한 hello 대상이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="183af-142">hello containers in this pool will be hello target for this load balancer.</span></span> |
   | <span data-ttu-id="183af-143">프로브</span><span class="sxs-lookup"><span data-stu-id="183af-143">Probe</span></span> |<span data-ttu-id="183af-144">경우 hello에 대상을 사용 하는 프로브 toodetermine hello **백 엔드 풀** 정상입니다.</span><span class="sxs-lookup"><span data-stu-id="183af-144">hello probe used toodetermine if a target in hello **Backend pool** is healthy.</span></span> |
   | <span data-ttu-id="183af-145">세션 지속성</span><span class="sxs-lookup"><span data-stu-id="183af-145">Session persistence</span></span> |<span data-ttu-id="183af-146">Hello hello 세션 기간에 대 한 클라이언트의 트래픽을 처리 되는 방법을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-146">Determines how traffic from a client should be handled for hello duration of hello session.</span></span><br><br><span data-ttu-id="183af-147">**None**: 연속 요청만 hello 동일한 클라이언트 모든 컨테이너에 의해 처리 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="183af-147">**None**: Successive requests from hello same client can be handled by any container.</span></span><br><span data-ttu-id="183af-148">**클라이언트 IP**: 동일한 컨테이너를 hello 연속 요청만 hello 동일한 클라이언트 IP에 의해 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="183af-148">**Client IP**: Successive requests from hello same client IP are handled by hello same container.</span></span><br><span data-ttu-id="183af-149">**클라이언트 IP 및 프로토콜**: 동일한 컨테이너를 hello 연속 요청만 hello 동일한 클라이언트 IP 및 프로토콜 조합에 의해 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="183af-149">**Client IP and protocol**: Successive requests from hello same client IP and protocol combination are handled by hello same container.</span></span> |
   | <span data-ttu-id="183af-150">유휴 상태 시간 제한</span><span class="sxs-lookup"><span data-stu-id="183af-150">Idle timeout</span></span> |<span data-ttu-id="183af-151">TCP (만) 분에서 시간 tookeep TCP/HTTP 클라이언트에 의존 하지 않고 열 hello *유지* 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="183af-151">(TCP only) In minutes, hello time tookeep a TCP/HTTP client open without relying on *keep-alive* messages.</span></span> |

## <a name="add-a-security-rule-portal"></a><span data-ttu-id="183af-152">보안 규칙 추가(포털)</span><span class="sxs-lookup"><span data-stu-id="183af-152">Add a security rule (portal)</span></span>
<span data-ttu-id="183af-153">다음으로, tooadd hello 방화벽을 통해이 열린된 포트에서 트래픽을 라우팅하는 보안 규칙 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-153">Next, we need tooadd a security rule that routes traffic from our opened port through hello firewall.</span></span>

1. <span data-ttu-id="183af-154">Toohello 포털에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-154">Log in toohello portal.</span></span>
2. <span data-ttu-id="183af-155">찾기 hello 리소스 그룹 배포 된 hello Azure 컨테이너 서비스를 합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-155">Find hello resource group that you deployed hello Azure Container Service to.</span></span>
3. <span data-ttu-id="183af-156">선택 hello **공용** 에이전트 네트워크 보안 그룹 (라는 비슷한 너무**XXXX 에이전트-public이-nsg-XXXX**).</span><span class="sxs-lookup"><span data-stu-id="183af-156">Select hello **public** agent network security group (which is named similar too**XXXX-agent-public-nsg-XXXX**).</span></span>
   
    ![Azure Container Service 네트워크 보안 그룹](./media/container-service-enable-public-access/agent-nsg.png)
4. <span data-ttu-id="183af-158">**인바운드 보안 규칙**을 선택한 후 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-158">Select **Inbound security rules** and then **Add**.</span></span>
   
    ![Azure Container Service 네트워크 보안 그룹 규칙](./media/container-service-enable-public-access/add-firewall-rule.png)
5. <span data-ttu-id="183af-160">공용 포트 hello 방화벽 규칙 tooallow 작성 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-160">Fill out hello firewall rule tooallow your public port and click **OK**.</span></span>
   
   | <span data-ttu-id="183af-161">필드</span><span class="sxs-lookup"><span data-stu-id="183af-161">Field</span></span> | <span data-ttu-id="183af-162">설명</span><span class="sxs-lookup"><span data-stu-id="183af-162">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="183af-163">이름</span><span class="sxs-lookup"><span data-stu-id="183af-163">Name</span></span> |<span data-ttu-id="183af-164">Hello 방화벽 규칙의 설명이 포함 된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="183af-164">A descriptive name of hello firewall rule.</span></span> |
   | <span data-ttu-id="183af-165">우선 순위</span><span class="sxs-lookup"><span data-stu-id="183af-165">Priority</span></span> |<span data-ttu-id="183af-166">Hello 규칙에 대 한 우선 순위입니다.</span><span class="sxs-lookup"><span data-stu-id="183af-166">Priority rank for hello rule.</span></span> <span data-ttu-id="183af-167">hello 낮은 hello 숫자 hello 더 높은 hello 우선 순위입니다.</span><span class="sxs-lookup"><span data-stu-id="183af-167">hello lower hello number hello higher hello priority.</span></span> |
   | <span data-ttu-id="183af-168">원본</span><span class="sxs-lookup"><span data-stu-id="183af-168">Source</span></span> |<span data-ttu-id="183af-169">Hello 들어오는 IP 주소 범위 toobe이이 규칙에 따라 허용 되거나 거부를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-169">Restrict hello incoming IP address range toobe allowed or denied by this rule.</span></span> <span data-ttu-id="183af-170">사용 하 여 **모든** toonot 제한을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-170">Use **Any** toonot specify a restriction.</span></span> |
   | <span data-ttu-id="183af-171">부여</span><span class="sxs-lookup"><span data-stu-id="183af-171">Service</span></span> |<span data-ttu-id="183af-172">이 보안 규칙을 위한 미리 정의된 서비스 집합을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-172">Select a set of predefined services this security rule is for.</span></span> <span data-ttu-id="183af-173">그렇지 않으면 사용 **사용자 지정** toocreate 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-173">Otherwise use **Custom** toocreate your own.</span></span> |
   | <span data-ttu-id="183af-174">프로토콜</span><span class="sxs-lookup"><span data-stu-id="183af-174">Protocol</span></span> |<span data-ttu-id="183af-175">**TCP** 또는 **UDP**에 따라 트래픽을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-175">Restrict traffic based on **TCP** or **UDP**.</span></span> <span data-ttu-id="183af-176">사용 하 여 **모든** toonot 제한을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-176">Use **Any** toonot specify a restriction.</span></span> |
   | <span data-ttu-id="183af-177">포트 범위</span><span class="sxs-lookup"><span data-stu-id="183af-177">Port range</span></span> |<span data-ttu-id="183af-178">때 **서비스** 은 **사용자 지정**,이 규칙에 영향을 주는 포트의 hello 범위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-178">When **Service** is **Custom**, specifies hello range of ports that this rule affects.</span></span> <span data-ttu-id="183af-179">**80**과 같은 단일 포트 또는 **1024-1500**과 같은 범위를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="183af-179">You can use a single port, such as **80**, or a range like **1024-1500**.</span></span> |
   | <span data-ttu-id="183af-180">동작</span><span class="sxs-lookup"><span data-stu-id="183af-180">Action</span></span> |<span data-ttu-id="183af-181">트래픽을 허용 하거나 거부 hello 조건을 만족 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-181">Allow or deny traffic that meets hello criteria.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="183af-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="183af-182">Next steps</span></span>
<span data-ttu-id="183af-183">Hello 차이점에 대 한 자세한 내용은 [공용 및 개인 DC/OS 에이전트](container-service-dcos-agents.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="183af-183">Learn about hello difference between [public and private DC/OS agents](container-service-dcos-agents.md).</span></span>

<span data-ttu-id="183af-184">[DC/OS 컨테이너 관리](container-service-mesos-marathon-ui.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="183af-184">Read more information about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

