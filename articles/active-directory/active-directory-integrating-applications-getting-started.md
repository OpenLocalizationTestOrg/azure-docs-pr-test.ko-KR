---
title: "aaaGet 앱과 Azure AD를 통합 하기 시작 | Microsoft Docs"
description: "이 문서는 온-프레미스 응용 프로그램 및 클라우드 응용 프로그램과 Azure Active Directory(AD)를 통합하는 시작 가이드입니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: db6d210d-c970-49e9-bd20-36d984bcd1c3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: 5a7a851e8418083fee72ab58477a9cab75d0d4bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-azure-active-directory-with-applications-getting-started-guide"></a><span data-ttu-id="e2a0f-103">응용 프로그램과 Azure Active Directory 통합 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="e2a0f-103">Integrating Azure Active Directory with applications getting started guide</span></span>
## <a name="overview"></a><span data-ttu-id="e2a0f-104">개요</span><span class="sxs-lookup"><span data-stu-id="e2a0f-104">Overview</span></span>
<span data-ttu-id="e2a0f-105">이 항목은 의도 한 toogive 응용 프로그램으로 Azure AD (Active Directory) 통합에 대 한 로드맵 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a0f-105">This topic is intended toogive you a roadmap for integrating applications with Azure Active Directory (AD).</span></span> <span data-ttu-id="e2a0f-106">이 시작된 가이드의 어떤 부분이 관련 tooyou 식별할 수 있도록 더 자세한 항목에 대 한 간단한 요약을 포함 하는 각 hello 섹션 아래</span><span class="sxs-lookup"><span data-stu-id="e2a0f-106">Each of hello sections below contain a brief summary of a more detailed topic so you can identify which parts of this getting started guide are relevant tooyou.</span></span>  <span data-ttu-id="e2a0f-107">각 주제에 자세히 알아보려면 hello 링크를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="e2a0f-107">Follow hello links for a deeper dive on each subject.</span></span>

## <a name="before-you-begin-take-inventory"></a><span data-ttu-id="e2a0f-108">시작 하기 전에 인벤토리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a0f-108">Before you begin, take inventory</span></span>
<span data-ttu-id="e2a0f-109">Toointegrating 응용 프로그램과 Azure AD에서에서 이동 전에 고 toogo 원하는 중요 한 tooknow 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2a0f-109">Before you jump in toointegrating applications with Azure AD, it is important tooknow where you are and where you want toogo.</span></span>  <span data-ttu-id="e2a0f-110">hello 다음 질문은 Azure AD 응용 프로그램 통합 프로젝트에 대해 의견이 의도 한 toohelp입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a0f-110">hello following questions are intended toohelp you think about your Azure AD application integration project.</span></span>

### <a name="application-inventory"></a><span data-ttu-id="e2a0f-111">응용 프로그램 인벤토리</span><span class="sxs-lookup"><span data-stu-id="e2a0f-111">Application inventory</span></span>
* <span data-ttu-id="e2a0f-112">응용 프로그램은 모두 어디에 있습니까?</span><span class="sxs-lookup"><span data-stu-id="e2a0f-112">Where are all of your applications?</span></span> <span data-ttu-id="e2a0f-113">누가 소유합니까?</span><span class="sxs-lookup"><span data-stu-id="e2a0f-113">Who owns them?</span></span>
* <span data-ttu-id="e2a0f-114">응용 프로그램에 어떤 종류의 인증이 필요합니까?</span><span class="sxs-lookup"><span data-stu-id="e2a0f-114">What kind of authentication do your applications require?</span></span>
* <span data-ttu-id="e2a0f-115">응용 프로그램에 액세스할 toowhich 인원?</span><span class="sxs-lookup"><span data-stu-id="e2a0f-115">Who needs access toowhich applications?</span></span>
* <span data-ttu-id="e2a0f-116">새 응용 프로그램 toodeploy 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="e2a0f-116">Do you want toodeploy a new application?</span></span>
  * <span data-ttu-id="e2a0f-117">사내에 구축하고 Azure 계산 인스턴스에 배포하시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="e2a0f-117">Will you build it in-house and deploy it on an Azure compute instance?</span></span>
  * <span data-ttu-id="e2a0f-118">Hello Azure 응용 프로그램 갤러리에서에서 사용할 수 있는 하나 사용할 것인가?</span><span class="sxs-lookup"><span data-stu-id="e2a0f-118">Will you use one that is available in hello Azure Application Gallery?</span></span>

### <a name="user-and-group-inventory"></a><span data-ttu-id="e2a0f-119">사용자 및 그룹 인벤토리</span><span class="sxs-lookup"><span data-stu-id="e2a0f-119">User and group inventory</span></span>
* <span data-ttu-id="e2a0f-120">사용자 계정은 어디에 있습니까?</span><span class="sxs-lookup"><span data-stu-id="e2a0f-120">Where do your user accounts reside?</span></span>
  * <span data-ttu-id="e2a0f-121">온-프레미스 Active Directory</span><span class="sxs-lookup"><span data-stu-id="e2a0f-121">On-premises Active Directory</span></span>
  * <span data-ttu-id="e2a0f-122">Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2a0f-122">Azure AD</span></span>
  * <span data-ttu-id="e2a0f-123">사용자가 소유한 별도 응용 프로그램 데이터베이스 내에서</span><span class="sxs-lookup"><span data-stu-id="e2a0f-123">Within a separate application database that you own</span></span>
  * <span data-ttu-id="e2a0f-124">허용되지 않은 응용 프로그램에서</span><span class="sxs-lookup"><span data-stu-id="e2a0f-124">In unsanctioned applications</span></span>
  * <span data-ttu-id="e2a0f-125">위의 hello의 모든</span><span class="sxs-lookup"><span data-stu-id="e2a0f-125">All of hello above</span></span>
* <span data-ttu-id="e2a0f-126">개별 사용자는 현재 어떤 사용 권한 및 역할 할당을 가지고 있습니까?</span><span class="sxs-lookup"><span data-stu-id="e2a0f-126">What permissions and role assignments do individual users currently have?</span></span> <span data-ttu-id="e2a0f-127">필요 한가요 tooreview 액세스 또는 사용자 액세스 및 역할 할당 적절 하 게 이제 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="e2a0f-127">Do you need tooreview their access or are you sure that your user access and role assignments are appropriate now?</span></span>
* <span data-ttu-id="e2a0f-128">그룹은 온-프레미스 Active Directory 내에 만들어 집니까?</span><span class="sxs-lookup"><span data-stu-id="e2a0f-128">Are groups already established in your on-premises Active Directory?</span></span>
  * <span data-ttu-id="e2a0f-129">그룹을 어떻게 구성합니까?</span><span class="sxs-lookup"><span data-stu-id="e2a0f-129">How are your groups organized?</span></span>
  * <span data-ttu-id="e2a0f-130">Hello 그룹 멤버는 누구 인가요?</span><span class="sxs-lookup"><span data-stu-id="e2a0f-130">Who are hello group members?</span></span>
  * <span data-ttu-id="e2a0f-131">어떤 사용 권한/역할 할당 hello 그룹 현재 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="e2a0f-131">What permissions/role assignments do hello groups currently have?</span></span>
* <span data-ttu-id="e2a0f-132">사용자/그룹 데이터베이스를 tooclean을 통합 하기 전에 필요 한가요?</span><span class="sxs-lookup"><span data-stu-id="e2a0f-132">Will you need tooclean up user/group databases before integrating?</span></span>  <span data-ttu-id="e2a0f-133">(매우 중요한 질문입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a0f-133">(This is a pretty important question.</span></span> <span data-ttu-id="e2a0f-134">쓰레기를 넣고 쓰레기를 얻는 현상.)</span><span class="sxs-lookup"><span data-stu-id="e2a0f-134">Garbage in, garbage out.)</span></span>

### <a name="access-management-inventory"></a><span data-ttu-id="e2a0f-135">액세스 관리 인벤토리</span><span class="sxs-lookup"><span data-stu-id="e2a0f-135">Access management inventory</span></span>
* <span data-ttu-id="e2a0f-136">어떻게 하면 현재 관리 사용자 액세스 tooapplications?</span><span class="sxs-lookup"><span data-stu-id="e2a0f-136">How do you currently manage user access tooapplications?</span></span> <span data-ttu-id="e2a0f-137">toochange에 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="e2a0f-137">Does that need toochange?</span></span>  <span data-ttu-id="e2a0f-138">고려 했습니까 다른 방법으로 toomanage 액세스와 같은 [RBAC](role-based-access-control-configure.md) 예를 들어?</span><span class="sxs-lookup"><span data-stu-id="e2a0f-138">Have you considered other ways toomanage access, such as with [RBAC](role-based-access-control-configure.md) for example?</span></span>
* <span data-ttu-id="e2a0f-139">액세스 toowhat 인원?</span><span class="sxs-lookup"><span data-stu-id="e2a0f-139">Who needs access toowhat?</span></span>

<span data-ttu-id="e2a0f-140">어쩌면 없는 이러한 질문의 답변 tooall hello 들겠지만 하지만 괜찮습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a0f-140">Maybe you don't have hello answers tooall of these questions up front but that's okay.</span></span>  <span data-ttu-id="e2a0f-141">이 가이드는 이러한 일부 질문에 대답하고 합리적인 결정을 내릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a0f-141">This guide can help you answer some of those questions and make some informed decisions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2a0f-142">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e2a0f-142">Prerequisites</span></span>
* <span data-ttu-id="e2a0f-143">Azure 구독 및 Azure Active Directory입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a0f-143">An Azure subscription and an Azure Active Directory directory.</span></span>  <span data-ttu-id="e2a0f-144">Azure 구독이 아직 없는 경우 Azure를 30일 동안 무료로 사용해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a0f-144">If you don't already have an Azure subscription, you can try out Azure for free for 30 days.</span></span> [<span data-ttu-id="e2a0f-145">사용해 보세요!</span><span class="sxs-lookup"><span data-stu-id="e2a0f-145">Try it out!</span></span>](https://azure.microsoft.com/trial/get-started-active-directory/)

## <a name="application-integration-with-azure-ad"></a><span data-ttu-id="e2a0f-146">Azure AD와 응용 프로그램 통합</span><span class="sxs-lookup"><span data-stu-id="e2a0f-146">Application integration with Azure AD</span></span>
### <a name="finding-unsanctioned-cloud-applications-with-cloud-app-discovery"></a><span data-ttu-id="e2a0f-147">클라우드 앱 검색을 사용하여 허용되지 않은 클라우드 응용 프로그램 찾기</span><span class="sxs-lookup"><span data-stu-id="e2a0f-147">Finding unsanctioned cloud applications with Cloud App Discovery</span></span>
<span data-ttu-id="e2a0f-148">위에서 설명한 대로 지금까지 조직에서 관리하지 않은 응용 프로그램이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a0f-148">As mentioned above, there may be applications that haven't been managed by your organization until now.</span></span>  <span data-ttu-id="e2a0f-149">Hello 인벤토리 프로세스의 일환으로, 가능한 toofind 승인 하지 않은 클라우드 응용 프로그램은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e2a0f-149">As part of hello inventory process, it is possible toofind unsanctioned cloud applications.</span></span> <span data-ttu-id="e2a0f-150">[클라우드 앱 검색을 사용하여 허용되지 않은 클라우드 응용 프로그램 찾기](active-directory-cloudappdiscovery-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e2a0f-150">See [Finding unsanctioned cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

### <a name="authentication-types"></a><span data-ttu-id="e2a0f-151">인증 형식</span><span class="sxs-lookup"><span data-stu-id="e2a0f-151">Authentication Types</span></span>
<span data-ttu-id="e2a0f-152">응용 프로그램에는 각자 다른 인증 요구 사항이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a0f-152">Each of your applications may have different authentication requirements.</span></span> <span data-ttu-id="e2a0f-153">Azure AD과 함께 인증서 서명은 SAML 2.0, WS-페더레이션 또는 OpenID 연결 프로토콜 뿐만 아니라 암호 Single Sign-on을 사용하는 응용 프로그램을 사용하는 응용 프로그램과 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a0f-153">With Azure AD, signing certificates can be used with applications that use SAML 2.0, WS-Federation, or OpenID Connect Protocols as well as Password Single Sign On.</span></span> <span data-ttu-id="e2a0f-154">Azure AD와 함께 사용할 응용 프로그램 인증 형식에 대한 자세한 내용은 [Azure Active Directory에서 페더레이션된 Single Sign-on에 대한 인증서 관리](active-directory-sso-certs.md) 및 [암호 기반 Single Sign On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e2a0f-154">For more information about application authentication types for use with Azure AD see [Managing Certificates for Federated Single Sign-On in Azure Active Directory](active-directory-sso-certs.md) and [Password based single sign on](active-directory-appssoaccess-whatis.md).</span></span>

### <a name="enabling-sso-with-azure-ad-app-proxy"></a><span data-ttu-id="e2a0f-155">Azure AD 앱 프록시를 사용하는 SSO 사용</span><span class="sxs-lookup"><span data-stu-id="e2a0f-155">Enabling SSO with Azure AD App Proxy</span></span>
<span data-ttu-id="e2a0f-156">Microsoft Azure AD 응용 프로그램 프록시 액세스 tooapplications 어디에서 든 및 모든 장치에서 안전 하 게 개인 네트워크 내부에 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a0f-156">With Microsoft Azure AD Application Proxy, you can provide access tooapplications located inside your private network securely, from anywhere and on any device.</span></span> <span data-ttu-id="e2a0f-157">환경 내에서 응용 프로그램 프록시 커넥터를 설치한 후에 Azure AD를 이용하여 쉽게 구성될 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="e2a0f-157">After you have installed an application proxy connector within your environment, it can be easily configured with Azure AD.</span></span>

### <a name="integrating-applications-with-azure-ad"></a><span data-ttu-id="e2a0f-158">Azure AD와 응용 프로그램 통합</span><span class="sxs-lookup"><span data-stu-id="e2a0f-158">Integrating applications with Azure AD</span></span>
<span data-ttu-id="e2a0f-159">hello 다음 문서에서 설명 hello 가지가 응용 프로그램을 Azure AD와 통합 하 고 몇 가지 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a0f-159">hello following articles discuss hello different ways applications integrate with Azure AD, and provide some guidance.</span></span>

* [<span data-ttu-id="e2a0f-160">Active Directory toouse 결정</span><span class="sxs-lookup"><span data-stu-id="e2a0f-160">Determining which Active Directory toouse</span></span>](active-directory-administer.md)
* [<span data-ttu-id="e2a0f-161">응용 프로그램을 사용 하 여 hello Azure 응용 프로그램 갤러리에서</span><span class="sxs-lookup"><span data-stu-id="e2a0f-161">Using applications in hello Azure application gallery</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="e2a0f-162">SaaS 응용 프로그램 통합 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="e2a0f-162">Integrating SaaS applications tutorials list</span></span>](active-directory-saas-tutorial-list.md)

## <a name="managing-access-tooapplications"></a><span data-ttu-id="e2a0f-163">액세스 tooapplications 관리</span><span class="sxs-lookup"><span data-stu-id="e2a0f-163">Managing access tooapplications</span></span>
<span data-ttu-id="e2a0f-164">hello 다음 문서 설명 방법으로 Azure AD 커넥터를 사용 하 여 Azure AD 및 Azure AD와 통합 되나요 되 면 액세스 tooapplications를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2a0f-164">hello following articles describe ways you can manage access tooapplications once they have been integrated with Azure AD using Azure AD Connectors and Azure AD.</span></span>

* [<span data-ttu-id="e2a0f-165">Azure AD를 사용 하 여 액세스 tooapps 관리</span><span class="sxs-lookup"><span data-stu-id="e2a0f-165">Managing access tooapps using Azure AD</span></span>](active-directory-managing-access-to-apps.md)
* [<span data-ttu-id="e2a0f-166">Azure AD 커넥터를 사용하여 자동화</span><span class="sxs-lookup"><span data-stu-id="e2a0f-166">Automating with Azure AD Connectors</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="e2a0f-167">Tooan 응용 프로그램 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a0f-167">Assigning users tooan application</span></span>](active-directory-applications-guiding-developers-assigning-users.md)
* [<span data-ttu-id="e2a0f-168">Tooan 응용 프로그램 그룹 지정</span><span class="sxs-lookup"><span data-stu-id="e2a0f-168">Assigning groups tooan application</span></span>](active-directory-applications-guiding-developers-assigning-groups.md)
* [<span data-ttu-id="e2a0f-169">계정 공유</span><span class="sxs-lookup"><span data-stu-id="e2a0f-169">Sharing accounts</span></span>](active-directory-sharing-accounts.md)

## <a name="integrating-custom-applications"></a><span data-ttu-id="e2a0f-170">사용자 지정 응용 프로그램 통합</span><span class="sxs-lookup"><span data-stu-id="e2a0f-170">Integrating custom applications</span></span>
<span data-ttu-id="e2a0f-171">새 응용 프로그램을 작성 하는 tooassist 개발자가 hello 전원 Azure AD를 활용 하는 경우 참조 [Guiding 개발자](active-directory-applications-guiding-developers-for-lob-applications.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a0f-171">If you are writing a new application and want tooassist developers in leveraging hello power Azure AD, see [Guiding developers](active-directory-applications-guiding-developers-for-lob-applications.md).</span></span>

<span data-ttu-id="e2a0f-172">Azure 응용 프로그램 갤러리에 사용자 지정 응용 프로그램 toohello tooadd을 원하는 경우 참조 ["준수 위해 자신의 앱" Azure AD 셀프 서비스 SAML 구성](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2a0f-172">If you want tooadd your custom application toohello Azure Application Gallery, see [“Bring your own app” with Azure AD Self-Service SAML configuration](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).</span></span>

## <a name="see-also"></a><span data-ttu-id="e2a0f-173">참고 항목</span><span class="sxs-lookup"><span data-stu-id="e2a0f-173">See also</span></span>
* [<span data-ttu-id="e2a0f-174">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="e2a0f-174">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

