---
title: "SaaS 앱에 대한 Azure 조건부 액세스 | Microsoft Docs"
description: "Azure AD의 조건부 액세스를 사용하면 응용 프로그램별 다단계 인증 액세스 규칙 및 신뢰할 수 있는 네트워크에 없는 사용자에 대한 액세스 차단 기능을 구성할 수 있습니다. "
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 51a1ee61-3ffe-4f65-b8de-ff21903e1e74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: efaa70467346e910a78a63d182041029bb34b1cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="getting-started-with-azure-active-directory-conditional-access"></a><span data-ttu-id="ce3bf-103">Azure Active Directory 조건부 액세스 시작</span><span class="sxs-lookup"><span data-stu-id="ce3bf-103">Getting started with Azure Active Directory Conditional Access</span></span>
<span data-ttu-id="ce3bf-104">[SaaS](https://azure.microsoft.com/overview/what-is-saas/) 앱과 Azure AD 연결 앱에 대한 Azure Active Directory 조건부 액세스는 그룹, 위치 및 응용 프로그램 민감도에 따라 조건부 액세스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-104">Azure Active Directory Conditional Access for [SaaS](https://azure.microsoft.com/overview/what-is-saas/) apps and Azure AD connected apps lets you configure conditional access based on group, location, and application sensitivity.</span></span> 

<span data-ttu-id="ce3bf-105">응용 프로그램 민감도를 기반으로 하는 조건부 액세스를 통해 응용 프로그램당 Multi-Factor Authentication(MFA) 액세스 규칙을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-105">With conditional access based on application sensitivity, you can set multi-factor authentication (MFA) access rules per application.</span></span> <span data-ttu-id="ce3bf-106">응용 프로그램당 MFA는 신뢰할 수 있는 네트워크에 없는 사용자에 대한 액세스 차단 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-106">MFA per application provides the ability to block access for users who are not on a trusted network.</span></span> <span data-ttu-id="ce3bf-107">응용 프로그램에 할당된 모든 사용자 또는 지정된 보안 그룹 내의 사용자에 제한적으로 MFA 규칙을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-107">You can apply MFA rules to all users that are assigned to the application, or only for users within specified security groups.</span></span>  <span data-ttu-id="ce3bf-108">조직 네트워크 내부에 있는 IP 주소에서 응용 프로그램에 액세스하는 경우에는 MFA 요구 사항에서 제외될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-108">Users may be excluded from the MFA requirement if they are accessing the application from an IP address that is inside the organization’s network.</span></span>

<span data-ttu-id="ce3bf-109">이러한 기능은 Azure Active Directory Premium 라이선스를 구입한 고객에게 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-109">These capabilities will be available to customers that have purchased an Azure Active Directory Premium license.</span></span>

## <a name="scenario-prerequisites"></a><span data-ttu-id="ce3bf-110">시나리오 필수 조건</span><span class="sxs-lookup"><span data-stu-id="ce3bf-110">Scenario prerequisites</span></span>
* <span data-ttu-id="ce3bf-111">Azure Active Directory Premium에 대한 라이선스</span><span class="sxs-lookup"><span data-stu-id="ce3bf-111">License for Azure Active Directory Premium</span></span>
* <span data-ttu-id="ce3bf-112">페더레이션 또는 관리되는 Azure Active Directory 테넌트</span><span class="sxs-lookup"><span data-stu-id="ce3bf-112">Federated or managed Azure Active Directory tenant</span></span>
* <span data-ttu-id="ce3bf-113">페더레이션된 테넌트가 해당 다단계 인증의 사용 요구</span><span class="sxs-lookup"><span data-stu-id="ce3bf-113">Federated tenants require that multi-factor authentication be enabled.</span></span>

## <a name="configure-per-application-access-rules"></a><span data-ttu-id="ce3bf-114">응용 프로그램별 액세스 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="ce3bf-114">Configure per-application access rules</span></span>
<span data-ttu-id="ce3bf-115">이 섹션에서는 응용 프로그램별 액세스 규칙을 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-115">This section describes how to configure per-application access rules.</span></span>

1. <span data-ttu-id="ce3bf-116">Azure AD의 전역 관리자 계정을 사용하여 Azure 클래식 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-116">Sign in to the Azure classic portal Using an account that is a global administrator for Azure AD.</span></span>
2. <span data-ttu-id="ce3bf-117">왼쪽 창에서 **Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-117">On the left pane, select **Active Directory**.</span></span>
3. <span data-ttu-id="ce3bf-118">디렉터리 탭에서 해당 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-118">On the Directory tab, select your directory.</span></span>
4. <span data-ttu-id="ce3bf-119">**응용 프로그램** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-119">Select the **Applications** tab.</span></span>
5. <span data-ttu-id="ce3bf-120">규칙을 설정할 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-120">Select the application that the rule will be set for.</span></span>
6. <span data-ttu-id="ce3bf-121">**구성** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-121">Select the **Configure** tab.</span></span>
7. <span data-ttu-id="ce3bf-122">액세스 규칙 섹션까지 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-122">Scroll down to the access rules section.</span></span> <span data-ttu-id="ce3bf-123">원하는 액세스 규칙을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-123">Select the desired access rule.</span></span>
8. <span data-ttu-id="ce3bf-124">규칙을 적용할 사용자를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-124">Specify the users the rule will apply to.</span></span>
9. <span data-ttu-id="ce3bf-125">**사용**을 선택하여 정책을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-125">Enable the policy by selecting **Enabled to be On**.</span></span>

## <a name="understanding-access-rules"></a><span data-ttu-id="ce3bf-126">액세스 규칙 이해</span><span class="sxs-lookup"><span data-stu-id="ce3bf-126">Understanding access rules</span></span>
<span data-ttu-id="ce3bf-127">이 섹션에서는 Azure 조건부 응용 프로그램 액세스에서 지원되는 액세스 규칙에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-127">This section gives a detailed description of the access rules supported in the Azure Conditional Application Access.</span></span>

### <a name="specifying-the-users-the-access-rules-apply-to"></a><span data-ttu-id="ce3bf-128">액세스 규칙이 적용되는 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="ce3bf-128">Specifying the users the access rules apply to</span></span>
<span data-ttu-id="ce3bf-129">기본적으로 정책은 응용 프로그램에 대한 액세스 권한이 있는 모든 사용자에게 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-129">By default the policy will apply to all users that have access to the application.</span></span> <span data-ttu-id="ce3bf-130">그러나 지정된 보안 그룹의 구성원인 사용자로만 정책을 제한할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-130">However, you can also restrict the policy to users that are members of the specified security groups.</span></span> <span data-ttu-id="ce3bf-131">**그룹 추가** 단추는 그룹 선택 대화 상자에서 액세스 규칙을 적용할 그룹을 하나 이상 선택하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-131">The **Add Group** button is used to select one or more groups from the group selection dialog that the access rule will apply to.</span></span> <span data-ttu-id="ce3bf-132">이 대화 상자는 선택한 그룹을 제거하는 데 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-132">This dialog can also be used to remove selected groups.</span></span> <span data-ttu-id="ce3bf-133">그룹에 적용할 규칙이 선택되면 액세스 규칙이 지정된 보안 그룹 중 하나에 속한 사용자에 대해서만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-133">When the rules are selected to apply to Groups, the access rules will only be enforced for users that belong to one of the specified security groups.</span></span>

<span data-ttu-id="ce3bf-134">**제외** 옵션을 선택하고 하나 이상의 그룹을 지정하여 정책에서 보안 그룹을 명시적으로 제외할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-134">Security groups can also be explicitly excluded from the policy by selecting the **Except** option and specifying one or more groups.</span></span> <span data-ttu-id="ce3bf-135">**제외** 목록에 있는 그룹의 구성원인 사용자는 액세스 규칙이 적용되는 그룹의 구성원인 경우에도 다단계 인증 요구 사항이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-135">Users that are a member of a group in the **Except** list will not be subject to the multi-factor authentication requirement, even if they are a member of a group that the access rule applies to.</span></span>
<span data-ttu-id="ce3bf-136">아래 표시된 액세스 규칙의 경우 관리자 그룹의 모든 사용자가 응용 프로그램에 액세스할 때 다단계 인증을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-136">The access rule shown below will require all users in the Managers group to use multi-factor authentication when accessing the application.</span></span>

![MFA를 사용하는 조건부 액세스 규칙 설정](./media/active-directory-conditional-access-azuread-connected-apps/conditionalaccess-saas-apps.png)

## <a name="conditional-access-rules-with-mfa"></a><span data-ttu-id="ce3bf-138">MFA를 사용하는 조건부 액세스 규칙</span><span class="sxs-lookup"><span data-stu-id="ce3bf-138">Conditional Access Rules with MFA</span></span>
<span data-ttu-id="ce3bf-139">사용자가 사용자별 다단계 인증 기능을 사용하여 구성된 경우 사용자에 대한 이 설정이 앱 다단계 인증 규칙과 결합됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-139">If a user has been configured using the per-user multi-factor authentication feature, this setting on the user will combine with the multi-factor authentication rules of the app.</span></span> <span data-ttu-id="ce3bf-140">즉, 사용자별 다단계 인증에 대해 구성된 사용자는 응용 프로그램 다단계 인증 규칙에서 제외된 경우에도 다단계 인증을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-140">This means a user that has been configured for per-user multi-factor authentication will be required to perform multi-factor authentication even if they have been exempted from the application multi-factor authentication rules.</span></span> <span data-ttu-id="ce3bf-141">다단계 인증 및 사용자별 설정에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-141">Learn more about multi-factor authentication and per-user settings.</span></span>

### <a name="access-rule-options"></a><span data-ttu-id="ce3bf-142">액세스 규칙 옵션</span><span class="sxs-lookup"><span data-stu-id="ce3bf-142">Access rule options</span></span>
<span data-ttu-id="ce3bf-143">다음과 같은 옵션이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-143">The following options are supported:</span></span>

* <span data-ttu-id="ce3bf-144">**다단계 인증 요구**: 액세스 규칙이 적용되는 사용자는 정책이 적용되는 응용 프로그램에 액세스하기 전에 다단계 인증을 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-144">**Require multi-factor authentication**: The users to whom the access rules apply to, will be required to complete multi-factor authentication before accessing the application that the policy applies to.</span></span>
* <span data-ttu-id="ce3bf-145">**회사에 있지 않을 때 Multi-Factor Authentication 요구**: 신뢰할 수 있는 IP 주소에서 액세스하는 사용자는 Multi-Factor Authentication을 수행하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-145">**Require multi-factor authentication when not at work**: A user that is coming from a trusted IP address will not be required to perform multi-factor authentication.</span></span> <span data-ttu-id="ce3bf-146">신뢰되는 IP 주소 범위는 Multi-Factor Authentication 설정 페이지에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-146">The trusted IP address ranges can be configured on the multi-factor authentication settings page.</span></span>
* <span data-ttu-id="ce3bf-147">**회사에 있지 않을 때 액세스 차단**: 신뢰할 수 있는 IP 주소에서 액세스하는 사용자가 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-147">**Block access when not at work**: A user that is not coming from a trusted IP address will be blocked.</span></span> <span data-ttu-id="ce3bf-148">신뢰되는 IP 주소 범위는 Multi-Factor Authentication 설정 페이지에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-148">The trusted IP address ranges can be configured on the multi-factor authentication settings page.</span></span>

### <a name="setting-rule-status"></a><span data-ttu-id="ce3bf-149">규칙 상태 설정</span><span class="sxs-lookup"><span data-stu-id="ce3bf-149">Setting rule status</span></span>
<span data-ttu-id="ce3bf-150">액세스 규칙 상태를 통해 규칙을 켜고 끌 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-150">Access rule status allows turning the rules on or off.</span></span> <span data-ttu-id="ce3bf-151">액세스 규칙이 꺼져 있으면 다단계 인증 요구 사항이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-151">When the access rules are off, the multi-factor authentication requirement is not enforced.</span></span>

### <a name="access-rule-evaluation"></a><span data-ttu-id="ce3bf-152">액세스 규칙 평가</span><span class="sxs-lookup"><span data-stu-id="ce3bf-152">Access rule evaluation</span></span>
<span data-ttu-id="ce3bf-153">사용자가 OAuth 2.0, OpenID Connect, SAML 또는 WS-Federation을 사용하는 페더레이션된 응용 프로그램에 액세스할 때 액세스 규칙이 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-153">Access rules are evaluated when a user accesses a federated application that uses OAuth 2.0, OpenID Connect, SAML or WS-Federation.</span></span> <span data-ttu-id="ce3bf-154">또한 액세스 규칙은 OAuth 2.0 및 OpenID Connect가 새로 고침 토큰을 사용하여 액세스 토큰을 얻을 때 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-154">In addition, access rules are evaluated when the OAuth 2.0 and OpenID Connect use a refresh token to acquire an access token.</span></span> <span data-ttu-id="ce3bf-155">새로 고침 토큰을 사용할 때 정책 평가에 실패하면 **invalid_grant** 오류가 반환됩니다. 이 오류는 사용자가 클라이언트에 다시 인증해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-155">If policy evaluation fails when a refresh token is used, the error **invalid_grant** will be returned, this indicates the user needs to re-authenticate to the client.</span></span>

### <a name="configure-federation-services-to-provide-multi-factor-authentication"></a><span data-ttu-id="ce3bf-156">다단계 인증을 제공하도록 페더레이션 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="ce3bf-156">Configure federation services to provide multi-factor authentication</span></span>
<span data-ttu-id="ce3bf-157">페더레이션된 테넌트의 경우 MFA를 Azure Active Directory 또는 온-프레미스 AD FS 서버에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-157">For federated tenants, MFA may be performed by Azure Active Directory or by the on-premises AD FS server.</span></span>

<span data-ttu-id="ce3bf-158">기본적으로 MFA는 Azure Active Directory에서 호스트되는 모든 페이지에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-158">By default, MFA will occur at a page hosted by Azure Active Directory.</span></span> <span data-ttu-id="ce3bf-159">온-프레미스에서 MFA를 구성하려면 Windows PowerShell용 Azure AD 모듈을 사용하여 Azure Active Directory에서 **–SupportsMFA** 속성을 **true**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-159">To configure MFA on-premises, the **–SupportsMFA** property must be set to **true** in Azure Active Directory, by using the Azure AD module for Windows PowerShell.</span></span>

<span data-ttu-id="ce3bf-160">다음 예제는 contoso.com 테넌트에서 [Set-MsolDomainFederationSettings cmdlet](https://msdn.microsoft.com/library/azure/dn194088.aspx) 을 사용하여 온-프레미스 MFA를 사용하도록 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-160">The following example shows how to enable on-premises MFA by using the [Set-MsolDomainFederationSettings cmdlet](https://msdn.microsoft.com/library/azure/dn194088.aspx) on the contoso.com tenant:</span></span>

    Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true

<span data-ttu-id="ce3bf-161">이 플래그를 설정하는 것 외에도 페더레이션 테넌트 AD FS 인스턴스에서 다단계 인증을 수행하도록 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-161">In addition to setting this flag, the federated tenant AD FS instance must be configured to perform multi-factor authentication.</span></span> <span data-ttu-id="ce3bf-162">[온-프레미스에 Azure Multi-Factor Authentication을 배포](../multi-factor-authentication/multi-factor-authentication-get-started-server.md)하기 위한 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="ce3bf-162">Follow the instructions for [deploying Azure Multi-Factor Authentication on-premises](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="ce3bf-163">관련 문서</span><span class="sxs-lookup"><span data-stu-id="ce3bf-163">Related Articles</span></span>
* [<span data-ttu-id="ce3bf-164">Azure Active Directory에 연결된 Office 365 및 기타 앱에 대한 액세스 보호</span><span class="sxs-lookup"><span data-stu-id="ce3bf-164">Securing access to Office 365 and other apps connected to Azure Active Directory</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="ce3bf-165">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="ce3bf-165">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

