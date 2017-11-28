---
title: "자습서: 온-프레미스 Active Directory 및 Azure Active Directory를 사용하여 사용자를 자동으로 프로비전하도록 Workday 구성 | Microsoft Docs"
description: "자세한 내용은 방법 toouse Active Directory와 Azure Active Directory에 대 한 id 데이터의 원본으로 Workday 합니다."
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
ms.openlocfilehash: d4eb3237b8fe7614606c58b39fbefcb44f4060fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workday-for-automatic-user-provisioning-with-on-premises-active-directory-and-azure-active-directory"></a><span data-ttu-id="992d5-103">자습서: 온-프레미스 Active Directory 및 Azure Active Directory를 사용하여 사용자를 자동으로 프로비전하도록 Workday 구성</span><span class="sxs-lookup"><span data-stu-id="992d5-103">Tutorial: Configure Workday for automatic user provisioning with on-premises Active Directory and Azure Active Directory</span></span>
<span data-ttu-id="992d5-104">hello이이 자습서의 일부 특성 tooWorkday의 선택적 쓰기 저장으로 작업일에서 tooperform tooimport 사용자는 Active Directory 및 Azure Active Directory에 필요한 단계를 hello tooshow가 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-104">hello objective of this tutorial is tooshow you hello steps you need tooperform tooimport people from Workday into both Active Directory and Azure Active Directory, with optional writeback of some attributes tooWorkday.</span></span> 



## <a name="overview"></a><span data-ttu-id="992d5-105">개요</span><span class="sxs-lookup"><span data-stu-id="992d5-105">Overview</span></span>

<span data-ttu-id="992d5-106">hello [서비스 프로 비전 하는 Azure Active Directory 사용자](active-directory-saas-app-provisioning.md) hello와 통합 되어 [Workday 인적 자원 API](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html) 의 순서로 tooprovision 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-106">hello [Azure Active Directory user provisioning service](active-directory-saas-app-provisioning.md) integrates with hello [Workday Human Resources API](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html) in order tooprovision user accounts.</span></span> <span data-ttu-id="992d5-107">Azure AD 사용자 프로 비전 워크플로가 다음이 연결 tooenable hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-107">Azure AD uses this connection tooenable hello following user provisioning workflows:</span></span>

* <span data-ttu-id="992d5-108">**사용자가 tooActive 디렉터리를 프로 비전** -하나 이상의 Active Directory 포리스트를 선택한 유형의 작업일에서 사용자가 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-108">**Provisioning users tooActive Directory** - Synchronize selected sets of users from Workday into one or more Active Directory forests.</span></span> 

* <span data-ttu-id="992d5-109">**클라우드 전용 사용자 tooAzure Active Directory 프로비저닝** -하이브리드 사용자에 게는 Active Directory 및 Azure Active Directory에 존재 hello 후자 사용 하 여 프로 비전 할 수 [AAD Connect](connect/active-directory-aadconnect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-109">**Provisioning cloud-only users tooAzure Active Directory** - Hybrid users who exist in both Active Directory and Azure Active Directory can be provisioned into hello latter using [AAD Connect](connect/active-directory-aadconnect.md).</span></span> <span data-ttu-id="992d5-110">그러나 클라우드 전용 사용자가 서비스를 프로 비전 하는 Azure AD 사용자 hello tooAzure Active Directory를 사용 하 여 Workday에서 직접 프로 비전 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-110">However, users that are cloud-only can be provisioned directly from Workday tooAzure Active Directory using hello Azure AD user provisioning service.</span></span>

* <span data-ttu-id="992d5-111">**전자 메일의 쓰기 저장 주소 tooWorkday** -서비스를 프로 비전 하는 hello Azure AD 사용자 Azure AD 사용자 특성 백 tooWorkday, 예: hello 전자 메일 주소를 선택 합니다. 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-111">**Writeback of email addresses tooWorkday** - hello Azure AD user provisioning service can write selected Azure AD user attributes back tooWorkday, such as hello email address.</span></span>

### <a name="scenarios-covered"></a><span data-ttu-id="992d5-112">포함되는 시나리오</span><span class="sxs-lookup"><span data-stu-id="992d5-112">Scenarios covered</span></span>

<span data-ttu-id="992d5-113">hello Workday 사용자 서비스를 프로 비전 하는 hello Azure AD 사용자가 지원 되는 워크플로 프로 비전 hello 다음 인적 자원 및 id 수명 주기 관리 시나리오의 자동화를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-113">hello Workday user provisioning workflows supported by hello Azure AD user provisioning service enables automation of hello following human resources and identity lifecycle management scenarios:</span></span>

* <span data-ttu-id="992d5-114">**새 직원을 채용** -새 직원 tooWorkday를 추가 하는 경우 사용자 계정을 자동으로 만들어집니다 Active Directory, Azure Active Directory와 선택적으로 Office 365 및 [Azure AD에서 지 원하는 다른 SaaS 응용 프로그램 ](active-directory-saas-app-provisioning.md), hello 전자 메일 주소 tooWorkday 뒷면 쓰기입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-114">**Hiring new employees** - When a new employee is added tooWorkday, a user account will be automatically created in Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](active-directory-saas-app-provisioning.md), with write back of hello email address tooWorkday.</span></span>

* <span data-ttu-id="992d5-115">**직원 특성 및 프로필 업데이트** - Workday에서 이름, 직함, 관리자 등의 직원 레코드가 업데이트되면 Active Directory, Azure Active Directory 그리고 선택적으로 Office 365 및 [Azure AD에서 지원하는 기타 SaaS 응용 프로그램](active-directory-saas-app-provisioning.md)에서 해당 사용자 계정이 자동으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-115">**Employee attribute and profile updates** - When an employee record is updated in Workday (such as their name, title, or manager), their user account will be automatically updated in Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](active-directory-saas-app-provisioning.md).</span></span>

* <span data-ttu-id="992d5-116">**직원 퇴사** - Workday에서 직원이 퇴사하면 Active Directory, Azure Active Directory 그리고 선택적으로 Office 365 및 [Azure AD에서 지원하는 기타 SaaS 응용 프로그램](active-directory-saas-app-provisioning.md)에서 해당 사용자 계정이 자동으로 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-116">**Employee terminations** - When an employee is terminated in Workday, their user account is automatically disabled in Active Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](active-directory-saas-app-provisioning.md).</span></span>

* <span data-ttu-id="992d5-117">**직원 채용 다시** -직원이 Workday에서 rehired 되 면 이전 계정으로 자동으로 다시 활성화할 수 있습니다 (기본 설정)에 따라 다시 프로 비전된 tooActive 디렉터리, Azure Active Directory 및 필요에 따라 Office 365 및 또는[Azure AD에서 지 원하는 다른 SaaS 응용 프로그램](active-directory-saas-app-provisioning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-117">**Employee re-hires** - When an employee is rehired in Workday, their old account can be automatically reactivated or re-provisioned (depending on your preference) tooActive Directory, Azure Active Directory, and optionally Office 365 and [other SaaS applications supported by Azure AD](active-directory-saas-app-provisioning.md).</span></span>


## <a name="planning-your-solution"></a><span data-ttu-id="992d5-118">솔루션 계획</span><span class="sxs-lookup"><span data-stu-id="992d5-118">Planning your solution</span></span>

<span data-ttu-id="992d5-119">Workday의 통합을 시작 하기 전에 아래과 읽기 hello 방법에 대 한 지침을 따르면 hello 필수 구성 요소를 확인, 현재 Active Directory 아키텍처와 사용자에 게 요구를 프로 비전 hello 활성 Azure에서 제공 하는 솔루션이 toomatch 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-119">Before beginning your Workday integration, check hello prerequisites below and read hello following guidance on how toomatch your current Active Directory architecture and user provisioning requirements with hello solution(s) provided by Azure Active Directory.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="992d5-120">필수 조건</span><span class="sxs-lookup"><span data-stu-id="992d5-120">Prerequisites</span></span>

<span data-ttu-id="992d5-121">이 자습서에 설명 된 hello 시나리오 다음 항목 hello 이미 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-121">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="992d5-122">전역 관리자 액세스 권한이 있는 유효한 Azure AD Premium P1 구독</span><span class="sxs-lookup"><span data-stu-id="992d5-122">A valid Azure AD Premium P1 subscription with global administrator access</span></span>
* <span data-ttu-id="992d5-123">테스트 및 통합을 위한 Workday 구현 테넌트</span><span class="sxs-lookup"><span data-stu-id="992d5-123">A Workday implementation tenant for testing and integration purposes</span></span>
* <span data-ttu-id="992d5-124">Workday toocreate 시스템 통합 사용자에에서 대 한 관리자 권한이 및 테스트 목적으로 확인 tootest 직원 데이터를 변경 합니다</span><span class="sxs-lookup"><span data-stu-id="992d5-124">Administrator permissions in Workday toocreate a system integration user, and make changes tootest employee data for testing purposes</span></span>
* <span data-ttu-id="992d5-125">사용자 프로 비전 tooActive 디렉터리, 2012 또는 큰 Windows 서비스를 실행 하는 도메인에 가입 된 서버는 필요한 toohost hello [온-프레미스 동기화 에이전트](https://go.microsoft.com/fwlink/?linkid=847801)</span><span class="sxs-lookup"><span data-stu-id="992d5-125">For user provisioning tooActive Directory, a domain-joined server running Windows Service 2012 or greater is required toohost hello [on-premises synchronization agent](https://go.microsoft.com/fwlink/?linkid=847801)</span></span>
* <span data-ttu-id="992d5-126">Active Directory와 Azure AD 간의 동기화를 위한 [Azure AD Connect](connect/active-directory-aadconnect.md)</span><span class="sxs-lookup"><span data-stu-id="992d5-126">[Azure AD Connect](connect/active-directory-aadconnect.md) for synchronizing between Active Directory and Azure AD</span></span>

> [!NOTE]
> <span data-ttu-id="992d5-127">유럽의 Azure AD 테 넌 트 있으면 hello를 참조 하십시오 [알려진 문제](#known-issues) 아래 섹션.</span><span class="sxs-lookup"><span data-stu-id="992d5-127">If your Azure AD tenant is located in Europe, please see hello [Known issues](#known-issues) section below.</span></span>


### <a name="solution-architecture"></a><span data-ttu-id="992d5-128">솔루션 아키텍처</span><span class="sxs-lookup"><span data-stu-id="992d5-128">Solution architecture</span></span>

<span data-ttu-id="992d5-129">Azure AD에서는 다양 한 프로 비전 및 id 수명 주기 관리 Workday tooActive 디렉터리를 Azure AD에서 SaaS 응용 프로그램에서에서와 같거나 이보다 뒤 해결 커넥터 toohelp 프로 비전을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-129">Azure AD provides a rich set of provisioning connectors toohelp you solve provisioning and identity lifecycle management from Workday tooActive Directory, Azure AD, SaaS apps, and beyond.</span></span> <span data-ttu-id="992d5-130">사용 되는 기능 하 고 hello 솔루션을 설정 하는 방법을 조직 환경 및 요구 사항에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-130">Which features you will use and how you set up hello solution will vary depending on your organization's environment and requirements.</span></span> <span data-ttu-id="992d5-131">첫 번째 단계로, hello 다음의 수가 존재 하 고 조직에 배포 된의 재고를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-131">As a first step, take stock of how many of hello following are present and deployed in your organization:</span></span>

* <span data-ttu-id="992d5-132">Active Directory 포리스트를 몇 개나 사용하고 있나요?</span><span class="sxs-lookup"><span data-stu-id="992d5-132">How many Active Directory Forests are in use?</span></span>
* <span data-ttu-id="992d5-133">Active Directory 도메인을 몇 개나 사용하고 있나요?</span><span class="sxs-lookup"><span data-stu-id="992d5-133">How many Active Directory Domains are in use?</span></span>
* <span data-ttu-id="992d5-134">Active Directory OU(조직 구성 단위)를 몇 개나 사용하고 있나요?</span><span class="sxs-lookup"><span data-stu-id="992d5-134">How many Active Directory Organizational Units (OUs) are in use?</span></span>
* <span data-ttu-id="992d5-135">Azure Active Directory 테넌트를 몇 개나 사용하고 있나요?</span><span class="sxs-lookup"><span data-stu-id="992d5-135">How many Azure Active Directory tenants are in use?</span></span>
* <span data-ttu-id="992d5-136">사용자를 프로 비전 toobe tooboth Active Directory와 Azure Active Directory (예: "하이브리드" 사용자)에 게 있나요?</span><span class="sxs-lookup"><span data-stu-id="992d5-136">Are there users who need toobe provisioned tooboth Active Directory and Azure Active Directory (e.g. "hybrid" users)?</span></span>
* <span data-ttu-id="992d5-137">Active Directory 사용자를 프로 비전 toobe tooAzure 하지만 Active Directory 없습니다 (예: "클라우드 전용" 사용자의 경우) 해야 하는 사용자가 있습니까?</span><span class="sxs-lookup"><span data-stu-id="992d5-137">Are there users who need toobe provisioned tooAzure Active Directory, but not Active Directory (e.g. "cloud-only" users)?</span></span>
* <span data-ttu-id="992d5-138">사용자 전자 메일 주소를 다시 tooWorkday 기록 toobe 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="992d5-138">Do user email addresses need toobe written back tooWorkday?</span></span>

<span data-ttu-id="992d5-139">대답 toothese 질문을 만든 후 다음 hello 설명서 아래에서 배포를 프로 비전 하면 업무를 계획할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-139">Once you have answers toothese questions, you can plan your Workday provisioning deployment by following hello guidance below.</span></span>

#### <a name="using-provisioning-connector-apps"></a><span data-ttu-id="992d5-140">프로비전 커넥터 앱 사용</span><span class="sxs-lookup"><span data-stu-id="992d5-140">Using provisioning connector apps</span></span>

<span data-ttu-id="992d5-141">Azure Active Directory는 Workday용으로 사전 통합된 프로비전 커넥터와 수많은 기타 SaaS 응용 프로그램을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-141">Azure Active Directory supports pre-integrated provisioning connectors for Workday and a large number of other SaaS applications.</span></span> 

<span data-ttu-id="992d5-142">하나의 프로비저닝 커넥터 단일 원본 시스템의 hello API와 상호 작용 하 고 프로 비전 데이터 tooa 단일 대상 시스템을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-142">A single provisioning connector interfaces with hello API of a single source system, and helps provision data tooa single target system.</span></span> <span data-ttu-id="992d5-143">대부분의 프로 비전 커넥터를 지 원하는 Azure AD는 단일 소스 및 대상 시스템 (예: Azure AD tooServiceNow) 수 있으며 설치 hello 앱을 추가 하기만 하면 문제의 hello Azure AD 앱 갤러리 (예: ServiceNow)에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-143">Most provisioning connectors that Azure AD supports are for a single source and target system (e.g. Azure AD tooServiceNow), and can be setup by simply adding hello app in question from hello Azure AD app gallery (e.g. ServiceNow).</span></span> 

<span data-ttu-id="992d5-144">Azure AD의 프로비전 커넥터 인스턴스와 앱 인스턴스는 일대일 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-144">There is a one-to-one relationship between provisioning connector instances and app instances in Azure AD:</span></span>

| <span data-ttu-id="992d5-145">원본 시스템</span><span class="sxs-lookup"><span data-stu-id="992d5-145">Source System</span></span> | <span data-ttu-id="992d5-146">대상 시스템</span><span class="sxs-lookup"><span data-stu-id="992d5-146">Target System</span></span> |
| ---------- | ---------- | 
| <span data-ttu-id="992d5-147">Azure AD 테넌트</span><span class="sxs-lookup"><span data-stu-id="992d5-147">Azure AD tenant</span></span> | <span data-ttu-id="992d5-148">SaaS 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="992d5-148">SaaS application</span></span> |


<span data-ttu-id="992d5-149">그러나 Workday 및 Active Directory를 사용할 때는 간주 여러 소스 및 대상 시스템 toobe 가지.</span><span class="sxs-lookup"><span data-stu-id="992d5-149">However, when working with Workday and Active Directory, there are multiple source and target systems toobe considered:</span></span>

| <span data-ttu-id="992d5-150">원본 시스템</span><span class="sxs-lookup"><span data-stu-id="992d5-150">Source System</span></span> | <span data-ttu-id="992d5-151">대상 시스템</span><span class="sxs-lookup"><span data-stu-id="992d5-151">Target System</span></span> | <span data-ttu-id="992d5-152">참고 사항</span><span class="sxs-lookup"><span data-stu-id="992d5-152">Notes</span></span> |
| ---------- | ---------- | ---------- |
| <span data-ttu-id="992d5-153">Workday</span><span class="sxs-lookup"><span data-stu-id="992d5-153">Workday</span></span> | <span data-ttu-id="992d5-154">Active Directory 포리스트</span><span class="sxs-lookup"><span data-stu-id="992d5-154">Active Directory Forest</span></span> | <span data-ttu-id="992d5-155">각 포리스트는 고유한 대상 시스템으로 처리됨</span><span class="sxs-lookup"><span data-stu-id="992d5-155">Each forest is treated as a distinct target system</span></span> |
| <span data-ttu-id="992d5-156">Workday</span><span class="sxs-lookup"><span data-stu-id="992d5-156">Workday</span></span> | <span data-ttu-id="992d5-157">Azure AD 테넌트</span><span class="sxs-lookup"><span data-stu-id="992d5-157">Azure AD tenant</span></span> | <span data-ttu-id="992d5-158">클라우드 전용 사용자에 필요한 경우</span><span class="sxs-lookup"><span data-stu-id="992d5-158">As required for cloud-only users</span></span> |
| <span data-ttu-id="992d5-159">Active Directory 포리스트</span><span class="sxs-lookup"><span data-stu-id="992d5-159">Active Directory Forest</span></span> | <span data-ttu-id="992d5-160">Azure AD 테넌트</span><span class="sxs-lookup"><span data-stu-id="992d5-160">Azure AD tenant</span></span> | <span data-ttu-id="992d5-161">이 흐름은 현재 AAD Connect에서 처리</span><span class="sxs-lookup"><span data-stu-id="992d5-161">This flow is handled by AAD Connect today</span></span> |
| <span data-ttu-id="992d5-162">Azure AD 테넌트</span><span class="sxs-lookup"><span data-stu-id="992d5-162">Azure AD tenant</span></span> | <span data-ttu-id="992d5-163">Workday</span><span class="sxs-lookup"><span data-stu-id="992d5-163">Workday</span></span> | <span data-ttu-id="992d5-164">이메일 주소의 쓰기 저장</span><span class="sxs-lookup"><span data-stu-id="992d5-164">For writeback of email addresses</span></span> |

<span data-ttu-id="992d5-165">toofacilitate 이러한 여러 개의 워크플로 toomultiple 소스 및 대상 시스템에 Azure AD hello Azure AD 앱 갤러리에서 추가할 수 있는 여러 프로비저닝 커넥터 앱을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-165">toofacilitate these multiple workflows toomultiple source and target systems, Azure AD provides multiple provisioning connector apps that you can add from hello Azure AD app gallery:</span></span>

![AAD 앱 갤러리](./media/active-directory-saas-workday-inbound-tutorial/WD_Gallery.PNG)

* <span data-ttu-id="992d5-167">**디렉터리 프로비저닝이 workday tooActive** -이 앱 Workday tooa 단일 Active Directory 포리스트의 사용자 계정 프로비저닝을 용이 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-167">**Workday tooActive Directory Provisioning** - This app facilitates user account provisioning from Workday tooa single Active Directory forest.</span></span> <span data-ttu-id="992d5-168">여러 포리스트에 있는 경우에 tooprovision 필요한 각 Active Directory 포리스트에 대 한 hello Azure AD 앱 갤러리에서이 응용 프로그램의 인스턴스 하나를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-168">If you have multiple forests, you can add one instance of this app from hello Azure AD app gallery for each Active Directory forest you need tooprovision to.</span></span>

* <span data-ttu-id="992d5-169">**Workday tooAzure AD 프로 비전** -동안 AAD Connect는 hello 도구 사용된 toosynchronize Active Directory 사용자 tooAzure Active Directory 되어야 하는이 앱에 사용 되는 toofacilitate 될 수 있습니다 Workday tooa 단일에서 클라우드 전용 사용자 프로 비전 Azure Active Directory 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-169">**Workday tooAzure AD Provisioning** - While AAD Connect is hello tool that should be used toosynchronize Active Directory users tooAzure Active Directory, this app can be used toofacilitate provisioning of cloud-only users from Workday tooa single Azure Active Directory tenant.</span></span>

* <span data-ttu-id="992d5-170">**Workday 쓰기 저장** -이 앱에서 Azure Active Directory tooWorkday 사용자의 전자 메일 주소의 쓰기 저장을 용이 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-170">**Workday Writeback** - This app facilitates writeback of user's email addresses from Azure Active Directory tooWorkday.</span></span>

> [!TIP]
> <span data-ttu-id="992d5-171">hello 일반 "Workday" 응용 프로그램은 Azure Active Directory와 Workday에서 single sign-on을 설정 하기 위한 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-171">hello regular "Workday" app is used for setting up single sign-on between Workday and Azure Active Directory.</span></span> 

<span data-ttu-id="992d5-172">어떻게 tooset 및 이러한 특별 한 구성 섹션에서는이 자습서의 나머지 hello의 hello 주제는 커넥터 응용 프로그램을 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-172">How tooset up and configure these special provisioning connector apps is hello subject of hello remaining sections of this tutorial.</span></span> <span data-ttu-id="992d5-173">테 넌 트 환경에서 되 tooconfigure, tooprovision 개수 Active Directory 포리스트 및 Azure AD 필요는 시스템에 따라 달라 집니다 선택 하는 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-173">Which apps you choose tooconfigure will depend on which systems you need tooprovision to, and how many Active Directory Forests and Azure AD tenants are in your environment.</span></span>

![개요](./media/active-directory-saas-workday-inbound-tutorial/WD_Overview.PNG)

## <a name="configure-a-system-integration-user-in-workday"></a><span data-ttu-id="992d5-175">Workday에서 시스템 통합 사용자 구성</span><span class="sxs-lookup"><span data-stu-id="992d5-175">Configure a system integration user in Workday</span></span>
<span data-ttu-id="992d5-176">모든 hello Workday 프로비저닝 커넥터의 일반적인 요구 사항은 Workday 시스템 통합 계정 tooconnect toohello Workday 인적 자원 API에 대 한 자격 증명이 필요한입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-176">A common requirement of all hello Workday provisioning connectors is they require credentials for a Workday system integration account tooconnect toohello Workday Human Resources API.</span></span> <span data-ttu-id="992d5-177">이 섹션에서는 Workday의 toocreate 시스템 통합을 고려 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-177">This section describes how toocreate a system integrator account in Workday.</span></span>

> [!NOTE]
> <span data-ttu-id="992d5-178">가능한 toobypass이이 절차 이며 대신 hello 시스템 통합 계정으로 Workday 전역 관리자 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-178">It is possible toobypass this procedure and instead use a Workday global administrator account as hello system integration account.</span></span> <span data-ttu-id="992d5-179">이 방법이 데모에서는 제대로 작동할 수 있지만 프로덕션 배포에는 권장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-179">This may work fine for demos, but is not recommended for production deployments.</span></span>

### <a name="create-an-integration-system-user"></a><span data-ttu-id="992d5-180">통합 시스템 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="992d5-180">Create an integration system user</span></span>

<span data-ttu-id="992d5-181">**통합 시스템 사용자 toocreate:**</span><span class="sxs-lookup"><span data-stu-id="992d5-181">**toocreate an integration system user:**</span></span>

1. <span data-ttu-id="992d5-182">Administrator 계정을 사용하여 Workday 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-182">Sign into your Workday tenant using an administrator account.</span></span> <span data-ttu-id="992d5-183">Hello에 **Workday Workbench**, 입력 hello 검색 상자에 사용자를 만들고 클릭 **통합 시스템 사용자 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-183">In hello **Workday Workbench**, enter create user in hello search box, and then click **Create Integration System User**.</span></span> 
   
    <span data-ttu-id="992d5-184">![사용자 만들기](./media/active-directory-saas-workday-inbound-tutorial/IC750979.png "사용자 만들기")</span><span class="sxs-lookup"><span data-stu-id="992d5-184">![Create user](./media/active-directory-saas-workday-inbound-tutorial/IC750979.png "Create user")</span></span>
2. <span data-ttu-id="992d5-185">전체 hello **통합 시스템 사용자 만들기** 새 통합 시스템 사용자에 대 한 사용자 이름 및 암호를 제공 하 여 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-185">Complete hello **Create Integration System User** task by supplying a user name and password for a new Integration System User.</span></span>  
 * <span data-ttu-id="992d5-186">Hello 둡니다 **다음 로그인 시 새 암호 필요** 옵션을 선택 하지 않는 경우이 사용자에 프로그래밍 방식으로 로그인 때문에 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-186">Leave hello **Require New Password at Next Sign In** option unchecked, because this user will be logging on programmatically.</span></span> 
 * <span data-ttu-id="992d5-187">Hello 둡니다 **세션 제한 시간 (분)** 0의 기본 값을 갖는 것을 방지할 hello 사용자 세션이 중간 초과 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-187">Leave hello **Session Timeout Minutes** with its default value of 0, which will prevent hello user’s sessions from timing out prematurely.</span></span> 
   
    <span data-ttu-id="992d5-188">![통합 시스템 사용자 만들기](./media/active-directory-saas-workday-inbound-tutorial/IC750980.png "통합 시스템 사용자 만들기")</span><span class="sxs-lookup"><span data-stu-id="992d5-188">![Create Integration System User](./media/active-directory-saas-workday-inbound-tutorial/IC750980.png "Create Integration System User")</span></span>

### <a name="create-a-security-group"></a><span data-ttu-id="992d5-189">보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="992d5-189">Create a security group</span></span>
<span data-ttu-id="992d5-190">제한 없는 통합 시스템 보안 그룹 toocreate 필요 하 고이 정보를 사용자 tooit hello를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-190">You need toocreate an unconstrained integration system security group and assign hello user tooit.</span></span>

<span data-ttu-id="992d5-191">**toocreate 보안 그룹:**</span><span class="sxs-lookup"><span data-stu-id="992d5-191">**toocreate a security group:**</span></span>

1. <span data-ttu-id="992d5-192">입력 hello 검색 상자에 보안 그룹을 만들고 클릭 **보안 그룹 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-192">Enter create security group in hello search box, and then click **Create Security Group**.</span></span> 
   
    <span data-ttu-id="992d5-193">![보안 그룹 만들기](./media/active-directory-saas-workday-inbound-tutorial/IC750981.png "보안 그룹 만들기")</span><span class="sxs-lookup"><span data-stu-id="992d5-193">![CreateSecurity Group](./media/active-directory-saas-workday-inbound-tutorial/IC750981.png "CreateSecurity Group")</span></span>
2. <span data-ttu-id="992d5-194">전체 hello **보안 그룹 만들기** 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-194">Complete hello **Create Security Group** task.</span></span>  
3. <span data-ttu-id="992d5-195">통합 시스템 보안 그룹 선택-hello에서 제약 없이 **종류의 테 넌 트 보안 그룹** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-195">Select Integration System Security Group—Unconstrained from hello **Type of Tenanted Security Group** dropdown.</span></span>
4. <span data-ttu-id="992d5-196">추가 될 멤버가 명시적으로 보안 그룹 toowhich를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-196">Create a security group toowhich members will be explicitly added.</span></span> 
   
    <span data-ttu-id="992d5-197">![보안 그룹 만들기](./media/active-directory-saas-workday-inbound-tutorial/IC750982.png "보안 그룹 만들기")</span><span class="sxs-lookup"><span data-stu-id="992d5-197">![CreateSecurity Group](./media/active-directory-saas-workday-inbound-tutorial/IC750982.png "CreateSecurity Group")</span></span>

### <a name="assign-hello-integration-system-user-toohello-security-group"></a><span data-ttu-id="992d5-198">Hello 통합 시스템 사용자 toohello 보안 그룹에 할당</span><span class="sxs-lookup"><span data-stu-id="992d5-198">Assign hello integration system user toohello security group</span></span>

<span data-ttu-id="992d5-199">**tooassign hello 통합 시스템 사용자:**</span><span class="sxs-lookup"><span data-stu-id="992d5-199">**tooassign hello integration system user:**</span></span>

1. <span data-ttu-id="992d5-200">보안 그룹 편집 hello 검색 상자에 입력 한 다음 클릭 **보안 그룹 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-200">Enter edit security group in hello search box, and then click **Edit Security Group**.</span></span> 
   
    <span data-ttu-id="992d5-201">![보안 그룹 편집](./media/active-directory-saas-workday-inbound-tutorial/IC750983.png "보안 그룹 편집")</span><span class="sxs-lookup"><span data-stu-id="992d5-201">![Edit Security Group](./media/active-directory-saas-workday-inbound-tutorial/IC750983.png "Edit Security Group")</span></span>
2. <span data-ttu-id="992d5-202">를 검색 하 고 이름으로 hello 새 통합 보안 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-202">Search for, and select hello new integration security group by name.</span></span> 
   
    <span data-ttu-id="992d5-203">![보안 그룹 편집](./media/active-directory-saas-workday-inbound-tutorial/IC750984.png "보안 그룹 편집")</span><span class="sxs-lookup"><span data-stu-id="992d5-203">![Edit Security Group](./media/active-directory-saas-workday-inbound-tutorial/IC750984.png "Edit Security Group")</span></span>
3. <span data-ttu-id="992d5-204">Hello 새 통합 시스템 사용자 toohello 새 보안 그룹을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-204">Add hello new integration system user toohello new security group.</span></span> 
   
    <span data-ttu-id="992d5-205">![시스템 보안 그룹](./media/active-directory-saas-workday-inbound-tutorial/IC750985.png "시스템 보안 그룹")</span><span class="sxs-lookup"><span data-stu-id="992d5-205">![System Security Group](./media/active-directory-saas-workday-inbound-tutorial/IC750985.png "System Security Group")</span></span>  

### <a name="configure-security-group-options"></a><span data-ttu-id="992d5-206">보안 그룹 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="992d5-206">Configure security group options</span></span>
<span data-ttu-id="992d5-207">이 단계에서는 있습니다 toohello 새 보안 그룹에 권한을 부여 **가져오기** 및 **배치** hello 다음 도메인 보안 정책으로 보호 되는 hello 개체에 대 한 작업:</span><span class="sxs-lookup"><span data-stu-id="992d5-207">In this step, you grant toohello new security group permissions for **Get** and **Put** operations on hello objects secured by hello following domain security policies:</span></span>

* <span data-ttu-id="992d5-208">외부 계정 프로비저닝</span><span class="sxs-lookup"><span data-stu-id="992d5-208">External Account Provisioning</span></span>
* <span data-ttu-id="992d5-209">작업자 데이터: 공용 작업자 보고서</span><span class="sxs-lookup"><span data-stu-id="992d5-209">Worker Data: Public Worker Reports</span></span>
* <span data-ttu-id="992d5-210">작업자 데이터: 모든 위치</span><span class="sxs-lookup"><span data-stu-id="992d5-210">Worker Data: All Positions</span></span>
* <span data-ttu-id="992d5-211">작업자 데이터: 현재 인력 관리 정보</span><span class="sxs-lookup"><span data-stu-id="992d5-211">Worker Data: Current Staffing Information</span></span>
* <span data-ttu-id="992d5-212">작업자 데이터: 작업자 프로필 직함</span><span class="sxs-lookup"><span data-stu-id="992d5-212">Worker Data: Business Title on Worker Profile</span></span>

<span data-ttu-id="992d5-213">**tooconfigure 보안 그룹 옵션:**</span><span class="sxs-lookup"><span data-stu-id="992d5-213">**tooconfigure security group options:**</span></span>

1. <span data-ttu-id="992d5-214">도메인 보안 정책을 hello 검색 상자에 입력 한 다음 링크를 클릭 hello **기능 영역에 대 한 도메인 보안 정책**합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-214">Enter domain security policies in hello search box, and then click on hello link **Domain Security Policies for Functional Area**.</span></span>  
   
    <span data-ttu-id="992d5-215">![도메인 보안 정책](./media/active-directory-saas-workday-inbound-tutorial/IC750986.png "도메인 보안 정책")</span><span class="sxs-lookup"><span data-stu-id="992d5-215">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750986.png "Domain Security Policies")</span></span>  
2. <span data-ttu-id="992d5-216">시스템 및 선택 hello에 대 한 검색 **시스템** 기능 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-216">Search for system and select hello **System** functional area.</span></span>  <span data-ttu-id="992d5-217">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-217">Click **OK**.</span></span>  
   
    <span data-ttu-id="992d5-218">![도메인 보안 정책](./media/active-directory-saas-workday-inbound-tutorial/IC750987.png "도메인 보안 정책")</span><span class="sxs-lookup"><span data-stu-id="992d5-218">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750987.png "Domain Security Policies")</span></span>  
3. <span data-ttu-id="992d5-219">Hello hello 시스템 기능 영역에 대 한 보안 정책 목록에서 확장 **보안 관리** hello 도메인 보안 정책을 선택 하 고 **외부 계정 프로 비전**합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-219">In hello list of security policies for hello System functional area, expand **Security Administration** and select hello domain security policy **External Account Provisioning**.</span></span>  
   
    <span data-ttu-id="992d5-220">![도메인 보안 정책](./media/active-directory-saas-workday-inbound-tutorial/IC750988.png "도메인 보안 정책")</span><span class="sxs-lookup"><span data-stu-id="992d5-220">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750988.png "Domain Security Policies")</span></span>  
4. <span data-ttu-id="992d5-221">클릭 **사용 권한 편집**를 선택한 후 hello **사용 권한 편집**대화 상자 페이지에서 hello 새 보안 그룹 toohello 목록으로 보안 그룹의 추가 **가져오기** 및 **배치** 통합 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="992d5-221">Click **Edit Permissions**, and then, on hello **Edit Permissions**dialog page, add hello new security group toohello list of security groups with **Get** and **Put** integration permissions.</span></span> 
   
    <span data-ttu-id="992d5-222">![사용 권한 편집](./media/active-directory-saas-workday-inbound-tutorial/IC750989.png "사용 권한 편집")</span><span class="sxs-lookup"><span data-stu-id="992d5-222">![Edit Permission](./media/active-directory-saas-workday-inbound-tutorial/IC750989.png "Edit Permission")</span></span>  
5. <span data-ttu-id="992d5-223">기능 영역을 선택 하기 위한 tooreturn toohello 화면 위의 1 단계와 검색 인력 선택 hello 반복 **인력 기능 영역** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-223">Repeat step 1 above tooreturn toohello screen for selecting functional areas, and this time, search for staffing, select hello **Staffing functional area** and click **OK**.</span></span>
   
    <span data-ttu-id="992d5-224">![도메인 보안 정책](./media/active-directory-saas-workday-inbound-tutorial/IC750990.png "도메인 보안 정책")</span><span class="sxs-lookup"><span data-stu-id="992d5-224">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750990.png "Domain Security Policies")</span></span>  
6. <span data-ttu-id="992d5-225">Hello hello 인력 기능 영역에 대 한 보안 정책 목록에서 확장 **작업자 데이터: 직원 배치** 및 보안 정책에 남아 있는이 각각에 대해 4 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-225">In hello list of security policies for hello Staffing functional area, expand **Worker Data: Staffing** and repeat step 4 above for each of these remaining security policies:</span></span>

   * <span data-ttu-id="992d5-226">작업자 데이터: 공용 작업자 보고서</span><span class="sxs-lookup"><span data-stu-id="992d5-226">Worker Data: Public Worker Reports</span></span>
   * <span data-ttu-id="992d5-227">작업자 데이터: 모든 위치</span><span class="sxs-lookup"><span data-stu-id="992d5-227">Worker Data: All Positions</span></span>
   * <span data-ttu-id="992d5-228">작업자 데이터: 현재 인력 관리 정보</span><span class="sxs-lookup"><span data-stu-id="992d5-228">Worker Data: Current Staffing Information</span></span>
   * <span data-ttu-id="992d5-229">작업자 데이터: 작업자 프로필 직함</span><span class="sxs-lookup"><span data-stu-id="992d5-229">Worker Data: Business Title on Worker Profile</span></span>
   
7. <span data-ttu-id="992d5-230">Tooreturn toohello 화면 선택 기능 영역에 대 한 위의 1 단계를 반복 하 고이 시간에 대 한 검색 **연락처 정보**, hello 인력 기능 영역을 선택 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-230">Repeat step 1, above, tooreturn toohello screen for selecting  functional areas, and this time, search for **Contact Information**,  select hello Staffing functional area, and click **OK**.</span></span>

8.  <span data-ttu-id="992d5-231">Hello hello 인력 기능 영역에 대 한 보안 정책 목록에서 확장 **작업자 데이터: 작업 연락처 정보**, 및 아래 hello 보안 정책에 대 한 위의 4 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-231">In hello list of security policies for hello Staffing functional area, expand **Worker Data: Work Contact Information**, and repeat step 4 above for hello security policies below:</span></span>

    * <span data-ttu-id="992d5-232">작업자 데이터: 업무용 메일</span><span class="sxs-lookup"><span data-stu-id="992d5-232">Worker Data: Work Email</span></span>

    <span data-ttu-id="992d5-233">![도메인 보안 정책](./media/active-directory-saas-workday-inbound-tutorial/IC750991.png "도메인 보안 정책")</span><span class="sxs-lookup"><span data-stu-id="992d5-233">![Domain Security Policies](./media/active-directory-saas-workday-inbound-tutorial/IC750991.png "Domain Security Policies")</span></span>  
    
### <a name="activate-security-policy-changes"></a><span data-ttu-id="992d5-234">보안 정책 변경 사항 활성화</span><span class="sxs-lookup"><span data-stu-id="992d5-234">Activate security policy changes</span></span>

<span data-ttu-id="992d5-235">**tooactivate 보안 정책 변경 내용:**</span><span class="sxs-lookup"><span data-stu-id="992d5-235">**tooactivate security policy changes:**</span></span>

1. <span data-ttu-id="992d5-236">입력 hello 검색 상자에 활성화 하 고 hello 링크를 클릭 한 다음 **보류 중인 보안 정책 변경 내용 활성화**합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-236">Enter activate in hello search box, and then click on hello link **Activate Pending Security Policy Changes**.</span></span> 
   
    <span data-ttu-id="992d5-237">![활성화](./media/active-directory-saas-workday-inbound-tutorial/IC750992.png "활성화")</span><span class="sxs-lookup"><span data-stu-id="992d5-237">![Activate](./media/active-directory-saas-workday-inbound-tutorial/IC750992.png "Activate")</span></span> 
2. <span data-ttu-id="992d5-238">보류 중인 보안 정책 변경 내용 활성화 감사할 목적에 대 한 설명을 입력 하 여 작업 하 고 클릭 한 다음 시작 hello **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-238">Begin hello Activate Pending Security Policy Changes task by entering a comment for auditing purposes, and then click **OK**.</span></span> 
   
    <span data-ttu-id="992d5-239">![보류 중인 보안 활성화](./media/active-directory-saas-workday-inbound-tutorial/IC750993.png "보류 중인 보안 활성화")</span><span class="sxs-lookup"><span data-stu-id="992d5-239">![Activate Pending Security](./media/active-directory-saas-workday-inbound-tutorial/IC750993.png "Activate Pending Security")</span></span>   
3. <span data-ttu-id="992d5-240">Hello hello 확인란을 선택 하 여 다음 화면에서 작업 완료 hello **확인**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-240">Complete hello task on hello next screen by checking hello checkbox **Confirm**, and then click **OK**.</span></span> 
   
    <span data-ttu-id="992d5-241">![보류 중인 보안 활성화](./media/active-directory-saas-workday-inbound-tutorial/IC750994.png "보류 중인 보안 활성화")</span><span class="sxs-lookup"><span data-stu-id="992d5-241">![Activate Pending Security](./media/active-directory-saas-workday-inbound-tutorial/IC750994.png "Activate Pending Security")</span></span>  

## <a name="configuring-user-provisioning-from-workday-tooactive-directory"></a><span data-ttu-id="992d5-242">Workday tooActive 디렉터리에서에서 사용자 프로비저닝 구성</span><span class="sxs-lookup"><span data-stu-id="992d5-242">Configuring user provisioning from Workday tooActive Directory</span></span>
<span data-ttu-id="992d5-243">이러한 지침 tooconfigure 사용자 계정 프로 비전 필요로 하는 Active Directory 포리스트 Workday tooeach에서 프로 비전을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-243">Follow these instructions tooconfigure user account provisioning from Workday tooeach Active Directory forest that you require provisioning to.</span></span>

### <a name="part-1-adding-hello-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a><span data-ttu-id="992d5-244">1 부: 커넥터 응용 프로그램을 프로 비전 하는 hello를 추가 하 고 hello 연결 tooWorkday 만들기</span><span class="sxs-lookup"><span data-stu-id="992d5-244">Part 1: Adding hello provisioning connector app and creating hello connection tooWorkday</span></span>

<span data-ttu-id="992d5-245">**tooconfigure Workday tooActive 디렉터리 프로비저닝이:**</span><span class="sxs-lookup"><span data-stu-id="992d5-245">**tooconfigure Workday tooActive Directory provisioning:**</span></span>

1.  <span data-ttu-id="992d5-246">너무 이동<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="992d5-246">Go too<https://portal.azure.com></span></span>

2.  <span data-ttu-id="992d5-247">Hello 왼쪽된 탐색 모음에서 선택 **Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="992d5-247">In hello left navigation bar, select **Azure Active Directory**</span></span>

3.  <span data-ttu-id="992d5-248">**엔터프라이즈 응용 프로그램**, **모든 응용 프로그램**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-248">Select **Enterprise Applications**, then **All Applications**.</span></span>

4.  <span data-ttu-id="992d5-249">선택 **응용 프로그램 추가**, 및 select hello **모든** 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-249">Select **Add an application**, and select hello **All** category.</span></span>

5.  <span data-ttu-id="992d5-250">검색할 **Workday에 프로 비전 tooActive 디렉터리**, hello 갤러리에서 해당 앱을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-250">Search for **Workday Provisioning tooActive Directory**, and add that app from hello gallery.</span></span>

6.  <span data-ttu-id="992d5-251">선택, hello 후 앱 추가 되 고 hello 앱 세부 정보 화면이 표시 **프로 비전**</span><span class="sxs-lookup"><span data-stu-id="992d5-251">After hello app is added and hello app details screen is shown, select **Provisioning**</span></span>

7.  <span data-ttu-id="992d5-252">변경 hello **프로 비전** **모드** 너무**자동**</span><span class="sxs-lookup"><span data-stu-id="992d5-252">Change hello **Provisioning** **Mode** too**Automatic**</span></span>

8.  <span data-ttu-id="992d5-253">전체 hello **관리자 자격 증명** 다음과 같은 섹션:</span><span class="sxs-lookup"><span data-stu-id="992d5-253">Complete hello **Admin Credentials** section as follows:</span></span>

   * <span data-ttu-id="992d5-254">**관리자 사용자 이름** – hello 테 넌 트 도메인 이름을 추가한 함께 hello hello Workday 통합 시스템 계정 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-254">**Admin Username** – Enter hello username of hello Workday integration system account, with hello tenant domain name appended.</span></span> <span data-ttu-id="992d5-255">**다음과 같은 형태여야 합니다. username@contoso4**</span><span class="sxs-lookup"><span data-stu-id="992d5-255">**Should look something like: username@contoso4**</span></span>

   * <span data-ttu-id="992d5-256">**관리자 암호 –** hello Workday 통합 시스템 계정의 hello 암호 입력</span><span class="sxs-lookup"><span data-stu-id="992d5-256">**Admin password –** Enter hello password of hello Workday    integration system account</span></span>

   * <span data-ttu-id="992d5-257">**테 넌 트 URL –** 테 넌 트에 대 한 hello URL toohello Workday 웹 서비스 끝점을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-257">**Tenant URL –** Enter hello URL toohello Workday web services endpoint for your tenant.</span></span> <span data-ttu-id="992d5-258">이 같아야 합니다: https://wd3-impl-services1.workday.com/ccx/service/contoso4, 여기서 contoso4 올바른 테 넌 트 이름으로 대체 되 고 wd3 impl hello 올바른 환경 문자열으로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-258">This should look like: https://wd3-impl-services1.workday.com/ccx/service/contoso4, where contoso4 is replaced with your correct tenant name and wd3-impl is replaced with hello correct environment string.</span></span>

   * <span data-ttu-id="992d5-259">**Active Directory 포리스트-** hello Get ADForest powershell commandlet에 의해 반환 된 Active Directory 포리스트 "Name" hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-259">**Active Directory Forest -** hello “Name” of your Active Directory forest, as returned by hello Get-ADForest powershell commandlet.</span></span> <span data-ttu-id="992d5-260">일반적으로 *contoso.com* 형태의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-260">This is typically a string like: *contoso.com*</span></span>

   * <span data-ttu-id="992d5-261">**Active Directory 컨테이너-** AD 포리스트에 있는 모든 사용자가 포함 된 hello 컨테이너 문자열을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-261">**Active Directory Container -** Enter hello container string that contains all users in your AD forest.</span></span> <span data-ttu-id="992d5-262">예: *OU=Standard Users,OU=Users,DC=contoso,DC=test*</span><span class="sxs-lookup"><span data-stu-id="992d5-262">Example: *OU=Standard Users,OU=Users,DC=contoso,DC=test*</span></span>

   * <span data-ttu-id="992d5-263">**알림 이메일 –** 이메일 주소를 입력하고 "오류가 발생하면 이메일 보내기" 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-263">**Notification Email –** Enter your email address, and check the    “send email if failure occurs” checkbox.</span></span>

   * <span data-ttu-id="992d5-264">Hello 클릭 **연결 테스트** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-264">Click hello **Test Connection** button.</span></span> <span data-ttu-id="992d5-265">Hello 연결 테스트에 성공 하면 클릭 hello **저장** hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-265">If hello connection test succeeds, click hello **Save** button at hello top.</span></span> <span data-ttu-id="992d5-266">실패 한 경우 hello Workday 자격 증명이 Workday에 유효한 지 다시 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="992d5-266">If it fails, double-check that hello Workday credentials are valid in Workday.</span></span> 

![Azure portal](./media/active-directory-saas-workday-inbound-tutorial/WD_1.PNG)

### <a name="part-2-configure-attribute-mappings"></a><span data-ttu-id="992d5-268">2부: 특성 매핑 구성</span><span class="sxs-lookup"><span data-stu-id="992d5-268">Part 2: Configure attribute mappings</span></span> 

<span data-ttu-id="992d5-269">이 섹션에서는 사용자 데이터가 Workday에서 Active Directory로 흐르는 방식을 구성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-269">In this section, you will configure how user data flows from Workday to Active Directory.</span></span>

1.  <span data-ttu-id="992d5-270">Hello 프로 비전 탭에서 **매핑**, 클릭 **Workday 작업자 동기화 tooOnPremises**합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-270">On hello Provisioning tab under **Mappings**, click **Synchronize Workday Workers tooOnPremises**.</span></span>

2.  <span data-ttu-id="992d5-271">Hello에 **소스 개체 범위** 필드에서 어떤 유형의 사용자가 Workday의 tooAD, 일련의 특성 기반 필터를 정의 하 여 프로 비전에 대 한 범위에 속해야 합니다. 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-271">In hello **Source Object Scope** field, you can select which sets of users in Workday should be in scope for provisioning tooAD, by defining a set of attribute-based filters.</span></span> <span data-ttu-id="992d5-272">hello 기본 범위는 "업무 시간에 모든 사용자".</span><span class="sxs-lookup"><span data-stu-id="992d5-272">hello default scope is “all users in Workday”.</span></span> <span data-ttu-id="992d5-273">예제 필터:</span><span class="sxs-lookup"><span data-stu-id="992d5-273">Example filters:</span></span>

   * <span data-ttu-id="992d5-274">예: 1000000 사이의 2000000 작업자 Id를 가진 toousers 범위</span><span class="sxs-lookup"><span data-stu-id="992d5-274">Example: Scope toousers with Worker IDs between 1000000 and    2000000</span></span>

      * <span data-ttu-id="992d5-275">특성: WorkerID</span><span class="sxs-lookup"><span data-stu-id="992d5-275">Attribute: WorkerID</span></span>

      * <span data-ttu-id="992d5-276">연산자: REGEX Match</span><span class="sxs-lookup"><span data-stu-id="992d5-276">Operator: REGEX Match</span></span>

      * <span data-ttu-id="992d5-277">값: (1[0-9][0-9][0-9][0-9][0-9][0-9])</span><span class="sxs-lookup"><span data-stu-id="992d5-277">Value: (1[0-9][0-9][0-9][0-9][0-9][0-9])</span></span>

   * <span data-ttu-id="992d5-278">예: 정규직 직원만 포함하고 비정규직 직원은 포함하지 않음</span><span class="sxs-lookup"><span data-stu-id="992d5-278">Example: Only employees and not contingent workers</span></span> 

      * <span data-ttu-id="992d5-279">특성: EmployeeID</span><span class="sxs-lookup"><span data-stu-id="992d5-279">Attribute: EmployeeID</span></span>

      * <span data-ttu-id="992d5-280">연산자: IS NOT NULL</span><span class="sxs-lookup"><span data-stu-id="992d5-280">Operator: IS NOT NULL</span></span>

3.  <span data-ttu-id="992d5-281">Hello에 **대상 개체 작업** 필드 어떤 작업이 Active Directory에 수행 하는 toobe 허용 전체적으로 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-281">In hello **Target Object Actions** field, you can globally filter what actions are allowed toobe performed on Active Directory.</span></span> <span data-ttu-id="992d5-282">**만들기** 및 **업데이트**가 가장 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-282">**Create** and **Update** are most common.</span></span>

4.  <span data-ttu-id="992d5-283">Hello에 **특성 매핑을** 섹션 특성 tooActive 디렉터리 특성을 매핑할 개별 업무 시간을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-283">In hello **Attribute mappings** section, you can define how individual Workday attributes map tooActive Directory attributes.</span></span>

5. <span data-ttu-id="992d5-284">기존 특성 매핑 tooupdate를 클릭 하거나 클릭 **새 매핑을 추가** hello 화면 tooadd 새 매핑 hello 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-284">Click on an existing attribute mapping tooupdate it, or click **Add new mapping** at hello bottom of hello screen tooadd new mappings.</span></span> <span data-ttu-id="992d5-285">개별 특성 매핑은 다음 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-285">An individual attribute mapping supports these properties:</span></span>

      * <span data-ttu-id="992d5-286">**매핑 유형**</span><span class="sxs-lookup"><span data-stu-id="992d5-286">**Mapping Type**</span></span>

         * <span data-ttu-id="992d5-287">**직접** – hello 변경 하지 않고 hello Workday 특성 toohello AD 특성의 값을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-287">**Direct** – Writes hello value of hello Workday attribute      toohello AD attribute, with no changes</span></span>

         * <span data-ttu-id="992d5-288">**상수** -hello AD 특성에 정적 상수 문자열 값을 기록</span><span class="sxs-lookup"><span data-stu-id="992d5-288">**Constant** - Write a static, constant string value to      hello AD attribute</span></span>

         * <span data-ttu-id="992d5-289">**식** – toowrite hello AD 특성에 하나 이상의 Workday 특성을 기반으로 사용자 지정 값을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-289">**Expression** – Allows you toowrite a custom value to hello AD attribute, based on one or more Workday attributes.</span></span> <span data-ttu-id="992d5-290">[자세한 내용은 식에 대한 이 문서를 참조하세요](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="992d5-290">[For more info, see this article on expressions](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>

      * <span data-ttu-id="992d5-291">**원본 특성** -작업일에서 hello 사용자 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-291">**Source attribute** - hello user attribute from Workday.</span></span>

      * <span data-ttu-id="992d5-292">**기본값** – 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-292">**Default value** – Optional.</span></span> <span data-ttu-id="992d5-293">Hello 원본 특성 값이 비어 있으면 hello 매핑이이 값 대신 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-293">If hello source attribute has an empty value, hello mapping will write this value instead.</span></span>
            <span data-ttu-id="992d5-294">가장 일반적인 구성은 빈 tooleave 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-294">Most common configuration is tooleave this blank.</span></span>

      * <span data-ttu-id="992d5-295">**대상 특성** – Active Directory의 사용자 특성 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-295">**Target attribute** – hello user attribute in Active     Directory.</span></span>

      * <span data-ttu-id="992d5-296">**이 특성을 사용 하 여 개체를 일치** 이 매핑을 사용할지 여부-toouniquely Workday와 Active Directory 간에 사용자를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-296">**Match objects using this attribute** – Whether or not this mapping should be used toouniquely identify users between Workday and Active Directory.</span></span> <span data-ttu-id="992d5-297">일반적으로 Active Directory의 hello 직원 ID 특성 중 하나에 매핑되는 Workday에 일반적으로 작업자 ID 필드에서 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-297">This is typically set on the Worker ID field for Workday, which is typically mapped to one of hello Employee ID attributes in Active Directory.</span></span>

      * <span data-ttu-id="992d5-298">**일치 우선 순위** – 여러 일치 특성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-298">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="992d5-299">일치 특성이 여러 개 있으면 이 필드에 정의된 순서대로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-299">When there are multiple, they are evaluated in the order defined by this field.</span></span> <span data-ttu-id="992d5-300">일치 항목이 발견되는 즉시 더 이상 일치 특성을 평가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-300">As soon as a match is found, no further matching attributes are evaluated.</span></span>

      * <span data-ttu-id="992d5-301">**이 매핑 적용**</span><span class="sxs-lookup"><span data-stu-id="992d5-301">**Apply this mapping**</span></span>
       
         * <span data-ttu-id="992d5-302">**항상** – 사용자 만들기 및 업데이트 작업 시 이 매핑을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-302">**Always** – Apply this mapping on both user creation      and update actions</span></span>

         * <span data-ttu-id="992d5-303">**만들기 작업 시에만** - 사용자 만들기 작업 시에만 이 매핑을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-303">**Only during creation** - Apply this mapping only on      user creation actions</span></span>

6. <span data-ttu-id="992d5-304">toosave 매핑을 클릭 **저장** hello 위쪽 특성 매핑 섹션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-304">toosave your mappings, click **Save** at hello top of the      Attribute Mapping section.</span></span>

![Azure portal](./media/active-directory-saas-workday-inbound-tutorial/WD_2.PNG)

<span data-ttu-id="992d5-306">**아래는 몇 가지 일반적인 식을 사용한 Workday와 Active Directory 간의 특성 매핑을 보여주는 예입니다.**</span><span class="sxs-lookup"><span data-stu-id="992d5-306">**Below are some example attribute mappings between Workday and Active Directory, with some common expressions**</span></span>

-   <span data-ttu-id="992d5-307">toohello parentDistinguishedName AD 특성을 매핑하는 hello 식을 사용 하는 특정 OU 특성을 기반으로 하나 이상의 Workday 소스 사용자 tooa tooprovision 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-307">hello expression that maps toohello parentDistinguishedName AD attribute can be used tooprovision a user tooa specific OU based on one or more Workday source attributes.</span></span> <span data-ttu-id="992d5-308">이 예에서는 Workday의 도시 데이터에 따라 사용자를 여러 OU에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-308">This example places users in different OUs depending on their city data in Workday.</span></span>

-   <span data-ttu-id="992d5-309">toohello AD userPrincipalName 특성을 매핑하는 hello 식의 UPN을 만들려면 firstName.LastName@contoso.com합니다. 또한 잘못된 특수 문자를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-309">hello expression that maps toohello userPrincipalName AD attribute create a UPN of firstName.LastName@contoso.com. It also replaces illegal special characters.</span></span>

-   [<span data-ttu-id="992d5-310">식을 쓰는 방법에 대한 설명서는 여기</span><span class="sxs-lookup"><span data-stu-id="992d5-310">There is documentation on writing expressions here</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)

  
| <span data-ttu-id="992d5-311">WORKDAY 특성</span><span class="sxs-lookup"><span data-stu-id="992d5-311">WORKDAY ATTRIBUTE</span></span> | <span data-ttu-id="992d5-312">ACTIVE DIRECTORY 특성</span><span class="sxs-lookup"><span data-stu-id="992d5-312">ACTIVE DIRECTORY ATTRIBUTE</span></span> |  <span data-ttu-id="992d5-313">ID 일치 여부</span><span class="sxs-lookup"><span data-stu-id="992d5-313">MATCHING ID?</span></span> | <span data-ttu-id="992d5-314">만들기/업데이트</span><span class="sxs-lookup"><span data-stu-id="992d5-314">CREATE / UPDATE</span></span> |
| ---------- | ---------- | ---------- | ---------- |
|  <span data-ttu-id="992d5-315">**WorkerID**</span><span class="sxs-lookup"><span data-stu-id="992d5-315">**WorkerID**</span></span>  |  <span data-ttu-id="992d5-316">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="992d5-316">EmployeeID</span></span> | <span data-ttu-id="992d5-317">**예**</span><span class="sxs-lookup"><span data-stu-id="992d5-317">**Yes**</span></span> | <span data-ttu-id="992d5-318">만들기 작업 시에만 기록</span><span class="sxs-lookup"><span data-stu-id="992d5-318">Written on create only</span></span> | 
|  <span data-ttu-id="992d5-319">**Municipality**</span><span class="sxs-lookup"><span data-stu-id="992d5-319">**Municipality**</span></span>   |   <span data-ttu-id="992d5-320">l</span><span class="sxs-lookup"><span data-stu-id="992d5-320">l</span></span>   |     | <span data-ttu-id="992d5-321">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="992d5-321">Create + update</span></span> |
|  <span data-ttu-id="992d5-322">**Company**</span><span class="sxs-lookup"><span data-stu-id="992d5-322">**Company**</span></span>         | <span data-ttu-id="992d5-323">company</span><span class="sxs-lookup"><span data-stu-id="992d5-323">company</span></span>   |     |  <span data-ttu-id="992d5-324">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="992d5-324">Create + update</span></span> |
|  <span data-ttu-id="992d5-325">**CountryReferenceTwoLetter**</span><span class="sxs-lookup"><span data-stu-id="992d5-325">**CountryReferenceTwoLetter**</span></span>      |   <span data-ttu-id="992d5-326">co</span><span class="sxs-lookup"><span data-stu-id="992d5-326">co</span></span> |     |   <span data-ttu-id="992d5-327">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="992d5-327">Create + update</span></span> |
| <span data-ttu-id="992d5-328">**CountryReferenceTwoLetter**</span><span class="sxs-lookup"><span data-stu-id="992d5-328">**CountryReferenceTwoLetter**</span></span>    |  <span data-ttu-id="992d5-329">C</span><span class="sxs-lookup"><span data-stu-id="992d5-329">c</span></span>  |     |         <span data-ttu-id="992d5-330">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="992d5-330">Create + update</span></span> |
| <span data-ttu-id="992d5-331">**SupervisoryOrganization**</span><span class="sxs-lookup"><span data-stu-id="992d5-331">**SupervisoryOrganization**</span></span>  | <span data-ttu-id="992d5-332">department</span><span class="sxs-lookup"><span data-stu-id="992d5-332">department</span></span>  |     |  <span data-ttu-id="992d5-333">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="992d5-333">Create + update</span></span> |
|  <span data-ttu-id="992d5-334">**PreferredNameData**</span><span class="sxs-lookup"><span data-stu-id="992d5-334">**PreferredNameData**</span></span>  |  <span data-ttu-id="992d5-335">displayName</span><span class="sxs-lookup"><span data-stu-id="992d5-335">displayName</span></span> |     |   <span data-ttu-id="992d5-336">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="992d5-336">Create + update</span></span> |
| <span data-ttu-id="992d5-337">**EmployeeID**</span><span class="sxs-lookup"><span data-stu-id="992d5-337">**EmployeeID**</span></span>    |  <span data-ttu-id="992d5-338">cn</span><span class="sxs-lookup"><span data-stu-id="992d5-338">cn</span></span>    |   |   <span data-ttu-id="992d5-339">만들기 작업 시에만 기록</span><span class="sxs-lookup"><span data-stu-id="992d5-339">Written on create only</span></span> |
| <span data-ttu-id="992d5-340">**Fax**</span><span class="sxs-lookup"><span data-stu-id="992d5-340">**Fax**</span></span>      | <span data-ttu-id="992d5-341">facsimileTelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="992d5-341">facsimileTelephoneNumber</span></span>     |     |    <span data-ttu-id="992d5-342">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="992d5-342">Create + update</span></span> |
| <span data-ttu-id="992d5-343">**FirstName**</span><span class="sxs-lookup"><span data-stu-id="992d5-343">**FirstName**</span></span>   | <span data-ttu-id="992d5-344">givenName</span><span class="sxs-lookup"><span data-stu-id="992d5-344">givenName</span></span>       |     |    <span data-ttu-id="992d5-345">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="992d5-345">Create + update</span></span> |
| <span data-ttu-id="992d5-346">**Switch(\[Active\], , "0", "True", "1",)**</span><span class="sxs-lookup"><span data-stu-id="992d5-346">**Switch(\[Active\], , "0", "True", "1",)**</span></span> |  <span data-ttu-id="992d5-347">accountDisabled</span><span class="sxs-lookup"><span data-stu-id="992d5-347">accountDisabled</span></span>      |     | <span data-ttu-id="992d5-348">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="992d5-348">Create + update</span></span> |
| <span data-ttu-id="992d5-349">**Mobile**</span><span class="sxs-lookup"><span data-stu-id="992d5-349">**Mobile**</span></span>  |    <span data-ttu-id="992d5-350">mobile</span><span class="sxs-lookup"><span data-stu-id="992d5-350">mobile</span></span>       |     |       <span data-ttu-id="992d5-351">만들기 작업 시에만 기록</span><span class="sxs-lookup"><span data-stu-id="992d5-351">Written on create only</span></span> |
| <span data-ttu-id="992d5-352">**EmailAddress**</span><span class="sxs-lookup"><span data-stu-id="992d5-352">**EmailAddress**</span></span>    | <span data-ttu-id="992d5-353">mail</span><span class="sxs-lookup"><span data-stu-id="992d5-353">mail</span></span>    |     |     <span data-ttu-id="992d5-354">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="992d5-354">Create + update</span></span> |
| <span data-ttu-id="992d5-355">**ManagerReference**</span><span class="sxs-lookup"><span data-stu-id="992d5-355">**ManagerReference**</span></span>   | <span data-ttu-id="992d5-356">manager</span><span class="sxs-lookup"><span data-stu-id="992d5-356">manager</span></span>  |     |  <span data-ttu-id="992d5-357">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="992d5-357">Create + update</span></span> |
| <span data-ttu-id="992d5-358">**WorkSpaceReference**</span><span class="sxs-lookup"><span data-stu-id="992d5-358">**WorkSpaceReference**</span></span> | <span data-ttu-id="992d5-359">physicalDeliveryOfficeName</span><span class="sxs-lookup"><span data-stu-id="992d5-359">physicalDeliveryOfficeName</span></span>    |     |  <span data-ttu-id="992d5-360">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="992d5-360">Create + update</span></span> |
| <span data-ttu-id="992d5-361">**PostalCode**</span><span class="sxs-lookup"><span data-stu-id="992d5-361">**PostalCode**</span></span>  |   <span data-ttu-id="992d5-362">postalCode</span><span class="sxs-lookup"><span data-stu-id="992d5-362">postalCode</span></span>  |     | <span data-ttu-id="992d5-363">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="992d5-363">Create + update</span></span> |
| <span data-ttu-id="992d5-364">**LocalReference**</span><span class="sxs-lookup"><span data-stu-id="992d5-364">**LocalReference**</span></span> |  <span data-ttu-id="992d5-365">preferredLanguage</span><span class="sxs-lookup"><span data-stu-id="992d5-365">preferredLanguage</span></span>  |     |  <span data-ttu-id="992d5-366">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="992d5-366">Create + update</span></span> |
| <span data-ttu-id="992d5-367">**Replace(Mid(Replace(\[EmployeeID\], , "(\[\\\\/\\\\\\\\\\\\\[\\\\\]\\\\:\\\\;\\\\</span><span class="sxs-lookup"><span data-stu-id="992d5-367">**Replace(Mid(Replace(\[EmployeeID\], , "(\[\\\\/\\\\\\\\\\\\\[\\\\\]\\\\:\\\\;\\\\</span></span>|<span data-ttu-id="992d5-368">\\\\=\\\\,\\\\+\\\\\*\\\\?\\ \\&lt;\\\\&gt;\])", , "", , ), 1, 20), , "([\\\\.) \*\$](file:///\\.) *$)", , "", , )**</span><span class="sxs-lookup"><span data-stu-id="992d5-368">\\\\=\\\\,\\\\+\\\\\*\\\\?\\\\&lt;\\\\&gt;\])", , "", , ), 1, 20), , "([\\\\.)\*\$](file:///\\.)*$)", , "", , )**</span></span>      |    <span data-ttu-id="992d5-369">sAMAccountName</span><span class="sxs-lookup"><span data-stu-id="992d5-369">sAMAccountName</span></span>            |     |         <span data-ttu-id="992d5-370">만들기 작업 시에만 기록</span><span class="sxs-lookup"><span data-stu-id="992d5-370">Written on create only</span></span> |
| <span data-ttu-id="992d5-371">**LastName**</span><span class="sxs-lookup"><span data-stu-id="992d5-371">**LastName**</span></span>   |   <span data-ttu-id="992d5-372">sn</span><span class="sxs-lookup"><span data-stu-id="992d5-372">sn</span></span>   |     |  <span data-ttu-id="992d5-373">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="992d5-373">Create + update</span></span> |
| <span data-ttu-id="992d5-374">**CountryRegionReference**</span><span class="sxs-lookup"><span data-stu-id="992d5-374">**CountryRegionReference**</span></span> |  <span data-ttu-id="992d5-375">st</span><span class="sxs-lookup"><span data-stu-id="992d5-375">st</span></span>     |     | <span data-ttu-id="992d5-376">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="992d5-376">Create + update</span></span> |
| <span data-ttu-id="992d5-377">**AddressLineData**</span><span class="sxs-lookup"><span data-stu-id="992d5-377">**AddressLineData**</span></span>    |  <span data-ttu-id="992d5-378">streetAddress</span><span class="sxs-lookup"><span data-stu-id="992d5-378">streetAddress</span></span>  |     |   <span data-ttu-id="992d5-379">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="992d5-379">Create + update</span></span> |
| <span data-ttu-id="992d5-380">**PrimaryWorkTelephone**</span><span class="sxs-lookup"><span data-stu-id="992d5-380">**PrimaryWorkTelephone**</span></span>  |  <span data-ttu-id="992d5-381">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="992d5-381">telephoneNumber</span></span>   |     | <span data-ttu-id="992d5-382">만들기 작업 시에만 기록</span><span class="sxs-lookup"><span data-stu-id="992d5-382">Written on create only</span></span> |
| <span data-ttu-id="992d5-383">**BusinessTitle**</span><span class="sxs-lookup"><span data-stu-id="992d5-383">**BusinessTitle**</span></span>   |  <span data-ttu-id="992d5-384">title</span><span class="sxs-lookup"><span data-stu-id="992d5-384">title</span></span>     |     |  <span data-ttu-id="992d5-385">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="992d5-385">Create + update</span></span> |
| <span data-ttu-id="992d5-386">**Join("@",Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Join(".", [FirstName], [LastName]), , "([Øø])", , "oe", , ), , "[Ææ]", , "ae", , ), , "([äãàâãåáąÄÃÀÂÃÅÁĄA])", , "a", , ), , "([B])", , "b", , ), , "([CçčćÇČĆ])", , "c", , ), , "([ďĎD])", , "d", , ), , "([ëèéêęěËÈÉÊĘĚE])", , "e", , ), , "([F])", , "f", , ), , "([G])", , "g", , ), , "([H])", , "h", , ), , "([ïîìíÏÎÌÍI])", , "i", , ), , "([J])", , "j", , ), , "([K])", , "k", , ), , "([ľłŁĽL])", , "l", , ), , "([M])", , "m", , ), , "([ñńňÑŃŇN])", , "n", , ), , "([öòőõôóÖÒŐÕÔÓO])", , "o", , ), , "([P])", , "p", , ), , "([Q])", , "q", , ), , "([řŘR])", , "r", , ), , "([ßšśŠŚS])", , "s", , ), , "([TŤť])", , "t", , ), , "([üùûúůűÜÙÛÚŮŰU])", , "u", , ), , "([V])", , "v", , ), , "([W])", , "w", , ), , "([ýÿýŸÝY])", , "y", , ), , "([źžżŹŽŻZ])", , "z", , ), " ", , , "", , ), "contoso.com")**</span><span class="sxs-lookup"><span data-stu-id="992d5-386">**Join("@",Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Join(".", [FirstName], [LastName]), , "([Øø])", , "oe", , ), , "[Ææ]", , "ae", , ), , "([äãàâãåáąÄÃÀÂÃÅÁĄA])", , "a", , ), , "([B])", , "b", , ), , "([CçčćÇČĆ])", , "c", , ), , "([ďĎD])", , "d", , ), , "([ëèéêęěËÈÉÊĘĚE])", , "e", , ), , "([F])", , "f", , ), , "([G])", , "g", , ), , "([H])", , "h", , ), , "([ïîìíÏÎÌÍI])", , "i", , ), , "([J])", , "j", , ), , "([K])", , "k", , ), , "([ľłŁĽL])", , "l", , ), , "([M])", , "m", , ), , "([ñńňÑŃŇN])", , "n", , ), , "([öòőõôóÖÒŐÕÔÓO])", , "o", , ), , "([P])", , "p", , ), , "([Q])", , "q", , ), , "([řŘR])", , "r", , ), , "([ßšśŠŚS])", , "s", , ), , "([TŤť])", , "t", , ), , "([üùûúůűÜÙÛÚŮŰU])", , "u", , ), , "([V])", , "v", , ), , "([W])", , "w", , ), , "([ýÿýŸÝY])", , "y", , ), , "([źžżŹŽŻZ])", , "z", , ), " ", , , "", , ), "contoso.com")**</span></span>   | <span data-ttu-id="992d5-387">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="992d5-387">userPrincipalName</span></span>     |     | <span data-ttu-id="992d5-388">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="992d5-388">Create + update</span></span>                                                   
| <span data-ttu-id="992d5-389">**Switch(\[Municipality\], "OU=Standard Users,OU=Users,OU=Default,OU=Locations,DC=contoso,DC=com", "Dallas", "OU=Standard Users,OU=Users,OU=Dallas,OU=Locations,DC=contoso,DC=com", "Austin", "OU=Standard Users,OU=Users,OU=Austin,OU=Locations,DC=contoso,DC=com", "Seattle", "OU=Standard Users,OU=Users,OU=Seattle,OU=Locations,DC=contoso,DC=com", “London", "OU=Standard Users,OU=Users,OU=London,OU=Locations,DC=contoso,DC=com")**</span><span class="sxs-lookup"><span data-stu-id="992d5-389">**Switch(\[Municipality\], "OU=Standard Users,OU=Users,OU=Default,OU=Locations,DC=contoso,DC=com", "Dallas", "OU=Standard Users,OU=Users,OU=Dallas,OU=Locations,DC=contoso,DC=com", "Austin", "OU=Standard Users,OU=Users,OU=Austin,OU=Locations,DC=contoso,DC=com", "Seattle", "OU=Standard Users,OU=Users,OU=Seattle,OU=Locations,DC=contoso,DC=com", “London", "OU=Standard Users,OU=Users,OU=London,OU=Locations,DC=contoso,DC=com")**</span></span>  | <span data-ttu-id="992d5-390">parentDistinguishedName</span><span class="sxs-lookup"><span data-stu-id="992d5-390">parentDistinguishedName</span></span>     |     |  <span data-ttu-id="992d5-391">만들기 + 업데이트</span><span class="sxs-lookup"><span data-stu-id="992d5-391">Create + update</span></span> |
  
### <a name="part-3-configure-hello-on-premises-synchronization-agent"></a><span data-ttu-id="992d5-392">3 부: hello 온-프레미스 동기화 에이전트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-392">Part 3: Configure hello on-premises synchronization agent</span></span>

<span data-ttu-id="992d5-393">순서 tooprovision tooActive Directory 온-프레미스에 hello desire Active Directory 포리스트에 도메인에 가입 된 서버에 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-393">In order tooprovision tooActive Directory on-premises, an agent must be installed on a domain-joined server in hello desire Active Directory forest.</span></span> <span data-ttu-id="992d5-394">Hello 절차를 완료 하려면 자격 증명이 필요 도메인 관리자 (또는 엔터프라이즈 관리자)입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-394">Domain admin (or Enterprise admin) credentials are required to complete hello procedure.</span></span>

<span data-ttu-id="992d5-395">**[Hello 온-프레미스 동기화 에이전트 여기를 다운로드할 수 있습니다.](https://go.microsoft.com/fwlink/?linkid=847801)**</span><span class="sxs-lookup"><span data-stu-id="992d5-395">**[You can download hello on-premises synchronization agent here](https://go.microsoft.com/fwlink/?linkid=847801)**</span></span>

<span data-ttu-id="992d5-396">에이전트를 설치한 후 사용자 환경에 대 한 tooconfigure hello 에이전트 다음과 같은 hello Powershell 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-396">After installing agent, run hello Powershell commands below tooconfigure hello agent for your environment.</span></span>

<span data-ttu-id="992d5-397">**명령 #1**</span><span class="sxs-lookup"><span data-stu-id="992d5-397">**Command #1**</span></span>

> <span data-ttu-id="992d5-398">cd C:\\Program Files\\Microsoft Azure Active Directory Synchronization Agent\\Modules\\AADSyncAgent</span><span class="sxs-lookup"><span data-stu-id="992d5-398">cd C:\\Program Files\\Microsoft Azure Active Directory Synchronization Agent\\Modules\\AADSyncAgent</span></span>

> <span data-ttu-id="992d5-399">import-module AADSyncAgent.psd1</span><span class="sxs-lookup"><span data-stu-id="992d5-399">import-module AADSyncAgent.psd1</span></span>

<span data-ttu-id="992d5-400">**명령 #2**</span><span class="sxs-lookup"><span data-stu-id="992d5-400">**Command #2**</span></span>

> <span data-ttu-id="992d5-401">Add-ADSyncAgentActiveDirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="992d5-401">Add-ADSyncAgentActiveDirectoryConfiguration</span></span>

* <span data-ttu-id="992d5-402">입력: "Directory Name"에 대 한 입력 hello AD 포리스트 이름 일부를 입력 한 대로 \#2</span><span class="sxs-lookup"><span data-stu-id="992d5-402">Input: For "Directory Name", enter hello AD Forest name, as entered in part \#2</span></span>
* <span data-ttu-id="992d5-403">입력: Active Directory 포리스트의 관리 사용자 이름 및 암호 입력</span><span class="sxs-lookup"><span data-stu-id="992d5-403">Input: Admin username and password for Active Directory forest</span></span>

<span data-ttu-id="992d5-404">**명령 #3**</span><span class="sxs-lookup"><span data-stu-id="992d5-404">**Command #3**</span></span>

> <span data-ttu-id="992d5-405">Add-ADSyncAgentAzureActiveDirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="992d5-405">Add-ADSyncAgentAzureActiveDirectoryConfiguration</span></span>

* <span data-ttu-id="992d5-406">입력: Azure AD 테넌트의 전역 관리 사용자 이름 및 암호</span><span class="sxs-lookup"><span data-stu-id="992d5-406">Input: Global admin username and password for your Azure AD tenant</span></span>

<span data-ttu-id="992d5-407">**명령 #4**</span><span class="sxs-lookup"><span data-stu-id="992d5-407">**Command #4**</span></span>

> <span data-ttu-id="992d5-408">Get-AdSyncAgentProvisioningTasks</span><span class="sxs-lookup"><span data-stu-id="992d5-408">Get-AdSyncAgentProvisioningTasks</span></span>

* <span data-ttu-id="992d5-409">작업: 데이터가 반환되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-409">Action: Confirm data is returned.</span></span> <span data-ttu-id="992d5-410">이 명령은 Azure AD 테넌트에서 Workday 프로비전 앱을 자동으로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-410">This command automatically discovers Workday provisioning apps in your Azure AD tenant.</span></span> <span data-ttu-id="992d5-411">예제 출력:</span><span class="sxs-lookup"><span data-stu-id="992d5-411">Example output:</span></span>

> <span data-ttu-id="992d5-412">Name          : My AD Forest</span><span class="sxs-lookup"><span data-stu-id="992d5-412">Name          : My AD Forest</span></span>
>
> <span data-ttu-id="992d5-413">Enabled       : True</span><span class="sxs-lookup"><span data-stu-id="992d5-413">Enabled       : True</span></span>
>
> <span data-ttu-id="992d5-414">DirectoryName : mydomain.contoso.com</span><span class="sxs-lookup"><span data-stu-id="992d5-414">DirectoryName : mydomain.contoso.com</span></span>
>
> <span data-ttu-id="992d5-415">Credentialed  : False</span><span class="sxs-lookup"><span data-stu-id="992d5-415">Credentialed  : False</span></span>
>
> <span data-ttu-id="992d5-416">Identifier    : WDAYdnAppDelta.c2ef8d247a61499ba8af0a29208fb853.4725aa7b-1103-41e6-8929-75a5471a5203</span><span class="sxs-lookup"><span data-stu-id="992d5-416">Identifier    : WDAYdnAppDelta.c2ef8d247a61499ba8af0a29208fb853.4725aa7b-1103-41e6-8929-75a5471a5203</span></span>

<span data-ttu-id="992d5-417">**명령 #5**</span><span class="sxs-lookup"><span data-stu-id="992d5-417">**Command #5**</span></span>

> <span data-ttu-id="992d5-418">Start-AdSyncAgentSynchronization -Automatic</span><span class="sxs-lookup"><span data-stu-id="992d5-418">Start-AdSyncAgentSynchronization -Automatic</span></span>

<span data-ttu-id="992d5-419">**명령 #6**</span><span class="sxs-lookup"><span data-stu-id="992d5-419">**Command #6**</span></span>

> <span data-ttu-id="992d5-420">net stop aadsyncagent</span><span class="sxs-lookup"><span data-stu-id="992d5-420">net stop aadsyncagent</span></span>

<span data-ttu-id="992d5-421">**명령 #7**</span><span class="sxs-lookup"><span data-stu-id="992d5-421">**Command #7**</span></span>

> <span data-ttu-id="992d5-422">net start aadsyncagent</span><span class="sxs-lookup"><span data-stu-id="992d5-422">net start aadsyncagent</span></span>

### <a name="part-4-start-hello-service"></a><span data-ttu-id="992d5-423">4 단계: hello 서비스 시작</span><span class="sxs-lookup"><span data-stu-id="992d5-423">Part 4: Start hello service</span></span>
<span data-ttu-id="992d5-424">파트 1-3가 완료 되 면 hello hello Azure 관리 포털에 다시 서비스를 프로 비전을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-424">Once parts 1-3 have been completed, you can start hello provisioning service back in hello Azure Management Portal.</span></span>

1.  <span data-ttu-id="992d5-425">Hello에 **프로 비전** 탭, 집합 hello **프로 비전 상태** 를 **에**합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-425">In hello **Provisioning** tab, set hello **Provisioning Status** to **On**.</span></span>

2. <span data-ttu-id="992d5-426">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-426">Click **Save**.</span></span>

3. <span data-ttu-id="992d5-427">가변 개수의 Workday에 있는 사용자 수에 따라 시간이 걸릴 수 있습니다 hello 초기 동기화가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-427">This will start hello initial sync, which can take a variable number of hours depending on how many users are in Workday.</span></span>

4. <span data-ttu-id="992d5-428">Workday에서 사용자가 같은 개별 동기화 이벤트를 읽어 되 고 다음 hello에 이후에 추가 되거나 업데이트 된 tooActive 디렉터리를 볼 수 있습니다 **감사 로그** 탭 합니다. **[Hello 프로비저닝 tooread hello 감사 기록 하는 방법에 대 한 자세한 지침은 보고 가이드를 참조 하십시오.](active-directory-saas-provisioning-reporting.md)**</span><span class="sxs-lookup"><span data-stu-id="992d5-428">Individual sync events such as what users are being read out of  Workday, and then subsequently added or updated tooActive Directory,  can be viewed in hello **Audit Logs** tab. **[See hello provisioning reporting guide for detailed instructions on how tooread hello audit logs](active-directory-saas-provisioning-reporting.md)**</span></span>

5.  <span data-ttu-id="992d5-429">hello 에이전트 컴퓨터에서 Windows 응용 프로그램 로그 hello hello 에이전트를 통해 수행 되는 모든 작업 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-429">hello Windows Application log on hello agent machine will show all operations performed via hello agent.</span></span>

6. <span data-ttu-id="992d5-430">작업이 완료되면 아래와 같이 **프로비전** 탭에 감사 요약 보고서가 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-430">One completed, it will write an audit summary report in the  **Provisioning** tab, as shown below.</span></span>

![Azure portal](./media/active-directory-saas-workday-inbound-tutorial/WD_3.PNG)


## <a name="configuring-user-provisioning-tooazure-active-directory"></a><span data-ttu-id="992d5-432">사용자 프로비저닝 tooAzure Active Directory를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-432">Configuring user provisioning tooAzure Active Directory</span></span>
<span data-ttu-id="992d5-433">프로 비전 tooAzure Active Directory를 구성 하는 방법 hello 테이블 아래에 설명 된 대로 프로 비전 요구 사항에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-433">How you configure provisioning tooAzure Active Directory will depend on your provisioning requirements, as detailed in hello table below.</span></span>

| <span data-ttu-id="992d5-434">시나리오</span><span class="sxs-lookup"><span data-stu-id="992d5-434">Scenario</span></span> | <span data-ttu-id="992d5-435">해결 방법</span><span class="sxs-lookup"><span data-stu-id="992d5-435">Solution</span></span> |
| -------- | -------- |
| <span data-ttu-id="992d5-436">**사용자를 프로 비전 toobe tooActive 디렉터리와 Azure AD 사용자가 필요**</span><span class="sxs-lookup"><span data-stu-id="992d5-436">**Users need toobe provisioned tooActive Directory and Azure AD**</span></span> | <span data-ttu-id="992d5-437">**[AAD Connect](connect/active-directory-aadconnect.md)** 사용</span><span class="sxs-lookup"><span data-stu-id="992d5-437">Use **[AAD Connect](connect/active-directory-aadconnect.md)**</span></span> |
| <span data-ttu-id="992d5-438">**사용자가 필요한 사용자를 프로 비전 toobe tooActive 디렉터리만**</span><span class="sxs-lookup"><span data-stu-id="992d5-438">**Users need toobe provisioned tooActive Directory only**</span></span> | <span data-ttu-id="992d5-439">**[AAD Connect](connect/active-directory-aadconnect.md)** 사용</span><span class="sxs-lookup"><span data-stu-id="992d5-439">Use **[AAD Connect](connect/active-directory-aadconnect.md)**</span></span> |
| <span data-ttu-id="992d5-440">**사용자가 필요한 사용자를 프로 비전 toobe tooAzure AD만 (클라우드 전용)**</span><span class="sxs-lookup"><span data-stu-id="992d5-440">**Users need toobe provisioned tooAzure AD only (cloud only)**</span></span> | <span data-ttu-id="992d5-441">사용 하 여 hello **Workday tooAzure Active Directory 프로비저닝** hello 응용 프로그램 갤러리에서 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="992d5-441">Use hello **Workday tooAzure Active Directory provisioning** app in hello app gallery</span></span> |

<span data-ttu-id="992d5-442">Azure AD Connect 설치에 자세한 내용은 hello [Azure AD Connect 설명서](connect/active-directory-aadconnect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-442">For instructions on setting up Azure AD Connect, see hello [Azure AD Connect documentation](connect/active-directory-aadconnect.md).</span></span>

<span data-ttu-id="992d5-443">다음 섹션 hello tooprovision 클라우드 전용 사용자 Workday와 Azure AD 간의 연결 설정을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-443">hello following sections describe setting up a connection between Workday and Azure AD tooprovision cloud-only users.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="992d5-444">클라우드 전용 사용자 프로 비전 toobe tooAzure AD 및 온-프레미스 Active Directory 하지 필요로 하는 경우에 아래 hello 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-444">Only follow hello procedure below if you have cloud-only users that need toobe provisioned tooAzure AD and not on-premises Active Directory.</span></span>

### <a name="part-1-adding-hello-azure-ad-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a><span data-ttu-id="992d5-445">1 부: 커넥터 응용 프로그램을 프로 비전 하는 hello Azure AD 추가 하 고 hello 연결 tooWorkday 만들기</span><span class="sxs-lookup"><span data-stu-id="992d5-445">Part 1: Adding hello Azure AD provisioning connector app and creating hello connection tooWorkday</span></span>

<span data-ttu-id="992d5-446">**tooconfigure 클라우드 전용 사용자에 대 한 Workday tooAzure Active Directory 프로비저닝.**</span><span class="sxs-lookup"><span data-stu-id="992d5-446">**tooconfigure Workday tooAzure Active Directory provisioning for cloud-only users:**</span></span>

1.  <span data-ttu-id="992d5-447">너무 이동<https://portal.azure.com>합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-447">Go too<https://portal.azure.com>.</span></span>

2.  <span data-ttu-id="992d5-448">Hello 왼쪽된 탐색 모음에서 선택 **Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="992d5-448">In hello left navigation bar, select **Azure Active Directory**</span></span>

3.  <span data-ttu-id="992d5-449">**엔터프라이즈 응용 프로그램**, **모든 응용 프로그램**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-449">Select **Enterprise Applications**, then **All Applications**.</span></span>

4.  <span data-ttu-id="992d5-450">선택 **응용 프로그램 추가**를 선택한 후 hello **모든** 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-450">Select **Add an application**, and then select hello **All** category.</span></span>

5.  <span data-ttu-id="992d5-451">검색할 **Workday tooAzure AD 프로 비전**, hello 갤러리에서 해당 앱을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-451">Search for **Workday tooAzure AD provisioning**, and add that app from hello gallery.</span></span>

6.  <span data-ttu-id="992d5-452">선택, hello 후 앱 추가 되 고 hello 앱 세부 정보 화면이 표시 **프로 비전**</span><span class="sxs-lookup"><span data-stu-id="992d5-452">After hello app is added and hello app details screen is shown, select **Provisioning**</span></span>

7.  <span data-ttu-id="992d5-453">변경 hello **프로 비전** **모드** 너무**자동**</span><span class="sxs-lookup"><span data-stu-id="992d5-453">Change hello **Provisioning** **Mode** too**Automatic**</span></span>

8.  <span data-ttu-id="992d5-454">전체 hello **관리자 자격 증명** 다음과 같은 섹션:</span><span class="sxs-lookup"><span data-stu-id="992d5-454">Complete hello **Admin Credentials** section as follows:</span></span>

   * <span data-ttu-id="992d5-455">**관리자 사용자 이름** – hello 테 넌 트 도메인 이름을 추가한 함께 hello hello Workday 통합 시스템 계정 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-455">**Admin Username** – Enter hello username of hello Workday integration system account, with hello tenant domain name appended.</span></span> <span data-ttu-id="992d5-456">다음과 같은 형태여야 합니다. username@contoso4</span><span class="sxs-lookup"><span data-stu-id="992d5-456">Should look something like: username@contoso4</span></span>

   * <span data-ttu-id="992d5-457">**관리자 암호 –** hello Workday 통합 시스템 계정의 hello 암호 입력</span><span class="sxs-lookup"><span data-stu-id="992d5-457">**Admin password –** Enter hello password of hello Workday    integration system account</span></span>

   * <span data-ttu-id="992d5-458">**테 넌 트 URL –** 테 넌 트에 대 한 hello URL toohello Workday 웹 서비스 끝점을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-458">**Tenant URL –** Enter hello URL toohello Workday web services endpoint for your tenant.</span></span> <span data-ttu-id="992d5-459">이 같아야 합니다: https://wd3-impl-services1.workday.com/ccx/service/contoso4, 여기서 contoso4 올바른 테 넌 트 이름으로 대체 되 고 wd3 impl 아래 템플릿으로 바뀝니다 hello 올바른 환경 문자열 (필요한 경우).</span><span class="sxs-lookup"><span data-stu-id="992d5-459">This should look like: https://wd3-impl-services1.workday.com/ccx/service/contoso4, where contoso4 is replaced with your correct tenant name and wd3-impl is replaced with hello correct environment string (if necessary).</span></span>

   * <span data-ttu-id="992d5-460">**알림 이메일 –** 이메일 주소를 입력하고 "오류가 발생하면 이메일 보내기" 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-460">**Notification Email –** Enter your email address, and check the    “send email if failure occurs” checkbox.</span></span>

   * <span data-ttu-id="992d5-461">Hello 클릭 **연결 테스트** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-461">Click hello **Test Connection** button.</span></span>

   * <span data-ttu-id="992d5-462">Hello 연결 테스트에 성공 하면 클릭 hello **저장** hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-462">If hello connection test succeeds, click hello **Save** button at hello top.</span></span> <span data-ttu-id="992d5-463">실패 한 경우 해당 hello 작업일 URL을 다시 확인 하 고 자격 증명이 Workday에서 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-463">If it fails, double-check that hello Workday URL and credentials are valid in Workday.</span></span>


### <a name="part-2-configure-attribute-mappings"></a><span data-ttu-id="992d5-464">2부: 특성 매핑 구성</span><span class="sxs-lookup"><span data-stu-id="992d5-464">Part 2: Configure attribute mappings</span></span> 

<span data-ttu-id="992d5-465">이 섹션에서는 클라우드 전용 사용자의 사용자 데이터가 Workday에서 Azure Active Directory로 흐르는 방식을 구성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-465">In this section, you will configure how user data flows from Workday to Azure Active Directory for cloud-only users.</span></span>

1.  <span data-ttu-id="992d5-466">Hello 프로 비전 탭에서 **매핑**, 클릭 **동기화 작업자 tooAzure AD**합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-466">On hello Provisioning tab under **Mappings**, click **Synchronize Workers tooAzure AD**.</span></span>

2.   <span data-ttu-id="992d5-467">Hello에 **소스 개체 범위** 필드에서 어떤 유형의 사용자가 Workday의 특성 기반 필터 집합을 정의 하 여 tooAzure 광고를 프로 비전에 대 한 범위에 속해야 합니다. 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-467">In hello **Source Object Scope** field, you can select which sets of users in Workday should be in scope for provisioning tooAzure AD, by defining a set of attribute-based filters.</span></span> <span data-ttu-id="992d5-468">hello 기본 범위는 "업무 시간에 모든 사용자".</span><span class="sxs-lookup"><span data-stu-id="992d5-468">hello default scope is “all users in Workday”.</span></span> <span data-ttu-id="992d5-469">예제 필터:</span><span class="sxs-lookup"><span data-stu-id="992d5-469">Example filters:</span></span>

   * <span data-ttu-id="992d5-470">예: 1000000 사이의 2000000 작업자 Id를 가진 toousers 범위</span><span class="sxs-lookup"><span data-stu-id="992d5-470">Example: Scope toousers with Worker IDs between 1000000 and   2000000</span></span>

      * <span data-ttu-id="992d5-471">특성: WorkerID</span><span class="sxs-lookup"><span data-stu-id="992d5-471">Attribute: WorkerID</span></span>

      * <span data-ttu-id="992d5-472">연산자: REGEX Match</span><span class="sxs-lookup"><span data-stu-id="992d5-472">Operator: REGEX Match</span></span>

      * <span data-ttu-id="992d5-473">값: (1[0-9][0-9][0-9][0-9][0-9][0-9])</span><span class="sxs-lookup"><span data-stu-id="992d5-473">Value: (1[0-9][0-9][0-9][0-9][0-9][0-9])</span></span>

   * <span data-ttu-id="992d5-474">예: 비정규직 직원만 포함하고 정규직 직원은 포함하지 않음</span><span class="sxs-lookup"><span data-stu-id="992d5-474">Example: Only contingent workers and not regular employees</span></span>

      * <span data-ttu-id="992d5-475">특성: ContingentID</span><span class="sxs-lookup"><span data-stu-id="992d5-475">Attribute: ContingentID</span></span>

      * <span data-ttu-id="992d5-476">연산자: IS NOT NULL</span><span class="sxs-lookup"><span data-stu-id="992d5-476">Operator: IS NOT NULL</span></span>

3.  <span data-ttu-id="992d5-477">Hello에 **대상 개체 작업** 필드 어떤 작업이 Azure AD에 수행 하는 toobe 허용 전체적으로 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-477">In hello **Target Object Actions** field, you can globally filter what actions are allowed toobe performed on Azure AD.</span></span> <span data-ttu-id="992d5-478">**만들기** 및 **업데이트**가 가장 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-478">**Create** and **Update** are most common.</span></span>

4.  <span data-ttu-id="992d5-479">Hello에 **특성 매핑을** 섹션 특성 tooActive 디렉터리 특성을 매핑할 개별 업무 시간을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-479">In hello **Attribute mappings** section, you can define how individual Workday attributes map tooActive Directory attributes.</span></span>

5. <span data-ttu-id="992d5-480">기존 특성 매핑 tooupdate를 클릭 하거나 클릭 **새 매핑을 추가** hello 화면 tooadd 새 매핑 hello 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-480">Click on an existing attribute mapping tooupdate it, or click **Add new mapping** at hello bottom of hello screen tooadd new mappings.</span></span> <span data-ttu-id="992d5-481">개별 특성 매핑은 다음 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-481">An individual attribute mapping supports these properties:</span></span>

   * <span data-ttu-id="992d5-482">**매핑 유형**</span><span class="sxs-lookup"><span data-stu-id="992d5-482">**Mapping Type**</span></span>

      * <span data-ttu-id="992d5-483">**직접** – hello 변경 하지 않고 hello Workday 특성 toohello AD 특성의 값을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-483">**Direct** – Writes hello value of hello Workday attribute         toohello AD attribute, with no changes</span></span>

      * <span data-ttu-id="992d5-484">**상수** -hello AD 특성에 정적 상수 문자열 값을 기록</span><span class="sxs-lookup"><span data-stu-id="992d5-484">**Constant** - Write a static, constant string value to         hello AD attribute</span></span>

      * <span data-ttu-id="992d5-485">**식** – toowrite hello AD 특성에 하나 이상의 Workday 특성을 기반으로 사용자 지정 값을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-485">**Expression** – Allows you toowrite a custom value to hello AD attribute, based on one or more Workday attributes.</span></span> <span data-ttu-id="992d5-486">[자세한 내용은 식에 대한 이 문서를 참조하세요](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="992d5-486">[For more info, see this article on expressions](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>

   * <span data-ttu-id="992d5-487">**원본 특성** -작업일에서 hello 사용자 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-487">**Source attribute** - hello user attribute from Workday.</span></span>

   * <span data-ttu-id="992d5-488">**기본값** – 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-488">**Default value** – Optional.</span></span> <span data-ttu-id="992d5-489">Hello 원본 특성 값이 비어 있으면 hello 매핑이이 값 대신 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-489">If hello source attribute has an empty value, hello mapping will write this value instead.</span></span>
            <span data-ttu-id="992d5-490">가장 일반적인 구성은 빈 tooleave 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-490">Most common configuration is tooleave this blank.</span></span>

   * <span data-ttu-id="992d5-491">**대상 특성** – Azure AD의 사용자 특성 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-491">**Target attribute** – hello user attribute in Azure AD.</span></span>

   * <span data-ttu-id="992d5-492">**이 특성을 사용 하 여 개체를 일치** 이 매핑을 사용할지 여부-toouniquely Workday와 Azure AD 간에 사용자를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-492">**Match objects using this attribute** – Whether or not this mapping should be used toouniquely identify users between Workday and Azure AD.</span></span> <span data-ttu-id="992d5-493">일반적으로 Azure AD에서 일반적으로 hello 직원 ID 특성 (새) 또는 확장 특성에 매핑되는 Workday에 대 한 작업자 ID 필드에서 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-493">This is typically set on the Worker ID field for Workday, which is typically mapped to hello Employee ID attribute (new) or an extension attribute in Azure AD.</span></span>

   * <span data-ttu-id="992d5-494">**일치 우선 순위** – 여러 일치 특성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-494">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="992d5-495">일치 특성이 여러 개 있으면 이 필드에 정의된 순서대로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-495">When there are multiple, they are evaluated in the order defined by this field.</span></span> <span data-ttu-id="992d5-496">일치 항목이 발견되는 즉시 더 이상 일치 특성을 평가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-496">As soon as a match is found, no further matching attributes are evaluated.</span></span>

   * <span data-ttu-id="992d5-497">**이 매핑 적용**</span><span class="sxs-lookup"><span data-stu-id="992d5-497">**Apply this mapping**</span></span>

     * <span data-ttu-id="992d5-498">**항상** – 사용자 만들기 및 업데이트 작업 시 이 매핑을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-498">**Always** – Apply this mapping on both user creation          and update actions</span></span>

     * <span data-ttu-id="992d5-499">**만들기 작업 시에만** - 사용자 만들기 작업 시에만 이 매핑을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-499">**Only during creation** - Apply this mapping only on          user creation actions</span></span>

6. <span data-ttu-id="992d5-500">toosave 매핑을 클릭 **저장** hello 위쪽 특성 매핑 섹션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-500">toosave your mappings, click **Save** at hello top of the      Attribute Mapping section.</span></span>

### <a name="part-3-start-hello-service"></a><span data-ttu-id="992d5-501">3 부: hello 서비스 시작</span><span class="sxs-lookup"><span data-stu-id="992d5-501">Part 3: Start hello service</span></span>
<span data-ttu-id="992d5-502">파트 1-2가 완료 되 면 hello 서비스를 프로 비전을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-502">Once parts 1-2 have been completed, you can start hello provisioning service.</span></span>

1.  <span data-ttu-id="992d5-503">Hello에 **프로 비전** 탭, 집합 hello **프로 비전 상태** 를 **에**합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-503">In hello **Provisioning** tab, set hello **Provisioning Status** to **On**.</span></span>

2. <span data-ttu-id="992d5-504">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-504">Click **Save**.</span></span>

3. <span data-ttu-id="992d5-505">가변 개수의 Workday에 있는 사용자 수에 따라 시간이 걸릴 수 있습니다 hello 초기 동기화가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-505">This will start hello initial sync, which can take a variable number  of hours depending on how many users are in Workday.</span></span>

4. <span data-ttu-id="992d5-506">Hello에 개별 동기화 이벤트를 볼 수 있습니다 **감사 로그** 탭 합니다. **[Hello 프로비저닝 tooread hello 감사 기록 하는 방법에 대 한 자세한 지침은 보고 가이드를 참조 하십시오.](active-directory-saas-provisioning-reporting.md)**</span><span class="sxs-lookup"><span data-stu-id="992d5-506">Individual sync events can be viewed in hello **Audit Logs** tab. **[See hello provisioning reporting guide for detailed instructions on how tooread hello audit logs](active-directory-saas-provisioning-reporting.md)**</span></span>

5. <span data-ttu-id="992d5-507">작업이 완료되면 아래와 같이 **프로비전** 탭에 감사 요약 보고서가 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-507">One completed, it will write an audit summary report in the  **Provisioning** tab, as shown below.</span></span>


## <a name="configuring-writeback-of-email-addresses-tooworkday"></a><span data-ttu-id="992d5-508">전자 메일 주소 tooWorkday의 쓰기 저장 구성</span><span class="sxs-lookup"><span data-stu-id="992d5-508">Configuring writeback of email addresses tooWorkday</span></span>
<span data-ttu-id="992d5-509">Azure Active Directory tooWorkday에서 사용자 전자 메일 주소의 이러한 지침 tooconfigure 쓰기 저장을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-509">Follow these instructions tooconfigure writeback of user email addresses from Azure Active Directory tooWorkday.</span></span>

### <a name="part-1-adding-hello-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a><span data-ttu-id="992d5-510">1 부: 커넥터 응용 프로그램을 프로 비전 하는 hello를 추가 하 고 hello 연결 tooWorkday 만들기</span><span class="sxs-lookup"><span data-stu-id="992d5-510">Part 1: Adding hello provisioning connector app and creating hello connection tooWorkday</span></span>

<span data-ttu-id="992d5-511">**tooconfigure Workday tooActive 디렉터리 프로비저닝이:**</span><span class="sxs-lookup"><span data-stu-id="992d5-511">**tooconfigure Workday tooActive Directory provisioning:**</span></span>

1.  <span data-ttu-id="992d5-512">너무 이동<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="992d5-512">Go too<https://portal.azure.com></span></span>

2.  <span data-ttu-id="992d5-513">Hello 왼쪽된 탐색 모음에서 선택 **Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="992d5-513">In hello left navigation bar, select **Azure Active Directory**</span></span>

3.  <span data-ttu-id="992d5-514">**엔터프라이즈 응용 프로그램**, **모든 응용 프로그램**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-514">Select **Enterprise Applications**, then **All Applications**.</span></span>

4.  <span data-ttu-id="992d5-515">선택 **응용 프로그램 추가**을 선택한 후 hello **모든** 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-515">Select **Add an application**, then select hello **All** category.</span></span>

5.  <span data-ttu-id="992d5-516">검색할 **Workday 쓰기 저장**, hello 갤러리에서 해당 앱을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-516">Search for **Workday Writeback**, and add that app from hello gallery.</span></span>

6.  <span data-ttu-id="992d5-517">선택, hello 후 앱 추가 되 고 hello 앱 세부 정보 화면이 표시 **프로 비전**</span><span class="sxs-lookup"><span data-stu-id="992d5-517">After hello app is added and hello app details screen is shown, select **Provisioning**</span></span>

7.  <span data-ttu-id="992d5-518">변경 hello **프로 비전** **모드** 너무**자동**</span><span class="sxs-lookup"><span data-stu-id="992d5-518">Change hello **Provisioning** **Mode** too**Automatic**</span></span>

8.  <span data-ttu-id="992d5-519">전체 hello **관리자 자격 증명** 다음과 같은 섹션:</span><span class="sxs-lookup"><span data-stu-id="992d5-519">Complete hello **Admin Credentials** section as follows:</span></span>

   * <span data-ttu-id="992d5-520">**관리자 사용자 이름** – hello 테 넌 트 도메인 이름을 추가한 함께 hello hello Workday 통합 시스템 계정 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-520">**Admin Username** – Enter hello username of hello Workday integration system account, with hello tenant domain name appended.</span></span> <span data-ttu-id="992d5-521">다음과 같은 형태여야 합니다. username@contoso4</span><span class="sxs-lookup"><span data-stu-id="992d5-521">Should look something like: username@contoso4</span></span>

   * <span data-ttu-id="992d5-522">**관리자 암호 –** hello Workday 통합 시스템 계정의 hello 암호 입력</span><span class="sxs-lookup"><span data-stu-id="992d5-522">**Admin password –** Enter hello password of hello Workday    integration system account</span></span>

   * <span data-ttu-id="992d5-523">**테 넌 트 URL –** 테 넌 트에 대 한 hello URL toohello Workday 웹 서비스 끝점을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-523">**Tenant URL –** Enter hello URL toohello Workday web services endpoint for your tenant.</span></span> <span data-ttu-id="992d5-524">이 같아야 합니다: https://wd3-impl-services1.workday.com/ccx/service/contoso4, 여기서 contoso4 올바른 테 넌 트 이름으로 대체 되 고 wd3 impl 아래 템플릿으로 바뀝니다 hello 올바른 환경 문자열 (필요한 경우).</span><span class="sxs-lookup"><span data-stu-id="992d5-524">This should look like: https://wd3-impl-services1.workday.com/ccx/service/contoso4, where contoso4 is replaced with your correct tenant name and wd3-impl is replaced with hello correct environment string (if necessary).</span></span>

   * <span data-ttu-id="992d5-525">**알림 이메일 –** 이메일 주소를 입력하고 "오류가 발생하면 이메일 보내기" 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-525">**Notification Email –** Enter your email address, and check the    “send email if failure occurs” checkbox.</span></span>

   * <span data-ttu-id="992d5-526">Hello 클릭 **연결 테스트** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-526">Click hello **Test Connection** button.</span></span> <span data-ttu-id="992d5-527">Hello 연결 테스트에 성공 하면 클릭 hello **저장** hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-527">If hello connection test succeeds, click hello **Save** button at hello top.</span></span> <span data-ttu-id="992d5-528">실패 한 경우 해당 hello 작업일 URL을 다시 확인 하 고 자격 증명이 Workday에서 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-528">If it fails, double-check that hello Workday URL and credentials are valid in Workday.</span></span>


### <a name="part-2-configure-attribute-mappings"></a><span data-ttu-id="992d5-529">2부: 특성 매핑 구성</span><span class="sxs-lookup"><span data-stu-id="992d5-529">Part 2: Configure attribute mappings</span></span> 


<span data-ttu-id="992d5-530">이 섹션에서는 사용자 데이터가 Workday에서 Active Directory로 흐르는 방식을 구성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-530">In this section, you will configure how user data flows from Workday to Active Directory.</span></span>

1.  <span data-ttu-id="992d5-531">Hello 프로 비전 탭에서 **매핑**, 클릭 **동기화 Azure AD 사용자 tooWorkday**합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-531">On hello Provisioning tab under **Mappings**, click **Synchronize Azure AD Users tooWorkday**.</span></span>

2.  <span data-ttu-id="992d5-532">Hello에 **소스 개체 범위** 필드를 필요에 따라가 전자 메일 주소로 서 면으로 다시 tooWorkday 어떤 유형의 Azure Active Directory에서 사용자가 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-532">In hello **Source Object Scope** field, you can optionally filter which sets of users in Azure Active Directory should have their email addresses written back tooWorkday.</span></span> <span data-ttu-id="992d5-533">hello 기본 범위는 "Azure AD의 모든 사용자".</span><span class="sxs-lookup"><span data-stu-id="992d5-533">hello default scope is “all users in Azure AD”.</span></span> 

3.  <span data-ttu-id="992d5-534">Hello에 **특성 매핑을** 섹션 특성 tooActive 디렉터리 특성을 매핑할 개별 업무 시간을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-534">In hello **Attribute mappings** section, you can define how individual Workday attributes map tooActive Directory attributes.</span></span> <span data-ttu-id="992d5-535">기본적으로 hello 전자 메일 주소에 대 한 매핑이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-535">There is a mapping for hello email address by default.</span></span> <span data-ttu-id="992d5-536">그러나 일치 하는 ID hello Workday에 해당 하는 항목이으로 Azure AD에 업데이트 된 toomatch 사용자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-536">However, hello matching ID must be updated toomatch users in Azure AD with their corresponding entries in Workday.</span></span> <span data-ttu-id="992d5-537">일치 하는 인기 있는 메서드는 toosynchronize hello Workday 작업자 ID 또는 직원 tooextensionAttribute1 15 Azure AD에서 ID이 고 Workday에 다시 toomatch 사용자가 Azure AD에서이 특성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-537">A popular matching method is toosynchronize hello Workday worker ID or employee ID tooextensionAttribute1-15 in Azure AD, and then use this attribute in Azure AD toomatch users back in Workday.</span></span>

4.  <span data-ttu-id="992d5-538">toosave 매핑을 클릭 **저장** hello 위쪽 hello 특성 매핑 섹션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-538">toosave your mappings, click **Save** at hello top of hello Attribute Mapping section.</span></span>

### <a name="part-3-start-hello-service"></a><span data-ttu-id="992d5-539">3 부: hello 서비스 시작</span><span class="sxs-lookup"><span data-stu-id="992d5-539">Part 3: Start hello service</span></span>
<span data-ttu-id="992d5-540">파트 1-2가 완료 되 면 hello 서비스를 프로 비전을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-540">Once parts 1-2 have been completed, you can start hello provisioning service.</span></span>

1.  <span data-ttu-id="992d5-541">Hello에 **프로 비전** 탭, 집합 hello **프로 비전 상태** 를 **에**합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-541">In hello **Provisioning** tab, set hello **Provisioning Status** to **On**.</span></span>

2. <span data-ttu-id="992d5-542">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-542">Click **Save**.</span></span>

3. <span data-ttu-id="992d5-543">가변 개수의 Workday에 있는 사용자 수에 따라 시간이 걸릴 수 있습니다 hello 초기 동기화가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-543">This will start hello initial sync, which can take a variable number  of hours depending on how many users are in Workday.</span></span>

4. <span data-ttu-id="992d5-544">Hello에 개별 동기화 이벤트를 볼 수 있습니다 **감사 로그** 탭 합니다. **[Hello 프로비저닝 tooread hello 감사 기록 하는 방법에 대 한 자세한 지침은 보고 가이드를 참조 하십시오.](active-directory-saas-provisioning-reporting.md)**</span><span class="sxs-lookup"><span data-stu-id="992d5-544">Individual sync events can be viewed in hello **Audit Logs** tab. **[See hello provisioning reporting guide for detailed instructions on how tooread hello audit logs](active-directory-saas-provisioning-reporting.md)**</span></span>

5. <span data-ttu-id="992d5-545">작업이 완료되면 아래와 같이 **프로비전** 탭에 감사 요약 보고서가 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-545">One completed, it will write an audit summary report in the  **Provisioning** tab, as shown below.</span></span>

## <a name="known-issues"></a><span data-ttu-id="992d5-546">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="992d5-546">Known issues</span></span>

* <span data-ttu-id="992d5-547">**감사 로그 유럽 로캘의** -hello이 기술 미리 보기 릴리스는 hello로 알려진된 문제 [감사 로그](active-directory-saas-provisioning-reporting.md) hello에 표시 되지 않는 hello Workday 커넥터 앱에 대 한 [Azure포털](https://portal.azure.com) hello Azure AD 테 넌 트 유럽 데이터 센터에 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="992d5-547">**Audit logs in European locales** - As of hello release of this technical preview, there is a known issue with hello [audit logs](active-directory-saas-provisioning-reporting.md) for hello Workday connector apps not appearing in hello [Azure portal](https://portal.azure.com) if hello Azure AD tenant resides in a European data center.</span></span> <span data-ttu-id="992d5-548">이 문제에 대한 픽스가 곧 출시될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="992d5-548">A fix for this issue is forthcoming.</span></span> <span data-ttu-id="992d5-549">가까운 미래 업데이트에 대 한 hello에 다시이 공간을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="992d5-549">Please check this space again in hello near future for updates.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="992d5-550">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="992d5-550">Additional resources</span></span>
* [<span data-ttu-id="992d5-551">자습서: Workday와 Azure Active Directory 간 Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="992d5-551">Tutorial: Configuring single sign-on between Workday and Azure Active Directory</span></span>](active-directory-saas-workday-tutorial.md)
* [<span data-ttu-id="992d5-552">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="992d5-552">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="992d5-553">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="992d5-553">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="992d5-554">다음 단계</span><span class="sxs-lookup"><span data-stu-id="992d5-554">Next steps</span></span>

* [<span data-ttu-id="992d5-555">Tooreview 기록 하는 방법을 알아보고 프로 비전 활동에 대 한 보고서</span><span class="sxs-lookup"><span data-stu-id="992d5-555">Learn how tooreview logs and get reports on provisioning activity</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-provisioning-reporting)
