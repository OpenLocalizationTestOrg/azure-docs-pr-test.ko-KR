---
title: "Operations Management Suite 보안 및 감사 솔루션 기준 | Microsoft Docs"
description: "이 문서에서는 OMS 보안 및 감사 솔루션을 사용하여 규정 준수 및 보안 목적을 위해 모니터링되는 모든 컴퓨터의 기준 평가를 수행하는 방법을 설명합니다."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: d538eee4dccdbf158baab8908ebfff56713bde95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="a0975-103">Operations Management Suite 보안 및 감사 솔루션의 기준 평가</span><span class="sxs-lookup"><span data-stu-id="a0975-103">Baseline Assessment in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="a0975-104">이 문서를 통해 [OMS(Operations Management Suite) 보안 및 감사 솔루션](operations-management-suite-overview.md) 기준 평가 기능을 사용하여 모니터링된 리소스의 보안 상태에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-104">This document helps you to use [Operations Management Suite (OMS) Security and Audit Solution](operations-management-suite-overview.md) baseline assessment capabilities to access the secure state of your monitored resources.</span></span>

## <a name="what-is-baseline-assessment"></a><span data-ttu-id="a0975-105">기준 평가란?</span><span class="sxs-lookup"><span data-stu-id="a0975-105">What is Baseline Assessment?</span></span>
<span data-ttu-id="a0975-106">전 세계 산업 및 정부 조직과 함께 Microsoft에서는 보안 수준이 높은 서버 배포를 나타내는 Windows 구성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-106">Microsoft, together with industry and government organizations worldwide, defines a Windows configuration that represents highly secure server deployments.</span></span> <span data-ttu-id="a0975-107">이 구성은 일련의 레지스트리 키, 감사 정책 설정 및 이러한 설정에 대한 Microsoft의 권장된 값과 함께 보안 정책 설정을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-107">This configuration is a set of registry keys, audit policy settings, and security policy settings along with Microsoft’s recommended values for these settings.</span></span> <span data-ttu-id="a0975-108">이러한 규칙 집합을 보안 기준이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-108">This set of rules is known as Security baseline.</span></span> <span data-ttu-id="a0975-109">OMS 보안 및 감사 초기 평가 기능은 규정 준수를 위해 모든 컴퓨터를 원활하게 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-109">OMS Security and Audit baseline assessment capability can seamlessly scan all your computers for compliance.</span></span> 

<span data-ttu-id="a0975-110">세 가지 유형의 규칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-110">There are three types of rules:</span></span>

* <span data-ttu-id="a0975-111">**레지스트리 규칙**: 레지스트리 키가 올바르게 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-111">**Registry rules**: check that registry keys are set correctly.</span></span>
* <span data-ttu-id="a0975-112">**감사 정책 규칙**: 감사 정책과 관한 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-112">**Audit policy rules**: rules regarding your audit policy.</span></span>
* <span data-ttu-id="a0975-113">**보안 정책 규칙**: 컴퓨터에 대한 사용자의 사용 권한에 관한 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-113">**Security policy rules**: rules regarding the user’s permissions on the machine.</span></span>

> [!NOTE]
> <span data-ttu-id="a0975-114">이 기능의 간략한 개요는 [OMS 보안을 사용하여 보안 구성 기준 평가](https://blogs.technet.microsoft.com/msoms/2016/08/12/use-oms-security-to-assess-the-security-configuration-baseline/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0975-114">Read [Use OMS Security to assess the Security Configuration Baseline](https://blogs.technet.microsoft.com/msoms/2016/08/12/use-oms-security-to-assess-the-security-configuration-baseline/) for a brief overview of this feature.</span></span>
> 
> 

## <a name="security-baseline-assessment"></a><span data-ttu-id="a0975-115">보안 기준 평가</span><span class="sxs-lookup"><span data-stu-id="a0975-115">Security Baseline Assessment</span></span>
<span data-ttu-id="a0975-116">대시보드를 사용하여 OMS 보안 및 감사에서 모니터링되는 모든 컴퓨터에 대한 현재 보안 기준 평가를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-116">You can review your current security baseline assessment for all computers that are monitored by OMS Security and Audit using the dashboard.</span></span>  <span data-ttu-id="a0975-117">보안 기준 평가 대시보드에 액세스하려면 다음 단계를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-117">Execute the following steps to access the security baseline assessment dashboard:</span></span>

1. <span data-ttu-id="a0975-118">**Microsoft Operations Management Suite** 기본 대시보드에서 **보안 및 감사** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-118">In the **Microsoft Operations Management Suite** main dashboard, click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="a0975-119">**보안 및 감사** 대시보드에서 **보안 도메인**의 **기준 평가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-119">In the **Security and Audit** dashboard, click **Baseline Assessment** under **Security Domains**.</span></span> <span data-ttu-id="a0975-120">다음 이미지처럼 **보안 기준 평가** 대시보드가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-120">The **Security Baseline Assessment** dashboard appears as shown in the following image:</span></span>
   
    ![OMS 보안 및 감사 기준 평가](./media/oms-security-baseline/oms-security-baseline-fig1.png)

<span data-ttu-id="a0975-122">이 대시보드는 세 가지 주요 영역으로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-122">This dashboard is divided in three major areas:</span></span>

* <span data-ttu-id="a0975-123">**컴퓨터를 기준에 비교**: 이 섹션에서는 액세스된 컴퓨터 수 및 평가를 통과한 컴퓨터 비율을 요약하여 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-123">**Computers compared to baseline**: this section gives a summary of the number of computers that were accessed and the percentage of computers that passed the assessment.</span></span> <span data-ttu-id="a0975-124">또한 평가에 대해 상위 10개의 컴퓨터 및 백분율 결과를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-124">It also gives the top 10 computers and the percentage result for the assessment.</span></span>
* <span data-ttu-id="a0975-125">**필수 규칙 상태**: 이 섹션에서는 심각도별 실패한 규칙 및 유형별 실패한 규칙을 알아보려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-125">**Required Rules Status**: this section has the intent to bring awareness of the failed rules by severity and failed rules by type.</span></span> <span data-ttu-id="a0975-126">첫 번째 그래프를 확인하여 대부분의 실패한 규칙이 중요한지 아닌지를 신속하게 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-126">By looking to the first graph you can quickly identify if most the failed rules are critical, or not.</span></span> <span data-ttu-id="a0975-127">또한 상위 10개의 실패한 규칙 및 심각도 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-127">It also gives a list of the top 10 failed rules and their severity.</span></span> <span data-ttu-id="a0975-128">두 번째 그래프에서는 평가하는 동안 실패한 규칙의 유형을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-128">The second graph shows the type of rule that failed during the assessment.</span></span> 
* <span data-ttu-id="a0975-129">**기준 평가가 누락된 컴퓨터**:이 섹션에서는 운영 체제 비호환성 또는 오류로 인해 액세스되지 않는 컴퓨터를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-129">**Computers missing baseline assessment**: this section list the computers that were not accessed due to operating system incompatibility or failures.</span></span> 

### <a name="accessing-computers-compared-to-baseline"></a><span data-ttu-id="a0975-130">기준에 비교한 컴퓨터에 액세스</span><span class="sxs-lookup"><span data-stu-id="a0975-130">Accessing computers compared to baseline</span></span>
<span data-ttu-id="a0975-131">이상적으로 모든 컴퓨터는 보안 기준 평가와 호환되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-131">Ideally all your computers are be compliant with the security baseline assessment.</span></span> <span data-ttu-id="a0975-132">그러나 어떤 상황에서는 호환되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-132">However it is expected that in some circumstances this doesn't happen.</span></span> <span data-ttu-id="a0975-133">보안 관리 프로세스의 일부로 보안 평가 테스트를 모두 통과하지 못한 컴퓨터를 검토하는 작업을 포함하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-133">As part of the security management process, it is important to include reviewing the computers that failed to pass all security assessment tests.</span></span> <span data-ttu-id="a0975-134">이를 신속하게 시각화하려면 **기준에 비교한 컴퓨터** 섹션에 있는 **액세스한 컴퓨터** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-134">A quick way to visualize that is by selecting the option **Computers accessed** located in the **Computers compared to baseline** section.</span></span> <span data-ttu-id="a0975-135">다음 화면에서 볼 수 있듯이 컴퓨터의 목록을 보여 주는 로그 검색 결과가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-135">You should see the log search result showing the list of computers as shows in the following screen:</span></span>

![컴퓨터가 액세스한 결과](./media/oms-security-baseline/oms-security-baseline-fig2.png)

<span data-ttu-id="a0975-137">검색 결과가 테이블 형식으로 표시되며 여기서 첫 번째 열에는 컴퓨터 이름이 표시되고 두 번째 열에는 실패한 규칙 수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-137">The search result is shown in a table format, where the first column has the computer name and the second color has the number of rules that failed.</span></span> <span data-ttu-id="a0975-138">실패한 규칙의 종류에 대한 정보를 검색하려면 컴퓨터 이름 외에도 실패한 규칙 수를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-138">To retrieve the information regarding the type of rule that failed, click in the number of failed rules besides the computer name.</span></span> <span data-ttu-id="a0975-139">다음 이미지에 나와 있는 것과 같은 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-139">You should see a result similar to the one shown in the following image:</span></span>

![컴퓨터가 액세스한 결과 세부 정보](./media/oms-security-baseline/oms-security-baseline-fig3.png)

<span data-ttu-id="a0975-141">이 검색 결과에는 액세스된 규칙, 실패한 중요한 규칙 수, 경고 규칙 및 정보가 실패한 규칙의 합계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-141">In this search result, you have the total of accessed rules, the number of critical rules that failed, the warning rules and the information failed rules.</span></span>

### <a name="accessing-required-rules-status"></a><span data-ttu-id="a0975-142">필수 규칙 상태 액세스</span><span class="sxs-lookup"><span data-stu-id="a0975-142">Accessing required rules status</span></span>
<span data-ttu-id="a0975-143">평가를 통과한 컴퓨터의 백분율에 관한 정보를 가져온 후에 중요도에 따라 실패하는 규칙에 대한 자세한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-143">After obtaining the information regarding the percentage number of computers that passed the assessment, you may want to obtain more information about which rules are failing according to the criticality.</span></span> <span data-ttu-id="a0975-144">이 시각화를 통해 다음 평가에서 먼저 호환될 컴퓨터를 결정하도록 우선 순위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-144">This visualization helps you to prioritize which computers should be addressed first to ensure they will be compliant in the next assessment.</span></span> <span data-ttu-id="a0975-145">**심각도별 실패한 규칙** 타일의 **필수 규칙 상태**에 있는 그래프의 중요한 부분 위로 마우스를 이동하고 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-145">Hover over the Critical part of the graph located in the **Failed rules by severity** tile, under **Required rules status** and click it.</span></span> <span data-ttu-id="a0975-146">다음 화면과 유사한 결과가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-146">You should see a result similar to the following screen:</span></span>

![심각도별 실패한 규칙 정보](./media/oms-security-baseline/oms-security-baseline-fig4.png) 

<span data-ttu-id="a0975-148">이 로그 결과에서 실패한 기준 규칙, 이 규칙의 설명 및 이 보안 규칙의 CCE(Common Configuration Enumeration) ID의 유형이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-148">In this log result you see the type of baseline rule that failed, the description of this rule, and the Common Configuration Enumeration (CCE) ID of this security rule.</span></span> <span data-ttu-id="a0975-149">이러한 특성은 대상 컴퓨터에서 이 문제를 해결하는 정정 작업을 충분히 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-149">These attributes should be enough to perform a corrective action to fix this problem in the target computer.</span></span>

> [!NOTE]
> <span data-ttu-id="a0975-150">CCE에 대한 자세한 정보는 [National Vulnerability Database](https://nvd.nist.gov/cce/index.cfm)에 액세스하세요.</span><span class="sxs-lookup"><span data-stu-id="a0975-150">For more information about CCE, access the [National Vulnerability Database](https://nvd.nist.gov/cce/index.cfm).</span></span>
> 
> 

### <a name="accessing-computers-missing-baseline-assessment"></a><span data-ttu-id="a0975-151">기준 평가가 누락된 컴퓨터에 액세스</span><span class="sxs-lookup"><span data-stu-id="a0975-151">Accessing computers missing baseline assessment</span></span>
<span data-ttu-id="a0975-152">OMS는 Windows Server 2008 R2에서 Windows Server 2012 R2까지 도메인 구성원 및 도메인 컨토롤러 기준 프로필을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-152">OMS supports the domain member and Domain Controller baseline profile on Windows Server 2008 R2 up to Windows Server 2012 R2.</span></span> <span data-ttu-id="a0975-153">Windows Server 2016 기준은 계획은 아직 최종본이 아니며 게시되는 즉시 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-153">Windows Server 2016 baseline isn’t final yet and will be added as soon as it is published.</span></span> <span data-ttu-id="a0975-154">OMS 보안 및 감사 기준 평가를 통해 검색된 다른 모든 운영 체제는 **기준 평가가 누락된 컴퓨터** 섹션에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-154">All other operating systems scanned via OMS Security and Audit baseline assessment appears under the **Computers missing baseline assessment** section.</span></span>

## <a name="see-also"></a><span data-ttu-id="a0975-155">참고 항목</span><span class="sxs-lookup"><span data-stu-id="a0975-155">See also</span></span>
<span data-ttu-id="a0975-156">이 문서에서는 OMS 보안 및 감사 기준 평가에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="a0975-156">In this document, you learned about OMS Security and Audit baseline assessment.</span></span> <span data-ttu-id="a0975-157">OMS 보안에 대해 자세히 알아보려면 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0975-157">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="a0975-158">OMS(Operations Management Suite) 개요</span><span class="sxs-lookup"><span data-stu-id="a0975-158">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="a0975-159">Operations Management Suite 보안 및 감사 솔루션의 보안 경고 모니터링 및 응답</span><span class="sxs-lookup"><span data-stu-id="a0975-159">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="a0975-160">Operations Management Suite 보안 및 감사 솔루션의 리소스 모니터링</span><span class="sxs-lookup"><span data-stu-id="a0975-160">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

