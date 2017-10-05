---
title: "Azure Active Directory와 응용 프로그램 관리 | Microsoft Docs"
description: "이 문서는 온-프레미스, 클라우드 및 SaaS 응용 프로그램을 사용하여 Azure Active Directory를 통합하는 이점을 얻을 수 있습니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 95b96f10-2d5c-4b78-8af8-d3657a24140f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: b8f0cfdb468094bc761d6b939ca318fcfbea3ea4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="managing-applications-with-azure-active-directory"></a><span data-ttu-id="c7747-103">Azure Active Directory로 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="c7747-103">Managing Applications with Azure Active Directory</span></span>
<span data-ttu-id="c7747-104">실제 워크플로 또는 콘텐츠를 넘어 비즈니스에는 모든 응용 프로그램에 대한 두 가지 기본 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-104">Beyond the actual workflow or content, businesses have two basic requirements for all applications:</span></span>

1. <span data-ttu-id="c7747-105">생산성을 높이려면 응용 프로그램을 쉽게 검색하고 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-105">To increase productivity, applications should be easy to discover and access</span></span>
2. <span data-ttu-id="c7747-106">보안 및 관리를 사용하려면 조직은 각 응용 프로그램에 실제로 액세스할 수 있는 사람을 제어하고 감독해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-106">To enable security and governance, the organization needs control and oversight on who can and actually is accessing each application</span></span>

<span data-ttu-id="c7747-107">클라우드 응용 프로그램의 세계에서는 ID를 사용하여 “*누가 무엇을 수행할 수 있는지*”를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-107">In the world of cloud applications this can best be achieved using identity to control “*WHO is allowed to do WHAT*”.</span></span>

<span data-ttu-id="c7747-108">용어 계산에서</span><span class="sxs-lookup"><span data-stu-id="c7747-108">In computing terminology:</span></span>

* <span data-ttu-id="c7747-109">*누가*는 *ID*라고 합니다. - 사용자 및 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="c7747-109">*Who* is known as *identity* - the management of users and groups</span></span>
* <span data-ttu-id="c7747-110">*무엇*은 *액세스 관리*입니다. - 보호된 리소스에 대한 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="c7747-110">*What* is known as *access management* – the management of access to protected resources</span></span>

<span data-ttu-id="c7747-111">두 구성 요소는 모두 *IAM(ID 및 액세스 관리)*으로 알려져 있으며 [Gartner](http://www.gartner.com/it-glossary/identity-and-access-management-iam) 그룹에서 “*적당한 사람이 적당한 때에 적당한 이유로 적당한 리소스에 액세스할 수 있도록 하는 보안 분야*”로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-111">Both components together are known as *Identity and Access Management (IAM)*, which is defined by the [Gartner](http://www.gartner.com/it-glossary/identity-and-access-management-iam) group as “*the security discipline that enables the right individuals to access the right resources at the right times for the right reasons*”.</span></span>

<span data-ttu-id="c7747-112">그럼 무엇이 문제입니까?</span><span class="sxs-lookup"><span data-stu-id="c7747-112">Okay, so what’s the problem?</span></span> <span data-ttu-id="c7747-113">IAM이 한 곳에서 통합 솔루션으로 *관리되지 않는* 경우 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-113">If IAM is *not managed* in one place with an integrated solution:</span></span>

* <span data-ttu-id="c7747-114">ID 관리자는 모든 응용 프로그램에서 개별적으로 사용자 계정을 만들고 업데이트해야 하며 이는 중복되고 시간이 많이 걸리는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-114">Identity administrators have to individually create and update user accounts in all applications separately, a redundant and time consuming activity.</span></span>
* <span data-ttu-id="c7747-115">사용자는 작업에 필요한 응용 프로그램에 액세스하기 위해 여러 자격 증명을 기억해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-115">Users have to memorize multiple credentials to access the applications they need to work with.</span></span> <span data-ttu-id="c7747-116">결과적으로 사용자는 자신의 암호를 적거나 기타 데이터 보안 위험을 소개하는 다른 암호 관리 솔루션을 사용하는 경향이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-116">As a result, users tend to write down their passwords or use other password management solutions which introduces other data security risks.</span></span>
* <span data-ttu-id="c7747-117">중복되고 시간이 많이 걸리는 작업은 사용자 및 관리자가 비즈니스의 이익을 증가시키는 비즈니스 활동에서 작업하는 시간을 감소시킵니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-117">Redundant, time consuming activities reduce the amount of time users and administrators are working on business activities that increase your business’s bottom line.</span></span>

<span data-ttu-id="c7747-118">따라서 무엇이 일반적으로 조직이 통합된 IAM 솔루션을 채택하지 못하게 합니까?</span><span class="sxs-lookup"><span data-stu-id="c7747-118">So, what generally prevents organizations from adopting integrated IAM solutions?</span></span>

* <span data-ttu-id="c7747-119">대부분의 기술 솔루션은 각 조직에서 고유의 응용 프로그램에 배포하고 적용해야 하는 소프트웨어 플랫폼을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-119">Most technical solutions are based on software platforms that need to be deployed and adapted by each organization for their own applications.</span></span>
* <span data-ttu-id="c7747-120">종종 클라우드 응용 프로그램은 IT 조직이 기존 IAM 솔루션을 통합할 수 있는 것 보다 빠른 속도로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-120">Cloud applications are often adopted at a higher rate than IT organization can integrate with existing IAM solutions.</span></span>
* <span data-ttu-id="c7747-121">보안 및 모니터링 도구는 포괄적인 E2E 시나리오를 달성하기 위해 추가 사용자 지정 및 통합이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-121">Security and monitoring tooling require additional customization and integration to achieve comprehensive E2E scenarios.</span></span>

## <a name="azure-active-directory-integrated-with-applications"></a><span data-ttu-id="c7747-122">응용 프로그램과 통합된 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c7747-122">Azure Active Directory integrated with applications</span></span>
<span data-ttu-id="c7747-123">Azure Active Directory는 Microsoft의 포괄적인 IDaaS(Identity as a Service) 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-123">Azure Active Directory is Microsoft’s comprehensive Identity as a Service (IDaaS) solution that:</span></span>

* <span data-ttu-id="c7747-124">클라우드 서비스로 IAM 사용</span><span class="sxs-lookup"><span data-stu-id="c7747-124">Enables IAM as a cloud service</span></span> 
* <span data-ttu-id="c7747-125">중앙 액세스 관리, SSO(Single Sign-On) 및 보고 제공</span><span class="sxs-lookup"><span data-stu-id="c7747-125">Provides central access management, single-sign on (SSO), and reporting</span></span> 
* <span data-ttu-id="c7747-126">Salesforce, Google Apps, Box, Concur 등을 포함하여 응용 프로그램 갤러리에서 [수천 개의 응용 프로그램](https://azure.microsoft.com/marketplace/active-directory/) 에 대한 통합된 액세스 관리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-126">Supports integrated access management for [thousands of applications](https://azure.microsoft.com/marketplace/active-directory/) in the application gallery, including Salesforce, Google Apps, Box, Concur, and more.</span></span> 

<span data-ttu-id="c7747-127">Azure Active Directory를 사용하여 파트너 및 고객(비즈니스 또는 소비자)을 위해 게시한 모든 응용 프로그램에는 동일한 ID 및 액세스 관리 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-127">With Azure Active Directory, all applications you publish for your partners and customers (business or consumer) have the same identity and access management capabilities.</span></span><br> <span data-ttu-id="c7747-128">이렇게 하면 운영 비용을 크게 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-128">This enables you to significantly reduce your operational costs.</span></span>

<span data-ttu-id="c7747-129">응용 프로그램 갤러리에 아직 나열되지 않은 응용 프로그램을 구현해야 하는 경우 어떻게 합니까?</span><span class="sxs-lookup"><span data-stu-id="c7747-129">What if you need to implement an application that is not yet listed in the application gallery?</span></span> <span data-ttu-id="c7747-130">응용 프로그램 갤러리에서 응용 프로그램에 SSO를 구성하는 것 보다 약간 더 시간이 걸리지만 Azure AD는 구성에 도움이 되는 마법사를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-130">While this is a bit more time-consuming than configuring SSO for applications from the application gallery, Azure AD provides you with a wizard that helps you with the configuration.</span></span>

<span data-ttu-id="c7747-131">Azure AD의 값은 “그저” 클라우드 응용 프로그램의 수준을 넘어섭니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-131">The value of Azure AD goes beyond “just” cloud applications.</span></span> <span data-ttu-id="c7747-132">또한 보안된 원격 액세스를 제공하여 온-프레미스 응용 프로그램과 함께 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-132">You can also use it with on-premises applications by providing secure remote access.</span></span> <span data-ttu-id="c7747-133">보안된 원격 액세스를 사용하면 VPN 또는 기타 기존의 원격 액세스 관리 구현이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-133">With secure remote access, you can eliminate the the need for VPNs or other traditional remote access management implementations.</span></span>

<span data-ttu-id="c7747-134">모든 응용 프로그램에 대한 중앙 액세스 관리 및 SSO(Single Sign On)를 제공하여 Azure AD는 주요 데이터 보안 및 생산성 문제에 대한 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-134">By providing central access management and single sign on (SSO) for all your applications, Azure AD provides the solution to the main data security and productivity problems.</span></span>

* <span data-ttu-id="c7747-135">사용자는 한 번의 로그온으로 여러 응용 프로그램에 액세스하여 수입을 만들거나 비즈니스 작업이 이루어지는 데 더 많은 시간을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-135">Users can access multiple applications with one sign on giving more time to income generating or business operations activities done.</span></span>
* <span data-ttu-id="c7747-136">ID 관리자는 한 곳에서 응용 프로그램에 대한 액세스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-136">Identity administrators can manage access to applications in one place.</span></span>

<span data-ttu-id="c7747-137">사용자 및 회사에 주는 혜택은 분명합니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-137">The benefit for the user and for your company is obvious.</span></span> <span data-ttu-id="c7747-138">ID 관리자 및 조직에 대한 혜택은 좀 더 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-138">Let’s take a closer look at the benefits for an identity administrator and the organization.</span></span>

## <a name="integrated-application-benefits"></a><span data-ttu-id="c7747-139">통합된 응용 프로그램 혜택</span><span class="sxs-lookup"><span data-stu-id="c7747-139">Integrated application benefits</span></span>
<span data-ttu-id="c7747-140">SSO 프로세스는 두 단계로 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-140">The SSO process has two steps:</span></span>

* <span data-ttu-id="c7747-141">인증은 사용자 ID의 유효성을 검사하는 과정입니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-141">Authentication, the process of validating the user’s identity.</span></span>
* <span data-ttu-id="c7747-142">권한 부여는 액세스 정책을 사용하여 리소스에 대한 액세스를 활성화 또는 차단하도록 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-142">Authorization, the decision to enable or block access to a resource with an access policy.</span></span>

<span data-ttu-id="c7747-143">Azure AD를 사용하여 응용 프로그램을 관리하고 SSO를 사용하도록 설정하는 경우 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-143">When using Azure AD to manage applications and enable SSO:</span></span>

* <span data-ttu-id="c7747-144">인증은 사용자의 온-프레미스(예: AD) 또는 Azure AD 계정에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-144">Authentication is done on the user’s on-premises (e.g. AD) or Azure AD account.</span></span>
* <span data-ttu-id="c7747-145">권한 부여는 일관된 최종 사용자 환경을 보장하고 내부 기능에 관계 없이 모든 응용 프로그램에 할당, 위치 및 MFA 조건을 추가하여 Azure AD에서 할당 및 보호 정책을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-145">Authorization executes on the Azure AD assignment and protection policy ensuring consistent end user experience and enabling you to add assignment, locations, and MFA conditions on any application, regardless of its internal capabilities.</span></span>

<span data-ttu-id="c7747-146">권한 부여가 대상 응용 프로그램에서 시행되는 방식은 응용 프로그램이 Azure AD와 통합된 방법에 따라 달라진다는 점을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-146">It important to understand that the way the authorization is enacted on the target application varies depending on how the application was integrated with Azure AD.</span></span>

* <span data-ttu-id="c7747-147">**서비스 공급자에 의해 미리 통합된 응용 프로그램** Office 365나 Azure와 같이 이러한 응용 프로그램은 Azure AD에서 직접 작성하고 해당되는 포괄적인 ID 및 액세스 관리 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-147">**Applications pre-integrated by service provider** Like Office 365 and Azure, these are applications built directly on Azure AD and relying on it for their comprehensive identity and access management capabilities.</span></span> <span data-ttu-id="c7747-148">이러한 응용 프로그램에 대한 액세스는 디렉터리 정보 및 토큰 발급을 통해 사용되도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-148">Access to these applications is enabled through directory information and token issuance.</span></span>
* <span data-ttu-id="c7747-149">**Microsoft 및 사용자 지정 응용 프로그램에서 통합된 응용 프로그램** 내부 응용 프로그램 디렉터리를 사용하고 Azure AD와 독립적으로 작동할 수 있는 독립적인 클라우드 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-149">**Applications pre-integrated by Microsoft and custom applications** These are independent cloud applications that rely on an internal application directory and can operate independently of Azure AD.</span></span> <span data-ttu-id="c7747-150">이러한 응용 프로그램에 대한 액세스는 응용 프로그램 계정이 매핑되는 응용 프로그램 특정 자격 증명을 발급하여 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-150">Access to these applications is enabled by issuing an application specific credential mapped to an application account.</span></span> <span data-ttu-id="c7747-151">응용 프로그램 기능에 따라 자격 증명은 응용 프로그램에서 이전에 프로비전된 계정의 페더레이션 토큰 또는 사용자 이름 및 암호일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-151">Depending on the application capabilities, the credential may be a federation token or user-name and password for an account that was previously provisioned in the application.</span></span>
* <span data-ttu-id="c7747-152">**온-프레미스 응용 프로그램** 기본적으로 온-프레미스 응용 프로그램에 대한 액세스를 사용하여 Azure AD 응용 프로그램 프록시를 통해 게시된 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-152">**On-premises applications** Applications published through the Azure AD application proxy primarily enabling access to on-premises applications.</span></span> <span data-ttu-id="c7747-153">이러한 응용 프로그램은 Windows Server Active Directory와 같은 온-프레미스 디렉터리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-153">These applications rely on a central on-premises directory like Windows Server Active Directory.</span></span> <span data-ttu-id="c7747-154">이러한 응용 프로그램에 대한 액세스를 사용하면 온-프레미스 로그인 요구 사항을 적용하는 동안 프록시를 트리거하여 최종 사용자에게 응용 프로그램 콘텐츠를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-154">Access to these applications is enabled by triggering the proxy to deliver the application content to the end user while honoring the on-premises sign-on requirement.</span></span>

<span data-ttu-id="c7747-155">예를 들어 사용자가 조직에 합류하는 경우 기본 로그인 작업에 Azure AD의 사용자에 대한 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-155">For example, if a user joins your organization, you need to create an account for the user in Azure AD for the primary sign-on operations.</span></span> <span data-ttu-id="c7747-156">이 사용자가 Salesforce와 같은 관리 응용 프로그램에 대한 액세스를 필요로 하는 경우 또한 Salesforce에서 이 사용자에 대한 계정을 만들고 Azure 계정에 연결하여 SSO를 작동시킵니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-156">If this user requires access to a managed application such as Salesforce, you also need to create an account for this user in Salesforce and link it to the Azure account to make SSO work.</span></span> <span data-ttu-id="c7747-157">사용자가 조직을 떠나는 경우 Azure AD 계정 및 사용자가 액세스한 응용 프로그램의 IAM 스토어에서 모든 해당 사용자 계정을 삭제하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-157">When the user leaves your organization, it is advisable to delete the Azure AD account and all counterpart accounts in the IAM stores of the applications the user had access to.</span></span>

## <a name="access-detection"></a><span data-ttu-id="c7747-158">액세스 감지</span><span class="sxs-lookup"><span data-stu-id="c7747-158">Access detection</span></span>
<span data-ttu-id="c7747-159">오늘날 기업에서 IT 부서가 사용되는 클라우드 응용 프로그램의 일부를 인지하지 못하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-159">In modern enterprises, IT departments are often not aware of all the cloud applications that are being used.</span></span> <span data-ttu-id="c7747-160">클라우드 앱 검색과 함께 Azure AD는 이러한 응용 프로그램을 검색하는 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-160">In conjunction with Cloud App Discovery, Azure AD provides you with a solution to detect these applications.</span></span>

## <a name="account-management"></a><span data-ttu-id="c7747-161">계정 관리</span><span class="sxs-lookup"><span data-stu-id="c7747-161">Account management</span></span>
<span data-ttu-id="c7747-162">일반적으로 다양한 응용 프로그램의 계정을 관리하는 작업은 조직의 IT 또는 지원 담당자가 수행하는 수동 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-162">Traditionally, managing accounts in the various applications is a manual process performed by IT or support personal in the organization.</span></span> <span data-ttu-id="c7747-163">Azure AD는 모든 서비스 공급자 통합 응용 프로그램에 걸쳐 계정 관리를 완전히 자동화했으며 해당 응용 프로그램은 Microsoft가 지원하는 자동화된 사용자 프로비전 또는 SAML JIT에서 사전 통합되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-163">Azure AD fully automated account management across all service provider integrated applications and those applications pre-integrated by Microsoft supporting automated user provisioning or SAML JIT.</span></span>

## <a name="automated-user-provisioning"></a><span data-ttu-id="c7747-164">자동화된 사용자 프로비전</span><span class="sxs-lookup"><span data-stu-id="c7747-164">Automated user provisioning</span></span>
<span data-ttu-id="c7747-165">일부 응용 프로그램은 계정 만들기 및 제거(또는 비활성화)에 자동화 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-165">Some applications provide automation interfaces for creation and removal (or deactivation) of accounts.</span></span> <span data-ttu-id="c7747-166">공급자가 이러한 인터페이스를 제공하는 경우 Azure AD에서 활용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-166">If a provider offers such an interface, it is leveraged by Azure AD.</span></span> <span data-ttu-id="c7747-167">관리 작업이 자동으로 발생하기 때문에 운영 비용을 감소하고 무단으로 액세스할 가능성이 줄어들기 때문에 사용자 환경의 보안을 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-167">This reduces your operational costs because administrative tasks happen automatically, and improves the security of your environment because it decreases the chance of unauthorized access.</span></span>

## <a name="access-management"></a><span data-ttu-id="c7747-168">액세스 관리</span><span class="sxs-lookup"><span data-stu-id="c7747-168">Access management</span></span>
<span data-ttu-id="c7747-169">Azure AD를 사용하여 개별 또는 규칙 기반 할당을 사용하는 응용 프로그램에 대한 액세스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-169">Using Azure AD you can manage access to applications using individual or rule driven assignments.</span></span> <span data-ttu-id="c7747-170">또한 최상의 감독을 보장하고 Helpdesk의 부담을 줄이는 조직에서 적당한 사람에게 액세스 관리를 위임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-170">You can also delegate access management to the right people in the organization ensuring the best oversight and reducing the burden on helpdesk.</span></span>

## <a name="on-premises-applications"></a><span data-ttu-id="c7747-171">온-프레미스 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="c7747-171">On-premises applications</span></span>
<span data-ttu-id="c7747-172">기본 제공 응용 프로그램 프록시를 사용하면 결과적으로 사용자에게 최신 클라우드 응용 프로그램과 함께 일관된 액세스 환경 및 Azure AD 모니터링, 보고 및 보안 기능에서 혜택을 주어 온-프레미스 응용 프로그램을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-172">The built in application proxy enables you to publish your on-premises applications to your users resulting in both consistent access experience with modern cloud application and the benefits from Azure AD monitoring, reporting, and security capabilities.</span></span>

## <a name="reporting-and-monitoring"></a><span data-ttu-id="c7747-173">보고 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="c7747-173">Reporting and monitoring</span></span>
<span data-ttu-id="c7747-174">Azure AD는 응용 프로그램에 액세스하는 사람과 응용 프로그램을 실제로 사용한 시간을 알 수 있도록 사전 통합된 보고 및 모니터링 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-174">Azure AD provides you with pre-integrated reporting and monitoring capabilities that enable you to know who has access to applications and when they actually used them.</span></span>

## <a name="related-capabilities"></a><span data-ttu-id="c7747-175">관련 기능</span><span class="sxs-lookup"><span data-stu-id="c7747-175">Related capabilities</span></span>
<span data-ttu-id="c7747-176">Azure AD를 사용하여 세부적인 액세스 정책 및 사전 통합된 MFA로 응용 프로그램을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-176">With Azure AD you can secure your applications with granular access policies and pre-integrated MFA.</span></span> <span data-ttu-id="c7747-177">Azure MFA에 대해 자세히 알아보려면 [Azure MFA](https://azure.microsoft.com/services/multi-factor-authentication/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c7747-177">To learn more about Azure MFA see [Azure MFA](https://azure.microsoft.com/services/multi-factor-authentication/).</span></span>

## <a name="getting-started"></a><span data-ttu-id="c7747-178">시작</span><span class="sxs-lookup"><span data-stu-id="c7747-178">Getting started</span></span>
<span data-ttu-id="c7747-179">응용 프로그램을 Azure AD와 통합하기 시작하려면 [응용 프로그램과 Azure Active Directory 통합 시작 가이드](active-directory-integrating-applications-getting-started.md)를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="c7747-179">To get started integrating applications with Azure AD, take a look at the [Integrating Azure Active Directory with applications getting started guide](active-directory-integrating-applications-getting-started.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="c7747-180">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c7747-180">See also</span></span>
[<span data-ttu-id="c7747-181">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="c7747-181">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

