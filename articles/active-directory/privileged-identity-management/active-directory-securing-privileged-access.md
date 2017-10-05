---
title: "Azure AD에서 권한 있는 액세스 보안 | Microsoft Docs"
description: "Azure, Azure Active Directory 및 Microsoft Online Services에서 권한 있는 액세스 보안에 대한 접근 방법을 설명하는 항목입니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: mwahl
ms.assetid: 235a0ce9-1daf-4433-8f65-9c6afcd64d08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: acd1c11cecfa37f607fe5d82a76a40647093f43f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="securing-privileged-access-in-azure-ad"></a><span data-ttu-id="bd3e6-103">Azure AD에서 권한 있는 액세스 보안</span><span class="sxs-lookup"><span data-stu-id="bd3e6-103">Securing privileged access in Azure AD</span></span>
<span data-ttu-id="bd3e6-104">최신 조직에서 비즈니스 자산 보호를 위해 중요한 첫 번째 단계는 권한 있는 액세스 보안입니다.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-104">Securing privileged access is a critical first step to help protect business assets in a modern organization.</span></span> <span data-ttu-id="bd3e6-105">권한 있는 계정은 IT 시스템을 운영하고 관리하는 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-105">Privileged accounts are accounts that administer and manage IT systems.</span></span> <span data-ttu-id="bd3e6-106">사이버 공격자는 조직의 데이터와 시스템에 대한 액세스 권한을 얻기 위해 이러한 계정을 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-106">Cyber-attackers target these accounts to gain access to an organization’s data and systems.</span></span> <span data-ttu-id="bd3e6-107">권한 있는 액세스를 보호하려면 계정과 시스템을 악의적 사용자에게 노출될 위험으로부터 격리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-107">To secure privileged access, you should isolate the accounts and systems from the risk of being exposed to a malicious user.</span></span>

<span data-ttu-id="bd3e6-108">더 많은 사용자가 클라우드 서비스를 통해 권한 있는 액세스를 얻기 시작했습니다.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-108">More users are starting to get privileged access through cloud services.</span></span> <span data-ttu-id="bd3e6-109">여기에는 Office365의 전역 관리자, Azure 구독 관리자 및 SaaS 앱 또는 VM에서 관리 액세스 권한이 있는 사용자가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-109">This can include global administrators of Office365, Azure subscription administrators, and users who have administrative access in VMs or on SaaS apps.</span></span>

<span data-ttu-id="bd3e6-110">[권한 있는 액세스 보안](https://technet.microsoft.com/library/mt631194.aspx)에서 이 로드맵을 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-110">Microsoft recommends you follow this roadmap on [Securing Privileged Access](https://technet.microsoft.com/library/mt631194.aspx).</span></span>

<span data-ttu-id="bd3e6-111">Azure Active Directory, Office 365 또는 다른 Microsoft 서비스 및 응용 프로그램을 사용하는 고객의 경우 이러한 원칙은 Active Directory 또는 Azure Active Directory에서 사용자 계정을 관리하고 인증하는지 여부에 관계없이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-111">For customers using Azure Active Directory, Office 365, or other Microsoft services and applications, these principles apply whether user accounts are managed and authenticated by Active Directory or in Azure Active Directory.</span></span> <span data-ttu-id="bd3e6-112">다음 섹션에서는 권한 있는 액세스 보안을 지원하는 Azure AD 기능에 대한 자세한 내용을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-112">The following sections provide more information on Azure AD features to support securing privileged access.</span></span>

## <a name="azure-multi-factor-authentication"></a><span data-ttu-id="bd3e6-113">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="bd3e6-113">Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="bd3e6-114">관리자 인증의 보안을 강화하려면 권한을 부여하기 전에 2단계 인증이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-114">To increase the security of administrator authentication, you should require two-step verification before granting privileges.</span></span> <span data-ttu-id="bd3e6-115">2단계 인증은 사용자 이름과 암호 이외의 다른 항목을 사용해야 하는 사람인지를 확인하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-115">Two-step verification is a method of verifying who you are that requires the use of more than just a username and password.</span></span> <span data-ttu-id="bd3e6-116">사용자 로그인 및 트랜잭션에 대한 보안의 두 번째 계층을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-116">It provides a second layer of security to user sign-ins and transactions.</span></span>

<span data-ttu-id="bd3e6-117">Azure MFA(Multi-Factor Authentication)는 간단한 로그인 프로세스에 대한 사용자의 요구를 충족하면서 데이터와 응용 프로그램에 대한 액세스를 보호하는 Microsoft의 2단계 인증 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-117">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution, which helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="bd3e6-118">다음과 같이 다양하고 손쉬운 인증 옵션을 통해 강력한 인증을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-118">It delivers strong authentication via a range of easy verification options including:</span></span>

- <span data-ttu-id="bd3e6-119">전화 통화</span><span class="sxs-lookup"><span data-stu-id="bd3e6-119">phone calls</span></span>
- <span data-ttu-id="bd3e6-120">문자 메시지</span><span class="sxs-lookup"><span data-stu-id="bd3e6-120">text messages</span></span>
- <span data-ttu-id="bd3e6-121">모바일 앱 알림</span><span class="sxs-lookup"><span data-stu-id="bd3e6-121">mobile app notifications</span></span>
- <span data-ttu-id="bd3e6-122">모바일 앱 확인 코드</span><span class="sxs-lookup"><span data-stu-id="bd3e6-122">mobile app verification codes</span></span>
- <span data-ttu-id="bd3e6-123">타사 OATH 토큰</span><span class="sxs-lookup"><span data-stu-id="bd3e6-123">third-party OATH tokens</span></span>

<span data-ttu-id="bd3e6-124">Azure Multi-Factor Authentication의 작동 방식에 대한 개요는 다음 비디오를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-124">For an overview of how Azure Multi-Factor Authentication works see the following video:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]

<span data-ttu-id="bd3e6-125">자세한 내용은 [Office 365용 MFA 및 Azure용 MFA](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-125">For more information, see [MFA for Office 365 and MFA for Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).</span></span>

## <a name="time-bound-privileges"></a><span data-ttu-id="bd3e6-126">시간 제한 권한</span><span class="sxs-lookup"><span data-stu-id="bd3e6-126">Time-bound privileges</span></span>
<span data-ttu-id="bd3e6-127">일부 조직에서는 높은 권한이 있는 역할의 사용자가 너무 많은 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-127">Some organizations may find that they have too many users in highly privileged roles.</span></span> <span data-ttu-id="bd3e6-128">서비스 등록 등의 특정 작업에 대한 역할에 사용자가 추가되었을 수 있지만 이후 그러한 권한을 자주 사용하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-128">A user might have been added to the role for a particular activity, like to sign up for a service, but didn't use those privileges frequently afterward.</span></span>

<span data-ttu-id="bd3e6-129">권한에 대한 노출 시간을 줄이고 사용에 대한 가시성을 높이려면 사용자가 작업을 수행해야 하는 "적시에"(JIT)에 권한만 사용하도록 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-129">To lower the exposure time of privileges and increase your visibility into their use, limit users to only taking on their privileges "just in time" (JIT), when they need to perform a task.</span></span> <span data-ttu-id="bd3e6-130">Azure Active Directory 및 Microsoft Online Services에서 [Azure AD PIM(Privileged Identity Management)](http://aka.ms/AzurePIM)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-130">For Azure Active Directory and Microsoft Online Services, you can use [Azure AD Privileged Identity Management (PIM)](http://aka.ms/AzurePIM).</span></span>

![PIM 대시보드][2]

## <a name="attack-detection"></a><span data-ttu-id="bd3e6-132">공격 탐지</span><span class="sxs-lookup"><span data-stu-id="bd3e6-132">Attack detection</span></span>
<span data-ttu-id="bd3e6-133">[Azure Active Directory ID 보호](../active-directory-identityprotection.md)는 조직의 ID에 영향을 주는 위험 이벤트와 잠재적 취약성에 대한 통합된 뷰를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-133">[Azure Active Directory Identity Protection](../active-directory-identityprotection.md) provides a consolidated view into risk events and potential vulnerabilities affecting your organization’s identities.</span></span> <span data-ttu-id="bd3e6-134">ID 보호는 위험 이벤트에 따라 각 사용자에 대한 위험 수준을 계산하며 이는 위험 기반 정책을 구성하여 조직의 ID를 자동으로 보호할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-134">Based on risk events, Identity Protection calculates a user risk level for each user, enabling you to configure risk-based policies to automatically protect the identities of your organization.</span></span> <span data-ttu-id="bd3e6-135">이 정책은 Azure Active Directory 및 EMS에서 제공하는 다른 조건부 액세스 제어와 함께 자동적으로 사용자를 차단하거나 암호 재설정 및 다단계 인증 적용을 포함한 제안 사항을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-135">These policies, along with other conditional access controls provided by Azure Active Directory and EMS, can automatically block the user or offer suggestions that include password resets and multi-factor authentication enforcement.</span></span>

![Azure AD ID 보호][3]

## <a name="conditional-access"></a><span data-ttu-id="bd3e6-137">조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="bd3e6-137">Conditional access</span></span>
<span data-ttu-id="bd3e6-138">조건부 액세스 제어를 통해 Azure Active Directory는 사용자를 인증할 때 및 응용 프로그램에 대한 액세스를 허용하기 전에 선택한 특정 조건을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-138">With conditional access control, Azure Active Directory checks the specific conditions you choose when authenticating a user, before allowing access to an application.</span></span> <span data-ttu-id="bd3e6-139">이러한 조건이 충족되면 사용자가 인증되고 응용 프로그램에 대한 액세스가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-139">Once those conditions are met, the user is authenticated and allowed access to the application.</span></span>

![MFA를 사용하는 조건부 액세스 규칙 설정][4]

## <a name="related-articles"></a><span data-ttu-id="bd3e6-141">관련된 문서</span><span class="sxs-lookup"><span data-stu-id="bd3e6-141">Related articles</span></span>
* <span data-ttu-id="bd3e6-142">[Azure Multi-Factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md) 사용</span><span class="sxs-lookup"><span data-stu-id="bd3e6-142">Enable [Azure Multi-Factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)</span></span>
* <span data-ttu-id="bd3e6-143">[Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md) 사용</span><span class="sxs-lookup"><span data-stu-id="bd3e6-143">Enable [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)</span></span>
* <span data-ttu-id="bd3e6-144">[Azure AD ID 보호](../active-directory-identityprotection.md) 사용</span><span class="sxs-lookup"><span data-stu-id="bd3e6-144">Enable [Azure AD Identity Protection](../active-directory-identityprotection.md)</span></span>
* <span data-ttu-id="bd3e6-145">[조건부 액세스 제어](../active-directory-conditional-access.md) 사용</span><span class="sxs-lookup"><span data-stu-id="bd3e6-145">Enable [conditional access controls](../active-directory-conditional-access.md)</span></span>

<span data-ttu-id="bd3e6-146">완벽한 보안 로드맵 작성에 대한 자세한 내용은 [Microsoft Cloud Security for Enterprise Architects(엔터프라이즈 설계자를 위한 Microsoft 클라우드 보안)](http://aka.ms/securecustomer) 문서의 "Customer responsibilities and roadmap(고객 책임 및 로드맵)" 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-146">For more information on building a complete security roadmap, see the “Customer responsibilities and roadmap” section of the [Microsoft Cloud Security for Enterprise Architects](http://aka.ms/securecustomer) document.</span></span> <span data-ttu-id="bd3e6-147">이러한 항목에 도움이 되는 Microsoft 서비스 참여에 대한 자세한 내용은 Microsoft 담당자에게 문의하거나 [사이버 보안 솔루션 페이지](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="bd3e6-147">For more information on engaging Microsoft services to assist with any of these topics, contact your Microsoft representative or visit our [Cybersecurity solutions page](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).</span></span>

<!--Image references-->
[1]: ../media/active-directory-privileged-identity-management-configure/Search_PIM.png
[2]: ../media/active-directory-privileged-identity-management-configure/PIM_Dash.png
[3]: ../media/active-directory-identityprotection/29.png
[4]: ../media/active-directory-conditional-access/conditionalaccess-saas-apps.png
