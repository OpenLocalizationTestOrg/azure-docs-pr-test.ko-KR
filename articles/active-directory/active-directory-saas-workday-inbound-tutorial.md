---
title: "자습서: 온-프레미스 Active Directory 및 Azure Active Directory를 사용하여 사용자를 자동으로 프로비전하도록 Workday 구성 | Microsoft Docs"
description: "Active Directory 및 Azure Active Directory의 ID 데이터의 원본으로 Workday를 사용하는 방법에 대해 알아봅니다."
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: 1a2c375a-1bb1-4a61-8115-5a69972c6ad6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/26/2017
ms.author: asmalser
ms.openlocfilehash: f9cc94ca1fc44d10af19debab49435b265bf6e7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configure-workday-for-automatic-user-provisioning-with-on-premises-active-directory-and-azure-active-directory"></a><span data-ttu-id="16c76-103">자습서: 온-프레미스 Active Directory 및 Azure Active Directory를 사용하여 사용자를 자동으로 프로비전하도록 Workday 구성</span><span class="sxs-lookup"><span data-stu-id="16c76-103">Tutorial: Configure Workday for automatic user provisioning with on-premises Active Directory and Azure Active Directory</span></span>
<span data-ttu-id="16c76-104">이 자습서의 목표는 Workday에서 Active Directory 및 Azure Active Directory로 사람을 가져오기 위해 수행해야 하는 단계, 그리고 선택 사항으로 일부 특성을 Workday에 쓰는 방법을 보여주는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-104">The objective of this tutorial is to show you the steps you need to perform to import people from Workday into both Active Directory and Azure Active Directory, with optional writeback of some attributes to Workday.</span></span> 



## <a name="overview"></a><span data-ttu-id="16c76-105">개요</span><span class="sxs-lookup"><span data-stu-id="16c76-105">Overview</span></span>

<span data-ttu-id="16c76-106">[Azure Active Directory 사용자 프로비전 서비스](active-directory-saas-app-provisioning.md)는 사용자 계정을 프로비전하기 위해 [Workday 인적 자원 API](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html)와 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-106">The [Azure Active Directory user provisioning service](active-directory-saas-app-provisioning.md) integrates with the [Workday Human Resources API](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html) in order to provision user accounts.</span></span> <span data-ttu-id="16c76-107">Azure AD는 이 연결을 사용하여 다음 사용자 프로비전 워크플로를 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-107">Azure AD uses this connection to enable the following user provisioning workflows:</span></span>

* <span data-ttu-id="16c76-108">**사용자를 Active Directory에 프로비전** - Workday에서 선택한 사용자 집합을 하나 이상의 Active Directory 포리스트와 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-108">**Provisioning users to Active Directory** - Synchronize selected sets of users from Workday into one or more Active Directory forests.</span></span> 

* <span data-ttu-id="16c76-109">**클라우드 전용 사용자를 Azure Active Directory에 프로비전** - Active Directory와 Azure Active Directory에 모두 있는 하이브리드 사용자는 [AAD Connect](connect/active-directory-aadconnect.md)를 사용하여 Azure Active Directory에 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-109">**Provisioning cloud-only users to Azure Active Directory** - Hybrid users who exist in both Active Directory and Azure Active Directory can be provisioned into the latter using [AAD Connect](connect/active-directory-aadconnect.md).</span></span> <span data-ttu-id="16c76-110">그러나 클라우드 전용 사용자는 Azure AD 사용자 프로비전 서비스를 사용하여 Workday에서 직접 Azure Active Directory에 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-110">However, users that are cloud-only can be provisioned directly from Workday to Azure Active Directory using the Azure AD user provisioning service.</span></span>

* <span data-ttu-id="16c76-111">**Workday에 이메일 주소 쓰기 저장** - Azure AD 사용자 프로비전 서비스는 선택한 Azure AD 사용자 특성(예: 이메일 주소)을 Workday에 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-111">**Writeback of email addresses to Workday** - the Azure AD user provisioning service can write selected Azure AD user attributes back to Workday, such as the email address.</span></span>

### <a name="scenarios-covered"></a><span data-ttu-id="16c76-112">포함되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="16c76-112">Scenarios covered</span></span>

<span data-ttu-id="16c76-113">Azure AD 사용자 프로비전 서비스에서 지원되는 Workday 사용자 프로비전 워크플로는 다음과 같은 인적 자원 및 ID 수명 주기 관리 시나리오의 자동화를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-113">The Workday user provisioning workflows supported by the Azure AD user provisioning service enables automation of the following human resources and identity lifecycle management scenarios:</span></span>

* <span data-ttu-id="16c76-114">**신규 직원 고용** - 신규 직원이 Workday에 추가되면 Active Directory, Azure Active Directory 그리고 선택적으로 Office 365 및 [Azure AD에서 지원하는 기타 SaaS 응용 프로그램](active-directory-saas-app-provisioning.md)에서 사용자 계정이 자동으로 생성되며, Workday에 이메일 주소를 다시 씁니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-114">**Hiring new employees** - When a new employee is added to Workday, a user account will be automatically created in Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](active-directory-saas-app-provisioning.md), with write back of the email address to Workday.</span></span>

* <span data-ttu-id="16c76-115">**직원 특성 및 프로필 업데이트** - Workday에서 이름, 직함, 관리자 등의 직원 레코드가 업데이트되면 Active Directory, Azure Active Directory 그리고 선택적으로 Office 365 및 [Azure AD에서 지원하는 기타 SaaS 응용 프로그램](active-directory-saas-app-provisioning.md)에서 해당 사용자 계정이 자동으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-115">**Employee attribute and profile updates** - When an employee record is updated in Workday (such as their name, title, or manager), their user account will be automatically updated in Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](active-directory-saas-app-provisioning.md).</span></span>

* <span data-ttu-id="16c76-116">**직원 퇴사** - Workday에서 직원이 퇴사하면 Active Directory, Azure Active Directory 그리고 선택적으로 Office 365 및 [Azure AD에서 지원하는 기타 SaaS 응용 프로그램](active-directory-saas-app-provisioning.md)에서 해당 사용자 계정이 자동으로 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-116">**Employee terminations** - When an employee is terminated in Workday, their user account is automatically disabled in Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](active-directory-saas-app-provisioning.md).</span></span>

* <span data-ttu-id="16c76-117">**직원 재고용** - Workday에서 직원이 다시 고용되면 Active Directory, Azure Active Directory 그리고 선택적으로 Office 365 및 [Azure AD에서 지원하는 기타 SaaS 응용 프로그램](active-directory-saas-app-provisioning.md)에서 해당 직원의 기존 계정이 자동으로 다시 활성화되거나 다시 프로비전됩니다(기본 설정에 따라).</span><span class="sxs-lookup"><span data-stu-id="16c76-117">**Employee re-hires** - When an employee is rehired in Workday, their old account can be automatically reactivated or re-provisioned (depending on your preference) to Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](active-directory-saas-app-provisioning.md).</span></span>


## <a name="planning-your-solution"></a><span data-ttu-id="16c76-118">솔루션 계획</span><span class="sxs-lookup"><span data-stu-id="16c76-118">Planning your solution</span></span>

<span data-ttu-id="16c76-119">Workday 통합을 시작하기 전에 다음과 같은 필수 조건을 확인하고, 현재 Active Directory 아키텍처 및 사용자 프로비전 요구 사항을 Azure Active Directory에서 제공하는 솔루션과 일치시키는 방법에 대한 지침을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="16c76-119">Before beginning your Workday integration, check the prerequisites below and read the following guidance on how to match your current Active Directory architecture and user provisioning requirements with the solution(s) provided by Azure Active Directory.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="16c76-120">필수 조건</span><span class="sxs-lookup"><span data-stu-id="16c76-120">Prerequisites</span></span>

<span data-ttu-id="16c76-121">이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-121">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="16c76-122">전역 관리자 액세스 권한이 있는 유효한 Azure AD Premium P1 구독</span><span class="sxs-lookup"><span data-stu-id="16c76-122">A valid Azure AD Premium P1 subscription with global administrator access</span></span>
* <span data-ttu-id="16c76-123">테스트 및 통합을 위한 Workday 구현 테넌트</span><span class="sxs-lookup"><span data-stu-id="16c76-123">A Workday implementation tenant for testing and integration purposes</span></span>
* <span data-ttu-id="16c76-124">테스트 목적으로 시스템 통합 사용자를 만들고 직원 데이터를 변경하기 위한 관리자 권한</span><span class="sxs-lookup"><span data-stu-id="16c76-124">Administrator permissions in Workday to create a system integration user, and make changes to test employee data for testing purposes</span></span>
* <span data-ttu-id="16c76-125">Active Directory에 사용자 프로비전의 경우 [온-프레미스 동기화 에이전트](https://go.microsoft.com/fwlink/?linkid=847801)를 호스트하려면 Windows Service 2012 이상을 실행하는 도메인에 가입된 서버가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-125">For user provisioning to Active Directory, a domain-joined server running Windows Service 2012 or greater is required to host the [on-premises synchronization agent](https://go.microsoft.com/fwlink/?linkid=847801)</span></span>
* <span data-ttu-id="16c76-126">Active Directory와 Azure AD 간의 동기화를 위한 [Azure AD Connect](connect/active-directory-aadconnect.md)</span><span class="sxs-lookup"><span data-stu-id="16c76-126">[Azure AD Connect](connect/active-directory-aadconnect.md) for synchronizing between Active Directory and Azure AD</span></span>

> [!NOTE]
> <span data-ttu-id="16c76-127">Azure AD 테넌트가 유럽에 있는 경우 아래의 [알려진 문제](#known-issues) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16c76-127">If your Azure AD tenant is located in Europe, please see the [Known issues](#known-issues) section below.</span></span>


### <a name="solution-architecture"></a><span data-ttu-id="16c76-128">솔루션 아키텍처</span><span class="sxs-lookup"><span data-stu-id="16c76-128">Solution architecture</span></span>

<span data-ttu-id="16c76-129">Azure AD는 Workday에서 Active Directory, Azure AD, SaaS 앱 등으로 프로비전하고 ID 수명 주기 관리 문제를 해결할 수 있는 다양한 프로비전 커넥터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-129">Azure AD provides a rich set of provisioning connectors to help you solve provisioning and identity lifecycle management from Workday to Active Directory, Azure AD, SaaS apps, and beyond.</span></span> <span data-ttu-id="16c76-130">사용하게 될 기능과 솔루션 설정 방법은 조직의 환경과 요구 사항에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-130">Which features you will use and how you set up the solution will vary depending on your organization's environment and requirements.</span></span> <span data-ttu-id="16c76-131">첫 번째 단계로 조직에서 다음 항목 중 몇 개를 갖고 있으며 몇 개가 배포되었는지 점검합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-131">As a first step, take stock of how many of the following are present and deployed in your organization:</span></span>

* <span data-ttu-id="16c76-132">Active Directory 포리스트를 몇 개나 사용하고 있나요?</span><span class="sxs-lookup"><span data-stu-id="16c76-132">How many Active Directory Forests are in use?</span></span>
* <span data-ttu-id="16c76-133">Active Directory 도메인을 몇 개나 사용하고 있나요?</span><span class="sxs-lookup"><span data-stu-id="16c76-133">How many Active Directory Domains are in use?</span></span>
* <span data-ttu-id="16c76-134">Active Directory OU(조직 구성 단위)를 몇 개나 사용하고 있나요?</span><span class="sxs-lookup"><span data-stu-id="16c76-134">How many Active Directory Organizational Units (OUs) are in use?</span></span>
* <span data-ttu-id="16c76-135">Azure Active Directory 테넌트를 몇 개나 사용하고 있나요?</span><span class="sxs-lookup"><span data-stu-id="16c76-135">How many Azure Active Directory tenants are in use?</span></span>
* <span data-ttu-id="16c76-136">Active Directory와 Azure Active Directory에 모두 프로비전해야 하는 사용자(예: "하이브리드" 사용자)가 있나요?</span><span class="sxs-lookup"><span data-stu-id="16c76-136">Are there users who need to be provisioned to both Active Directory and Azure Active Directory (e.g. "hybrid" users)?</span></span>
* <span data-ttu-id="16c76-137">Azure Active Directory에만 프로비전하고 Active Directory에는 프로비전하면 안 되는 사용자(예: "클라우드 전용" 사용자)가 있나요?</span><span class="sxs-lookup"><span data-stu-id="16c76-137">Are there users who need to be provisioned to Azure Active Directory, but not Active Directory (e.g. "cloud-only" users)?</span></span>
* <span data-ttu-id="16c76-138">사용자 이메일 주소를 Workday에 다시 써야 하나요?</span><span class="sxs-lookup"><span data-stu-id="16c76-138">Do user email addresses need to be written back to Workday?</span></span>

<span data-ttu-id="16c76-139">이러한 질문에 대답한 후에는 아래 지침에 따라 Workday 프로비전 배포를 계획할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-139">Once you have answers to these questions, you can plan your Workday provisioning deployment by following the guidance below.</span></span>

#### <a name="using-provisioning-connector-apps"></a><span data-ttu-id="16c76-140">프로비전 커넥터 앱 사용</span><span class="sxs-lookup"><span data-stu-id="16c76-140">Using provisioning connector apps</span></span>

<span data-ttu-id="16c76-141">Azure Active Directory는 Workday용으로 사전 통합된 프로비전 커넥터와 수많은 기타 SaaS 응용 프로그램을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-141">Azure Active Directory supports pre-integrated provisioning connectors for Workday and a large number of other SaaS applications.</span></span> 

<span data-ttu-id="16c76-142">단일 프로비전 커넥터가 단일 원본 시스템의 API와 상호 작용하고, 단일 대상 시스템에 데이터를 프로비전하도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-142">A single provisioning connector interfaces with the API of a single source system, and helps provision data to a single target system.</span></span> <span data-ttu-id="16c76-143">Azure AD에서 지원하는 대부분의 프로비전 커넥터는 단일 원본 및 대상 시스템용이며(예: Azure AD에서 ServiceNow로), 간단하게 Azure AD 앱 갤러리에서 문제의 앱(예: ServiceNow)을 추가하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-143">Most provisioning connectors that Azure AD supports are for a single source and target system (e.g. Azure AD to ServiceNow), and can be setup by simply adding the app in question from the Azure AD app gallery (e.g. ServiceNow).</span></span> 

<span data-ttu-id="16c76-144">Azure AD의 프로비전 커넥터 인스턴스와 앱 인스턴스는 일대일 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-144">There is a one-to-one relationship between provisioning connector instances and app instances in Azure AD:</span></span>

| <span data-ttu-id="16c76-145">원본 시스템</span><span class="sxs-lookup"><span data-stu-id="16c76-145">Source System</span></span> | <span data-ttu-id="16c76-146">대상 시스템</span><span class="sxs-lookup"><span data-stu-id="16c76-146">Target System</span></span> |
| ---------- | ---------- | 
| <span data-ttu-id="16c76-147">Azure AD 테넌트</span><span class="sxs-lookup"><span data-stu-id="16c76-147">Azure AD tenant</span></span> | <span data-ttu-id="16c76-148">SaaS 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="16c76-148">SaaS application</span></span> |


<span data-ttu-id="16c76-149">그러나 Workday 및 Active Directory를 사용할 때 여러 원본 및 대상 시스템을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-149">However, when working with Workday and Active Directory, there are multiple source and target systems to be considered:</span></span>

| <span data-ttu-id="16c76-150">원본 시스템</span><span class="sxs-lookup"><span data-stu-id="16c76-150">Source System</span></span> | <span data-ttu-id="16c76-151">대상 시스템</span><span class="sxs-lookup"><span data-stu-id="16c76-151">Target System</span></span> | <span data-ttu-id="16c76-152">참고 사항</span><span class="sxs-lookup"><span data-stu-id="16c76-152">Notes</span></span> |
| ---------- | ---------- | ---------- |
| <span data-ttu-id="16c76-153">Workday</span><span class="sxs-lookup"><span data-stu-id="16c76-153">Workday</span></span> | <span data-ttu-id="16c76-154">Active Directory 포리스트</span><span class="sxs-lookup"><span data-stu-id="16c76-154">Active Directory Forest</span></span> | <span data-ttu-id="16c76-155">각 포리스트는 고유한 대상 시스템으로 처리됨</span><span class="sxs-lookup"><span data-stu-id="16c76-155">Each forest is treated as a distinct target system</span></span> |
| <span data-ttu-id="16c76-156">Workday</span><span class="sxs-lookup"><span data-stu-id="16c76-156">Workday</span></span> | <span data-ttu-id="16c76-157">Azure AD 테넌트</span><span class="sxs-lookup"><span data-stu-id="16c76-157">Azure AD tenant</span></span> | <span data-ttu-id="16c76-158">클라우드 전용 사용자에 필요한 경우</span><span class="sxs-lookup"><span data-stu-id="16c76-158">As required for cloud-only users</span></span> |
| <span data-ttu-id="16c76-159">Active Directory 포리스트</span><span class="sxs-lookup"><span data-stu-id="16c76-159">Active Directory Forest</span></span> | <span data-ttu-id="16c76-160">Azure AD 테넌트</span><span class="sxs-lookup"><span data-stu-id="16c76-160">Azure AD tenant</span></span> | <span data-ttu-id="16c76-161">이 흐름은 현재 AAD Connect에서 처리</span><span class="sxs-lookup"><span data-stu-id="16c76-161">This flow is handled by AAD Connect today</span></span> |
| <span data-ttu-id="16c76-162">Azure AD 테넌트</span><span class="sxs-lookup"><span data-stu-id="16c76-162">Azure AD tenant</span></span> | <span data-ttu-id="16c76-163">Workday</span><span class="sxs-lookup"><span data-stu-id="16c76-163">Workday</span></span> | <span data-ttu-id="16c76-164">이메일 주소의 쓰기 저장</span><span class="sxs-lookup"><span data-stu-id="16c76-164">For writeback of email addresses</span></span> |

<span data-ttu-id="16c76-165">이러한 여러 워크플로를 여러 원본 및 대상 시스템에 사용할 수 있도록 Azure AD는 Azure AD 앱 갤러리에서 추가할 수 있는 여러 프로비전 커넥터 앱을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-165">To facilitate these multiple workflows to multiple source and target systems, Azure AD provides multiple provisioning connector apps that you can add from the Azure AD app gallery:</span></span>

![AAD 앱 갤러리](./media/active-directory-saas-workday-inbound-tutorial/WD_Gallery.PNG)

* <span data-ttu-id="16c76-167">**Workday에서 Active Directory로 프로비전** - 이 앱은 Workday에서 단일 Active Directory 포리스트로 사용자 계정 프로비전을 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-167">**Workday to Active Directory Provisioning** - This app facilitates user account provisioning from Workday to a single Active Directory forest.</span></span> <span data-ttu-id="16c76-168">포리스트가 여러 개 있는 경우 프로비전해야 하는 각 Active Directory 포리스트에 대해 Azure AD 앱 갤러리에서 이 앱의 하나의 인스턴스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-168">If you have multiple forests, you can add one instance of this app from the Azure AD app gallery for each Active Directory forest you need to provision to.</span></span>

* <span data-ttu-id="16c76-169">**Workday에서 Azure AD로 프로비전** - AAD Connect는 Active Directory 사용자를 Azure Active Directory와 동기화하는 데 사용되는 도구이지만, 이 앱을 사용하여 Workday에서 단일 Azure Active Directory 테넌트로 클라우드 전용 사용자를 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-169">**Workday to Azure AD Provisioning** - While AAD Connect is the tool that should be used to synchronize Active Directory users to Azure Active Directory, this app can be used to facilitate provisioning of cloud-only users from Workday to a single Azure Active Directory tenant.</span></span>

* <span data-ttu-id="16c76-170">**Workday 쓰기 저장** - 이 앱은 사용자 이메일 주소를 Azure Active Directory에서 Workday로 쓰기 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-170">**Workday Writeback** - This app facilitates writeback of user's email addresses from Azure Active Directory to Workday.</span></span>

> [!TIP]
> <span data-ttu-id="16c76-171">일반 "Workday" 앱은 Workday와 Azure Active Directory 간의 Single Sign-On을 설정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-171">The regular "Workday" app is used for setting up single sign-on between Workday and Azure Active Directory.</span></span> 

<span data-ttu-id="16c76-172">이러한 특수 프로비전 커넥터 앱을 설정하고 구성하는 방법은 본 자습서의 나머지 섹션에서 다루겠습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-172">How to set up and configure these special provisioning connector apps is the subject of the remaining sections of this tutorial.</span></span> <span data-ttu-id="16c76-173">구성을 위해 선택할 앱은 프로비전해야 하는 시스템, 환경에 있는 Active Directory 포리스트 및 Azure AD 테넌트 수에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-173">Which apps you choose to configure will depend on which systems you need to provision to, and how many Active Directory Forests and Azure AD tenants are in your environment.</span></span>

![개요](./media/active-directory-saas-workday-inbound-tutorial/WD_Overview.PNG)

## <a name="configure-a-system-integration-user-in-workday"></a><span data-ttu-id="16c76-175">Workday에서 시스템 통합 사용자 구성</span><span class="sxs-lookup"><span data-stu-id="16c76-175">Configure a system integration user in Workday</span></span>
<span data-ttu-id="16c76-176">모든 Workday 프로비전 커넥터의 일반적인 요구 사항으로, Workday 시스템 통합 계정이 Workday 인적 자원 API에 연결하는 데 사용할 할 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-176">A common requirement of all the Workday provisioning connectors is they require credentials for a Workday system integration account to connect to the Workday Human Resources API.</span></span> <span data-ttu-id="16c76-177">이 섹션에서는 Workday에서 시스템 통합자 계정을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-177">This section describes how to create a system integrator account in Workday.</span></span>

> [!NOTE]
> <span data-ttu-id="16c76-178">이 절차를 건너뛰고 Workday 전역 Administrator 계정을 시스템 통합 계정으로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-178">It is possible to bypass this procedure and instead use a Workday global administrator account as the system integration account.</span></span> <span data-ttu-id="16c76-179">이 방법이 데모에서는 제대로 작동할 수 있지만 프로덕션 배포에는 권장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-179">This may work fine for demos, but is not recommended for production deployments.</span></span>

### <a name="create-an-integration-system-user"></a><span data-ttu-id="16c76-180">통합 시스템 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="16c76-180">Create an integration system user</span></span>

<span data-ttu-id="16c76-181">**통합 시스템 사용자를 만들려면**</span><span class="sxs-lookup"><span data-stu-id="16c76-181">**To create an integration system user:**</span></span>

1. <span data-ttu-id="16c76-182">Administrator 계정을 사용하여 Workday 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-182">Sign into your Workday tenant using an administrator account.</span></span> <span data-ttu-id="16c76-183">**Workday Workbench**의 검색 상자에서 사용자 만들기를 입력하고 **통합 시스템 사용자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-183">In the **Workday Workbench**, enter create user in the search box, and then click **Create Integration System User**.</span></span> 
   
    <span data-ttu-id="16c76-184">![사용자 만들기](./media/active-directory-saas-workday-inbound-tutorial/IC750979.png "사용자 만들기")</span><span class="sxs-lookup"><span data-stu-id="16c76-184">![Create user](./media/active-directory-saas-workday-inbound-tutorial/IC750979.png "Create user")</span></span>
2. <span data-ttu-id="16c76-185">새 통합 시스템 사용자에 대한 사용자 이름과 암호를 입력하여 **통합 시스템 사용자 만들기** 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-185">Complete the **Create Integration System User** task by supplying a user name and password for a new Integration System User.</span></span>  
 * <span data-ttu-id="16c76-186">이 사용자는 프로그래밍 방식으로 로그인할 것이므로 **다음 로그인할 때 새 암호 필요** 옵션을 선택하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-186">Leave the **Require New Password at Next Sign In** option unchecked, because this user will be logging on programmatically.</span></span> 
 * <span data-ttu-id="16c76-187">사용자의 세션이 너무 빨리 시간 초과되지 않도록 **세션 시간 초과 분**을 기본값인 0으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-187">Leave the **Session Timeout Minutes** with its default value of 0, which will prevent the user’s sessions from timing out prematurely.</span></span> 
   
    <span data-ttu-id="16c76-188">![통합 시스템 사용자 만들기](./media/active-directory-saas-workday-inbound-tutorial/IC750980.png "통합 시스템 사용자 만들기")</span><span class="sxs-lookup"><span data-stu-id="16c76-188">![Create Integration System User](./media/active-directory-saas-workday-inbound-tutorial/IC750980.png "Create Integration System User")</span></span>

### <a name="create-a-security-group"></a><span data-ttu-id="16c76-189">보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="16c76-189">Create a security group</span></span>
<span data-ttu-id="16c76-190">무제한 통합 시스템 보안 그룹을 만들고 사용자를 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-190">You need to create an unconstrained integration system security group and assign the user to it.</span></span>

<span data-ttu-id="16c76-191">**보안 그룹을 만들려면**</span><span class="sxs-lookup"><span data-stu-id="16c76-191">**To create a security group:**</span></span>

1. <span data-ttu-id="16c76-192">검색 상자에 보안 그룹 만들기를 입력하고 **보안 그룹 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-192">Enter create security group in the search box, and then click **Create Security Group**.</span></span> 
   
    <span data-ttu-id="16c76-193">![보안 그룹 만들기](./media/active-directory-saas-workday-inbound-tutorial/IC750981.png "보안 그룹 만들기")</span><span class="sxs-lookup"><span data-stu-id="16c76-193">![CreateSecurity Group](./media/active-directory-saas-workday-inbound-tutorial/IC750981.png "CreateSecurity Group")</span></span>
2. <span data-ttu-id="16c76-194">**보안 그룹 만들기** 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-194">Complete the **Create Security Group** task.</span></span>  
3. <span data-ttu-id="16c76-195">**테넌트 보안 그룹의 유형**에서 통합 시스템 보안 그룹 - 제한되지 않음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-195">Select Integration System Security Group—Unconstrained from the **Type of Tenanted Security Group** dropdown.</span></span>
4. <span data-ttu-id="16c76-196">구성원이 명시적으로 추가될 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-196">Create a security group to which members will be explicitly added.</span></span> 
   
    <span data-ttu-id="16c76-197">![보안 그룹 만들기](./media/active-directory-saas-workday-inbound-tutorial/IC750982.png "보안 그룹 만들기")</span><span class="sxs-lookup"><span data-stu-id="16c76-197">![CreateSecurity Group](./media/active-directory-saas-workday-inbound-tutorial/IC750982.png "CreateSecurity Group")</span></span>

### <a name="assign-the-integration-system-user-to-the-security-group"></a><span data-ttu-id="16c76-198">보안 그룹에 통합 시스템 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="16c76-198">Assign the integration system user to the security group</span></span>

<span data-ttu-id="16c76-199">**통합 시스템 사용자를 할당하려면**</span><span class="sxs-lookup"><span data-stu-id="16c76-199">**To assign the integration system user:**</span></span>

1. <span data-ttu-id="16c76-200">검색 상자에 보안 그룹 편집을 입력하고 **보안 그룹 편집**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-200">Enter edit security group in the search box, and then click **Edit Security Group**.</span></span> 
   
    <span data-ttu-id="16c76-201">![보안 그룹 편집](./media/active-directory-saas-workday-inbound-tutorial/IC750983.png "보안 그룹 편집")</span><span class="sxs-lookup"><span data-stu-id="16c76-201">![Edit Security Group](./media/active-directory-saas-workday-inbound-tutorial/IC750983.png "Edit Security Group")</span></span>
2. <span data-ttu-id="16c76-202">이름으로 새 통합 보안 그룹을 검색하고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-202">Search for, and select the new integration security group by name.</span></span> 
   
    <span data-ttu-id="16c76-203">![보안 그룹 편집](./media/active-directory-saas-workday-inbound-tutorial/IC750984.png "보안 그룹 편집")</span><span class="sxs-lookup"><span data-stu-id="16c76-203">![Edit Security Group](./media/active-directory-saas-workday-inbound-tutorial/IC750984.png "Edit Security Group")</span></span>
3. <span data-ttu-id="16c76-204">새 보안 그룹에 새 통합 시스템 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="16c76-204">Add the new integration system user to the new security group.</span></span> 
   
    <span data-ttu-id="16c76-205">![시스템 보안 그룹](./media/active-directory-saas-workday-inbound-tutorial/IC750985.png "시스템 보안 그룹")</span><span class="sxs-lookup"><span data-stu-id="16c76-205">![System Security Group](./media/active-directory-saas-workday-inbound-tutorial/IC750985.png "System Security Group")</span></span>  

### <a name="configure-security-group-options"></a><span data-ttu-id="16c76-206">보안 그룹 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="16c76-206">Configure security group options</span></span>
<span data-ttu-id="16c76-207">이 단계에서는 다음 도메인 보안 정책에 의해 보호되는 개체에 대한 **Get** 및 **Put** 작업을 위해 새 보안 그룹 사용 권한을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-207">In this step, you grant to the new security group permissions for **Get** and **Put** operations on the objects secured by the following domain security policies:</span></span>

* <span data-ttu-id="16c76-208">외부 계정 프로비저닝</span><span class="sxs-lookup"><span data-stu-id="16c76-208">External Account Provisioning</span></span>
* <span data-ttu-id="16c76-209">작업자 데이터: 공용 작업자 보고서</span><span class="sxs-lookup"><span data-stu-id="16c76-209">Worker Data: Public Worker Reports</span></span>
* <span data-ttu-id="16c76-210">작업자 데이터: 모든 위치</span><span class="sxs-lookup"><span data-stu-id="16c76-210">Worker Data: All Positions</span></span>
* <span data-ttu-id="16c76-211">작업자 데이터: 현재 인력 관리 정보</span><span class="sxs-lookup"><span data-stu-id="16c76-211">Worker Data: Current Staffing Information</span></span>
* <span data-ttu-id="16c76-212">작업자 데이터: 작업자 프로필 직함</span><span class="sxs-lookup"><span data-stu-id="16c76-212">Worker Data: Business Title on Worker Profile</span></span>

<span data-ttu-id="16c76-213">**보안 그룹 옵션을 구성하려면**</span><span class="sxs-lookup"><span data-stu-id="16c76-213">**To configure security group options:**</span></span>

1. <span data-ttu-id="16c76-214">검색 상자에 도메인 보안 정책을 입력하고 **기능 영역에 대한 보안 정책** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-214">Enter domain security policies in the search box, and then click on the link **Domain Security Policies for Functional Area**.</span></span>  
   
    <span data-ttu-id="16c76-215">![도메인 보안 정책](./media/active-directory-saas-workday-inbound-tutorial/IC750986.png "도메인 보안 정책")</span><span class="sxs-lookup"><span data-stu-id="16c76-215">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750986.png "Domain Security Policies")</span></span>  
2. <span data-ttu-id="16c76-216">시스템을 검색하여 **시스템** 기능 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-216">Search for system and select the **System** functional area.</span></span>  <span data-ttu-id="16c76-217">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-217">Click **OK**.</span></span>  
   
    <span data-ttu-id="16c76-218">![도메인 보안 정책](./media/active-directory-saas-workday-inbound-tutorial/IC750987.png "도메인 보안 정책")</span><span class="sxs-lookup"><span data-stu-id="16c76-218">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750987.png "Domain Security Policies")</span></span>  
3. <span data-ttu-id="16c76-219">시스템 기능 영역에 대한 보안 정책 목록에서 **보안 관리**를 확장하고, 도메인 보안 정책 **외부 계정 프로비저닝**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-219">In the list of security policies for the System functional area, expand **Security Administration** and select the domain security policy **External Account Provisioning**.</span></span>  
   
    <span data-ttu-id="16c76-220">![도메인 보안 정책](./media/active-directory-saas-workday-inbound-tutorial/IC750988.png "도메인 보안 정책")</span><span class="sxs-lookup"><span data-stu-id="16c76-220">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750988.png "Domain Security Policies")</span></span>  
4. <span data-ttu-id="16c76-221">**사용 권한 편집**을 클릭한 다음, **사용 권한 편집** 대화 상자 페이지에서 **Get** 및 **Put** 통합 사용 권한이 있는 보안 그룹의 목록에 새 보안 그룹을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-221">Click **Edit Permissions**, and then, on the **Edit Permissions**dialog page, add the new security group to the list of security groups with **Get** and **Put** integration permissions.</span></span> 
   
    <span data-ttu-id="16c76-222">![사용 권한 편집](./media/active-directory-saas-workday-inbound-tutorial/IC750989.png "사용 권한 편집")</span><span class="sxs-lookup"><span data-stu-id="16c76-222">![Edit Permission](./media/active-directory-saas-workday-inbound-tutorial/IC750989.png "Edit Permission")</span></span>  
5. <span data-ttu-id="16c76-223">1단계를 반복하여 기능 영역을 선택하는 화면으로 돌아간 다음, 이번에는 인력 관리를 검색하고 **인력 관리 기능 영역**을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-223">Repeat step 1 above to return to the screen for selecting functional areas, and this time, search for staffing, select the **Staffing functional area** and click **OK**.</span></span>
   
    <span data-ttu-id="16c76-224">![도메인 보안 정책](./media/active-directory-saas-workday-inbound-tutorial/IC750990.png "도메인 보안 정책")</span><span class="sxs-lookup"><span data-stu-id="16c76-224">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750990.png "Domain Security Policies")</span></span>  
6. <span data-ttu-id="16c76-225">인력 관리 영역에 대한 보안 정책 목록에서 **작업자 데이터: 인력 관리**를 확장하고 다음과 같은 남은 각 보안 정책에 대해 위의 4단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-225">In the list of security policies for the Staffing functional area, expand **Worker Data: Staffing** and repeat step 4 above for each of these remaining security policies:</span></span>

   * <span data-ttu-id="16c76-226">작업자 데이터: 공용 작업자 보고서</span><span class="sxs-lookup"><span data-stu-id="16c76-226">Worker Data: Public Worker Reports</span></span>
   * <span data-ttu-id="16c76-227">작업자 데이터: 모든 위치</span><span class="sxs-lookup"><span data-stu-id="16c76-227">Worker Data: All Positions</span></span>
   * <span data-ttu-id="16c76-228">작업자 데이터: 현재 인력 관리 정보</span><span class="sxs-lookup"><span data-stu-id="16c76-228">Worker Data: Current Staffing Information</span></span>
   * <span data-ttu-id="16c76-229">작업자 데이터: 작업자 프로필 직함</span><span class="sxs-lookup"><span data-stu-id="16c76-229">Worker Data: Business Title on Worker Profile</span></span>
   
7. <span data-ttu-id="16c76-230">위의 1단계를 반복하여 기능 영역을 선택하는 화면으로 돌아간 다음, 이번에는 **연락처 정보**를 검색하고 인력 관리 기능 영역을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-230">Repeat step 1, above, to return to the screen for selecting  functional areas, and this time, search for **Contact Information**,  select the Staffing functional area, and click **OK**.</span></span>

8.  <span data-ttu-id="16c76-231">인력 관리 기능 영역에 대한 보안 정책 목록에서 **작업자 데이터: 작업자 연락처 정보**를 확장하고 아래 보안 정책에 대해 위의 4단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-231">In the list of security policies for the Staffing functional area, expand **Worker Data: Work Contact Information**, and repeat step 4 above for the security policies below:</span></span>

    * <span data-ttu-id="16c76-232">작업자 데이터: 업무용 메일</span><span class="sxs-lookup"><span data-stu-id="16c76-232">Worker Data: Work Email</span></span>

    <span data-ttu-id="16c76-233">![도메인 보안 정책](./media/active-directory-saas-workday-inbound-tutorial/IC750991.png "도메인 보안 정책")</span><span class="sxs-lookup"><span data-stu-id="16c76-233">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750991.png "Domain Security Policies")</span></span>  
    
### <a name="activate-security-policy-changes"></a><span data-ttu-id="16c76-234">보안 정책 변경 사항 활성화</span><span class="sxs-lookup"><span data-stu-id="16c76-234">Activate security policy changes</span></span>

<span data-ttu-id="16c76-235">**보안 정책 변경 사항을 활성화하려면**</span><span class="sxs-lookup"><span data-stu-id="16c76-235">**To activate security policy changes:**</span></span>

1. <span data-ttu-id="16c76-236">검색 상자에 활성화를 입력하고 **보류 중인 보안 정책 변경 내용 활성화** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-236">Enter activate in the search box, and then click on the link **Activate Pending Security Policy Changes**.</span></span> 
   
    <span data-ttu-id="16c76-237">![활성화](./media/active-directory-saas-workday-inbound-tutorial/IC750992.png "활성화")</span><span class="sxs-lookup"><span data-stu-id="16c76-237">![Activate](./media/active-directory-saas-workday-inbound-tutorial/IC750992.png "Activate")</span></span> 
2. <span data-ttu-id="16c76-238">감사 목적에 대한 메모를 입력하고 **확인**을 클릭하여 보류 중인 보안 정책 변경 내용의 활성화 태스크를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-238">Begin the Activate Pending Security Policy Changes task by entering a comment for auditing purposes, and then click **OK**.</span></span> 
   
    <span data-ttu-id="16c76-239">![보류 중인 보안 활성화](./media/active-directory-saas-workday-inbound-tutorial/IC750993.png "보류 중인 보안 활성화")</span><span class="sxs-lookup"><span data-stu-id="16c76-239">![Activate Pending Security](./media/active-directory-saas-workday-inbound-tutorial/IC750993.png "Activate Pending Security")</span></span>   
3. <span data-ttu-id="16c76-240">다음 화면에서 **확인** 확인란을 선택하여 태스크를 완료한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-240">Complete the task on the next screen by checking the checkbox **Confirm**, and then click **OK**.</span></span> 
   
    <span data-ttu-id="16c76-241">![보류 중인 보안 활성화](./media/active-directory-saas-workday-inbound-tutorial/IC750994.png "보류 중인 보안 활성화")</span><span class="sxs-lookup"><span data-stu-id="16c76-241">![Activate Pending Security](./media/active-directory-saas-workday-inbound-tutorial/IC750994.png "Activate Pending Security")</span></span>  

## <a name="configuring-user-provisioning-from-workday-to-active-directory"></a><span data-ttu-id="16c76-242">Workday에서 Active Directory로 사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="16c76-242">Configuring user provisioning from Workday to Active Directory</span></span>
<span data-ttu-id="16c76-243">다음 지침에 따라 Workday에서 프로비전이 필요한 각 Active Directory 포리스트로 사용자 계정 프로비전을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-243">Follow these instructions to configure user account provisioning from Workday to each Active Directory forest that you require provisioning to.</span></span>

### <a name="part-1-adding-the-provisioning-connector-app-and-creating-the-connection-to-workday"></a><span data-ttu-id="16c76-244">1부: 프로비전 커넥터 앱을 추가하고 Workday에 대한 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="16c76-244">Part 1: Adding the provisioning connector app and creating the connection to Workday</span></span>

<span data-ttu-id="16c76-245">**Workday에서 Active Directory로의 프로비전을 구성하려면:**</span><span class="sxs-lookup"><span data-stu-id="16c76-245">**To configure Workday to Active Directory provisioning:**</span></span>

1.  <span data-ttu-id="16c76-246"><https://portal.azure.com>으로 이동</span><span class="sxs-lookup"><span data-stu-id="16c76-246">Go to <https://portal.azure.com></span></span>

2.  <span data-ttu-id="16c76-247">왼쪽 탐색 모음에서 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-247">In the left navigation bar, select **Azure Active Directory**</span></span>

3.  <span data-ttu-id="16c76-248">**엔터프라이즈 응용 프로그램**, **모든 응용 프로그램**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-248">Select **Enterprise Applications**, then **All Applications**.</span></span>

4.  <span data-ttu-id="16c76-249">**응용 프로그램 추가**를 선택하고 **모두** 범주를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-249">Select **Add an application**, and select the **All** category.</span></span>

5.  <span data-ttu-id="16c76-250">**Active Directory에 Workday 프로비전**을 검색하고, 갤러리에서 해당 앱을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-250">Search for **Workday Provisioning to Active Directory**, and add that app from the gallery.</span></span>

6.  <span data-ttu-id="16c76-251">앱이 추가되고 앱 세부 정보 화면이 표시되면 **프로비전**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-251">After the app is added and the app details screen is shown, select **Provisioning**</span></span>

7.  <span data-ttu-id="16c76-252">**프로비전** **모드**를 **자동**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-252">Change the **Provisioning** **Mode** to **Automatic**</span></span>

8.  <span data-ttu-id="16c76-253">다음과 같이 **관리자 자격 증명** 섹션을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-253">Complete the **Admin Credentials** section as follows:</span></span>

   * <span data-ttu-id="16c76-254">**관리 사용자 이름** – 테넌트 도메인 이름이 추가된 Workday 통합 시스템 계정의 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-254">**Admin Username** – Enter the username of the Workday integration system account, with the tenant domain name appended.</span></span> <span data-ttu-id="16c76-255">**다음과 같은 형태여야 합니다. username@contoso4**</span><span class="sxs-lookup"><span data-stu-id="16c76-255">**Should look something like: username@contoso4**</span></span>

   * <span data-ttu-id="16c76-256">**관리자 암호 –** Workday 통합 시스템 계정의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-256">**Admin password –** Enter the password of the Workday    integration system account</span></span>

   * <span data-ttu-id="16c76-257">**테넌트 URL –** 해당 테넌트의 Workday 웹 서비스 끝점에 대한 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-257">**Tenant URL –** Enter the URL to the Workday web services endpoint for your tenant.</span></span> <span data-ttu-id="16c76-258">https://wd3-impl-services1.workday.com/ccx/service/contoso4와 같은 형태여야 하며, 여기서 contoso4를 올바른 테넌트 이름으로 바꾸고 wd3-impl을 올바른 환경 문자열로 바꾸면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-258">This should look like: https://wd3-impl-services1.workday.com/ccx/service/contoso4, where contoso4 is replaced with your correct tenant name and wd3-impl is replaced with the correct environment string.</span></span>

   * <span data-ttu-id="16c76-259">**Active Directory 포리스트 -** Get-ADForest powershell 명령에서 반환하는 Active Directory 포리스트의 "이름"입니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-259">**Active Directory Forest -** The “Name” of your Active Directory forest, as returned by the Get-ADForest powershell commandlet.</span></span> <span data-ttu-id="16c76-260">일반적으로 *contoso.com* 형태의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-260">This is typically a string like: *contoso.com*</span></span>

   * <span data-ttu-id="16c76-261">**Active Directory 컨테이너 -** AD 포리스트의 모든 사용자를 포함하는 컨테이너 문자열을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-261">**Active Directory Container -** Enter the container string that contains all users in your AD forest.</span></span> <span data-ttu-id="16c76-262">예: *OU=Standard Users,OU=Users,DC=contoso,DC=test*</span><span class="sxs-lookup"><span data-stu-id="16c76-262">Example: *OU=Standard Users,OU=Users,DC=contoso,DC=test*</span></span>

   * <span data-ttu-id="16c76-263">**알림 이메일 –** 이메일 주소를 입력하고 "오류가 발생하면 이메일 보내기" 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-263">**Notification Email –** Enter your email address, and check the    “send email if failure occurs” checkbox.</span></span>

   * <span data-ttu-id="16c76-264">**연결 테스트** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-264">Click the **Test Connection** button.</span></span> <span data-ttu-id="16c76-265">연결 테스트가 성공하면 맨 위에서 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-265">If the connection test succeeds, click the **Save** button at the top.</span></span> <span data-ttu-id="16c76-266">연결 테스트가 실패하면 Workday에서 Workday 자격 증명이 유효한지 다시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-266">If it fails, double-check that the Workday credentials are valid in Workday.</span></span> 

![Azure 포털](./media/active-directory-saas-workday-inbound-tutorial/WD_1.PNG)

### <a name="part-2-configure-attribute-mappings"></a><span data-ttu-id="16c76-268">2부: 특성 매핑 구성</span><span class="sxs-lookup"><span data-stu-id="16c76-268">Part 2: Configure attribute mappings</span></span> 

<span data-ttu-id="16c76-269">이 섹션에서는 사용자 데이터가 Workday에서 Active Directory로 흐르는 방식을 구성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-269">In this section, you will configure how user data flows from Workday to Active Directory.</span></span>

1.  <span data-ttu-id="16c76-270">**매핑** 아래의 프로비전 탭에서 **Workday 작업자를 온-프레미스와 동기화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-270">On the Provisioning tab under **Mappings**, click **Synchronize Workday Workers to OnPremises**.</span></span>

2.  <span data-ttu-id="16c76-271">**원본 개체 범위** 필드에서 특성 기반 필터 집합을 정의하여 AD 프로비전 범위에 포함할 Workday 사용자 집합을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-271">In the **Source Object Scope** field, you can select which sets of users in Workday should be in scope for provisioning to AD, by defining a set of attribute-based filters.</span></span> <span data-ttu-id="16c76-272">기본 범위는 "Workday의 모든 사용자"입니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-272">The default scope is “all users in Workday”.</span></span> <span data-ttu-id="16c76-273">예제 필터:</span><span class="sxs-lookup"><span data-stu-id="16c76-273">Example filters:</span></span>

   * <span data-ttu-id="16c76-274">예: 작업자 ID가 1000000-2000000 사이인 사용자를 범위에 포함</span><span class="sxs-lookup"><span data-stu-id="16c76-274">Example: Scope to users with Worker IDs between 1000000 and    2000000</span></span>

      * <span data-ttu-id="16c76-275">특성: WorkerID</span><span class="sxs-lookup"><span data-stu-id="16c76-275">Attribute: WorkerID</span></span>

      * <span data-ttu-id="16c76-276">연산자: REGEX Match</span><span class="sxs-lookup"><span data-stu-id="16c76-276">Operator: REGEX Match</span></span>

      * <span data-ttu-id="16c76-277">값: (1[0-9][0-9][0-9][0-9][0-9][0-9])</span><span class="sxs-lookup"><span data-stu-id="16c76-277">Value: (1[0-9][0-9][0-9][0-9][0-9][0-9])</span></span>

   * <span data-ttu-id="16c76-278">예: 정규직 직원만 포함하고 비정규직 직원은 포함하지 않음</span><span class="sxs-lookup"><span data-stu-id="16c76-278">Example: Only employees and not contingent workers</span></span> 

      * <span data-ttu-id="16c76-279">특성: EmployeeID</span><span class="sxs-lookup"><span data-stu-id="16c76-279">Attribute: EmployeeID</span></span>

      * <span data-ttu-id="16c76-280">연산자: IS NOT NULL</span><span class="sxs-lookup"><span data-stu-id="16c76-280">Operator: IS NOT NULL</span></span>

3.  <span data-ttu-id="16c76-281">**대상 개체 작업** 필드에서 어떤 작업을 Active Directory에서 수행할 수 있도록 허용할 것인지 전역적으로 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-281">In the **Target Object Actions** field, you can globally filter what actions are allowed to be performed on Active Directory.</span></span> <span data-ttu-id="16c76-282">**만들기** 및 **업데이트**가 가장 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-282">**Create** and **Update** are most common.</span></span>

4.  <span data-ttu-id="16c76-283">**특성 매핑** 섹션에서 개별 Workday 특성이 Active Directory 특성에 매핑되는 방식을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-283">In the **Attribute mappings** section, you can define how individual Workday attributes map to Active Directory attributes.</span></span>

5. <span data-ttu-id="16c76-284">기존 특성 매핑을 클릭하여 업데이트하거나 화면 맨 아래에서 **새 매핑 추가**를 클릭하여 새 매핑을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-284">Click on an existing attribute mapping to update it, or click **Add new mapping** at the bottom of the screen to add new mappings.</span></span> <span data-ttu-id="16c76-285">개별 특성 매핑은 다음 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-285">An individual attribute mapping supports these properties:</span></span>

      * <span data-ttu-id="16c76-286">**매핑 유형**</span><span class="sxs-lookup"><span data-stu-id="16c76-286">**Mapping Type**</span></span>

         * <span data-ttu-id="16c76-287">**직접** – Workday 특성 값을 변경하지 않고 AD 특성에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-287">**Direct** – Writes the value of the Workday attribute      to the AD attribute, with no changes</span></span>

         * <span data-ttu-id="16c76-288">**상수** - AD 특성에 고정적인 상수 문자열 값을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-288">**Constant** - Write a static, constant string value to      the AD attribute</span></span>

         * <span data-ttu-id="16c76-289">**식** – 하나 이상의 Workday 특성에 따라 AD 특성에 사용자 지정 값을 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-289">**Expression** – Allows you to write a custom value to the AD attribute, based on one or more Workday attributes.</span></span> <span data-ttu-id="16c76-290">[자세한 내용은 식에 대한 이 문서를 참조하세요](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="16c76-290">[For more info, see this article on expressions](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>

      * <span data-ttu-id="16c76-291">**원본 특성** - Workday의 사용자 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-291">**Source attribute** - The user attribute from Workday.</span></span>

      * <span data-ttu-id="16c76-292">**기본값** – 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-292">**Default value** – Optional.</span></span> <span data-ttu-id="16c76-293">원본 특성의 값이 비어 있는 경우 매핑에서 이 값을 대신 씁니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-293">If the source attribute has an empty value, the mapping will write this value instead.</span></span>
            <span data-ttu-id="16c76-294">이 값을 비워두는 것이 가장 일반적인 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-294">Most common configuration is to leave this blank.</span></span>

      * <span data-ttu-id="16c76-295">**대상 특성** – Active의 사용자 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-295">**Target attribute** – The user attribute in Active     Directory.</span></span>

      * <span data-ttu-id="16c76-296">**이 특성을 사용하여 개체 일치** – Workday와 Active Directory 간에 사용자를 고유하게 식별하는 데 이 매핑을 사용할지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-296">**Match objects using this attribute** – Whether or not this mapping should be used to uniquely identify users between Workday and Active Directory.</span></span> <span data-ttu-id="16c76-297">일반적으로 Workday의 작업자 ID 필드에서 설정하며, 대개 Active Directory의 직원 ID 특성 중 하나에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-297">This is typically set on the Worker ID field for Workday, which is typically mapped to one of the Employee ID attributes in Active Directory.</span></span>

      * <span data-ttu-id="16c76-298">**일치 우선 순위** – 여러 일치 특성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-298">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="16c76-299">일치 특성이 여러 개 있으면 이 필드에 정의된 순서대로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-299">When there are multiple, they are evaluated in the order defined by this field.</span></span> <span data-ttu-id="16c76-300">일치 항목이 발견되는 즉시 더 이상 일치 특성을 평가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-300">As soon as a match is found, no further matching attributes are evaluated.</span></span>

      * <span data-ttu-id="16c76-301">**이 매핑 적용**</span><span class="sxs-lookup"><span data-stu-id="16c76-301">**Apply this mapping**</span></span>
       
         * <span data-ttu-id="16c76-302">**항상** – 사용자 만들기 및 업데이트 작업 시 이 매핑을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-302">**Always** – Apply this mapping on both user creation      and update actions</span></span>

         * <span data-ttu-id="16c76-303">**만들기 작업 시에만** - 사용자 만들기 작업 시에만 이 매핑을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-303">**Only during creation** - Apply this mapping only on      user creation actions</span></span>

6. <span data-ttu-id="16c76-304">매핑을 저장하려면 특성 매핑 섹션 맨 위에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-304">To save your mappings, click **Save** at the top of the      Attribute Mapping section.</span></span>

![Azure 포털](./media/active-directory-saas-workday-inbound-tutorial/WD_2.PNG)

<span data-ttu-id="16c76-306">**아래는 몇 가지 일반적인 식을 사용한 Workday와 Active Directory 간의 특성 매핑을 보여주는 예입니다.**</span><span class="sxs-lookup"><span data-stu-id="16c76-306">**Below are some example attribute mappings between Workday and Active Directory, with some common expressions**</span></span>

-   <span data-ttu-id="16c76-307">parentDistinguishedName AD 특성에 매핑되는 식을 사용하여 하나 이상의 Workday 원본 특성에 따라 특정 OU에 사용자를 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-307">The expression that maps to the parentDistinguishedName AD attribute can be used to provision a user to a specific OU based on one or more Workday source attributes.</span></span> <span data-ttu-id="16c76-308">이 예에서는 Workday의 도시 데이터에 따라 사용자를 여러 OU에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-308">This example places users in different OUs depending on their city data in Workday.</span></span>

-   <span data-ttu-id="16c76-309">userPrincipalName AD 특성에 매핑되는 식은 firstName.LastName@contoso.com의 UPN을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-309">The expression that maps to the userPrincipalName AD attribute create a UPN of firstName.LastName@contoso.com.</span></span> <span data-ttu-id="16c76-310">또한 잘못된 특수 문자를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-310">It also replaces illegal special characters.</span></span>

-   [<span data-ttu-id="16c76-311">식을 쓰는 방법에 대한 설명서는 여기</span><span class="sxs-lookup"><span data-stu-id="16c76-311">There is documentation on writing expressions here</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)

  
| <span data-ttu-id="16c76-312">WORKDAY 특성</span><span class="sxs-lookup"><span data-stu-id="16c76-312">WORKDAY ATTRIBUTE</span></span> | <span data-ttu-id="16c76-313">ACTIVE DIRECTORY 특성</span><span class="sxs-lookup"><span data-stu-id="16c76-313">ACTIVE DIRECTORY ATTRIBUTE</span></span> |  <span data-ttu-id="16c76-314">ID 일치 여부</span><span class="sxs-lookup"><span data-stu-id="16c76-314">MATCHING ID?</span></span> | <span data-ttu-id="16c76-315">만들기/업데이트</span><span class="sxs-lookup"><span data-stu-id="16c76-315">CREATE / UPDATE</span></span> |
| ---------- | ---------- | ---------- | ---------- |
|  <span data-ttu-id="16c76-316">**WorkerID**</span><span class="sxs-lookup"><span data-stu-id="16c76-316">**WorkerID**</span></span>  |  <span data-ttu-id="16c76-317">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="16c76-317">EmployeeID</span></span> | <span data-ttu-id="16c76-318">**예**</span><span class="sxs-lookup"><span data-stu-id="16c76-318">**Yes**</span></span> | <span data-ttu-id="16c76-319">만들기 작업 시에만 기록</span><span class="sxs-lookup"><span data-stu-id="16c76-319">Written on create only</span></span> | 
|  <span data-ttu-id="16c76-320">**Municipality**</span><span class="sxs-lookup"><span data-stu-id="16c76-320">**Municipality**</span></span>   |   <span data-ttu-id="16c76-321">l</span><span class="sxs-lookup"><span data-stu-id="16c76-321">l</span></span>   |     | <span data-ttu-id="16c76-322">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="16c76-322">Create + update</span></span> |
|  <span data-ttu-id="16c76-323">**Company**</span><span class="sxs-lookup"><span data-stu-id="16c76-323">**Company**</span></span>         | <span data-ttu-id="16c76-324">company</span><span class="sxs-lookup"><span data-stu-id="16c76-324">company</span></span>   |     |  <span data-ttu-id="16c76-325">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="16c76-325">Create + update</span></span> |
|  <span data-ttu-id="16c76-326">**CountryReferenceTwoLetter**</span><span class="sxs-lookup"><span data-stu-id="16c76-326">**CountryReferenceTwoLetter**</span></span>      |   <span data-ttu-id="16c76-327">co</span><span class="sxs-lookup"><span data-stu-id="16c76-327">co</span></span> |     |   <span data-ttu-id="16c76-328">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="16c76-328">Create + update</span></span> |
| <span data-ttu-id="16c76-329">**CountryReferenceTwoLetter**</span><span class="sxs-lookup"><span data-stu-id="16c76-329">**CountryReferenceTwoLetter**</span></span>    |  <span data-ttu-id="16c76-330">C</span><span class="sxs-lookup"><span data-stu-id="16c76-330">c</span></span>  |     |         <span data-ttu-id="16c76-331">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="16c76-331">Create + update</span></span> |
| <span data-ttu-id="16c76-332">**SupervisoryOrganization**</span><span class="sxs-lookup"><span data-stu-id="16c76-332">**SupervisoryOrganization**</span></span>  | <span data-ttu-id="16c76-333">department</span><span class="sxs-lookup"><span data-stu-id="16c76-333">department</span></span>  |     |  <span data-ttu-id="16c76-334">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="16c76-334">Create + update</span></span> |
|  <span data-ttu-id="16c76-335">**PreferredNameData**</span><span class="sxs-lookup"><span data-stu-id="16c76-335">**PreferredNameData**</span></span>  |  <span data-ttu-id="16c76-336">displayName</span><span class="sxs-lookup"><span data-stu-id="16c76-336">displayName</span></span> |     |   <span data-ttu-id="16c76-337">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="16c76-337">Create + update</span></span> |
| <span data-ttu-id="16c76-338">**EmployeeID**</span><span class="sxs-lookup"><span data-stu-id="16c76-338">**EmployeeID**</span></span>    |  <span data-ttu-id="16c76-339">cn</span><span class="sxs-lookup"><span data-stu-id="16c76-339">cn</span></span>    |   |   <span data-ttu-id="16c76-340">만들기 작업 시에만 기록</span><span class="sxs-lookup"><span data-stu-id="16c76-340">Written on create only</span></span> |
| <span data-ttu-id="16c76-341">**Fax**</span><span class="sxs-lookup"><span data-stu-id="16c76-341">**Fax**</span></span>      | <span data-ttu-id="16c76-342">facsimileTelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="16c76-342">facsimileTelephoneNumber</span></span>     |     |    <span data-ttu-id="16c76-343">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="16c76-343">Create + update</span></span> |
| <span data-ttu-id="16c76-344">**FirstName**</span><span class="sxs-lookup"><span data-stu-id="16c76-344">**FirstName**</span></span>   | <span data-ttu-id="16c76-345">givenName</span><span class="sxs-lookup"><span data-stu-id="16c76-345">givenName</span></span>       |     |    <span data-ttu-id="16c76-346">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="16c76-346">Create + update</span></span> |
| <span data-ttu-id="16c76-347">**Switch(\[Active\], , "0", "True", "1",)**</span><span class="sxs-lookup"><span data-stu-id="16c76-347">**Switch(\[Active\], , "0", "True", "1",)**</span></span> |  <span data-ttu-id="16c76-348">accountDisabled</span><span class="sxs-lookup"><span data-stu-id="16c76-348">accountDisabled</span></span>      |     | <span data-ttu-id="16c76-349">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="16c76-349">Create + update</span></span> |
| <span data-ttu-id="16c76-350">**Mobile**</span><span class="sxs-lookup"><span data-stu-id="16c76-350">**Mobile**</span></span>  |    <span data-ttu-id="16c76-351">mobile</span><span class="sxs-lookup"><span data-stu-id="16c76-351">mobile</span></span>       |     |       <span data-ttu-id="16c76-352">만들기 작업 시에만 기록</span><span class="sxs-lookup"><span data-stu-id="16c76-352">Written on create only</span></span> |
| <span data-ttu-id="16c76-353">**EmailAddress**</span><span class="sxs-lookup"><span data-stu-id="16c76-353">**EmailAddress**</span></span>    | <span data-ttu-id="16c76-354">mail</span><span class="sxs-lookup"><span data-stu-id="16c76-354">mail</span></span>    |     |     <span data-ttu-id="16c76-355">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="16c76-355">Create + update</span></span> |
| <span data-ttu-id="16c76-356">**ManagerReference**</span><span class="sxs-lookup"><span data-stu-id="16c76-356">**ManagerReference**</span></span>   | <span data-ttu-id="16c76-357">manager</span><span class="sxs-lookup"><span data-stu-id="16c76-357">manager</span></span>  |     |  <span data-ttu-id="16c76-358">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="16c76-358">Create + update</span></span> |
| <span data-ttu-id="16c76-359">**WorkSpaceReference**</span><span class="sxs-lookup"><span data-stu-id="16c76-359">**WorkSpaceReference**</span></span> | <span data-ttu-id="16c76-360">physicalDeliveryOfficeName</span><span class="sxs-lookup"><span data-stu-id="16c76-360">physicalDeliveryOfficeName</span></span>    |     |  <span data-ttu-id="16c76-361">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="16c76-361">Create + update</span></span> |
| <span data-ttu-id="16c76-362">**PostalCode**</span><span class="sxs-lookup"><span data-stu-id="16c76-362">**PostalCode**</span></span>  |   <span data-ttu-id="16c76-363">postalCode</span><span class="sxs-lookup"><span data-stu-id="16c76-363">postalCode</span></span>  |     | <span data-ttu-id="16c76-364">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="16c76-364">Create + update</span></span> |
| <span data-ttu-id="16c76-365">**LocalReference**</span><span class="sxs-lookup"><span data-stu-id="16c76-365">**LocalReference**</span></span> |  <span data-ttu-id="16c76-366">preferredLanguage</span><span class="sxs-lookup"><span data-stu-id="16c76-366">preferredLanguage</span></span>  |     |  <span data-ttu-id="16c76-367">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="16c76-367">Create + update</span></span> |
| <span data-ttu-id="16c76-368">**Replace(Mid(Replace(\[EmployeeID\], , "(\[\\\\/\\\\\\\\\\\\\[\\\\\]\\\\:\\\\;\\\\</span><span class="sxs-lookup"><span data-stu-id="16c76-368">**Replace(Mid(Replace(\[EmployeeID\], , "(\[\\\\/\\\\\\\\\\\\\[\\\\\]\\\\:\\\\;\\\\</span></span>|<span data-ttu-id="16c76-369">\\\\=\\\\,\\\\+\\\\\*\\\\?\\ \\&lt;\\\\&gt;\])", , "", , ), 1, 20), , "([\\\\.) \*\$](file:///\\.) *$)", , "", , )**</span><span class="sxs-lookup"><span data-stu-id="16c76-369">\\\\=\\\\,\\\\+\\\\\*\\\\?\\\\&lt;\\\\&gt;\])", , "", , ), 1, 20), , "([\\\\.)\*\$](file:///\\.)*$)", , "", , )**</span></span>      |    <span data-ttu-id="16c76-370">sAMAccountName</span><span class="sxs-lookup"><span data-stu-id="16c76-370">sAMAccountName</span></span>            |     |         <span data-ttu-id="16c76-371">만들기 작업 시에만 기록</span><span class="sxs-lookup"><span data-stu-id="16c76-371">Written on create only</span></span> |
| <span data-ttu-id="16c76-372">**LastName**</span><span class="sxs-lookup"><span data-stu-id="16c76-372">**LastName**</span></span>   |   <span data-ttu-id="16c76-373">sn</span><span class="sxs-lookup"><span data-stu-id="16c76-373">sn</span></span>   |     |  <span data-ttu-id="16c76-374">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="16c76-374">Create + update</span></span> |
| <span data-ttu-id="16c76-375">**CountryRegionReference**</span><span class="sxs-lookup"><span data-stu-id="16c76-375">**CountryRegionReference**</span></span> |  <span data-ttu-id="16c76-376">st</span><span class="sxs-lookup"><span data-stu-id="16c76-376">st</span></span>     |     | <span data-ttu-id="16c76-377">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="16c76-377">Create + update</span></span> |
| <span data-ttu-id="16c76-378">**AddressLineData**</span><span class="sxs-lookup"><span data-stu-id="16c76-378">**AddressLineData**</span></span>    |  <span data-ttu-id="16c76-379">streetAddress</span><span class="sxs-lookup"><span data-stu-id="16c76-379">streetAddress</span></span>  |     |   <span data-ttu-id="16c76-380">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="16c76-380">Create + update</span></span> |
| <span data-ttu-id="16c76-381">**PrimaryWorkTelephone**</span><span class="sxs-lookup"><span data-stu-id="16c76-381">**PrimaryWorkTelephone**</span></span>  |  <span data-ttu-id="16c76-382">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="16c76-382">telephoneNumber</span></span>   |     | <span data-ttu-id="16c76-383">만들기 작업 시에만 기록</span><span class="sxs-lookup"><span data-stu-id="16c76-383">Written on create only</span></span> |
| <span data-ttu-id="16c76-384">**BusinessTitle**</span><span class="sxs-lookup"><span data-stu-id="16c76-384">**BusinessTitle**</span></span>   |  <span data-ttu-id="16c76-385">title</span><span class="sxs-lookup"><span data-stu-id="16c76-385">title</span></span>     |     |  <span data-ttu-id="16c76-386">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="16c76-386">Create + update</span></span> |
| <span data-ttu-id="16c76-387">**Join("@",Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Join(".", [FirstName], [LastName]), , "([Øø])", , "oe", , ), , "[Ææ]", , "ae", , ), , "([äãàâãåáąÄÃÀÂÃÅÁĄA])", , "a", , ), , "([B])", , "b", , ), , "([CçčćÇČĆ])", , "c", , ), , "([ďĎD])", , "d", , ), , "([ëèéêęěËÈÉÊĘĚE])", , "e", , ), , "([F])", , "f", , ), , "([G])", , "g", , ), , "([H])", , "h", , ), , "([ïîìíÏÎÌÍI])", , "i", , ), , "([J])", , "j", , ), , "([K])", , "k", , ), , "([ľłŁĽL])", , "l", , ), , "([M])", , "m", , ), , "([ñńňÑŃŇN])", , "n", , ), , "([öòőõôóÖÒŐÕÔÓO])", , "o", , ), , "([P])", , "p", , ), , "([Q])", , "q", , ), , "([řŘR])", , "r", , ), , "([ßšśŠŚS])", , "s", , ), , "([TŤť])", , "t", , ), , "([üùûúůűÜÙÛÚŮŰU])", , "u", , ), , "([V])", , "v", , ), , "([W])", , "w", , ), , "([ýÿýŸÝY])", , "y", , ), , "([źžżŹŽŻZ])", , "z", , ), " ", , , "", , ), "contoso.com")**</span><span class="sxs-lookup"><span data-stu-id="16c76-387">**Join("@",Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Join(".", [FirstName], [LastName]), , "([Øø])", , "oe", , ), , "[Ææ]", , "ae", , ), , "([äãàâãåáąÄÃÀÂÃÅÁĄA])", , "a", , ), , "([B])", , "b", , ), , "([CçčćÇČĆ])", , "c", , ), , "([ďĎD])", , "d", , ), , "([ëèéêęěËÈÉÊĘĚE])", , "e", , ), , "([F])", , "f", , ), , "([G])", , "g", , ), , "([H])", , "h", , ), , "([ïîìíÏÎÌÍI])", , "i", , ), , "([J])", , "j", , ), , "([K])", , "k", , ), , "([ľłŁĽL])", , "l", , ), , "([M])", , "m", , ), , "([ñńňÑŃŇN])", , "n", , ), , "([öòőõôóÖÒŐÕÔÓO])", , "o", , ), , "([P])", , "p", , ), , "([Q])", , "q", , ), , "([řŘR])", , "r", , ), , "([ßšśŠŚS])", , "s", , ), , "([TŤť])", , "t", , ), , "([üùûúůűÜÙÛÚŮŰU])", , "u", , ), , "([V])", , "v", , ), , "([W])", , "w", , ), , "([ýÿýŸÝY])", , "y", , ), , "([źžżŹŽŻZ])", , "z", , ), " ", , , "", , ), "contoso.com")**</span></span>   | <span data-ttu-id="16c76-388">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="16c76-388">userPrincipalName</span></span>     |     | <span data-ttu-id="16c76-389">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="16c76-389">Create + update</span></span>                                                   
| <span data-ttu-id="16c76-390">**Switch(\[Municipality\], "OU=Standard Users,OU=Users,OU=Default,OU=Locations,DC=contoso,DC=com", "Dallas", "OU=Standard Users,OU=Users,OU=Dallas,OU=Locations,DC=contoso,DC=com", "Austin", "OU=Standard Users,OU=Users,OU=Austin,OU=Locations,DC=contoso,DC=com", "Seattle", "OU=Standard Users,OU=Users,OU=Seattle,OU=Locations,DC=contoso,DC=com", “London", "OU=Standard Users,OU=Users,OU=London,OU=Locations,DC=contoso,DC=com")**</span><span class="sxs-lookup"><span data-stu-id="16c76-390">**Switch(\[Municipality\], "OU=Standard Users,OU=Users,OU=Default,OU=Locations,DC=contoso,DC=com", "Dallas", "OU=Standard Users,OU=Users,OU=Dallas,OU=Locations,DC=contoso,DC=com", "Austin", "OU=Standard Users,OU=Users,OU=Austin,OU=Locations,DC=contoso,DC=com", "Seattle", "OU=Standard Users,OU=Users,OU=Seattle,OU=Locations,DC=contoso,DC=com", “London", "OU=Standard Users,OU=Users,OU=London,OU=Locations,DC=contoso,DC=com")**</span></span>  | <span data-ttu-id="16c76-391">parentDistinguishedName</span><span class="sxs-lookup"><span data-stu-id="16c76-391">parentDistinguishedName</span></span>     |     |  <span data-ttu-id="16c76-392">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="16c76-392">Create + update</span></span> |
  
### <a name="part-3-configure-the-on-premises-synchronization-agent"></a><span data-ttu-id="16c76-393">3부: 온-프레미스 동기화 에이전트 구성</span><span class="sxs-lookup"><span data-stu-id="16c76-393">Part 3: Configure the on-premises synchronization agent</span></span>

<span data-ttu-id="16c76-394">Active Directory 온-프레미스로 프로비전하려면 원하는 Active Directory 포리스트의 도메인에 가입된 서버에 에이전트를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-394">In order to provision to Active Directory on-premises, an agent must be installed on a domain-joined server in the desire Active Directory forest.</span></span> <span data-ttu-id="16c76-395">이 절차를 완료하려면 도메인 관리자(또는 엔터프라이즈 관리자) 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-395">Domain admin (or Enterprise admin) credentials are required to complete the procedure.</span></span>

<span data-ttu-id="16c76-396">**[온-프레미스 동기화 에이전트는 여기서 다운로드 가능](https://go.microsoft.com/fwlink/?linkid=847801)**</span><span class="sxs-lookup"><span data-stu-id="16c76-396">**[You can download the on-premises synchronization agent here](https://go.microsoft.com/fwlink/?linkid=847801)**</span></span>

<span data-ttu-id="16c76-397">에이전트를 설치한 후에는 아래의 Powershell 명령을 실행하여 환경에 맞게 에이전트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-397">After installing agent, run the Powershell commands below to configure the agent for your environment.</span></span>

<span data-ttu-id="16c76-398">**명령 #1**</span><span class="sxs-lookup"><span data-stu-id="16c76-398">**Command #1**</span></span>

> <span data-ttu-id="16c76-399">cd C:\\Program Files\\Microsoft Azure Active Directory Synchronization Agent\\Modules\\AADSyncAgent</span><span class="sxs-lookup"><span data-stu-id="16c76-399">cd C:\\Program Files\\Microsoft Azure Active Directory Synchronization Agent\\Modules\\AADSyncAgent</span></span>

> <span data-ttu-id="16c76-400">import-module AADSyncAgent.psd1</span><span class="sxs-lookup"><span data-stu-id="16c76-400">import-module AADSyncAgent.psd1</span></span>

<span data-ttu-id="16c76-401">**명령 #2**</span><span class="sxs-lookup"><span data-stu-id="16c76-401">**Command #2**</span></span>

> <span data-ttu-id="16c76-402">Add-ADSyncAgentActiveDirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="16c76-402">Add-ADSyncAgentActiveDirectoryConfiguration</span></span>

* <span data-ttu-id="16c76-403">입력: "디렉터리 이름"으로 파트 \#2에서 입력한 AD 포리스트 이름 입력</span><span class="sxs-lookup"><span data-stu-id="16c76-403">Input: For "Directory Name", enter the AD Forest name, as entered in part \#2</span></span>
* <span data-ttu-id="16c76-404">입력: Active Directory 포리스트의 관리 사용자 이름 및 암호 입력</span><span class="sxs-lookup"><span data-stu-id="16c76-404">Input: Admin username and password for Active Directory forest</span></span>

<span data-ttu-id="16c76-405">**명령 #3**</span><span class="sxs-lookup"><span data-stu-id="16c76-405">**Command #3**</span></span>

> <span data-ttu-id="16c76-406">Add-ADSyncAgentAzureActiveDirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="16c76-406">Add-ADSyncAgentAzureActiveDirectoryConfiguration</span></span>

* <span data-ttu-id="16c76-407">입력: Azure AD 테넌트의 전역 관리 사용자 이름 및 암호</span><span class="sxs-lookup"><span data-stu-id="16c76-407">Input: Global admin username and password for your Azure AD tenant</span></span>

<span data-ttu-id="16c76-408">**명령 #4**</span><span class="sxs-lookup"><span data-stu-id="16c76-408">**Command #4**</span></span>

> <span data-ttu-id="16c76-409">Get-AdSyncAgentProvisioningTasks</span><span class="sxs-lookup"><span data-stu-id="16c76-409">Get-AdSyncAgentProvisioningTasks</span></span>

* <span data-ttu-id="16c76-410">작업: 데이터가 반환되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-410">Action: Confirm data is returned.</span></span> <span data-ttu-id="16c76-411">이 명령은 Azure AD 테넌트에서 Workday 프로비전 앱을 자동으로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-411">This command automatically discovers Workday provisioning apps in your Azure AD tenant.</span></span> <span data-ttu-id="16c76-412">예제 출력:</span><span class="sxs-lookup"><span data-stu-id="16c76-412">Example output:</span></span>

> <span data-ttu-id="16c76-413">Name          : My AD Forest</span><span class="sxs-lookup"><span data-stu-id="16c76-413">Name          : My AD Forest</span></span>
>
> <span data-ttu-id="16c76-414">Enabled       : True</span><span class="sxs-lookup"><span data-stu-id="16c76-414">Enabled       : True</span></span>
>
> <span data-ttu-id="16c76-415">DirectoryName : mydomain.contoso.com</span><span class="sxs-lookup"><span data-stu-id="16c76-415">DirectoryName : mydomain.contoso.com</span></span>
>
> <span data-ttu-id="16c76-416">Credentialed  : False</span><span class="sxs-lookup"><span data-stu-id="16c76-416">Credentialed  : False</span></span>
>
> <span data-ttu-id="16c76-417">Identifier    : WDAYdnAppDelta.c2ef8d247a61499ba8af0a29208fb853.4725aa7b-1103-41e6-8929-75a5471a5203</span><span class="sxs-lookup"><span data-stu-id="16c76-417">Identifier    : WDAYdnAppDelta.c2ef8d247a61499ba8af0a29208fb853.4725aa7b-1103-41e6-8929-75a5471a5203</span></span>

<span data-ttu-id="16c76-418">**명령 #5**</span><span class="sxs-lookup"><span data-stu-id="16c76-418">**Command #5**</span></span>

> <span data-ttu-id="16c76-419">Start-AdSyncAgentSynchronization -Automatic</span><span class="sxs-lookup"><span data-stu-id="16c76-419">Start-AdSyncAgentSynchronization -Automatic</span></span>

<span data-ttu-id="16c76-420">**명령 #6**</span><span class="sxs-lookup"><span data-stu-id="16c76-420">**Command #6**</span></span>

> <span data-ttu-id="16c76-421">net stop aadsyncagent</span><span class="sxs-lookup"><span data-stu-id="16c76-421">net stop aadsyncagent</span></span>

<span data-ttu-id="16c76-422">**명령 #7**</span><span class="sxs-lookup"><span data-stu-id="16c76-422">**Command #7**</span></span>

> <span data-ttu-id="16c76-423">net start aadsyncagent</span><span class="sxs-lookup"><span data-stu-id="16c76-423">net start aadsyncagent</span></span>

### <a name="part-4-start-the-service"></a><span data-ttu-id="16c76-424">4부: 서비스 시작</span><span class="sxs-lookup"><span data-stu-id="16c76-424">Part 4: Start the service</span></span>
<span data-ttu-id="16c76-425">1-3부를 완료했으면 Azure 관리 포털에서 프로비전 서비스를 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-425">Once parts 1-3 have been completed, you can start the provisioning service back in the Azure Management Portal.</span></span>

1.  <span data-ttu-id="16c76-426">**프로비전** 탭에서 **프로비전 상태**를 **켜기**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-426">In the **Provisioning** tab, set the **Provisioning Status** to **On**.</span></span>

2. <span data-ttu-id="16c76-427">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-427">Click **Save**.</span></span>

3. <span data-ttu-id="16c76-428">그러면 초기 동기화가 시작되며, Workday에 있는 사용자 수에 따라 동기화에 걸리는 시간이 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-428">This will start the initial sync, which can take a variable number of hours depending on how many users are in Workday.</span></span>

4. <span data-ttu-id="16c76-429">Workday에서 어떤 사용자를 읽은 후 Active Directory에 추가 또는 업데이트되는지와 같은 개별 동기화 이벤트는 **감사 로그** 탭에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-429">Individual sync events such as what users are being read out of Workday, and then subsequently added or updated to Active Directory, can be viewed in the **Audit Logs** tab.</span></span> <span data-ttu-id="16c76-430">**[감사 로그를 읽는 방법에 대한 자세한 지침은 프로비전 보고 가이드 참조](active-directory-saas-provisioning-reporting.md)**</span><span class="sxs-lookup"><span data-stu-id="16c76-430">**[See the provisioning reporting guide for detailed instructions on how to read the audit logs](active-directory-saas-provisioning-reporting.md)**</span></span>

5.  <span data-ttu-id="16c76-431">에이전트 컴퓨터의 Windows 응용 프로그램 로그에는 에이전트를 통해 수행된 모든 작업이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-431">The Windows Application log on the agent machine will show all operations performed via the agent.</span></span>

6. <span data-ttu-id="16c76-432">작업이 완료되면 아래와 같이 **프로비전** 탭에 감사 요약 보고서가 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-432">One completed, it will write an audit summary report in the  **Provisioning** tab, as shown below.</span></span>

![Azure portal](./media/active-directory-saas-workday-inbound-tutorial/WD_3.PNG)


## <a name="configuring-user-provisioning-to-azure-active-directory"></a><span data-ttu-id="16c76-434">Azure Active Directory로 사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="16c76-434">Configuring user provisioning to Azure Active Directory</span></span>
<span data-ttu-id="16c76-435">Azure Active Directory로 프로비전을 구성하는 방법은 프로비전 요구 사항에 따라 달라지며, 아래 표에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-435">How you configure provisioning to Azure Active Directory will depend on your provisioning requirements, as detailed in the table below.</span></span>

| <span data-ttu-id="16c76-436">시나리오</span><span class="sxs-lookup"><span data-stu-id="16c76-436">Scenario</span></span> | <span data-ttu-id="16c76-437">해결 방법</span><span class="sxs-lookup"><span data-stu-id="16c76-437">Solution</span></span> |
| -------- | -------- |
| <span data-ttu-id="16c76-438">**사용자를 Active Directory 및 Azure AD에 프로비전 해야 함**</span><span class="sxs-lookup"><span data-stu-id="16c76-438">**Users need to be provisioned to Active Directory and Azure AD**</span></span> | <span data-ttu-id="16c76-439">**[AAD Connect](connect/active-directory-aadconnect.md)** 사용</span><span class="sxs-lookup"><span data-stu-id="16c76-439">Use **[AAD Connect](connect/active-directory-aadconnect.md)**</span></span> |
| <span data-ttu-id="16c76-440">**사용자를 Active Directory에만 프로비전 해야 함**</span><span class="sxs-lookup"><span data-stu-id="16c76-440">**Users need to be provisioned to Active Directory only**</span></span> | <span data-ttu-id="16c76-441">**[AAD Connect](connect/active-directory-aadconnect.md)** 사용</span><span class="sxs-lookup"><span data-stu-id="16c76-441">Use **[AAD Connect](connect/active-directory-aadconnect.md)**</span></span> |
| <span data-ttu-id="16c76-442">**사용자를 Azure AD에만(클라우드에만) 프로비전 해야 함**</span><span class="sxs-lookup"><span data-stu-id="16c76-442">**Users need to be provisioned to Azure AD only (cloud only)**</span></span> | <span data-ttu-id="16c76-443">앱 갤러리의 **Workday에서 Azure Active Directory로 프로비전** 앱 사용</span><span class="sxs-lookup"><span data-stu-id="16c76-443">Use the **Workday to Azure Active Directory provisioning** app in the app gallery</span></span> |

<span data-ttu-id="16c76-444">Azure AD Connect 설정에 대한 자세한 지침은 [Azure AD Connect 설명서](connect/active-directory-aadconnect.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16c76-444">For instructions on setting up Azure AD Connect, see the [Azure AD Connect documentation](connect/active-directory-aadconnect.md).</span></span>

<span data-ttu-id="16c76-445">다음 섹션에서는 클라우드 전용 사용자를 프로비전하기 위해 Workday와 Azure AD 간 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-445">The following sections describe setting up a connection between Workday and Azure AD to provision cloud-only users.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="16c76-446">Azure AD에만 프로비전해야 하고 온-프레미스 Active Directory에는 프로비전하면 안 되는 클라우드 전용 사용자가 있는 경우 아래 절차만 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-446">Only follow the procedure below if you have cloud-only users that need to be provisioned to Azure AD and not on-premises Active Directory.</span></span>

### <a name="part-1-adding-the-azure-ad-provisioning-connector-app-and-creating-the-connection-to-workday"></a><span data-ttu-id="16c76-447">1부: Azure AD 프로비전 커넥터 앱을 추가하고 Workday에 대한 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="16c76-447">Part 1: Adding the Azure AD provisioning connector app and creating the connection to Workday</span></span>

<span data-ttu-id="16c76-448">**클라우드 전용 사용자에 대한 Workday-Azure Active Directory 프로비전을 구성하려면:**</span><span class="sxs-lookup"><span data-stu-id="16c76-448">**To configure Workday to Azure Active Directory provisioning for cloud-only users:**</span></span>

1.  <span data-ttu-id="16c76-449"><https://portal.azure.com>으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-449">Go to <https://portal.azure.com>.</span></span>

2.  <span data-ttu-id="16c76-450">왼쪽 탐색 모음에서 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-450">In the left navigation bar, select **Azure Active Directory**</span></span>

3.  <span data-ttu-id="16c76-451">**엔터프라이즈 응용 프로그램**, **모든 응용 프로그램**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-451">Select **Enterprise Applications**, then **All Applications**.</span></span>

4.  <span data-ttu-id="16c76-452">**응용 프로그램 추가**를 선택한 후 **모두** 범주를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-452">Select **Add an application**, and then select the **All** category.</span></span>

5.  <span data-ttu-id="16c76-453">**Workday-Azure AD 프로비전**을 검색하고, 갤러리에서 해당 앱을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-453">Search for **Workday to Azure AD provisioning**, and add that app from the gallery.</span></span>

6.  <span data-ttu-id="16c76-454">앱이 추가되고 앱 세부 정보 화면이 표시되면 **프로비전**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-454">After the app is added and the app details screen is shown, select **Provisioning**</span></span>

7.  <span data-ttu-id="16c76-455">**프로비전** **모드**를 **자동**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-455">Change the **Provisioning** **Mode** to **Automatic**</span></span>

8.  <span data-ttu-id="16c76-456">다음과 같이 **관리자 자격 증명** 섹션을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-456">Complete the **Admin Credentials** section as follows:</span></span>

   * <span data-ttu-id="16c76-457">**관리 사용자 이름** – 테넌트 도메인 이름이 추가된 Workday 통합 시스템 계정의 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-457">**Admin Username** – Enter the username of the Workday integration system account, with the tenant domain name appended.</span></span> <span data-ttu-id="16c76-458">다음과 같은 형태여야 합니다. username@contoso4</span><span class="sxs-lookup"><span data-stu-id="16c76-458">Should look something like: username@contoso4</span></span>

   * <span data-ttu-id="16c76-459">**관리자 암호 –** Workday 통합 시스템 계정의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-459">**Admin password –** Enter the password of the Workday    integration system account</span></span>

   * <span data-ttu-id="16c76-460">**테넌트 URL –** 해당 테넌트의 Workday 웹 서비스 끝점에 대한 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-460">**Tenant URL –** Enter the URL to the Workday web services endpoint for your tenant.</span></span> <span data-ttu-id="16c76-461">https://wd3-impl-services1.workday.com/ccx/service/contoso4와 같은 형태여야 하며, 여기서 contoso4를 올바른 테넌트 이름으로 바꾸고 wd3-impl을 올바른 환경 문자열로 바꾸면 됩니다(필요한 경우).</span><span class="sxs-lookup"><span data-stu-id="16c76-461">This should look like: https://wd3-impl-services1.workday.com/ccx/service/contoso4, where contoso4 is replaced with your correct tenant name and wd3-impl is replaced with the correct environment string (if necessary).</span></span>

   * <span data-ttu-id="16c76-462">**알림 이메일 –** 이메일 주소를 입력하고 "오류가 발생하면 이메일 보내기" 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-462">**Notification Email –** Enter your email address, and check the    “send email if failure occurs” checkbox.</span></span>

   * <span data-ttu-id="16c76-463">**연결 테스트** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-463">Click the **Test Connection** button.</span></span>

   * <span data-ttu-id="16c76-464">연결 테스트가 성공하면 맨 위에서 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-464">If the connection test succeeds, click the **Save** button at the top.</span></span> <span data-ttu-id="16c76-465">연결 테스트가 실패하면 Workday에서 Workday URL 및 자격 증명이 유효한지 다시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-465">If it fails, double-check that the Workday URL and credentials are valid in Workday.</span></span>


### <a name="part-2-configure-attribute-mappings"></a><span data-ttu-id="16c76-466">2부: 특성 매핑 구성</span><span class="sxs-lookup"><span data-stu-id="16c76-466">Part 2: Configure attribute mappings</span></span> 

<span data-ttu-id="16c76-467">이 섹션에서는 클라우드 전용 사용자의 사용자 데이터가 Workday에서 Azure Active Directory로 흐르는 방식을 구성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-467">In this section, you will configure how user data flows from Workday to Azure Active Directory for cloud-only users.</span></span>

1.  <span data-ttu-id="16c76-468">**매핑** 아래의 프로비전 탭에서 **Workday 작업자를 Azure AD와 동기화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-468">On the Provisioning tab under **Mappings**, click **Synchronize Workers to Azure AD**.</span></span>

2.   <span data-ttu-id="16c76-469">**원본 개체 범위** 필드에서 특성 기반 필터 집합을 정의하여 Azure AD 프로비전 범위에 포함할 Workday 사용자 집합을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-469">In the **Source Object Scope** field, you can select which sets of users in Workday should be in scope for provisioning to Azure AD, by defining a set of attribute-based filters.</span></span> <span data-ttu-id="16c76-470">기본 범위는 "Workday의 모든 사용자"입니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-470">The default scope is “all users in Workday”.</span></span> <span data-ttu-id="16c76-471">예제 필터:</span><span class="sxs-lookup"><span data-stu-id="16c76-471">Example filters:</span></span>

   * <span data-ttu-id="16c76-472">예: 작업자 ID가 1000000-2000000 사이인 사용자를 범위에 포함</span><span class="sxs-lookup"><span data-stu-id="16c76-472">Example: Scope to users with Worker IDs between 1000000 and   2000000</span></span>

      * <span data-ttu-id="16c76-473">특성: WorkerID</span><span class="sxs-lookup"><span data-stu-id="16c76-473">Attribute: WorkerID</span></span>

      * <span data-ttu-id="16c76-474">연산자: REGEX Match</span><span class="sxs-lookup"><span data-stu-id="16c76-474">Operator: REGEX Match</span></span>

      * <span data-ttu-id="16c76-475">값: (1[0-9][0-9][0-9][0-9][0-9][0-9])</span><span class="sxs-lookup"><span data-stu-id="16c76-475">Value: (1[0-9][0-9][0-9][0-9][0-9][0-9])</span></span>

   * <span data-ttu-id="16c76-476">예: 비정규직 직원만 포함하고 정규직 직원은 포함하지 않음</span><span class="sxs-lookup"><span data-stu-id="16c76-476">Example: Only contingent workers and not regular employees</span></span>

      * <span data-ttu-id="16c76-477">특성: ContingentID</span><span class="sxs-lookup"><span data-stu-id="16c76-477">Attribute: ContingentID</span></span>

      * <span data-ttu-id="16c76-478">연산자: IS NOT NULL</span><span class="sxs-lookup"><span data-stu-id="16c76-478">Operator: IS NOT NULL</span></span>

3.  <span data-ttu-id="16c76-479">**대상 개체 작업** 필드에서 어떤 작업을 Azure AD에서 수행할 수 있도록 허용할 것인지 전역적으로 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-479">In the **Target Object Actions** field, you can globally filter what actions are allowed to be performed on Azure AD.</span></span> <span data-ttu-id="16c76-480">**만들기** 및 **업데이트**가 가장 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-480">**Create** and **Update** are most common.</span></span>

4.  <span data-ttu-id="16c76-481">**특성 매핑** 섹션에서 개별 Workday 특성이 Active Directory 특성에 매핑되는 방식을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-481">In the **Attribute mappings** section, you can define how individual Workday attributes map to Active Directory attributes.</span></span>

5. <span data-ttu-id="16c76-482">기존 특성 매핑을 클릭하여 업데이트하거나 화면 맨 아래에서 **새 매핑 추가**를 클릭하여 새 매핑을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-482">Click on an existing attribute mapping to update it, or click **Add new mapping** at the bottom of the screen to add new mappings.</span></span> <span data-ttu-id="16c76-483">개별 특성 매핑은 다음 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-483">An individual attribute mapping supports these properties:</span></span>

   * <span data-ttu-id="16c76-484">**매핑 유형**</span><span class="sxs-lookup"><span data-stu-id="16c76-484">**Mapping Type**</span></span>

      * <span data-ttu-id="16c76-485">**직접** – Workday 특성 값을 변경하지 않고 AD 특성에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-485">**Direct** – Writes the value of the Workday attribute         to the AD attribute, with no changes</span></span>

      * <span data-ttu-id="16c76-486">**상수** - AD 특성에 고정적인 상수 문자열 값을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-486">**Constant** - Write a static, constant string value to         the AD attribute</span></span>

      * <span data-ttu-id="16c76-487">**식** – 하나 이상의 Workday 특성에 따라 AD 특성에 사용자 지정 값을 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-487">**Expression** – Allows you to write a custom value to the AD attribute, based on one or more Workday attributes.</span></span> <span data-ttu-id="16c76-488">[자세한 내용은 식에 대한 이 문서를 참조하세요](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="16c76-488">[For more info, see this article on expressions](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>

   * <span data-ttu-id="16c76-489">**원본 특성** - Workday의 사용자 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-489">**Source attribute** - The user attribute from Workday.</span></span>

   * <span data-ttu-id="16c76-490">**기본값** – 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-490">**Default value** – Optional.</span></span> <span data-ttu-id="16c76-491">원본 특성의 값이 비어 있는 경우 매핑에서 이 값을 대신 씁니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-491">If the source attribute has an empty value, the mapping will write this value instead.</span></span>
            <span data-ttu-id="16c76-492">이 값을 비워두는 것이 가장 일반적인 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-492">Most common configuration is to leave this blank.</span></span>

   * <span data-ttu-id="16c76-493">**대상 특성** – Azure AD의 사용자 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-493">**Target attribute** – The user attribute in Azure AD.</span></span>

   * <span data-ttu-id="16c76-494">**이 특성을 사용하여 개체 일치** – Workday와 Azure AD 간에 사용자를 고유하게 식별하는 데 이 매핑을 사용할지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-494">**Match objects using this attribute** – Whether or not this mapping should be used to uniquely identify users between Workday and Azure AD.</span></span> <span data-ttu-id="16c76-495">일반적으로 Workday의 작업자 ID 필드에서 설정하며, 대개 Azure AD의 직원 ID 특성(신규) 또는 확장 특성에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-495">This is typically set on the Worker ID field for Workday, which is typically mapped to the Employee ID attribute (new) or an extension attribute in Azure AD.</span></span>

   * <span data-ttu-id="16c76-496">**일치 우선 순위** – 여러 일치 특성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-496">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="16c76-497">일치 특성이 여러 개 있으면 이 필드에 정의된 순서대로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-497">When there are multiple, they are evaluated in the order defined by this field.</span></span> <span data-ttu-id="16c76-498">일치 항목이 발견되는 즉시 더 이상 일치 특성을 평가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-498">As soon as a match is found, no further matching attributes are evaluated.</span></span>

   * <span data-ttu-id="16c76-499">**이 매핑 적용**</span><span class="sxs-lookup"><span data-stu-id="16c76-499">**Apply this mapping**</span></span>

     * <span data-ttu-id="16c76-500">**항상** – 사용자 만들기 및 업데이트 작업 시 이 매핑을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-500">**Always** – Apply this mapping on both user creation          and update actions</span></span>

     * <span data-ttu-id="16c76-501">**만들기 작업 시에만** - 사용자 만들기 작업 시에만 이 매핑을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-501">**Only during creation** - Apply this mapping only on          user creation actions</span></span>

6. <span data-ttu-id="16c76-502">매핑을 저장하려면 특성 매핑 섹션 맨 위에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-502">To save your mappings, click **Save** at the top of the      Attribute Mapping section.</span></span>

### <a name="part-3-start-the-service"></a><span data-ttu-id="16c76-503">3부: 서비스 시작</span><span class="sxs-lookup"><span data-stu-id="16c76-503">Part 3: Start the service</span></span>
<span data-ttu-id="16c76-504">1-2부를 완료했으면 프로비전 서비스를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-504">Once parts 1-2 have been completed, you can start the provisioning service.</span></span>

1.  <span data-ttu-id="16c76-505">**프로비전** 탭에서 **프로비전 상태**를 **켜기**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-505">In the **Provisioning** tab, set the **Provisioning Status** to **On**.</span></span>

2. <span data-ttu-id="16c76-506">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-506">Click **Save**.</span></span>

3. <span data-ttu-id="16c76-507">그러면 초기 동기화가 시작되며, Workday에 있는 사용자 수에 따라 동기화에 걸리는 시간이 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-507">This will start the initial sync, which can take a variable number  of hours depending on how many users are in Workday.</span></span>

4. <span data-ttu-id="16c76-508">개별 동기화 이벤트는 **감사 로그** 탭에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-508">Individual sync events can be viewed in the **Audit Logs** tab.</span></span> <span data-ttu-id="16c76-509">**[감사 로그를 읽는 방법에 대한 자세한 지침은 프로비전 보고 가이드 참조](active-directory-saas-provisioning-reporting.md)**</span><span class="sxs-lookup"><span data-stu-id="16c76-509">**[See the provisioning reporting guide for detailed instructions on how to read the audit logs](active-directory-saas-provisioning-reporting.md)**</span></span>

5. <span data-ttu-id="16c76-510">작업이 완료되면 아래와 같이 **프로비전** 탭에 감사 요약 보고서가 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-510">One completed, it will write an audit summary report in the  **Provisioning** tab, as shown below.</span></span>


## <a name="configuring-writeback-of-email-addresses-to-workday"></a><span data-ttu-id="16c76-511">Workday로 이메일 주소 쓰기 저장 구성</span><span class="sxs-lookup"><span data-stu-id="16c76-511">Configuring writeback of email addresses to Workday</span></span>
<span data-ttu-id="16c76-512">다음 지침에 따라 Azure Active Directory에서 Workday로 사용자 이메일 주소 쓰기 저장을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-512">Follow these instructions to configure writeback of user email addresses from Azure Active Directory to Workday.</span></span>

### <a name="part-1-adding-the-provisioning-connector-app-and-creating-the-connection-to-workday"></a><span data-ttu-id="16c76-513">1부: 프로비전 커넥터 앱을 추가하고 Workday에 대한 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="16c76-513">Part 1: Adding the provisioning connector app and creating the connection to Workday</span></span>

<span data-ttu-id="16c76-514">**Workday에서 Active Directory로의 프로비전을 구성하려면:**</span><span class="sxs-lookup"><span data-stu-id="16c76-514">**To configure Workday to Active Directory provisioning:**</span></span>

1.  <span data-ttu-id="16c76-515"><https://portal.azure.com>으로 이동</span><span class="sxs-lookup"><span data-stu-id="16c76-515">Go to <https://portal.azure.com></span></span>

2.  <span data-ttu-id="16c76-516">왼쪽 탐색 모음에서 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-516">In the left navigation bar, select **Azure Active Directory**</span></span>

3.  <span data-ttu-id="16c76-517">**엔터프라이즈 응용 프로그램**, **모든 응용 프로그램**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-517">Select **Enterprise Applications**, then **All Applications**.</span></span>

4.  <span data-ttu-id="16c76-518">**응용 프로그램 추가**를 선택한 후 **모두** 범주를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-518">Select **Add an application**, then select the **All** category.</span></span>

5.  <span data-ttu-id="16c76-519">**Workday 쓰기 저장**을 검색하고, 갤러리에서 해당 앱을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-519">Search for **Workday Writeback**, and add that app from the gallery.</span></span>

6.  <span data-ttu-id="16c76-520">앱이 추가되고 앱 세부 정보 화면이 표시되면 **프로비전**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-520">After the app is added and the app details screen is shown, select **Provisioning**</span></span>

7.  <span data-ttu-id="16c76-521">**프로비전** **모드**를 **자동**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-521">Change the **Provisioning** **Mode** to **Automatic**</span></span>

8.  <span data-ttu-id="16c76-522">다음과 같이 **관리자 자격 증명** 섹션을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-522">Complete the **Admin Credentials** section as follows:</span></span>

   * <span data-ttu-id="16c76-523">**관리 사용자 이름** – 테넌트 도메인 이름이 추가된 Workday 통합 시스템 계정의 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-523">**Admin Username** – Enter the username of the Workday integration system account, with the tenant domain name appended.</span></span> <span data-ttu-id="16c76-524">다음과 같은 형태여야 합니다. username@contoso4</span><span class="sxs-lookup"><span data-stu-id="16c76-524">Should look something like: username@contoso4</span></span>

   * <span data-ttu-id="16c76-525">**관리자 암호 –** Workday 통합 시스템 계정의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-525">**Admin password –** Enter the password of the Workday    integration system account</span></span>

   * <span data-ttu-id="16c76-526">**테넌트 URL –** 해당 테넌트의 Workday 웹 서비스 끝점에 대한 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-526">**Tenant URL –** Enter the URL to the Workday web services endpoint for your tenant.</span></span> <span data-ttu-id="16c76-527">https://wd3-impl-services1.workday.com/ccx/service/contoso4와 같은 형태여야 하며, 여기서 contoso4를 올바른 테넌트 이름으로 바꾸고 wd3-impl을 올바른 환경 문자열로 바꾸면 됩니다(필요한 경우).</span><span class="sxs-lookup"><span data-stu-id="16c76-527">This should look like: https://wd3-impl-services1.workday.com/ccx/service/contoso4, where contoso4 is replaced with your correct tenant name and wd3-impl is replaced with the correct environment string (if necessary).</span></span>

   * <span data-ttu-id="16c76-528">**알림 이메일 –** 이메일 주소를 입력하고 "오류가 발생하면 이메일 보내기" 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-528">**Notification Email –** Enter your email address, and check the    “send email if failure occurs” checkbox.</span></span>

   * <span data-ttu-id="16c76-529">**연결 테스트** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-529">Click the **Test Connection** button.</span></span> <span data-ttu-id="16c76-530">연결 테스트가 성공하면 맨 위에서 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-530">If the connection test succeeds, click the **Save** button at the top.</span></span> <span data-ttu-id="16c76-531">연결 테스트가 실패하면 Workday에서 Workday URL 및 자격 증명이 유효한지 다시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-531">If it fails, double-check that the Workday URL and credentials are valid in Workday.</span></span>


### <a name="part-2-configure-attribute-mappings"></a><span data-ttu-id="16c76-532">2부: 특성 매핑 구성</span><span class="sxs-lookup"><span data-stu-id="16c76-532">Part 2: Configure attribute mappings</span></span> 


<span data-ttu-id="16c76-533">이 섹션에서는 사용자 데이터가 Workday에서 Active Directory로 흐르는 방식을 구성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-533">In this section, you will configure how user data flows from Workday to Active Directory.</span></span>

1.  <span data-ttu-id="16c76-534">**매핑** 아래의 프로비전 탭에서 **Azure AD 사용자를 Workday와 동기화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-534">On the Provisioning tab under **Mappings**, click **Synchronize Azure AD Users to Workday**.</span></span>

2.  <span data-ttu-id="16c76-535">선택 사항으로 **원본 개체 범위** 필드에서 Azure Active Directory의 사용자 집합 중 Workday에 이메일 주소를 기록할 사용자 집합을 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-535">In the **Source Object Scope** field, you can optionally filter which sets of users in Azure Active Directory should have their email addresses written back to Workday.</span></span> <span data-ttu-id="16c76-536">기본 범위는 "Azure AD의 모든 사용자"입니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-536">The default scope is “all users in Azure AD”.</span></span> 

3.  <span data-ttu-id="16c76-537">**특성 매핑** 섹션에서 개별 Workday 특성이 Active Directory 특성에 매핑되는 방식을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-537">In the **Attribute mappings** section, you can define how individual Workday attributes map to Active Directory attributes.</span></span> <span data-ttu-id="16c76-538">기본적으로 이메일 주소에 대한 매핑이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-538">There is a mapping for the email address by default.</span></span> <span data-ttu-id="16c76-539">그러나 Azure AD의 사용자가 Workday의 해당 항목과 일치하도록 일치 ID를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-539">However, the matching ID must be updated to match users in Azure AD with their corresponding entries in Workday.</span></span> <span data-ttu-id="16c76-540">Workday 작업자 ID 또는 직원 ID를 Azure AD의 extensionAttribute1-15와 동기화한 후 Azure AD에서 이 특성을 사용하여 Workday에서 사용자를 다시 일치시키는 방법이 주로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-540">A popular matching method is to synchronize the Workday worker ID or employee ID to extensionAttribute1-15 in Azure AD, and then use this attribute in Azure AD to match users back in Workday.</span></span>

4.  <span data-ttu-id="16c76-541">매핑을 저장하려면 특성 매핑 섹션 맨 위에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-541">To save your mappings, click **Save** at the top of the Attribute Mapping section.</span></span>

### <a name="part-3-start-the-service"></a><span data-ttu-id="16c76-542">3부: 서비스 시작</span><span class="sxs-lookup"><span data-stu-id="16c76-542">Part 3: Start the service</span></span>
<span data-ttu-id="16c76-543">1-2부를 완료했으면 프로비전 서비스를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-543">Once parts 1-2 have been completed, you can start the provisioning service.</span></span>

1.  <span data-ttu-id="16c76-544">**프로비전** 탭에서 **프로비전 상태**를 **켜기**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-544">In the **Provisioning** tab, set the **Provisioning Status** to **On**.</span></span>

2. <span data-ttu-id="16c76-545">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-545">Click **Save**.</span></span>

3. <span data-ttu-id="16c76-546">그러면 초기 동기화가 시작되며, Workday에 있는 사용자 수에 따라 동기화에 걸리는 시간이 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-546">This will start the initial sync, which can take a variable number  of hours depending on how many users are in Workday.</span></span>

4. <span data-ttu-id="16c76-547">개별 동기화 이벤트는 **감사 로그** 탭에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-547">Individual sync events can be viewed in the **Audit Logs** tab.</span></span> <span data-ttu-id="16c76-548">**[감사 로그를 읽는 방법에 대한 자세한 지침은 프로비전 보고 가이드 참조](active-directory-saas-provisioning-reporting.md)**</span><span class="sxs-lookup"><span data-stu-id="16c76-548">**[See the provisioning reporting guide for detailed instructions on how to read the audit logs](active-directory-saas-provisioning-reporting.md)**</span></span>

5. <span data-ttu-id="16c76-549">작업이 완료되면 아래와 같이 **프로비전** 탭에 감사 요약 보고서가 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-549">One completed, it will write an audit summary report in the  **Provisioning** tab, as shown below.</span></span>

## <a name="known-issues"></a><span data-ttu-id="16c76-550">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="16c76-550">Known issues</span></span>

* <span data-ttu-id="16c76-551">**유럽 로캘의 감사 로그** - 이 기술 미리 보기가 릴리스된 날짜를 기준으로, Azure AD 테넌트가 유럽 데이터 센터에 상주하는 경우 Workday 커넥터 앱의 [감사 로그](active-directory-saas-provisioning-reporting.md)가 [Azure Portal](https://portal.azure.com)에 표시되지 않는 알려진 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-551">**Audit logs in European locales** - As of the release of this technical preview, there is a known issue with the [audit logs](active-directory-saas-provisioning-reporting.md) for the Workday connector apps not appearing in the [Azure portal](https://portal.azure.com) if the Azure AD tenant resides in a European data center.</span></span> <span data-ttu-id="16c76-552">이 문제에 대한 픽스가 곧 출시될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="16c76-552">A fix for this issue is forthcoming.</span></span> <span data-ttu-id="16c76-553">가까운 시일 안에 이 페이지를 다시 방문하여 업데이트를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="16c76-553">Please check this space again in the near future for updates.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="16c76-554">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="16c76-554">Additional resources</span></span>
* [<span data-ttu-id="16c76-555">자습서: Workday와 Azure Active Directory 간 Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="16c76-555">Tutorial: Configuring single sign-on between Workday and Azure Active Directory</span></span>](active-directory-saas-workday-tutorial.md)
* [<span data-ttu-id="16c76-556">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="16c76-556">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="16c76-557">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="16c76-557">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="16c76-558">다음 단계</span><span class="sxs-lookup"><span data-stu-id="16c76-558">Next steps</span></span>

* <span data-ttu-id="16c76-559">[프로비전 활동에 대한 로그를 검토하고 보고서를 받아 보는 방법을 살펴봅니다](https://docs.microsoft.com/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="16c76-559">[Learn how to review logs and get reports on provisioning activity](https://docs.microsoft.com/azure/active-directory/active-directory-saas-provisioning-reporting)</span></span>
