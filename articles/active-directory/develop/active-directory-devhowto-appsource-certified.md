---
title: "Azure Active Directory에 대 한 인증 AppSource aaaHow tooget | Microsoft Docs"
description: "어떻게 tooget AppSource 응용 프로그램에 대해 인증 된 Azure Active Directory에 대 한 세부 정보입니다."
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
ms.openlocfilehash: e9f07e9220afcba1120b987122fe770fe5225eed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-appsource-certified-for-azure-active-directory"></a><span data-ttu-id="1b00a-103">Azure Active Directory에 대 한 tooget AppSource 인증 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1b00a-103">How tooget AppSource Certified for Azure Active Directory</span></span>
<span data-ttu-id="1b00a-104">[Microsoft AppSource](https://appsource.microsoft.com/) 대상이 되는 비즈니스 사용자가 toodiscover를 실행 하 고 관리 업무의 SaaS 응용 프로그램 (독립 실행형 추가 기능 및 SaaS tooexisting SaaS 제품).</span><span class="sxs-lookup"><span data-stu-id="1b00a-104">[Microsoft AppSource](https://appsource.microsoft.com/) is a destination for business users toodiscover, try, and manage line-of-business SaaS applications (standalone SaaS and add-on tooexisting Microsoft SaaS products).</span></span>

<span data-ttu-id="1b00a-105">독립 실행형 AppSource에서 SaaS 응용 프로그램 toolist single sign on에서 모든 회사 또는 조직 Azure Active Directory에서 작업 계정에서 응용 프로그램 동의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-105">toolist a standalone SaaS application on AppSource, your application must accept single sign-on from work accounts from any company or organization that has Azure Active Directory.</span></span> <span data-ttu-id="1b00a-106">hello 로그인 프로세스는 hello를 사용 해야 [OpenID Connect](./active-directory-protocols-openid-connect-code.md) 또는 [OAuth 2.0](./active-directory-protocols-oauth-code.md) 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-106">hello sign-in process must use hello [OpenID Connect](./active-directory-protocols-openid-connect-code.md) or [OAuth 2.0](./active-directory-protocols-oauth-code.md) protocols.</span></span> <span data-ttu-id="1b00a-107">SAML 통합은 AppSource 인증에 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-107">SAML integration is not accepted for AppSource certification.</span></span>

## <a name="guides-and-code-samples"></a><span data-ttu-id="1b00a-108">지침 및 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="1b00a-108">Guides and code samples</span></span>
<span data-ttu-id="1b00a-109">가이드에 따라 및 코드 hello에 대 한 샘플 Openid를 사용 하 여 Azure Active Directory와 응용 프로그램 연결 하는 toointegrate 방법에 대 한 toolearn 하려는 경우 [Azure Active Directory 개발자 가이드](./active-directory-developers-guide.md#get-started "시작 개발자를 위한 azure AD")합니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-109">If you want toolearn about how toointegrate your application with Azure Active Directory using Open ID connect, follow our guides and code samples in hello [Azure Active Directory developer's guide](./active-directory-developers-guide.md#get-started "Get Started with Azure AD for developers").</span></span>

## <a name="multi-tenant-applications"></a><span data-ttu-id="1b00a-110">다중 테넌트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="1b00a-110">Multi-tenant applications</span></span>

<span data-ttu-id="1b00a-111">별도 인스턴스, 구성 또는 배포를 요구하지 않고 Azure Active Directory가 있는 모든 회사 또는 조직에서 사용자의 로그인을 허용하는 응용 프로그램은 *다중 테넌트 응용 프로그램*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-111">An application that accepts sign-ins from users from any company or organization that have Azure Active Directory without requiring a separate instance, configuration, or deployment is known as a *multi-tenant application*.</span></span> <span data-ttu-id="1b00a-112">AppSource 응용 프로그램은 다중 테 넌 트 tooenable hello 구현 하는 것이 좋습니다. *단일 클릭* 평가판 체험을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-112">AppSource recommends that applications implement multi-tenancy tooenable hello *single-click* free trial experience.</span></span>

<span data-ttu-id="1b00a-113">순서 tooenable 다중 테 넌 트 응용 프로그램에서:</span><span class="sxs-lookup"><span data-stu-id="1b00a-113">In order tooenable multi-tenancy on your application:</span></span>
- <span data-ttu-id="1b00a-114">설정 `Multi-Tenanted` 속성 너무`Yes` hello의 응용 프로그램 등록의 정보에 [Azure 포털](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (기본적으로 hello Azure 포털에서에서 만든 응용 프로그램으로 구성 된 *단일-테넌트*)</span><span class="sxs-lookup"><span data-stu-id="1b00a-114">Set `Multi-Tenanted` property too`Yes` on your application registration's information in hello [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (by default, applications created in hello Azure Portal are configured as *single-tenant*)</span></span>
- <span data-ttu-id="1b00a-115">프로그램 코드 toosend 요청 toohello 업데이트 '`common`' 끝점 (hello 끝점에서 업데이트 *https://login.microsoftonline.com/ {yourtenant}* 너무*https://login.microsoftonline.com/common*)</span><span class="sxs-lookup"><span data-stu-id="1b00a-115">Update your code toosend requests toohello '`common`' endpoint (update hello endpoint from *https://login.microsoftonline.com/{yourtenant}* too*https://login.microsoftonline.com/common*)</span></span>
- <span data-ttu-id="1b00a-116">ASP.NET과 같은 일부 플랫폼에 대 한 필요한도 tooupdate 코드 tooaccept 여러 발급자</span><span class="sxs-lookup"><span data-stu-id="1b00a-116">For some platforms, like ASP.NET, you need also tooupdate your code tooaccept multiple issuers</span></span>

<span data-ttu-id="1b00a-117">다중 테 넌 트에 대 한 자세한 내용은 참조: [방법을 사용 하 여 모든 Azure AD (Active Directory) 사용자의 toosign hello 다중 테 넌 트 응용 프로그램 패턴](./active-directory-devhowto-multi-tenant-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-117">For more information about multi-tenancy, see: [How toosign in any Azure Active Directory (AD) user using hello multi-tenant application pattern](./active-directory-devhowto-multi-tenant-overview.md).</span></span>

### <a name="single-tenant-applications"></a><span data-ttu-id="1b00a-118">단일 테넌트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="1b00a-118">Single-tenant applications</span></span>
<span data-ttu-id="1b00a-119">정의된 Azure Active Directory 인스턴스의 사용자의 로그인만 허용하는 응용 프로그램은 *단일 테넌트 응용 프로그램*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-119">Applications that only accept sign-ins from users of a defined Azure Active Directory instance are known as *single-tenant application*.</span></span> <span data-ttu-id="1b00a-120">외부 사용자 (다른 조직에서 회사 또는 학교 계정 또는 개인 계정 포함)으로 각 사용자를 추가한 후 tooa 단일 테 넌 트 응용 프로그램에 로그인 할 수 *게스트 계정* toohello Azure Active Directory 인스턴스를 hello 응용 프로그램 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-120">External users (including Work or School accounts from other organizations, or personal account) can sign in tooa single-tenant application after adding each user as *guest account* toohello Azure Active Directory instance that hello application is registered.</span></span> <span data-ttu-id="1b00a-121">Hello 통해 게스트 계정 tooan Azure Active Directory로 사용자를 추가할 수 있습니다 [ *Azure AD B2B 공동 작업* ](../active-directory-b2b-what-is-azure-ad-b2b.md) -수행 될 수 있습니다 [프로그래밍](../active-directory-b2b-code-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-121">You can add users as guest accounts tooan Azure Active Directory via hello [*Azure AD B2B collaboration*](../active-directory-b2b-what-is-azure-ad-b2b.md) - and it can be done [programatically](../active-directory-b2b-code-samples.md).</span></span> <span data-ttu-id="1b00a-122">게스트 계정 tooan Azure Active Directory로 사용자를 추가 하면 hello hello 초대 메일 링크를 클릭 하 여 tooaccept hello 초대를 가진 toohello 사용자 초대 메일 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-122">When you add a user as guest account tooan Azure Active Directory, an invitation email is sent toohello user, who has tooaccept hello invitation by clicking on hello link in hello invitation email.</span></span> <span data-ttu-id="1b00a-123">Hello 파트너 조식의 멤버 이기도 초대 조직의 tooan 추가 사용자 보낸 초대에는 초대 toosign를 tooaccept 필요 하지 않습니다는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-123">Invitations that are sent tooan additional user in an inviting organization that is also a member of hello partner organization are not required tooaccept an invitation toosign in.</span></span>

<span data-ttu-id="1b00a-124">단일 테 넌 트 응용 프로그램에는 hello 사용 하도록 설정할 수 *연락처 Me* 을 발생 하지만 tooenable hello 단일 클릭 / 무료 평가판 체험 AppSource 권장 하는 경우 사용 하도록 설정 응용 프로그램에 다중 테 넌 트 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-124">Single-tenant applications can enable hello *Contact Me* experience, but if you want tooenable hello single-click/ free trial experience that AppSource recommends, enable multi-tenancy on your application instead.</span></span>


## <a name="appsource-trial-experiences"></a><span data-ttu-id="1b00a-125">AppSource 평가판 체험</span><span class="sxs-lookup"><span data-stu-id="1b00a-125">AppSource trial experiences</span></span>

### <a name="free-trial-customer-led-trial-experience"></a><span data-ttu-id="1b00a-126">평가판(고객 주도 평가판 체험)</span><span class="sxs-lookup"><span data-stu-id="1b00a-126">Free Trial (Customer-led trial experience)</span></span> 
<span data-ttu-id="1b00a-127">hello *고객 이끄는 평가판* AppSource 권장 단일 클릭 액세스 tooyour 응용 프로그램이 제공 하는 hello 환경 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-127">hello *customer-led trial* is hello experience that AppSource recommends as it offers a single-click access tooyour application.</span></span> <span data-ttu-id="1b00a-128">아래는 이 체험이 표시되는 방식의 그림입니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-128">Below an illustration of how this experience looks like:</span></span><br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="1b00a-129">사용자는 AppSource 웹 사이트에서 응용 프로그램을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-129">User finds your application in AppSource Web Site</span></span></li><li><span data-ttu-id="1b00a-130">‘평가판’ 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-130">Selects ‘Free trial’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li><span data-ttu-id="1b00a-131">AppSource 리디렉션하여 사용자 tooa URL은 웹 사이트에서</span><span class="sxs-lookup"><span data-stu-id="1b00a-131">AppSource redirects user tooa URL in your web site</span></span></li><li><span data-ttu-id="1b00a-132">웹 사이트가 시작 hello <i>단일 로그온</i> 에서 자동으로 (페이지 로드) 프로세스</span><span class="sxs-lookup"><span data-stu-id="1b00a-132">Your web site starts hello <i>single-sign-on</i> process automatically (on page load)</span></span></li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="1b00a-133">사용자가 리디렉션된 tooMicrosoft 로그인 페이지</span><span class="sxs-lookup"><span data-stu-id="1b00a-133">User is redirected tooMicrosoft Sign-in page</span></span></li><li><span data-ttu-id="1b00a-134">사용자의 자격 증명 toosign를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-134">User provides credentials toosign in</span></span></li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="1b00a-135">사용자는 응용 프로그램에 대한 동의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-135">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="1b00a-136">로그인을 완료 하 고 사용자가 리디렉션된 백 tooyour 웹 사이트</span><span class="sxs-lookup"><span data-stu-id="1b00a-136">Sign-in completes and user is redirected back tooyour web site</span></span></li><li><span data-ttu-id="1b00a-137">사용자가 hello 무료 평가판 시작</span><span class="sxs-lookup"><span data-stu-id="1b00a-137">User starts hello free trial</span></span></li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a><span data-ttu-id="1b00a-138">연락처(파트너 주도 평가판 체험)</span><span class="sxs-lookup"><span data-stu-id="1b00a-138">Contact Me (Partner-led trial experience)</span></span>
<span data-ttu-id="1b00a-139">hello *평가판 체험 파트너* 수동 또는 장기 작업 toohappen tooprovision hello 사용자 필요로 하는 경우 사용할 수 있습니다 / 회사: 예를 들어 응용 프로그램에 필요한 tooprovision 가상 컴퓨터, 데이터베이스 인스턴스 또는 많은 시간 toocomplete를 사용 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-139">hello *partner trial experience* can be used when a manual or a long-term operation needs toohappen tooprovision hello user/ company: for example, your application needs tooprovision virtual machines, database instances, or operations that take much time toocomplete.</span></span> <span data-ttu-id="1b00a-140">이 경우 사용자가 선택 되어 hello 후 *요청 평가판* 단추를 사용자의 연락처 정보를 hello 보냅니다 AppSource는 양식을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-140">In this case, after user selects hello *'Request Trial'* button and fills out a form, AppSource sends you hello user's contact information.</span></span> <span data-ttu-id="1b00a-141">이 정보를 받으면 다음 프로 비전 hello 환경 및 있습니다 어떻게 tooaccess hello 평가판 체험에 hello 지침 toohello 사용자 보내기:</span><span class="sxs-lookup"><span data-stu-id="1b00a-141">Upon receiving this information, you then provision hello environment and send hello instructions toohello user on how tooaccess hello trial experience:</span></span><br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="1b00a-142">사용자는 AppSource 웹 사이트에서 응용 프로그램을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-142">User finds your application in AppSource web site</span></span></li><li><span data-ttu-id="1b00a-143">'연락처' 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-143">Selects ‘Contact Me’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li><span data-ttu-id="1b00a-144">연락처 정보로 양식을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-144">Fills out a form with contact information</span></span></li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td><span data-ttu-id="1b00a-145">사용자 정보를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-145">You receive user information</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td><span data-ttu-id="1b00a-146">환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-146">Setup environment</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td><span data-ttu-id="1b00a-147">평가판 정보로 사용자에게 연락합니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-147">Contact user with trial info</span></span></td>
        </tr>
        </table><br/><br/>
        <ul><li><span data-ttu-id="1b00a-148">사용자의 정보를 받고 평가판 인스턴스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-148">You receive user's information and setup trial instance</span></span></li><li><span data-ttu-id="1b00a-149">Hello 하이퍼링크 tooaccess 응용 프로그램 toohello 사용자 보내기</span><span class="sxs-lookup"><span data-stu-id="1b00a-149">You send hello hyperlink tooaccess your application toohello user</span></span></li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="1b00a-150">사용자가 응용 프로그램 및 전체 hello 단일 로그온 프로세스를 액세스</span><span class="sxs-lookup"><span data-stu-id="1b00a-150">User accesses your application and complete hello single-sign-on process</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="1b00a-151">사용자는 응용 프로그램에 대한 동의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-151">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="1b00a-152">로그인을 완료 하 고 사용자가 리디렉션된 백 tooyour 웹 사이트</span><span class="sxs-lookup"><span data-stu-id="1b00a-152">Sign-in completes and user is redirected back tooyour web site</span></span></li><li><span data-ttu-id="1b00a-153">사용자가 hello 무료 평가판 시작</span><span class="sxs-lookup"><span data-stu-id="1b00a-153">User starts hello free trial</span></span></li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a><span data-ttu-id="1b00a-154">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="1b00a-154">More information</span></span>
<span data-ttu-id="1b00a-155">Hello AppSource 평가판 체험 방법에 대 한 자세한 내용은 참조 [이 비디오](https://aka.ms/trialexperienceforwebapps)합니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-155">For more information about hello AppSource trial experience, see [this video](https://aka.ms/trialexperienceforwebapps).</span></span> 
 
## <a name="next-steps"></a><span data-ttu-id="1b00a-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1b00a-156">Next Steps</span></span>

- <span data-ttu-id="1b00a-157">Azure Active Directory 로그인을 지원하는 응용 프로그램 구축에 대한 자세한 내용은 [Azure AD에 대한 인증 시나리오](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1b00a-157">For more information on building applications that support Azure Active Directory sign-ins, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span></span> 

- <span data-ttu-id="1b00a-158">방법 toolist AppSource에서 SaaS 응용 프로그램으로 참조에 대 한 내용은 [AppSource 파트너 정보](https://appsource.microsoft.com/partners)</span><span class="sxs-lookup"><span data-stu-id="1b00a-158">For information on how toolist your SaaS application in AppSource, go see [AppSource Partner Information](https://appsource.microsoft.com/partners)</span></span>


## <a name="get-support"></a><span data-ttu-id="1b00a-159">지원 받기</span><span class="sxs-lookup"><span data-stu-id="1b00a-159">Get Support</span></span>
<span data-ttu-id="1b00a-160">Azure Active Directory 통합을 위해 사용 하 여 [스택 오버플로](http://stackoverflow.com/questions/tagged/azure-active-directory) hello 커뮤니티 tooprovide 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-160">For Azure Active Directory integration, we use [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory) with hello community tooprovide support.</span></span> 

<span data-ttu-id="1b00a-161">스택 오버플로에 질문을 먼저 확인 하 고 질문 하기 전에 요청에 다른 사람이 되 면 기존 문제 toosee 찾아보기 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-161">We highly recommend you ask your questions on Stack Overflow first and browse existing issues toosee if someone has asked your question before.</span></span> <span data-ttu-id="1b00a-162">질문이나 의견이 `[azure-active-directory]`로 태그가 지정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-162">Make sure that your questions or comments are tagged with `[azure-active-directory]`.</span></span>

<span data-ttu-id="1b00a-163">다음 설명 섹션 tooprovide 피드백 hello를 사용 하 여 및 구체화 하 고 콘텐츠를 셰이핑 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b00a-163">Use hello following comments section tooprovide feedback and help us refine and shape our content.</span></span>

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->