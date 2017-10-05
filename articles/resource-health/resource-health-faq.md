---
title: Azure Resource Health FAQ | Microsoft Docs
description: "Azure 리소스 상태 개요"
services: Resource health
documentationcenter: dev-center-name
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 06/01/2016
ms.author: BernardoAMunoz
ms.openlocfilehash: 41522a85cac05304b3ae60c45b48920eefbe8f5c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-resource-health-faq"></a><span data-ttu-id="0d509-103">Azure Resource Health FAQ</span><span class="sxs-lookup"><span data-stu-id="0d509-103">Azure Resource health FAQ</span></span>
<span data-ttu-id="0d509-104">Azure Resource Health에 대해 자주 묻는 질문과 답변에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="0d509-104">Learn the answers to common questions about Azure resource health.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="0d509-105">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="0d509-105">Frequently asked questions</span></span>
* [<span data-ttu-id="0d509-106">Azure Resource Health란?</span><span class="sxs-lookup"><span data-stu-id="0d509-106">What is Azure resource health?</span></span>](#what-is-azure-resource-health)
* [<span data-ttu-id="0d509-107">리소스 상태는 어떤 목적으로 고안되었나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-107">What is the resource health intended for?</span></span>](#what-is-the-resource-health-intended-for)
* [<span data-ttu-id="0d509-108">리소스 상태에서 어떤 상태 검사를 수행하나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-108">What health checks are performed by resource health?</span></span>](#what-health-checks-are-performed-by-resource-health)
* [<span data-ttu-id="0d509-109">각 상태는 무엇을 의미하나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-109">What does each of the health status mean?</span></span>](#what-does-each-of-the-health-status-mean)
* [<span data-ttu-id="0d509-110">알 수 없는 상태는 무엇을 의미하나요? 내 리소스에 문제가 있나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-110">What does the unknown status mean? Is something wrong with my resource?</span></span>](#what-does-the-unknown-status-mean-is-something-wrong-with-my-resource)
* [<span data-ttu-id="0d509-111">사용할 수 없는 리소스에 대한 도움을 받으려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-111">How can I get help for a resource that is unavailable?</span></span>](#how-can-i-get-help-for-a-resource-that-is-unavailable)
* [<span data-ttu-id="0d509-112">리소스 상태에서는 플랫폼 문제로 인한 사용 불가와 사용자가 의도한 사용 불가가 구분되나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-112">Does resource health differentiate between unavailability cased by platform problems versus something I did?</span></span>](#does-resource-health-differentiate-between-unavailability-cased-by-platform-problems-versus-something-i-did)
* [<span data-ttu-id="0d509-113">리소스 상태를 내 모니터링 도구에 통합할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-113">Can I integrate resource health with my monitoring tools?</span></span>](#can-i-integrate-resource-health-with-my-monitoring-tools)
* [<span data-ttu-id="0d509-114">리소스 상태는 어디서 찾을 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-114">Where do I find resource health?</span></span>](#where-do-i-find-resource-health)
* [<span data-ttu-id="0d509-115">모든 리소스 유형에 리소스 상태를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-115">Is resource health available for all resource types?</span></span>](#is-resource-health-available-for-all-resource-types)
* [<span data-ttu-id="0d509-116">내 리소스가 사용 가능으로 표시되지만 그렇지 않다고 생각되면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-116">What should I do if my resource is showing available but I believe it is not?</span></span>](#what-should-i-do-if-my-resource-is-showing-available-but-i-believe-it-is-not)
* [<span data-ttu-id="0d509-117">모든 Azure 지역에서 리소스 상태가 제공되나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-117">Is resource health available for all Azure regions?</span></span>](#is-resource-health-available-for-all-azure-regions)
* [<span data-ttu-id="0d509-118">리소스 상태는 서비스 상태 대시보드 또는 Azure Portal 서비스 알림과 어떻게 다른가요?</span><span class="sxs-lookup"><span data-stu-id="0d509-118">How is resource health different from the Service Health Dashboard or the Azure portal service notifications?</span></span>](#how-is-resource-health-different-from-the-service-health-dashboard-or-the-azure-portal-service-notifications)
* [<span data-ttu-id="0d509-119">각 리소스에 대해 리소스 상태를 활성화해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-119">Do I need to activate resource health for each resource?</span></span>](#do-i-need-to-activate-resource-health-for-each-resource)
* [<span data-ttu-id="0d509-120">내 조직에 대한 리소스 상태를 활성화해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-120">Do we need to enable resource health for my organization?</span></span>](#do-we-need-to-enable-resource-health-for-my-organization)
* [<span data-ttu-id="0d509-121">리소스 상태는 비용 없이 제공되나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-121">Is resource health available free of charge?</span></span>](#is-resource-health-available-free-of-charge)
* [<span data-ttu-id="0d509-122">리소스 상태에서 어떤 권장 사항을 제공하나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-122">What are the recommendations that resource health provides?</span></span>](#what-are-the-recommendations-that-resource-health-provides)


## <a name="what-is-azure-resource-health"></a><span data-ttu-id="0d509-123">Azure Resource Health란?</span><span class="sxs-lookup"><span data-stu-id="0d509-123">What is Azure resource health?</span></span>
<span data-ttu-id="0d509-124">Resource Health는 Azure 문제가 리소스에 영향을 주는 경우 진단 및 지원을 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-124">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="0d509-125">리소스의 현재 및 이전 상태에 대해 알려주고 문제를 완화하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-125">It informs you about the current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="0d509-126">Resource Health는 Azure 서비스 문제와 관련된 도움이 필요할 때 기술 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-126">Resource health provides technical support when you need help with Azure service issues.</span></span>  

## <a name="what-is-the-resource-health-intended-for"></a><span data-ttu-id="0d509-127">리소스 상태는 어떤 목적으로 고안되었나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-127">What is the resource health intended for?</span></span>
<span data-ttu-id="0d509-128">리소스에 문제가 감지되면 리소스 상태를 통해 근본 원인을 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-128">Once an issue with a resource has been detected, resource health can help you diagnose the root cause.</span></span> <span data-ttu-id="0d509-129">Azure 서비스 문제와 관련된 도움이 더 필요할 때 기술 지원을 제공하고 문제를 완화하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-129">It provides help to mitigate the issue and technical support when you need more help with Azure service issues.</span></span>

## <a name="what-health-checks-are-performed-by-resource-health"></a><span data-ttu-id="0d509-130">리소스 상태에서 어떤 상태 검사를 수행하나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-130">What health checks are performed by resource health?</span></span>
<span data-ttu-id="0d509-131">리소스 상태에서는 [리소스 유형](resource-health-checks-resource-types.md)에 따라 다양한 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-131">Resource health performs various checks based on the [resource type](resource-health-checks-resource-types.md).</span></span> <span data-ttu-id="0d509-132">이러한 검사는 3가지 문제 유형을 구현하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-132">These checks are designed to implement three types of issues:</span></span> 
1. <span data-ttu-id="0d509-133">계획되지 않은 이벤트(예: 예기치 않은 호스트 재부팅)</span><span class="sxs-lookup"><span data-stu-id="0d509-133">Unplanned events, for example an unexpected host reboot</span></span>
2. <span data-ttu-id="0d509-134">계획된 이벤트(예약된 호스트 OS 업데이트)</span><span class="sxs-lookup"><span data-stu-id="0d509-134">Planned events, like scheduled host OS updates</span></span>
3. <span data-ttu-id="0d509-135">사용자 작업으로 트리거된 이벤트(예: 사용자가 가상 컴퓨터를 다시 부팅)</span><span class="sxs-lookup"><span data-stu-id="0d509-135">Events triggered by user actions, for example a user rebooting a virtual machine</span></span>

## <a name="what-does-each-of-the-health-status-mean"></a><span data-ttu-id="0d509-136">각 상태는 무엇을 의미하나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-136">What does each of the health status mean?</span></span>
<span data-ttu-id="0d509-137">3가지 상태가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-137">There are three different health statuses:</span></span>
1. <span data-ttu-id="0d509-138">사용 가능: Azure 플랫폼에 이 리소스에 영향을 줄 수 있는 알려진 문제가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-138">Available: There aren't any known problems in the Azure platform that could be impacting this resource</span></span>
2. <span data-ttu-id="0d509-139">사용할 수 없음: 리소스 상태에서 리소스에 영향을 주는 문제를 감지했습니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-139">Unavailable: Resource health has detected issues that are impacting the resource</span></span>
3. <span data-ttu-id="0d509-140">알 수 없음: Resource Health에서 리소스에 대한 정보 수신을 중지했으므로 리소스의 상태를 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-140">Unknown: Resource health can not determine the health of a resource because it has stopped receiving information about it.</span></span> 

## <a name="what-does-the-unknown-status-mean-is-something-wrong-with-my-resource"></a><span data-ttu-id="0d509-141">알 수 없는 상태는 무엇을 의미하나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-141">What does the unknown status mean?</span></span> <span data-ttu-id="0d509-142">내 리소스에 문제가 있나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-142">Is something wrong with my resource?</span></span>
<span data-ttu-id="0d509-143">리소스 상태에서 특정 리소스에 대한 정보 수신을 중지하면 상태가 알 수 없음으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-143">The health status is set to unknown when resource health stops receiving information about a specific resource.</span></span> <span data-ttu-id="0d509-144">이 상태는 리소스 상태의 최종적인 표시는 아니지만 문제가 발생한 경우 Azure 문제가 있음을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-144">While this status is not a definitive indication of the state of the resource, in cases where you are experiencing problems, it may indicate there is an Azure problem.</span></span>

## <a name="how-can-i-get-help-for-a-resource-that-is-unavailable"></a><span data-ttu-id="0d509-145">사용할 수 없는 리소스에 대한 도움을 받으려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-145">How can I get help for a resource that is unavailable?</span></span>
<span data-ttu-id="0d509-146">리소스 상태 블레이드에서 지원 요청을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-146">You can submit a support request from the resource health blade.</span></span> <span data-ttu-id="0d509-147">플랫폼 이벤트로 인해 리소스를 사용할 수 없는 경우 요청을 열기 위해 Microsoft와 지원 계약이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-147">You do not need a support agreement with Microsoft to open a request when the resource is unavailable because platform events.</span></span>

## <a name="does-resource-health-differentiate-between-unavailability-cased-by-platform-problems-versus-something-i-did"></a><span data-ttu-id="0d509-148">리소스 상태에서는 플랫폼 문제로 인한 사용 불가와 사용자가 의도한 사용 불가가 구분되나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-148">Does resource health differentiate between unavailability cased by platform problems versus something I did?</span></span>
<span data-ttu-id="0d509-149">예, 리소스를 사용할 수 없는 경우 리소스 상태는 다음과 같은 범주 중 하나에서 근본 원인을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-149">Yes, when a resource is unavailable, resource health identifies the root cause within one of these categories:</span></span> 
1.  <span data-ttu-id="0d509-150">사용자가 시작한 작업</span><span class="sxs-lookup"><span data-stu-id="0d509-150">User initiated action</span></span>
2.  <span data-ttu-id="0d509-151">계획된 이벤트</span><span class="sxs-lookup"><span data-stu-id="0d509-151">Planned event</span></span> 
3.  <span data-ttu-id="0d509-152">계획되지 않은 이벤트</span><span class="sxs-lookup"><span data-stu-id="0d509-152">Unplanned event</span></span>

<span data-ttu-id="0d509-153">포털에서는 사용자가 시작한 작업이 파란색 알림 아이콘을 사용하여 표시되지만 계획 및 계획되지 않은 이벤트는 빨간색 경고 아이콘을 사용하여 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-153">In the portal, user initiated actions are shown using a blue notification icon, while planned and unplanned events are shown using a red warning icon.</span></span> <span data-ttu-id="0d509-154">자세한 내용은 [리소스 상태 개요](Resource-health-overview.md)에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-154">More details are provided in the [resource health overview](Resource-health-overview.md).</span></span>  

## <a name="can-i-integrate-resource-health-with-my-monitoring-tools"></a><span data-ttu-id="0d509-155">리소스 상태를 내 모니터링 도구에 통합할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-155">Can I integrate resource health with my monitoring tools?</span></span>
<span data-ttu-id="0d509-156">리소스 상태는 리소스에 영향을 주는 Azure 서비스 문제를 진단 및 완화할 수 있도록 설계된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-156">Resource health is a service designed to help you diagnose and mitigate Azure service issues that impact your resources.</span></span> <span data-ttu-id="0d509-157">리소스 상태 API를 사용하여 프로그래밍 방식으로 상태를 얻을 수 있지만 리소스를 모니터링하는 데는 메트릭을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-157">While you can use the resource health API to programmatically obtain the health status, we recommend you use metrics to monitor your resources.</span></span> <span data-ttu-id="0d509-158">일단 문제가 감지되면 리소스 상태를 통해 근본 원인을 파악하고 이를 해결하기 위한 작업을 안내할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-158">Once an issue is detected, resource health helps you determine the root cause and guides you through actions to address them.</span></span> <span data-ttu-id="0d509-159">메트릭을 사용하여 리소스를 확인하는 방법은 [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="0d509-159">Visit [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) to learn more about how you can use metrics to check your resources.</span></span>

## <a name="where-do-i-find-resource-health"></a><span data-ttu-id="0d509-160">리소스 상태는 어디서 찾을 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-160">Where do I find resource health?</span></span>
<span data-ttu-id="0d509-161">Azure Portal에 로그인하면 여러 가지 방법으로 리소스 상태에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-161">After you log in to the Azure portal, there are multiple ways you can access resource health:</span></span>
1. <span data-ttu-id="0d509-162">리소스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-162">Navigate to your resource.</span></span> <span data-ttu-id="0d509-163">왼쪽 탐색에서 **리소스 상태**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-163">In the left-hand navigation, click **Resource health**.</span></span>
2. <span data-ttu-id="0d509-164">Azure Monitor 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-164">Go to the Azure Monitor blade.</span></span>  <span data-ttu-id="0d509-165">왼쪽 탐색에서 **리소스 상태**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-165">In the left-hand navigation, click **Resource health**.</span></span>
3. <span data-ttu-id="0d509-166">포털 오른쪽 위 모서리에서 물음표를 클릭하고 **도움말 + 지원**을 선택하여 **도움말 + 지원** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-166">Open the **Help + Support** blade by clicking the question mark in the upper right corner of the portal and then selecting **Help + Support**.</span></span> <span data-ttu-id="0d509-167">블레이드가 열리면 **리소스 상태**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-167">Once the blade opens, click **Resource health**</span></span>

<span data-ttu-id="0d509-168">리소스 상태 API를 사용하여 리소스 상태에 대한 정보를 얻을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-168">You can also use the resource health API to obtain information about the health of your resources.</span></span>

## <a name="is-resource-health-available-for-all-resource-types"></a><span data-ttu-id="0d509-169">모든 리소스 유형에 리소스 상태를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-169">Is resource health available for all resource types?</span></span>
<span data-ttu-id="0d509-170">리소스 상태를 통해 지원되는 상태 검사 및 리소스 유형 목록은 [여기](resource-health-checks-resource-types.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-170">The list of health checks and resource types supported through resource health can be found [here](resource-health-checks-resource-types.md)</span></span>

## <a name="what-should-i-do-if-my-resource-is-showing-available-but-i-believe-it-is-not"></a><span data-ttu-id="0d509-171">내 리소스가 사용 가능으로 표시되지만 그렇지 않다고 생각되면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-171">What should I do if my resource is showing available but I believe it is not?”</span></span>
<span data-ttu-id="0d509-172">리소스 상태를 검사할 때는 상태 오른쪽 아래에서 **Report incorrect health status(잘못된 상태 보고)**를 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-172">When checking the health of a resource, right under the health status you can click **Report incorrect health status**.</span></span> <span data-ttu-id="0d509-173">보고서를 제출하기 전에 현재 상태가 잘못되었다고 생각하는 이유에 대해 자세히 입력하는 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-173">Before submitting the report, you have the option of providing additional details on why you believe the current health status is incorrect.</span></span>

## <a name="is-resource-health-available-for-all-azure-regions"></a><span data-ttu-id="0d509-174">모든 Azure 지역에서 리소스 상태가 제공되나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-174">Is resource health available for all Azure regions?</span></span> 
<span data-ttu-id="0d509-175">리소스 상태는 다음 지역을 제외한 모든 Azure 지역 간에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-175">Resource health is available in across all Azure geos except the following regions:</span></span>
* <span data-ttu-id="0d509-176">미국 정부 버지니아</span><span class="sxs-lookup"><span data-stu-id="0d509-176">US Gov Virginia</span></span>
* <span data-ttu-id="0d509-177">미국 정부 아이오와</span><span class="sxs-lookup"><span data-stu-id="0d509-177">US Gov Iowa</span></span>
* <span data-ttu-id="0d509-178">미국 국방부 동부</span><span class="sxs-lookup"><span data-stu-id="0d509-178">US DoD East</span></span>
* <span data-ttu-id="0d509-179">미국 국방부 중부</span><span class="sxs-lookup"><span data-stu-id="0d509-179">US DoD Central</span></span>
* <span data-ttu-id="0d509-180">독일 중부</span><span class="sxs-lookup"><span data-stu-id="0d509-180">Germany Central</span></span>
* <span data-ttu-id="0d509-181">독일 북동부</span><span class="sxs-lookup"><span data-stu-id="0d509-181">Germany Northeast</span></span>
* <span data-ttu-id="0d509-182">중국 동부</span><span class="sxs-lookup"><span data-stu-id="0d509-182">China East</span></span>
* <span data-ttu-id="0d509-183">중국 북부</span><span class="sxs-lookup"><span data-stu-id="0d509-183">China North</span></span>

## <a name="how-is-resource-health-different-from-the-service-health-dashboard-or-the-azure-portal-service-notifications"></a><span data-ttu-id="0d509-184">리소스 상태는 서비스 상태 대시보드 또는 Azure Portal 서비스 알림과 어떻게 다른가요?</span><span class="sxs-lookup"><span data-stu-id="0d509-184">How is resource health different from the Service Health Dashboard or the Azure portal service notifications?</span></span>
<span data-ttu-id="0d509-185">리소스 상태에서 제공하는 정보는 Azure 서비스 상태 대시보드에서 제공하는 정보보다 더 구체적입니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-185">The information provided by resource health is more specific than what is provided by the Azure Service Health Dashboard.</span></span>

<span data-ttu-id="0d509-186">[Azure 상태](https://status.azure.com)와 포털 서비스 알림은 광범위한 고객 집합(예: Azure 지역)에 영향을 주는 서비스 문제를 알려주지만, 리소스 상태는 특정 리소스에만 관련된 보다 세분화된 이벤트를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-186">Whereas [Azure Status](https://status.azure.com) and the portal service notifications inform you about service issues that affect a broad set of customers (for example an Azure region), resource health exposes more granular events that are relevant only to the specific resource.</span></span> <span data-ttu-id="0d509-187">예를 들어 호스트가 예기치 않게 재부팅되는 경우 리소스 상태는 가상 컴퓨터가 해당 호스트에서 실행 중인 고객에게만 경고합니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-187">For example, if a host unexpectedly reboots, resource health alerts only those customers whose virtual machines were running on that host.</span></span>

<span data-ttu-id="0d509-188">리소스에 영향을 주는 이벤트에 대한 충분한 가시성을 제공하는 것이 중요하며 리소스 상태는 서비스 알림 및 서비스 상태 대시보드에 게시된 이벤트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-188">It is important to notice that to provide you complete visibility of events impacting your resources, resource health also surfaces events published in Service notifications and the Service Health Dashboard.</span></span>

## <a name="do-i-need-to-activate-resource-health-for-each-resource"></a><span data-ttu-id="0d509-189">각 리소스에 대해 리소스 상태를 활성화해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-189">Do I need to activate resource health for each resource?</span></span>
<span data-ttu-id="0d509-190">아니요, 상태 정보는 리소스 상태를 통해 제공되는 모든 리소스 유형에 대해 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-190">No, health information is available for all resource types available through resource health.</span></span> 

## <a name="do-we-need-to-enable-resource-health-for-my-organization"></a><span data-ttu-id="0d509-191">내 조직에 대한 리소스 상태를 활성화해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-191">Do we need to enable resource health for my organization?</span></span>
<span data-ttu-id="0d509-192">아니요.</span><span class="sxs-lookup"><span data-stu-id="0d509-192">No.</span></span>  <span data-ttu-id="0d509-193">Azure Resource Health는 어떠한 설정 없이도 Azure Portal 내에서 액세스 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-193">Azure resource health is accessible within the Azure portal without any setup requirements.</span></span>

## <a name="is-resource-health-available-free-of-charge"></a><span data-ttu-id="0d509-194">리소스 상태는 비용 없이 제공되나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-194">Is resource health available free of charge?</span></span>
<span data-ttu-id="0d509-195">예.</span><span class="sxs-lookup"><span data-stu-id="0d509-195">Yes.</span></span>  <span data-ttu-id="0d509-196">Azure Resource Health에는 비용이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-196">Azure resource health is free of charge.</span></span>

## <a name="what-are-the-recommendations-that-resource-health-provides"></a><span data-ttu-id="0d509-197">리소스 상태에서 어떤 권장 사항을 제공하나요?</span><span class="sxs-lookup"><span data-stu-id="0d509-197">What are the recommendations that resource health provides?</span></span>
<span data-ttu-id="0d509-198">리소스 상태는 상태에 따라 문제 해결에 소요되는 시간을 줄이는 것을 목적으로 권장 사항을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-198">Based on the health status, resource health provides you with recommendations with the goal of reducing the time you spent troubleshooting.</span></span> <span data-ttu-id="0d509-199">사용 가능한 리소스에 대한 권장 사항은 고객이 직면하는 가장 일반적인 문제를 해결하는 방법에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-199">For available resources, the recommendations focus on how to solve the most common problems customers encounter.</span></span> <span data-ttu-id="0d509-200">Azure 계획되지 않은 이벤트로 인해 리소스를 사용할 수 없는 경우 복구 프로세스 동안과 복구 이후 지원에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="0d509-200">If the resource is unavailable due to an Azure unplanned event, the focus will be on assisting you during and after the recovery process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0d509-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0d509-201">Next steps</span></span>

<span data-ttu-id="0d509-202">리소스 상태에 대한 자세한 내용은 다음 리소스를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="0d509-202">Check out these resources to learn more about resource health:</span></span>
-  [<span data-ttu-id="0d509-203">Azure Resource Health 개요</span><span class="sxs-lookup"><span data-stu-id="0d509-203">Azure resource health overview</span></span>](Resource-health-overview.md)
-  [<span data-ttu-id="0d509-204">Azure Resource Health를 통해 사용할 수 있는 리소스 유형 및 상태 검사</span><span class="sxs-lookup"><span data-stu-id="0d509-204">Resource types and health checks available through Azure resource health</span></span>](resource-health-checks-resource-types.md)
