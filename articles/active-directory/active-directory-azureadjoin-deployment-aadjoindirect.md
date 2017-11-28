---
title: "aaaUsage 시나리오 및 Azure AD Join에 대 한 배포 고려 사항 | Microsoft Docs"
description: "관리자가 최종 사용자(직원, 학생, 다른 사용자)를 위해 Azure AD 조인을 설정하는 방법을 설명합니다. 또한 Azure AD Join을 사용 하기 위한 hello 다른 실제 시나리오를 설명 합니다."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 81d4461e-21c8-4fdd-9076-0e4991979f62
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 7e57971481aa312ebf8a69999d194f9dcc3d4708
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="usage-scenarios-and-deployment-considerations-for-azure-ad-join"></a><span data-ttu-id="44809-104">Azure AD 연결에 대한 사용 시나리오와 배포 고려 사항</span><span class="sxs-lookup"><span data-stu-id="44809-104">Usage scenarios and deployment considerations for Azure AD Join</span></span>
## <a name="usage-scenarios-for-azure-ad-join"></a><span data-ttu-id="44809-105">Azure AD 연결에 대한 사용 시나리오</span><span class="sxs-lookup"><span data-stu-id="44809-105">Usage scenarios for Azure AD Join</span></span>
### <a name="scenario-1-businesses-largely-in-hello-cloud"></a><span data-ttu-id="44809-106">Hello 클라우드에서 대부분의 시나리오 1: 비즈니스</span><span class="sxs-lookup"><span data-stu-id="44809-106">Scenario 1: Businesses largely in hello cloud</span></span>
<span data-ttu-id="44809-107">Azure Active Directory Join (Azure AD Join) 장점 현재 작동 하 고 hello 클라우드에서 비즈니스에 대 한 id를 관리 하거나 toohello 클라우드 곧 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="44809-107">Azure Active Directory Join (Azure AD Join) can benefit you if you currently operate and manage identities for your business in hello cloud or are moving toohello cloud soon.</span></span> <span data-ttu-id="44809-108">사용자가 만든 tooWindows 10의에서 Azure AD toosign에서 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44809-108">You can use an account that you have created in Azure AD toosign in tooWindows 10.</span></span> <span data-ttu-id="44809-109">통해 [먼저 경험 (FRX) 프로세스를 실행 하는 hello](active-directory-azureadjoin-user-frx.md), 또는 Azure AD에서 조인 하 여 [hello 설정 메뉴](active-directory-azureadjoin-user-upgrade.md), 사용자가 자신의 컴퓨터 tooAzure AD에 조인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44809-109">Through [hello first run experience (FRX) process](active-directory-azureadjoin-user-frx.md), or by joining Azure AD from [hello settings menu](active-directory-azureadjoin-user-upgrade.md), your users can join their machines tooAzure AD.</span></span>  <span data-ttu-id="44809-110">사용자가 single sign on (SSO)도 즐길 수 너무 클라우드 Office 응용 프로그램 또는 브라우저에 Office 365와 같은 리소스를 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="44809-110">Your users can also enjoy single sign-on (SSO) access too cloud resources like Office 365, either in their browsers or in Office applications.</span></span>

### <a name="scenario-2-educational-institutions"></a><span data-ttu-id="44809-111">시나리오 2: 교육 기관</span><span class="sxs-lookup"><span data-stu-id="44809-111">Scenario 2: Educational institutions</span></span>
<span data-ttu-id="44809-112">교육 기관에는 일반적으로 두 가지 사용자 유형인 교직원 및 학생이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44809-112">Educational institutions usually have two user types: faculty and students.</span></span> <span data-ttu-id="44809-113">교사는 hello 조직의 장기적인 멤버로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="44809-113">Faculty members are considered longer-term members of hello organization.</span></span> <span data-ttu-id="44809-114">교직원에 대한 온-프레미스 계정을 만드는 것이 바람직합니다.</span><span class="sxs-lookup"><span data-stu-id="44809-114">Creating on-premises accounts for them is desirable.</span></span> <span data-ttu-id="44809-115">하지만 학생 shorter-term 팀원 들의 hello 되며 Azure AD에서 자신의 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44809-115">But students are shorter-term members of hello organization and  their accounts can be managed in Azure AD.</span></span> <span data-ttu-id="44809-116">즉, 온 프레미스 저장된 되지 않고 toohello 클라우드 디렉터리 눈금을 밀어넣을 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44809-116">This means that directory scale can be pushed toohello cloud instead of being stored on-premises.</span></span> <span data-ttu-id="44809-117">또한 학생 수에 Azure AD 계정와 tooWindows 수 toosign 되며 Office 응용 프로그램에서 액세스 tooOffice 365 리소스를 가져올 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="44809-117">It also means that students  will be able toosign in tooWindows with their Azure AD accounts and get access tooOffice 365 resources in Office applications.</span></span>

### <a name="scenario-3-retail-businesses"></a><span data-ttu-id="44809-118">시나리오 3: 소매 기업</span><span class="sxs-lookup"><span data-stu-id="44809-118">Scenario 3: Retail businesses</span></span>
<span data-ttu-id="44809-119">소매 기업에는 비정규직 근로자가 있고 장기 직원이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44809-119">Retail businesses have seasonal workers and long-term employees.</span></span> <span data-ttu-id="44809-120">일반적으로 장기적인 정규직 직원에 대해서는 온-프레미스 계정을 만든 후 도메인에 연결된 컴퓨터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="44809-120">You typically create on-premises accounts and use domain-joined machines for longer-term full-time employees.</span></span> <span data-ttu-id="44809-121">하지만 계절별 작업자는 hello 조직의 shorter-term 멤버 이므로 바람직한 toomanage 자신의 계정에 사용자 라이선스를 더 쉽게 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44809-121">But seasonal workers are shorter-term members of hello organization, and it's desirable toomanage their accounts where user licenses can be more easily moved around.</span></span> <span data-ttu-id="44809-122">Office 365 라이선스를 갖고 있는 hello 클라우드에서 자신의 사용자 계정을 만들 때 이러한 사용자가 hello 활용 남깁니다 후에 자신의 라이선스를 갖고 있는 더 많은 유연성을 유지 관리 하는 동안 tooWindows와 Azure AD 계정으로 Office 응용 프로그램에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="44809-122">When you create their user accounts in hello cloud with Office 365 licenses, these users get hello benefits of signing in tooWindows and Office applications with an Azure AD account, while you maintain more flexibility with their licenses after they leave.</span></span>

### <a name="scenario-4-additional-scenarios"></a><span data-ttu-id="44809-123">시나리오 4: 시나리오</span><span class="sxs-lookup"><span data-stu-id="44809-123">Scenario 4: Additional scenarios</span></span>
<span data-ttu-id="44809-124">사용자가 자신의 장치 tooAzure AD 단순화 조인 환경을, 효율적인 장치 관리, 자동 모바일 장치 관리 등록 및 single sign on tooAzure 때문에 조인 하는 것과 이점이 있습니다. 앞에서 설명한 hello 혜택을 함께 AD 및 온-프레미스 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="44809-124">Along with hello benefits discussed earlier, you  benefit from having your users join their devices tooAzure AD because of a simplified joining experience, efficient device management, automatic mobile device management enrollment, and single sign-on tooAzure AD and on-premises resources.</span></span>  

## <a name="deployment-considerations-for-azure-ad-join"></a><span data-ttu-id="44809-125">Azure AD 연결에 대한 배포 고려 사항</span><span class="sxs-lookup"><span data-stu-id="44809-125">Deployment considerations for Azure AD Join</span></span>
### <a name="enable-your-users-toojoin-a-company-owned-device-directly-tooazure-ad"></a><span data-ttu-id="44809-126">에 사용자가 toojoin 회사 소유 장치를 사용 하도록 설정 tooAzure AD 직접</span><span class="sxs-lookup"><span data-stu-id="44809-126">Enable your users toojoin a company-owned device directly tooAzure AD</span></span>
<span data-ttu-id="44809-127">클라우드 전용 계정 toopartner 회사와 조직에 기업에서는 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44809-127">Enterprises can provide cloud-only accounts toopartner companies and organizations.</span></span> <span data-ttu-id="44809-128">이러한 파트너는 Single Sign-On을 사용하여 회사 앱 및 리소스에 쉽게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44809-128">These partners can then easily access company apps and resources with single sign-on.</span></span> <span data-ttu-id="44809-129">이 시나리오는 주로 hello 클라우드 인증을 위해 Azure AD를 사용 하는 Office 365 또는 SaaS 앱 등의 리소스에 액세스 하는 적용 가능한 toousers입니다.</span><span class="sxs-lookup"><span data-stu-id="44809-129">This scenario is applicable toousers who access resources primarily in hello cloud, such as Office 365 or SaaS apps that rely on Azure AD for authentication.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="44809-130">필수 조건</span><span class="sxs-lookup"><span data-stu-id="44809-130">Prerequisites</span></span>
<span data-ttu-id="44809-131">**Hello 엔터프라이즈 수준 (관리자)**</span><span class="sxs-lookup"><span data-stu-id="44809-131">**At hello enterprise level (administrator)**</span></span>

* <span data-ttu-id="44809-132">Azure Active Directory를 사용하는 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="44809-132">Azure subscription with Azure Active Directory</span></span>  

<span data-ttu-id="44809-133">**Hello 사용자 수준**</span><span class="sxs-lookup"><span data-stu-id="44809-133">**At hello user level**</span></span>

* <span data-ttu-id="44809-134">Windows 10(Professional 및 Enterprise 버전)</span><span class="sxs-lookup"><span data-stu-id="44809-134">Windows 10 (Professional and Enterprise editions)</span></span>

### <a name="administrator-tasks"></a><span data-ttu-id="44809-135">관리자 작업</span><span class="sxs-lookup"><span data-stu-id="44809-135">Administrator tasks</span></span>
* [<span data-ttu-id="44809-136">장치 등록 설정</span><span class="sxs-lookup"><span data-stu-id="44809-136">Set up device registration</span></span>](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a><span data-ttu-id="44809-137">사용자 작업</span><span class="sxs-lookup"><span data-stu-id="44809-137">User tasks</span></span>
* [<span data-ttu-id="44809-138">설치하는 동안 Azure AD로 새 Windows 10 장치 설정</span><span class="sxs-lookup"><span data-stu-id="44809-138">Set up a new Windows 10 device with Azure AD during setup</span></span>](active-directory-azureadjoin-user-frx.md)
* [<span data-ttu-id="44809-139">Hello 설정 메뉴에서 Azure AD와 Windows 10 장치를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="44809-139">Set up a Windows 10 device with Azure AD from hello settings menu</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="44809-140">개인 Windows 10 장치 tooyour 조직 참가</span><span class="sxs-lookup"><span data-stu-id="44809-140">Join a personal Windows 10 device tooyour organization</span></span>](active-directory-azureadjoin-personal-device.md)

## <a name="enable-byod-in-your-organization-for-windows-10"></a><span data-ttu-id="44809-141">조직의 BYOD를 Windows 10에서 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="44809-141">Enable BYOD in your organization for Windows 10</span></span>
<span data-ttu-id="44809-142">사용자 및 직원 toouse 자신의 개인 Windows 장치 (BYOD) tooaccess 회사 앱 및 리소스 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44809-142">You can set up your users and employees toouse their personal Windows devices (BYOD) tooaccess company apps and resources.</span></span> <span data-ttu-id="44809-143">사용자가 안전 하 고 규격 방식 자신의 Azure AD 계정 (회사 또는 학교 계정) tooa 개인 Windows 장치 tooaccess 리소스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44809-143">Your users can add their Azure AD accounts (work or school accounts) tooa personal Windows device tooaccess resources in a secure and compliant fashion.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="44809-144">필수 조건</span><span class="sxs-lookup"><span data-stu-id="44809-144">Prerequisites</span></span>
<span data-ttu-id="44809-145">**Hello 엔터프라이즈 수준 (관리자)**</span><span class="sxs-lookup"><span data-stu-id="44809-145">**At hello enterprise level (administrator)**</span></span>

* <span data-ttu-id="44809-146">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="44809-146">Azure AD subscription</span></span>

<span data-ttu-id="44809-147">**Hello 사용자 수준**</span><span class="sxs-lookup"><span data-stu-id="44809-147">**At hello user level**</span></span>

* <span data-ttu-id="44809-148">Windows 10(Professional 및 Enterprise 버전)</span><span class="sxs-lookup"><span data-stu-id="44809-148">Windows 10 (Professional and Enterprise editions)</span></span>

### <a name="administrator-tasks"></a><span data-ttu-id="44809-149">관리자 작업</span><span class="sxs-lookup"><span data-stu-id="44809-149">Administrator tasks</span></span>
* [<span data-ttu-id="44809-150">장치 등록 설정</span><span class="sxs-lookup"><span data-stu-id="44809-150">Set up device registration</span></span>](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a><span data-ttu-id="44809-151">사용자 작업</span><span class="sxs-lookup"><span data-stu-id="44809-151">User tasks</span></span>
* [<span data-ttu-id="44809-152">개인 Windows 10 장치 tooyour 조직 참가</span><span class="sxs-lookup"><span data-stu-id="44809-152">Join a personal Windows 10 device tooyour organization</span></span>](active-directory-azureadjoin-personal-device.md)

## <a name="additional-information"></a><span data-ttu-id="44809-153">추가 정보</span><span class="sxs-lookup"><span data-stu-id="44809-153">Additional information</span></span>
* [<span data-ttu-id="44809-154">Hello 엔터프라이즈용 Windows 10: 작업에 대 한 방법으로 toouse 장치</span><span class="sxs-lookup"><span data-stu-id="44809-154">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="44809-155">Azure Active Directory Join을 통해 기능 10 tooWindows 장치 클라우드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="44809-155">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="44809-156">Microsoft Passport를 통해 암호 없이 ID 인증</span><span class="sxs-lookup"><span data-stu-id="44809-156">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="44809-157">Azure AD 조인에 대한 사용 시나리오에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="44809-157">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="44809-158">Windows 10 환경용에 대 한 AD 도메인에 가입 된 장치 tooAzure 연결</span><span class="sxs-lookup"><span data-stu-id="44809-158">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="44809-159">Azure AD 조인 설정</span><span class="sxs-lookup"><span data-stu-id="44809-159">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

