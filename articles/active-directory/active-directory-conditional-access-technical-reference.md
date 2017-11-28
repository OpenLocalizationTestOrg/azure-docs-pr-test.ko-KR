---
title: "Active Directory의 조건부 액세스 기술 참조 aaaAzure | Microsoft Docs"
description: "조건부 액세스 제어를 통해 Azure Active Directory hello 사용자를 인증할 때 및 toohello 응용 프로그램 액세스를 허용 하기 전에 선택 hello 특정 상태를 확인 합니다. 이러한 조건이 충족 되 면 hello 사용자가 인증 되 고 toohello 응용 프로그램 액세스를 허용 합니다."
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
ms.openlocfilehash: ee201405d1d17f130607a95bf455b60cd222dd0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a><span data-ttu-id="5908e-104">Azure Active Directory 조건부 액세스 기술 참조</span><span class="sxs-lookup"><span data-stu-id="5908e-104">Azure Active Directory Conditional Access technical reference</span></span>

## <a name="services-enabled-with-conditional-access"></a><span data-ttu-id="5908e-105">조건부 액세스로 설정된 서비스</span><span class="sxs-lookup"><span data-stu-id="5908e-105">Services enabled with conditional access</span></span>

<span data-ttu-id="5908e-106">조건부 액세스 규칙은 다양한 Azure AD 응용 프로그램 종류에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-106">Conditional Access rules are supported across various Azure AD application types.</span></span> <span data-ttu-id="5908e-107">이 목록에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-107">This list includes:</span></span>


* <span data-ttu-id="5908e-108">응용 프로그램에 등록 된 hello Azure 응용 프로그램 프록시</span><span class="sxs-lookup"><span data-stu-id="5908e-108">Applications registered with hello Azure Application Proxy</span></span>
* <span data-ttu-id="5908e-109">Azure 원격 앱</span><span class="sxs-lookup"><span data-stu-id="5908e-109">Azure Remote App</span></span>
* <span data-ttu-id="5908e-110">Azure AD에 등록된 개발 LOB(기간 업무) 및 다중 테넌트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="5908e-110">Developed line of business and multi-tenant applications registered with Azure AD</span></span>
* <span data-ttu-id="5908e-111">Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="5908e-111">Dynamics CRM</span></span>
* <span data-ttu-id="5908e-112">Hello Azure AD 응용 프로그램 갤러리에서 페더레이션된 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="5908e-112">Federated applications from hello Azure AD application gallery</span></span>
* <span data-ttu-id="5908e-113">Microsoft Office 365 Yammer</span><span class="sxs-lookup"><span data-stu-id="5908e-113">Microsoft Office 365 Yammer</span></span>
* <span data-ttu-id="5908e-114">Microsoft Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="5908e-114">Microsoft Office 365 Exchange Online</span></span>
* <span data-ttu-id="5908e-115">Microsoft Office 365 SharePoint Online(비즈니스용 OneDrive 포함)</span><span class="sxs-lookup"><span data-stu-id="5908e-115">Microsoft Office 365 SharePoint Online (includes OneDrive for Business)</span></span>
* <span data-ttu-id="5908e-116">Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="5908e-116">Microsoft Power BI</span></span> 
* <span data-ttu-id="5908e-117">Hello Azure AD 응용 프로그램 갤러리에서 암호 SSO 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="5908e-117">Password SSO applications from hello Azure AD application gallery</span></span>
* <span data-ttu-id="5908e-118">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="5908e-118">Visual Studio Team Services</span></span>
* <span data-ttu-id="5908e-119">Microsoft 팀</span><span class="sxs-lookup"><span data-stu-id="5908e-119">Microsoft Teams</span></span>









## <a name="enable-access-rules"></a><span data-ttu-id="5908e-120">액세스 규칙 사용</span><span class="sxs-lookup"><span data-stu-id="5908e-120">Enable access rules</span></span>
<span data-ttu-id="5908e-121">각 규칙을 응용 프로그램 단위로 사용하거나 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-121">Each rule can be enabled or disabled on a per application bases.</span></span> <span data-ttu-id="5908e-122">규칙은 때 **ON** 사용할 수 있고 hello 응용 프로그램에 액세스 하는 사용자가 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-122">When rules are **ON** they will be enabled and enforced for users accessing hello application.</span></span> <span data-ttu-id="5908e-123">공백 문자가 있는 경우 **OFF** 영향 hello 사용자가 아닌가 환경에 로그인 하 고 사용 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-123">When they are **OFF** they will not be used and will not impact hello users sign in experience.</span></span>

## <a name="applying-rules-toospecific-users"></a><span data-ttu-id="5908e-124">규칙 toospecific 사용자가 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-124">Applying rules toospecific users</span></span>
<span data-ttu-id="5908e-125">규칙 적용된 toospecific 유형의 설정 하 여 보안 그룹에 따라 사용자가 될 수 있습니다 **적용 대상**합니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-125">Rules can be applied toospecific sets of users based on security group by setting **Apply To**.</span></span> <span data-ttu-id="5908e-126">**적용 대상** 너무 설정할 수 있습니다**모든 사용자에 게** 또는 **그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-126">**Apply To** can be set too**All Users** or **Groups**.</span></span> <span data-ttu-id="5908e-127">설정 된 경우 너무**모든 사용자에 게** hello 규칙이 tooany 사용자 액세스 toohello 응용 프로그램에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-127">When set too**All Users** hello rules will apply tooany user with access toohello application.</span></span> <span data-ttu-id="5908e-128">hello **그룹** 특정 보안 및 배포 그룹 toobe 선택 옵션을 사용 하면 규칙이 이러한 그룹에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-128">hello **Groups** option allows specific security and distribution groups toobe selected, rules will only be enforced for these groups.</span></span>

<span data-ttu-id="5908e-129">일반적 이기는 규칙을 배포할 때는 toofirst 파일럿 그룹의 구성원 인 사용자가 제한적으로 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-129">When deploying a rule,  it is common toofirst apply it a limited set of users, that are members of a piloting groups.</span></span> <span data-ttu-id="5908e-130">너무 완료 hello 규칙을 적용할 수 면**모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-130">Once complete hello rule can be applied too**All Users**.</span></span> <span data-ttu-id="5908e-131">이렇게 하면 hello 규칙 toobe hello 조직의 모든 사용자에 대해 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-131">This will cause hello rule toobe enforced for all users in hello organization.</span></span>

<span data-ttu-id="5908e-132">그룹을 선택할 수 있습니다도 hello를 사용 하 여 정책에서 제외 해야 **제외한** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-132">Select groups may also be exempted from policy using hello **Except** option.</span></span> <span data-ttu-id="5908e-133">제외 옵션으로 선택한 그룹의 모든 멤버는 포함되는 그룹에 표시되더라도 제외됩니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-133">Any members of these groups will be exempted even if they appear in an included group.</span></span>

## <a name="at-work-networks"></a><span data-ttu-id="5908e-134">"회사" 네트워크</span><span class="sxs-lookup"><span data-stu-id="5908e-134">“At work” networks</span></span>
<span data-ttu-id="5908e-135">Azure AD에서 구성 된 신뢰할 수 있는 IP 주소 범위에 의존 하는 "회사"에서 네트워크를 사용 하는 조건부 액세스 규칙 또는 AD FS에서 클레임 "내부 corpnet" hello 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-135">Conditional access rules that use an “At work” network, rely on trusted IP address ranges that have been configured in Azure AD, or use of hello "inside corpnet" claim from AD FS.</span></span> <span data-ttu-id="5908e-136">이러한 규칙에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-136">These rules include:</span></span>

* <span data-ttu-id="5908e-137">회사에 있지 않을 때 다단계 인증 필요</span><span class="sxs-lookup"><span data-stu-id="5908e-137">Require multi-factor authentication when not at work</span></span>
* <span data-ttu-id="5908e-138">회사에 있지 않을 때 액세스 차단</span><span class="sxs-lookup"><span data-stu-id="5908e-138">Block access when not at work</span></span>

<span data-ttu-id="5908e-139">“회사” 네트워크 지정 옵션</span><span class="sxs-lookup"><span data-stu-id="5908e-139">Options for specifiying “at work” networks</span></span>

1. <span data-ttu-id="5908e-140">Hello에 신뢰할 수 있는 IP 주소 범위 구성 [multi-factor authentication 구성 페이지](../multi-factor-authentication/multi-factor-authentication-whats-next.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-140">Configure trusted IP address ranges in hello [multi-factor authentication configuration page](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span></span> <span data-ttu-id="5908e-141">조건부 액세스 정책 각 인증 요청과 토큰 발급 tooevaluate 규칙에 구성 된 hello 범위를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-141">Conditional Access policy will use hello configured ranges on each authentication request and token issuance tooevaluate rules.</span></span> 
2. <span data-ttu-id="5908e-142">회사 네트워크 클레임 내 hello 사용 구성, AD FS를 사용 하는 페더레이션된 디렉터리와이 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-142">Configure use of hello inside corpnet claim, this option can be used with federated directories, using AD FS.</span></span> <span data-ttu-id="5908e-143">회사 네트워크 클레임 내 hello에 대 한 자세한 toolearn 참조 [Tusted Ip](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips)합니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-143">toolearn more about hello inside corpnet claims, see [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="rules-based-on-application-sensitivity"></a><span data-ttu-id="5908e-144">응용 프로그램 민감도에 기반한 규칙</span><span class="sxs-lookup"><span data-stu-id="5908e-144">Rules based on application sensitivity</span></span>
<span data-ttu-id="5908e-145">규칙은 hello 귀중 서비스 toobe 액세스 tooother 서비스 영향을 주지 않고 보안을 허용 하는 응용 프로그램 단위로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-145">Rules are configured per application allowing hello high value services toobe secured without impacting access tooother services.</span></span> <span data-ttu-id="5908e-146">Hello에 조건부 액세스 규칙을 구성할 수 있습니다 **구성** hello 응용 프로그램을 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-146">Conditional access rules can be configured on hello  **Configure** tab of hello application.</span></span> 

<span data-ttu-id="5908e-147">현재 제공되는 규칙은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-147">Rules currently offered:</span></span>

* <span data-ttu-id="5908e-148">**다단계 인증 필요**</span><span class="sxs-lookup"><span data-stu-id="5908e-148">**Require multi-factor authentication**</span></span>
  
  * <span data-ttu-id="5908e-149">이 정책이 적용 된 toowill 인지 하는 모든 사용자가 적어도 한 번에 다단계 인증을 통해 필요한 tooauthenticate 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-149">All users that this policy is applied toowill be required tooauthenticate via multi-factor authentication at least once.</span></span>
* <span data-ttu-id="5908e-150">**회사에 있지 않을 때 다단계 인증 필요**</span><span class="sxs-lookup"><span data-stu-id="5908e-150">**Require multi-factor authentication when not at work**</span></span>
  
  * <span data-ttu-id="5908e-151">이 정책이 적용 된 경우 비 작업 원격 위치에서 hello 서비스에 액세스할 경우 모든 사용자가 한 번 이상 수행 필요한 toohave 다단계 인증을 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-151">If this policy is applied, all users will be required toohave performed multi-factor authentication at least once if they access hello service from a non-work remote location.</span></span> <span data-ttu-id="5908e-152">작업 tooremote 위치에서 이동 하는 경우 hello 서비스에 액세스할 때 필요한 tooperform 다단계 인증 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-152">If they move from a work tooremote location, they will be required tooperform multifactor authentication when accessing hello service.</span></span>
* <span data-ttu-id="5908e-153">**회사에 있지 않을 때 액세스 차단**</span><span class="sxs-lookup"><span data-stu-id="5908e-153">**Block access when not at work**</span></span> 
  
  * <span data-ttu-id="5908e-154">사용자가 작업 tooa 원격 위치에서 이동, 이면 hello 정책 ""이 아닐 때 작업 액세스 차단 적용 된 toothem 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-154">When users move from work tooa remote location, they will be blocked if hello "Block access when not at work" policy is applied toothem.</span></span>  <span data-ttu-id="5908e-155">회사에 있을 때에는 액세스가 다시 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5908e-155">They will be re-allowed access when at a work location.</span></span>

## <a name="related-topics"></a><span data-ttu-id="5908e-156">관련된 항목</span><span class="sxs-lookup"><span data-stu-id="5908e-156">Related topics</span></span>
* [<span data-ttu-id="5908e-157">연결 된 Active Directory tooAzure tooOffice 365 및 기타 응용 프로그램 액세스 보안</span><span class="sxs-lookup"><span data-stu-id="5908e-157">Securing access tooOffice 365 and other apps connected tooAzure Active Directory</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="5908e-158">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="5908e-158">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

