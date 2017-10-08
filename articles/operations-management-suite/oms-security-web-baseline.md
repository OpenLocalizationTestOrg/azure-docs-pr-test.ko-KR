---
title: "관리 도구 모음 보안 및 감사 솔루션 웹 초기 aaaOperations | Microsoft Docs"
description: "이 문서에서는 설명 어떻게 toouse OMS 보안 및 감사 솔루션 tooperform 규정 준수 및 보안 용도 대 한 모든 모니터링 대상된 웹 서버에 대 한 웹 초기 평가 합니다."
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
ms.openlocfilehash: 8aa87fa404ff97ab549dda3f9bebb75766055963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="c6638-103">Operations Management Suite 보안 및 감사 솔루션의 웹 기준 평가</span><span class="sxs-lookup"><span data-stu-id="c6638-103">Web Baseline Assessment in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="c6638-104">이 문서를 사용 하면 toouse [Operations Management Suite (OMS) 보안 및 감사 솔루션](operations-management-suite-overview.md) 웹 기능 tooaccess hello 보안 리소스 상태를 모니터링 하는 초기 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-104">This document helps you toouse [Operations Management Suite (OMS) Security and Audit Solution](operations-management-suite-overview.md) web baseline assessment capabilities tooaccess hello secure state of your monitored resources.</span></span>

## <a name="what-is-web-baseline-assessment"></a><span data-ttu-id="c6638-105">웹 기준 평가란?</span><span class="sxs-lookup"><span data-stu-id="c6638-105">What is Web Baseline Assessment?</span></span>
<span data-ttu-id="c6638-106">현재 OMS 보안은 운영 체제에 대한 보안 기준 평가를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-106">Currently OMS Security provides security baseline assessment for operating systems.</span></span> <span data-ttu-id="c6638-107">24 시간 마다 서버 운영 체제 설정을 hello를 검색 하 고 잠재적으로 취약 한 설정에 대 한 뷰를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-107">It scans hello operating system settings of your servers every 24 hours and provides a view into potentially vulnerable settings.</span></span> <span data-ttu-id="c6638-108">이에 대한 자세한 내용은 [Operations Management Suite 보안 및 감사 솔루션의 기준 평가](oms-security-baseline.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6638-108">Read [Baseline Assessment in Operations Management Suite Security and Audit Solution](oms-security-baseline.md) for more information on this.</span></span>

<span data-ttu-id="c6638-109">hello hello 웹 초기 평가의 ´ ֲ toofind 잠재적으로 취약 한 웹 서버 설정.</span><span class="sxs-lookup"><span data-stu-id="c6638-109">hello goal of hello web baseline assessment is toofind potentially vulnerable web server settings.</span></span> <span data-ttu-id="c6638-110">hello 웹 초기 구성에 대 한 기본 원본은 다음 세 가지 hello:.NET, ASP.NET 및 IIS 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-110">hello three primary sources for hello web baseline configurations are: .NET, ASP.NET, and IIS configuration.</span></span>  <span data-ttu-id="c6638-111">운영 시스템 초기 평가 hello, 처럼 OMS 보안은 사용 하겠습니다 tooscan 사용자 웹 서버에 24 시간 마다 하 고 그 중 보안 상태에 대 한 뷰를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-111">Just like hello operating system baseline assessment, OMS Security is going tooscan your web servers every 24hrs and provide a view into security state of them.</span></span>  <span data-ttu-id="c6638-112">인터넷 정보 서비스 (IIS), 구성은 하는 고도로 사용자 지정 가능한 재정의 된 다양 한 사이트 및 응용 프로그램 수준 toobe 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-112">In Internet Information Service (IIS), configurations are highly customizable, which allows various site and application levels toobe overridden.</span></span> <span data-ttu-id="c6638-113">hello 스캐너 추가 toohello 기본 루트 수준에서 각 응용 프로그램/사이트 수준에서 hello 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-113">hello scanner checks hello settings at each application/site level in addition toohello default root level.</span></span> <span data-ttu-id="c6638-114">이 tooidentify 잠재적인 취약점 설정 위치를 사용 하면 고 신속 하 게 재구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-114">This helps you tooidentify potential vulnerability settings locations and quickly remediate.</span></span>


## <a name="web-security-baseline-assessment"></a><span data-ttu-id="c6638-115">웹 보안 기준 평가</span><span class="sxs-lookup"><span data-stu-id="c6638-115">Web Security Baseline Assessment</span></span>
<span data-ttu-id="c6638-116">이 미리 보기에 대 한이 기능은 toobe hello OMS 검색 옵션을 사용 하 여 액세스 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-116">For this preview this feature is going toobe accessed using hello OMS Search option.</span></span> <span data-ttu-id="c6638-117">Tooperform appropriated hello 쿼리 아래 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-117">Follow hello steps below tooperform hello appropriated query:</span></span>

1. <span data-ttu-id="c6638-118">Hello에 **Microsoft Operations Management Suite** 기본 대시보드 클릭 **보안 및 감사** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-118">In hello **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="c6638-119">Hello에 **보안 및 감사** 대시보드를 클릭 하 여 **로그 검색** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-119">In hello **Security and Audit** dashboard, click **Log Search** button.</span></span>
3. <span data-ttu-id="c6638-120">사용할 수 있는 hello 첫 번째 쿼리는 hello **웹 초기 평가 요약**합니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-120">hello first query that you can use is hello **Web Baseline Assessment Summary**.</span></span> <span data-ttu-id="c6638-121">Hello에 **검색 시작** 필드에서이 쿼리를 입력: 형식*SecurityBaselineSummary BaselineType = 웹 =*합니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-121">In hello **Begin search here** field, type this query: Type*=SecurityBaselineSummary BaselineType=web*.</span></span> <span data-ttu-id="c6638-122">hello 화면에 다음 출력 예제에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-122">hello following screen has an output sample:</span></span>

![웹 기준 평가 요약](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> <span data-ttu-id="c6638-124">이 쿼리에서 각 레코드는 단일 서버에 대한 요약 평가를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-124">In this query, each record indicates assessment summary on a single server.</span></span>

<span data-ttu-id="c6638-125">Hello에 있는 경우 **로그 검색**을 각각 다른 쿼리에 tooobtain hello 웹 초기 평가 대 한 자세한 정보를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-125">Once you are in hello **Log Search**, you can type different queries tooobtain more information about hello web baseline assessment.</span></span> <span data-ttu-id="c6638-126">또한 toohello 이전 쿼리를 사용할 수도 있습니다 hello이 미리이 보기에는 스토리를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-126">In addition toohello previous query, you can also use hello following ones in this preview.</span></span>

<span data-ttu-id="c6638-127">**웹 기준 규칙 평가**: 각 레코드는 단일 서버에서 단일 웹 기준 규칙 평가를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-127">**Web Baseline Rule Assessment**: Each record represents a single web baseline rule evaluation on a single server.</span></span> <span data-ttu-id="c6638-128">Hello 규칙과 위치, hello 예상 결과 hello 실제 결과 대 한 모든 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-128">It includes all data for hello rule, location, hello expected result, and hello actual result.</span></span>

<span data-ttu-id="c6638-129">**쿼리**: Type*=SecurityBaseline BaselineType=web*</span><span class="sxs-lookup"><span data-stu-id="c6638-129">**Query**: Type*=SecurityBaseline BaselineType=web*</span></span>

![웹 기준 규칙 평가](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

<span data-ttu-id="c6638-131">**특정 서버에 대 한 모든 결과 표시**:이 쿼리에서 toosee 발생 하는 방법을 보여 줍니다. 특정 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-131">**Show all results for a specific server**: This query shows how toosee results of a specific server.</span></span>

<span data-ttu-id="c6638-132">**쿼리**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span><span class="sxs-lookup"><span data-stu-id="c6638-132">**Query**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span></span>

![모든 결과](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

<span data-ttu-id="c6638-134">이러한 레코드/쿼리 toocreate 고유한 대시보드, 보고서 또는 경고에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-134">You can also use these records/queries toocreate your own dashboards, reports, or alerts.</span></span> <span data-ttu-id="c6638-135">hello 화면 아래에 샘플 UI 컨트롤이 tooyour 대시보드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-135">hello screen below has a sample UI control that you can add tooyour dashboard.</span></span> <span data-ttu-id="c6638-136">학습할 수 있는 방법을 toovisualize OMS 뷰 디자이너를 사용 하 여 데이터 [여기](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-136">You can learn how toovisualize your data using OMS View Designer [here](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span></span> <span data-ttu-id="c6638-137">hello 아래 화면은이 사용자 지정 확인 되 면 hello 타일 방법의 예는 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-137">hello screen below is an example of how hello tile will look like once you make this customization.</span></span>

![샘플 UI](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> <span data-ttu-id="c6638-139">다운로드할 수 있습니다 hello 초기 평가 대 한 체크 인 된 tooknow hello 설정, 원하는 경우 [이 Excel 스프레드시트](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) 이러한 설정을 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-139">If you would like tooknow hello settings that are checked for hello baseline assessment, you can download [this Excel spreadsheet](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) that contains these settings.</span></span>

## <a name="see-also"></a><span data-ttu-id="c6638-140">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c6638-140">See also</span></span>
<span data-ttu-id="c6638-141">이 문서에서는 OMS 보안 및 감사 웹 기준 평가에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="c6638-141">In this document, you learned about OMS Security and Audit web baseline assessment.</span></span> <span data-ttu-id="c6638-142">OMS 보안에 대해 자세히 toolearn hello 다음 문서 참조:</span><span class="sxs-lookup"><span data-stu-id="c6638-142">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="c6638-143">OMS(Operations Management Suite) 개요</span><span class="sxs-lookup"><span data-stu-id="c6638-143">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="c6638-144">모니터링 및 Operations Management Suite 보안 및 감사 솔루션에 응답 중 tooSecurity 경고</span><span class="sxs-lookup"><span data-stu-id="c6638-144">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="c6638-145">Operations Management Suite 보안 및 감사 솔루션의 리소스 모니터링</span><span class="sxs-lookup"><span data-stu-id="c6638-145">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

