---
title: "Azure Active Directory 조건부 액세스 기술 참조 | Microsoft Docs"
description: "조건부 액세스 제어를 통해 Azure Active Directory는 사용자를 인증할 때 및 응용 프로그램에 대한 액세스를 허용하기 전에 선택한 특정 조건을 확인합니다. 이러한 조건이 충족되면 사용자가 인증되고 응용 프로그램에 대한 액세스가 허용됩니다."
services: active-directory.
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 56a5bade-7dcc-4dcf-8092-a7d4bf5df3c1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ca16a5399f94fd1ab267e0798cade3fd83f75b13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a><span data-ttu-id="38690-104">Azure Active Directory 조건부 액세스 기술 참조</span><span class="sxs-lookup"><span data-stu-id="38690-104">Azure Active Directory Conditional Access technical reference</span></span>

## <a name="services-enabled-with-conditional-access"></a><span data-ttu-id="38690-105">조건부 액세스로 설정된 서비스</span><span class="sxs-lookup"><span data-stu-id="38690-105">Services enabled with conditional access</span></span>

<span data-ttu-id="38690-106">조건부 액세스 규칙은 다양한 Azure AD 응용 프로그램 종류에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="38690-106">Conditional Access rules are supported across various Azure AD application types.</span></span> <span data-ttu-id="38690-107">이 목록에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="38690-107">This list includes:</span></span>


* <span data-ttu-id="38690-108">Azure 응용 프로그램 프록시에 등록된 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="38690-108">Applications registered with the Azure Application Proxy</span></span>
* <span data-ttu-id="38690-109">Azure 원격 앱</span><span class="sxs-lookup"><span data-stu-id="38690-109">Azure Remote App</span></span>
* <span data-ttu-id="38690-110">Azure AD에 등록된 개발 LOB(기간 업무) 및 다중 테넌트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="38690-110">Developed line of business and multi-tenant applications registered with Azure AD</span></span>
* <span data-ttu-id="38690-111">Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="38690-111">Dynamics CRM</span></span>
* <span data-ttu-id="38690-112">Azure AD 응용 프로그램 갤러리의 페더레이션 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="38690-112">Federated applications from the Azure AD application gallery</span></span>
* <span data-ttu-id="38690-113">Microsoft Office 365 Yammer</span><span class="sxs-lookup"><span data-stu-id="38690-113">Microsoft Office 365 Yammer</span></span>
* <span data-ttu-id="38690-114">Microsoft Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="38690-114">Microsoft Office 365 Exchange Online</span></span>
* <span data-ttu-id="38690-115">Microsoft Office 365 SharePoint Online(비즈니스용 OneDrive 포함)</span><span class="sxs-lookup"><span data-stu-id="38690-115">Microsoft Office 365 SharePoint Online (includes OneDrive for Business)</span></span>
* <span data-ttu-id="38690-116">Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="38690-116">Microsoft Power BI</span></span> 
* <span data-ttu-id="38690-117">Azure AD 응용 프로그램 갤러리의 암호 SSO 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="38690-117">Password SSO applications from the Azure AD application gallery</span></span>
* <span data-ttu-id="38690-118">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="38690-118">Visual Studio Team Services</span></span>
* <span data-ttu-id="38690-119">Microsoft 팀</span><span class="sxs-lookup"><span data-stu-id="38690-119">Microsoft Teams</span></span>









## <a name="enable-access-rules"></a><span data-ttu-id="38690-120">액세스 규칙 사용</span><span class="sxs-lookup"><span data-stu-id="38690-120">Enable access rules</span></span>
<span data-ttu-id="38690-121">각 규칙을 응용 프로그램 단위로 사용하거나 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38690-121">Each rule can be enabled or disabled on a per application bases.</span></span> <span data-ttu-id="38690-122">**설정** 인 경우 규칙을 사용할 수 있으며 응용 프로그램에 액세스하는 사용자에게 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="38690-122">When rules are **ON** they will be enabled and enforced for users accessing the application.</span></span> <span data-ttu-id="38690-123">**해제** 인 경우 규칙을 사용할 수 없으며 사용자 로그인 환경에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38690-123">When they are **OFF** they will not be used and will not impact the users sign in experience.</span></span>

## <a name="applying-rules-to-specific-users"></a><span data-ttu-id="38690-124">특정 사용자에게 규칙 적용</span><span class="sxs-lookup"><span data-stu-id="38690-124">Applying rules to specific users</span></span>
<span data-ttu-id="38690-125">규칙은 **적용 대상**을 설정하여 보안 그룹을 기반으로 특정 사용자 집합에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38690-125">Rules can be applied to specific sets of users based on security group by setting **Apply To**.</span></span> <span data-ttu-id="38690-126">**적용 대상**으로 **모든 사용자** 또는 **그룹**을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38690-126">**Apply To** can be set to **All Users** or **Groups**.</span></span> <span data-ttu-id="38690-127">**모든 사용자** 로 설정하면 규칙은 응용 프로그램에 액세스하는 모든 사용자에게 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="38690-127">When set to **All Users** the rules will apply to any user with access to the application.</span></span> <span data-ttu-id="38690-128">**그룹** 옵션을 통해 특정 보안 및 배포 그룹을 선택할 수 있으며 이러한 그룹에 대해서만 규칙이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="38690-128">The **Groups** option allows specific security and distribution groups to be selected, rules will only be enforced for these groups.</span></span>

<span data-ttu-id="38690-129">규칙을 배포하는 경우 파일럿 그룹의 멤버인 제한된 사용자 집합에 먼저 적용하는 것이 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="38690-129">When deploying a rule,  it is common to first apply it a limited set of users, that are members of a piloting groups.</span></span> <span data-ttu-id="38690-130">완료되면 규칙을 **모든 사용자**에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38690-130">Once complete the rule can be applied to **All Users**.</span></span> <span data-ttu-id="38690-131">이렇게 하면 조직의 모든 사용자에게 규칙이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="38690-131">This will cause the rule to be enforced for all users in the organization.</span></span>

<span data-ttu-id="38690-132">**제외** 옵션을 사용하여 정책에서 제외되도록 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38690-132">Select groups may also be exempted from policy using the **Except** option.</span></span> <span data-ttu-id="38690-133">제외 옵션으로 선택한 그룹의 모든 멤버는 포함되는 그룹에 표시되더라도 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="38690-133">Any members of these groups will be exempted even if they appear in an included group.</span></span>

## <a name="at-work-networks"></a><span data-ttu-id="38690-134">"회사" 네트워크</span><span class="sxs-lookup"><span data-stu-id="38690-134">“At work” networks</span></span>
<span data-ttu-id="38690-135">"회사" 네트워크를 사용하는 조건부 액세스 규칙은 Azure AD에서 구성된 신뢰할 수 있는 IP 주소 범위를 사용하거나 AD FS의 “Corpnet 내부" 클레임을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="38690-135">Conditional access rules that use an “At work” network, rely on trusted IP address ranges that have been configured in Azure AD, or use of the "inside corpnet" claim from AD FS.</span></span> <span data-ttu-id="38690-136">이러한 규칙에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="38690-136">These rules include:</span></span>

* <span data-ttu-id="38690-137">회사에 있지 않을 때 다단계 인증 필요</span><span class="sxs-lookup"><span data-stu-id="38690-137">Require multi-factor authentication when not at work</span></span>
* <span data-ttu-id="38690-138">회사에 있지 않을 때 액세스 차단</span><span class="sxs-lookup"><span data-stu-id="38690-138">Block access when not at work</span></span>

<span data-ttu-id="38690-139">“회사” 네트워크 지정 옵션</span><span class="sxs-lookup"><span data-stu-id="38690-139">Options for specifiying “at work” networks</span></span>

1. <span data-ttu-id="38690-140">신뢰할 수 있는 IP 주소 범위는 [다단계 인증 구성 페이지](../multi-factor-authentication/multi-factor-authentication-whats-next.md)에서 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="38690-140">Configure trusted IP address ranges in the [multi-factor authentication configuration page](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span></span> <span data-ttu-id="38690-141">조건부 액세스 정책은 각 인증 요청 및 토큰 발급의 구성 범위를 사용하여 규칙을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="38690-141">Conditional Access policy will use the configured ranges on each authentication request and token issuance to evaluate rules.</span></span> 
2. <span data-ttu-id="38690-142">Corpnet 내부 클레임을 사용하여 구성합니다. 이 옵션은 AD FS를 이용하여 페더레이트된 디렉터리와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38690-142">Configure use of the inside corpnet claim, this option can be used with federated directories, using AD FS.</span></span> <span data-ttu-id="38690-143">회사 네트워크 내부 클레임에 대한 자세한 내용은 [Tusted IP](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="38690-143">To learn more about the inside corpnet claims, see [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="rules-based-on-application-sensitivity"></a><span data-ttu-id="38690-144">응용 프로그램 민감도에 기반한 규칙</span><span class="sxs-lookup"><span data-stu-id="38690-144">Rules based on application sensitivity</span></span>
<span data-ttu-id="38690-145">다른 서비스에 대한 액세스에 영향을 주지 않고 중요한 서비스의 보안이 유지되도록 허용하는 응용 프로그램 단위로 규칙이 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="38690-145">Rules are configured per application allowing the high value services to be secured without impacting access to other services.</span></span> <span data-ttu-id="38690-146">응용 프로그램의 **구성** 탭에서 조건부 액세스 규칙을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38690-146">Conditional access rules can be configured on the  **Configure** tab of the application.</span></span> 

<span data-ttu-id="38690-147">현재 제공되는 규칙은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="38690-147">Rules currently offered:</span></span>

* <span data-ttu-id="38690-148">**다단계 인증 필요**</span><span class="sxs-lookup"><span data-stu-id="38690-148">**Require multi-factor authentication**</span></span>
  
  * <span data-ttu-id="38690-149">정책이 적용되는 모든 사용자는 다단계 인증을 한 번 이상 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38690-149">All users that this policy is applied to will be required to authenticate via multi-factor authentication at least once.</span></span>
* <span data-ttu-id="38690-150">**회사에 있지 않을 때 다단계 인증 필요**</span><span class="sxs-lookup"><span data-stu-id="38690-150">**Require multi-factor authentication when not at work**</span></span>
  
  * <span data-ttu-id="38690-151">이 정책이 적용되는 경우 모든 사용자는 회사 외부의 원격 위치에서 서비스를 액세스하는 경우 다단계 인증을 한 번 이상 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38690-151">If this policy is applied, all users will be required to have performed multi-factor authentication at least once if they access the service from a non-work remote location.</span></span> <span data-ttu-id="38690-152">회사에서 원격 위치로 이동하는 경우 서비스에 액세스할 때 다단계 인증을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38690-152">If they move from a work to remote location, they will be required to perform multifactor authentication when accessing the service.</span></span>
* <span data-ttu-id="38690-153">**회사에 있지 않을 때 액세스 차단**</span><span class="sxs-lookup"><span data-stu-id="38690-153">**Block access when not at work**</span></span> 
  
  * <span data-ttu-id="38690-154">사용자가 회사에서 원격 위치로 이동할 때 "회사에 있지 않을 때 액세스 차단" 정책이 적용되는 경우 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="38690-154">When users move from work to a remote location, they will be blocked if the "Block access when not at work" policy is applied to them.</span></span>  <span data-ttu-id="38690-155">회사에 있을 때에는 액세스가 다시 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="38690-155">They will be re-allowed access when at a work location.</span></span>

## <a name="related-topics"></a><span data-ttu-id="38690-156">관련된 항목</span><span class="sxs-lookup"><span data-stu-id="38690-156">Related topics</span></span>
* [<span data-ttu-id="38690-157">Azure Active Directory에 연결된 Office 365 및 기타 앱에 대한 액세스 보호</span><span class="sxs-lookup"><span data-stu-id="38690-157">Securing access to Office 365 and other apps connected to Azure Active Directory</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="38690-158">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="38690-158">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

