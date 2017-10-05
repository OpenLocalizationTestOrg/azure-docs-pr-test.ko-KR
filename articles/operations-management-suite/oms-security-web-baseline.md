---
title: "Operations Management Suite 보안 및 감사 솔루션 웹 기준 | Microsoft Docs"
description: "이 문서에서는 OMS 보안 및 감사 솔루션을 사용하여 규정 준수 및 보안 목적을 위해 모니터링되는 모든 웹 서버의 웹 기준 평가를 수행하는 방법을 설명합니다."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ROBOTS: NOINDEX
redirect_url: https://www.microsoft.com/cloud-platform/security-and-compliance
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: 0d4707dc0c0ffbf40d0d10a6d12b9709a9655258
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="10b59-103">Operations Management Suite 보안 및 감사 솔루션의 웹 기준 평가</span><span class="sxs-lookup"><span data-stu-id="10b59-103">Web Baseline Assessment in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="10b59-104">이 문서를 통해 [OMS(Operations Management Suite) 보안 및 감사 솔루션](operations-management-suite-overview.md) 웹 기준 평가 기능을 사용하여 모니터링된 리소스의 보안 상태에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-104">This document helps you to use [Operations Management Suite (OMS) Security and Audit Solution](operations-management-suite-overview.md) web baseline assessment capabilities to access the secure state of your monitored resources.</span></span>

## <a name="what-is-web-baseline-assessment"></a><span data-ttu-id="10b59-105">웹 기준 평가란?</span><span class="sxs-lookup"><span data-stu-id="10b59-105">What is Web Baseline Assessment?</span></span>
<span data-ttu-id="10b59-106">현재 OMS 보안은 운영 체제에 대한 보안 기준 평가를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-106">Currently OMS Security provides security baseline assessment for operating systems.</span></span> <span data-ttu-id="10b59-107">24시간마다 서버의 운영 체제 설정을 검색하고 잠재적으로 취약한 설정에 대한 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-107">It scans the operating system settings of your servers every 24 hours and provides a view into potentially vulnerable settings.</span></span> <span data-ttu-id="10b59-108">이에 대한 자세한 내용은 [Operations Management Suite 보안 및 감사 솔루션의 기준 평가](oms-security-baseline.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="10b59-108">Read [Baseline Assessment in Operations Management Suite Security and Audit Solution](oms-security-baseline.md) for more information on this.</span></span>

<span data-ttu-id="10b59-109">웹 기준 평가의 목표는 잠재적으로 취약 한 웹 서버 설정을 찾는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-109">The goal of the web baseline assessment is to find potentially vulnerable web server settings.</span></span> <span data-ttu-id="10b59-110">웹 기준 구성에 대한 세 가지 기본 소스는 .NET, ASP.NET 및 IIS 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-110">The three primary sources for the web baseline configurations are: .NET, ASP.NET, and IIS configuration.</span></span>  <span data-ttu-id="10b59-111">운영 체제 기준 평가와 마찬가지로 OMS 보안은 24시간마다 웹 서버를 검색하고 그 중 보안 상태에 대한 보기를 제공하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-111">Just like the operating system baseline assessment, OMS Security is going to scan your web servers every 24hrs and provide a view into security state of them.</span></span>  <span data-ttu-id="10b59-112">IIS(인터넷 정보 서비스)에서 구성은 고도로 사용자 지정되어 다양한 사이트 및 응용 프로그램 수준을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-112">In Internet Information Service (IIS), configurations are highly customizable, which allows various site and application levels to be overridden.</span></span> <span data-ttu-id="10b59-113">스캐너는 기본 루트 수준 외에도 각 응용 프로그램/사이트 수준의 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-113">The scanner checks the settings at each application/site level in addition to the default root level.</span></span> <span data-ttu-id="10b59-114">그러면 잠재적인 취약점 설정 위치를 식별하고 신속하게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-114">This helps you to identify potential vulnerability settings locations and quickly remediate.</span></span>


## <a name="web-security-baseline-assessment"></a><span data-ttu-id="10b59-115">웹 보안 기준 평가</span><span class="sxs-lookup"><span data-stu-id="10b59-115">Web Security Baseline Assessment</span></span>
<span data-ttu-id="10b59-116">이 미리 보기에서는 OMS 검색 옵션을 사용하여 이 기능에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-116">For this preview this feature is going to be accessed using the OMS Search option.</span></span> <span data-ttu-id="10b59-117">아래의 단계를 수행하여 적절한 쿼리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-117">Follow the steps below to perform the appropriated query:</span></span>

1. <span data-ttu-id="10b59-118">**Microsoft Operations Management Suite** 기본 대시보드에서 **보안 및 감사** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-118">In the **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="10b59-119">**보안 및 감사** 대시보드에서 **로그 검색** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-119">In the **Security and Audit** dashboard, click **Log Search** button.</span></span>
3. <span data-ttu-id="10b59-120">사용할 수 있는 첫 번째 쿼리는 **웹 기준 평가 요약**입니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-120">The first query that you can use is the **Web Baseline Assessment Summary**.</span></span> <span data-ttu-id="10b59-121">**여기에서 검색 시작** 필드에서 다음 쿼리를 입력합니다. Type*=SecurityBaselineSummary BaselineType=web*</span><span class="sxs-lookup"><span data-stu-id="10b59-121">In the **Begin search here** field, type this query: Type*=SecurityBaselineSummary BaselineType=web*.</span></span> <span data-ttu-id="10b59-122">다음 화면에는 출력 샘플이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-122">The following screen has an output sample:</span></span>

![웹 기준 평가 요약](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> <span data-ttu-id="10b59-124">이 쿼리에서 각 레코드는 단일 서버에 대한 요약 평가를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-124">In this query, each record indicates assessment summary on a single server.</span></span>

<span data-ttu-id="10b59-125">**로그 검색**에 있는 경우 여러 쿼리를 입력하여 웹 기준 평가에 대한 자세한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-125">Once you are in the **Log Search**, you can type different queries to obtain more information about the web baseline assessment.</span></span> <span data-ttu-id="10b59-126">이 미리 보기에서는 이전 쿼리 외에도 다음과 같은 쿼리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-126">In addition to the previous query, you can also use the following ones in this preview.</span></span>

<span data-ttu-id="10b59-127">**웹 기준 규칙 평가**: 각 레코드는 단일 서버에서 단일 웹 기준 규칙 평가를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-127">**Web Baseline Rule Assessment**: Each record represents a single web baseline rule evaluation on a single server.</span></span> <span data-ttu-id="10b59-128">규칙, 위치, 예상된 결과 및 실제 결과의 모든 데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-128">It includes all data for the rule, location, the expected result, and the actual result.</span></span>

<span data-ttu-id="10b59-129">**쿼리**: Type*=SecurityBaseline BaselineType=web*</span><span class="sxs-lookup"><span data-stu-id="10b59-129">**Query**: Type*=SecurityBaseline BaselineType=web*</span></span>

![웹 기준 규칙 평가](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

<span data-ttu-id="10b59-131">**특정 서버의 모든 결과 표시**: 이 쿼리는 특정 서버의 결과를 확인하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-131">**Show all results for a specific server**: This query shows how to see results of a specific server.</span></span>

<span data-ttu-id="10b59-132">**쿼리**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span><span class="sxs-lookup"><span data-stu-id="10b59-132">**Query**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span></span>

![모든 결과](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

<span data-ttu-id="10b59-134">또한 이러한 레코드/쿼리를 사용하여 고유한 대시보드, 보고서 또는 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-134">You can also use these records/queries to create your own dashboards, reports, or alerts.</span></span> <span data-ttu-id="10b59-135">아래 화면에는 대시보드에 추가할 수 있는 샘플 UI 컨트롤이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-135">The screen below has a sample UI control that you can add to your dashboard.</span></span> <span data-ttu-id="10b59-136">[여기](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/)에서 OMS 뷰 디자이너를 사용하여 데이터를 시각화하는 방법을 배울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-136">You can learn how to visualize your data using OMS View Designer [here](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span></span> <span data-ttu-id="10b59-137">이를 사용자 지정하면 아래 화면은 타일의 모양을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-137">The screen below is an example of how the tile will look like once you make this customization.</span></span>

![샘플 UI](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> <span data-ttu-id="10b59-139">기준 평가를 위해 확인된 설정을 알아보려면 이러한 설정이 포함된 [이 Excel 스프레드시트](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690)를 다운로드하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-139">If you would like to know the settings that are checked for the baseline assessment, you can download [this Excel spreadsheet](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) that contains these settings.</span></span>

## <a name="see-also"></a><span data-ttu-id="10b59-140">참고 항목</span><span class="sxs-lookup"><span data-stu-id="10b59-140">See also</span></span>
<span data-ttu-id="10b59-141">이 문서에서는 OMS 보안 및 감사 웹 기준 평가에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="10b59-141">In this document, you learned about OMS Security and Audit web baseline assessment.</span></span> <span data-ttu-id="10b59-142">OMS 보안에 대해 자세히 알아보려면 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="10b59-142">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="10b59-143">OMS(Operations Management Suite) 개요</span><span class="sxs-lookup"><span data-stu-id="10b59-143">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="10b59-144">Operations Management Suite 보안 및 감사 솔루션의 보안 경고 모니터링 및 응답</span><span class="sxs-lookup"><span data-stu-id="10b59-144">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="10b59-145">Operations Management Suite 보안 및 감사 솔루션의 리소스 모니터링</span><span class="sxs-lookup"><span data-stu-id="10b59-145">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

