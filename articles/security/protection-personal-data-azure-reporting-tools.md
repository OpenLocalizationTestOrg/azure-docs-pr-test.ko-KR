---
title: "Azure 보고 도구로 개인 데이터의 문서 보호 | Microsoft Docs"
description: "Azure 보고 도구 서비스 및 기술을 사용하여 개인 데이터의 프라이버시를 보호하는 방법입니다."
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
ms.openlocfilehash: bd9d94f13a304f4bf9818df50541894bdbb4f379
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="document-protection-of-personal-data-with-azure-reporting-tools"></a><span data-ttu-id="2f4ae-103">Azure 보고 도구로 개인 데이터의 문서 보호</span><span class="sxs-lookup"><span data-stu-id="2f4ae-103">Document protection of personal data with Azure reporting tools</span></span>

<span data-ttu-id="2f4ae-104">이 문서에서는 Azure 보고 도구 서비스 및 기술을 사용하여 개인 데이터의 프라이버시를 보호하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-104">This article will discuss how to use Azure reporting services and technologies to help protect privacy of personal data.</span></span>

## <a name="scenario"></a><span data-ttu-id="2f4ae-105">시나리오</span><span class="sxs-lookup"><span data-stu-id="2f4ae-105">Scenario</span></span>

<span data-ttu-id="2f4ae-106">미국에 본사를 둔 대형 크루즈 회사는 영국 제도뿐만 아니라 지중해, 아드리아해 및 발트해의 여정을 제공하기 위해 운영을 확대하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-106">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, Adriatic, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="2f4ae-107">이러한 노력의 일환으로 이탈리아, 독일, 덴마크 및 영국에 기반을 둔 여러 개의 소형 크루즈 라인을 인수했습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-107">To help these efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and the U.K.</span></span>

<span data-ttu-id="2f4ae-108">이 회사는 회사 데이터의 처리 및 저장에 Microsoft Azure를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-108">The company uses Microsoft Azure for processing and storage of corporate data.</span></span> <span data-ttu-id="2f4ae-109">여기에는 전 세계 고객 기반의 이름, 주소, 전화 번호 및 신용 카드 정보와 같이 식별 가능한 개인 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="2f4ae-110">또한 모든 위치에 주소, 전화 번호, 세금 id 번호, 회사 직원에 대 한 의료 보험 정보 등 기존의 인적 자원 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-110">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="2f4ae-111">또한 크루즈 라인에서 현재 및 과거 고객과의 관계를 추적하기 위해 개인 정보가 포함된 보상 및 충성도 프로그램 구성원에 대한 대규모 데이터베이스를 유지하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-111">The cruise line also maintains a large database of reward and loyalty program members that includes personal information to track relationships with current and past customers.</span></span>

<span data-ttu-id="2f4ae-112">회사 직원은 회사의 원격 사무실에서 네트워크에 액세스하고 전 세계에 위치한 여행사는 일부 회사 리소스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-112">Corporate employees access the network from the company’s remote offices and travel agents located around the world have access to some company resources.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="2f4ae-113">문제 설명</span><span class="sxs-lookup"><span data-stu-id="2f4ae-113">Problem statement</span></span>

<span data-ttu-id="2f4ae-114">회사의 직원 및 고객의 개인 데이터에 대 한 액세스 및 개인 데이터 처리에 엄격한 제어를 적용 하려면 Azure 관리 및 보안 기능을 사용 하 고 내부 및 외부 감사자를 해당 보호 조치를 보여 주기 위해 있어야 하는 다중 계층된 보안 전략을 통해 개인 정보를 보호 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-114">The company must protect the privacy of employees’ and customers’ personal data through a multi-layered security strategy that uses Azure management and security features to impose strict controls on access to and processing of personal data, and must be able to demonstrate its protective measures to internal and external auditors.</span></span>

## <a name="company-goal"></a><span data-ttu-id="2f4ae-115">회사 목표</span><span class="sxs-lookup"><span data-stu-id="2f4ae-115">Company goal</span></span>

<span data-ttu-id="2f4ae-116">심층 방어 보안 전략의 일환으로, 개인 데이터에 대한 모든 액세스 및 처리를 추적하고 개인 데이터에 대한 적절한 개인 정보 보호 설명서가 마련되어 제공되는지 확인하는 것이 회사의 목표입니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-116">As part of its defense-in-depth security strategy, it is a company goal to track all access to and processing of personal data, and ensure that documentation of adequate privacy protections for personal data are in place and working.</span></span>

## <a name="solutions"></a><span data-ttu-id="2f4ae-117">솔루션</span><span class="sxs-lookup"><span data-stu-id="2f4ae-117">Solutions</span></span>

<span data-ttu-id="2f4ae-118">Microsoft Azure는 포괄적인 모니터링, 로깅 및 진단 도구를 제공하여 개인 데이터의 액세스 및 처리, 데이터의 지리적 흐름 및 개인 데이터에 대한 타사 액세스와 관련된 활동 및 이벤트를 추적하고 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-118">Microsoft Azure provides comprehensive monitoring, logging, and diagnostics tools to help track and record activities and events associated with accessing and processing personal data, geographic flow of data, and third-party access to personal data.</span></span> <span data-ttu-id="2f4ae-119">클라우드에서는 개인 데이터의 보안이 공동 책임이므로 Microsoft는 고객에게 다음 사항도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-119">Because security of personal data in the cloud is a shared responsibility, Microsoft also provides customers with:</span></span>

- <span data-ttu-id="2f4ae-120">고객 데이터의 자체적인 처리에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="2f4ae-120">Detailed information about its own processing of customers’ data</span></span>

- <span data-ttu-id="2f4ae-121">Microsoft에서 관리하는 보안 조치</span><span class="sxs-lookup"><span data-stu-id="2f4ae-121">Security measures administered by Microsoft</span></span>

- <span data-ttu-id="2f4ae-122">고객의 데이터를 보낼 위치와 방법</span><span class="sxs-lookup"><span data-stu-id="2f4ae-122">Where and how it sends customers’ data</span></span>

- <span data-ttu-id="2f4ae-123">Microsoft의 개인 정보 검토 프로세스의 세부 정보</span><span class="sxs-lookup"><span data-stu-id="2f4ae-123">Details of Microsoft’s own privacy reviews process</span></span>

### <a name="azure-active-directory"></a><span data-ttu-id="2f4ae-124">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2f4ae-124">Azure Active Directory</span></span>

<span data-ttu-id="2f4ae-125">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/)는 Microsoft의 클라우드 기반, 다중 테넌트 디렉터리 및 ID 관리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-125">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span> <span data-ttu-id="2f4ae-126">서비스의 로그인 및 감사 보고 기능은 고객 및 직원의 개인 데이터에 대한 적절한 액세스를 모니터링하고 확인할 수 있도록 자세한 로그인 및 응용 프로그램 사용 활동 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-126">The service’s sign-in and audit reporting capabilities provide you with detailed sign-in and application usage activity information to help you monitor and ensure proper access to customers’ and employees’ personal data.</span></span>

<span data-ttu-id="2f4ae-127">활동 보고서에는 다음 두 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-127">There are two types of activity reports:</span></span>

- <span data-ttu-id="2f4ae-128">[감사 활동 보고서/로그](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs)는 시스템 활동/작업에 대한 자세한 레코드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-128">The [audit activity reports/logs](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) provide a detailed record of system activities/tasks</span></span>

- <span data-ttu-id="2f4ae-129">[로그인 활동 보고서/로그](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins)는 감사 보고서에 나열된 각 활동을 수행한 사용자를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-129">The [sign-ins activity report/log](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) shows you who has performed each activity listed in the audit report</span></span>

<span data-ttu-id="2f4ae-130">둘을 함께 사용하면 수행한 모든 작업의 기록과 각각을 수행한 사용자를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-130">Using the two together, you can track the history of every task performed and who performed each.</span></span> <span data-ttu-id="2f4ae-131">두 보고서 유형 모두 사용자 지정이 가능하고 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-131">Both types of reports are customizable and can be filtered.</span></span>

#### <a name="how-do-i-access-the-audit-and-security-logs"></a><span data-ttu-id="2f4ae-132">감사 및 보안 로그에 액세스하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="2f4ae-132">How do I access the audit and security logs?</span></span>

<span data-ttu-id="2f4ae-133">감사 및 보안 로그는 세 가지 방법으로 Active Directory 포털에서 액세스할 수 있습니다. **활동** 섹션(**감사 로그** 또는 **로그인** 중 하나 선택)을 통하거나 Active Directory의 **관리** 아래 **사용자 및 그룹** 또는 **엔터프라이즈 응용 프로그램**에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-133">The audit and security logs can be accessed from the Active Directory portal in three different ways: through the **Activity** section (select either **Audit logs** or **Sign-ins**), or from **Users and groups** or **Enterprise applications** under **Manage** in Active Directory.</span></span> <span data-ttu-id="2f4ae-134">또한 Azure Active Directory 보고 API를 통해서도 보고서에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-134">Reports can also be accessed through the Azure Active Directory reporting API.</span></span> 

1. <span data-ttu-id="2f4ae-135">Azure Portal에서 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-135">In the Azure portal, select **Azure Active Directory.**</span></span>

2. <span data-ttu-id="2f4ae-136">**활동** 섹션에서 **감사 로그**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-136">In the **Activity** section, select **Audit logs.**</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image001.png)

3. <span data-ttu-id="2f4ae-137">도구 모음에서 **열**을 클릭하여 목록 보기를 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-137">Customize the list view by clicking **Columns** in the toolbar.</span></span>

4.  <span data-ttu-id="2f4ae-138">목록 보기에서 항목을 선택하면 사용할 수 있는 세부 정보를 모두 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-138">Select an item in the list view to see all available details about it.</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image003.png)

<span data-ttu-id="2f4ae-139">또한 Azure Active Directory 보고에는 **위험 플래그가 지정된 사용자** 및 **위험한 로그인**이라는 두 가지 유형의 보안 보고서가 포함되어 Azure 환경에서 잠재적인 위험을 모니터링하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-139">Azure Active Directory reporting also includes two types of security reports, **users flagged for risk** and **risky sign-ins**, which can help you monitor potential risks in your Azure environment.</span></span>

<span data-ttu-id="2f4ae-140">보고 서비스에 대한 자세한 내용은 [Azure Active Directory 보고](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-140">For more information about the reporting service, see [Azure Active Directory reporting](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal)</span></span>

<span data-ttu-id="2f4ae-141">Azure Active Directory에서 제공되는 보고서에 대한 자세한 내용을 보려면 [Azure Active Directory 작업 보고서](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal#activity-reports)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-141">Visit [Azure Active Directory activity reports](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal#activity-reports) for more specifics about the reports available in Azure Active Directory.</span></span> <span data-ttu-id="2f4ae-142">이 사이트에는 포털에서 [감사 로그 활동 보고서](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) 및 [로그인 활동 보고서](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins)에 액세스하고 사용하는 방법에 대한 자세한 내용이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-142">This site includes more details about how to access and use [audit logs activity reports](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) and [sign-in activity reports](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) in the portal.</span></span> <span data-ttu-id="2f4ae-143">또한 [위험에 대한 플래그가 지정된 사용자](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-user-at-risk) 및 [위험한 로그인](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-risky-sign-ins) 보안 보고서에 대한 정보도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-143">It also includes information about [users flagged for risk](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-user-at-risk) and [risky sign-in](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-risky-sign-ins) security reports.</span></span>

<span data-ttu-id="2f4ae-144">프로그래밍 방식으로 Azure Directory 보고에 연결하는 방법에 대한 자세한 내용을 보려면 [Azure Active Directory 감사 API 참조](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-audit-reference) 사이트를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-144">Visit the [Azure Active Directory audit API reference](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-audit-reference) site for more information on how to connect to Azure Directory reporting programmatically.</span></span>

### <a name="log-analytics"></a><span data-ttu-id="2f4ae-145">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="2f4ae-145">Log Analytics</span></span>

<span data-ttu-id="2f4ae-146">[Log Analytics](https://azure.microsoft.com/services/log-analytics/)는 [Azure Monitor의 데이터를 수집](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage)하여 다른 데이터와 상호 연결하고 추가 분석을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-146">[Log Analytics](https://azure.microsoft.com/services/log-analytics/) can [collect data from Azure Monitor](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage) to correlate it with other data and provide additional analysis.</span></span> <span data-ttu-id="2f4ae-147">Azure Monitor는 Azure 환경에 대한 모니터링 데이터를 수집하고 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-147">Azure Monitor collects and analyzes monitoring data for your Azure environment.</span></span> 

<span data-ttu-id="2f4ae-148">로그 검색, 뷰 및 솔루션과 같은 Log Analytics의 분석 도구는 전체 사용자 환경의 중앙 집중식 분석을 제공하는 모든 수집된 데이터에 대해 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-148">Analysis tools in Log Analytics such as log searches, views, and solutions work against all collected data, providing you with centralized analysis of your entire environment.</span></span> <span data-ttu-id="2f4ae-149">Log Analytics는 Windows 이벤트 로그, IIS 로그 및 Syslog를 집계 및 분석하여 개인 데이터가 권한이 없는 사용자에게 공개될 수 있는 잠재적인 개인 데이터 위반을 감지하는 데 도움을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-149">Log Analytics can aggregate and analyze Windows Event logs, IIS logs, and Syslogs, which can help detect potential personal data breaches that could expose personal data to unauthorized users.</span></span>

#### <a name="how-do-i-use-log-analytics"></a><span data-ttu-id="2f4ae-150">Log Analytics를 사용하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="2f4ae-150">How do I use Log Analytics?</span></span>

<span data-ttu-id="2f4ae-151">Log Analytics는 OMS 포털 또는 Azure Portal을 통해 모든 웹 브라우저에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-151">You can access Log Analytics through the OMS portal or the Azure portal, from any web browser.</span></span> <span data-ttu-id="2f4ae-152">Log Analytics는 리포지토리의 데이터를 신속하게 검색하고 통합할 수 있는 쿼리 언어를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-152">Log Analytics includes a query language to quickly retrieve and consolidate data in the repository.</span></span> <span data-ttu-id="2f4ae-153">로그 검색을 만들고 저장하여 포털에서 데이터를 직접 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-153">You can create and save Log Searches to directly analyze data in the portal.</span></span>

<span data-ttu-id="2f4ae-154">Azure Portal에서 Log Analytics 작업 영역을 만들려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-154">To create a Log Analytics workspace in the Azure portal, do the following:</span></span>

1. <span data-ttu-id="2f4ae-155">Marketplace의 서비스 목록에서 **Log Analytics**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-155">Select **Log Analytics** from the list of services in the Marketplace.</span></span>

2. <span data-ttu-id="2f4ae-156">**만들기**를 선택한 후 OMS 작업 영역 이름을 지정하고 구독, 리소스 그룹, 위치 및 가격 책정 계층을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-156">Select **Create,** then specify the name of your OMS workspace, select your subscription, resource group, location, and pricing tier.</span></span>

3. <span data-ttu-id="2f4ae-157">**확인**을 클릭하면 작업 영역 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-157">Click **OK** to display a list of your workspaces.</span></span>

4. <span data-ttu-id="2f4ae-158">세부 정보를 보려면 작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-158">Select a workspace to see its details.</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image004.png)

<span data-ttu-id="2f4ae-159">서비스에 대한 자세한 정보를 보려면 [Log Analytics 설명서](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-159">Visit the [Log Analytics documentation](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) to learn more about the service.</span></span>

<span data-ttu-id="2f4ae-160">평가 작업 영역을 만들고 서비스를 사용하는 방법에 대한 기본 사항을 보려면 [Log Analytics 작업 영역 시작](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started) 자습서를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-160">Visit the [Get started with a Log Analytics workspace](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started) tutorial to create an evaluation workspace and learn the basics of how to use the service.</span></span>

<span data-ttu-id="2f4ae-161">위에 설명된 로그와 함께 Log Analytics를 사용하도록 연결하는 방법에 대한 자세한 내용을 보려면 다음 웹 페이지를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-161">Visit the following web pages for more specific information on how to connect to use Log Analytics with the logs described above:</span></span>

[<span data-ttu-id="2f4ae-162">Log Analytics의 Windows 이벤트 로그 데이터 원본</span><span class="sxs-lookup"><span data-stu-id="2f4ae-162">Windows event logs data sources in Log Analytics</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)

[<span data-ttu-id="2f4ae-163">Log Analytics의 IIS 로그</span><span class="sxs-lookup"><span data-stu-id="2f4ae-163">IIS logs in Log Analytics</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-iis-logs)

[<span data-ttu-id="2f4ae-164">Log Analytics의 Syslog 데이터 원본</span><span class="sxs-lookup"><span data-stu-id="2f4ae-164">Syslog data sources in Log Analytics</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-syslog)

### <a name="azure-monitorazure-activity-log"></a><span data-ttu-id="2f4ae-165">Azure Monitor/Azure 활동 로그</span><span class="sxs-lookup"><span data-stu-id="2f4ae-165">Azure Monitor/Azure Activity Log</span></span> 

<span data-ttu-id="2f4ae-166">[Azure Monitor](https://azure.microsoft.com/services/monitor/)는 대부분의 Microsoft Azure 서비스에 대한 기본 수준의 인프라 메트릭과 로그를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-166">[Azure Monitor](https://azure.microsoft.com/services/monitor/) provides base level infrastructure metrics and logs for most services in Microsoft Azure.</span></span>
<span data-ttu-id="2f4ae-167">모니터링을 통해 Azure 응용 프로그램에 대한 깊은 통찰력을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-167">Monitoring can help you to gain deep insights about your Azure applications.</span></span> <span data-ttu-id="2f4ae-168">Azure Monitor는 Azure 진단 확장(Windows 또는 Linux)을 사용하여 대부분의 응용 프로그램 수준 메트릭과 로그를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-168">Azure Monitor relies on the Azure diagnostics extension (Windows or Linux) to collect most application level metrics and logs.</span></span> <span data-ttu-id="2f4ae-169">[Azure 활동 로그](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)는 Azure Monitor로 볼 수 있는 리소스 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-169">[The Azure Activity Log](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) is one of the resources you can view with Azure Monitor.</span></span> <span data-ttu-id="2f4ae-170">모든 API 호출을 추적하고 [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)에서 발생하는 활동에 대한 다양한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-170">It tracks every API call, and provides a wealth of information about activities that occur in [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span>
<span data-ttu-id="2f4ae-171">Azure 인프라에 표시되는 대로 리소스에 대한 자세한 내용은 활동 로그(이전에 작업 또는 감사 로그라고도 함)를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-171">You can search the Activity Log (previously called Operational or Audit Logs) for information about your resource as seen by the Azure infrastructure.</span></span> 

<span data-ttu-id="2f4ae-172">활동 로그에 기록된 대부분의 정보는 성능 및 서비스 상태와 관련되지만 데이터 보호와 관련된 정보도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-172">Although much of the information recorded in the Activity log pertains to performance and service health, there is also information that is related to protection of data.</span></span> <span data-ttu-id="2f4ae-173">활동 로그를 통해 Azure 구독의 리소스에 대한 모든 쓰기 작업(PUT, POST, DELETE)에서 “무엇을, 누가, 언제”를 판단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-173">Using the Activity Log, you can determine the “what, who, and when” for any write operations (PUT, POST, DELETE) taken on the resources in your Azure subscription.</span></span>

<span data-ttu-id="2f4ae-174">예를 들어 관리자가 개인 데이터 보호에 영향을 줄 수 있는 네트워크 보안 그룹을 삭제할 경우 레코드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-174">For example, it provides a record when an administrator deletes a network security group, which could impact the protection of personal data.</span></span> <span data-ttu-id="2f4ae-175">활동 로그 항목은 Azure Monitor에 90일 동안 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-175">Activity log entries are stored in Azure Monitor for 90 days.</span></span>

#### <a name="how-do-i-use-the-data-collected-by-azure-monitor"></a><span data-ttu-id="2f4ae-176">Azure Monitor로 수집된 데이터는 어떻게 사용하나요?</span><span class="sxs-lookup"><span data-stu-id="2f4ae-176">How do I use the data collected by Azure Monitor?</span></span>

<span data-ttu-id="2f4ae-177">활동 로그 및 기타 Azure Monitor 리소스의 데이터를 사용하는 방법은 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-177">There are a number of ways to use the data in the Activity log and other Azure Monitor resources.</span></span>

- <span data-ttu-id="2f4ae-178">데이터를 실제 위치에서 다른 위치로 실시간으로 스트리밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-178">You can stream the data to other locations in real line.</span></span>

- <span data-ttu-id="2f4ae-179">[Azure Storage 계정](https://docs.microsoft.com/azure/storage/common/storage-introduction)을 사용하고 보존 정책을 설정하여 기본값보다 더 오랫동안 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-179">You can store the data for longer time periods than the defaults, using an [Azure storage account](https://docs.microsoft.com/azure/storage/common/storage-introduction) and setting a retention policy.</span></span>

- <span data-ttu-id="2f4ae-180">[Azure Portal](https://azure.microsoft.com/features/azure-portal/), [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), [Microsoft PowerBI](https://powerbi.microsoft.com/) 또는 타사 시각화 도구를 사용하여 그래픽 및 차트로 데이터를 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-180">You can visual the data in graphics and charts, using the [Azure portal](https://azure.microsoft.com/features/azure-portal/), [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), [Microsoft PowerBI](https://powerbi.microsoft.com/), or third-party visualization tools.</span></span>

- <span data-ttu-id="2f4ae-181">Azure Monitor REST API, CLI 명령, [PowerShell](https://docs.microsoft.com/powershell/) cmdlet 또는 .NET SDK를 사용하여 데이터를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-181">You can query the data using the Azure Monitor REST API, CLI commands, [PowerShell](https://docs.microsoft.com/powershell/) cmdlets, or the .NET SDK.</span></span>

<span data-ttu-id="2f4ae-182">Azure Monitor를 시작하려면 Azure Portal에서 **추가 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-182">To get started with Azure Monitor, select **More Services** in the Azure portal.</span></span>

1. <span data-ttu-id="2f4ae-183">**모니터링 및 관리** 섹션에서 **모니터**로 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-183">Scroll down to **Monitor** in the **Monitoring and Managing** section.</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image005.png)

2.  <span data-ttu-id="2f4ae-184">모니터가 **활동 로그** 보기에 열립니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-184">Monitor opens in the **Activity Log** view.</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image007.png)

<span data-ttu-id="2f4ae-185">공통 필터에 대한 쿼리를 만들어 저장한 다음 가장 중요한 쿼리를 포털 대시보드에 고정하면 기준에 부합하는 이벤트가 발생할 경우 항상 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-185">You can create and save queries for common filters, then pin the most important queries to a portal dashboard so you'll always know if events that meet your criteria have occurred.</span></span>

1. <span data-ttu-id="2f4ae-186">리소스 그룹, timespan 및 이벤트 범주에 따라 보기를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-186">You can filter the view by resource group, timespan, and event category.</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image008.png)

2. <span data-ttu-id="2f4ae-187">그런 다음 **고정** 단추를 클릭하여 포털 대시보드에 쿼리를 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-187">You can then pin queries to a portal dashboard by clicking the **Pin** button.</span></span> <span data-ttu-id="2f4ae-188">이렇게 하면 서비스에 대한 운영 데이터 정보를 제공하는 단일 출처를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-188">This helps you create a single source of information for operational  data on your services.</span></span> <span data-ttu-id="2f4ae-189">쿼리 이름 및 결과 수가 대시보드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-189">The query name and number of results will be displayed on the dashboard.</span></span>

<span data-ttu-id="2f4ae-190">또한 모니터를 사용하여 모든 Azure 리소스에 대한 메트릭을 보고 진단 설정 및 경고를 구성하며 로그를 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-190">You can also use the Monitor to view metrics for all Azure resources, configure diagnostics settings and alerts, and search the log.</span></span> <span data-ttu-id="2f4ae-191">Azure Monitor 및 활동 로그를 사용하는 방법에 대한 자세한 내용은 [Azure Monitor 시작](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-191">For more information on how to use the Azure Monitor and Activity Log, see [Get Started with Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started).</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="2f4ae-192">Azure 진단</span><span class="sxs-lookup"><span data-stu-id="2f4ae-192">Azure Diagnostics</span></span> 

<span data-ttu-id="2f4ae-193">Azure의 진단 기능을 통해 여러 원본에서 데이터 수집이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-193">The diagnostics capability in Azure enables collection of data from several sources.</span></span> <span data-ttu-id="2f4ae-194">보안 로그를 포함하는 Windows 이벤트 로그는 개인 데이터 보호를 추적하고 문서화하는 데 특히 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-194">The Windows Event logs, which include the Security log, can be especially useful in tracking and documenting protection of personal data.</span></span> <span data-ttu-id="2f4ae-195">보안 로그는 로그온 성공 및 실패 이벤트는 물론 사용 권한 변경, 특정 유형의 공격을 나타내는 패턴 검색, 보안 관련 정책 변경, 보안 그룹 멤버 자격 변경 등을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-195">The security log tracks logon success and failure events, as well as permissions changes, detection of patterns indicating certain types of attacks, changes to security-related policies, security group membership changes, and much more.</span></span>

<span data-ttu-id="2f4ae-196">예를 들어 이벤트 ID 4695는 감사 가능한 보호된 데이터의 보호되지 않은 시도에 대해 경고합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-196">For example, Event ID 4695 alerts you to the attempted unprotection of auditable protected data.</span></span> <span data-ttu-id="2f4ae-197">이는 개인 키, 저장된 자격 증명 및 기타 기밀 정보와 같은 데이터를 보호하는 데 도움이 되는 DPAPI(데이터 보호 API)와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-197">This pertains to the Data Protection API (DPAPI), which helps to protect data such as private keys, stored credentials, and other confidential information.</span></span>

#### <a name="how-do-i-enable-the-diagnostics-extension-for-windows-vms"></a><span data-ttu-id="2f4ae-198">Windows VM에 대해 진단 확장을 사용하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="2f4ae-198">How do I enable the diagnostics extension for Windows VMs?</span></span>

<span data-ttu-id="2f4ae-199">PowerShell을 사용하여 Windows VM에 대해 진단 확장을 사용하도록 설정하여 로그 데이터를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-199">You can use PowerShell to enable the diagnostics extension for a Windows VM, so as to collect log data.</span></span> <span data-ttu-id="2f4ae-200">이렇게 하는 단계는 사용하는 배포 모델(리소스 관리자 또는 클래식)에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-200">The steps for doing so depend on which deployment model you use (Resource Manager or Classic).</span></span> <span data-ttu-id="2f4ae-201">리소스 관리자 배포 모델을 통해 만든 기존 VM에서 진단 확장을 사용하도록 설정하려면 [Set-AzureRMVMDiagnosticsExtension PowerShell cmdlet](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension?view=azurermps-4.3.1)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-201">To enable the diagnostics extension on an existing VM that was created through the Resource Manager deployment model, you can use the [Set-AzureRMVMDiagnosticsExtension PowerShell cmdlet](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension?view=azurermps-4.3.1).</span></span>

   ![](media/protection-personal-data-azure-reporting-tools/image009.png)

<span data-ttu-id="2f4ae-202">*\$diagnosticsconfig_path*는 XML의 진단 구성이 포함된 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-202">*\$diagnosticsconfig_path* is the path to the file that contains the diagnostics configuration in XML.</span></span> <span data-ttu-id="2f4ae-203">VM에 Azure 진단을 사용하도록 설정하는 방법은 [PowerShell을 사용하여 Windows를 실행하는 가상 컴퓨터에서 Azure 진단을 사용하도록 설정](https://docs.microsoft.com/azure/virtual-machines/windows/ps-extensions-diagnostics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-203">For more detailed instructions on enabling Azure Diagnostics on a VM, see [Use PowerShell to enable Azure Diagnostics in a virtual machine running Windows.](https://docs.microsoft.com/azure/virtual-machines/windows/ps-extensions-diagnostics)</span></span>

<span data-ttu-id="2f4ae-204">Azure 진단 확장은 수집된 데이터를 Azure Storage 계정에 전송하거나 Application Insights와 같은 서비스에 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-204">The Azure diagnostics extension can transfer the collected data to an Azure storage account or send it to services such as Application Insights.</span></span> <span data-ttu-id="2f4ae-205">그런 다음 감사를 위해 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-205">You can then use the data for auditing.</span></span>

#### <a name="how-do-i-store-and-view-diagnostic-data"></a><span data-ttu-id="2f4ae-206">진단 데이터를 저장하고 보려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="2f4ae-206">How do I store and view diagnostic data?</span></span>

<span data-ttu-id="2f4ae-207">진단 데이터를 Microsoft Azure Storage 에뮬레이터 또는 Azure Storage에 전송하지 않는 한 진단 데이터는 영구적으로 저장되지 않는다는 것을 유념해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-207">It’s important to remember that diagnostic data is not permanently stored unless you transfer it to the Microsoft Azure storage emulator or to Azure storage.</span></span> <span data-ttu-id="2f4ae-208">Azure Storage에서 진단 데이터를 저장하고 보려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-208">To store and view diagnostic data in Azure Storage, follow these steps:</span></span>

1. <span data-ttu-id="2f4ae-209">ServiceConfiguration.cscfg 파일에서 저장소 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-209">Specify a storage account in the ServiceConfiguration.cscfg file.</span></span> <span data-ttu-id="2f4ae-210">Azure 진단에서는 데이터 형식에 따라 Blob service 또는 Table service를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-210">Azure Diagnostics can use either the Blob service or the Table service, depending on the type of data.</span></span> <span data-ttu-id="2f4ae-211">Windows 이벤트 로그는 테이블 형식으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-211">Windows Event logs are stored in Table format.</span></span>

2. <span data-ttu-id="2f4ae-212">데이터를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-212">Transfer the data.</span></span> <span data-ttu-id="2f4ae-213">구성 파일을 통해 진단 데이터 전송을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-213">You can request to transfer the diagnostic data through the configuration file.</span></span> <span data-ttu-id="2f4ae-214">SDK 2.4 이하에서는 프로그래밍 방식으로 요청을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-214">For SDK 2.4 and previous, you can also make the request programmatically.</span></span>

3. <span data-ttu-id="2f4ae-215">[Azure Storage 탐색기](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer), Visual Studio의 [서버 탐색기](https://docs.microsoft.com/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) 또는 Azure Management Studio의 [Azure 진단 관리자](https://www.cerebrata.com/products/azure-diagnostics-manager)를 사용하여 데이터를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-215">View the data, using [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer),  [Server Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) in Visual Studio, or [Azure Diagnostics Manager](https://www.cerebrata.com/products/azure-diagnostics-manager) in Azure Management Studio.</span></span>

<span data-ttu-id="2f4ae-216">이러한 각 단계를 수행하는 방법에 대한 자세한 내용은 [Azure Storage에서 진단 데이터 저장 및 보기](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-216">For more information on how to perform each of these steps, see [Store and view diagnostic data in Azure Storage.](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)</span></span>

### <a name="azure-storage-analytics"></a><span data-ttu-id="2f4ae-217">Azure Storage 분석</span><span class="sxs-lookup"><span data-stu-id="2f4ae-217">Azure Storage Analytics</span></span> 

<span data-ttu-id="2f4ae-218">저장소 분석은 저장소 서비스에 대해 성공한 요청과 실패한 요청 관련 상세 정보를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-218">Storage Analytics logs detailed information about successful and failed requests to a storage service.</span></span> <span data-ttu-id="2f4ae-219">이 정보는 개별 요청을 모니터링하는 데 사용할 수 있으며 서비스에 저장된 개인 데이터에 대한 액세스를 문서화하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-219">This information can be used to monitor individual requests, which can help in documenting access to personal data stored in the service.</span></span> <span data-ttu-id="2f4ae-220">하지만 저장소 분석 로깅은 저장소 계정에 대해 기본적으로 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-220">However, Storage Analytics logging is not enabled by default for your storage account.</span></span> <span data-ttu-id="2f4ae-221">Azure Portal에서 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-221">You can enable it in the Azure portal.</span></span>

#### <a name="how-do-i-configure-monitoring-for-a-storage-account"></a><span data-ttu-id="2f4ae-222">저장소 계정에 대한 모니터링은 어떻게 구성하나요?</span><span class="sxs-lookup"><span data-stu-id="2f4ae-222">How do I configure monitoring for a storage account?</span></span>

<span data-ttu-id="2f4ae-223">저장소 계정에 대한 모니터링을 구성하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-223">To configure monitoring for a storage account, do the following:</span></span>

1. <span data-ttu-id="2f4ae-224">Azure Portal에서 **저장소 계정**을 선택한 후 모니터링하려는 계정 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-224">Select **Storage accounts** in the Azure portal, then select the name of the account you want to monitor.</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image011.png)

2. <span data-ttu-id="2f4ae-225">**모니터링** 섹션에서 **진단**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-225">In the **Monitoring** section, select **Diagnostics.**</span></span>

3.  <span data-ttu-id="2f4ae-226">각 서비스에 대해 모니터링하려는 메트릭 데이터의 **형식**을 선택합니다(Blob, 테이블, 파일).</span><span class="sxs-lookup"><span data-stu-id="2f4ae-226">Select the **type** of metrics data you want to monitor for each service (Blob, Table, File).</span></span> <span data-ttu-id="2f4ae-227">Azure Storage에서 Blob, 테이블 및 큐 서비스에 대한 읽기, 쓰기 및 삭제 요청에 대한 진단 로그를 저장하도록 지시하려면 **Blob 로그, 테이블 로그** 및 **큐 로그**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-227">To instruct Azure Storage to save diagnostics logs for read, write, and delete requests for the blob, table, and queue services, select **Blob logs, Table logs** and **Queue logs.**</span></span>

    ![](media/protection-personal-data-azure-reporting-tools/image013.png)

4. <span data-ttu-id="2f4ae-228">아래에 있는 슬라이더를 사용하여 **보존** 정책을 일 단위(1-365 값)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-228">Using the slider at the bottom, set the **retention** policy in days (value of 1 – 365).</span></span> <span data-ttu-id="2f4ae-229">기본값은 7일입니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-229">Seven days is the default.</span></span>

5. <span data-ttu-id="2f4ae-230">**저장**을 선택하여 구성 설정을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-230">Select **Save** to apply the configuration settings.</span></span>

<span data-ttu-id="2f4ae-231">저장소 로깅 로그 항목에는 개별 요청에 대 한 다음 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-231">Storage Logging log entries contain the following information about individual requests:</span></span>

- <span data-ttu-id="2f4ae-232">시작 시간, 종단 간 대기 시간, 서버 대기 시간 등의 타이밍 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-232">Timing information such as start time, end-to-end latency, and server latency.</span></span>

- <span data-ttu-id="2f4ae-233">작업 유형, 클라이언트가 액세스하는 저장소 개체의 키, 성공 또는 실패 여부, 클라이언트로 반환된 HTTP 상태 코드와 같은 저장소 작업에 대한 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-233">Details of the storage operation such as the operation type, the key of the storage object the client is accessing, success or failure, and the HTTP   status code returned to the client.</span></span>

- <span data-ttu-id="2f4ae-234">클라이언트에서 사용한 인증 유형과 같은 인증 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-234">Authentication details such as the type of authentication the client used.</span></span>

- <span data-ttu-id="2f4ae-235">ETag 값과 마지막으로 수정된 타임스탬프와 같은 동시성 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-235">Concurrency information such as the ETag value and last modified timestamp.</span></span>

- <span data-ttu-id="2f4ae-236">요청 및 응답 메시지의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-236">The sizes of the request and response messages.</span></span>

<span data-ttu-id="2f4ae-237">저장소 분석 로깅을 사용하도록 설정하는 방법에 대한 자세한 내용은 [Azure Portal에서 저장소 계정 모니터링](https://docs.microsoft.com/azure/storage/common/storage-monitor-storage-account)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-237">For more detailed instructions on how to enable Storage Analytics logging, see [Monitor a storage account in the Azure portal.](https://docs.microsoft.com/azure/storage/common/storage-monitor-storage-account)</span></span>

### <a name="azure-security-center"></a><span data-ttu-id="2f4ae-238">Azure 보안 센터</span><span class="sxs-lookup"><span data-stu-id="2f4ae-238">Azure Security Center</span></span> 

<span data-ttu-id="2f4ae-239">[Azure Security Center](https://azure.microsoft.com/services/security-center/)는 위협을 예방 및 감지하고 대응 권장 사항을 제공하기 위해 Azure 리소스의 보안 상태를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-239">[Azure Security Center](https://azure.microsoft.com/services/security-center/) monitors the security state of your Azure resources in order to prevent and detect threats, and provide recommendations for responding.</span></span> <span data-ttu-id="2f4ae-240">개인 데이터의 프라이버시를 보호하는 보안 조치를 문서화하는 데 도움이 되는 다양한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-240">It provides several ways to help document your security measures that protect the privacy of personal data.</span></span>

<span data-ttu-id="2f4ae-241">보안 상태 모니터링을 통해 보안 정책 준수를 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-241">Security health monitoring helps you ensure compliance with your security policies.</span></span> <span data-ttu-id="2f4ae-242">보안 모니터링은 리소스를 감사하여 조직의 표준 또는 모범 사례를 충족하지 않는 시스템을 식별하는 사전 예방 전략입니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-242">Security monitoring is a proactive strategy that audits your resources to identify systems that do not meet organizational standards or best practices.</span></span> <span data-ttu-id="2f4ae-243">다음 리소스의 보안 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-243">You can monitor the security state of the following resources:</span></span>

- <span data-ttu-id="2f4ae-244">Compute(가상 컴퓨터 및 클라우드 서비스)</span><span class="sxs-lookup"><span data-stu-id="2f4ae-244">Compute (virtual machines and cloud services)</span></span>

- <span data-ttu-id="2f4ae-245">네트워킹(가상 네트워크)</span><span class="sxs-lookup"><span data-stu-id="2f4ae-245">Networking (virtual networks)</span></span>

- <span data-ttu-id="2f4ae-246">저장소 및 데이터(서버와 데이터베이스 감사 및 위협 감지, TDE, 저장소 암호화)</span><span class="sxs-lookup"><span data-stu-id="2f4ae-246">Storage and data (server and database auditing and threat detection, TDE, storage encryption)</span></span>

- <span data-ttu-id="2f4ae-247">응용 프로그램(잠재적 보안 문제)</span><span class="sxs-lookup"><span data-stu-id="2f4ae-247">Applications (potential security issues)</span></span>

<span data-ttu-id="2f4ae-248">이러한 범주의 보안 문제는 개인 데이터의 프라이버시에 위협이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-248">Security issues in any of these categories could pose a threat to the privacy of personal data.</span></span>

#### <a name="how-do-i-view-the-security-state-of-my-azure-resources"></a><span data-ttu-id="2f4ae-249">Azure 리소스의 보안 상태를 보려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="2f4ae-249">How do I view the security state of my Azure resources?</span></span>

<span data-ttu-id="2f4ae-250">보안 센터에서는 Azure 리소스의 보안 상태를 주기적으로 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-250">Security Center periodically analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="2f4ae-251">대시보드의 **방지** 섹션에서 식별된 잠재적인 보안 취약성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-251">You can view any potential security vulnerabilities it identifies in the **Prevention** section of the dashboard.</span></span>

   ![](media/protection-personal-data-azure-reporting-tools/image014.png)

1. <span data-ttu-id="2f4ae-252">**방지** 섹션에서 **Compute** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-252">In the **Prevention** section, select the **Compute** tile.</span></span> <span data-ttu-id="2f4ae-253">여기에는 **개요**와 함께, 모든 VM 및 해당 보안 상태가 포함된 **가상 컴퓨터** 목록, Security Center에서 모니터링된 웹 및 작업자 역할의 **클라우드 서비스** 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-253">You’ll see here an **Overview,** along with the **Virtual machines** listing of all VMs and their security states, and the **Cloud services** list of web and worker roles monitored by Security Center.</span></span>

2. <span data-ttu-id="2f4ae-254">**개요** 탭에는 추가 정보를 볼 권장 사항이 제안됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-254">On the **Overview** tab, second a recommendation to view more information.</span></span>

3. <span data-ttu-id="2f4ae-255">**가상 컴퓨터** 탭에서 VM을 선택하여 추가 세부 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-255">On the **Virtual machines** tab, select a VM to view additional details.</span></span>

<span data-ttu-id="2f4ae-256">Azure Security Center에서 데이터 수집을 사용하도록 설정하면 Microsoft Monitoring Agent가 배포되는 모든 지원되는 새 가상 컴퓨터와 기존 가상 컴퓨터에 자동으로 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-256">When data collection is enabled in Azure Security Center, the Microsoft Monitoring Agent is automatically provisioned on all existing and any new supported virtual machines that are deployed.</span></span> <span data-ttu-id="2f4ae-257">이 에이전트에서 수집된 데이터는 구독 또는 새 작업 영역에 연결된 기존 [Log Analytics](https://azure.microsoft.com/services/log-analytics/) 작업 영역 중 하나에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-257">Data collected from this agent is stored in either an existing [Log Analytics](https://azure.microsoft.com/services/log-analytics/) workspace associated with your subscription or a new workspace.</span></span>

<span data-ttu-id="2f4ae-258">[위협 인텔리전스 보고서](https://docs.microsoft.com/azure/security-center/security-center-threat-report)는 Security Center에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-258">[Threat Intelligence Reports](https://docs.microsoft.com/azure/security-center/security-center-threat-report) are provided by Security Center.</span></span> <span data-ttu-id="2f4ae-259">이 보고서는 공격자의 ID, 목표, 현재 및 과거의 공격 캠페인, 사용된 전술, 도구 및 절차를 식별하는 데 도움이 되는 유용한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-259">These give you useful information to help discern the attacker’s identity, objectives, current and historical attack campaigns, and tactics, tools and procedures used.</span></span> <span data-ttu-id="2f4ae-260">마이그레이션 및 수정 정보도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-260">Mitigation and remediation information is also included.</span></span>

<span data-ttu-id="2f4ae-261">이러한 위협 보고서의 주요 목적은 즉각적인 위협에 효과적으로 대응하고 후속 조치를 통해 문제를 완화하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-261">The primary purpose of these threat reports is to help you to respond effectively to the immediate threat and help take measures afterward to mitigate the issue.</span></span> <span data-ttu-id="2f4ae-262">보고서에 포함된 정보는 보고 및 감사용으로 사고 대응을 문서화할 때도 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-262">The information in the reports can also be useful when you document your incident response for reporting and auditing purposes.</span></span>

<span data-ttu-id="2f4ae-263">위협 인텔리전스 보고서는 .PDF 형식으로 표시되며 Azure Security Center에서 각 보안 경고에 대한 **의심스러운 프로세스 실행** 블레이드의 **보고서** 필드에 있는 링크를 통해 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-263">The Threat Intelligence Reports are presented in .PDF format, accessed via a link in the **Reports** field of the **Suspicious process executed** blade for each security alert in Azure Security Center.</span></span>

<span data-ttu-id="2f4ae-264">위협 인텔리전스 보고서를 보고 사용하는 방법에 대한 자세한 내용은 [Azure Security Center 위협 인텔리전스 보고서](https://docs.microsoft.com/azure/security-center/security-center-threat-report)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2f4ae-264">For more information on how to view and use the Threat Intelligence Report, see [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f4ae-265">다음 단계:</span><span class="sxs-lookup"><span data-stu-id="2f4ae-265">Next Steps:</span></span>

[<span data-ttu-id="2f4ae-266">Azure Active Directory 보고 API 시작</span><span class="sxs-lookup"><span data-stu-id="2f4ae-266">Getting Started with the Azure Active Directory reporting API</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started-azure-portal)

[<span data-ttu-id="2f4ae-267">Log Analytics란?</span><span class="sxs-lookup"><span data-stu-id="2f4ae-267">What is Log Analytics?</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)

[<span data-ttu-id="2f4ae-268">Microsoft Azure의 모니터링 개요</span><span class="sxs-lookup"><span data-stu-id="2f4ae-268">Overview of Monitoring in Microsoft Azure</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

[<span data-ttu-id="2f4ae-269">Azure 활동 로그 소개(비디오)</span><span class="sxs-lookup"><span data-stu-id="2f4ae-269">Introduction to the Azure Activity Log (video)</span></span>](https://azure.microsoft.com/resources/videos/intro-activity-log/)
