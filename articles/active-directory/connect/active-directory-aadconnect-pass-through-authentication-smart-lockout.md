---
title: "Azure AD Connect: 통과 인증 - 스마트 잠금 | Microsoft Docs"
description: "이 문서에서는 Azure AD(Active Directory) 통과 인증이 클라우드에서의 무차별 암호 대입 공격으로부터 온-프레미스 계정을 보호하는 방법에 대해 설명합니다."
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
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: c84b2406e6373701c83c509342129bd6d7d4034b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a><span data-ttu-id="0f469-104">Azure Active Directory 통과 인증: 스마트 잠금</span><span class="sxs-lookup"><span data-stu-id="0f469-104">Azure Active Directory Pass-through Authentication: Smart Lockout</span></span>

## <a name="overview"></a><span data-ttu-id="0f469-105">개요</span><span class="sxs-lookup"><span data-stu-id="0f469-105">Overview</span></span>

<span data-ttu-id="0f469-106">Azure AD는 무차별 암호 대입 공격으로부터 보호하고 실제 사용자가 Office 365 및 SaaS 응용 프로그램에서 잠기지 않게 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-106">Azure AD protects against brute force password attacks and prevents genuine users from being locked out of their Office 365 and SaaS applications.</span></span> <span data-ttu-id="0f469-107">이 기능을 **스마트 잠금**이라고 하며 로그인 방법으로 통과 인증을 사용할 때 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-107">This capability, called **Smart Lockout**, is supported when you use Pass-through Authentication as your sign-in method.</span></span> <span data-ttu-id="0f469-108">스마트 잠금은 기본적으로 모든 테넌트에 대해 사용하며 항상 사용자 계정을 보호하므로 사용자가 실행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-108">Smart Lockout is enabled by default for all tenants and are protecting your user accounts all the time; there is no need to turn it on.</span></span>

<span data-ttu-id="0f469-109">스마트 잠금은 실패한 모든 로그인 시도를 추적하며 특정 **잠금 임계값** 이후 **잠금 기간**을 시작하는 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-109">Smart Lockout works by keeping track of failed sign-in attempts, and after a certain **Lockout Threshold**, starting a **Lockout Duration**.</span></span> <span data-ttu-id="0f469-110">잠금 기간 동안 공격자의 모든 로그인 시도가 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-110">Any sign-in attempts from the attacker during the Lockout Duration are rejected.</span></span> <span data-ttu-id="0f469-111">공격이 지속될 경우 잠근 기간이 종료된 후에 실패한 로그인 시도로 인해 잠금 기간이 더 길어집니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-111">If the attack continues, the subsequent failed sign-in attempts after the Lockout Duration ends result in longer Lockout Durations.</span></span>

>[!NOTE]
><span data-ttu-id="0f469-112">기본 잠금 임계값은 10회 실패이며 기본 잠금 기간은 60초입니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-112">The default Lockout Threshold is 10 failed attempts, and the default Lockout Duration is 60 seconds.</span></span>

<span data-ttu-id="0f469-113">스마트 잠금은 실제 사용자의 로그인과 공격자의 로그인을 구분하며 대부분의 경우 공격자만 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-113">Smart Lockout also distinguishes between sign-ins from genuine users and from attackers and only locks out the attackers in most cases.</span></span> <span data-ttu-id="0f469-114">이 기능은 공격자가 악의적으로 실제 사용자를 잠그지 못하게 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-114">This functionality prevents attackers from maliciously locking out genuine users.</span></span> <span data-ttu-id="0f469-115">과거 로그인 행위, 사용자 장치 및 브라우저, 기타 신호를 사용하여 실제 사용자와 공격자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-115">We use past sign-in behavior, users’ devices & browsers and other signals to distinguish between genuine users and attackers.</span></span> <span data-ttu-id="0f469-116">이 알고리즘은 지속적으로 개선 중입니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-116">We are constantly improving our algorithms.</span></span>

<span data-ttu-id="0f469-117">통과 인증은 암호 유효성 검사 요청을 온-프레미스 AD(Active Directory)로 전달하므로 공격자가 사용자의 AD 계정을 잠그지 못하게 차단해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-117">Because Pass-through Authentication forwards password validation requests onto your on-premises Active Directory (AD), you need to prevent attackers from locking out your users’ AD accounts.</span></span> <span data-ttu-id="0f469-118">자체 AD 계정 잠금 정책([**계정 잠금 임계값**](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) 및 [**일정 시간 이후 계정 잠금 재설정 카운터 정책**](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx))이 있으므로 Azure AD의 잠금 임계값과 잠금 기간 값을 적합하게 구성하여 공격자가 온-프레미스 AD에 도달하기 전에 클라우드의 공격을 필터링해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-118">Since you have your own AD Account Lockout policies (specifically, [**Account Lockout Threshold**](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) and [**Reset Account Lockout Counter After policies**](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), you need to configure Azure AD’s Lockout Threshold and Lockout Duration values appropriately to filter out attacks in the cloud before they reach your on-premises AD.</span></span>

>[!NOTE]
><span data-ttu-id="0f469-119">스마트 잠금 기능은 추가 비용 없이 제공되며, 기본적으로 _모든 고객이 사용_할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-119">The Smart Lockout feature is free and is _on_ by default for all customers.</span></span> <span data-ttu-id="0f469-120">그러나 Graph API를 사용하여 Azure AD의 잠금 임계값 및 잠금 기간을 수정하기 위해 테넌트에 Azure AD Premium P2 라이선스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-120">However, modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API needs your tenant to have at least one Azure AD Premium P2 license.</span></span> <span data-ttu-id="0f469-121">통과 인증을 사용하여 스마트 잠금 기능을 얻기 위해 _사용자당_ Azure AD Premium P2 라이선스가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-121">You don't need an Azure AD Premium P2 license _per user_ to get the Smart Lockout feature with Pass-through Authentication.</span></span>

<span data-ttu-id="0f469-122">사용자의 온-프레미스 AD 계정을 제대로 보호하기 위해 다음을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-122">To ensure that your users’ on-premises AD accounts are well protected, you need to ensure that:</span></span>

1.  <span data-ttu-id="0f469-123">Azure AD의 잠금 임계값은 AD의 계정 잠금 임계값보다 _작아야_ 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-123">Azure AD’s Lockout Threshold is _less_ than AD’s Account Lockout Threshold.</span></span> <span data-ttu-id="0f469-124">AD의 계정 잠금 임계값은 Azure AD의 잠금 임계값보다 2-3배 이상은 크게 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-124">We recommend that you set the values such that AD’s Account Lockout Threshold is at least two or three times Azure AD’s Lockout Threshold.</span></span>
2.  <span data-ttu-id="0f469-125">Azure AD의 잠금 기간(초 단위)이 AD의 다음 시간 이후 계정 잠금 재설정(분 단위)보다 _길어야_ 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-125">Azure AD’s Lockout Duration (represented in seconds) is _longer_ than AD’s Reset Account Lockout Counter After (represented in minutes).</span></span>

## <a name="verify-your-ad-account-lockout-policies"></a><span data-ttu-id="0f469-126">AD 계정 잠금 정책 확인</span><span class="sxs-lookup"><span data-stu-id="0f469-126">Verify your AD Account Lockout policies</span></span>

<span data-ttu-id="0f469-127">다음 지침을 사용하여 AD 계정 잠금 정책을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-127">Use the following instructions to verify your AD Account Lockout policies:</span></span>

1.  <span data-ttu-id="0f469-128">그룹 정책 관리 도구를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-128">Open the Group Policy Management tool.</span></span>
2.  <span data-ttu-id="0f469-129">모든 사용자에게 적용된 그룹 정책(예: 기본 도메인 정책)을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-129">Edit the group policy that is applied to all users, for example, the Default Domain Policy.</span></span>
3.  <span data-ttu-id="0f469-130">Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Account Lockout Policy로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-130">Navigate to Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Account Lockout Policy.</span></span>
4.  <span data-ttu-id="0f469-131">계정 잠금 임계값 및 다음 이후 계정 잠금 카운터 재설정 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-131">Verify your Account Lockout Threshold and Reset Account Lockout Counter After values.</span></span>

![AD 계정 잠금 정책](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-the-graph-api-to-manage-your-tenants-smart-lockout-values"></a><span data-ttu-id="0f469-133">Graph API를 사용하여 테넌트의 스마트 잠금 값 관리</span><span class="sxs-lookup"><span data-stu-id="0f469-133">Use the Graph API to manage your tenant’s Smart Lockout values</span></span>

>[!IMPORTANT]
><span data-ttu-id="0f469-134">그래픽 API를 사용하여 Azure AD의 잠금 임계값 및 잠금 기간을 수정하는 것은 Azure AD Premium P2 기능입니다. </span><span class="sxs-lookup"><span data-stu-id="0f469-134">Modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API is an Azure AD Premium P2 feature.</span></span> <span data-ttu-id="0f469-135">또한 사용자가 테넌트에서 전역 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-135">It also needs you to be a Global Administrator on your tenant.</span></span>

<span data-ttu-id="0f469-136">[Graph 탐색기](https://developer.microsoft.com/graph/graph-explorer)를 사용하여 Azure AD의 스마트 잠금 값을 읽고, 설정하고, 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-136">You can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) to read, set, and update Azure AD’s Smart Lockout values.</span></span> <span data-ttu-id="0f469-137">하지만 이러한 작업을 프로그래밍 방식으로 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-137">But you can also do these operations programmatically.</span></span>

### <a name="read-smart-lockout-values"></a><span data-ttu-id="0f469-138">스마트 잠금 값 읽기</span><span class="sxs-lookup"><span data-stu-id="0f469-138">Read Smart Lockout values</span></span>

<span data-ttu-id="0f469-139">다음 단계에 따라 테넌트의 스마트 잠금 값을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-139">Follow these steps to read your tenant’s Smart Lockout values:</span></span>

1. <span data-ttu-id="0f469-140">Graph 탐색기에 테넌트의 전역 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-140">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="0f469-141">메시지가 표시되면 요청된 권한에 대해 액세스를 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-141">If prompted, grant access for the requested permissions.</span></span>
2. <span data-ttu-id="0f469-142">"권한 수정"을 클릭하고 "Directory.ReadWrite.All" 권한을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-142">Click “Modify permissions” and select the “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="0f469-143">Graph API 요청을 다음과 같이 구성합니다. 버전을 "BETA"로, 요청 유형을 "GET"으로, URL을 `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-143">Configure the Graph API request as follows: Set version to “BETA”, request type to “GET” and URL to `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="0f469-144">"쿼리 실행"을 클릭하여 테넌트의 스마트 잠금 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-144">Click "Run Query" to see your tenant's Smart Lockout values.</span></span> <span data-ttu-id="0f469-145">앞서 테넌트의 값을 설정하지 않은 경우 빈 집합이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-145">If you haven't set your tenant's values before, you see an empty set.</span></span>

### <a name="set-smart-lockout-values"></a><span data-ttu-id="0f469-146">스마트 잠금 값 설정</span><span class="sxs-lookup"><span data-stu-id="0f469-146">Set Smart Lockout values</span></span>

<span data-ttu-id="0f469-147">다음 단계에 따라 테넌트의 스마트 잠금 값을 설정합니다(최초에만).</span><span class="sxs-lookup"><span data-stu-id="0f469-147">Follow these steps to set your tenant’s Smart Lockout values (for the first time only):</span></span>

1. <span data-ttu-id="0f469-148">Graph 탐색기에 테넌트의 전역 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-148">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="0f469-149">메시지가 표시되면 요청된 권한에 대해 액세스를 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-149">If prompted, grant access for the requested permissions.</span></span>
2. <span data-ttu-id="0f469-150">"권한 수정"을 클릭하고 "Directory.ReadWrite.All" 권한을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-150">Click “Modify permissions” and select the “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="0f469-151">Graph API 요청을 다음과 같이 구성합니다. 버전을 "BETA"로, 요청 유형을 "POST"로, URL을 `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-151">Configure the Graph API request as follows: Set version to “BETA”, request type to “POST” and URL to `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="0f469-152">다음 JSON 요청을 복사하여 "요청 본문" 필드에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-152">Copy and paste the following JSON request into the "Request Body" field.</span></span> <span data-ttu-id="0f469-153">스마트 잠금 값을 적절하게 변경하고 `templateId`에 대해 임의의 GUID를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-153">Change the Smart Lockout values as appropriate and use a random GUID for `templateId`.</span></span>
5. <span data-ttu-id="0f469-154">"쿼리 실행"을 클릭하여 테넌트의 스마트 잠금 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-154">Click "Run Query" to set your tenant's Smart Lockout values.</span></span>

```
{
  "templateId": "5cf42378-d67d-4f36-ba46-e8b86229381d",
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "300"
    },
    {
      "name": "LockoutThreshold",
      "value": "5"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

>[!NOTE]
><span data-ttu-id="0f469-155">이들을 사용하지 않는 경우 **BannedPasswordList** 및**EnableBannedPasswordCheck** 값이 각각 공백("") 및 "false"가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-155">If you are not using them, you can leave the **BannedPasswordList** and **EnableBannedPasswordCheck** values as empty ("") and "false" respectively.</span></span>

<span data-ttu-id="0f469-156">[이 단계](#read-smart-lockout-values)를 사용하여 테넌트의 스마트 잠금 값을 올바르게 설정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-156">Verify that you have set your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

### <a name="update-smart-lockout-values"></a><span data-ttu-id="0f469-157">스마트 잠금 값 업데이트</span><span class="sxs-lookup"><span data-stu-id="0f469-157">Update Smart Lockout values</span></span>

<span data-ttu-id="0f469-158">이 단계에 따라 테넌트의 스마트 잠금 값을 업데이트합니다(앞서 설정한 경우).</span><span class="sxs-lookup"><span data-stu-id="0f469-158">Follow these steps to update your tenant’s Smart Lockout values (if you have already set them before):</span></span>

1. <span data-ttu-id="0f469-159">Graph 탐색기에 테넌트의 전역 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-159">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="0f469-160">메시지가 표시되면 요청된 권한에 대해 액세스를 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-160">If prompted, grant access for the requested permissions.</span></span>
2. <span data-ttu-id="0f469-161">"권한 수정"을 클릭하고 "Directory.ReadWrite.All" 권한을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-161">Click “Modify permissions” and select the “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="0f469-162">[다음 단계에 따라 테넌트의 스마트 잠금 값을 읽습니다](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="0f469-162">[Follow these steps to read your tenant's Smart Lockout values](#read-smart-lockout-values).</span></span> <span data-ttu-id="0f469-163">"displayName"이 "PasswordRuleSettings"인 항목의 `id` 값(GUID)을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-163">Copy the `id` value (a GUID) of the item with "displayName" as "PasswordRuleSettings".</span></span>
4. <span data-ttu-id="0f469-164">Graph API 요청을 다음과 같이 구성합니다. 버전을 "BETA"로, 요청 유형을 "PATCH"로, URL을 `https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>`로 설정합니다. `<id>`에는 3단계의 GUID를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-164">Configure the Graph API request as follows: Set version to “BETA”, request type to “PATCH” and URL to `https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` - use the GUID from Step 3 for `<id>`.</span></span>
5. <span data-ttu-id="0f469-165">다음 JSON 요청을 복사하여 "요청 본문" 필드에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-165">Copy and paste the following JSON request into the "Request Body" field.</span></span> <span data-ttu-id="0f469-166">스마트 잠금 값을 적절하게 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-166">Change the Smart Lockout values as appropriate.</span></span>
6. <span data-ttu-id="0f469-167">"쿼리 실행"을 클릭하여 테넌트의 스마트 잠금 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-167">Click "Run Query" to update your tenant's Smart Lockout values.</span></span>

```
{
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "30"
    },
    {
      "name": "LockoutThreshold",
      "value": "4"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

<span data-ttu-id="0f469-168">[이 단계](#read-smart-lockout-values)를 사용하여 테넌트의 스마트 잠금 값을 올바르게 업데이트했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-168">Verify that you have updated your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f469-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0f469-169">Next steps</span></span>
- <span data-ttu-id="0f469-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 새로운 기능 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="0f469-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
