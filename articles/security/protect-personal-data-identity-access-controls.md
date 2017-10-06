---
title: "Azure id 및 액세스 제어를 사용 하 여 개인 데이터 aaaProtect | Microsoft Docs"
description: "개인 데이터를 보호 Azure id 및 액세스 제어 toohelp를 사용 하 여"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3132c2af25f86662668e5b555eab1d81de7f2e6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a><span data-ttu-id="e66b9-103">Azure Active Directory 및 Multi-Factor Authentication: ID 및 액세스 제어를 사용하여 개인 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="e66b9-103">Azure Active Directory and Multi-Factor Authentication: Protect personal data with identity and access controls</span></span>

<span data-ttu-id="e66b9-104">이 문서 정보 및 Azure Active Directory 및 다단계 인증 보안 기능 및 서비스를 사용 하 여 tooprotect 개인 데이터를 사용할 수 있는 절차를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-104">This article provides information and procedures you can use tooprotect personal data using Azure Active Directory and Multi-factor authentication security features and services.</span></span>

## <a name="scenario"></a><span data-ttu-id="e66b9-105">시나리오</span><span class="sxs-lookup"><span data-stu-id="e66b9-105">Scenario</span></span>

<span data-ttu-id="e66b9-106">Hello 미국에서 본사는 큰 크루즈 회사 hello 지중해, Adriatic, 발트어 바다 뿐 아니라 hello 영국 제도에서 해당 작업 toooffer 여정이 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-106">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="e66b9-107">toosupport 이탈리아를 더 작은 여러 크루즈 줄 획득 이러한 노력 독일, 덴마크 및 hello 영국</span><span class="sxs-lookup"><span data-stu-id="e66b9-107">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span> 

<span data-ttu-id="e66b9-108">hello 회사 hello 클라우드에서 Microsoft Azure toostore 회사 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-108">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="e66b9-109">여기에는 전 세계 고객 기반의 이름, 주소, 전화 번호 및 신용 카드 정보와 같이 식별 가능한 개인 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="e66b9-110">또한 모든 위치에 주소, 전화 번호, 세금 id 번호, 회사 직원에 대 한 의료 보험 정보 등 기존의 인적 자원 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-110">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="e66b9-111">hello 크루즈 줄에는 현재 및 과거 고객과 개인 정보 tootrack 관계를 포함 하는 보상 및 충성도 프로그램 멤버의 큰 데이터베이스 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-111">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="e66b9-112">회사 직원 hello 네트워크 hello 회사의 원격 사무실 및 여행사에서 액세스 하는 hello world 주변에 있는 toosome 회사 리소스에 액세스 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-112">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="e66b9-113">문제 설명</span><span class="sxs-lookup"><span data-stu-id="e66b9-113">Problem statement</span></span>

<span data-ttu-id="e66b9-114">hello 회사 손상 toouse 대 id toogain의 액세스는 침입자에서 고객의 및 직원의 개인 데이터의 hello 개인 정보를 보호 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-114">hello company must protect hello privacy of customers’ and employees’ personal data from attackers seeking toouse compromised identities toogain access.</span></span> <span data-ttu-id="e66b9-115">또한 확인 해야 합니다 합법적인 사용자가 데이터 toodo 해야 하는 사용자만 제한 되는 액세스 toopersonal 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-115">They also must ensure that access toopersonal data by legitimate users is restricted to only those who need it toodo their jobs.</span></span>

## <a name="company-goal"></a><span data-ttu-id="e66b9-116">회사 목표</span><span class="sxs-lookup"><span data-stu-id="e66b9-116">Company goal</span></span>

<span data-ttu-id="e66b9-117">hello 회사의 목표는 tooensure toopersonal 데이터에 액세스 하는 엄격 하 게 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-117">hello company’s goal is tooensure that access toopersonal data is strictly controlled.</span></span> <span data-ttu-id="e66b9-118">Access toopersonal 데이터를 사용자의 신원을 강력한 인증에서 보호할 수 있다는 반드시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-118">It is essential that identities of users with access toopersonal data be protected by strong authentication.</span></span> <span data-ttu-id="e66b9-119">[최소 권한]에 대 한 정책을 합법적인 사용자가 필요로 하는 액세스 하는 유일한 hello 수준을 갖도록 (https://en.wikipedia.org/wiki/Principle_of_least_privilege)을 적용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-119">A policy of [least privilege] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) must be enforced so that legitimate users have only hello level of  access they need, and no more.</span></span>

## <a name="solutions"></a><span data-ttu-id="e66b9-120">솔루션</span><span class="sxs-lookup"><span data-stu-id="e66b9-120">Solutions</span></span>

<span data-ttu-id="e66b9-121">Microsoft Azure 액세스 tooresources 개인 데이터를 포함 하는 사람을 toohelp 회사 제어 id 및 액세스 관리 도구를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-121">Microsoft Azure provides identity and access management tools toohelp companies control who has access tooresources that contain personal data.</span></span>

### <a name="azure-active-directory"></a><span data-ttu-id="e66b9-122">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e66b9-122">Azure Active Directory</span></span>

<span data-ttu-id="e66b9-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) id를 관리 하 고 다른 온-프레미스 및 다른 클라우드 리소스, 데이터 및 응용 프로그램 tooAzure의 액세스를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) manages identities and controls access tooAzure as well as other on-premises and other cloud resources, data, and applications.</span></span> <span data-ttu-id="e66b9-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) 개인 데이터와 같은 toocertain 정보에 액세스할 권한이 있는 사용자의 다단계 인증 toominimize hello 수는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) helps Azure administrators toominimize hello number of people who have access toocertain information such as personal data.</span></span> <span data-ttu-id="e66b9-125">Toodiscover 수 있기를 제한 하 고 권한 있는 id 및 액세스 tooresources, 및 tooassign 일시적 이며 jit (JUST-IN-TIME) 관리 권한 tooeligible 사용자를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-125">It enables them toodiscover, restrict, and monitor privileged identities and their access tooresources, and tooassign temporary, Just-In-Time (JIT) administrative rights tooeligible users.</span></span> <span data-ttu-id="e66b9-126">또한 AAD 관리 권한을 가진 사용자에 대한 정보도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-126">It also provides insight into those who have AAD administrative privileges.</span></span>

<span data-ttu-id="e66b9-127">AAD PIM를 사용 하 여 관련 된 전체 hello 활동은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-127">hello activities involved in using AAD PIM include:</span></span>

- <span data-ttu-id="e66b9-128">디렉터리에 대한 Privileged Identity Management 활성화</span><span class="sxs-lookup"><span data-stu-id="e66b9-128">Enabling Privileged Identity Management for your directory</span></span>

- <span data-ttu-id="e66b9-129">한 눈에 Privileged Identity Management 관리 대시보드 toosee 중요 한 정보를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e66b9-129">Using Privileged Identity Management admin dashboard toosee important information at a glance</span></span>

- <span data-ttu-id="e66b9-130">추가 하거나 영구 또는 적격 관리자 tooeach 역할을 제거 하 여 hello 권한 있는 id (관리자)를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-130">Managing hello privileged identities (administrators) by adding or removing permanent or eligible administrators tooeach role</span></span>

- <span data-ttu-id="e66b9-131">Hello 역할 활성화 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-131">Configuring hello role activation settings</span></span>

- <span data-ttu-id="e66b9-132">역할 활성화</span><span class="sxs-lookup"><span data-stu-id="e66b9-132">Activating roles</span></span>

- <span data-ttu-id="e66b9-133">역할 활동 검토</span><span class="sxs-lookup"><span data-stu-id="e66b9-133">Reviewing role activity</span></span>

#### <a name="how-do-i-enable-aad-pim"></a><span data-ttu-id="e66b9-134">AAD PIM을 사용하도록 설정하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="e66b9-134">How do I enable AAD PIM?</span></span>

<span data-ttu-id="e66b9-135">PIM을 사용 하 여 디렉터리에 대 한 toostart 다음 hello지 않습니다:</span><span class="sxs-lookup"><span data-stu-id="e66b9-135">toostart using PIM for your directory, do hello following:</span></span>

1. <span data-ttu-id="e66b9-136">디렉터리의 전역 관리자로 Azure 포털 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-136">Sign in toohello Azure portal as a global administrator of your directory.</span></span>

2. <span data-ttu-id="e66b9-137">조직에서 둘 이상의 디렉터리를 경우 hello hello Azure 포털의 상단 오른쪽 모서리에서 사용자 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-137">If your organization has more than one directory, select your username in hello upper right-hand corner of hello Azure portal.</span></span> <span data-ttu-id="e66b9-138">Azure AD Privileged Identity Management ´ hello 디렉터리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-138">Select hello directory where you will use Azure AD Privileged Identity Management.</span></span>

3. <span data-ttu-id="e66b9-139">선택 **더 많은 서비스** hello를 사용 하 여 **필터** Azure AD Privileged Identity Management에 대 한 toosearch 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-139">Select **More services** and use hello **Filter** textbox toosearch for Azure AD Privileged Identity Management.</span></span>

4. <span data-ttu-id="e66b9-140">확인 **Pin toodashboard** 클릭 하 고 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-140">Check **Pin toodashboard** and then click **Create**.</span></span> <span data-ttu-id="e66b9-141">hello Privileged Identity Management 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-141">hello Privileged Identity Management application opens.</span></span>

<span data-ttu-id="e66b9-142">Azure AD Privileged Identity Management 설정 되 고 나면 hello 응용 프로그램을 열 때마다 hello 탐색 블레이드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-142">Once Azure AD Privileged Identity Management is set up, you see hello navigation blade whenever you open hello application.</span></span>

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

<span data-ttu-id="e66b9-143">AAD PIM 시작에 대한 자세한 내용과 지침은 [Azure AD Privileged Identity Management 시작](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e66b9-143">For more information and instructions on getting started with AAD PIM, see [Start Using Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span></span>

### <a name="azure-role-based-access-control"></a><span data-ttu-id="e66b9-144">Azure 역할 기반 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="e66b9-144">Azure Role-based Access Control</span></span>

<span data-ttu-id="e66b9-145">[Azure 역할 기반 액세스 제어](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) 다단계 인증 hello hello 사용자의 할당 된 역할에 따라 액세스 권한을 부여 함으로써 tooAzure 리소스에 액세스를 관리 하는 (RBAC)는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-145">[Azure Role-Based Access Control](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) helps Azure administrators manage access tooAzure resources by enabling hello granting of access based on hello user’s assigned role.</span></span> <span data-ttu-id="e66b9-146">팀에서 의무를 분리 수 있으며 hello 양의 데이터만 액세스 toousers, 그룹 및 필요 하다는 tooperform 업무 응용 프로그램 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-146">You can segregate duties within a team and grant only hello amount of access toousers, groups and applications that they need tooperform their jobs.</span></span>

<span data-ttu-id="e66b9-147">Toousers hello Azure 포털, Azure 명령줄 도구 또는 Azure 관리 Api를 사용 하 여 역할 기반 액세스를 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-147">Role-based access can be granted toousers using hello Azure portal, Azure Command-Line tools or Azure Management APIs.</span></span>

<span data-ttu-id="e66b9-148">Azure RBAC 기본 사항에 대 한 자세한 내용은 참조 하세요. [hello Azure 포털에서에서 역할 기반 액세스 제어를 시작 합니다.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span><span class="sxs-lookup"><span data-stu-id="e66b9-148">For more information about Azure RBAC basics, see [Get started with Role-Based Access Control in hello Azure Portal.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span></span>

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a><span data-ttu-id="e66b9-149">PowerShell을 사용하여 Azure RBAC를 관리하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="e66b9-149">How do I manage Azure RBAC with PowerShell?</span></span>

<span data-ttu-id="e66b9-150">PowerShell cmdlet toomanage hello 다음 관리 작업을 포함 하 여 Azure RBAC를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-150">You can use PowerShell cmdlets toomanage Azure RBAC, including hello following management tasks:</span></span>

- <span data-ttu-id="e66b9-151">역할 나열</span><span class="sxs-lookup"><span data-stu-id="e66b9-151">List roles</span></span>

- <span data-ttu-id="e66b9-152">액세스 권한이 있는 사용자 확인</span><span class="sxs-lookup"><span data-stu-id="e66b9-152">See who has access</span></span>

- <span data-ttu-id="e66b9-153">액세스 권한 부여</span><span class="sxs-lookup"><span data-stu-id="e66b9-153">Grant access</span></span>

- <span data-ttu-id="e66b9-154">액세스 권한 제거</span><span class="sxs-lookup"><span data-stu-id="e66b9-154">Remove access</span></span>

- <span data-ttu-id="e66b9-155">사용자 지정 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="e66b9-155">Create a custom role</span></span>

- <span data-ttu-id="e66b9-156">리소스 공급자에 대한 작업 가져오기</span><span class="sxs-lookup"><span data-stu-id="e66b9-156">Get Actions for a Resource Provider</span></span>

- <span data-ttu-id="e66b9-157">사용자 지정 역할 수정</span><span class="sxs-lookup"><span data-stu-id="e66b9-157">Modify a custom role</span></span>

- <span data-ttu-id="e66b9-158">사용자 지정 역할 삭제</span><span class="sxs-lookup"><span data-stu-id="e66b9-158">Delete a custom role</span></span>

- <span data-ttu-id="e66b9-159">사용자 지정 역할 나열</span><span class="sxs-lookup"><span data-stu-id="e66b9-159">List custom roles</span></span>

<span data-ttu-id="e66b9-160">Toomanage PowerShell과 함께 Azure RBAC를 확인 하려면 어떻게에 대 한 지침은 [Azure powershell 관리 역할 기반 액세스](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell)합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-160">For instructions on how toomanage Azure RBAC with PowerShell, see [Manage Role-based Access with Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span></span>

### <a name="azure-multi-factor-authentication"></a><span data-ttu-id="e66b9-161">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="e66b9-161">Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="e66b9-162">[Azure Multi-factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA)은 간단한 로그인 프로세스에 대 한 사용자 요구를 충족 하면서 보호 액세스 toodata 및 응용 프로그램을 사용 하는 2 단계 확인 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-162">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) is a two-step verification solution that helps safeguard access toodata and applications, while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="e66b9-163">전화 통화, 문자 메시지 또는 모바일 앱 확인과 같은 다양한 확인 방법을 통해 강력한 인증을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-163">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

<span data-ttu-id="e66b9-164">toofirst 해야 toodeploy MFA에서 Azure 클라우드 hello 사용 하도록 설정 하 고 다음 사용자에 대 한 2 단계 인증을 켭니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-164">toodeploy MFA in hello Azure cloud, you need toofirst enable it and then turn on two-step verification for users.</span></span>

#### <a name="how-do-i-enable-azure-toouse-mfa"></a><span data-ttu-id="e66b9-165">Azure toouse MFA를 어떻게 사용 합니까?</span><span class="sxs-lookup"><span data-stu-id="e66b9-165">How do I enable Azure toouse MFA?</span></span>

<span data-ttu-id="e66b9-166">사용자에 게 Azure Multi-factor Authentication을 포함 하는 라이선스 있으면 Azure MFA에 toodo tooturn 해야 하는 일은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-166">If your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need toodo tooturn on Azure MFA.</span></span> <span data-ttu-id="e66b9-167">그렇지 않으면 디렉터리에 toocreate Multi-factor Auth 공급자를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-167">If not, you need toocreate a Multi-Factor Auth provider in your directory.</span></span> <span data-ttu-id="e66b9-168">toodo이를 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-168">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="e66b9-169">선택 **Active Directory** hello Azure 클래식 포털 (관리자 권한으로 로그온)에서.</span><span class="sxs-lookup"><span data-stu-id="e66b9-169">Select **Active Directory** in hello Azure classic portal (logged on as an administrator).</span></span>

2. <span data-ttu-id="e66b9-170">**Multi-Factor Authentication 공급자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-170">Select **Multi-Factor Authentication Providers.**</span></span>

3. <span data-ttu-id="e66b9-171">**새로 만들기**를 선택한 다음 **App Services** 아래에서 **Multi-Factor Auth 공급자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-171">Select **New,** and then under **App Services,** select **Multi-Factor Auth Provider.**</span></span>

4. <span data-ttu-id="e66b9-172">**빠른 생성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-172">Select **Quick Create.**</span></span>

5. <span data-ttu-id="e66b9-173">Hello 이름 필드에서 작성 (인증 단위 또는 활성화 된 사용자별) 사용 모델을 선택 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e66b9-173">Fill in hello name field and select a usage model (per authentication or per enabled user).</span></span>

6. <span data-ttu-id="e66b9-174">MFA 공급자는 hello와 연관 된 디렉터리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-174">Designate a directory with which hello MFA Provider is associated.</span></span>

7. <span data-ttu-id="e66b9-175">Hello 클릭 **만들기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-175">Click hello **Create** button.</span></span>

![](media/protect-personal-data-identity-access-controls/quick-create.png)

<span data-ttu-id="e66b9-176">자세한 방법에 대 한 toomanage Multi-factor Auth 공급자를 사용 하 여 참조 [Azure Multi-factor Auth 공급자 시작 합니다.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span><span class="sxs-lookup"><span data-stu-id="e66b9-176">For more instructions on how toomanage your Multi-Factor Auth Provider, see [Getting Started with an Azure Multi-Factor Auth Provider.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span></span>

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a><span data-ttu-id="e66b9-177">사용자에 대한 2단계 인증을 설정하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="e66b9-177">How do I turn on two-step verification for users?</span></span>

<span data-ttu-id="e66b9-178">모든 기호 기능에 대 한 2 단계 인증을 적용할 수 있습니다 또는 특정 조건을 만족할 경우에 조건부 액세스 정책을 toorequire 2 단계 인증을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-178">You can enforce two-step verification for all sign-ins, or you can create conditional access policies toorequire two-step verification only when specific conditions apply.</span></span>

<span data-ttu-id="e66b9-179">Azure MFA 사용자 상태를 변경 하 여 hello에 대 한 2 단계 인증을 요구 한 기존의 접근 방식은입니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-179">Enabling Azure MFA by changing user states is hello traditional approach for requiring two-step verification.</span></span> <span data-ttu-id="e66b9-180">사용 하도록 설정 하면 모든 hello 사용자가 로그인 할 때마다 동일한 요구 사항을 tooperform 2 단계 인증을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-180">All hello users that you enable will have hello same requirement tooperform two-step verification every time they sign in.</span></span> <span data-ttu-id="e66b9-181">사용자가 사용하도록 설정되면 해당 사용자에게 영향을 줄 수 있는 모든 조건부 액세스 정책이 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-181">Enabling a user overrides any conditional access policies that may affect that user.</span></span>

<span data-ttu-id="e66b9-182">조건부 액세스 정책을 사용하여 Azure MFA를 사용하도록 설정하는 것은 2단계 인증을 요구하는 것보다 더 유연한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-182">Enabling Azure MFA with a conditional access policy is a more flexible approach for requiring two-step verification.</span></span> <span data-ttu-id="e66b9-183">Toogroups 뿐만 아니라 개별 사용자에 게 적용 되는 조건부 액세스 정책을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-183">You can create conditional access policies that apply toogroups as well as individual users.</span></span> <span data-ttu-id="e66b9-184">위험 수준이 높은 그룹에는 위험 수준이 낮은 그룹보다 더 많은 제한이 제공되거나 위험 수준이 높은 클라우드 앱에만 2단계 인증이 요구되고 위험 수준이 낮은 그룹에는 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-184">High-risk groups can be given more restrictions than low-risk groups, or two-step verification can be required only for high-risk cloud apps and skipped for low-risk ones.</span></span> <span data-ttu-id="e66b9-185">그러나 조건부 액세스는 Azure Active Directory의 유료 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-185">However, conditional access is a paid feature of Azure Active Directory.</span></span>

<span data-ttu-id="e66b9-186">사용자 상태를 변경 하 여 MFA tooenable 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-186">tooenable MFA by changing user state, do hello following:</span></span>

1. <span data-ttu-id="e66b9-187">관리자 권한으로 Azure 포털 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-187">Sign in toohello Azure portal as an administrator.</span></span>
2. <span data-ttu-id="e66b9-188">너무 이동**Azure Active Directory \> 사용자 및 그룹 \> 모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-188">Go too**Azure Active Directory \> Users and groups \> All users**.</span></span>
3. <span data-ttu-id="e66b9-189">**Multi-Factor Authentication**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-189">Select **Multi-Factor Authentication**.</span></span>
4. <span data-ttu-id="e66b9-190">Azure MFA에 대 한 tooenable 되도록 찾기 hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-190">Find hello user that you want tooenable for Azure MFA.</span></span> <span data-ttu-id="e66b9-191">Toochange 할 수 있습니다 hello hello 위쪽에는 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-191">You may need toochange hello view at hello top.</span></span>
5. <span data-ttu-id="e66b9-192">Hello 상자 다음 toohello 사용자의 이름을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e66b9-192">Check hello box next toohello user’s name.</span></span>
6. <span data-ttu-id="e66b9-193">오른쪽의 빠른 단계에서 사용 되는 hello, 선택 **사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-193">On hello right, under quick steps, choose **Enable**.</span></span>

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. <span data-ttu-id="e66b9-194">Hello 팝업 창이 열리면 선택한 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-194">Confirm your selection in hello pop-up window that opens.</span></span>  <span data-ttu-id="e66b9-195">사용자가 MFA 활성화 된 사람 묻습니다 tooregister hello 다음 번에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-195">Users for whom MFA has been enabled will be asked tooregister hello next time they sign in.</span></span>

<span data-ttu-id="e66b9-196">조건부 액세스 정책 사용 하 여 Azure MFA tooenable 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-196">tooenable Azure MFA with a conditional access policy, do hello following:</span></span>

1. <span data-ttu-id="e66b9-197">관리자 권한으로 Azure 포털 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-197">Sign in toohello Azure portal as an administrator.</span></span>

2. <span data-ttu-id="e66b9-198">너무 이동**Azure Active Directory \> 조건부 액세스**합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-198">Go too**Azure Active Directory \> Conditional access**.</span></span>

3. <span data-ttu-id="e66b9-199">**새 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-199">Select **New policy**.</span></span>

4. <span data-ttu-id="e66b9-200">**할당** 아래에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-200">Under **Assignments**, select **Users and groups**.</span></span> <span data-ttu-id="e66b9-201">사용 하 여 hello **Include** 및 **제외** 탭 toospecify 있는 사용자 및 그룹 hello 정책에 의해 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-201">Use hello **Include** and     **Exclude** tabs toospecify which users and groups will be managed by hello policy.</span></span>

5. <span data-ttu-id="e66b9-202">**할당** 아래에서 **클라우드 앱**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-202">Under **Assignments**, select **Cloud apps.**</span></span> <span data-ttu-id="e66b9-203">너무 선택**모든 클라우드 앱이 포함**합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-203">Choose too**include All cloud apps**.</span></span>
6.  <span data-ttu-id="e66b9-204">**액세스 제어** 아래에서 **허용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-204">Under **Access controls**, select **Grant**.</span></span> <span data-ttu-id="e66b9-205">**다단계 인증 필요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-205">Choose **Require multi-factor authentication**.</span></span>
7.  <span data-ttu-id="e66b9-206">설정 **정책 사용** 너무**에** 선택한 후 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="e66b9-206">Turn **Enable policy** too**On** and then select **Save**.</span></span>

<span data-ttu-id="e66b9-207">에 대 한 내용은 사기 행위 경고를 tooconfigure Azure MFA 설정 tooset 일회성 바이패스를 만든 사용자 지정 음성 메시지를 사용 하 여, 캐싱을 구성 하 여, 신뢰할 수 있는 Ip를 지정, 앱 암호를 만들, 선택 및 사용자가 신뢰 하는 장치에 대 한 MFA를 기억 하는 것을 사용 하도록 설정 참조 확인 방법을 [Azure Multi-factor Authentication 설정 구성 합니다.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span><span class="sxs-lookup"><span data-stu-id="e66b9-207">For information on how tooconfigure Azure MFA settings tooset up fraud alerts, create a one-time bypass, use custom voice messages, configure caching, specify trusted IPs, create app passwords, enable remembering MFA for devices that users trust, and select verification methods, see [Configure Azure Multi-Factor Authentication Settings.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e66b9-208">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e66b9-208">Next steps</span></span>

- [<span data-ttu-id="e66b9-209">Azure AD에서 권한 있는 액세스 보안</span><span class="sxs-lookup"><span data-stu-id="e66b9-209">Securing privileged access in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [<span data-ttu-id="e66b9-210">Azure Multi-Factor Authentication에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="e66b9-210">Frequently asked questions about Azure Multi-Factor Authentication</span></span>](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [<span data-ttu-id="e66b9-211">역할 기반 액세스 제어 문제 해결</span><span class="sxs-lookup"><span data-stu-id="e66b9-211">Role-based Access Control troubleshooting</span></span>](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [<span data-ttu-id="e66b9-212">Azure Active Directory ID 보호</span><span class="sxs-lookup"><span data-stu-id="e66b9-212">Azure Active Directory Identity Protection</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)
