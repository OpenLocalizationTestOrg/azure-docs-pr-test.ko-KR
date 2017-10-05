---
title: "Azure Active Directory B2B 공동 작업이란? | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업은 비즈니스 파트너가 선택적으로 회사 응용 프로그램에 액세스할 수 있게 함으로써 회사 간 관계를 지원합니다."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 1464387b-ee8b-4c7c-94b3-2c5567224c27
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 06/27/2017
ms.author: curtand
ms.custom: aaddev
ms.reviewer: sasubram
ms.openlocfilehash: fbc12a52555b190d43b5e953fd4d19923a25b0ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-ad-b2b-collaboration"></a><span data-ttu-id="c3376-104">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="c3376-104">What is Azure AD B2B collaboration?</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/AhwrweCBdsc" frameborder="0" allowfullscreen></iframe>

<span data-ttu-id="c3376-105">Azure AD B2B(Business-to-Business) 공동 작업 기능을 통해 Azure AD를 사용하는 모든 조직은 크든 작든, 다른 조직의 사용자와 안전하게 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3376-105">Azure AD business-to-business (B2B) collaboration capabilities enable any organization using Azure AD to work safely and securely with users from any other organization, small or large.</span></span> <span data-ttu-id="c3376-106">이러한 조직은 Azure AD가 있거나 없을 수 있고, IT 조직이 있거나 없을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3376-106">Those organizations can be with Azure AD or without, or even with an IT organization or without.</span></span> 

<span data-ttu-id="c3376-107">Azure AD를 사용하는 조직은 회사 데이터를 완전하게 제어하면서 파트너가 문서, 리소스 및 응용 프로그램에 액세스하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3376-107">Organizations using Azure AD can provide access to documents, resources, and applications to their partners, while maintaining complete control over their own corporate data.</span></span> <span data-ttu-id="c3376-108">개발자는 Azure AD B2B API를 사용하여 두 조직을 안전한 방식으로 결합하는 응용 프로그램을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3376-108">Developers can use the Azure AD business-to-business APIs to write applications that bring two organizations together in more securely.</span></span> <span data-ttu-id="c3376-109">또한 최종 사용자가 탐색하기도 매우 편리합니다.</span><span class="sxs-lookup"><span data-stu-id="c3376-109">Also, it's pretty easy for end users to navigate.</span></span>

<span data-ttu-id="c3376-110">고객 중 97%가 Azure AD B2B 공동 작업이 매우 중요하다고 말했습니다.</span><span class="sxs-lookup"><span data-stu-id="c3376-110">97% of our customers have told us Azure AD B2B collaboration is very important to them.</span></span>

![원형 차트](media/active-directory-b2b-what-is-azure-ad-b2b/97-percent-support.png)

<span data-ttu-id="c3376-112">2017년 4월 초를 기준으로 Azure AD B2B 공동 작업 기능을 사용하는 사용자 수는 이미 약 3백만 명에 도달했습니다.</span><span class="sxs-lookup"><span data-stu-id="c3376-112">As of early April 2017, we had about 3 million users already using Azure AD B2B collaboration capabilities.</span></span> <span data-ttu-id="c3376-113">또한 10명 이상의 사용자가 있는 Azure AD 조직의 23% 이상이 이미 이러한 기능을 활용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3376-113">And more than 23% of Azure AD organizations that have more than 10 users are already benefiting from these capabilities.</span></span>

## <a name="the-key-benefits-of-azure-ad-b2b-collaboration-to-your-organization"></a><span data-ttu-id="c3376-114">조직에 대한 Azure AD B2B 공동 작업의 주요 이점</span><span class="sxs-lookup"><span data-stu-id="c3376-114">The key benefits of Azure AD B2B collaboration to your organization</span></span>

### <a name="work-with-any-user-from-any-partner"></a><span data-ttu-id="c3376-115">파트너의 사용자와 함께 작업</span><span class="sxs-lookup"><span data-stu-id="c3376-115">Work with any user from any partner</span></span>

* <span data-ttu-id="c3376-116">파트너가 자체 자격 증명을 사용함</span><span class="sxs-lookup"><span data-stu-id="c3376-116">Partners use their own credentials</span></span>

* <span data-ttu-id="c3376-117">파트너가 Azure AD를 사용할 필요가 없음</span><span class="sxs-lookup"><span data-stu-id="c3376-117">No requirement for partners to use Azure AD</span></span>

* <span data-ttu-id="c3376-118">외부 디렉터리 또는 복잡한 설정이 필요하지 않음</span><span class="sxs-lookup"><span data-stu-id="c3376-118">No external directories or complex set-up required</span></span>

### <a name="simple-and-secure-collaboration"></a><span data-ttu-id="c3376-119">간단하고 안전한 공동 작업</span><span class="sxs-lookup"><span data-stu-id="c3376-119">Simple and secure collaboration</span></span>

* <span data-ttu-id="c3376-120">정교한 Azure AD 기반 권한 부여 정책을 적용하면서 회사 앱 및 데이터에 액세스하도록 함</span><span class="sxs-lookup"><span data-stu-id="c3376-120">Provide access to any corporate app or data, while applying sophisticated, Azure AD-powered authorization policies</span></span>

* <span data-ttu-id="c3376-121">사용자에게 편리</span><span class="sxs-lookup"><span data-stu-id="c3376-121">Easy for users</span></span>

* <span data-ttu-id="c3376-122">앱 및 데이터에 대한 엔터프라이즈급 보안</span><span class="sxs-lookup"><span data-stu-id="c3376-122">Enterprise-grade security for apps and data</span></span>

### <a name="no-management-overhead"></a><span data-ttu-id="c3376-123">관리 오버헤드 없음</span><span class="sxs-lookup"><span data-stu-id="c3376-123">No management overhead</span></span>

* <span data-ttu-id="c3376-124">외부 계정 또는 암호 관리 없음</span><span class="sxs-lookup"><span data-stu-id="c3376-124">No external account or password management</span></span>

* <span data-ttu-id="c3376-125">동기화 또는 수동 계정 수명 주기 관리 없음</span><span class="sxs-lookup"><span data-stu-id="c3376-125">No sync or manual account lifecycle management</span></span>

* <span data-ttu-id="c3376-126">외부 관리 오버헤드 없음</span><span class="sxs-lookup"><span data-stu-id="c3376-126">No external administrative overhead</span></span>

## <a name="you-can-easily-add-b2b-collaboration-users-to-your-organization"></a><span data-ttu-id="c3376-127">조직에 B2B 공동 작업 사용자를 쉽게 추가할 수 있음</span><span class="sxs-lookup"><span data-stu-id="c3376-127">You can easily add B2B collaboration users to your organization</span></span>

<span data-ttu-id="c3376-128">관리자는 B2B 공동 작업(게스트) 사용자를 [Azure Portal](https://portal.azure.com)에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3376-128">Admins can add B2B collaboration (guest) users in the [Azure portal](https://portal.azure.com).</span></span>

![게스트 사용자 추가](media/active-directory-b2b-what-is-azure-ad-b2b/adding-b2b-users-admin.png)

### <a name="enable-your-collaborators-to-bring-their-own-identity"></a><span data-ttu-id="c3376-130">공동 작업자가 자신의 ID를 사용하도록 할 수 있음</span><span class="sxs-lookup"><span data-stu-id="c3376-130">Enable your collaborators to bring their own identity</span></span>

<span data-ttu-id="c3376-131">B2B 공동 작업자는 자신이 선택한 ID로 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3376-131">B2B collaborators can sign in with an identity of their choice.</span></span> <span data-ttu-id="c3376-132">사용자에게 Microsoft 계정 또는 Azure AD 계정이 없는 경우 제품 사용 시 계정이 원활하게 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3376-132">If the user doesn’t have a Microsoft account or an Azure AD account – one is created for them seamlessly at the time for offer redemption.</span></span>

![로그인 ID 선택](media/active-directory-b2b-what-is-azure-ad-b2b/sign-in-identity-choice.png)

### <a name="delegate-to-application-and-group-owners"></a><span data-ttu-id="c3376-134">응용 프로그램 및 그룹 소유자에게 위임</span><span class="sxs-lookup"><span data-stu-id="c3376-134">Delegate to application and group owners</span></span> 
<span data-ttu-id="c3376-135">응용 프로그램 및 그룹 소유자는 Microsoft 응용 프로그램이든 아니든 관계없이 관리하는 응용 프로그램에 직접 B2B 사용자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3376-135">Application and group owners can add B2B users directly to any application that you care about, whether it is a Microsoft application or not.</span></span> <span data-ttu-id="c3376-136">관리자는 B2B 사용자를 추가할 권한을 관리자가 아닌 사용자에게 위임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3376-136">Admins can delegate permission to add B2B users to non-admins.</span></span> <span data-ttu-id="c3376-137">관리자가 아닌 사용자는 [Azure AD Application Access Panel](https://myapps.microsoft.com)(Azure AD 응용 프로그램 액세스 패널)을 사용하여 B2B 공동 작업 사용자가 응용 프로그램이나 그룹에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3376-137">Non-admins can use the [Azure AD Application Access Panel](https://myapps.microsoft.com) to add B2B collaboration users to applications or groups.</span></span>

![액세스 패널](media/active-directory-b2b-what-is-azure-ad-b2b/access-panel.png)

![구성원 추가](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="authorization-policies-protect-your-corporate-content"></a><span data-ttu-id="c3376-140">권한 부여 정책으로 회사 콘텐츠 보호</span><span class="sxs-lookup"><span data-stu-id="c3376-140">Authorization policies protect your corporate content</span></span>

<span data-ttu-id="c3376-141">다단계 인증 등의 조건부 액세스 정책을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3376-141">Conditional access policies, such as multi-factor authentication, can be enforced:</span></span>
- <span data-ttu-id="c3376-142">테넌트 수준에서 적용</span><span class="sxs-lookup"><span data-stu-id="c3376-142">At the tenant level</span></span>
- <span data-ttu-id="c3376-143">응용 프로그램 수준에서 적용</span><span class="sxs-lookup"><span data-stu-id="c3376-143">At the application level</span></span>
- <span data-ttu-id="c3376-144">회사 앱과 데이터를 보호하기 위해 특정 사용자에 대해 적용</span><span class="sxs-lookup"><span data-stu-id="c3376-144">For specific users to protect corporate apps and data</span></span>

![구성원 추가](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="use-our-apis-and-sample-code-to-easily-build-applications-to-onboard"></a><span data-ttu-id="c3376-146">API 및 샘플 코드를 사용하여 등록할 응용 프로그램을 쉽게 빌드할 수 있음</span><span class="sxs-lookup"><span data-stu-id="c3376-146">Use our APIs and sample code to easily build applications to onboard</span></span>
<span data-ttu-id="c3376-147">조직의 요구에 맞게 사용자 지정된 방식으로 외부 파트너를 등록하세요.</span><span class="sxs-lookup"><span data-stu-id="c3376-147">Bring your external partners on board in ways customized to your organization’s needs.</span></span>

<span data-ttu-id="c3376-148">[B2B 공동 작업 초대 API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)를 사용하면 셀프 서비스 등록 포털 생성을 포함하여 등록 환경을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3376-148">Using the [B2B collaboration invitation APIs](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation), you can customize your onboarding experiences, including creating self-service sign-up portals.</span></span> <span data-ttu-id="c3376-149">셀프 서비스 포털에 대한 샘플 코드는 [Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3376-149">We provide sample code for a self-service portal [on Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

![등록 포털](media/active-directory-b2b-what-is-azure-ad-b2b/sign-up-portal.png)

<span data-ttu-id="c3376-151">Azure AD B2B 공동 작업에서는 Azure AD를 완전히 활용하여 최종 사용자가 간편하고 직관적으로 찾는 방식으로 파트너 관계를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3376-151">With Azure AD B2B collaboration, you can get the full power of Azure AD to protect your partner relationships in a way that end users find easy and intuitive.</span></span> <span data-ttu-id="c3376-152">지금 외부 공동 작업에 이미 Azure AD B2B를 사용 중인 수천 개 조직에 참여하세요!</span><span class="sxs-lookup"><span data-stu-id="c3376-152">So go ahead, join the thousands of organizations that are already using Azure AD B2B for their external collaboration!</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3376-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c3376-153">Next steps</span></span>

* <span data-ttu-id="c3376-154">관리자 환경은 [Azure Portal](https://portal.azure.com)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3376-154">Administrator experiences are found in the [Azure portal](https://portal.azure.com).</span></span>

* <span data-ttu-id="c3376-155">정보 근로자 환경은 [Access Panel](https://myapps.microsoft.com)(액세스 패널)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3376-155">Information worker experiences are available in the [Access Panel](https://myapps.microsoft.com).</span></span>

* <span data-ttu-id="c3376-156">또한 피드백, 논의 사항 및 제안이 있는 경우 언제나처럼 [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b)(Microsoft 기술 커뮤니티)를 통해 제품 팀에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3376-156">And, as always, connect with the product team for any feedback, discussions, and suggestions through our [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).</span></span>

<span data-ttu-id="c3376-157">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="c3376-157">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="c3376-158">Azure Active Directory 관리자가 B2B 공동 작업 사용자를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="c3376-158">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="c3376-159">정보 근로자가 B2B 공동 작업 사용자를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="c3376-159">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="c3376-160">B2B 공동 작업 초대 전자 메일의 요소</span><span class="sxs-lookup"><span data-stu-id="c3376-160">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="c3376-161">B2B 공동 작업 초대 상환</span><span class="sxs-lookup"><span data-stu-id="c3376-161">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="c3376-162">Azure AD B2B 공동 작업 라이선스</span><span class="sxs-lookup"><span data-stu-id="c3376-162">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="c3376-163">Azure Active Directory B2B 공동 작업 문제 해결</span><span class="sxs-lookup"><span data-stu-id="c3376-163">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="c3376-164">Azure Active Directory B2B 공동 작업 자주 묻는 질문(FAQ)</span><span class="sxs-lookup"><span data-stu-id="c3376-164">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="c3376-165">Azure Active Directory B2B 공동 작업 API 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="c3376-165">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="c3376-166">B2B 공동 작업 사용자에 대한 다단계 인증</span><span class="sxs-lookup"><span data-stu-id="c3376-166">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="c3376-167">초대 없이 B2B 공동 작업 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="c3376-167">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="c3376-168">B2B 공동 작업 사용자 감사 및 보고</span><span class="sxs-lookup"><span data-stu-id="c3376-168">B2B collaboration user auditing and reporting</span></span>](active-directory-b2b-auditing-and-reporting.md)
* [<span data-ttu-id="c3376-169">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="c3376-169">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
