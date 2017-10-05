---
title: "Azure Active Directory에 대해 인증된 AppSource 가져오는 방법 | Microsoft Docs"
description: "Azure Active Directory에 대해 인증된 응용 프로그램 AppSource 가져오는 방법에 대한 세부 정보."
services: active-directory
documentationcenter: 
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 21206407-49f8-4c0b-84d1-c25e17cd4183
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/03/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: d8e2f8fc19ff879e6a7b632f033fd0ed9d77392a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-get-appsource-certified-for-azure-active-directory"></a><span data-ttu-id="1319c-103">Azure Active Directory에 대해 인증된 AppSource 가져오는 방법</span><span class="sxs-lookup"><span data-stu-id="1319c-103">How to get AppSource Certified for Azure Active Directory</span></span>
<span data-ttu-id="1319c-104">[Microsoft AppSource](https://appsource.microsoft.com/)는 기간 업무 SaaS 응용 프로그램을 검색, 시도 및 관리하는 비즈니스 사용자에 대한 대상입니다(기존 Microsoft SaaS 제품에 대한 독립 실행형 SaaS 및 추가 기능).</span><span class="sxs-lookup"><span data-stu-id="1319c-104">[Microsoft AppSource](https://appsource.microsoft.com/) is a destination for business users to discover, try, and manage line-of-business SaaS applications (standalone SaaS and add-on to existing Microsoft SaaS products).</span></span>

<span data-ttu-id="1319c-105">AppSource에서 독립 실행형 SaaS 응용 프로그램을 나열하려면 응용 프로그램은 Azure Active Directory가 있는 모든 회사 또는 조직의 작업 계정에서 Single Sign-On을 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-105">To list a standalone SaaS application on AppSource, your application must accept single sign-on from work accounts from any company or organization that has Azure Active Directory.</span></span> <span data-ttu-id="1319c-106">로그인 프로세스는 [OpenID Connect](./active-directory-protocols-openid-connect-code.md) 또는 [OAuth 2.0](./active-directory-protocols-oauth-code.md) 프로토콜을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-106">The sign-in process must use the [OpenID Connect](./active-directory-protocols-openid-connect-code.md) or [OAuth 2.0](./active-directory-protocols-oauth-code.md) protocols.</span></span> <span data-ttu-id="1319c-107">SAML 통합은 AppSource 인증에 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-107">SAML integration is not accepted for AppSource certification.</span></span>

## <a name="guides-and-code-samples"></a><span data-ttu-id="1319c-108">지침 및 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="1319c-108">Guides and code samples</span></span>
<span data-ttu-id="1319c-109">Open ID를 사용하여 응용 프로그램을 Azure Active Directory와 통합하는 방법에 대해 자세히 알아보려면 [Azure Active Directory 개발자 가이드](./active-directory-developers-guide.md#get-started "개발자를 위한 Azure AD 시작")에서 지침 및 코드 샘플을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-109">If you want to learn about how to integrate your application with Azure Active Directory using Open ID connect, follow our guides and code samples in the [Azure Active Directory developer's guide](./active-directory-developers-guide.md#get-started "Get Started with Azure AD for developers").</span></span>

## <a name="multi-tenant-applications"></a><span data-ttu-id="1319c-110">다중 테넌트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="1319c-110">Multi-tenant applications</span></span>

<span data-ttu-id="1319c-111">별도 인스턴스, 구성 또는 배포를 요구하지 않고 Azure Active Directory가 있는 모든 회사 또는 조직에서 사용자의 로그인을 허용하는 응용 프로그램은 *다중 테넌트 응용 프로그램*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-111">An application that accepts sign-ins from users from any company or organization that have Azure Active Directory without requiring a separate instance, configuration, or deployment is known as a *multi-tenant application*.</span></span> <span data-ttu-id="1319c-112">AppSource에서는 응용 프로그램이 *단일 클릭* 평가판 체험을 활성화하도록 다중 테넌트를 구현하는 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-112">AppSource recommends that applications implement multi-tenancy to enable the *single-click* free trial experience.</span></span>

<span data-ttu-id="1319c-113">응용 프로그램에서 다중 테넌트를 활성화하기 위해:</span><span class="sxs-lookup"><span data-stu-id="1319c-113">In order to enable multi-tenancy on your application:</span></span>
- <span data-ttu-id="1319c-114">[Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps)의 응용 프로그램 등록 정보에서 `Multi-Tenanted` 속성을 `Yes`로 설정합니다(기본적으로 Azure Portal에서 만든 응용 프로그램은 *단일 테넌트*로 구성됨).</span><span class="sxs-lookup"><span data-stu-id="1319c-114">Set `Multi-Tenanted` property to `Yes` on your application registration's information in the [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (by default, applications created in the Azure Portal are configured as *single-tenant*)</span></span>
- <span data-ttu-id="1319c-115">'`common`' 끝점에 요청을 보내도록 코드를 업데이트합니다(*https://login.microsoftonline.com/{yourtenant}*에서 *https://login.microsoftonline.com/common*으로 끝점 업데이트).</span><span class="sxs-lookup"><span data-stu-id="1319c-115">Update your code to send requests to the '`common`' endpoint (update the endpoint from *https://login.microsoftonline.com/{yourtenant}* to *https://login.microsoftonline.com/common*)</span></span>
- <span data-ttu-id="1319c-116">ASP.NET과 같은 일부 플랫폼의 경우 여러 발급자를 허용하도록 코드를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-116">For some platforms, like ASP.NET, you need also to update your code to accept multiple issuers</span></span>

<span data-ttu-id="1319c-117">다중 테넌트에 대한 정보는 [다중 테넌트 응용 프로그램 패턴을 사용하여 모든 Azure AD(Active Directory) 사용자를 로그인하는 방법](./active-directory-devhowto-multi-tenant-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1319c-117">For more information about multi-tenancy, see: [How to sign in any Azure Active Directory (AD) user using the multi-tenant application pattern](./active-directory-devhowto-multi-tenant-overview.md).</span></span>

### <a name="single-tenant-applications"></a><span data-ttu-id="1319c-118">단일 테넌트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="1319c-118">Single-tenant applications</span></span>
<span data-ttu-id="1319c-119">정의된 Azure Active Directory 인스턴스의 사용자의 로그인만 허용하는 응용 프로그램은 *단일 테넌트 응용 프로그램*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-119">Applications that only accept sign-ins from users of a defined Azure Active Directory instance are known as *single-tenant application*.</span></span> <span data-ttu-id="1319c-120">외부 사용자(다른 조직의 회사 또는 학교 계정 또는 개인 계정 포함)는 각 사용자를 *게스트 계정*으로 응용 프로그램이 등록된 Azure Active Directory 인스턴스에 추가한 후 단일 테넌트 응용 프로그램에 로그인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-120">External users (including Work or School accounts from other organizations, or personal account) can sign in to a single-tenant application after adding each user as *guest account* to the Azure Active Directory instance that the application is registered.</span></span> <span data-ttu-id="1319c-121">사용자를 게스트 계정으로 [*Azure AD B2B 공동 작업*](../active-directory-b2b-what-is-azure-ad-b2b.md)을 통해 Azure Active Directory에 추가할 수 있으며 이는 [프로그래밍 방식으로](../active-directory-b2b-code-samples.md) 수행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-121">You can add users as guest accounts to an Azure Active Directory via the [*Azure AD B2B collaboration*](../active-directory-b2b-what-is-azure-ad-b2b.md) - and it can be done [programatically](../active-directory-b2b-code-samples.md).</span></span> <span data-ttu-id="1319c-122">사용자를 게스트 계정으로 Azure Active Directory에 추가할 때 초대 전자 메일의 링크를 클릭하여 초대를 수락해야 하는 사용자에게 초대 전자 메일이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-122">When you add a user as guest account to an Azure Active Directory, an invitation email is sent to the user, who has to accept the invitation by clicking on the link in the invitation email.</span></span> <span data-ttu-id="1319c-123">파트너 조직의 멤버이기도 한 초대 조직의 추가 사용자에게 전송되는 초대는 로그인하기 위해 초대를 수락할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-123">Invitations that are sent to an additional user in an inviting organization that is also a member of the partner organization are not required to accept an invitation to sign in.</span></span>

<span data-ttu-id="1319c-124">단일 테넌트 응용 프로그램은 *연락처* 환경을 활성화할 수 있지만 AppSource가 권장하는 단일 클릭/평가판 체험을 활성화하려는 경우 응용 프로그램에서 다중 테넌트를 대신 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-124">Single-tenant applications can enable the *Contact Me* experience, but if you want to enable the single-click/ free trial experience that AppSource recommends, enable multi-tenancy on your application instead.</span></span>


## <a name="appsource-trial-experiences"></a><span data-ttu-id="1319c-125">AppSource 평가판 체험</span><span class="sxs-lookup"><span data-stu-id="1319c-125">AppSource trial experiences</span></span>

### <a name="free-trial-customer-led-trial-experience"></a><span data-ttu-id="1319c-126">평가판(고객 주도 평가판 체험)</span><span class="sxs-lookup"><span data-stu-id="1319c-126">Free Trial (Customer-led trial experience)</span></span> 
<span data-ttu-id="1319c-127">*고객 주도 평가판*은 응용 프로그램에 대한 단일 클릭 액세스를 제공하므로 AppSource에서 권장하는 체험입니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-127">The *customer-led trial* is the experience that AppSource recommends as it offers a single-click access to your application.</span></span> <span data-ttu-id="1319c-128">아래는 이 체험이 표시되는 방식의 그림입니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-128">Below an illustration of how this experience looks like:</span></span><br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="1319c-129">사용자는 AppSource 웹 사이트에서 응용 프로그램을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-129">User finds your application in AppSource Web Site</span></span></li><li><span data-ttu-id="1319c-130">‘평가판’ 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-130">Selects ‘Free trial’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li><span data-ttu-id="1319c-131">AppSource는 웹 사이트의 URL로 사용자를 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-131">AppSource redirects user to a URL in your web site</span></span></li><li><span data-ttu-id="1319c-132">웹 사이트는 <i>Single Sign-On</i> 프로세스를 자동으로 시작합니다(페이지 로드에서).</span><span class="sxs-lookup"><span data-stu-id="1319c-132">Your web site starts the <i>single-sign-on</i> process automatically (on page load)</span></span></li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="1319c-133">사용자는 Microsoft 로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-133">User is redirected to Microsoft Sign-in page</span></span></li><li><span data-ttu-id="1319c-134">사용자는 로그인하기 위해 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-134">User provides credentials to sign in</span></span></li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="1319c-135">사용자는 응용 프로그램에 대한 동의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-135">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="1319c-136">로그인을 완료하고 사용자는 웹 사이트로 다시 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-136">Sign-in completes and user is redirected back to your web site</span></span></li><li><span data-ttu-id="1319c-137">사용자는 평가판을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-137">User starts the free trial</span></span></li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a><span data-ttu-id="1319c-138">연락처(파트너 주도 평가판 체험)</span><span class="sxs-lookup"><span data-stu-id="1319c-138">Contact Me (Partner-led trial experience)</span></span>
<span data-ttu-id="1319c-139">*파트너 평가판 체험*은 사용자/회사를 프로비전하기 위해 수동 또는 장기 작업을 발생해야 하는 경우에 사용될 수 있습니다. 예를 들어 응용 프로그램은 가상 컴퓨터, 데이터베이스 인스턴스 또는 완료하는 데 시간이 많이 걸리는 작업을 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-139">The *partner trial experience* can be used when a manual or a long-term operation needs to happen to provision the user/ company: for example, your application needs to provision virtual machines, database instances, or operations that take much time to complete.</span></span> <span data-ttu-id="1319c-140">이 경우 사용자가 *'평가판 요청'* 단추를 선택하고 양식을 채운 후 AppSource는 사용자의 연락처 정보를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-140">In this case, after user selects the *'Request Trial'* button and fills out a form, AppSource sends you the user's contact information.</span></span> <span data-ttu-id="1319c-141">이 정보를 받으면 환경을 프로비전하고 평가판 체험에 액세스하는 방법에 대한 지침을 사용자에게 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-141">Upon receiving this information, you then provision the environment and send the instructions to the user on how to access the trial experience:</span></span><br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="1319c-142">사용자는 AppSource 웹 사이트에서 응용 프로그램을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-142">User finds your application in AppSource web site</span></span></li><li><span data-ttu-id="1319c-143">'연락처' 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-143">Selects ‘Contact Me’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li><span data-ttu-id="1319c-144">연락처 정보로 양식을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-144">Fills out a form with contact information</span></span></li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td><span data-ttu-id="1319c-145">사용자 정보를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-145">You receive user information</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td><span data-ttu-id="1319c-146">환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-146">Setup environment</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td><span data-ttu-id="1319c-147">평가판 정보로 사용자에게 연락합니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-147">Contact user with trial info</span></span></td>
        </tr>
        </table><br/><br/>
        <ul><li><span data-ttu-id="1319c-148">사용자의 정보를 받고 평가판 인스턴스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-148">You receive user's information and setup trial instance</span></span></li><li><span data-ttu-id="1319c-149">응용 프로그램이 사용자에게 액세스하기 위한 하이퍼링크를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-149">You send the hyperlink to access your application to the user</span></span></li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="1319c-150">사용자는 응용 프로그램에 액세스하고 Single Sign-On 프로세스를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-150">User accesses your application and complete the single-sign-on process</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="1319c-151">사용자는 응용 프로그램에 대한 동의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-151">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="1319c-152">로그인을 완료하고 사용자는 웹 사이트로 다시 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-152">Sign-in completes and user is redirected back to your web site</span></span></li><li><span data-ttu-id="1319c-153">사용자는 평가판을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-153">User starts the free trial</span></span></li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a><span data-ttu-id="1319c-154">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="1319c-154">More information</span></span>
<span data-ttu-id="1319c-155">AppSource 평가판 체험에 대한 자세한 내용은 [이 비디오](https://aka.ms/trialexperienceforwebapps)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1319c-155">For more information about the AppSource trial experience, see [this video](https://aka.ms/trialexperienceforwebapps).</span></span> 
 
## <a name="next-steps"></a><span data-ttu-id="1319c-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1319c-156">Next Steps</span></span>

- <span data-ttu-id="1319c-157">Azure Active Directory 로그인을 지원하는 응용 프로그램 구축에 대한 자세한 내용은 [Azure AD에 대한 인증 시나리오](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1319c-157">For more information on building applications that support Azure Active Directory sign-ins, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span></span> 

- <span data-ttu-id="1319c-158">AppSource에 SaaS 응용 프로그램을 나열하는 방법에 대한 내용은 [AppSource 파트너 정보](https://appsource.microsoft.com/partners)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1319c-158">For information on how to list your SaaS application in AppSource, go see [AppSource Partner Information](https://appsource.microsoft.com/partners)</span></span>


## <a name="get-support"></a><span data-ttu-id="1319c-159">지원 받기</span><span class="sxs-lookup"><span data-stu-id="1319c-159">Get Support</span></span>
<span data-ttu-id="1319c-160">Azure Active Directory 통합의 경우 지원을 제공하기 위해 커뮤니티와 함께 [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-160">For Azure Active Directory integration, we use [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory) with the community to provide support.</span></span> 

<span data-ttu-id="1319c-161">먼저 Stack Overflow에 질문하고 이전에 다른 사용자가 질문했는지 확인하기 위해 기존 문제를 찾아보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-161">We highly recommend you ask your questions on Stack Overflow first and browse existing issues to see if someone has asked your question before.</span></span> <span data-ttu-id="1319c-162">질문이나 의견이 `[azure-active-directory]`로 태그가 지정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-162">Make sure that your questions or comments are tagged with `[azure-active-directory]`.</span></span>

<span data-ttu-id="1319c-163">다음 설명 섹션을 사용하여 피드백을 제공하고 콘텐츠를 구체화하고 모양을 갖출 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1319c-163">Use the following comments section to provide feedback and help us refine and shape our content.</span></span>

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->