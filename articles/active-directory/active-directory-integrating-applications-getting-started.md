---
title: "앱과 Azure AD 통합 시작 | Microsoft Docs"
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
ms.openlocfilehash: e273d27bacf6978c5056c0ab09846c26426dd12b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="integrating-azure-active-directory-with-applications-getting-started-guide"></a><span data-ttu-id="2aa09-103">응용 프로그램과 Azure Active Directory 통합 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="2aa09-103">Integrating Azure Active Directory with applications getting started guide</span></span>
## <a name="overview"></a><span data-ttu-id="2aa09-104">개요</span><span class="sxs-lookup"><span data-stu-id="2aa09-104">Overview</span></span>
<span data-ttu-id="2aa09-105">이 항목은 Azure AD(Active Directory)와 응용 프로그램을 통합하기 위한 로드맵을 제공하려는 용도로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aa09-105">This topic is intended to give you a roadmap for integrating applications with Azure Active Directory (AD).</span></span> <span data-ttu-id="2aa09-106">아래의 각 섹션에는 더 자세한 항목의 요약이 포함되므로 이 시작 가이드의 어떤 부분이 사용자와 관련 있는지 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aa09-106">Each of the sections below contain a brief summary of a more detailed topic so you can identify which parts of this getting started guide are relevant to you.</span></span>  <span data-ttu-id="2aa09-107">각 주제에 대해 자세히 알아보려면 링크를 따라갑니다.</span><span class="sxs-lookup"><span data-stu-id="2aa09-107">Follow the links for a deeper dive on each subject.</span></span>

## <a name="before-you-begin-take-inventory"></a><span data-ttu-id="2aa09-108">시작 하기 전에 인벤토리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2aa09-108">Before you begin, take inventory</span></span>
<span data-ttu-id="2aa09-109">응용 프로그램을 Azure AD와 통합하는 것을 알아보기 전에 현재 위치와 목표를 아는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="2aa09-109">Before you jump in to integrating applications with Azure AD, it is important to know where you are and where you want to go.</span></span>  <span data-ttu-id="2aa09-110">다음 질문은 Azure AD 응용 프로그램 통합 프로젝트에 대해 생각해볼 수 있도록 하기 위한 용도로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aa09-110">The following questions are intended to help you think about your Azure AD application integration project.</span></span>

### <a name="application-inventory"></a><span data-ttu-id="2aa09-111">응용 프로그램 인벤토리</span><span class="sxs-lookup"><span data-stu-id="2aa09-111">Application inventory</span></span>
* <span data-ttu-id="2aa09-112">응용 프로그램은 모두 어디에 있습니까?</span><span class="sxs-lookup"><span data-stu-id="2aa09-112">Where are all of your applications?</span></span> <span data-ttu-id="2aa09-113">누가 소유합니까?</span><span class="sxs-lookup"><span data-stu-id="2aa09-113">Who owns them?</span></span>
* <span data-ttu-id="2aa09-114">응용 프로그램에 어떤 종류의 인증이 필요합니까?</span><span class="sxs-lookup"><span data-stu-id="2aa09-114">What kind of authentication do your applications require?</span></span>
* <span data-ttu-id="2aa09-115">누가 어떤 응용 프로그램에 액세스하려 합니까?</span><span class="sxs-lookup"><span data-stu-id="2aa09-115">Who needs access to which applications?</span></span>
* <span data-ttu-id="2aa09-116">새 응용 프로그램을 배포하시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="2aa09-116">Do you want to deploy a new application?</span></span>
  * <span data-ttu-id="2aa09-117">사내에 구축하고 Azure 계산 인스턴스에 배포하시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="2aa09-117">Will you build it in-house and deploy it on an Azure compute instance?</span></span>
  * <span data-ttu-id="2aa09-118">Azure 응용 프로그램 갤러리에서 사용할 수 있는 응용 프로그램을 사용하시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="2aa09-118">Will you use one that is available in the Azure Application Gallery?</span></span>

### <a name="user-and-group-inventory"></a><span data-ttu-id="2aa09-119">사용자 및 그룹 인벤토리</span><span class="sxs-lookup"><span data-stu-id="2aa09-119">User and group inventory</span></span>
* <span data-ttu-id="2aa09-120">사용자 계정은 어디에 있습니까?</span><span class="sxs-lookup"><span data-stu-id="2aa09-120">Where do your user accounts reside?</span></span>
  * <span data-ttu-id="2aa09-121">온-프레미스 Active Directory</span><span class="sxs-lookup"><span data-stu-id="2aa09-121">On-premises Active Directory</span></span>
  * <span data-ttu-id="2aa09-122">Azure AD</span><span class="sxs-lookup"><span data-stu-id="2aa09-122">Azure AD</span></span>
  * <span data-ttu-id="2aa09-123">사용자가 소유한 별도 응용 프로그램 데이터베이스 내에서</span><span class="sxs-lookup"><span data-stu-id="2aa09-123">Within a separate application database that you own</span></span>
  * <span data-ttu-id="2aa09-124">허용되지 않은 응용 프로그램에서</span><span class="sxs-lookup"><span data-stu-id="2aa09-124">In unsanctioned applications</span></span>
  * <span data-ttu-id="2aa09-125">위의 모든 항목</span><span class="sxs-lookup"><span data-stu-id="2aa09-125">All of the above</span></span>
* <span data-ttu-id="2aa09-126">개별 사용자는 현재 어떤 사용 권한 및 역할 할당을 가지고 있습니까?</span><span class="sxs-lookup"><span data-stu-id="2aa09-126">What permissions and role assignments do individual users currently have?</span></span> <span data-ttu-id="2aa09-127">액세스를 검토해야 하거나 사용자 액세스 및 역할 할당이 적절하다고 생각합니까?</span><span class="sxs-lookup"><span data-stu-id="2aa09-127">Do you need to review their access or are you sure that your user access and role assignments are appropriate now?</span></span>
* <span data-ttu-id="2aa09-128">그룹은 온-프레미스 Active Directory 내에 만들어 집니까?</span><span class="sxs-lookup"><span data-stu-id="2aa09-128">Are groups already established in your on-premises Active Directory?</span></span>
  * <span data-ttu-id="2aa09-129">그룹을 어떻게 구성합니까?</span><span class="sxs-lookup"><span data-stu-id="2aa09-129">How are your groups organized?</span></span>
  * <span data-ttu-id="2aa09-130">그룹 멤버는 누구입니까?</span><span class="sxs-lookup"><span data-stu-id="2aa09-130">Who are the group members?</span></span>
  * <span data-ttu-id="2aa09-131">그룹은 현재 어떤 사용 권한/역할 할당을 가지고 있습니까?</span><span class="sxs-lookup"><span data-stu-id="2aa09-131">What permissions/role assignments do the groups currently have?</span></span>
* <span data-ttu-id="2aa09-132">통합하기 전에 사용자/그룹 데이터베이스를 정리해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="2aa09-132">Will you need to clean up user/group databases before integrating?</span></span>  <span data-ttu-id="2aa09-133">(매우 중요한 질문입니다.</span><span class="sxs-lookup"><span data-stu-id="2aa09-133">(This is a pretty important question.</span></span> <span data-ttu-id="2aa09-134">쓰레기를 넣고 쓰레기를 얻는 현상.)</span><span class="sxs-lookup"><span data-stu-id="2aa09-134">Garbage in, garbage out.)</span></span>

### <a name="access-management-inventory"></a><span data-ttu-id="2aa09-135">액세스 관리 인벤토리</span><span class="sxs-lookup"><span data-stu-id="2aa09-135">Access management inventory</span></span>
* <span data-ttu-id="2aa09-136">응용 프로그램에 대한 사용자 액세스를 현재 어떻게 관리합니까?</span><span class="sxs-lookup"><span data-stu-id="2aa09-136">How do you currently manage user access to applications?</span></span> <span data-ttu-id="2aa09-137">변경해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="2aa09-137">Does that need to change?</span></span>  <span data-ttu-id="2aa09-138">예를 들어 [RBAC](role-based-access-control-configure.md) 와 같이 액세스를 관리하는 다른 방법을 고려한 적이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="2aa09-138">Have you considered other ways to manage access, such as with [RBAC](role-based-access-control-configure.md) for example?</span></span>
* <span data-ttu-id="2aa09-139">누구에게 어떤 액세스가 필요합니까?</span><span class="sxs-lookup"><span data-stu-id="2aa09-139">Who needs access to what?</span></span>

<span data-ttu-id="2aa09-140">아마 이러한 모든 질문에 대한 답변은 없겠지만 괜찮습니다.</span><span class="sxs-lookup"><span data-stu-id="2aa09-140">Maybe you don't have the answers to all of these questions up front but that's okay.</span></span>  <span data-ttu-id="2aa09-141">이 가이드는 이러한 일부 질문에 대답하고 합리적인 결정을 내릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aa09-141">This guide can help you answer some of those questions and make some informed decisions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2aa09-142">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2aa09-142">Prerequisites</span></span>
* <span data-ttu-id="2aa09-143">Azure 구독 및 Azure Active Directory입니다.</span><span class="sxs-lookup"><span data-stu-id="2aa09-143">An Azure subscription and an Azure Active Directory directory.</span></span>  <span data-ttu-id="2aa09-144">Azure 구독이 아직 없는 경우 Azure를 30일 동안 무료로 사용해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aa09-144">If you don't already have an Azure subscription, you can try out Azure for free for 30 days.</span></span> [<span data-ttu-id="2aa09-145">사용해 보세요!</span><span class="sxs-lookup"><span data-stu-id="2aa09-145">Try it out!</span></span>](https://azure.microsoft.com/trial/get-started-active-directory/)

## <a name="application-integration-with-azure-ad"></a><span data-ttu-id="2aa09-146">Azure AD와 응용 프로그램 통합</span><span class="sxs-lookup"><span data-stu-id="2aa09-146">Application integration with Azure AD</span></span>
### <a name="finding-unsanctioned-cloud-applications-with-cloud-app-discovery"></a><span data-ttu-id="2aa09-147">클라우드 앱 검색을 사용하여 허용되지 않은 클라우드 응용 프로그램 찾기</span><span class="sxs-lookup"><span data-stu-id="2aa09-147">Finding unsanctioned cloud applications with Cloud App Discovery</span></span>
<span data-ttu-id="2aa09-148">위에서 설명한 대로 지금까지 조직에서 관리하지 않은 응용 프로그램이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aa09-148">As mentioned above, there may be applications that haven't been managed by your organization until now.</span></span>  <span data-ttu-id="2aa09-149">인벤토리 프로세스의 일부로 허용되지 않은 클라우드 응용 프로그램을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aa09-149">As part of the inventory process, it is possible to find unsanctioned cloud applications.</span></span> <span data-ttu-id="2aa09-150">[클라우드 앱 검색을 사용하여 허용되지 않은 클라우드 응용 프로그램 찾기](active-directory-cloudappdiscovery-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aa09-150">See [Finding unsanctioned cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

### <a name="authentication-types"></a><span data-ttu-id="2aa09-151">인증 형식</span><span class="sxs-lookup"><span data-stu-id="2aa09-151">Authentication Types</span></span>
<span data-ttu-id="2aa09-152">응용 프로그램에는 각자 다른 인증 요구 사항이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aa09-152">Each of your applications may have different authentication requirements.</span></span> <span data-ttu-id="2aa09-153">Azure AD과 함께 인증서 서명은 SAML 2.0, WS-페더레이션 또는 OpenID 연결 프로토콜 뿐만 아니라 암호 Single Sign-on을 사용하는 응용 프로그램을 사용하는 응용 프로그램과 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aa09-153">With Azure AD, signing certificates can be used with applications that use SAML 2.0, WS-Federation, or OpenID Connect Protocols as well as Password Single Sign On.</span></span> <span data-ttu-id="2aa09-154">Azure AD와 함께 사용할 응용 프로그램 인증 형식에 대한 자세한 내용은 [Azure Active Directory에서 페더레이션된 Single Sign-on에 대한 인증서 관리](active-directory-sso-certs.md) 및 [암호 기반 Single Sign On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aa09-154">For more information about application authentication types for use with Azure AD see [Managing Certificates for Federated Single Sign-On in Azure Active Directory](active-directory-sso-certs.md) and [Password based single sign on](active-directory-appssoaccess-whatis.md).</span></span>

### <a name="enabling-sso-with-azure-ad-app-proxy"></a><span data-ttu-id="2aa09-155">Azure AD 앱 프록시를 사용하는 SSO 사용</span><span class="sxs-lookup"><span data-stu-id="2aa09-155">Enabling SSO with Azure AD App Proxy</span></span>
<span data-ttu-id="2aa09-156">Microsoft Azure AD 응용 프로그램 프록시를 사용하여 어디서든 어떤 장치에서든 안전하게 개인 네트워크 내부에 위치한 응용 프로그램에 액세스를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aa09-156">With Microsoft Azure AD Application Proxy, you can provide access to applications located inside your private network securely, from anywhere and on any device.</span></span> <span data-ttu-id="2aa09-157">환경 내에서 응용 프로그램 프록시 커넥터를 설치한 후에 Azure AD를 이용하여 쉽게 구성될 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="2aa09-157">After you have installed an application proxy connector within your environment, it can be easily configured with Azure AD.</span></span>

### <a name="integrating-applications-with-azure-ad"></a><span data-ttu-id="2aa09-158">Azure AD와 응용 프로그램 통합</span><span class="sxs-lookup"><span data-stu-id="2aa09-158">Integrating applications with Azure AD</span></span>
<span data-ttu-id="2aa09-159">다음 문서에서는 응용 프로그램을 Azure AD와 통합하는 여러 가지 방법을 설명하고 일부 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2aa09-159">The following articles discuss the different ways applications integrate with Azure AD, and provide some guidance.</span></span>

* [<span data-ttu-id="2aa09-160">사용할 Active Directory 결정</span><span class="sxs-lookup"><span data-stu-id="2aa09-160">Determining which Active Directory to use</span></span>](active-directory-administer.md)
* [<span data-ttu-id="2aa09-161">Azure 응용 프로그램 갤러리에서 응용 프로그램 사용</span><span class="sxs-lookup"><span data-stu-id="2aa09-161">Using applications in the Azure application gallery</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="2aa09-162">SaaS 응용 프로그램 통합 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="2aa09-162">Integrating SaaS applications tutorials list</span></span>](active-directory-saas-tutorial-list.md)

## <a name="managing-access-to-applications"></a><span data-ttu-id="2aa09-163">응용 프로그램에 대한 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="2aa09-163">Managing access to applications</span></span>
<span data-ttu-id="2aa09-164">다음 문서는 응용 프로그램이 Azure AD와 통합되면 Azure AD 커넥터 및 Azure AD를 사용하여 응용 프로그램에 대한 액세스를 관리할 수 있는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2aa09-164">The following articles describe ways you can manage access to applications once they have been integrated with Azure AD using Azure AD Connectors and Azure AD.</span></span>

* [<span data-ttu-id="2aa09-165">Azure AD를 사용하는 앱에 대한 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="2aa09-165">Managing access to apps using Azure AD</span></span>](active-directory-managing-access-to-apps.md)
* [<span data-ttu-id="2aa09-166">Azure AD 커넥터를 사용하여 자동화</span><span class="sxs-lookup"><span data-stu-id="2aa09-166">Automating with Azure AD Connectors</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="2aa09-167">응용 프로그램에 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="2aa09-167">Assigning users to an application</span></span>](active-directory-applications-guiding-developers-assigning-users.md)
* [<span data-ttu-id="2aa09-168">응용 프로그램에 그룹 지정</span><span class="sxs-lookup"><span data-stu-id="2aa09-168">Assigning groups to an application</span></span>](active-directory-applications-guiding-developers-assigning-groups.md)
* [<span data-ttu-id="2aa09-169">계정 공유</span><span class="sxs-lookup"><span data-stu-id="2aa09-169">Sharing accounts</span></span>](active-directory-sharing-accounts.md)

## <a name="integrating-custom-applications"></a><span data-ttu-id="2aa09-170">사용자 지정 응용 프로그램 통합</span><span class="sxs-lookup"><span data-stu-id="2aa09-170">Integrating custom applications</span></span>
<span data-ttu-id="2aa09-171">전원 Azure AD를 활용하여 새 응용 프로그램을 작성하고 개발자를 지원하려면 [개발자 가이드](active-directory-applications-guiding-developers-for-lob-applications.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aa09-171">If you are writing a new application and want to assist developers in leveraging the power Azure AD, see [Guiding developers](active-directory-applications-guiding-developers-for-lob-applications.md).</span></span>

<span data-ttu-id="2aa09-172">Azure 응용 프로그램 갤러리에 사용자 지정 응용 프로그램을 추가하려는 경우 [Azure AD 셀프 서비스 SAML 구성을 사용하여 "앱 가져오기"](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2aa09-172">If you want to add your custom application to the Azure Application Gallery, see [“Bring your own app” with Azure AD Self-Service SAML configuration](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).</span></span>

## <a name="see-also"></a><span data-ttu-id="2aa09-173">참고 항목</span><span class="sxs-lookup"><span data-stu-id="2aa09-173">See also</span></span>
* [<span data-ttu-id="2aa09-174">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="2aa09-174">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

