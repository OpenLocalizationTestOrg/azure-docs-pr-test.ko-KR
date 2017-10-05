---
title: 'Azure Active Directory B2C: Multi-Factor Authentication | Microsoft Docs'
description: "Azure Active Directory B2C에서 보호하는 소비자 지향 응용 프로그램에서 Multi-Factor Authentication을 사용하는 방법"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 53ef86c4-1586-45dc-9952-dbbd62f68afc
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 62ec48ab067cf02bc8409aca6da704a5418ec270
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-enable-multi-factor-authentication-in-your-consumer-facing-applications"></a><span data-ttu-id="6135d-103">Azure Active Directory B2C: 소비자 지향 응용 프로그램에서 Multi-Factor Authentication 사용</span><span class="sxs-lookup"><span data-stu-id="6135d-103">Azure Active Directory B2C: Enable Multi-Factor Authentication in your consumer-facing applications</span></span>
<span data-ttu-id="6135d-104">Azure Active Directory(Azure AD) B2C는 [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) 에 직접 통합하여 소비자 지향 응용 프로그램에서 등록 및 로그인하는 데 두 번째 보안 계층을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-104">Azure Active Directory (Azure AD) B2C integrates directly with [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) so that you can add a second layer of security to sign-up and sign-in experiences in your consumer-facing applications.</span></span> <span data-ttu-id="6135d-105">이 작업을 한 줄의 코드도 작성하지 않고 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-105">And you can do this without writing a single line of code.</span></span> <span data-ttu-id="6135d-106">현재 전화 통화 및 문자 메시지를 확인을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-106">Currently we support phone call and text message verification.</span></span> <span data-ttu-id="6135d-107">이미 등록 및 로그인 정책을 만든 경우에도 다단계 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-107">If you already created sign-up and sign-in policies, you can still enable Multi-Factor Authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="6135d-108">단지 기존 정책을 편집하지 않고 등록 및 로그인 정책을 만들 때 다단계 인증을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-108">Multi-Factor Authentication can also be enabled when you create sign-up and sign-in policies, not just by editing existing policies.</span></span>
> 
> 

<span data-ttu-id="6135d-109">이 기능은 응용 프로그램에서 다음과 같은 시나리오를 처리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-109">This feature helps applications handle scenarios such as the following:</span></span>

* <span data-ttu-id="6135d-110">하나의 응용 프로그램에 액세스하려는 경우 다단계 인증이 필요하지 않지만 다른 응용 프로그램에 액세스하려면 다단계 인증이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-110">You don't require Multi-Factor Authentication to access one application, but you do require it to access another one.</span></span> <span data-ttu-id="6135d-111">예를 들어 소비자는 소셜 또는 로컬 계정을 사용하여 자동차 보험 응용 프로그램에 로그인할 수 있지만 동일한 디렉터리에 등록된 주택 보험 응용 프로그램에 액세스하기 전에 전화번호를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-111">For example, the consumer can sign into an auto insurance application with a social or local account, but must verify the phone number before accessing the home insurance application registered in the same directory.</span></span>
* <span data-ttu-id="6135d-112">일반적으로 응용 프로그램에 액세스하는 데 다단계 인증이 필요하지 않지만 그 안에 중요한 부분에 액세스하하려면 다단계 인증이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-112">You don't require Multi-Factor Authentication to access an application in general, but you do require it to access the sensitive portions within it.</span></span> <span data-ttu-id="6135d-113">예를 들어 소비자는 소셜 또는 로컬 계정으로 은행 응용 프로그램에 로그인하고 계정 잔액을 확인할 수 있지만 유선 전송을 시도하기 전에 전화번호를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-113">For example, the consumer can sign in to a banking application with a social or local account and check account balance, but must verify the phone number before attempting a wire transfer.</span></span>

## <a name="modify-your-sign-up-policy-to-enable-multi-factor-authentication"></a><span data-ttu-id="6135d-114">다단계 인증을 사용하도록 등록 정책을 수정합니다</span><span class="sxs-lookup"><span data-stu-id="6135d-114">Modify your sign-up policy to enable Multi-Factor Authentication</span></span>
1. <span data-ttu-id="6135d-115">[다음 단계에 따라 Azure 포털의 B2C 기능 블레이드로 이동합니다](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="6135d-115">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="6135d-116">**등록 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-116">Click **Sign-up policies**.</span></span>
3. <span data-ttu-id="6135d-117">사용자의 등록 정책(예: "B2C_1_SiUp")을 클릭하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-117">Click your sign-up policy (for example, "B2C_1_SiUp") to open it.</span></span>
4. <span data-ttu-id="6135d-118">**Multi-Factor Authentication**을 클릭하고 **상태**를 **켜기**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-118">Click **Multi-factor authentication** and turn the **State** to **ON**.</span></span> <span data-ttu-id="6135d-119">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-119">Click **OK**.</span></span>
5. <span data-ttu-id="6135d-120">블레이드 위쪽에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-120">Click **Save** at the top of the blade.</span></span>

<span data-ttu-id="6135d-121">정책에서 "지금 실행" 기능을 사용하여 고객 환경을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-121">You can use the "Run now" feature on the policy to verify the consumer experience.</span></span> <span data-ttu-id="6135d-122">다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-122">Confirm the following:</span></span>

<span data-ttu-id="6135d-123">다단계 인증 단계가 실행되기 전에 사용자의 디렉터리에 소비자 계정이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-123">A consumer account gets created in your directory before the Multi-Factor Authentication step occurs.</span></span> <span data-ttu-id="6135d-124">이 단계에서 소비자에게 자신의 전화 번호를 제공하고 확인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-124">During the step, the consumer is asked to provide his or her phone number and verify it.</span></span> <span data-ttu-id="6135d-125">확인에 성공한 경우 전화번호는 나중에 사용하도록 소비자 계정에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-125">If verification is successful, the phone number is attached to the consumer account for later use.</span></span> <span data-ttu-id="6135d-126">소비자가 취소 또는 삭제하더라도 다음에 로그인하는 동안 다시 전화 번호를 확인하도록 요청할 수 있습니다(다단계 인증을 사용하도록 설정한 경우).</span><span class="sxs-lookup"><span data-stu-id="6135d-126">Even if the consumer cancels or drops out, he or she can be asked to verify a phone number again during the next sign-in (with Multi-Factor Authentication enabled).</span></span>

## <a name="modify-your-sign-in-policy-to-enable-multi-factor-authentication"></a><span data-ttu-id="6135d-127">다단계 인증을 사용하도록 로그인 정책 수정</span><span class="sxs-lookup"><span data-stu-id="6135d-127">Modify your sign-in policy to enable Multi-Factor Authentication</span></span>
1. <span data-ttu-id="6135d-128">[다음 단계에 따라 Azure 포털의 B2C 기능 블레이드로 이동합니다](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="6135d-128">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="6135d-129">**로그인 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-129">Click **Sign-in policies**.</span></span>
3. <span data-ttu-id="6135d-130">사용자의 로그인 정책(예: "B2C_1_SiUp")을 클릭하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-130">Click your sign-in policy (for example, "B2C_1_SiIn") to open it.</span></span> <span data-ttu-id="6135d-131">블레이드 위쪽에서 **편집** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-131">Click **Edit** at the top of the blade.</span></span>
4. <span data-ttu-id="6135d-132">**Multi-Factor Authentication**을 클릭하고 **상태**를 **켜기**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-132">Click **Multi-factor authentication** and turn the **State** to **ON**.</span></span> <span data-ttu-id="6135d-133">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-133">Click **OK**.</span></span>
5. <span data-ttu-id="6135d-134">블레이드 위쪽에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-134">Click **Save** at the top of the blade.</span></span>

<span data-ttu-id="6135d-135">정책에서 "지금 실행" 기능을 사용하여 고객 환경을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-135">You can use the "Run now" feature on the policy to verify the consumer experience.</span></span> <span data-ttu-id="6135d-136">다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-136">Confirm the following:</span></span>

<span data-ttu-id="6135d-137">소비자가 (소셜 또는 로컬 계정을 사용하여)로그인할 때 확인된 전화번호가 소비자 계정에 연결된 경우 확인하도록 요청을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-137">When the consumer signs in (using a social or local account), if a verified phone number is attached to the consumer account, he or she is asked to verify it.</span></span> <span data-ttu-id="6135d-138">전화 번호가 연결되지 않은 경우 소비자에게 전화 번호를 제공하고 확인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-138">If no phone number is attached, the consumer is asked to provide one and verify it.</span></span> <span data-ttu-id="6135d-139">확인에 성공한 경우 전화번호는 나중에 사용하도록 소비자 계정에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-139">On successful verification, the phone number is attached to the consumer account for later use.</span></span>

## <a name="multi-factor-authentication-on-other-policies"></a><span data-ttu-id="6135d-140">기타 정책에서 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="6135d-140">Multi-Factor Authentication on other policies</span></span>
<span data-ttu-id="6135d-141">위의 등록 및 로그인 정책에 설명한 대로 등록 또는 로그인 정책과 암호 재설정 정책에 Multi-Factor Authentication을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-141">As described for sign-up & sign-in policies above, it is also possible to enable multi-factor authentication on sign-up or sign-in policies and password reset policies.</span></span> <span data-ttu-id="6135d-142">정책을 편집하는 프로필에서 곧 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="6135d-142">It will be available soon on profile editing policies.</span></span>

