---
title: "Azure AD Connect: 통과 인증 - 미리 보기 인증 에이전트 업그레이드 | Microsoft Docs"
description: "이 문서에서는 Azure AD(Azure Active Directory) 통과 인증 구성을 업그레이드하는 방법에 대해 설명합니다."
services: active-directory
keywords: "Azure AD Connect 통과 인증, Active Directory 설치, Azure AD에 대한 필수 구성 요소, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 940cb4466ef5d730c42d04d0107f6901f55eb155
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-pass-through-authentication-upgrade-preview-authentication-agents"></a><span data-ttu-id="e6f0a-104">Azure Active Directory 통과 인증: 미리 보기 인증 에이전트 업그레이드</span><span class="sxs-lookup"><span data-stu-id="e6f0a-104">Azure Active Directory Pass-through Authentication: Upgrade preview Authentication Agents</span></span>

## <a name="overview"></a><span data-ttu-id="e6f0a-105">개요</span><span class="sxs-lookup"><span data-stu-id="e6f0a-105">Overview</span></span>

<span data-ttu-id="e6f0a-106">이 문서는 미리 보기를 통해 Azure AD 통과 인증을 사용하는 고객을 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-106">This article is for customers using Azure AD Pass-through Authentication through preview.</span></span> <span data-ttu-id="e6f0a-107">최근에 인증 에이전트 소프트웨어를 업그레이드(및 변경)했습니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-107">We recently upgraded (and rebranded) the Authentication Agent software.</span></span> <span data-ttu-id="e6f0a-108">온-프레미스 서버에 설치된 미리 보기 인증 에이전트를 _수동으로_ 업그레이드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-108">You need to _manually_ upgrade preview Authentication Agents installed on your on-premises servers.</span></span> <span data-ttu-id="e6f0a-109">이 수동 업그레이드는 일회성 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-109">This manual upgrade is a one-time action only.</span></span> <span data-ttu-id="e6f0a-110">인증 에이전트에 대한 모든 향후 업데이트는 자동입니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-110">All future updates to Authentication Agents are automatic.</span></span> <span data-ttu-id="e6f0a-111">업그레이드하는 이유는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-111">The reasons to upgrade are as follows:</span></span>

- <span data-ttu-id="e6f0a-112">인증 에이전트의 미리 보기 버전에는 추가 보안 또는 버그 수정이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-112">The preview versions of Authentication Agents will not receive any further security or bug fixes.</span></span>
-   <span data-ttu-id="e6f0a-113">고가용성을 위해 추가 서버에 인증 에이전트의 미리 보기 버전을 설치하는 것은 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-113">The preview versions of Authentication Agents can't be installed on additional servers, for high availability.</span></span>

## <a name="check-versions-of-your-authentication-agents"></a><span data-ttu-id="e6f0a-114">인증 에이전트의 버전 확인</span><span class="sxs-lookup"><span data-stu-id="e6f0a-114">Check versions of your Authentication Agents</span></span>

### <a name="step-1-check-where-your-authentication-agents-are-installed"></a><span data-ttu-id="e6f0a-115">1단계: 인증 에이전트가 설치된 위치 확인</span><span class="sxs-lookup"><span data-stu-id="e6f0a-115">Step 1: Check where your Authentication Agents are installed</span></span>

<span data-ttu-id="e6f0a-116">다음 단계에 따라 인증 에이전트가 설치된 위치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-116">Follow these steps to check where your Authentication Agents are installed:</span></span>

1. <span data-ttu-id="e6f0a-117">테넌트에 대한 전역 관리자 자격 증명을 사용하여 [Azure Active Directory 관리 센터](https://aad.portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-117">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with the Global Administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="e6f0a-118">왼쪽 탐색에서 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-118">Select **Azure Active Directory** on the left-hand navigation.</span></span>
3. <span data-ttu-id="e6f0a-119">**Azure AD Connect**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-119">Select **Azure AD Connect**.</span></span> 
4. <span data-ttu-id="e6f0a-120">**통과 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-120">Select **Pass-through Authentication**.</span></span> <span data-ttu-id="e6f0a-121">이 블레이드는 인증 에이전트가 설치된 서버를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-121">This blade lists the servers where your Authentication Agents are installed.</span></span>

![Azure Active Directory 관리 센터 - 통과 인증 블레이드](./media/active-directory-aadconnect-pass-through-authentication/pta8.png)

### <a name="step-2-check-the-versions-of-your-authentication-agents"></a><span data-ttu-id="e6f0a-123">2단계: 인증 에이전트의 버전 확인</span><span class="sxs-lookup"><span data-stu-id="e6f0a-123">Step 2: Check the versions of your Authentication Agents</span></span>

<span data-ttu-id="e6f0a-124">이전 단계에서 식별된 각 서버에서 사용자의 인증 에이전트 버전을 확인하려면 다음 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-124">To check the versions of your Authentication Agents, on each server identified in the preceding step, follow these instructions:</span></span>

1. <span data-ttu-id="e6f0a-125">온-프레미스 서버에서 **제어판 -> 프로그램 -> 프로그램 및 기능**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-125">Go to **Control Panel -> Programs -> Programs and Features** on the on-premises server.</span></span>
2. <span data-ttu-id="e6f0a-126">“**Microsoft Azure AD Connect 인증 에이전트**”에 대한 항목이 있는 경우 이 서버에 대해 어떤 조치도 취할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-126">If there is an entry for "**Microsoft Azure AD Connect Authentication Agent**", you don't need to take any action on this server.</span></span>
3. <span data-ttu-id="e6f0a-127">“**Microsoft Azure AD 응용 프로그램 프록시 커넥터**” 버전 1.5.132.0 이하에 대한 항목이 있는 경우 서버를 수동으로 업그레이드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-127">If there is an entry for "**Microsoft Azure AD Application Proxy Connector**", versions 1.5.132.0 or earlier, you need to manually upgrade on this server.</span></span>

![인증 에이전트의 미리 보기 버전](./media/active-directory-aadconnect-pass-through-authentication/pta6.png)

## <a name="best-practices-to-follow-before-starting-the-upgrade"></a><span data-ttu-id="e6f0a-129">업그레이드를 시작하기 전에 참고할 모범 사례</span><span class="sxs-lookup"><span data-stu-id="e6f0a-129">Best practices to follow before starting the upgrade</span></span>

<span data-ttu-id="e6f0a-130">업그레이드하기 전에 다음 항목이 준비되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-130">Before upgrading, ensure that you have the following items in place:</span></span>

1. <span data-ttu-id="e6f0a-131">**클라우드 전용 전역 관리자 계정 만들기**: 통과 인증 에이전트가 제대로 작동하지 않는 비상 상황에서는 사용할 클라우드 전용 전역 관리자 계정이 없다면 업그레이드하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-131">**Create cloud-only Global Administrator account**: Don’t upgrade without having a cloud-only Global Administrator account to use in emergency situations where your Pass-through Authentication Agents are not working properly.</span></span> <span data-ttu-id="e6f0a-132">[클라우드 전용 전역 관리자 계정 추가](../active-directory-users-create-azure-portal.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-132">Learn about [adding a cloud-only Global Administrator account](../active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="e6f0a-133">이 단계를 수행하는 것이 중요하며 테넌트가 잠기지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-133">Doing this step is critical and ensures that you don't get locked out of your tenant.</span></span>
2.  <span data-ttu-id="e6f0a-134">**고가용성 보장**: 이전에 완료되지 않은 경우, 로그인 요청에 대해 고가용성을 제공하기 위해 [지침](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability)에 따라 두 번째 독립 실행형 인증 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-134">**Ensure high availability**: If not completed previously, install a second standalone Authentication Agent to provide high availability for sign-in requests, using these [instructions](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability).</span></span>

## <a name="upgrading-the-authentication-agent-on-your-azure-ad-connect-server"></a><span data-ttu-id="e6f0a-135">Azure AD Connect 서버에서 인증 에이전트 업그레이드</span><span class="sxs-lookup"><span data-stu-id="e6f0a-135">Upgrading the Authentication Agent on your Azure AD Connect server</span></span>

<span data-ttu-id="e6f0a-136">동일한 서버에 인증 에이전트를 업그레이드하기 전에 Azure AD Connect를 업그레이드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-136">You need upgrade Azure AD Connect before upgrading the Authentication Agent on the same server.</span></span> <span data-ttu-id="e6f0a-137">주 및 스테이징 Azure AD Connect 서버 모두에서 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-137">Follow these steps on both your primary and staging Azure AD Connect servers:</span></span>

1. <span data-ttu-id="e6f0a-138">**Azure AD Connect 업그레이드**: 이 [문서](./active-directory-aadconnect-upgrade-previous-version.md)에 따라 최신 Azure AD Connect 버전으로 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-138">**Upgrade Azure AD Connect**: Follow this [article](./active-directory-aadconnect-upgrade-previous-version.md) and upgrade to the latest Azure AD Connect version.</span></span>
2. <span data-ttu-id="e6f0a-139">**인증 에이전트의 미리 보기 버전 제거**: [이 PowerShell 스크립트](https://aka.ms/rmpreviewagent)를 다운로드하여 서버에서 관리자 권한으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-139">**Uninstall the preview version of the Authentication Agent**: Download [this PowerShell script](https://aka.ms/rmpreviewagent) and run it as an Administrator on the server.</span></span>
3. <span data-ttu-id="e6f0a-140">**인증 에이전트의 최신 버전(버전 1.5.193.0 이상) 다운로드**: 테넌트의 전역 관리자 자격 증명을 사용하여 [Azure Active Directory 관리 센터](https://aad.portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-140">**Download the latest version of the Authentication Agent (versions 1.5.193.0 or later)**: Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with your tenant's Global Administrator credentials.</span></span> <span data-ttu-id="e6f0a-141">**Azure Active Directory -> Azure AD Connect -> 통과 인증 -> 에이전트 다운로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-141">Select **Azure Active Directory -> Azure AD Connect -> Pass-through Authentication -> Download agent**.</span></span> <span data-ttu-id="e6f0a-142">서비스 약관에 동의하고 인증 에이전트의 최신 버전을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-142">Accept the terms of service and download the latest version of the Authentication Agent.</span></span>
4. <span data-ttu-id="e6f0a-143">**인증 에이전트의 최신 버전 설치**: 3단계에서 다운로드한 실행 파일을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-143">**Install the latest version of the Authentication Agent**: Run the executable downloaded in Step 3.</span></span> <span data-ttu-id="e6f0a-144">메시지가 표시되면 테넌트의 전역 관리자 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-144">Provide your tenant's Global Administrator credentials when prompted.</span></span>
5. <span data-ttu-id="e6f0a-145">**최신 버전이 설치되었는지 확인**: 이전에 설명한 것처럼 **제어판 -> 프로그램 -> 프로그램 및 기능**으로 이동하여 “**Microsoft Azure AD Connect 인증 에이전트**”에 대한 항목이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-145">**Verify that the latest version has been installed**: As shown before, go to **Control Panel -> Programs -> Programs and Features** and verify that there is an entry for "**Microsoft Azure AD Connect Authentication Agent**".</span></span>

>[!NOTE]
><span data-ttu-id="e6f0a-146">위의 단계를 완료한 후 [Azure Active Directory 관리 센터](https://aad.portal.azure.com)에서 통과 인증 블레이드를 확인하는 경우 서버당 두 개의 인증 에이전트 항목이 표시됩니다. 하나의 항목은 **활성**으로 인증 에이전트를 보여 주고, 다른 하나는 **비활성**으로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-146">If you check the Pass-through Authentication blade on the [Azure Active Directory admin center](https://aad.portal.azure.com) after  completing the preceding steps, you'll see two Authentication Agent entries per server - one entry showing the Authentication Agent as **Active** and the other as **Inactive**.</span></span> <span data-ttu-id="e6f0a-147">_예상된_ 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-147">This is _expected_.</span></span> <span data-ttu-id="e6f0a-148">**비활성** 항목은 몇 일 후 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-148">The **Inactive** entry is automatically dropped after a few days.</span></span>

## <a name="upgrading-the-authentication-agent-on-other-servers"></a><span data-ttu-id="e6f0a-149">다른 서버에서 인증 에이전트 업그레이드</span><span class="sxs-lookup"><span data-stu-id="e6f0a-149">Upgrading the Authentication Agent on other servers</span></span>

<span data-ttu-id="e6f0a-150">다음 단계에 따라 다른 서버에서 인증 에이전트를 업그레이드합니다(여기서는 Azure AD Connect가 설치되지 않음).</span><span class="sxs-lookup"><span data-stu-id="e6f0a-150">Follow these steps to upgrade Authentication Agents on other servers (where Azure AD Connect is not installed):</span></span>

1. <span data-ttu-id="e6f0a-151">**인증 에이전트의 미리 보기 버전 제거**: [이 PowerShell 스크립트](https://aka.ms/rmpreviewagent)를 다운로드하여 서버에서 관리자 권한으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-151">**Uninstall the preview version of the Authentication Agent**: Download [this PowerShell script](https://aka.ms/rmpreviewagent) and run it as an Administrator on the server.</span></span>
2. <span data-ttu-id="e6f0a-152">**인증 에이전트의 최신 버전(버전 1.5.193.0 이상) 다운로드**: 테넌트의 전역 관리자 자격 증명을 사용하여 [Azure Active Directory 관리 센터](https://aad.portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-152">**Download the latest version of the Authentication Agent (versions 1.5.193.0 or later)**: Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with your tenant's Global Administrator credentials.</span></span> <span data-ttu-id="e6f0a-153">**Azure Active Directory -> Azure AD Connect -> 통과 인증 -> 에이전트 다운로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-153">Select **Azure Active Directory -> Azure AD Connect -> Pass-through Authentication -> Download agent**.</span></span> <span data-ttu-id="e6f0a-154">서비스 약관에 동의하고 최신 버전을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-154">Accept the terms of service and download the latest version.</span></span>
3. <span data-ttu-id="e6f0a-155">**인증 에이전트의 최신 버전 설치**: 2단계에서 다운로드한 실행 파일을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-155">**Install the latest version of the Authentication Agent**: Run the executable downloaded in Step 2.</span></span> <span data-ttu-id="e6f0a-156">메시지가 표시되면 테넌트의 전역 관리자 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-156">Provide your tenant's Global Administrator credentials when prompted.</span></span>
4. <span data-ttu-id="e6f0a-157">**최신 버전이 설치되었는지 확인**: 이전에 설명한 것처럼 **제어판 -> 프로그램 -> 프로그램 및 기능**으로 이동하여 **Microsoft Azure AD Connect 인증 에이전트**라는 항목이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-157">**Verify that the latest version has been installed**: As shown before, go to **Control Panel -> Programs -> Programs and Features** and verify that there is an entry called **Microsoft Azure AD Connect Authentication Agent**.</span></span>

>[!NOTE]
><span data-ttu-id="e6f0a-158">위의 단계를 완료한 후 [Azure Active Directory 관리 센터](https://aad.portal.azure.com)에서 통과 인증 블레이드를 확인하는 경우 서버당 두 개의 인증 에이전트 항목이 표시됩니다. 하나의 항목은 **활성**으로 인증 에이전트를 보여 주고, 다른 하나는 **비활성**으로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-158">If you check the Pass-through Authentication blade on the [Azure Active Directory admin center](https://aad.portal.azure.com) after  completing the preceding steps, you'll see two Authentication Agent entries per server - one entry showing the Authentication Agent as **Active** and the other as **Inactive**.</span></span> <span data-ttu-id="e6f0a-159">_예상된_ 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-159">This is _expected_.</span></span> <span data-ttu-id="e6f0a-160">**비활성** 항목은 몇 일 후 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-160">The **Inactive** entry is automatically dropped after a few days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6f0a-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e6f0a-161">Next steps</span></span>
- <span data-ttu-id="e6f0a-162">[**문제 해결**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - 기능과 관련된 일반적인 문제를 해결하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e6f0a-162">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how to resolve common issues with the feature.</span></span>
