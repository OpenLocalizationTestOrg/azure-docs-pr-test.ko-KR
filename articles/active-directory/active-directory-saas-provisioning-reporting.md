---
title: "Azure Active Directory 자동 사용자 계정 tooSaaS 응용 프로그램을 프로 비전에 대 한 보고 | Microsoft Docs"
description: "Toocheck hello 자동 사용자 계정 작업, 프로 비전 상태 방법 등에 대해 알아보기 tootroubleshoot hello 개별 사용자의 프로 비전 합니다."
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
ms.openlocfilehash: 5dcf9e5dbaacf3a2c81183c5d81e331858671b86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-reporting-on-automatic-user-account-provisioning"></a><span data-ttu-id="aa811-103">자습서: 자동 사용자 계정 프로비전에 대한 보고</span><span class="sxs-lookup"><span data-stu-id="aa811-103">Tutorial: Reporting on automatic user account provisioning</span></span>


<span data-ttu-id="aa811-104">Azure Active Directory에 포함 되어는 [서비스 프로 비전 하는 사용자 계정](active-directory-saas-app-provisioning.md) hello 프로비저닝 SaaS 앱와 종단 간 identity 수명 주기의 hello 목적을 위해 다른 시스템의 사용자 계정 프로 비전 해제 자동화 하 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-104">Azure Active Directory includes a [user account provisioning service](active-directory-saas-app-provisioning.md) that helps automate hello provisioning de-provisioning of user accounts in SaaS apps and other systems, for hello purpose of end-to-end identity lifecycle management.</span></span> <span data-ttu-id="aa811-105">Azure AD 커넥터 hello 응용 프로그램과의 hello hello "주요" 섹션에에서는 시스템의 모든 프로 비전 하는 사전 통합 된 사용자를 지원 [Azure AD 응용 프로그램 갤러리](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-105">Azure AD supports pre-integrated user provisioning connectors for all of hello applications and systems in hello "Featured" section of hello [Azure AD application gallery](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured).</span></span>

<span data-ttu-id="aa811-106">이 문서에서는 프로 비전의 toocheck hello 상태를 설정 된 후 작업 하는 방법을 설명 tootroubleshoot hello 개별 사용자 및 그룹의 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-106">This article describes how toocheck hello status of provisioning jobs after they have been set up, and how tootroubleshoot hello provisioning of individual users and groups.</span></span>

## <a name="overview"></a><span data-ttu-id="aa811-107">개요</span><span class="sxs-lookup"><span data-stu-id="aa811-107">Overview</span></span>

<span data-ttu-id="aa811-108">프로 비전 커넥터는 기본적으로 설정 되 고 hello를 사용 하 여 구성 [Azure 관리 포털](https://portal.azure.com), 다음 hello 여 [설명서 제공](active-directory-saas-tutorial-list.md) hello 응용 프로그램 사용자 계정 프로 비전에 대 한 방법이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-108">Provisioning connectors are primarily set up and configured using hello [Azure management portal](https://portal.azure.com), by following hello [provided documentation](active-directory-saas-tutorial-list.md) for hello application where user account provisioning is desired.</span></span> <span data-ttu-id="aa811-109">일단 구성되고 실행된 후에는 다음 두 가지 방법 중 하나를 사용하여 응용 프로그램에 대한 프로비전 작업을 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-109">Once configured and running, provisioning jobs for an application can be reported on using one of two methods:</span></span>

* <span data-ttu-id="aa811-110">**Azure 관리 포털** -주로 설명 hello에서 보고서 정보를 검색 [Azure 관리 포털](https://portal.azure.com)는 프로 비전 요약 보고서를 비롯해 자세한 프로 비전을 제공 하는 지정된 된 응용 프로그램에 대 한 로그를 감사 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-110">**Azure management portal** - This article primarily describes retrieving report information from hello [Azure management portal](https://portal.azure.com), which provides both a provisioning summary report as well as detailed provisioning audit logs for a given application.</span></span>

* <span data-ttu-id="aa811-111">**감사 API** -Azure Active Directory도 감사 API hello의 프로그래밍 방식으로 검색 프로비저닝 자세한 감사 로그를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-111">**Audit API** - Azure Active Directory also provides an Audit API that enables programmatic retrieval of hello detailed provisioning audit logs.</span></span> <span data-ttu-id="aa811-112">참조 [Azure Active Directory 감사 API 참조](active-directory-reporting-api-audit-reference.md) 특정 toousing 설명서에 대 한이 API입니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-112">See [Azure Active Directory audit API reference](active-directory-reporting-api-audit-reference.md) for documentation specific toousing this API.</span></span> <span data-ttu-id="aa811-113">이 적용 되지 않습니다 특히 어떻게 toouse hello API, 동안 hello hello 감사 로그에 기록 되는 이벤트를 프로 비전 유형의 자세히 설명지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-113">While this article does not specifically cover how toouse hello API, it does detail hello types of provisioning events that are recorded in hello audit log.</span></span>

### <a name="definitions"></a><span data-ttu-id="aa811-114">정의</span><span class="sxs-lookup"><span data-stu-id="aa811-114">Definitions</span></span>

<span data-ttu-id="aa811-115">이 문서에서는 아래에 정의 된 용어를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-115">This article uses hello following terms, defined below:</span></span>

* <span data-ttu-id="aa811-116">**원본 시스템** -Azure AD에 프로 비전 서비스 hello 하는 사용자의 hello 저장소에서 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-116">**Source System** - hello repository of users that hello Azure AD provisioning service synchronizes from.</span></span> <span data-ttu-id="aa811-117">하지만 Azure Active Directory는 hello 대부분의 hello 소스 시스템 미리 통합 된 커넥터를 공급, 일부의 예외가 있습니다 (예: Workday 인바운드 동기화).</span><span class="sxs-lookup"><span data-stu-id="aa811-117">Azure Active Directory is hello source system for hello majority of pre-integrated provisioning connectors, however there are some exceptions (example: Workday Inbound Synchronization).</span></span>

* <span data-ttu-id="aa811-118">**시스템용** -hello 리포지토리 hello Azure AD에 프로 비전 서비스 사용자를 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-118">**Target System** - hello repository of users that hello Azure AD provisioning service synchronizes to.</span></span> <span data-ttu-id="aa811-119">이 일반적으로 SaaS 응용 프로그램 (예: Salesforce, ServiceNow, Google Apps, Dropbox for Business), 하지만 경우에 따라 Active Directory와 같은 온-프레미스 시스템 될 수 있습니다 (예: Workday 인바운드 동기화 tooActive 디렉터리).</span><span class="sxs-lookup"><span data-stu-id="aa811-119">This is typically a SaaS application (examples: Salesforce, ServiceNow, Google Apps, Dropbox for Business), but in some cases can be an on-premises system such as Active Directory (example: Workday Inbound Synchronization tooActive Directory).</span></span>


## <a name="getting-provisioning-reports-from-hello-azure-management-portal"></a><span data-ttu-id="aa811-120">프로비저닝 hello Azure 관리 포털에서 보고서 가져오기</span><span class="sxs-lookup"><span data-stu-id="aa811-120">Getting provisioning reports from hello Azure management portal</span></span>

<span data-ttu-id="aa811-121">지정된 된 응용 프로그램에 대 한 보고서 정보를 프로 비전 tooget hello를 시작 하 여 시작 [Azure 관리 포털](https://portal.azure.com) 검색 toohello 엔터프라이즈 프로 비전 구성 된 응용 프로그램 및입니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-121">tooget provisioning report information for a given application, start by launching hello [Azure management portal](https://portal.azure.com) and browsing toohello Enterprise Application for which provisioning is configured.</span></span> <span data-ttu-id="aa811-122">예를 들어 사용자가 tooLinkedIn 권한 상승 프로 비전 하는 hello 탐색 경로 toohello 응용 프로그램 세부 정보는:</span><span class="sxs-lookup"><span data-stu-id="aa811-122">For example, if you are provisioning users tooLinkedIn Elevate, hello navigation path toohello application details is:</span></span>

<span data-ttu-id="aa811-123">**Azure Active Directory > 엔터프라이즈 응용 프로그램 > 모든 응용 프로그램 > LinkedIn Elevate**</span><span class="sxs-lookup"><span data-stu-id="aa811-123">**Azure Active Directory > Enterprise Applications > All applications > LinkedIn Elevate**</span></span>

<span data-ttu-id="aa811-124">여기에서는 hello 프로 비전 요약 보고서와 hello 프로 비전 하는 감사 로그에 모두 액세스할 수 있습니다, 둘 다 아래에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-124">From here, you can access both hello Provisioning summary report, and hello provisioning audit logs, both described below.</span></span>


### <a name="provisioning-summary-report"></a><span data-ttu-id="aa811-125">요약 보고서 프로비전</span><span class="sxs-lookup"><span data-stu-id="aa811-125">Provisioning summary report</span></span>

<span data-ttu-id="aa811-126">요약 보고서를 프로 비전 하는 hello hello에 표시 됩니다. **프로 비전** 지정한 응용 프로그램에 대 한 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-126">hello provisioning summary report is visible in hello **Provisioning** tab for given application.</span></span> <span data-ttu-id="aa811-127">Hello 동기화 세부 정보 섹션 아래에 있는 **설정**, hello 다음 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-127">It is located in hello Synchronization Details section underneath **Settings**, and provides hello following information:</span></span>

* <span data-ttu-id="aa811-128">사용자의 총 hello 및 있는 동기화 된 그룹과 현재 hello 원본 시스템과 대상 시스템 hello 사이의 프로 비전에 대 한 범위에 /입니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-128">hello total number of users and/groups that have been synchronized and are currently in scope for provisioning between hello source system and hello target system.</span></span>

* <span data-ttu-id="aa811-129">hello 마지막 hello 동기화를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-129">hello last time hello synchronization was run.</span></span> <span data-ttu-id="aa811-130">일반적으로 전체 동기화가 완료된 후 20-40분마다 동기화가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-130">Synchronizations typically occur every 20-40 minutes, after a full synchronization has completed.</span></span>

* <span data-ttu-id="aa811-131">초기 전체 동기화가 완료되었는지 여부</span><span class="sxs-lookup"><span data-stu-id="aa811-131">Whether or not an initial full synchronization has been completed.</span></span>

* <span data-ttu-id="aa811-132">Hello를 프로 비전 프로세스를 격리에 배치 된 여부 및 hello 격리 상태 어떤 hello 원인은 예: (tooinvalid 관리자 자격 증명 인해 대상 시스템으로 실패 toocommunicate)</span><span class="sxs-lookup"><span data-stu-id="aa811-132">Whether or not hello provisioning process has been placed in quarantine, and what hello reason for hello quarantine status is (e.g. failure toocommunicate with target system due tooinvalid admin credentials)</span></span>

<span data-ttu-id="aa811-133">요약 보고서를 프로 비전 하는 hello hello 첫 번째 위치 admins 모양을 toocheck hello hello 프로 비전 작업이의 작동 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-133">hello provisioning summary report should be hello first place admins look toocheck on hello operational health of hello provisioning job.</span></span>

 ![요약 보고서](./media/active-directory-saas-provisioning-reporting/summary_report.PNG)

### <a name="provisioning-audit-logs"></a><span data-ttu-id="aa811-135">감사 로그 프로비전</span><span class="sxs-lookup"><span data-stu-id="aa811-135">Provisioning audit logs</span></span>
<span data-ttu-id="aa811-136">서비스를 프로 비전 하는 hello가 수행한 모든 활동은 hello에서 볼 수 있는 hello Azure AD 감사 로그에 기록 **감사 로그** hello 아래의 탭 **계정 프로 비전** 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-136">All activities performed by hello provisioning service are recorded in hello Azure AD audit logs, which can be viewed in hello **Audit logs** tab under hello **Account Provisioning** category.</span></span> <span data-ttu-id="aa811-137">기록되는 활동 이벤트 유형은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-137">Logged activity event types include:</span></span>

* <span data-ttu-id="aa811-138">**이벤트를 가져올** -"가져오기" 이벤트에는 원본 시스템 또는 대상 시스템에서 개별 사용자 또는 그룹에 대 한 정보를 검색 하는 hello Azure AD에 프로 비전 서비스 때마다 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-138">**Import events** - An "import" event is recorded each time hello Azure AD provisioning service retrieves information about an individual user or group from a source system or target system.</span></span> <span data-ttu-id="aa811-139">동기화 하는 동안 사용자가 "가져오기" 이벤트로 기록 하는 hello 결과 함께 먼저 hello 원본 시스템에서 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-139">During synchronization, users are retrieved from hello source system first, with hello results recorded as "import" events.</span></span> <span data-ttu-id="aa811-140">이벤트 "가져오기"으로 기록 hello 결과 함께 존재 하는 경우 대상 시스템 toocheck hello에 대 한 검색 hello 사용자의 Id를 일치 하는 다음 쿼리는 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-140">hello matching IDs of hello retrieved users are then queried against hello target system toocheck if they exist, with hello results also recorded as "import" events.</span></span> <span data-ttu-id="aa811-141">이러한 이벤트는 모든 매핑된 사용자 속성 및 hello 이벤트의 hello 시 hello Azure AD에 프로 비전 서비스에서 확인 된 된 값을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-141">These events record all mapped user attributes and their values that were seen by hello Azure AD provisioning service at hello time of hello event.</span></span> 

* <span data-ttu-id="aa811-142">**동기화 규칙 이벤트** -hello hello 특성 매핑 규칙 결과에 이러한 이벤트를 보고 하 고 사용자 데이터를 가져온 하 고 hello 원본 시스템과 대상 시스템에서 계산 된 후 범위 지정 필터를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-142">**Synchronization rule events** - These events report on hello results of hello attribute mapping rules and any configured scoping filters, after user data has been imported and evaluated from hello source and target systems.</span></span> <span data-ttu-id="aa811-143">예를 들어 원본 시스템의 사용자 프로 비전에 대 한 범위에서 toobe 하다 고 판단 되 것으로 간주 toonot hello 대상 시스템에 존재 하는 경우 사용자 hello이 이벤트 레코드 hello 대상 시스템에 구축 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-143">For example, if a user in a source system is deemed toobe in scope for provisioning, and deemed toonot exist in hello target system, then this event records that hello user will be provisioned in hello target system.</span></span> 

* <span data-ttu-id="aa811-144">**내보내기 이벤트** -"내보내기" 이벤트가 hello Azure AD 프로 비전 서비스가 사용자 계정 또는 그룹 개체 tooa 대상 시스템에 기록 될 때마다 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-144">**Export events** - An "export" event is recorded each time hello Azure AD provisioning service writes a user account or group object tooa target system.</span></span> <span data-ttu-id="aa811-145">모든 사용자 특성 및 해당 값으로 작성 된 hello 하 여 Azure AD에 프로 비전 서비스 hello hello 이벤트 시간에는 이러한 이벤트를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-145">These events record all user attributes and their values that were written by hello Azure AD provisioning service at hello time of hello event.</span></span> <span data-ttu-id="aa811-146">Hello 사용자 계정 또는 그룹 개체 toohello 대상 시스템에 쓰는 동안 오류가 발생 하는 경우 여기 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-146">If there was an error while writing hello user account or group object toohello target system, it will be displayed here.</span></span>

* <span data-ttu-id="aa811-147">**에스크로 이벤트 처리** -프로세스 escrows 발생할 때 hello에 오류가 발생 하는 작업을 시도 하는 동안 서비스를 프로 비전 및 시간의 백오프 간격으로 tooretry hello 작업을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-147">**Process escrow events** - Process escrows occur when hello provisioning service encounters a failure while attempting an operation, and begins tooretry hello operation on a back-off interval of time.</span></span> <span data-ttu-id="aa811-148">프로비전 작업이 중지될 때마다 "에스크로" 이벤트가 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-148">An "escrow" event is recorded each time a provisioning operation was retired.</span></span>

<span data-ttu-id="aa811-149">개별 사용자에 대 한 프로 비전 이벤트를 확인 하면 hello 이벤트는 일반적으로이 순서 대로 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-149">When looking at provisioning events for an individual user, hello events normally occur in this order:</span></span>

1. <span data-ttu-id="aa811-150">가져오기 이벤트: hello 원본 시스템에서 사용자가 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-150">Import event: User is retrieved from hello source system.</span></span>

2. <span data-ttu-id="aa811-151">가져오기 이벤트: 대상 시스템을 검색 하는 hello 사용자의 존재 hello에 대 한 쿼리 toocheck 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-151">Import event: Target system is queried toocheck for hello existence of hello retrieved user.</span></span>

3. <span data-ttu-id="aa811-152">동기화 규칙 이벤트: 소스 및 대상 시스템에서 사용자 데이터는 매핑 규칙 어떤 작업을 수행 해야 하면 필터 toodetermine 범위 지정 및 구성 하는 hello 특성에 대해 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-152">Synchronization rule event: User data from source and target systems are evaluated against hello configured attribute mapping rules and scoping filters toodetermine what action, if any, should be performed.</span></span>

4. <span data-ttu-id="aa811-153">이벤트 내보내기: hello 동기화 규칙 이벤트 동작 되어야 함을 지정 하는 경우 다음 hello 동작의 결과가 hello 내보내기 이벤트에 기록 됩니다 (예:: Add, Update, Delete)를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-153">Export event: If hello synchronization rule event dictated that an action should be performed (e.g. Add, Update, Delete), then hello results of hello action are recorded in an Export event.</span></span>

![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-provisioning-reporting/audit_logs.PNG)


### <a name="looking-up-provisioning-events-for-a-specific-user"></a><span data-ttu-id="aa811-155">특정 사용자에 대한 프로비전 이벤트 조회</span><span class="sxs-lookup"><span data-stu-id="aa811-155">Looking up provisioning events for a specific user</span></span>

<span data-ttu-id="aa811-156">hello 감사 로그를 프로 비전 하는 hello에 대 한 가장 일반적인 사용 사례는 toocheck hello 프로 비전의 개별 사용자 계정 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-156">hello most common use case for hello provisioning audit logs is toocheck hello provisioning status of an individual user account.</span></span> <span data-ttu-id="aa811-157">특정 사용자에 대 한 hello 마지막 프로 비전 이벤트를 toolook:</span><span class="sxs-lookup"><span data-stu-id="aa811-157">toolook up hello last provisioning events for a specific user:</span></span>

1. <span data-ttu-id="aa811-158">Toohello 이동 **감사 로그** 섹션.</span><span class="sxs-lookup"><span data-stu-id="aa811-158">Go toohello **Audit logs** section.</span></span>

2. <span data-ttu-id="aa811-159">Hello에서 **범주** 메뉴 선택 **계정 프로 비전**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-159">From hello **Category** menu, select **Account Provisioning**.</span></span>

3. <span data-ttu-id="aa811-160">Hello에 **날짜 범위** 메뉴, toosearch, 원하는 선택 hello 날짜 범위</span><span class="sxs-lookup"><span data-stu-id="aa811-160">In hello **Date Range** menu, select hello date range you want toosearch,</span></span>

4. <span data-ttu-id="aa811-161">Hello에 **검색** 막대에서 hello 사용자에 대 한 toosearch hello 사용자의 ID를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-161">In hello **Search** bar, enter hello user ID of hello user you wish toosearch for.</span></span> <span data-ttu-id="aa811-162">ID 값의 hello 형식은 hello 특성 매핑 구성 (예: userPrincipalName 나 직원 ID 번호)에서 일치 하는 기본 ID hello로 선택한 무엇이 든 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-162">hello format of ID value should match whatever you selected as hello primary matching ID in hello attribute mapping configuration (e.g. userPrincipalName or employee ID number).</span></span> <span data-ttu-id="aa811-163">hello ID 값이 필요한 hello 대상 열에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-163">hello ID value required will be visible in hello Target(s) column.</span></span>

5. <span data-ttu-id="aa811-164">Toosearch Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-164">Press Enter toosearch.</span></span> <span data-ttu-id="aa811-165">가장 최근 이벤트 프로 비전 hello 먼저 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-165">hello most recent provisioning events will be returned first.</span></span>

6. <span data-ttu-id="aa811-166">이벤트가 반환 되는 경우에 hello 활동 유형 및 성공 또는 실패 했는지 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-166">If events are returned, note hello activity types and whether they succeeded or failed.</span></span> <span data-ttu-id="aa811-167">결과가 반환 되는 경우 의미 합니다 hello 사용자 또는 존재 하지 않는 hello 전체 동기화를 아직 완료 되지 않은 경우 프로 비전 프로세스에서 아직 검색 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-167">If no results are returned, then it means hello user either does not exist, or has not yet been detected by hello provisioning process if a full sync has not yet completed.</span></span>

7. <span data-ttu-id="aa811-168">Tooview 확장 세부 정보를 검색, 평가 또는 hello 이벤트의 일부로 작성 된 모든 사용자 속성을 포함 하 여 개별 이벤트를 클릭 하십시오.</span><span class="sxs-lookup"><span data-stu-id="aa811-168">Click on individual events tooview extended details, including all user properties that were retrieved, evaluated, or written as part of hello event.</span></span>


### <a name="tips-for-viewing-hello-provisioning-audit-logs"></a><span data-ttu-id="aa811-169">감사 로그를 프로 비전 하는 hello를 보기 위한 팁</span><span class="sxs-lookup"><span data-stu-id="aa811-169">Tips for viewing hello provisioning audit logs</span></span>

<span data-ttu-id="aa811-170">Hello Azure 포털에서에서 최상의 가독성을 위해 선택 hello **열** 단추 하 고 이러한 열을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-170">For best readability in hello Azure portal, select hello **Columns** button and choose these columns:</span></span>

* <span data-ttu-id="aa811-171">**날짜** -hello 날짜 hello 이벤트가 발생 한 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-171">**Date** - Shows hello date hello event occurred.</span></span>
* <span data-ttu-id="aa811-172">**대상을** -hello 응용 프로그램 이름 및 사용자 ID를 hello 이벤트의 hello 주제가 모두 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-172">**Target(s)** - Shows hello app name and user ID that are hello subjects of hello event.</span></span>
* <span data-ttu-id="aa811-173">**활동** -앞에서 설명한 대로 활동 유형을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-173">**Activity** - hello activity type, as described previously.</span></span>
* <span data-ttu-id="aa811-174">**상태** -hello 이벤트 성공 있는지 여부.</span><span class="sxs-lookup"><span data-stu-id="aa811-174">**Status** - Whether hello event succeeded or not.</span></span>
* <span data-ttu-id="aa811-175">**상태 설명** -무슨 상황이 발생 이벤트를 프로 비전 하는 hello에 대 한 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-175">**Status Reason** - A summary of what happened in hello provisioning event.</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="aa811-176">문제 해결</span><span class="sxs-lookup"><span data-stu-id="aa811-176">Troubleshooting</span></span>

<span data-ttu-id="aa811-177">요약 보고서 및 감사 로그를 프로 비전 하는 hello 중요 한 역할 문제를 프로 비전 하는 다양 한 사용자 계정 문제를 해결 하는 관리자 수 있도록 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-177">hello provisioning summary report and audit logs play a key role helping admins troubleshoot various user account provisioning issues.</span></span>

<span data-ttu-id="aa811-178">방법에 대 한 시나리오 기반 지침에 대 한 tootroubleshoot 자동 사용자 프로비저닝, 참조 [구성 하 고 사용자가 tooan 응용 프로그램 프로 비전 문제](active-directory-application-provisioning-content-map.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa811-178">For scenario-based guidance on how tootroubleshoot automatic user provisioning, see [Problems configuring and provisioning users tooan application](active-directory-application-provisioning-content-map.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="aa811-179">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="aa811-179">Additional Resources</span></span>

* [<span data-ttu-id="aa811-180">엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리</span><span class="sxs-lookup"><span data-stu-id="aa811-180">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="aa811-181">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="aa811-181">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
