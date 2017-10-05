---
title: "Azure Log Analytics를 사용하여 Active Directory 환경 최적화 | Microsoft Docs"
description: "Active Directory 평가 솔루션을 사용하여 일정한 간격으로 서버 환경의 위험 및 상태를 평가할 수 있습니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 81eb41b8-eb62-4eb2-9f7b-fde5c89c9b47
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 97368f0b9e89ffd0cd982b6e8670d5a1f62ad42c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="optimize-your-active-directory-environment-with-the-active-directory-assessment-solution-in-log-analytics"></a><span data-ttu-id="2b13d-103">Log Analytics에서 Active Directory 평가 솔루션을 사용하여 사용자의 Active Directory 환경 최적화</span><span class="sxs-lookup"><span data-stu-id="2b13d-103">Optimize your Active Directory environment with the Active Directory Assessment solution in Log Analytics</span></span>

![AD 평가 기호](./media/log-analytics-ad-assessment/ad-assessment-symbol.png)

<span data-ttu-id="2b13d-105">Active Directory 평가 솔루션을 사용하여 일정한 간격으로 서버 환경의 위험 및 상태를 평가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-105">You can use the Active Directory Assessment solution to assess the risk and health of your server environments on a regular interval.</span></span> <span data-ttu-id="2b13d-106">이 문서에서는 잠재적인 문제에 대해 올바른 조치를 취할 수 있도록 솔루션을 설치하고 사용하도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-106">This article helps you install and use the solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="2b13d-107">이 솔루션은 배포된 서버 인프라 관련 우선순위가 지정된 권장 사항 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-107">This solution provides a prioritized list of recommendations specific to your deployed server infrastructure.</span></span> <span data-ttu-id="2b13d-108">권장 사항은 신속하게 위험을 이해하고 조치를 취할 수 있도록 네 가지 주요 영역으로 분류되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-108">The recommendations are categorized across four focus areas, which help you quickly understand the risk and take action.</span></span>

<span data-ttu-id="2b13d-109">권장 사항은 수천 번의 고객 방문에서 Microsoft 엔지니어가 얻은 지식과 경험을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-109">The recommendations are based on the knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="2b13d-110">각 권장 사항은 문제가 중요할 수 있는 이유 및 제안된 변경 내용을 구현하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-110">Each recommendation provides guidance about why an issue might matter to you and how to implement the suggested changes.</span></span>

<span data-ttu-id="2b13d-111">조직에 가장 중요한 주요 영역을 선택하여 위험이 없는 정상 환경을 실행 중인 프로그램의 진행을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-111">You can choose focus areas that are most important to your organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="2b13d-112">솔루션을 추가하고 평가가 완료되면 주요 영역의 요약 정보가 사용자 환경의 인프라에 대한 **AD 평가** 대시보드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-112">After you've added the solution and an assessment is completed, summary information for focus areas is shown on the **AD Assessment** dashboard for the infrastructure in your environment.</span></span> <span data-ttu-id="2b13d-113">다음 섹션에서는 **AD 평가** 대시보드의 정보를 사용하는 방법을 설명합니다. 이 대시보드의 정보를 보고 Active Directory 서버 인프라에 대한 권장 조치를 취할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-113">The following sections describe how to use the information on the **AD Assessment** dashboard, where you can view and then take recommended actions for your Active Directory server infrastructure.</span></span>

![SQL 평가 타일의 이미지](./media/log-analytics-ad-assessment/ad-tile.png)

![SQL 평가 대시보드의 이미지](./media/log-analytics-ad-assessment/ad-assessment.png)

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="2b13d-116">솔루션 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="2b13d-116">Installing and configuring the solution</span></span>
<span data-ttu-id="2b13d-117">다음 정보를 사용하여 솔루션을 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-117">Use the following information to install and configure the solutions.</span></span>

* <span data-ttu-id="2b13d-118">평가할 도메인의 구성원인 도메인 컨트롤러에 에이전트를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-118">Agents must be installed on domain controllers that are members of the domain to be evaluated.</span></span>
* <span data-ttu-id="2b13d-119">Active Directory 평가 솔루션을 사용하려면 OMS 에이전트가 있는 각 컴퓨터에 지원되는 버전의 .NET Framework 4(4.5.2 이상)를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-119">The Active Directory Assessment solution requires a supported version of .NET Framework 4 (4.5.2 or above) installed on each computer that has an OMS agent.</span></span>
* <span data-ttu-id="2b13d-120">[Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ADAssessmentOMS?tab=Overview)에서 또는 [솔루션 갤러리에서 Log Analytics 솔루션 추가](log-analytics-add-solutions.md)에서 설명하는 프로세스를 사용하여 OMS 작업 영역에 Active Directory 평가 솔루션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-120">Add the Active Directory Assessment solution to your OMS workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ADAssessmentOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>  <span data-ttu-id="2b13d-121">추가 구성은 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-121">There is no further configuration required.</span></span>

  > [!NOTE]
  > <span data-ttu-id="2b13d-122">솔루션을 추가하면 에이전트가 있는 서버에 AdvisorAssessment.exe 파일이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-122">After you've added the solution, the AdvisorAssessment.exe file is added to servers with agents.</span></span> <span data-ttu-id="2b13d-123">구성 데이터가 판독되고 처리를 위해 클라우드의 OMS 서비스로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-123">Configuration data is read and then sent to the OMS service in the cloud for processing.</span></span> <span data-ttu-id="2b13d-124">논리는 수신된 데이터에 적용되며 클라우드 서비스는 데이터를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-124">Logic is applied to the received data and the cloud service records the data.</span></span>
  >
  >

## <a name="active-directory-assessment-data-collection-details"></a><span data-ttu-id="2b13d-125">Active Directory 평가 데이터 수집 정보</span><span class="sxs-lookup"><span data-stu-id="2b13d-125">Active Directory Assessment data collection details</span></span>

<span data-ttu-id="2b13d-126">Active Directory 평가는 사용자가 사용하도록 설정한 에이전트를 통해 다음과 같은 소스에서 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-126">Active Directory Assessment collects data from the following sources using the agents that you have enabled:</span></span>

- <span data-ttu-id="2b13d-127">레지스트리 수집기</span><span class="sxs-lookup"><span data-stu-id="2b13d-127">Registry collectors</span></span>
- <span data-ttu-id="2b13d-128">LDAP 수집기</span><span class="sxs-lookup"><span data-stu-id="2b13d-128">LDAP collectors</span></span>
- <span data-ttu-id="2b13d-129">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="2b13d-129">.NET Framework</span></span>
- <span data-ttu-id="2b13d-130">이벤트 로그 수집기</span><span class="sxs-lookup"><span data-stu-id="2b13d-130">Event log collectors</span></span>
- <span data-ttu-id="2b13d-131">ADSI(Active Directory 서비스 인터페이스)</span><span class="sxs-lookup"><span data-stu-id="2b13d-131">Active Directory Service interfaces (ADSI)</span></span>
- <span data-ttu-id="2b13d-132">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="2b13d-132">Windows PowerShell</span></span>
- <span data-ttu-id="2b13d-133">파일 데이터 수집기</span><span class="sxs-lookup"><span data-stu-id="2b13d-133">File data collectors</span></span>
- <span data-ttu-id="2b13d-134">WMI(Windows Management Instrumentation)</span><span class="sxs-lookup"><span data-stu-id="2b13d-134">Windows Management Instrumentation (WMI)</span></span>
- <span data-ttu-id="2b13d-135">DCDIAG 도구 API</span><span class="sxs-lookup"><span data-stu-id="2b13d-135">DCDIAG tool API</span></span>
- <span data-ttu-id="2b13d-136">NTFRS(파일 복제 서비스) API</span><span class="sxs-lookup"><span data-stu-id="2b13d-136">File Replication Service (NTFRS) API</span></span>
- <span data-ttu-id="2b13d-137">사용자 지정 C# 코드</span><span class="sxs-lookup"><span data-stu-id="2b13d-137">Custom C# code</span></span>


<span data-ttu-id="2b13d-138">다음 표에는 에이전트에 대한 데이터 수집 방법, Operations Manager(SCOM)가 필요한지 여부 및 에이전트에서 데이터가 수집되는 빈도가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-138">The following table shows data collection methods for agents, whether Operations Manager (SCOM) is required, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="2b13d-139">플랫폼</span><span class="sxs-lookup"><span data-stu-id="2b13d-139">platform</span></span> | <span data-ttu-id="2b13d-140">직접 에이전트</span><span class="sxs-lookup"><span data-stu-id="2b13d-140">Direct Agent</span></span> | <span data-ttu-id="2b13d-141">SCOM 에이전트</span><span class="sxs-lookup"><span data-stu-id="2b13d-141">SCOM agent</span></span> | <span data-ttu-id="2b13d-142">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="2b13d-142">Azure Storage</span></span> | <span data-ttu-id="2b13d-143">SCOM 필요?</span><span class="sxs-lookup"><span data-stu-id="2b13d-143">SCOM required?</span></span> | <span data-ttu-id="2b13d-144">관리 그룹을 통해 전송되는 SCOM 에이전트 데이터</span><span class="sxs-lookup"><span data-stu-id="2b13d-144">SCOM agent data sent via management group</span></span> | <span data-ttu-id="2b13d-145">수집 빈도</span><span class="sxs-lookup"><span data-stu-id="2b13d-145">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="2b13d-146">Windows</span><span class="sxs-lookup"><span data-stu-id="2b13d-146">Windows</span></span> |<span data-ttu-id="2b13d-147">&#8226;</span><span class="sxs-lookup"><span data-stu-id="2b13d-147">&#8226;</span></span> |<span data-ttu-id="2b13d-148">&#8226;</span><span class="sxs-lookup"><span data-stu-id="2b13d-148">&#8226;</span></span> |  |  |<span data-ttu-id="2b13d-149">&#8226;</span><span class="sxs-lookup"><span data-stu-id="2b13d-149">&#8226;</span></span> |<span data-ttu-id="2b13d-150">7 일</span><span class="sxs-lookup"><span data-stu-id="2b13d-150">7 days</span></span> |

## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="2b13d-151">권장 사항 우선 순위 이해</span><span class="sxs-lookup"><span data-stu-id="2b13d-151">Understanding how recommendations are prioritized</span></span>
<span data-ttu-id="2b13d-152">작성된 모든 권장 구성은 권장 사항의 상대적 중요도를 식별하는 가중치 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-152">Every recommendation made is given a weighting value that identifies the relative importance of the recommendation.</span></span> <span data-ttu-id="2b13d-153">10개의 가장 중요한 권장 사항만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-153">Only the 10 most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="2b13d-154">가중치 계산 방법</span><span class="sxs-lookup"><span data-stu-id="2b13d-154">How weights are calculated</span></span>
<span data-ttu-id="2b13d-155">가중치는 3개의 주요 요인을 기반으로 하는 집계 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-155">Weightings are aggregate values based on three key factors:</span></span>

* <span data-ttu-id="2b13d-156">식별된 문제로 인해 문제가 발생될 수 있는 *확률*입니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-156">The *probability* that an issue identified causes problems.</span></span> <span data-ttu-id="2b13d-157">확률이 높을수록 권장 사항에 대한 전체 점수가 커집니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-157">A higher probability equates to a larger overall score for the recommendation.</span></span>
* <span data-ttu-id="2b13d-158">문제가 발생된 경우 조직에 대한 문제의 *영향* 입니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-158">The *impact* of the issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="2b13d-159">영향이 높을수록 권장 사항에 대한 전체 점수가 커집니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-159">A higher impact equates to a larger overall score for the recommendation.</span></span>
* <span data-ttu-id="2b13d-160">권장 구성을 구현하는 데 필요한 *노력* 입니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-160">The *effort* required to implement the recommendation.</span></span> <span data-ttu-id="2b13d-161">노력이 높을수록 권장 사항에 대한 전체 점수가 작아집니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-161">A higher effort equates to a smaller overall score for the recommendation.</span></span>

<span data-ttu-id="2b13d-162">각 권장 사항에 대한 가중치는 각 주요 영역에 사용할 수 있는 총 점수에 대한 백분율로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-162">The weighting for each recommendation is expressed as a percentage of the total score available for each focus area.</span></span> <span data-ttu-id="2b13d-163">예를 들어, 보안 및 규정 준수 주요 영역의 권장 사항의 점수가 5%라면, 해당 권장 사항 구현에는 전체 보안 및 규정 준수 점수에서 5%가 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-163">For example, if a recommendation in the Security and Compliance focus area has a score of 5%, implementing that recommendation increases your overall Security and Compliance score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="2b13d-164">주요 영역</span><span class="sxs-lookup"><span data-stu-id="2b13d-164">Focus areas</span></span>
<span data-ttu-id="2b13d-165">**보안 및 규정 준수** - 이 주요 영역은 잠재적 보안 위협 및 위반, 회사 정책, 기술, 법률 및 규정 준수 요구 사항 등에 대한 권장 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-165">**Security and Compliance** - This focus area shows recommendations for potential security threats and breaches, corporate policies, and technical, legal and regulatory compliance requirements.</span></span>

<span data-ttu-id="2b13d-166">**가용성 및 비즈니스 연속성** - 이 주요 영역은 서비스 가용성, 인프라 복원성 및 비즈니스 보호에 대한 권장 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-166">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="2b13d-167">**성능 및 확장성** - 이 주요 영역은 조직의 IT 인프라를 확장하고, IT 환경이 현재 성능 요구 사항을 충족하며, 변화하는 인프라 요구 사항에 대응할 수 있도록 하는 데 도움이 되는 권장 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-167">**Performance and Scalability** - This focus area shows recommendations to help your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able to respond to changing infrastructure needs.</span></span>

<span data-ttu-id="2b13d-168">**업그레이드, 마이그레이션 및 배포** - 이 주요 영역은 기존 인프라를 업그레이드 및 마이그레이션하고 Active Directory를 배포하는 데 도움이 되는 권장 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-168">**Upgrade, Migration and Deployment** - This focus area shows recommendations to help you upgrade, migrate, and deploy Active Directory to your existing infrastructure.</span></span>

### <a name="should-you-aim-to-score-100-in-every-focus-area"></a><span data-ttu-id="2b13d-169">모든 주요 영역에서 100%의 점수를 목표로 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="2b13d-169">Should you aim to score 100% in every focus area?</span></span>
<span data-ttu-id="2b13d-170">그럴 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-170">Not necessarily.</span></span> <span data-ttu-id="2b13d-171">권장 사항은 수천 번의 고객 방문에서 Microsoft 엔지니어가 얻은 지식과 경험을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-171">The recommendations are based on the knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="2b13d-172">그러나 두 서버 인프라는 동일하지 않으며 특정 권장 사항은 거의 사용자와 관련 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-172">However, no two server infrastructures are the same, and specific recommendations may be more or less relevant to you.</span></span> <span data-ttu-id="2b13d-173">예를 들어, 가상 컴퓨터가 인터넷에 노출되지 않는 경우 일부 보안 권장 사항의 관련성은 떨어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-173">For example, some security recommendations might be less relevant if your virtual machines are not exposed to the Internet.</span></span> <span data-ttu-id="2b13d-174">일부 가용성 권장 사항은 우선순위가 낮은 임시 데이터 수집 및 보고를 제공하는 서비스와는 관련성이 떨어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-174">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="2b13d-175">성숙한 비즈니스에 중요한 문제는 시작에 덜 중요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-175">Issues that are important to a mature business may be less important to a start-up.</span></span> <span data-ttu-id="2b13d-176">우선하는 주요 영역을 식별하고 시간이 지남에 따라 다음 점수가 어떻게 변경되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-176">You may want to identify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="2b13d-177">모든 권장 사항에는 중요한 이유에 대한 지침이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-177">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="2b13d-178">IT 서비스의 특성 및 조직의 비즈니스 요구를 고려해 볼 때, 이 가이드를 사용하여 권장 사항 구현이 사용자에 적절한지 여부를 평가해야 합니다</span><span class="sxs-lookup"><span data-stu-id="2b13d-178">You should use this guidance to evaluate whether implementing the recommendation is appropriate for you, given the nature of your IT services and the business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="2b13d-179">평가 주요 영역 권장 사항 사용</span><span class="sxs-lookup"><span data-stu-id="2b13d-179">Use assessment focus area recommendations</span></span>
<span data-ttu-id="2b13d-180">OMS에서 평가 솔루션을 사용하려면 먼저 솔루션이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-180">Before you can use an assessment solution in OMS, you must have the solution installed.</span></span> <span data-ttu-id="2b13d-181">솔루션 설치에 대한 자세한 내용은 [솔루션 갤러리에서 Log Analytics 솔루션 추가](log-analytics-add-solutions.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2b13d-181">To read more about installing solutions, see [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="2b13d-182">설치 후 OMS의 개요 페이지에서 평가 타일을 사용하여 권장 사항의 요약을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-182">After it is installed, you can view the summary of recommendations by using the Assessment tile on the Overview page in OMS.</span></span>

<span data-ttu-id="2b13d-183">인프라에 대한 요약된 규정 준수 평가를 본 다음 세부 권장 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-183">View the summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="to-view-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="2b13d-184">주요 영역에 대한 권장 사항을 보고 수정 작업을 수행하려면</span><span class="sxs-lookup"><span data-stu-id="2b13d-184">To view recommendations for a focus area and take corrective action</span></span>
1. <span data-ttu-id="2b13d-185">**개요** 페이지에서 서버 인프라에 대한 **평가** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-185">On the **Overview** page, click the **Assessment** tile for your server infrastructure.</span></span>
2. <span data-ttu-id="2b13d-186">**평가** 페이지에서, 주요 영역 블레이드 중 하나에 있는 요약 정보를 검토한 다음 하나를 클릭하여 해당 주요 영역에 대한 권장 사항을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-186">On the **Assessment** page, review the summary information in one of the focus area blades and then click one to view recommendations for that focus area.</span></span>
3. <span data-ttu-id="2b13d-187">주요 영역 페이지에서 사용자 환경에 대해 우선순위가 지정된 권장 사항을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-187">On any of the focus area pages, you can view the prioritized recommendations made for your environment.</span></span> <span data-ttu-id="2b13d-188">권장하는 이유에 대한 세부 정보를 보려면 **영향을 받는 개체** 아래에서 해당 권장 사항을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-188">Click a recommendation under **Affected Objects** to view details about why the recommendation is made.</span></span>  
    <span data-ttu-id="2b13d-189">![평가 권장 사항의 이미지](./media/log-analytics-ad-assessment/ad-focus.png)</span><span class="sxs-lookup"><span data-stu-id="2b13d-189">![image of Assessment recommendations](./media/log-analytics-ad-assessment/ad-focus.png)</span></span>
4. <span data-ttu-id="2b13d-190">**권장 조치**에 제안된 올바른 조치를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-190">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="2b13d-191">항목이 처리되면, 이후 평가는 수행된 권장 조치 및 늘어난 규정 준수 점수를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-191">When the item has been addressed, later assessments records that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="2b13d-192">수정된 항목은 **전달된 개체**로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-192">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="2b13d-193">권장 사항 무시</span><span class="sxs-lookup"><span data-stu-id="2b13d-193">Ignore recommendations</span></span>
<span data-ttu-id="2b13d-194">무시하려는 권장 사항이 있는 경우 OMS에서 평가 결과에 권장 사항이 표시되는 것을 방지하는 데 사용할 텍스트 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-194">If you have recommendations that you want to ignore, you can create a text file that OMS will use to prevent recommendations from appearing in your assessment results.</span></span>

### <a name="to-identify-recommendations-that-you-will-ignore"></a><span data-ttu-id="2b13d-195">무시할 권장 사항을 식별하려면</span><span class="sxs-lookup"><span data-stu-id="2b13d-195">To identify recommendations that you will ignore</span></span>
1. <span data-ttu-id="2b13d-196">작업 영역에 로그인하고 로그 검색을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-196">Sign in to your workspace and open Log Search.</span></span> <span data-ttu-id="2b13d-197">다음 쿼리를 사용하여 사용자 환경의 컴퓨터에 대해 실패한 권장 사항을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-197">Use the following query to list recommendations that have failed for computers in your environment.</span></span>

   ```
   Type=ADAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
>[!NOTE]
> <span data-ttu-id="2b13d-198">작업 영역을 [새 Log Analytics 쿼리 언어](log-analytics-log-search-upgrade.md)로 업그레이드한 경우에는 위 쿼리가 다음과 같이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-198">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above query would change to the following.</span></span>
>
> `ADAssessmentRecommendation | where RecommendationResult == "Failed" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

   <span data-ttu-id="2b13d-199">로그 검색 쿼리를 보여 주는 스크린샷은 다음과 같습니다.![실패한 권장 사항](./media/log-analytics-ad-assessment/ad-failed-recommendations.png)</span><span class="sxs-lookup"><span data-stu-id="2b13d-199">Here's a screen shot showing the Log Search query: ![failed recommendations](./media/log-analytics-ad-assessment/ad-failed-recommendations.png)</span></span>
2. <span data-ttu-id="2b13d-200">무시할 권장 사항을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-200">Choose recommendations that you want to ignore.</span></span> <span data-ttu-id="2b13d-201">RecommendationId 값은 다음 절차에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-201">You’ll use the values for RecommendationId in the next procedure.</span></span>

### <a name="to-create-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="2b13d-202">IgnoreRecommendations.txt 텍스트 파일을 만들고 사용하려면</span><span class="sxs-lookup"><span data-stu-id="2b13d-202">To create and use an IgnoreRecommendations.txt text file</span></span>
1. <span data-ttu-id="2b13d-203">IgnoreRecommendations.txt라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-203">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="2b13d-204">Log Analytics에서 무시할 각 권장 사항에 대한 RecommendationId를 별도의 줄에 붙여 넣거나 입력한 다음 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-204">Paste or type each RecommendationId for each recommendation that you want Log Analytics to ignore on a separate line and then save and close the file.</span></span>
3. <span data-ttu-id="2b13d-205">OMS에서 권장 사항을 무시할 각 컴퓨터의 다음 폴더에 파일을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-205">Put the file in the following folder on each computer where you want OMS to ignore recommendations.</span></span>
   * <span data-ttu-id="2b13d-206">Microsoft Monitoring Agent(직접 또는 Operations Manager를 통해 연결됨)가 있는 컴퓨터 - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span><span class="sxs-lookup"><span data-stu-id="2b13d-206">On computers with the Microsoft Monitoring Agent (connected directly or through Operations Manager) - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span></span>
   * <span data-ttu-id="2b13d-207">Operations Manager 관리 서버 - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span><span class="sxs-lookup"><span data-stu-id="2b13d-207">On the Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span></span>

### <a name="to-verify-that-recommendations-are-ignored"></a><span data-ttu-id="2b13d-208">권장 사항이 무시되었는지 확인하려면</span><span class="sxs-lookup"><span data-stu-id="2b13d-208">To verify that recommendations are ignored</span></span>
<span data-ttu-id="2b13d-209">예약된 다음 평가가 실행된 후(기본적으로 7일마다) 지정된 권장 사항이 평가 대시보드에 *무시됨*으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-209">After the next scheduled assessment runs, by default every 7 days, the specified recommendations are marked *Ignored* and will not appear on the assessment dashboard.</span></span>

1. <span data-ttu-id="2b13d-210">다음 로그 검색 쿼리를 사용하여 무시된 모든 권장 사항을 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-210">You can use the following Log Search queries to list all the ignored recommendations.</span></span>

    ```
    Type=ADAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```
>[!NOTE]
> <span data-ttu-id="2b13d-211">작업 영역을 [새 Log Analytics 쿼리 언어](log-analytics-log-search-upgrade.md)로 업그레이드한 경우에는 위 쿼리가 다음과 같이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-211">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above query would change to the following.</span></span>
>
> `ADAssessmentRecommendation | where RecommendationResult == "Ignored" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

2. <span data-ttu-id="2b13d-212">무시된 권장 사항을 나중에 보려면 IgnoreRecommendations.txt 파일을 제거합니다. 또는 파일에서 RecommendationID를 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-212">If you decide later that you want to see ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="ad-assessment-solutions-faq"></a><span data-ttu-id="2b13d-213">AD 평가 솔루션 FAQ</span><span class="sxs-lookup"><span data-stu-id="2b13d-213">AD Assessment solutions FAQ</span></span>
<span data-ttu-id="2b13d-214">*얼마나 자주 평가를 실행하나요?*</span><span class="sxs-lookup"><span data-stu-id="2b13d-214">*How often does an assessment run?*</span></span>

* <span data-ttu-id="2b13d-215">평가는 7일마다 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-215">The assessment runs every 7 days.</span></span>

<span data-ttu-id="2b13d-216">*평가를 실행 빈도를 구성하는 방법이 있나요?*</span><span class="sxs-lookup"><span data-stu-id="2b13d-216">*Is there a way to configure how often the assessment runs?*</span></span>

* <span data-ttu-id="2b13d-217">지금은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-217">Not at this time.</span></span>

<span data-ttu-id="2b13d-218">*평가 솔루션을 추가한 후 다른 서버가 발견되면, 이 서버를 평가하나요?*</span><span class="sxs-lookup"><span data-stu-id="2b13d-218">*If another server for is discovered after I’ve added an assessment solution, will it be assessed?*</span></span>

* <span data-ttu-id="2b13d-219">예, 발견되면 그 시간부터 7일마다 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-219">Yes, once it is discovered it is assessed from then on, every 7 days.</span></span>

<span data-ttu-id="2b13d-220">*서버를 서비스 해제하는 경우 언제 평가에서 제거되나요?*</span><span class="sxs-lookup"><span data-stu-id="2b13d-220">*If a server is decommissioned, when will it be removed from the assessment?*</span></span>

* <span data-ttu-id="2b13d-221">3주 동안 서버가 데이터를 전송하지 않은 경우 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-221">If a server does not submit data for 3 weeks, it is removed.</span></span>

<span data-ttu-id="2b13d-222">*데이터 수집을 수행하는 프로세스의 이름은 무엇인가요?*</span><span class="sxs-lookup"><span data-stu-id="2b13d-222">*What is the name of the process that does the data collection?*</span></span>

* <span data-ttu-id="2b13d-223">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="2b13d-223">AdvisorAssessment.exe</span></span>

<span data-ttu-id="2b13d-224">*데이터를 수집하려면 시간이 얼마나 걸리나요?*</span><span class="sxs-lookup"><span data-stu-id="2b13d-224">*How long does it take for data to be collected?*</span></span>

* <span data-ttu-id="2b13d-225">서버에서의 실제 데이터 수집은 약 1시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-225">The actual data collection on the server takes about 1 hour.</span></span> <span data-ttu-id="2b13d-226">Active Directory 서버가 많은 서버에서는 더 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-226">It may take longer on servers that have a large number of Active Directory servers.</span></span>

<span data-ttu-id="2b13d-227">*데이터를 수집하는 경우 구성하는 방법이 있나요?*</span><span class="sxs-lookup"><span data-stu-id="2b13d-227">*Is there a way to configure when data is collected?*</span></span>

* <span data-ttu-id="2b13d-228">지금은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-228">Not at this time.</span></span>

<span data-ttu-id="2b13d-229">*왜 상위 10개의 권장 사항만을 표시하나요?*</span><span class="sxs-lookup"><span data-stu-id="2b13d-229">*Why display only the top 10 recommendations?*</span></span>

* <span data-ttu-id="2b13d-230">엄청난 소비적인 작업을 나열하는 대신, 먼저 우선순위가 지정된 권장 사항 해결에 주의를 기울이는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-230">Instead of giving you an exhaustive overwhelming list of tasks, we recommend that you focus on addressing the prioritized recommendations first.</span></span> <span data-ttu-id="2b13d-231">권장 사항을 해결한 후에 추가 권장 사항을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-231">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="2b13d-232">자세한 목록을 참조하는 것을 선호하는 경우 로그 검색을 사용하여 모든 권장 사항을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-232">If you prefer to see the detailed list, you can view all recommendations using Log Search.</span></span>

<span data-ttu-id="2b13d-233">*권장 사항을 무시하는 방법이 있나요?*</span><span class="sxs-lookup"><span data-stu-id="2b13d-233">*Is there a way to ignore a recommendation?*</span></span>

* <span data-ttu-id="2b13d-234">예, 위의 [권장 사항 무시](#ignore-recommendations) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2b13d-234">Yes, see [Ignore recommendations](#ignore-recommendations) section above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b13d-235">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2b13d-235">Next steps</span></span>
* <span data-ttu-id="2b13d-236">[Log Analytics에서 로그 검색](log-analytics-log-searches.md)을 사용하여 자세한 AD 평가 데이터 및 권장 사항을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b13d-236">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed AD Assessment data and recommendations.</span></span>
