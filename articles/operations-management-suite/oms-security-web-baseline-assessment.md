---
title: "Operations Management Suite 보안 및 감사 솔루션 기준의 초기 평가 aaaWeb | Microsoft Docs"
description: "이 문서에서는 toouse OMS 보안 및 감사 솔루션 tooperform 규정 준수 및 보안 용도 대 한 모든 모니터링 대상된 웹 서버에 대 한 초기 평가의 초기 평가 웹 하는 방법을 설명 합니다."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: yurid
ms.openlocfilehash: dafa9d3d93fae31748306b60ee40b285dd59c802
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="b4ef2-103">Operations Management Suite 보안 및 감사 솔루션의 웹 기준 평가</span><span class="sxs-lookup"><span data-stu-id="b4ef2-103">Web Baseline Assessment in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="b4ef2-104">이 문서를 사용 하면 OMS 보안을 사용 하 고 감사 웹 초기 평가 기능 tooaccess hello 보안 리소스 상태를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-104">This document helps you use OMS Security and Audit web baseline assessment capabilities tooaccess hello secure state of your monitored resources.</span></span>

## <a name="what-is-web-baseline-assessment"></a><span data-ttu-id="b4ef2-105">웹 기준 평가란?</span><span class="sxs-lookup"><span data-stu-id="b4ef2-105">What is web baseline assessment?</span></span>
<span data-ttu-id="b4ef2-106">현재 OMS 보안은 운영 체제에 대한 보안 기준 평가를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-106">Currently OMS Security provides security baseline assessment for operating systems.</span></span> <span data-ttu-id="b4ef2-107">24 시간 마다 서버 운영 체제 설정을 hello를 검색 하 고 잠재적으로 취약 한 설정에 대 한 뷰를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-107">It scans hello OS settings of your servers every 24 hours, and provides a view into potentially vulnerable settings.</span></span> <span data-ttu-id="b4ef2-108">이에 대한 자세한 내용은 [Operations Management Suite 보안 및 감사 솔루션의 기준 평가](https://docs.microsoft.com/azure/operations-management-suite/oms-security-baseline)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-108">Read [Baseline Assessment in Operations Management Suite Security and Audit Solution](https://docs.microsoft.com/azure/operations-management-suite/oms-security-baseline) for more information on this.</span></span>

<span data-ttu-id="b4ef2-109">hello hello 웹 초기 평가의 ´ ֲ toofind 잠재적으로 취약 한 웹 서버 설정.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-109">hello goal of hello Web Baseline assessment is toofind potentially vulnerable web server settings.</span></span> <span data-ttu-id="b4ef2-110">hello 웹 초기 구성에 대 한 기본 원본은 다음 세 가지 hello:.NET, ASP.NET 및 IIS 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-110">hello three primary sources for hello web baseline configurations are: .NET, ASP.NET, and IIS configuration.</span></span>  <span data-ttu-id="b4ef2-111">운영 시스템 초기 평가 hello, 처럼 OMS 보안은 사용 하겠습니다 tooscan 사용자 웹 서버에 24 시간 마다 하 고 그 중 보안 상태에 대 한 뷰를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-111">Just like hello operating system baseline assessment, OMS Security is going tooscan your web servers every 24hrs and provide a view into security state of them.</span></span>  <span data-ttu-id="b4ef2-112">인터넷 정보 서비스 (IIS), 구성은 하는 고도로 사용자 지정 가능한 재정의 된 다양 한 사이트 및 응용 프로그램 수준 toobe 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-112">In Internet Information Service (IIS), configurations are highly customizable, which allows various site and application levels toobe overridden.</span></span> <span data-ttu-id="b4ef2-113">hello 스캐너 추가 toohello 기본 루트 수준에서 각 응용 프로그램/사이트 수준에서 hello 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-113">hello scanner checks hello settings at each application/site level in addition toohello default root level.</span></span> <span data-ttu-id="b4ef2-114">Tooidentify 잠재적으로 취약 한 설정을 사용 하면 하 고 해당 설정 하기 위한 권장 사항 함께 신속 하 게 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-114">This helps you tooidentify potentially vulnerable settings and quickly remediate, along with our recommendations for those settings.</span></span>

>[!NOTE] 
><span data-ttu-id="b4ef2-115">Hello 일반적인 구성 식별자와이 OMS 보안에서 사용 하는 기준 규칙을 다운로드할 수 있습니다 [페이지](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335?redir=0)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-115">You can download hello Common Configuration Identifiers and Baseline Rules used by OMS Security in this [page](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335?redir=0).</span></span>


## <a name="web-security-baseline-assessment"></a><span data-ttu-id="b4ef2-116">웹 보안 기준 평가</span><span class="sxs-lookup"><span data-stu-id="b4ef2-116">Web security baseline assessment</span></span>

<span data-ttu-id="b4ef2-117">이 미리 보기에 대 한 hello 기능은 hello OMS 검색 옵션 및 hello OMS 보안 및 감사 대시보드를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-117">For this preview hello feature can be accessed via hello OMS Search option, and hello OMS Security and Audit Dashboard.</span></span> <span data-ttu-id="b4ef2-118">Tooperform appropriated hello 쿼리 아래 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-118">Follow hello steps below tooperform hello appropriated query:</span></span>

1. <span data-ttu-id="b4ef2-119">Hello에 **Microsoft Operations Management Suite** 기본 대시보드 클릭 **보안 및 감사** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-119">In hello **Microsoft Operations Management Suite** main dashboard, click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="b4ef2-120">Hello에 **보안 및 감사** 대시보드를 hello 웹 초기 관점 다음 toohello OS 초기 관점을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-120">In hello **Security and Audit** dashboard, you can see hello Web Baseline perspective next toohello OS baseline perspective.</span></span>
   
    ![OMS 보안 및 감사 웹 보안 기준 평가](./media/oms-security-web-baseline/oms-security-web-baseline-fig5.png)

3. <span data-ttu-id="b4ef2-122">왼쪽된 창의 hello 모든 평가 hello 서버에 전달 하는 규칙의 hello 평균 백분율 및 평가 된 서버 hello 목록, 비교 하는 웹 서버 toohello 기준 hello 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-122">hello left pane shows hello number of Web Servers compared toohello baseline, hello average percentage of rules that passed on all hello evaluated servers, and hello list of Servers that were assessed.</span></span>
4. <span data-ttu-id="b4ef2-123">hello 오른쪽 창에는 고유한 hello 나열 하 여 실패 한 규칙 *심각도*, 및 *RuleType*합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-123">hello right pane lists hello unique rules that failed by *Severity*, and *RuleType*.</span></span> <span data-ttu-id="b4ef2-124">Hello 오른쪽 창 규칙 중 하나를 클릭 하면 해당 규칙의 hello 세부 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-124">Clicking on any of hello right pane rules will show hello details of that rule.</span></span> <span data-ttu-id="b4ef2-125">예제는 hello 이미지 아래에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-125">An example is shown in hello below image.</span></span> <span data-ttu-id="b4ef2-126">계산 되는 hello 규칙 아래에 나열 됩니다 *규칙 설정*합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-126">hello rule that is evaluated is listed under *Rule Setting*.</span></span> <span data-ttu-id="b4ef2-127">hello *AzId* 필드는 추적 hello 기준 규칙에 대 한 Microsoft에서 사용 되는 각 규칙에 대 한 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-127">hello *AzId* field which is a unique identifier for each rule used by Microsoft for tracking hello baseline rules.</span></span> <span data-ttu-id="b4ef2-128">또한 toothat 사용자 hello를 볼 수 *예상 결과* (Microsoft의 권장 값), 및 기타 세부 정보 hello 규칙의 hello 보안 영향에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-128">In addition toothat users can see hello *Expected Result* (Microsoft’s recommended value), and other details regarding hello security impact of hello rule.</span></span>
    
    ![쿼리](./media/oms-security-web-baseline/oms-security-web-baseline-fig6.png)

5. <span data-ttu-id="b4ef2-130">Tooreview hello 결과 사용자가 직접 쿼리를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-130">You can create your own queries tooreview hello results.</span></span> 

<span data-ttu-id="b4ef2-131">사용할 수 있는 hello 첫 번째 쿼리는 hello **웹 초기 평가 요약**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-131">hello first query that you can use is hello **Web Baseline Assessment Summary**.</span></span> <span data-ttu-id="b4ef2-132">Hello에 **검색 시작** 필드에서이 쿼리를 입력: *유형 = SecurityBaselineSummary BaselineType 웹 =*합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-132">In hello **Begin search here** field, type this query: *Type=SecurityBaselineSummary BaselineType=Web*.</span></span> <span data-ttu-id="b4ef2-133">hello 다음은 출력 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-133">hello following is an output sample:</span></span>

![쿼리 결과](./media/oms-security-web-baseline/oms-security-web-baseline-fig7.png)

>[!NOTE] 
><span data-ttu-id="b4ef2-135">이 쿼리에서 각 레코드는 단일 서버에 대한 요약 평가를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-135">In this query, each record indicates assessment summary on a single server.</span></span>

<span data-ttu-id="b4ef2-136">Hello에 있는 경우 **로그 검색**을 각각 다른 쿼리에 tooobtain hello 웹 초기 평가 대 한 자세한 정보를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-136">Once you are in hello **Log Search**, you can type different queries tooobtain more information about hello web baseline assessment.</span></span> <span data-ttu-id="b4ef2-137">또한 toohello 이전 쿼리를 사용할 수도 있습니다이 미리 보기에서 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="b4ef2-137">In addition toohello previous query, you can also use hello following ones in this preview:</span></span>

<span data-ttu-id="b4ef2-138">**웹 기준 규칙 평가**: 각 레코드는 단일 서버에서 단일 웹 기준 규칙 평가를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-138">**Web Baseline Rule Assessment**: Each record represents a single web baseline rule evaluation on a single server.</span></span> <span data-ttu-id="b4ef2-139">데이터를 포함 모든 실패 한 규칙에 대 한 hello *SitePath* 어떤 hello에 규칙이 확인 되었고, hello *예상 결과*, 및 hello *실제 결과*합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-139">It includes all data for a failed rule, hello *SitePath* on which hello rule was evaluated, hello *Expected Result*, and hello *Actual Result*.</span></span>

<span data-ttu-id="b4ef2-140">쿼리: *Type=SecurityBaseline BaselineType=Web AnalyzeResult=Failed*</span><span class="sxs-lookup"><span data-stu-id="b4ef2-140">Query: *Type=SecurityBaseline BaselineType=Web AnalyzeResult=Failed*</span></span>

![쿼리 결과 2](./media/oms-security-web-baseline/oms-security-web-baseline-fig8.png)

<span data-ttu-id="b4ef2-142">**특정 서버에 대 한 모든 결과 표시**:이 쿼리에서 toosee 발생 하는 방법을 보여 줍니다. 특정 서버의: 쿼리: *형식 SecurityBaseline BaselineType = = 웹 컴퓨터 BaselineTestVM1 =*</span><span class="sxs-lookup"><span data-stu-id="b4ef2-142">**Show all results for a specific server**: This query shows how toosee results of a specific server: Query: *Type=SecurityBaseline BaselineType=Web Computer=BaselineTestVM1*</span></span>

![쿼리 결과 3](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

<span data-ttu-id="b4ef2-144">이러한 레코드/쿼리 toocreate 고유한 대시보드, 보고서 또는 경고에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-144">You can use these records/queries toocreate your own dashboards, reports, or alerts.</span></span> <span data-ttu-id="b4ef2-145">다음은 샘플 UI 컨트롤 tooyour 대시보드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-145">Here is a sample UI control that you can add tooyour dashboard.</span></span> <span data-ttu-id="b4ef2-146">학습할 수 있는 방법을 toovisualize OMS 뷰 디자이너를 사용 하 여 데이터 [여기](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-146">You can learn how toovisualize your data using OMS View Designer [here](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span></span> <span data-ttu-id="b4ef2-147">hello 아래 화면은이 사용자 지정 확인 되 면 hello 타일 방법의 예는 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-147">hello screen below is an example of how hello tile will look like once you make this customization.</span></span>

![dashboard](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

## <a name="see-also"></a><span data-ttu-id="b4ef2-149">참고 항목</span><span class="sxs-lookup"><span data-stu-id="b4ef2-149">See also</span></span>
<span data-ttu-id="b4ef2-150">이 문서에서는 OMS 보안 및 감사 웹 기준 평가에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="b4ef2-150">In this document, you learned about OMS Security and Audit Web Baseline assessment.</span></span> <span data-ttu-id="b4ef2-151">OMS 보안에 대해 자세히 toolearn hello 다음 문서 참조:</span><span class="sxs-lookup"><span data-stu-id="b4ef2-151">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="b4ef2-152">OMS(Operations Management Suite) 개요</span><span class="sxs-lookup"><span data-stu-id="b4ef2-152">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="b4ef2-153">모니터링 및 Operations Management Suite 보안 및 감사 솔루션에 응답 중 tooSecurity 경고</span><span class="sxs-lookup"><span data-stu-id="b4ef2-153">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="b4ef2-154">Operations Management Suite 보안 및 감사 솔루션의 리소스 모니터링</span><span class="sxs-lookup"><span data-stu-id="b4ef2-154">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

