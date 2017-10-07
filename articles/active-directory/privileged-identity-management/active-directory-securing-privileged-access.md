---
title: "Azure AD에서 권한 있는 액세스 aaaSecuring | Microsoft Docs"
description: "Hello를 설명 하는 항목에서는 Azure, Azure Active Directory와 Microsoft 온라인 서비스에서 권한 있는 액세스를 보호 하기 위한 취급 합니다."
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
ms.openlocfilehash: 694835dc5c41640673dbd996d44b0d1f217220de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-privileged-access-in-azure-ad"></a><span data-ttu-id="2e90a-103">Azure AD에서 권한 있는 액세스 보안</span><span class="sxs-lookup"><span data-stu-id="2e90a-103">Securing privileged access in Azure AD</span></span>
<span data-ttu-id="2e90a-104">권한 있는 액세스 보안이 중요 한 첫 번째 단계 toohelp 최신 조직에서 비즈니스 자산을 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e90a-104">Securing privileged access is a critical first step toohelp protect business assets in a modern organization.</span></span> <span data-ttu-id="2e90a-105">권한 있는 계정은 IT 시스템을 운영하고 관리하는 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="2e90a-105">Privileged accounts are accounts that administer and manage IT systems.</span></span> <span data-ttu-id="2e90a-106">사이버 공격자가 이러한 계정 toogain 액세스 tooan 조직 데이터와 시스템 대상합니다.</span><span class="sxs-lookup"><span data-stu-id="2e90a-106">Cyber-attackers target these accounts toogain access tooan organization’s data and systems.</span></span> <span data-ttu-id="2e90a-107">toosecure 특권 수준의 액세스, hello 계정 격리 해야 및 hello 위험은에서 시스템 tooa 악의적인 사용자가을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e90a-107">toosecure privileged access, you should isolate hello accounts and systems from hello risk of being exposed tooa malicious user.</span></span>

<span data-ttu-id="2e90a-108">더 많은 사용자는 클라우드 서비스를 통해 tooget 권한 있는 액세스를 시작 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2e90a-108">More users are starting tooget privileged access through cloud services.</span></span> <span data-ttu-id="2e90a-109">여기에는 Office365의 전역 관리자, Azure 구독 관리자 및 SaaS 앱 또는 VM에서 관리 액세스 권한이 있는 사용자가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e90a-109">This can include global administrators of Office365, Azure subscription administrators, and users who have administrative access in VMs or on SaaS apps.</span></span>

<span data-ttu-id="2e90a-110">[권한 있는 액세스 보안](https://technet.microsoft.com/library/mt631194.aspx)에서 이 로드맵을 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2e90a-110">Microsoft recommends you follow this roadmap on [Securing Privileged Access](https://technet.microsoft.com/library/mt631194.aspx).</span></span>

<span data-ttu-id="2e90a-111">Azure Active Directory, Office 365 또는 다른 Microsoft 서비스 및 응용 프로그램을 사용하는 고객의 경우 이러한 원칙은 Active Directory 또는 Azure Active Directory에서 사용자 계정을 관리하고 인증하는지 여부에 관계없이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e90a-111">For customers using Azure Active Directory, Office 365, or other Microsoft services and applications, these principles apply whether user accounts are managed and authenticated by Active Directory or in Azure Active Directory.</span></span> <span data-ttu-id="2e90a-112">hello 다음 섹션에서는 대 한 자세한 내용은 Azure AD 기능 toosupport 권한 있는 액세스를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e90a-112">hello following sections provide more information on Azure AD features toosupport securing privileged access.</span></span>

## <a name="azure-multi-factor-authentication"></a><span data-ttu-id="2e90a-113">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="2e90a-113">Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="2e90a-114">관리자 인증 tooincrease hello 보안, 권한 부여 하기 전에 2 단계 인증을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e90a-114">tooincrease hello security of administrator authentication, you should require two-step verification before granting privileges.</span></span> <span data-ttu-id="2e90a-115">2 단계 인증은 되었음을 확인 하는 방법을 보다 더 사용자 이름 및 암호를 hello 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e90a-115">Two-step verification is a method of verifying who you are that requires hello use of more than just a username and password.</span></span> <span data-ttu-id="2e90a-116">보안 toouser 로그인 및 트랜잭션에 두 번째 계층을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2e90a-116">It provides a second layer of security toouser sign-ins and transactions.</span></span>

<span data-ttu-id="2e90a-117">Azure Multi-factor Authentication (MFA)는 Microsoft의 2 단계 확인 솔루션는 데 도움이 되는 간단한 로그인 프로세스에 대 한 사용자 요구를 충족 하면서 액세스 toodata 및 응용 프로그램 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e90a-117">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution, which helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="2e90a-118">다음과 같이 다양하고 손쉬운 인증 옵션을 통해 강력한 인증을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2e90a-118">It delivers strong authentication via a range of easy verification options including:</span></span>

- <span data-ttu-id="2e90a-119">전화 통화</span><span class="sxs-lookup"><span data-stu-id="2e90a-119">phone calls</span></span>
- <span data-ttu-id="2e90a-120">문자 메시지</span><span class="sxs-lookup"><span data-stu-id="2e90a-120">text messages</span></span>
- <span data-ttu-id="2e90a-121">모바일 앱 알림</span><span class="sxs-lookup"><span data-stu-id="2e90a-121">mobile app notifications</span></span>
- <span data-ttu-id="2e90a-122">모바일 앱 확인 코드</span><span class="sxs-lookup"><span data-stu-id="2e90a-122">mobile app verification codes</span></span>
- <span data-ttu-id="2e90a-123">타사 OATH 토큰</span><span class="sxs-lookup"><span data-stu-id="2e90a-123">third-party OATH tokens</span></span>

<span data-ttu-id="2e90a-124">Azure Multi-factor Authentication의 작동 방식에 대 한 개요 비디오를 따라 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="2e90a-124">For an overview of how Azure Multi-Factor Authentication works see hello following video:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]

<span data-ttu-id="2e90a-125">자세한 내용은 [Office 365용 MFA 및 Azure용 MFA](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e90a-125">For more information, see [MFA for Office 365 and MFA for Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).</span></span>

## <a name="time-bound-privileges"></a><span data-ttu-id="2e90a-126">시간 제한 권한</span><span class="sxs-lookup"><span data-stu-id="2e90a-126">Time-bound privileges</span></span>
<span data-ttu-id="2e90a-127">일부 조직에서는 높은 권한이 있는 역할의 사용자가 너무 많은 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e90a-127">Some organizations may find that they have too many users in highly privileged roles.</span></span> <span data-ttu-id="2e90a-128">사용자 추가 되었을 toosign는 서비스와 같은 특정 작업에 대 한 toohello 역할 있지만 해당 권한을 나중에 자주 사용 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="2e90a-128">A user might have been added toohello role for a particular activity, like toosign up for a service, but didn't use those privileges frequently afterward.</span></span>

<span data-ttu-id="2e90a-129">권한 toolower hello 노출 시간 제한 사용자 tooonly "just in time"의 권한 맡 사용에 대 한 가시성을 증가 하 고 JIT (), tooperform 작업 해야 할 때입니다.</span><span class="sxs-lookup"><span data-stu-id="2e90a-129">toolower hello exposure time of privileges and increase your visibility into their use, limit users tooonly taking on their privileges "just in time" (JIT), when they need tooperform a task.</span></span> <span data-ttu-id="2e90a-130">Azure Active Directory 및 Microsoft Online Services에서 [Azure AD PIM(Privileged Identity Management)](http://aka.ms/AzurePIM)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e90a-130">For Azure Active Directory and Microsoft Online Services, you can use [Azure AD Privileged Identity Management (PIM)](http://aka.ms/AzurePIM).</span></span>

![PIM 대시보드][2]

## <a name="attack-detection"></a><span data-ttu-id="2e90a-132">공격 탐지</span><span class="sxs-lookup"><span data-stu-id="2e90a-132">Attack detection</span></span>
<span data-ttu-id="2e90a-133">[Azure Active Directory ID 보호](../active-directory-identityprotection.md)는 조직의 ID에 영향을 주는 위험 이벤트와 잠재적 취약성에 대한 통합된 뷰를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2e90a-133">[Azure Active Directory Identity Protection](../active-directory-identityprotection.md) provides a consolidated view into risk events and potential vulnerabilities affecting your organization’s identities.</span></span> <span data-ttu-id="2e90a-134">위험 이벤트에 따라, Identity Protection을 각 사용자에 대 한 사용자 위험 수준을 계산, tooconfigure 위험 기반 정책 tooautomatically 보호 hello 수 있게 해 주는 조직의 id입니다.</span><span class="sxs-lookup"><span data-stu-id="2e90a-134">Based on risk events, Identity Protection calculates a user risk level for each user, enabling you tooconfigure risk-based policies tooautomatically protect hello identities of your organization.</span></span> <span data-ttu-id="2e90a-135">Azure Active Directory 및 EMS에서 제공 하는 다른 조건부 액세스 제어와 함께 이러한 정책에 자동으로 hello 사용자를 차단 하거나 암호 재설정 및 다단계 인증 적용을 포함 하는 제안 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e90a-135">These policies, along with other conditional access controls provided by Azure Active Directory and EMS, can automatically block hello user or offer suggestions that include password resets and multi-factor authentication enforcement.</span></span>

![Azure AD ID 보호][3]

## <a name="conditional-access"></a><span data-ttu-id="2e90a-137">조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="2e90a-137">Conditional access</span></span>
<span data-ttu-id="2e90a-138">조건부 액세스 제어를 통해 Azure Active Directory tooan 응용 프로그램 액세스를 허용 하기 전에 사용자를 인증할 때 선택 하는 hello 특정 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e90a-138">With conditional access control, Azure Active Directory checks hello specific conditions you choose when authenticating a user, before allowing access tooan application.</span></span> <span data-ttu-id="2e90a-139">이러한 조건이 충족 되 면 hello 사용자가 인증 되 고 toohello 응용 프로그램 액세스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e90a-139">Once those conditions are met, hello user is authenticated and allowed access toohello application.</span></span>

![MFA를 사용하는 조건부 액세스 규칙 설정][4]

## <a name="related-articles"></a><span data-ttu-id="2e90a-141">관련된 문서</span><span class="sxs-lookup"><span data-stu-id="2e90a-141">Related articles</span></span>
* <span data-ttu-id="2e90a-142">[Azure Multi-Factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md) 사용</span><span class="sxs-lookup"><span data-stu-id="2e90a-142">Enable [Azure Multi-Factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)</span></span>
* <span data-ttu-id="2e90a-143">[Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md) 사용</span><span class="sxs-lookup"><span data-stu-id="2e90a-143">Enable [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)</span></span>
* <span data-ttu-id="2e90a-144">[Azure AD ID 보호](../active-directory-identityprotection.md) 사용</span><span class="sxs-lookup"><span data-stu-id="2e90a-144">Enable [Azure AD Identity Protection](../active-directory-identityprotection.md)</span></span>
* <span data-ttu-id="2e90a-145">[조건부 액세스 제어](../active-directory-conditional-access.md) 사용</span><span class="sxs-lookup"><span data-stu-id="2e90a-145">Enable [conditional access controls](../active-directory-conditional-access.md)</span></span>

<span data-ttu-id="2e90a-146">완벽 한 보안 로드맵 구축에 대 한 자세한 내용은 hello의 hello "고객의 책임 및 로드맵" 섹션을 참조 [Enterprise 설계자를 위해 Microsoft 클라우드 보안](http://aka.ms/securecustomer) 문서.</span><span class="sxs-lookup"><span data-stu-id="2e90a-146">For more information on building a complete security roadmap, see hello “Customer responsibilities and roadmap” section of hello [Microsoft Cloud Security for Enterprise Architects](http://aka.ms/securecustomer) document.</span></span> <span data-ttu-id="2e90a-147">이 항목의 모든 Microsoft 서비스 tooassist 참여에 대 한 자세한 내용은 Microsoft 담당자에 게 문의 하거나 방문 우리의 [사이버 안보 솔루션 페이지](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e90a-147">For more information on engaging Microsoft services tooassist with any of these topics, contact your Microsoft representative or visit our [Cybersecurity solutions page](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).</span></span>

<!--Image references-->
[1]: ../media/active-directory-privileged-identity-management-configure/Search_PIM.png
[2]: ../media/active-directory-privileged-identity-management-configure/PIM_Dash.png
[3]: ../media/active-directory-identityprotection/29.png
[4]: ../media/active-directory-conditional-access/conditionalaccess-saas-apps.png
