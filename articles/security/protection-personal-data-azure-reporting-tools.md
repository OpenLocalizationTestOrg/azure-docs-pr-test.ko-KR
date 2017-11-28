---
title: "Azure 보고 도구를 사용 하 여 개인 데이터의 aaaDocument 보호 | Microsoft Docs"
description: "어떻게 toouse 보고 Azure 서비스 및 기술 toohelp 개인 데이터의 개인 정보를 보호 합니다."
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 3230d26ed308a8a0e72421c001793be06334a7c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="document-protection-of-personal-data-with-azure-reporting-tools"></a><span data-ttu-id="c454d-103">Azure 보고 도구로 개인 데이터의 문서 보호</span><span class="sxs-lookup"><span data-stu-id="c454d-103">Document protection of personal data with Azure reporting tools</span></span>

<span data-ttu-id="c454d-104">이 문서에서는 Azure reporting toouse 서비스 하는 방법을 설명 하 고 기술 toohelp 개인 데이터의 개인 정보를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-104">This article will discuss how toouse Azure reporting services and technologies toohelp protect privacy of personal data.</span></span>

## <a name="scenario"></a><span data-ttu-id="c454d-105">시나리오</span><span class="sxs-lookup"><span data-stu-id="c454d-105">Scenario</span></span>

<span data-ttu-id="c454d-106">Hello 미국에서 본사는 큰 크루즈 회사 hello 지중해, Adriatic, 발트어 바다 뿐 아니라 hello 영국 제도에서 해당 작업 toooffer 여정이 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-106">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="c454d-107">toohelp 이탈리아를 더 작은 여러 크루즈 줄 획득 이러한 노력을이 통해 독일, 덴마크 및 hello 영국</span><span class="sxs-lookup"><span data-stu-id="c454d-107">toohelp these efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span>

<span data-ttu-id="c454d-108">hello 회사에서 회사 데이터의 처리 및 저장에 대 한 Microsoft Azure를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-108">hello company uses Microsoft Azure for processing and storage of corporate data.</span></span> <span data-ttu-id="c454d-109">여기에는 전 세계 고객 기반의 이름, 주소, 전화 번호 및 신용 카드 정보와 같이 식별 가능한 개인 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="c454d-110">또한 모든 위치에 주소, 전화 번호, 세금 id 번호, 회사 직원에 대 한 의료 보험 정보 등 기존의 인적 자원 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-110">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="c454d-111">hello 크루즈 줄에는 현재 및 과거 고객과 개인 정보 tootrack 관계를 포함 하는 보상 및 충성도 프로그램 멤버의 큰 데이터베이스 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-111">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="c454d-112">회사 직원 hello 네트워크 hello 회사의 원격 사무실 및 여행사에서 액세스 하는 hello world 주변에 있는 toosome 회사 리소스에 액세스 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-112">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="c454d-113">문제 설명</span><span class="sxs-lookup"><span data-stu-id="c454d-113">Problem statement</span></span>

<span data-ttu-id="c454d-114">hello 회사 직원의 및 고객의 개인 데이터를 통해 Azure 관리 및 보안 기능 tooimpose 개인 데이터 액세스 tooand 처리에 엄격한 제어를 사용 하 고 있어야 하는 다중 계층된 보안 전략의 hello 개인 정보를 보호 해야 합니다. 수 toodemonstrate toointernal 및 외부 감사자의 보호를 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-114">hello company must protect hello privacy of employees’ and customers’ personal data through a multi-layered security strategy that uses Azure management and security features tooimpose strict controls on access tooand processing of personal data, and must be able toodemonstrate its protective measures toointernal and external auditors.</span></span>

## <a name="company-goal"></a><span data-ttu-id="c454d-115">회사 목표</span><span class="sxs-lookup"><span data-stu-id="c454d-115">Company goal</span></span>

<span data-ttu-id="c454d-116">해당 방어 보안 전략의 일환으로, 회사 목표 tootrack 개인 데이터의 모든 액세스 tooand 처리 되며 설명서 개인 데이터에 대 한 적절 한 개인 정보 보호의 위치와 작업에 있는지 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="c454d-116">As part of its defense-in-depth security strategy, it is a company goal tootrack all access tooand processing of personal data, and ensure that documentation of adequate privacy protections for personal data are in place and working.</span></span>

## <a name="solutions"></a><span data-ttu-id="c454d-117">솔루션</span><span class="sxs-lookup"><span data-stu-id="c454d-117">Solutions</span></span>

<span data-ttu-id="c454d-118">Microsoft Azure에서는 포괄적인 모니터링, 로깅 및 진단 도구 toohelp 추적 및 활동과 액세스 하 고 개인 데이터, 데이터 및 제 3 자 액세스 toopersonal 데이터의 흐름을 지리적 처리와 관련 된 이벤트를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-118">Microsoft Azure provides comprehensive monitoring, logging, and diagnostics tools toohelp track and record activities and events associated with accessing and processing personal data, geographic flow of data, and third-party access toopersonal data.</span></span> <span data-ttu-id="c454d-119">Hello 클라우드에서 개인 데이터의 보안 공유 책임 이기 때문에 Microsoft 고객에 게 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-119">Because security of personal data in hello cloud is a shared responsibility, Microsoft also provides customers with:</span></span>

- <span data-ttu-id="c454d-120">고객 데이터의 자체적인 처리에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="c454d-120">Detailed information about its own processing of customers’ data</span></span>

- <span data-ttu-id="c454d-121">Microsoft에서 관리하는 보안 조치</span><span class="sxs-lookup"><span data-stu-id="c454d-121">Security measures administered by Microsoft</span></span>

- <span data-ttu-id="c454d-122">고객의 데이터를 보낼 위치와 방법</span><span class="sxs-lookup"><span data-stu-id="c454d-122">Where and how it sends customers’ data</span></span>

- <span data-ttu-id="c454d-123">Microsoft의 개인 정보 검토 프로세스의 세부 정보</span><span class="sxs-lookup"><span data-stu-id="c454d-123">Details of Microsoft’s own privacy reviews process</span></span>

### <a name="azure-active-directory"></a><span data-ttu-id="c454d-124">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c454d-124">Azure Active Directory</span></span>

<span data-ttu-id="c454d-125">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/)는 Microsoft의 클라우드 기반, 다중 테넌트 디렉터리 및 ID 관리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-125">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span> <span data-ttu-id="c454d-126">서비스의 로그인 hello 및 감사 보고 기능 자세한 로그인 및 응용 프로그램 사용 현황 활동 정보 toohelp 모니터링 하 고 적절 한 액세스 toocustomers 및 직원의 개인 데이터 확인을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-126">hello service’s sign-in and audit reporting capabilities provide you with detailed sign-in and application usage activity information toohelp you monitor and ensure proper access toocustomers’ and employees’ personal data.</span></span>

<span data-ttu-id="c454d-127">활동 보고서에는 다음 두 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-127">There are two types of activity reports:</span></span>

- <span data-ttu-id="c454d-128">hello [활동 보고서/로그 감사](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) 시스템 활동/작업의 세부 레코드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-128">hello [audit activity reports/logs](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) provide a detailed record of system activities/tasks</span></span>

- <span data-ttu-id="c454d-129">hello [로그인 활동 보고서/로그](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) hello 감사 보고서에 나열 된 각 활동을 수행한 사용자 표시</span><span class="sxs-lookup"><span data-stu-id="c454d-129">hello [sign-ins activity report/log](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) shows you who has performed each activity listed in hello audit report</span></span>

<span data-ttu-id="c454d-130">Hello 두를 함께 사용 hello 수행 하는 각 작업의 기록과 각각을 수행한 사용자를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-130">Using hello two together, you can track hello history of every task performed and who performed each.</span></span> <span data-ttu-id="c454d-131">두 보고서 유형 모두 사용자 지정이 가능하고 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-131">Both types of reports are customizable and can be filtered.</span></span>

#### <a name="how-do-i-access-hello-audit-and-security-logs"></a><span data-ttu-id="c454d-132">액세스 하려면 어떻게 합니까 hello 감사 및 보안 로그?</span><span class="sxs-lookup"><span data-stu-id="c454d-132">How do I access hello audit and security logs?</span></span>

<span data-ttu-id="c454d-133">hello 감사 및 보안 로그에에서 액세스할 수 있습니다 hello Active Directory 포털에서 세 가지 방법으로: hello를 통해 **활동** 섹션 (중 하나를 선택 **감사 로그** 또는 **로그인**), 또는 **사용자 및 그룹** 또는 **엔터프라이즈 응용 프로그램** 아래 **관리** Active Directory에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-133">hello audit and security logs can be accessed from hello Active Directory portal in three different ways: through hello **Activity** section (select either **Audit logs** or **Sign-ins**), or from **Users and groups** or **Enterprise applications** under **Manage** in Active Directory.</span></span> <span data-ttu-id="c454d-134">또한 hello Azure Active Directory를 통해 보고서에 액세스할 수 API를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-134">Reports can also be accessed through hello Azure Active Directory reporting API.</span></span> 

1. <span data-ttu-id="c454d-135">Hello Azure 포털에서에서 선택 **Azure Active Directory 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c454d-135">In hello Azure portal, select **Azure Active Directory.**</span></span>

2. <span data-ttu-id="c454d-136">Hello에 **활동** 섹션에서 **감사 로그 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c454d-136">In hello **Activity** section, select **Audit logs.**</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image001.png)

3. <span data-ttu-id="c454d-137">Hello 목록 보기를 클릭 하 여 사용자 지정 **열** hello 도구 모음에서입니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-137">Customize hello list view by clicking **Columns** in hello toolbar.</span></span>

4.  <span data-ttu-id="c454d-138">항목에 대 한 모든 사용 가능한 세부 정보 목록 보기 toosee hello에서에서 항목을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-138">Select an item in hello list view toosee all available details about it.</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image003.png)

<span data-ttu-id="c454d-139">또한 Azure Active Directory 보고에는 **위험 플래그가 지정된 사용자** 및 **위험한 로그인**이라는 두 가지 유형의 보안 보고서가 포함되어 Azure 환경에서 잠재적인 위험을 모니터링하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-139">Azure Active Directory reporting also includes two types of security reports, **users flagged for risk** and **risky sign-ins**, which can help you monitor potential risks in your Azure environment.</span></span>

<span data-ttu-id="c454d-140">보고 서비스는 hello에 대 한 자세한 내용은 참조 하십시오. [Azure Active Directory 보고](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="c454d-140">For more information about hello reporting service, see [Azure Active Directory reporting](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal)</span></span>

<span data-ttu-id="c454d-141">방문 [Azure Active Directory 작업 보고서](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal#activity-reports) Azure Active Directory에서 사용할 수 있는 hello 보고서에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-141">Visit [Azure Active Directory activity reports](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal#activity-reports) for more specifics about hello reports available in Azure Active Directory.</span></span> <span data-ttu-id="c454d-142">이 사이트에 방법에 대 한 자세한 내용은 tooaccess 사용 하 여 [감사 로그를 작업 보고서](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) 및 [로그인 활동 보고서](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) hello 포털에서입니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-142">This site includes more details about how tooaccess and use [audit logs activity reports](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) and [sign-in activity reports](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) in hello portal.</span></span> <span data-ttu-id="c454d-143">또한 [위험에 대한 플래그가 지정된 사용자](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-user-at-risk) 및 [위험한 로그인](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-risky-sign-ins) 보안 보고서에 대한 정보도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-143">It also includes information about [users flagged for risk](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-user-at-risk) and [risky sign-in](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-risky-sign-ins) security reports.</span></span>

<span data-ttu-id="c454d-144">Hello 방문 [Azure Active Directory 감사 API 참조](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-audit-reference) 방법에 대 한 자세한 내용은 사이트 tooconnect tooAzure 디렉터리 프로그래밍 방식으로 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-144">Visit hello [Azure Active Directory audit API reference](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-audit-reference) site for more information on how tooconnect tooAzure Directory reporting programmatically.</span></span>

### <a name="log-analytics"></a><span data-ttu-id="c454d-145">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="c454d-145">Log Analytics</span></span>

<span data-ttu-id="c454d-146">[로그 분석](https://azure.microsoft.com/services/log-analytics/) 수 [Azure 모니터에서 데이터를 수집](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage) toocorrelate 다른 데이터와 분석 추가 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-146">[Log Analytics](https://azure.microsoft.com/services/log-analytics/) can [collect data from Azure Monitor](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage) toocorrelate it with other data and provide additional analysis.</span></span> <span data-ttu-id="c454d-147">Azure Monitor는 Azure 환경에 대한 모니터링 데이터를 수집하고 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-147">Azure Monitor collects and analyzes monitoring data for your Azure environment.</span></span> 

<span data-ttu-id="c454d-148">로그 검색, 뷰 및 솔루션과 같은 Log Analytics의 분석 도구는 전체 사용자 환경의 중앙 집중식 분석을 제공하는 모든 수집된 데이터에 대해 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-148">Analysis tools in Log Analytics such as log searches, views, and solutions work against all collected data, providing you with centralized analysis of your entire environment.</span></span> <span data-ttu-id="c454d-149">로그 분석 집계 하 고 Windows 이벤트 로그, IIS 로그 및 toounauthorized 사용자 개인 데이터에 노출 시킬 수 있는 잠재적인 개인 데이터 위반을 감지 하는 데 도움이 되는 Syslogs 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-149">Log Analytics can aggregate and analyze Windows Event logs, IIS logs, and Syslogs, which can help detect potential personal data breaches that could expose personal data toounauthorized users.</span></span>

#### <a name="how-do-i-use-log-analytics"></a><span data-ttu-id="c454d-150">Log Analytics를 사용하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="c454d-150">How do I use Log Analytics?</span></span>

<span data-ttu-id="c454d-151">로그 분석 hello OMS 포털 또는 hello 모든 웹 브라우저에서 Azure 포털을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-151">You can access Log Analytics through hello OMS portal or hello Azure portal, from any web browser.</span></span> <span data-ttu-id="c454d-152">로그 분석 쿼리 언어 tooquickly 검색을 포함 하며 hello 리포지토리에 데이터를 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-152">Log Analytics includes a query language tooquickly retrieve and consolidate data in hello repository.</span></span> <span data-ttu-id="c454d-153">만들 하 고 로그 검색 toodirectly 저장 hello 포털에서 데이터를 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-153">You can create and save Log Searches toodirectly analyze data in hello portal.</span></span>

<span data-ttu-id="c454d-154">toocreate hello Azure 포털에서에서 로그 분석 작업 영역 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-154">toocreate a Log Analytics workspace in hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="c454d-155">선택 **로그 분석** hello hello Marketplace의에서 서비스 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-155">Select **Log Analytics** from hello list of services in hello Marketplace.</span></span>

2. <span data-ttu-id="c454d-156">선택 **만들기,** 다음 hello OMS 작업 영역 이름을 지정 구독, 리소스 그룹, 위치를 선택 하 고 가격 책정 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-156">Select **Create,** then specify hello name of your OMS workspace, select your subscription, resource group, location, and pricing tier.</span></span>

3. <span data-ttu-id="c454d-157">클릭 **확인** toodisplay 작업 영역 목록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-157">Click **OK** toodisplay a list of your workspaces.</span></span>

4. <span data-ttu-id="c454d-158">작업 영역 toosee 세부 정보를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-158">Select a workspace toosee its details.</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image004.png)

<span data-ttu-id="c454d-159">Hello 방문 [로그 분석 설명서](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) toolearn hello 서비스에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-159">Visit hello [Log Analytics documentation](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) toolearn more about hello service.</span></span>

<span data-ttu-id="c454d-160">Hello 방문 [로그 분석 작업 영역 시작](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started) 자습서 toocreate는 평가 작업 영역 어떻게 toouse hello 서비스의 hello 기본 사항 학습 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-160">Visit hello [Get started with a Log Analytics workspace](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started) tutorial toocreate an evaluation workspace and learn hello basics of how toouse hello service.</span></span>

<span data-ttu-id="c454d-161">보다 구체적인 정보에 대 한 웹 페이지에 나오는 tooconnect toouse 로그 분석 hello로 기록 하는 방법에 hello를 방문 하 고 위에 설명 된 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-161">Visit hello following web pages for more specific information on how tooconnect toouse Log Analytics with hello logs described above:</span></span>

[<span data-ttu-id="c454d-162">Log Analytics의 Windows 이벤트 로그 데이터 원본</span><span class="sxs-lookup"><span data-stu-id="c454d-162">Windows event logs data sources in Log Analytics</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)

[<span data-ttu-id="c454d-163">Log Analytics의 IIS 로그</span><span class="sxs-lookup"><span data-stu-id="c454d-163">IIS logs in Log Analytics</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-iis-logs)

[<span data-ttu-id="c454d-164">Log Analytics의 Syslog 데이터 원본</span><span class="sxs-lookup"><span data-stu-id="c454d-164">Syslog data sources in Log Analytics</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-syslog)

### <a name="azure-monitorazure-activity-log"></a><span data-ttu-id="c454d-165">Azure Monitor/Azure 활동 로그</span><span class="sxs-lookup"><span data-stu-id="c454d-165">Azure Monitor/Azure Activity Log</span></span> 

<span data-ttu-id="c454d-166">[Azure Monitor](https://azure.microsoft.com/services/monitor/)는 대부분의 Microsoft Azure 서비스에 대한 기본 수준의 인프라 메트릭과 로그를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-166">[Azure Monitor](https://azure.microsoft.com/services/monitor/) provides base level infrastructure metrics and logs for most services in Microsoft Azure.</span></span>
<span data-ttu-id="c454d-167">모니터링 toogain Azure 응용 프로그램에 대 한 깊은 통찰력 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-167">Monitoring can help you toogain deep insights about your Azure applications.</span></span> <span data-ttu-id="c454d-168">Azure 모니터는 hello Azure 진단 확장 (Windows 또는 Linux) 대부분의 응용 프로그램 수준 메트릭 및 로그를 수집 하려면 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-168">Azure Monitor relies on hello Azure diagnostics extension (Windows or Linux) to collect most application level metrics and logs.</span></span> <span data-ttu-id="c454d-169">[Azure 활동 로그 hello](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) Azure 모니터를 볼 수는 hello 리소스 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-169">[hello Azure Activity Log](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) is one of hello resources you can view with Azure Monitor.</span></span> <span data-ttu-id="c454d-170">모든 API 호출을 추적하고 [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)에서 발생하는 활동에 대한 다양한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-170">It tracks every API call, and provides a wealth of information about activities that occur in [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span>
<span data-ttu-id="c454d-171">Hello Azure 인프라와 같이 리소스에 대 한 자세한 내용은 hello (이전에 운영 또는 감사 로그 호출) 활동 로그를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-171">You can search hello Activity Log (previously called Operational or Audit Logs) for information about your resource as seen by hello Azure infrastructure.</span></span> 

<span data-ttu-id="c454d-172">Hello 정보의 대부분 기록 하지만 hello 활동 로그 tooperformance과 서비스 상태를 관련 된., 정보를 데이터의 관련된 tooprotection 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-172">Although much of hello information recorded in hello Activity log pertains tooperformance and service health, there is also information that is related tooprotection of data.</span></span> <span data-ttu-id="c454d-173">Hello 활동 로그를 사용 하 여 hello 확인할 수 있습니다 "부분, who, 시기 및" 모든 쓰기 작업 (PUT, POST, DELETE) Azure 구독에서 hello 리소스에 대해 수행에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-173">Using hello Activity Log, you can determine hello “what, who, and when” for any write operations (PUT, POST, DELETE) taken on hello resources in your Azure subscription.</span></span>

<span data-ttu-id="c454d-174">예를 들어 관리자가 개인 데이터의 hello 보호에 영향을 줄 수 있는 네트워크 보안 그룹을 삭제 레코드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-174">For example, it provides a record when an administrator deletes a network security group, which could impact hello protection of personal data.</span></span> <span data-ttu-id="c454d-175">활동 로그 항목은 Azure Monitor에 90일 동안 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-175">Activity log entries are stored in Azure Monitor for 90 days.</span></span>

#### <a name="how-do-i-use-hello-data-collected-by-azure-monitor"></a><span data-ttu-id="c454d-176">Azure 모니터에 의해 수집 된 hello 데이터를 사용 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="c454d-176">How do I use hello data collected by Azure Monitor?</span></span>

<span data-ttu-id="c454d-177">다양 한 방법으로 toouse hello 데이터 hello 활동 로그에 및 기타 Azure 모니터 리소스.</span><span class="sxs-lookup"><span data-stu-id="c454d-177">There are a number of ways toouse hello data in hello Activity log and other Azure Monitor resources.</span></span>

- <span data-ttu-id="c454d-178">Hello 데이터 tooother 위치 실제 줄에서 스트리밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-178">You can stream hello data tooother locations in real line.</span></span>

- <span data-ttu-id="c454d-179">사용 하 여 hello 기본값 보다 더 긴 기간에 대 한 hello 데이터를 저장할 수 있습니다는 [Azure 저장소 계정](https://docs.microsoft.com/azure/storage/common/storage-introduction) 및 보존 정책을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-179">You can store hello data for longer time periods than hello defaults, using an [Azure storage account](https://docs.microsoft.com/azure/storage/common/storage-introduction) and setting a retention policy.</span></span>

- <span data-ttu-id="c454d-180">Hello를 사용 하 여 그래픽 및 차트를 보고서의 데이터를 시각적 hello 수 [Azure 포털](https://azure.microsoft.com/features/azure-portal/), [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), [Microsoft PowerBI](https://powerbi.microsoft.com/), 또는 제 3 자 시각화 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-180">You can visual hello data in graphics and charts, using hello [Azure portal](https://azure.microsoft.com/features/azure-portal/), [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), [Microsoft PowerBI](https://powerbi.microsoft.com/), or third-party visualization tools.</span></span>

- <span data-ttu-id="c454d-181">Hello CLI 명령 Azure 모니터 REST API를 사용 하 여 hello 데이터를 쿼리할 수 [PowerShell](https://docs.microsoft.com/powershell/) cmdlet 또는.NET SDK를 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-181">You can query hello data using hello Azure Monitor REST API, CLI commands, [PowerShell](https://docs.microsoft.com/powershell/) cmdlets, or hello .NET SDK.</span></span>

<span data-ttu-id="c454d-182">Azure 모니터 시작 tooget 선택 **더 서비스** hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="c454d-182">tooget started with Azure Monitor, select **More Services** in hello Azure portal.</span></span>

1. <span data-ttu-id="c454d-183">너무 아래로 스크롤하여**모니터** hello에 **모니터링 및 관리** 섹션.</span><span class="sxs-lookup"><span data-stu-id="c454d-183">Scroll down too**Monitor** in hello **Monitoring and Managing** section.</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image005.png)

2.  <span data-ttu-id="c454d-184">Hello에서 모니터 열립니다 **활동 로그** 보기.</span><span class="sxs-lookup"><span data-stu-id="c454d-184">Monitor opens in hello **Activity Log** view.</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image007.png)

<span data-ttu-id="c454d-185">수 만들고 저장 pin hello 가장 중요 한 쿼리 tooa 포털 대시보드에서 한 공통 필터 다음에 대 한 쿼리 조건을 충족 하는 이벤트가 발생 한 경우 항상 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-185">You can create and save queries for common filters, then pin hello most important queries tooa portal dashboard so you'll always know if events that meet your criteria have occurred.</span></span>

1. <span data-ttu-id="c454d-186">리소스 그룹, timespan 및 이벤트 범주에 따라 hello 보기를 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-186">You can filter hello view by resource group, timespan, and event category.</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image008.png)

2. <span data-ttu-id="c454d-187">Hello를 클릭 하 여 다음 쿼리 tooa 포털 대시보드에 고정할 수 있습니다 **Pin** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-187">You can then pin queries tooa portal dashboard by clicking hello **Pin** button.</span></span> <span data-ttu-id="c454d-188">이렇게 하면 서비스에 대한 운영 데이터 정보를 제공하는 단일 출처를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-188">This helps you create a single source of information for operational  data on your services.</span></span> <span data-ttu-id="c454d-189">hello 대시보드에서 hello 쿼리 이름 및 결과 수가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-189">hello query name and number of results will be displayed on hello dashboard.</span></span>

<span data-ttu-id="c454d-190">모든 Azure 리소스에 대 한 hello 모니터 tooview 메트릭을 사용 하 여 하 고 진단 설정 및 경고를 구성 다음 hello 로그를 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-190">You can also use hello Monitor tooview metrics for all Azure resources, configure diagnostics settings and alerts, and search hello log.</span></span> <span data-ttu-id="c454d-191">Toouse hello Azure 모니터 및 작업 로그를 참조 하는 방법에 대 한 자세한 내용은 [Azure 모니터를 시작](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started)합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-191">For more information on how toouse hello Azure Monitor and Activity Log, see [Get Started with Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started).</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="c454d-192">Azure 진단</span><span class="sxs-lookup"><span data-stu-id="c454d-192">Azure Diagnostics</span></span> 

<span data-ttu-id="c454d-193">Azure의 hello 진단 기능을 사용 하면 여러 원본에서 데이터의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-193">hello diagnostics capability in Azure enables collection of data from several sources.</span></span> <span data-ttu-id="c454d-194">hello 보안 로그를 포함 하는 hello Windows 이벤트 로그, 추적 및 개인 데이터의 보호를 문서화에 특히 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-194">hello Windows Event logs, which include hello Security log, can be especially useful in tracking and documenting protection of personal data.</span></span> <span data-ttu-id="c454d-195">hello 보안 로그 권한 변경, 특정 유형의 공격, 보안 관련 정책 변경, 보안 그룹 구성원 변경 등에 나타내는 패턴 검색 뿐 아니라 로그온 성공 및 실패 이벤트를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-195">hello security log tracks logon success and failure events, as well as permissions changes, detection of patterns indicating certain types of attacks, changes to security-related policies, security group membership changes, and much more.</span></span>

<span data-ttu-id="c454d-196">예를 들어 이벤트 ID 4695 감사 가능한 보호 된 데이터의 있습니다 시도 toohello unprotection을 경고합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-196">For example, Event ID 4695 alerts you toohello attempted unprotection of auditable protected data.</span></span> <span data-ttu-id="c454d-197">이 적용 toohello API DPAPI (데이터 보호), 개인 키, 저장 된 자격 증명 및 기타 기밀 정보 같은 tooprotect 데이터 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-197">This pertains toohello Data Protection API (DPAPI), which helps tooprotect data such as private keys, stored credentials, and other confidential information.</span></span>

#### <a name="how-do-i-enable-hello-diagnostics-extension-for-windows-vms"></a><span data-ttu-id="c454d-198">Windows Vm에 대 한 hello 진단 확장 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="c454d-198">How do I enable hello diagnostics extension for Windows VMs?</span></span>

<span data-ttu-id="c454d-199">Windows VM에 대 한 PowerShell tooenable hello 진단 확장을 따라서 toocollect 로그 데이터도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-199">You can use PowerShell tooenable hello diagnostics extension for a Windows VM, so as toocollect log data.</span></span> <span data-ttu-id="c454d-200">이렇게 hello 단계 (리소스 관리자 또는 클래식)를 사용 하는 배포 모델에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-200">hello steps for doing so depend on which deployment model you use (Resource Manager or Classic).</span></span> <span data-ttu-id="c454d-201">hello 리소스 관리자 배포 모델을 통해 생성 된 기존 VM에 tooenable hello 진단 확장을 hello를 사용할 수 있습니다 [집합 AzureRMVMDiagnosticsExtension PowerShell cmdlet](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension?view=azurermps-4.3.1)합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-201">tooenable hello diagnostics extension on an existing VM that was created through hello Resource Manager deployment model, you can use hello [Set-AzureRMVMDiagnosticsExtension PowerShell cmdlet](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension?view=azurermps-4.3.1).</span></span>

   ![](media/protection-personal-data-azure-reporting-tools/image009.png)

<span data-ttu-id="c454d-202">*\$diagnosticsconfig_path* hello 진단 구성을 XML에 포함 된 hello 경로 toohello 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-202">*\$diagnosticsconfig_path* is hello path toohello file that contains hello diagnostics configuration in XML.</span></span> <span data-ttu-id="c454d-203">VM에 Azure 진단 사용에 대 한 지침 보다 자세한 참조 [Windows를 실행 하는 가상 컴퓨터에서 PowerShell 사용 하 여 tooenable Azure 진단 합니다.](https://docs.microsoft.com/azure/virtual-machines/windows/ps-extensions-diagnostics)</span><span class="sxs-lookup"><span data-stu-id="c454d-203">For more detailed instructions on enabling Azure Diagnostics on a VM, see [Use PowerShell tooenable Azure Diagnostics in a virtual machine running Windows.](https://docs.microsoft.com/azure/virtual-machines/windows/ps-extensions-diagnostics)</span></span>

<span data-ttu-id="c454d-204">hello Azure 진단 확장 hello 수집 된 데이터 tooan Azure 저장소 계정에 전송 하거나 Application Insights와 같은 tooservices 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-204">hello Azure diagnostics extension can transfer hello collected data tooan Azure storage account or send it tooservices such as Application Insights.</span></span> <span data-ttu-id="c454d-205">그런 다음 감사에 대 한 hello 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-205">You can then use hello data for auditing.</span></span>

#### <a name="how-do-i-store-and-view-diagnostic-data"></a><span data-ttu-id="c454d-206">진단 데이터를 저장하고 보려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="c454d-206">How do I store and view diagnostic data?</span></span>

<span data-ttu-id="c454d-207">것이 중요 한 tooremember 오류 진단 데이터가 toohello Microsoft Azure 저장소 에뮬레이터 또는 tooAzure 저장소 전송 하지 않을 경우 영구적으로 저장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-207">It’s important tooremember that diagnostic data is not permanently stored unless you transfer it toohello Microsoft Azure storage emulator or tooAzure storage.</span></span> <span data-ttu-id="c454d-208">Azure 저장소에 진단 데이터 toostore 및 보기는 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="c454d-208">toostore and view diagnostic data in Azure Storage, follow these steps:</span></span>

1. <span data-ttu-id="c454d-209">Hello ServiceConfiguration.cscfg 파일에 저장소 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-209">Specify a storage account in hello ServiceConfiguration.cscfg file.</span></span> <span data-ttu-id="c454d-210">Azure 진단 hello Blob 서비스 또는 데이터의 hello 유형에 따라 hello 테이블 서비스에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-210">Azure Diagnostics can use either hello Blob service or hello Table service, depending on hello type of data.</span></span> <span data-ttu-id="c454d-211">Windows 이벤트 로그는 테이블 형식으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-211">Windows Event logs are stored in Table format.</span></span>

2. <span data-ttu-id="c454d-212">Hello 데이터를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-212">Transfer hello data.</span></span> <span data-ttu-id="c454d-213">Hello 구성 파일을 통해 tootransfer hello에 대 한 진단 데이터를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-213">You can request tootransfer hello diagnostic data through hello configuration file.</span></span> <span data-ttu-id="c454d-214">에 대 한 SDK 2.4 및 이전 프로그래밍 방식으로 hello 요청을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-214">For SDK 2.4 and previous, you can also make hello request programmatically.</span></span>

3. <span data-ttu-id="c454d-215">Hello 데이터를 사용 하 여 볼 [Azure 저장소 탐색기](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer), [서버 탐색기](https://docs.microsoft.com/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) Visual Studio에서 또는 [Azure 진단 관리자](https://www.cerebrata.com/products/azure-diagnostics-manager) Azure Management Studio에서.</span><span class="sxs-lookup"><span data-stu-id="c454d-215">View hello data, using [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer),  [Server Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) in Visual Studio, or [Azure Diagnostics Manager](https://www.cerebrata.com/products/azure-diagnostics-manager) in Azure Management Studio.</span></span>

<span data-ttu-id="c454d-216">방법에 대 한 자세한 내용은 각 tooperform 이러한 단계의 참조 [Azure 저장소에 진단 데이터 저장 및 확인 합니다.](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)</span><span class="sxs-lookup"><span data-stu-id="c454d-216">For more information on how tooperform each of these steps, see [Store and view diagnostic data in Azure Storage.](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)</span></span>

### <a name="azure-storage-analytics"></a><span data-ttu-id="c454d-217">Azure Storage 분석</span><span class="sxs-lookup"><span data-stu-id="c454d-217">Azure Storage Analytics</span></span> 

<span data-ttu-id="c454d-218">Storage Analytics는 성공 및 실패 한 요청 tooa 저장소 서비스에 대 한 세부 정보를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-218">Storage Analytics logs detailed information about successful and failed requests tooa storage service.</span></span> <span data-ttu-id="c454d-219">이 정보는 hello 서비스에 저장 된 액세스 toopersonal 데이터 문서화에 도움이 될 수 있는 사용된 toomonitor 개별 요청을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-219">This information can be used toomonitor individual requests, which can help in documenting access toopersonal data stored in hello service.</span></span> <span data-ttu-id="c454d-220">하지만 저장소 분석 로깅은 저장소 계정에 대해 기본적으로 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-220">However, Storage Analytics logging is not enabled by default for your storage account.</span></span> <span data-ttu-id="c454d-221">Hello Azure 포털에서에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-221">You can enable it in hello Azure portal.</span></span>

#### <a name="how-do-i-configure-monitoring-for-a-storage-account"></a><span data-ttu-id="c454d-222">저장소 계정에 대한 모니터링은 어떻게 구성하나요?</span><span class="sxs-lookup"><span data-stu-id="c454d-222">How do I configure monitoring for a storage account?</span></span>

<span data-ttu-id="c454d-223">저장소 계정에 대 한 모니터링 tooconfigure 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-223">tooconfigure monitoring for a storage account, do hello following:</span></span>

1. <span data-ttu-id="c454d-224">선택 **저장소 계정은** hello Azure 포털에서에서 다음 계정의 hello toomonitor hello 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-224">Select **Storage accounts** in hello Azure portal, then select hello name of hello account you want toomonitor.</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image011.png)

2. <span data-ttu-id="c454d-225">Hello에 **모니터링** 섹션에서 **진단 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c454d-225">In hello **Monitoring** section, select **Diagnostics.**</span></span>

3.  <span data-ttu-id="c454d-226">선택 hello **형식** 메트릭 데이터의 각 서비스 (Blob, 테이블, 파일)에 대 한 toomonitor 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-226">Select hello **type** of metrics data you want toomonitor for each service (Blob, Table, File).</span></span> <span data-ttu-id="c454d-227">tooinstruct Azure 저장소 toosave 진단 로그에 대 한 읽기, 쓰기 및 삭제 요청을 hello blob, 테이블 및 큐 서비스 선택에 대 한 **로그 Blob, 테이블 로그** 및 **로그 큐에 대기 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c454d-227">tooinstruct Azure Storage toosave diagnostics logs for read, write, and delete requests for hello blob, table, and queue services, select **Blob logs, Table logs** and **Queue logs.**</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image013.png)

4. <span data-ttu-id="c454d-228">Hello hello 슬라이더를 사용 하 여 hello 맨 아래에, 설정 **보존** 정책 일 (1-365 값).</span><span class="sxs-lookup"><span data-stu-id="c454d-228">Using hello slider at hello bottom, set hello **retention** policy in days (value of 1 – 365).</span></span> <span data-ttu-id="c454d-229">7 일 hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-229">Seven days is hello default.</span></span>

5. <span data-ttu-id="c454d-230">선택 **저장** tooapply hello 구성 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-230">Select **Save** tooapply hello configuration settings.</span></span>

<span data-ttu-id="c454d-231">저장소 로깅 로그 항목 hello 다음 개별 요청에 대 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-231">Storage Logging log entries contain hello following information about individual requests:</span></span>

- <span data-ttu-id="c454d-232">시작 시간, 종단 간 대기 시간, 서버 대기 시간 등의 타이밍 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-232">Timing information such as start time, end-to-end latency, and server latency.</span></span>

- <span data-ttu-id="c454d-233">Hello 연산 유형 같은 hello 저장소 작업의 세부 정보를 액세스, 성공 또는 실패 및 hello HTTP 상태 코드 반환 toohello 클라이언트 hello 저장소 개체 hello 클라이언트의 hello 키는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-233">Details of hello storage operation such as hello operation type, hello key of hello storage object hello client is accessing, success or failure, and hello HTTP   status code returned toohello client.</span></span>

- <span data-ttu-id="c454d-234">사용 되는 인증 hello 클라이언트 hello 유형의 같은 인증 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-234">Authentication details such as hello type of authentication hello client used.</span></span>

- <span data-ttu-id="c454d-235">Hello ETag 값과 마지막으로 수정 된 타임 스탬프와 같은 동시성 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-235">Concurrency information such as hello ETag value and last modified timestamp.</span></span>

- <span data-ttu-id="c454d-236">hello 요청 및 응답 메시지의 hello 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-236">hello sizes of hello request and response messages.</span></span>

<span data-ttu-id="c454d-237">자세한 방법은 tooenable 저장소 분석 로깅, 참조 [hello Azure 포털에서에서 저장소 계정을 모니터링 합니다.](https://docs.microsoft.com/azure/storage/common/storage-monitor-storage-account)</span><span class="sxs-lookup"><span data-stu-id="c454d-237">For more detailed instructions on how tooenable Storage Analytics logging, see [Monitor a storage account in hello Azure portal.](https://docs.microsoft.com/azure/storage/common/storage-monitor-storage-account)</span></span>

### <a name="azure-security-center"></a><span data-ttu-id="c454d-238">Azure 보안 센터</span><span class="sxs-lookup"><span data-stu-id="c454d-238">Azure Security Center</span></span> 

<span data-ttu-id="c454d-239">[Azure 보안 센터](https://azure.microsoft.com/services/security-center/) 모니터 순서 tooprevent에 Azure 리소스가의 보안 상태 hello 및 위협, 검색 및 응답에 대 한 권장 사항을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-239">[Azure Security Center](https://azure.microsoft.com/services/security-center/) monitors hello security state of your Azure resources in order tooprevent and detect threats, and provide recommendations for responding.</span></span> <span data-ttu-id="c454d-240">여러 가지 방법으로 toohelp 문서 hello 개인 정보 개인 데이터를 보호 하는 보안 조치를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-240">It provides several ways toohelp document your security measures that protect hello privacy of personal data.</span></span>

<span data-ttu-id="c454d-241">보안 상태 모니터링을 통해 보안 정책 준수를 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-241">Security health monitoring helps you ensure compliance with your security policies.</span></span> <span data-ttu-id="c454d-242">보안 모니터링 하는 것은 조직의 표준 또는 모범 사례를 충족 하지 않는 리소스 tooidentify 시스템을 감사 하는 사전 전략입니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-242">Security monitoring is a proactive strategy that audits your resources tooidentify systems that do not meet organizational standards or best practices.</span></span> <span data-ttu-id="c454d-243">다음 리소스는 hello hello 보안 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-243">You can monitor hello security state of hello following resources:</span></span>

- <span data-ttu-id="c454d-244">Compute(가상 컴퓨터 및 클라우드 서비스)</span><span class="sxs-lookup"><span data-stu-id="c454d-244">Compute (virtual machines and cloud services)</span></span>

- <span data-ttu-id="c454d-245">네트워킹(가상 네트워크)</span><span class="sxs-lookup"><span data-stu-id="c454d-245">Networking (virtual networks)</span></span>

- <span data-ttu-id="c454d-246">저장소 및 데이터(서버와 데이터베이스 감사 및 위협 감지, TDE, 저장소 암호화)</span><span class="sxs-lookup"><span data-stu-id="c454d-246">Storage and data (server and database auditing and threat detection, TDE, storage encryption)</span></span>

- <span data-ttu-id="c454d-247">응용 프로그램(잠재적 보안 문제)</span><span class="sxs-lookup"><span data-stu-id="c454d-247">Applications (potential security issues)</span></span>

<span data-ttu-id="c454d-248">이러한 범주에 대 한 보안 문제 개인 데이터의 위협 toohello 개인 정보 보호를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-248">Security issues in any of these categories could pose a threat toohello privacy of personal data.</span></span>

#### <a name="how-do-i-view-hello-security-state-of-my-azure-resources"></a><span data-ttu-id="c454d-249">내 Azure 리소스의 hello 보안 상태를 보려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="c454d-249">How do I view hello security state of my Azure resources?</span></span>

<span data-ttu-id="c454d-250">보안 센터 리소스를 Azure의 hello 보안 상태를 정기적으로 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-250">Security Center periodically analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="c454d-251">Hello에서 식별 하는 잠재적인 보안 취약점을 볼 수 있습니다 **방지** hello 대시보드의 섹션.</span><span class="sxs-lookup"><span data-stu-id="c454d-251">You can view any potential security vulnerabilities it identifies in hello **Prevention** section of hello dashboard.</span></span>

   ![](media/protection-personal-data-azure-reporting-tools/image014.png)

1. <span data-ttu-id="c454d-252">Hello에 **방지** 섹션을 선택 하는 hello **계산** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-252">In hello **Prevention** section, select hello **Compute** tile.</span></span> <span data-ttu-id="c454d-253">여기에 표시 됩니다는 **개요,** hello 함께 **가상 컴퓨터** 모든 Vm 및의 보안 상태를 나열 하 고 hello **클라우드 서비스** 웹 및 작업자 역할의 목록 보안 센터에 의해 모니터링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-253">You’ll see here an **Overview,** along with hello **Virtual machines** listing of all VMs and their security states, and hello **Cloud services** list of web and worker roles monitored by Security Center.</span></span>

2. <span data-ttu-id="c454d-254">Hello에 **개요** 탭, 자세한 내용은 추천 tooview에 두 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-254">On hello **Overview** tab, second a recommendation tooview more information.</span></span>

3. <span data-ttu-id="c454d-255">Hello에 **가상 컴퓨터** 탭 VM tooview 추가 세부 정보를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-255">On hello **Virtual machines** tab, select a VM tooview additional details.</span></span>

<span data-ttu-id="c454d-256">Azure 보안 센터에서 데이터 수집을 활성화 하는 경우 Microsoft Monitoring Agent hello 자동으로 모든 기존에 프로 비전 하 고 새로 지원 되는 모든 배포 된 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="c454d-256">When data collection is enabled in Azure Security Center, hello Microsoft Monitoring Agent is automatically provisioned on all existing and any new supported virtual machines that are deployed.</span></span> <span data-ttu-id="c454d-257">이 에이전트에서 수집된 데이터는 구독 또는 새 작업 영역에 연결된 기존 [Log Analytics](https://azure.microsoft.com/services/log-analytics/) 작업 영역 중 하나에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-257">Data collected from this agent is stored in either an existing [Log Analytics](https://azure.microsoft.com/services/log-analytics/) workspace associated with your subscription or a new workspace.</span></span>

<span data-ttu-id="c454d-258">[위협 인텔리전스 보고서](https://docs.microsoft.com/azure/security-center/security-center-threat-report)는 Security Center에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-258">[Threat Intelligence Reports](https://docs.microsoft.com/azure/security-center/security-center-threat-report) are provided by Security Center.</span></span> <span data-ttu-id="c454d-259">이러한 toohelp hello 공격자의 id, 목표, 현재 및 기록 공격 캠페인 및 전술을, 도구 및 사용 되는 프로시저를 식별 유용한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-259">These give you useful information toohelp discern hello attacker’s identity, objectives, current and historical attack campaigns, and tactics, tools and procedures used.</span></span> <span data-ttu-id="c454d-260">마이그레이션 및 수정 정보도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-260">Mitigation and remediation information is also included.</span></span>

<span data-ttu-id="c454d-261">이러한 위협 보고서의 주요 목적은 hello은 toohelp 있습니다 toorespond 효과적으로 toohello 즉시 위협 요소 및 도움말 take 측정 이후에 toomitigate hello 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-261">hello primary purpose of these threat reports is toohelp you toorespond effectively toohello immediate threat and help take measures afterward toomitigate hello issue.</span></span> <span data-ttu-id="c454d-262">프로그램 사고 대응 보고 및 감사용으로 문서화 하는 경우에 hello 보고서의 hello 정보 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-262">hello information in hello reports can also be useful when you document your incident response for reporting and auditing purposes.</span></span>

<span data-ttu-id="c454d-263">hello 위협 인텔리전스 보고서가 표시 됩니다. Hello에 대 한 링크를 통해 액세스 하는 PDF 형식으로 **보고서** hello 필드 **실행 된 의심 스러운 프로세스** Azure 보안 센터에서 각 보안 경고 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="c454d-263">hello Threat Intelligence Reports are presented in .PDF format, accessed via a link in hello **Reports** field of hello **Suspicious process executed** blade for each security alert in Azure Security Center.</span></span>

<span data-ttu-id="c454d-264">방법을 사용 하 여 tooview hello 위협 인텔리전스 보고서에 대 한 자세한 내용은 참조 하십시오. [Azure 보안 센터 위협 인텔리전스 보고서입니다.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span><span class="sxs-lookup"><span data-stu-id="c454d-264">For more information on how tooview and use hello Threat Intelligence Report, see [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c454d-265">다음 단계:</span><span class="sxs-lookup"><span data-stu-id="c454d-265">Next Steps:</span></span>

[<span data-ttu-id="c454d-266">Azure Active Directory 보고 API hello 시작</span><span class="sxs-lookup"><span data-stu-id="c454d-266">Getting Started with hello Azure Active Directory reporting API</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started-azure-portal)

[<span data-ttu-id="c454d-267">Log Analytics란?</span><span class="sxs-lookup"><span data-stu-id="c454d-267">What is Log Analytics?</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)

[<span data-ttu-id="c454d-268">Microsoft Azure의 모니터링 개요</span><span class="sxs-lookup"><span data-stu-id="c454d-268">Overview of Monitoring in Microsoft Azure</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

[<span data-ttu-id="c454d-269">소개 toohello Azure 활동 로그 (비디오)</span><span class="sxs-lookup"><span data-stu-id="c454d-269">Introduction toohello Azure Activity Log (video)</span></span>](https://azure.microsoft.com/resources/videos/intro-activity-log/)
