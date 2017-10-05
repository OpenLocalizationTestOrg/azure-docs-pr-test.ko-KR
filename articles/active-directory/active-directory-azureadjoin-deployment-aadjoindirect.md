---
title: "Azure AD 조인에 대한 사용 시나리오와 배포 고려 사항 | Microsoft Docs"
description: "관리자가 최종 사용자(직원, 학생, 다른 사용자)를 위해 Azure AD 조인을 설정하는 방법을 설명합니다. 또한 Azure AD 조인을 사용하는 데 대한 다양한 실제 시나리오에 대해서 설명합니다."
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
ms.openlocfilehash: fd0aab1a14bbd324e734e5efe8fe101e8a8dfefa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="usage-scenarios-and-deployment-considerations-for-azure-ad-join"></a><span data-ttu-id="4599d-104">Azure AD 연결에 대한 사용 시나리오와 배포 고려 사항</span><span class="sxs-lookup"><span data-stu-id="4599d-104">Usage scenarios and deployment considerations for Azure AD Join</span></span>
## <a name="usage-scenarios-for-azure-ad-join"></a><span data-ttu-id="4599d-105">Azure AD 연결에 대한 사용 시나리오</span><span class="sxs-lookup"><span data-stu-id="4599d-105">Usage scenarios for Azure AD Join</span></span>
### <a name="scenario-1-businesses-largely-in-the-cloud"></a><span data-ttu-id="4599d-106">시나리오 1: 클라우드에서 주로 업무 처리</span><span class="sxs-lookup"><span data-stu-id="4599d-106">Scenario 1: Businesses largely in the cloud</span></span>
<span data-ttu-id="4599d-107">Azure Active Directory 연결(Azure AD 연결)은 현재 클라우드에서 업무용 ID를 작동 및 관리하거나 곧 클라우드로 전환하려는 경우에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4599d-107">Azure Active Directory Join (Azure AD Join) can benefit you if you currently operate and manage identities for your business in the cloud or are moving to the cloud soon.</span></span> <span data-ttu-id="4599d-108">Azure AD에서 만든 계정을 사용하여 Windows 10에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4599d-108">You can use an account that you have created in Azure AD to sign in to Windows 10.</span></span> <span data-ttu-id="4599d-109">사용자는 [FRX(첫 실행 경험) 프로세스](active-directory-azureadjoin-user-frx.md)를 사용하거나 [설정 메뉴](active-directory-azureadjoin-user-upgrade.md)에서 Azure AD에 연결하여 Azure AD에 컴퓨터를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4599d-109">Through [the first run experience (FRX) process](active-directory-azureadjoin-user-frx.md), or by joining Azure AD from [the settings menu](active-directory-azureadjoin-user-upgrade.md), your users can join their machines to Azure AD.</span></span>  <span data-ttu-id="4599d-110">또한 사용자는 브라우저나 Office 응용 프로그램에서 SSO(Single-Sign-On)를 사용하여 Office 365와 같은 클라우드 리소스에 편리하게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4599d-110">Your users can also enjoy single sign-on (SSO) access to  cloud resources like Office 365, either in their browsers or in Office applications.</span></span>

### <a name="scenario-2-educational-institutions"></a><span data-ttu-id="4599d-111">시나리오 2: 교육 기관</span><span class="sxs-lookup"><span data-stu-id="4599d-111">Scenario 2: Educational institutions</span></span>
<span data-ttu-id="4599d-112">교육 기관에는 일반적으로 두 가지 사용자 유형인 교직원 및 학생이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4599d-112">Educational institutions usually have two user types: faculty and students.</span></span> <span data-ttu-id="4599d-113">교직원은 조직에서 장기 멤버로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="4599d-113">Faculty members are considered longer-term members of the organization.</span></span> <span data-ttu-id="4599d-114">교직원에 대한 온-프레미스 계정을 만드는 것이 바람직합니다.</span><span class="sxs-lookup"><span data-stu-id="4599d-114">Creating on-premises accounts for them is desirable.</span></span> <span data-ttu-id="4599d-115">하지만 학생은 조직의 단기 멤버이며 Azure AD에서 자신의 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4599d-115">But students are shorter-term members of the organization and  their accounts can be managed in Azure AD.</span></span> <span data-ttu-id="4599d-116">즉, 디렉터리 규모를 온-프레미스로 저장하는 대신 클라우드에 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4599d-116">This means that directory scale can be pushed to the cloud instead of being stored on-premises.</span></span> <span data-ttu-id="4599d-117">또한 학생들은 자신의 Azure AD 계정으로 Windows에 로그인하고 Office 응용 프로그램에서 Office 365 리소스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4599d-117">It also means that students  will be able to sign in to Windows with their Azure AD accounts and get access to Office 365 resources in Office applications.</span></span>

### <a name="scenario-3-retail-businesses"></a><span data-ttu-id="4599d-118">시나리오 3: 소매 기업</span><span class="sxs-lookup"><span data-stu-id="4599d-118">Scenario 3: Retail businesses</span></span>
<span data-ttu-id="4599d-119">소매 기업에는 비정규직 근로자가 있고 장기 직원이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4599d-119">Retail businesses have seasonal workers and long-term employees.</span></span> <span data-ttu-id="4599d-120">일반적으로 장기적인 정규직 직원에 대해서는 온-프레미스 계정을 만든 후 도메인에 연결된 컴퓨터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4599d-120">You typically create on-premises accounts and use domain-joined machines for longer-term full-time employees.</span></span> <span data-ttu-id="4599d-121">하지만 비정규직 근로자는 조직의 단기 멤버이므로 사용자 라이선스를 보다 쉽게 이동할 수 있도록 이들의 계정을 관리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4599d-121">But seasonal workers are shorter-term members of the organization, and it's desirable to manage their accounts where user licenses can be more easily moved around.</span></span> <span data-ttu-id="4599d-122">Office 365 라이선스를 사용하여 클라우드에 이러한 사용자의 계정을 만들면 이러한 사용자는 Azure AD 계정을 사용하여 Windows 및 Office 응용 프로그램에 로그인할 수 있으며 사용자가 조직을 떠난 후에 해당 라이선스의 이동을 보다 쉽게 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4599d-122">When you create their user accounts in the cloud with Office 365 licenses, these users get the benefits of signing in to Windows and Office applications with an Azure AD account, while you maintain more flexibility with their licenses after they leave.</span></span>

### <a name="scenario-4-additional-scenarios"></a><span data-ttu-id="4599d-123">시나리오 4: 시나리오</span><span class="sxs-lookup"><span data-stu-id="4599d-123">Scenario 4: Additional scenarios</span></span>
<span data-ttu-id="4599d-124">위에서 설명한 이점 외에도, 사용자의 장치를 Azure AD에 연결하여 간소화된 연결 환경, 효율적인 장치 관리, 자동 모바일 장치 관리 등록 및 Azure AD/온-프레미스 리소스에 대한 Single Sign-On 등에 따른 많은 이점을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4599d-124">Along with the benefits discussed earlier, you  benefit from having your users join their devices to Azure AD because of a simplified joining experience, efficient device management, automatic mobile device management enrollment, and single sign-on to Azure AD and on-premises resources.</span></span>  

## <a name="deployment-considerations-for-azure-ad-join"></a><span data-ttu-id="4599d-125">Azure AD 연결에 대한 배포 고려 사항</span><span class="sxs-lookup"><span data-stu-id="4599d-125">Deployment considerations for Azure AD Join</span></span>
### <a name="enable-your-users-to-join-a-company-owned-device-directly-to-azure-ad"></a><span data-ttu-id="4599d-126">사용자가 Azure AD에 직접 회사 소유의 장치를 연결하도록 허용</span><span class="sxs-lookup"><span data-stu-id="4599d-126">Enable your users to join a company-owned device directly to Azure AD</span></span>
<span data-ttu-id="4599d-127">기업에서는 파트너 회사 및 조직에 클라우드 전용 계정을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4599d-127">Enterprises can provide cloud-only accounts to partner companies and organizations.</span></span> <span data-ttu-id="4599d-128">이러한 파트너는 Single Sign-On을 사용하여 회사 앱 및 리소스에 쉽게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4599d-128">These partners can then easily access company apps and resources with single sign-on.</span></span> <span data-ttu-id="4599d-129">이 시나리오는 주로 인증을 위해 Azure AD에 의존하는 Office 365 또는 SaaS 앱과 같은 클라우드 리소스에 액세스하는 사용자에게 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="4599d-129">This scenario is applicable to users who access resources primarily in the cloud, such as Office 365 or SaaS apps that rely on Azure AD for authentication.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="4599d-130">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4599d-130">Prerequisites</span></span>
<span data-ttu-id="4599d-131">**엔터프라이즈 수준(관리자)**</span><span class="sxs-lookup"><span data-stu-id="4599d-131">**At the enterprise level (administrator)**</span></span>

* <span data-ttu-id="4599d-132">Azure Active Directory를 사용하는 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="4599d-132">Azure subscription with Azure Active Directory</span></span>  

<span data-ttu-id="4599d-133">**사용자 수준**</span><span class="sxs-lookup"><span data-stu-id="4599d-133">**At the user level**</span></span>

* <span data-ttu-id="4599d-134">Windows 10(Professional 및 Enterprise 버전)</span><span class="sxs-lookup"><span data-stu-id="4599d-134">Windows 10 (Professional and Enterprise editions)</span></span>

### <a name="administrator-tasks"></a><span data-ttu-id="4599d-135">관리자 작업</span><span class="sxs-lookup"><span data-stu-id="4599d-135">Administrator tasks</span></span>
* [<span data-ttu-id="4599d-136">장치 등록 설정</span><span class="sxs-lookup"><span data-stu-id="4599d-136">Set up device registration</span></span>](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a><span data-ttu-id="4599d-137">사용자 작업</span><span class="sxs-lookup"><span data-stu-id="4599d-137">User tasks</span></span>
* [<span data-ttu-id="4599d-138">설치하는 동안 Azure AD로 새 Windows 10 장치 설정</span><span class="sxs-lookup"><span data-stu-id="4599d-138">Set up a new Windows 10 device with Azure AD during setup</span></span>](active-directory-azureadjoin-user-frx.md)
* [<span data-ttu-id="4599d-139">설정 메뉴에서 Azure AD으로 Windows 10 장치 설정</span><span class="sxs-lookup"><span data-stu-id="4599d-139">Set up a Windows 10 device with Azure AD from the settings menu</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="4599d-140">개인 Windows 10 장치를 조직에 연결</span><span class="sxs-lookup"><span data-stu-id="4599d-140">Join a personal Windows 10 device to your organization</span></span>](active-directory-azureadjoin-personal-device.md)

## <a name="enable-byod-in-your-organization-for-windows-10"></a><span data-ttu-id="4599d-141">조직의 BYOD를 Windows 10에서 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="4599d-141">Enable BYOD in your organization for Windows 10</span></span>
<span data-ttu-id="4599d-142">사용자 및 직원이 개인 Windows 장치(BYOD)를 사용하여 회사 앱 및 리소스에 액세스하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4599d-142">You can set up your users and employees to use their personal Windows devices (BYOD) to access company apps and resources.</span></span> <span data-ttu-id="4599d-143">사용자는 안전하고 호환되는 방식으로  리소스에 액세스하기 위해 개인 Windows 장치에 자신의 Azure AD 계정(회사 또는 학교 계정)을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4599d-143">Your users can add their Azure AD accounts (work or school accounts) to a personal Windows device to access resources in a secure and compliant fashion.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="4599d-144">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4599d-144">Prerequisites</span></span>
<span data-ttu-id="4599d-145">**엔터프라이즈 수준(관리자)**</span><span class="sxs-lookup"><span data-stu-id="4599d-145">**At the enterprise level (administrator)**</span></span>

* <span data-ttu-id="4599d-146">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="4599d-146">Azure AD subscription</span></span>

<span data-ttu-id="4599d-147">**사용자 수준**</span><span class="sxs-lookup"><span data-stu-id="4599d-147">**At the user level**</span></span>

* <span data-ttu-id="4599d-148">Windows 10(Professional 및 Enterprise 버전)</span><span class="sxs-lookup"><span data-stu-id="4599d-148">Windows 10 (Professional and Enterprise editions)</span></span>

### <a name="administrator-tasks"></a><span data-ttu-id="4599d-149">관리자 작업</span><span class="sxs-lookup"><span data-stu-id="4599d-149">Administrator tasks</span></span>
* [<span data-ttu-id="4599d-150">장치 등록 설정</span><span class="sxs-lookup"><span data-stu-id="4599d-150">Set up device registration</span></span>](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a><span data-ttu-id="4599d-151">사용자 작업</span><span class="sxs-lookup"><span data-stu-id="4599d-151">User tasks</span></span>
* [<span data-ttu-id="4599d-152">개인 Windows 10 장치를 조직에 연결</span><span class="sxs-lookup"><span data-stu-id="4599d-152">Join a personal Windows 10 device to your organization</span></span>](active-directory-azureadjoin-personal-device.md)

## <a name="additional-information"></a><span data-ttu-id="4599d-153">추가 정보</span><span class="sxs-lookup"><span data-stu-id="4599d-153">Additional information</span></span>
* [<span data-ttu-id="4599d-154">엔터프라이즈를 위한 Windows 10: 작업에 장치를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="4599d-154">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="4599d-155">Azure Active Directory 조인을 통해 클라우드 기능을 Windows 10 장치로 확장</span><span class="sxs-lookup"><span data-stu-id="4599d-155">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="4599d-156">Microsoft Passport를 통해 암호 없이 ID 인증</span><span class="sxs-lookup"><span data-stu-id="4599d-156">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="4599d-157">Azure AD 조인에 대한 사용 시나리오에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="4599d-157">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="4599d-158">Windows 10 환경용 Azure AD에 도메인 가입된 장치 연결</span><span class="sxs-lookup"><span data-stu-id="4599d-158">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="4599d-159">Azure AD 조인 설정</span><span class="sxs-lookup"><span data-stu-id="4599d-159">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

