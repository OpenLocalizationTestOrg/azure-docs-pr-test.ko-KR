---
title: "SaaS 응용 프로그램에 대한 Azure Active Directory 자동 사용자 계정 프로비전 보고 | Microsoft Docs"
description: "자동 사용자 계정 프로비전 작업의 상태를 확인하는 방법과 개별 사용자의 프로비전 문제를 해결하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: asmalser-msft
ms.openlocfilehash: 86b9a3d93745045904c6038583b9bc6ebac5667e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-reporting-on-automatic-user-account-provisioning"></a><span data-ttu-id="8c773-103">자습서: 자동 사용자 계정 프로비전에 대한 보고</span><span class="sxs-lookup"><span data-stu-id="8c773-103">Tutorial: Reporting on automatic user account provisioning</span></span>


<span data-ttu-id="8c773-104">Azure Active Directory에는 종단 간 ID 수명 주기 관리를 위해 SaaS 앱 및 기타 시스템에서 사용자 계정을 자동으로 프로비전하거나 프로비전 해제하는 데 유용한 [사용자 계정 프로비전 서비스](active-directory-saas-app-provisioning.md)가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-104">Azure Active Directory includes a [user account provisioning service](active-directory-saas-app-provisioning.md) that helps automate the provisioning de-provisioning of user accounts in SaaS apps and other systems, for the purpose of end-to-end identity lifecycle management.</span></span> <span data-ttu-id="8c773-105">Azure AD는 [Azure AD 응용 프로그램 갤러리](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured)의 "추천 앱" 섹션에 있는 모든 응용 프로그램 및 시스템에 대해 사전 통합된 사용자 프로비전 커넥터를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-105">Azure AD supports pre-integrated user provisioning connectors for all of the applications and systems in the "Featured" section of the [Azure AD application gallery](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured).</span></span>

<span data-ttu-id="8c773-106">이 문서에서는 프로비전 작업을 설정한 후 해당 상태를 확인하는 방법과 개별 사용자 및 그룹의 프로비전 문제를 해결하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-106">This article describes how to check the status of provisioning jobs after they have been set up, and how to troubleshoot the provisioning of individual users and groups.</span></span>

## <a name="overview"></a><span data-ttu-id="8c773-107">개요</span><span class="sxs-lookup"><span data-stu-id="8c773-107">Overview</span></span>

<span data-ttu-id="8c773-108">프로비전 커넥터는 주로 사용자 계정 프로비전이 필요한 응용 프로그램에 [제공된 설명서](active-directory-saas-tutorial-list.md)에 따라 [Azure 관리 포털](https://portal.azure.com)을 사용하여 설정하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-108">Provisioning connectors are primarily set up and configured using the [Azure management portal](https://portal.azure.com), by following the [provided documentation](active-directory-saas-tutorial-list.md) for the application where user account provisioning is desired.</span></span> <span data-ttu-id="8c773-109">일단 구성되고 실행된 후에는 다음 두 가지 방법 중 하나를 사용하여 응용 프로그램에 대한 프로비전 작업을 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-109">Once configured and running, provisioning jobs for an application can be reported on using one of two methods:</span></span>

* <span data-ttu-id="8c773-110">**Azure 관리 포털** - 이 문서에서는 주로 지정된 응용 프로그램에 대한 프로비전 요약 보고서와 자세한 프로비전 감사 로그를 제공하는 [Azure 관리 포털](https://portal.azure.com)에서 보고서 정보를 검색하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-110">**Azure management portal** - This article primarily describes retrieving report information from the [Azure management portal](https://portal.azure.com), which provides both a provisioning summary report as well as detailed provisioning audit logs for a given application.</span></span>

* <span data-ttu-id="8c773-111">**감사 API** - Azure Active Directory는 자세한 프로비전 감사 로그를 프로그래밍 방식으로 검색할 수 있게 해주는 감사 API도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-111">**Audit API** - Azure Active Directory also provides an Audit API that enables programmatic retrieval of the detailed provisioning audit logs.</span></span> <span data-ttu-id="8c773-112">이 API의 사용과 관련하여 [Azure Active Directory 감사 API 참조](active-directory-reporting-api-audit-reference.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8c773-112">See [Azure Active Directory audit API reference](active-directory-reporting-api-audit-reference.md) for documentation specific to using this API.</span></span> <span data-ttu-id="8c773-113">이 문서에서는 API를 사용하는 방법을 구체적으로 다루지 않지만, 감사 로그에 기록되는 프로비전 이벤트 유형에 대해서는 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-113">While this article does not specifically cover how to use the API, it does detail the types of provisioning events that are recorded in the audit log.</span></span>

### <a name="definitions"></a><span data-ttu-id="8c773-114">정의</span><span class="sxs-lookup"><span data-stu-id="8c773-114">Definitions</span></span>

<span data-ttu-id="8c773-115">이 문서에서 사용하는 용어는 다음과 같이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-115">This article uses the following terms, defined below:</span></span>

* <span data-ttu-id="8c773-116">**원본 시스템** - Azure AD 프로비전 서비스에서 동기화하기 위해 원본이 되는 사용자의 리포지토리입니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-116">**Source System** - The repository of users that the Azure AD provisioning service synchronizes from.</span></span> <span data-ttu-id="8c773-117">Azure Active Directory는 대부분의 사전 통합된 프로비전 커넥터를 위한 원본 시스템이지만, Workday 인바운드 동기화와 같이 일부 예외가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-117">Azure Active Directory is the source system for the majority of pre-integrated provisioning connectors, however there are some exceptions (example: Workday Inbound Synchronization).</span></span>

* <span data-ttu-id="8c773-118">**대상 시스템** - Azure AD 프로비전 서비스에서 동기화하기 위해 대상이 되는 사용자의 리포지토리입니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-118">**Target System** - The repository of users that the Azure AD provisioning service synchronizes to.</span></span> <span data-ttu-id="8c773-119">이 시스템은 일반적으로 SaaS 응용 프로그램(예: Salesforce, ServiceNow, Google Apps, Dropbox for Business)이지만, Active Directory와 같은 온-프레미스 시스템일 수도 있습니다(예: Active Directory에 대한 Workday 인바운드 동기화).</span><span class="sxs-lookup"><span data-stu-id="8c773-119">This is typically a SaaS application (examples: Salesforce, ServiceNow, Google Apps, Dropbox for Business), but in some cases can be an on-premises system such as Active Directory (example: Workday Inbound Synchronization to Active Directory).</span></span>


## <a name="getting-provisioning-reports-from-the-azure-management-portal"></a><span data-ttu-id="8c773-120">Azure 관리 포털에서 프로비전 보고서 가져오기</span><span class="sxs-lookup"><span data-stu-id="8c773-120">Getting provisioning reports from the Azure management portal</span></span>

<span data-ttu-id="8c773-121">지정된 응용 프로그램에 대한 프로비전 보고서 정보를 가져오려면 [Azure 관리 포털](https://portal.azure.com)을 시작하고 프로비전이 구성된 엔터프라이즈 응용 프로그램을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-121">To get provisioning report information for a given application, start by launching the [Azure management portal](https://portal.azure.com) and browsing to the Enterprise Application for which provisioning is configured.</span></span> <span data-ttu-id="8c773-122">예를 들어 사용자를 LinkedIn Elevate로 프로비전하는 경우 응용 프로그램 세부 정보의 탐색 경로는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-122">For example, if you are provisioning users to LinkedIn Elevate, the navigation path to the application details is:</span></span>

<span data-ttu-id="8c773-123">**Azure Active Directory > 엔터프라이즈 응용 프로그램 > 모든 응용 프로그램 > LinkedIn Elevate**</span><span class="sxs-lookup"><span data-stu-id="8c773-123">**Azure Active Directory > Enterprise Applications > All applications > LinkedIn Elevate**</span></span>

<span data-ttu-id="8c773-124">여기서는 아래에서 설명하는 프로비전 요약 보고서와 프로비전 감사 로그에 모두 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-124">From here, you can access both the Provisioning summary report, and the provisioning audit logs, both described below.</span></span>


### <a name="provisioning-summary-report"></a><span data-ttu-id="8c773-125">요약 보고서 프로비전</span><span class="sxs-lookup"><span data-stu-id="8c773-125">Provisioning summary report</span></span>

<span data-ttu-id="8c773-126">프로비전 요약 보고서는 지정된 응용 프로그램에 대한 **프로비전** 탭에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-126">The provisioning summary report is visible in the **Provisioning** tab for given application.</span></span> <span data-ttu-id="8c773-127">**설정** 아래의 [동기화 세부 정보] 섹션에 있으며, 제공되는 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-127">It is located in the Synchronization Details section underneath **Settings**, and provides the following information:</span></span>

* <span data-ttu-id="8c773-128">동기화되어 현재의 원본 시스템과 대상 시스템 간 프로비전에 해당하는 범위에 포함된 총 사용자 및/또는 그룹 수</span><span class="sxs-lookup"><span data-stu-id="8c773-128">The total number of users and/groups that have been synchronized and are currently in scope for provisioning between the source system and the target system.</span></span>

* <span data-ttu-id="8c773-129">동기화가 마지막으로 실행된 시간 -</span><span class="sxs-lookup"><span data-stu-id="8c773-129">The last time the synchronization was run.</span></span> <span data-ttu-id="8c773-130">일반적으로 전체 동기화가 완료된 후 20-40분마다 동기화가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-130">Synchronizations typically occur every 20-40 minutes, after a full synchronization has completed.</span></span>

* <span data-ttu-id="8c773-131">초기 전체 동기화가 완료되었는지 여부</span><span class="sxs-lookup"><span data-stu-id="8c773-131">Whether or not an initial full synchronization has been completed.</span></span>

* <span data-ttu-id="8c773-132">프로비전 프로세스의 격리 여부 및 격리 상태에 대한 이유(예: 잘못된 관리자 자격 증명으로 인해 대상 시스템과 통신하지 못하는 경우)</span><span class="sxs-lookup"><span data-stu-id="8c773-132">Whether or not the provisioning process has been placed in quarantine, and what the reason for the quarantine status is (e.g. failure to communicate with target system due to invalid admin credentials)</span></span>

<span data-ttu-id="8c773-133">프로비전 요약 보고서는 프로비전 작업의 작동 상태를 확인하기 위해 관리자가 먼저 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-133">The provisioning summary report should be the first place admins look to check on the operational health of the provisioning job.</span></span>

 ![요약 보고서](./media/active-directory-saas-provisioning-reporting/summary_report.PNG)

### <a name="provisioning-audit-logs"></a><span data-ttu-id="8c773-135">감사 로그 프로비전</span><span class="sxs-lookup"><span data-stu-id="8c773-135">Provisioning audit logs</span></span>
<span data-ttu-id="8c773-136">프로비전 서비스에서 수행되는 모든 활동은 Azure AD 감사 로그에 기록되며, **계정 프로비전** 범주 아래의 **감사 로그** 탭에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-136">All activities performed by the provisioning service are recorded in the Azure AD audit logs, which can be viewed in the **Audit logs** tab under the **Account Provisioning** category.</span></span> <span data-ttu-id="8c773-137">기록되는 활동 이벤트 유형은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-137">Logged activity event types include:</span></span>

* <span data-ttu-id="8c773-138">**가져오기 이벤트** - Azure AD 프로비전 서비스에서 원본 시스템 또는 대상 시스템의 개별 사용자 또는 그룹에 대한 정보를 검색할 때마다 "가져오기" 이벤트가 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-138">**Import events** - An "import" event is recorded each time the Azure AD provisioning service retrieves information about an individual user or group from a source system or target system.</span></span> <span data-ttu-id="8c773-139">동기화하는 동안 먼저 "가져오기" 이벤트로 기록된 결과와 함께 원본 시스템에서 사용자를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-139">During synchronization, users are retrieved from the source system first, with the results recorded as "import" events.</span></span> <span data-ttu-id="8c773-140">그런 다음 검색된 사용자와 일치하는 ID에 대해 대상 시스템에 쿼리하여 "가져오기" 이벤트로 기록된 결과와 함께 해당 ID가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-140">The matching IDs of the retrieved users are then queried against the target system to check if they exist, with the results also recorded as "import" events.</span></span> <span data-ttu-id="8c773-141">이러한 이벤트는 이벤트 발생 시 Azure AD 프로비전 서비스에서 표시한 모든 매핑된 사용자 특성과 해당 값을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-141">These events record all mapped user attributes and their values that were seen by the Azure AD provisioning service at the time of the event.</span></span> 

* <span data-ttu-id="8c773-142">**동기화 규칙 이벤트** - 원본 및 대상 시스템에서 사용자 데이터를 가져와서 평가한 후에 특성 매핑 규칙 및 구성된 모든 범위 지정 필터에 기반한 결과를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-142">**Synchronization rule events** - These events report on the results of the attribute mapping rules and any configured scoping filters, after user data has been imported and evaluated from the source and target systems.</span></span> <span data-ttu-id="8c773-143">예를 들어 원본 시스템의 사용자가 프로비전 범위에 포함되지만 대상 시스템에 존재하지 않는 것으로 간주되는 경우 이 이벤트는 대상 시스템에 해당 사용자를 프로비전할 것이라고 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-143">For example, if a user in a source system is deemed to be in scope for provisioning, and deemed to not exist in the target system, then this event records that the user will be provisioned in the target system.</span></span> 

* <span data-ttu-id="8c773-144">**내보내기 이벤트** - Azure AD 프로비전 서비스에서 사용자 계정 또는 그룹 개체를 대상 시스템에 작성할 때마다 "내보내기" 이벤트가 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-144">**Export events** - An "export" event is recorded each time the Azure AD provisioning service writes a user account or group object to a target system.</span></span> <span data-ttu-id="8c773-145">이러한 이벤트는 이벤트 발생 시 Azure AD 프로비전 서비스에서 작성한 모든 사용자 특성과 해당 값을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-145">These events record all user attributes and their values that were written by the Azure AD provisioning service at the time of the event.</span></span> <span data-ttu-id="8c773-146">사용자 계정 또는 그룹 개체를 대상 시스템에 작성하는 동안 오류가 발생하면 여기에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-146">If there was an error while writing the user account or group object to the target system, it will be displayed here.</span></span>

* <span data-ttu-id="8c773-147">**프로세스 에스크로 이벤트** - 프로비전 서비스에서 작업을 시도하는 동안 오류가 발생하고 백오프 간격으로 작업 다시 시도를 시작할 때 프로세스 에스크로가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-147">**Process escrow events** - Process escrows occur when the provisioning service encounters a failure while attempting an operation, and begins to retry the operation on a back-off interval of time.</span></span> <span data-ttu-id="8c773-148">프로비전 작업이 중지될 때마다 "에스크로" 이벤트가 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-148">An "escrow" event is recorded each time a provisioning operation was retired.</span></span>

<span data-ttu-id="8c773-149">개별 사용자에 대한 프로비전 이벤트를 볼 때 일반적으로 다음과 같은 순서로 이벤트가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-149">When looking at provisioning events for an individual user, the events normally occur in this order:</span></span>

1. <span data-ttu-id="8c773-150">가져오기 이벤트: 원본 시스템의 사용자를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-150">Import event: User is retrieved from the source system.</span></span>

2. <span data-ttu-id="8c773-151">가져오기 이벤트: 검색된 사용자의 존재 여부를 확인하기 위해 대상 시스템을 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-151">Import event: Target system is queried to check for the existence of the retrieved user.</span></span>

3. <span data-ttu-id="8c773-152">동기화 규칙 이벤트: 원본 및 대상 시스템의 사용자 데이터를 구성된 특성 매핑 규칙 및 범위 지정 필터로 평가하여 수행해야 할 작업(있는 경우)을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-152">Synchronization rule event: User data from source and target systems are evaluated against the configured attribute mapping rules and scoping filters to determine what action, if any, should be performed.</span></span>

4. <span data-ttu-id="8c773-153">내보내기 이벤트: 동기화 규칙 이벤트에서 수행해야 할 작업(예: 추가, 업데이트, 삭제)을 지시하면 해당 작업 결과를 내보내기 이벤트에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-153">Export event: If the synchronization rule event dictated that an action should be performed (e.g. Add, Update, Delete), then the results of the action are recorded in an Export event.</span></span>

![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-provisioning-reporting/audit_logs.PNG)


### <a name="looking-up-provisioning-events-for-a-specific-user"></a><span data-ttu-id="8c773-155">특정 사용자에 대한 프로비전 이벤트 조회</span><span class="sxs-lookup"><span data-stu-id="8c773-155">Looking up provisioning events for a specific user</span></span>

<span data-ttu-id="8c773-156">프로비전 감사 로그에 대한 가장 일반적인 사용 사례는 개별 사용자 계정의 프로비전 상태를 확인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-156">The most common use case for the provisioning audit logs is to check the provisioning status of an individual user account.</span></span> <span data-ttu-id="8c773-157">특정 사용자에 대한 마지막 프로비전 이벤트를 조회하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-157">To look up the last provisioning events for a specific user:</span></span>

1. <span data-ttu-id="8c773-158">**감사 로그** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-158">Go to the **Audit logs** section.</span></span>

2. <span data-ttu-id="8c773-159">**범주** 메뉴에서 **계정 프로비전**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-159">From the **Category** menu, select **Account Provisioning**.</span></span>

3. <span data-ttu-id="8c773-160">**날짜 범위** 메뉴에서 검색할 날짜 범위를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-160">In the **Date Range** menu, select the date range you want to search,</span></span>

4. <span data-ttu-id="8c773-161">**검색** 창에서 검색하려는 사용자의 사용자 ID를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-161">In the **Search** bar, enter the user ID of the user you wish to search for.</span></span> <span data-ttu-id="8c773-162">ID 값의 형식은 특성 매핑 구성에서 일치하는 기본 ID로 선택한 것과 일치해야 합니다(예: userPrincipalName 또는 직원 ID 번호).</span><span class="sxs-lookup"><span data-stu-id="8c773-162">The format of ID value should match whatever you selected as the primary matching ID in the attribute mapping configuration (e.g. userPrincipalName or employee ID number).</span></span> <span data-ttu-id="8c773-163">필요한 ID 값은 [대상] 열에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-163">The ID value required will be visible in the Target(s) column.</span></span>

5. <span data-ttu-id="8c773-164">Enter 키를 눌러 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-164">Press Enter to search.</span></span> <span data-ttu-id="8c773-165">가장 최근의 프로비전 이벤트가 먼저 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-165">The most recent provisioning events will be returned first.</span></span>

6. <span data-ttu-id="8c773-166">이벤트가 반환되면 활동 유형과 성공 또는 실패 여부를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-166">If events are returned, note the activity types and whether they succeeded or failed.</span></span> <span data-ttu-id="8c773-167">결과가 반환되지 않으면 사용자가 존재하지 않거나 전체 동기화가 아직 완료되지 않은 경우 프로비전 프로세스에서 해당 사용자를 검색하지 못했음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-167">If no results are returned, then it means the user either does not exist, or has not yet been detected by the provisioning process if a full sync has not yet completed.</span></span>

7. <span data-ttu-id="8c773-168">개별 이벤트를 클릭하면 이벤트의 일부로 검색, 평가 또는 작성된 모든 사용자 특성을 포함하여 펼쳐진 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-168">Click on individual events to view extended details, including all user properties that were retrieved, evaluated, or written as part of the event.</span></span>


### <a name="tips-for-viewing-the-provisioning-audit-logs"></a><span data-ttu-id="8c773-169">프로비전 감사 로그 보기 팁</span><span class="sxs-lookup"><span data-stu-id="8c773-169">Tips for viewing the provisioning audit logs</span></span>

<span data-ttu-id="8c773-170">Azure Portal에서 최상의 가독성을 얻으려면 **열** 단추를 선택하고 다음 열을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-170">For best readability in the Azure portal, select the **Columns** button and choose these columns:</span></span>

* <span data-ttu-id="8c773-171">**날짜** - 이벤트가 발생한 날짜를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-171">**Date** - Shows the date the event occurred.</span></span>
* <span data-ttu-id="8c773-172">**대상** - 이벤트의 주체인 앱 이름과 사용자 ID를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-172">**Target(s)** - Shows the app name and user ID that are the subjects of the event.</span></span>
* <span data-ttu-id="8c773-173">**활동** - 앞에서 설명한 활동 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-173">**Activity** - The activity type, as described previously.</span></span>
* <span data-ttu-id="8c773-174">**상태** - 이벤트가 성공했는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-174">**Status** - Whether the event succeeded or not.</span></span>
* <span data-ttu-id="8c773-175">**상태 설명** - 프로비전 이벤트에서 발생한 상황에 대한 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-175">**Status Reason** - A summary of what happened in the provisioning event.</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="8c773-176">문제 해결</span><span class="sxs-lookup"><span data-stu-id="8c773-176">Troubleshooting</span></span>

<span data-ttu-id="8c773-177">프로비전 요약 보고서 및 감사 로그는 관리자가 다양한 사용자 계정 프로비전 문제를 해결하는 데 중요한 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c773-177">The provisioning summary report and audit logs play a key role helping admins troubleshoot various user account provisioning issues.</span></span>

<span data-ttu-id="8c773-178">자동 사용자 프로비전 문제를 해결하는 방법에 대한 시나리오 기반 지침은 [응용 프로그램에 사용자를 구성 및 프로비전하는 문제](active-directory-application-provisioning-content-map.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8c773-178">For scenario-based guidance on how to troubleshoot automatic user provisioning, see [Problems configuring and provisioning users to an application](active-directory-application-provisioning-content-map.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="8c773-179">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="8c773-179">Additional Resources</span></span>

* [<span data-ttu-id="8c773-180">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="8c773-180">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="8c773-181">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="8c773-181">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
