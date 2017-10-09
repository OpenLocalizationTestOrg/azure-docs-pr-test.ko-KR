---
title: "리소스 상태 FAQ aaaAzure | Microsoft Docs"
description: "Azure Resource Health 개요"
services: Resource health
documentationcenter: dev-center-name
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/05/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: fe29b2df1f9fee4b77d0100c7d872df837dc4b4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-faq"></a><span data-ttu-id="29554-103">Azure Resource Health FAQ</span><span class="sxs-lookup"><span data-stu-id="29554-103">Azure Resource Health FAQ</span></span>
<span data-ttu-id="29554-104">Hello Azure 리소스 상태에 대 한 toocommon 질문에 답변에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="29554-104">Learn hello answers toocommon questions about Azure Resource Health.</span></span>

## <a name="what-is-azure-resource-health"></a><span data-ttu-id="29554-105">Azure Resource Health란?</span><span class="sxs-lookup"><span data-stu-id="29554-105">What is Azure Resource Health?</span></span>
<span data-ttu-id="29554-106">Resource Health는 Azure 문제가 리소스에 영향을 주는 경우 진단 및 지원을 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="29554-106">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="29554-107">리소스의 hello 최신 및 이전 상태에 대해 알려 하 고 문제를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29554-107">It informs you about hello current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="29554-108">Resource Health는 Azure 서비스 문제와 관련된 도움이 필요할 때 기술 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="29554-108">Resource health provides technical support when you need help with Azure service issues.</span></span>  

## <a name="what-is-hello-resource-health-intended-for"></a><span data-ttu-id="29554-109">리소스 상태를 위한 hello 이란?</span><span class="sxs-lookup"><span data-stu-id="29554-109">What is hello Resource Health intended for?</span></span>
<span data-ttu-id="29554-110">리소스에 문제가 감지 되 면 리소스 상태 hello 근본 원인을 진단 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="29554-110">Once an issue with a resource has been detected, Resource Health can help you diagnose hello root cause.</span></span> <span data-ttu-id="29554-111">Azure 서비스 문제에 도움이 필요한 경우 도움말 toomitigate hello 문제 및 기술 지원을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="29554-111">It provides help toomitigate hello issue and technical support when you need more help with Azure service issues.</span></span>

## <a name="what-health-checks-are-performed-by-resource-health"></a><span data-ttu-id="29554-112">Resource Health에서 어떤 상태 검사를 수행하나요?</span><span class="sxs-lookup"><span data-stu-id="29554-112">What health checks are performed by Resource Health?</span></span>
<span data-ttu-id="29554-113">Hello에 따라 다양 한 검사를 수행 하는 리소스 상태 [리소스 종류](resource-health-checks-resource-types.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="29554-113">Resource health performs various checks based on hello [resource type](resource-health-checks-resource-types.md).</span></span> <span data-ttu-id="29554-114">이러한 검사는 세 가지 유형의 문제를 설계 된 tooimplement:</span><span class="sxs-lookup"><span data-stu-id="29554-114">These checks are designed tooimplement three types of issues:</span></span> 
- <span data-ttu-id="29554-115">계획되지 않은 이벤트(예: 예기치 않은 호스트 재부팅)</span><span class="sxs-lookup"><span data-stu-id="29554-115">Unplanned events, for example an unexpected host reboot</span></span>
- <span data-ttu-id="29554-116">계획된 이벤트(예약된 호스트 OS 업데이트)</span><span class="sxs-lookup"><span data-stu-id="29554-116">Planned events, like scheduled host OS updates</span></span>
- <span data-ttu-id="29554-117">사용자 작업으로 트리거된 이벤트(예: 사용자가 가상 컴퓨터를 다시 부팅)</span><span class="sxs-lookup"><span data-stu-id="29554-117">Events triggered by user actions, for example a user rebooting a virtual machine</span></span>

## <a name="what-does-each-of-hello-health-status-mean"></a><span data-ttu-id="29554-118">어떤 hello 상태의 각 의미 입니까?</span><span class="sxs-lookup"><span data-stu-id="29554-118">What does each of hello health status mean?</span></span>
<span data-ttu-id="29554-119">3가지 상태가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29554-119">There are three different health statuses:</span></span>
- <span data-ttu-id="29554-120">사용 가능한 공간: 알려진된 문제가 없습니다 hello이이 리소스에 미치는 영향 수 있는 Azure 플랫폼에서</span><span class="sxs-lookup"><span data-stu-id="29554-120">Available: There aren't any known problems in hello Azure platform that could be impacting this resource</span></span>
- <span data-ttu-id="29554-121">사용할 수 없음: 리소스 상태 요소가 hello 리소스 영향을 미치는 문제</span><span class="sxs-lookup"><span data-stu-id="29554-121">Unavailable: Resource health has detected issues that are impacting hello resource</span></span>
- <span data-ttu-id="29554-122">: 알 수 없는 리소스 상태가 확인할 수 없습니다 리소스의 hello 상태 항목에 대 한 정보를 받아 중지 했습니다.</span><span class="sxs-lookup"><span data-stu-id="29554-122">Unknown: Resource health can not determine hello health of a resource because it has stopped receiving information about it.</span></span> 

## <a name="what-does-hello-unknown-status-mean-is-something-wrong-with-my-resource"></a><span data-ttu-id="29554-123">알 수 없는 상태 평균 hello는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="29554-123">What does hello unknown status mean?</span></span> <span data-ttu-id="29554-124">내 리소스에 문제가 있나요?</span><span class="sxs-lookup"><span data-stu-id="29554-124">Is something wrong with my resource?</span></span>
<span data-ttu-id="29554-125">hello 상태는 리소스 상태 특정 리소스에 대 한 정보 수신이 중지 될 때 toounknown을 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29554-125">hello health status is set toounknown when Resource Health stops receiving information about a specific resource.</span></span> <span data-ttu-id="29554-126">이 상태가 되어 있지 않지만 문제가 발생 하는 경우에 hello 리소스의 hello 상태의 최종 표시를 Azure 문제가 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29554-126">While this status is not a definitive indication of hello state of hello resource, in cases where you are experiencing problems, it may indicate there is an Azure problem.</span></span>

## <a name="how-can-i-get-help-for-a-resource-that-is-unavailable"></a><span data-ttu-id="29554-127">사용할 수 없는 리소스에 대한 도움을 받으려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="29554-127">How can I get help for a resource that is unavailable?</span></span>
<span data-ttu-id="29554-128">Hello 리소스 상태 블레이드에서 지원 요청을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29554-128">You can submit a support request from hello Resource Health blade.</span></span> <span data-ttu-id="29554-129">Hello 리소스를 사용할 수 없는 경우 Microsoft tooopen 요청에 대 한 지원 계약 불필요 때문에 플랫폼 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="29554-129">You do not need a support agreement with Microsoft tooopen a request when hello resource is unavailable because platform events.</span></span>

## <a name="does-resource-health-differentiate-between-unavailability-cased-by-platform-problems-versus-something-i-did"></a><span data-ttu-id="29554-130">Resource Health에서는 플랫폼 문제로 인한 사용 불가와 사용자가 의도한 사용 불가가 구분되나요?</span><span class="sxs-lookup"><span data-stu-id="29554-130">Does Resource Health differentiate between unavailability cased by platform problems versus something I did?</span></span>
<span data-ttu-id="29554-131">예, 리소스를 사용할 수 없는 경우 리소스 상태에 이러한 범주 중 하나 내 hello 근본 원인을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="29554-131">Yes, when a resource is unavailable, Resource Health identifies hello root cause within one of these categories:</span></span> 
-   <span data-ttu-id="29554-132">사용자가 시작한 작업</span><span class="sxs-lookup"><span data-stu-id="29554-132">User initiated action</span></span>
-   <span data-ttu-id="29554-133">계획된 이벤트</span><span class="sxs-lookup"><span data-stu-id="29554-133">Planned event</span></span> 
-   <span data-ttu-id="29554-134">계획되지 않은 이벤트</span><span class="sxs-lookup"><span data-stu-id="29554-134">Unplanned event</span></span>

<span data-ttu-id="29554-135">Hello 포털에서 사용자가 시작한 작업 계획 되거나 계획 되지 않은 이벤트 빨간색 경고 아이콘이 사용 하 여 표시 되어 파란색 알림 아이콘을 사용 하 여 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29554-135">In hello portal, user initiated actions are shown using a blue notification icon, while planned and unplanned events are shown using a red warning icon.</span></span> <span data-ttu-id="29554-136">자세한 내용은 hello에서 제공 됩니다 [리소스 상태 개요](Resource-health-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="29554-136">More details are provided in hello [Resource Health overview](Resource-health-overview.md).</span></span>  

## <a name="can-i-integrate-resource-health-with-my-monitoring-tools"></a><span data-ttu-id="29554-137">Resource Health를 내 모니터링 도구에 통합할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="29554-137">Can I integrate Resource Health with my monitoring tools?</span></span>
<span data-ttu-id="29554-138">리소스 상태를 진단 하 고 리소스에 영향을 주는 Azure 서비스 문제를 완화 설계 된 서비스 toohelp 합니다.</span><span class="sxs-lookup"><span data-stu-id="29554-138">Resource health is a service designed toohelp you diagnose and mitigate Azure service issues that impact your resources.</span></span> <span data-ttu-id="29554-139">사용할 수 있지만, hello 리소스 상태 API tooprogrammatically hello 상태를 가져와서 메트릭 toomonitor 리소스를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="29554-139">While you can use hello Resource Health API tooprogrammatically obtain hello health status, we recommend you use metrics toomonitor your resources.</span></span> <span data-ttu-id="29554-140">리소스 상태 hello 근본 원인을 확인할 수 있습니다 및 작업 tooaddress 과정을 안내해 문제가 감지 되 면 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="29554-140">Once an issue is detected, Resource Health helps you determine hello root cause and guides you through actions tooaddress them.</span></span> <span data-ttu-id="29554-141">방문 [Azure 모니터](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) toolearn 사용 하는 방법을 메트릭 toocheck 리소스에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="29554-141">Visit [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) toolearn more about how you can use metrics toocheck your resources.</span></span>

## <a name="where-do-i-find-resource-health"></a><span data-ttu-id="29554-142">Resource Health는 어디서 찾을 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="29554-142">Where do I find Resource Health?</span></span>
<span data-ttu-id="29554-143">Toohello Azure 포털에에서 로그인 한 후 여러 가지 방법으로 리소스 상태에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29554-143">After you log in toohello Azure portal, there are multiple ways you can access Resource Health:</span></span>
- <span data-ttu-id="29554-144">Tooyour 리소스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="29554-144">Navigate tooyour resource.</span></span> <span data-ttu-id="29554-145">Hello 왼쪽 탐색에서 선택 **리소스 상태**</span><span class="sxs-lookup"><span data-stu-id="29554-145">In hello left-hand navigation, select **Resource health**</span></span>
- <span data-ttu-id="29554-146">Toohello Azure 모니터 블레이드로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="29554-146">Go toohello Azure Monitor blade.</span></span>  <span data-ttu-id="29554-147">Hello 왼쪽 탐색에서 선택 **리소스 상태**합니다.</span><span class="sxs-lookup"><span data-stu-id="29554-147">In hello left-hand navigation, select **Resource health**.</span></span>
- <span data-ttu-id="29554-148">열기 hello **도움말 + 지원** 블레이드에서 다음을 선택 하 고 hello 포털의 hello 상단 오른쪽 모서리에 hello 매개 변수를 선택 하 여 **도움말 + 지원**합니다.</span><span class="sxs-lookup"><span data-stu-id="29554-148">Open hello **Help + Support** blade by selecting hello question mark in hello upper right corner of hello portal and then selecting **Help + Support**.</span></span> <span data-ttu-id="29554-149">Hello 블레이드가 열리고 되 면 선택 **리소스 상태**</span><span class="sxs-lookup"><span data-stu-id="29554-149">Once hello blade opens, select **Resource health**</span></span>

<span data-ttu-id="29554-150">Hello 리소스 상태 API tooobtain 정보의 hello 상태에 대 한 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29554-150">You can also use hello Resource Health API tooobtain information about hello health of your resources.</span></span>

## <a name="is-resource-health-available-for-all-resource-types"></a><span data-ttu-id="29554-151">모든 리소스 유형에 Resource Health를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="29554-151">Is Resource Health available for all resource types?</span></span>
<span data-ttu-id="29554-152">hello 상태 검사 및 리소스 상태를 통해 지원 되는 리소스 형식 목록이 있습니다 [여기](resource-health-checks-resource-types.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="29554-152">hello list of health checks and resource types supported through Resource Health can be found [here](resource-health-checks-resource-types.md).</span></span>

## <a name="what-should-i-do-if-my-resource-is-showing-available-but-i-believe-it-is-not"></a><span data-ttu-id="29554-153">내 리소스가 사용 가능으로 표시되지만 그렇지 않다고 생각되면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="29554-153">What should I do if my resource is showing available but I believe it is not?”</span></span>
<span data-ttu-id="29554-154">리소스의 hello 상태를 확인할 때 바로 아래 hello 상태에서 클릭할 수 있는 **잘못 된 상태를 보고**합니다.</span><span class="sxs-lookup"><span data-stu-id="29554-154">When checking hello health of a resource, right under hello health status you can click **Report incorrect health status**.</span></span> <span data-ttu-id="29554-155">Hello 보고서를 전송 하기 전에 hello 현재 상태가 잘못 되었습니다. 생각 이유에서 추가 세부 정보를 제공 하는 중 hello 선택할을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29554-155">Before submitting hello report, you have hello option of providing additional details on why you believe hello current health status is incorrect.</span></span>

## <a name="is-resource-health-available-for-all-azure-regions"></a><span data-ttu-id="29554-156">모든 Azure 지역에서 Resource Health가 제공되나요?</span><span class="sxs-lookup"><span data-stu-id="29554-156">Is Resource Health available for all Azure regions?</span></span> 
<span data-ttu-id="29554-157">Hello 다음 영역을 제외한 모든 Azure geos에서 리소스 상태에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29554-157">Resource health is available in across all Azure geos except hello following regions:</span></span>
- <span data-ttu-id="29554-158">미국 정부 버지니아</span><span class="sxs-lookup"><span data-stu-id="29554-158">US Gov Virginia</span></span>
- <span data-ttu-id="29554-159">미국 정부 아이오와</span><span class="sxs-lookup"><span data-stu-id="29554-159">US Gov Iowa</span></span>
- <span data-ttu-id="29554-160">미국 국방부 동부</span><span class="sxs-lookup"><span data-stu-id="29554-160">US DoD East</span></span>
- <span data-ttu-id="29554-161">미국 국방부 중부</span><span class="sxs-lookup"><span data-stu-id="29554-161">US DoD Central</span></span>
- <span data-ttu-id="29554-162">독일 중부</span><span class="sxs-lookup"><span data-stu-id="29554-162">Germany Central</span></span>
- <span data-ttu-id="29554-163">독일 북동부</span><span class="sxs-lookup"><span data-stu-id="29554-163">Germany Northeast</span></span>
- <span data-ttu-id="29554-164">중국 동부</span><span class="sxs-lookup"><span data-stu-id="29554-164">China East</span></span>
- <span data-ttu-id="29554-165">중국 북부</span><span class="sxs-lookup"><span data-stu-id="29554-165">China North</span></span>

## <a name="how-is-resource-health-different-from-hello-service-health-dashboard-or-hello-azure-portal-service-notifications"></a><span data-ttu-id="29554-166">리소스 상태 hello 서비스 상태 대시보드 또는 hello Azure 포털 서비스 알림와 어떻게 다릅니까?</span><span class="sxs-lookup"><span data-stu-id="29554-166">How is Resource Health different from hello Service Health Dashboard or hello Azure portal service notifications?</span></span>
<span data-ttu-id="29554-167">리소스 상태에서 제공 하는 hello 정보 hello Azure 서비스 상태 대시보드에서 제공 하는 보다 구체적인입니다.</span><span class="sxs-lookup"><span data-stu-id="29554-167">hello information provided by Resource Health is more specific than what is provided by hello Azure Service Health Dashboard.</span></span>

<span data-ttu-id="29554-168">반면 [Azure 상태](https://status.azure.com) 및 hello 포털 서비스 알림 광범위 한 고객 (예: Azure 지역)에 영향을 주는 서비스 문제에 대 한 사용자에 게 알립니다만 관련이 있는 보다 세부적인 이벤트를 노출 하는 리소스 상태 toohello 특정 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="29554-168">Whereas [Azure Status](https://status.azure.com) and hello portal service notifications inform you about service issues that affect a broad set of customers (for example an Azure region), Resource Health exposes more granular events that are relevant only toohello specific resource.</span></span> <span data-ttu-id="29554-169">예를 들어 호스트가 예기치 않게 재부팅되는 경우 Resource Health는 가상 컴퓨터가 해당 호스트에서 실행 중인 고객에게만 경고합니다.</span><span class="sxs-lookup"><span data-stu-id="29554-169">For example, if a host unexpectedly reboots, Resource Health alerts only those customers whose virtual machines were running on that host.</span></span>

<span data-ttu-id="29554-170">중요 한 toonotice에서는 리소스를 표면 이벤트 알림 서비스에에서도 게시 하는 리소스 상태에 영향을 주지 이벤트의 표시 여부를 완료 하면 해당 tooprovide 사용 되며 서비스 상태 대시보드에서 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="29554-170">It is important toonotice that tooprovide you complete visibility of events impacting your resources, Resource Health also surfaces events published in Service notifications and hello Service Health Dashboard.</span></span>

## <a name="do-i-need-tooactivate-resource-health-for-each-resource"></a><span data-ttu-id="29554-171">각 리소스에 대 한 리소스 상태 tooactivate 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="29554-171">Do I need tooactivate Resource Health for each resource?</span></span>
<span data-ttu-id="29554-172">아니요, 상태 정보는 Resource Health를 통해 제공되는 모든 리소스 유형에 대해 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="29554-172">No, health information is available for all resource types available through Resource Health.</span></span> 

## <a name="do-we-need-tooenable-resource-health-for-my-organization"></a><span data-ttu-id="29554-173">내 조직에 대 한 리소스 상태 tooenable 필요한 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="29554-173">Do we need tooenable Resource Health for my organization?</span></span>
<span data-ttu-id="29554-174">아니요.</span><span class="sxs-lookup"><span data-stu-id="29554-174">No.</span></span>  <span data-ttu-id="29554-175">Azure 리소스 상태를 hello를 설치할 필요 없이 Azure 포털 내에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29554-175">Azure Resource Health is accessible within hello Azure portal without any setup requirements.</span></span>

## <a name="is-resource-health-available-free-of-charge"></a><span data-ttu-id="29554-176">Resource Health는 비용 없이 제공되나요?</span><span class="sxs-lookup"><span data-stu-id="29554-176">Is Resource Health available free of charge?</span></span>
<span data-ttu-id="29554-177">예.</span><span class="sxs-lookup"><span data-stu-id="29554-177">Yes.</span></span>  <span data-ttu-id="29554-178">Azure Resource Health에는 비용이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="29554-178">Azure Resource Health is free of charge.</span></span>

## <a name="what-are-hello-recommendations-that-resource-health-provides"></a><span data-ttu-id="29554-179">리소스 상태를 제공 하는 hello 권장 사항은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="29554-179">What are hello recommendations that Resource Health provides?</span></span>
<span data-ttu-id="29554-180">Hello 상태에 따라, 리소스 상태를 제공 돌려받을 문제 해결 권장 사항을 hello 시간을 줄이는 hello 목표와 합니다.</span><span class="sxs-lookup"><span data-stu-id="29554-180">Based on hello health status, Resource Health provides you with recommendations with hello goal of reducing hello time you spent troubleshooting.</span></span> <span data-ttu-id="29554-181">사용 가능한 리소스에 대 한 hello 권장 사항을 toosolve hello 가장 일반적인 문제 고객 발생 하는 방법에 집중 합니다.</span><span class="sxs-lookup"><span data-stu-id="29554-181">For available resources, hello recommendations focus on how toosolve hello most common problems customers encounter.</span></span> <span data-ttu-id="29554-182">Hello 리소스 인해 사용할 수 없는 경우 Azure의 계획 되지 않은 이벤트 tooan hello 포커스에 포함 될 동안과 그 후 hello 복구 과정을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="29554-182">If hello resource is unavailable due tooan Azure unplanned event, hello focus will be on assisting you during and after hello recovery process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="29554-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="29554-183">Next steps</span></span>

<span data-ttu-id="29554-184">Resource Health에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="29554-184">Learn more about Resource Health:</span></span>
-  [<span data-ttu-id="29554-185">Azure Resource Health 개요</span><span class="sxs-lookup"><span data-stu-id="29554-185">Azure Resource Health overview</span></span>](Resource-health-overview.md)
-  [<span data-ttu-id="29554-186">Azure Resource Health를 통해 사용할 수 있는 리소스 유형 및 상태 검사</span><span class="sxs-lookup"><span data-stu-id="29554-186">Resource types and health checks available through Azure Resource Health</span></span>](resource-health-checks-resource-types.md)
