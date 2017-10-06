---
title: "Active Directory의 조건부 액세스 Faq aaaAzure | Microsoft Docs"
description: "Azure Active Directory의 조건부 액세스에 대 한 질문과 대답 toofrequently를 가져옵니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: d23acbb01217d7e9717d1a43de1b46a929404118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a><span data-ttu-id="d61d5-103">Azure Active Directory 조건부 액세스 FAQ</span><span class="sxs-lookup"><span data-stu-id="d61d5-103">Azure Active Directory conditional access FAQs</span></span>

## <a name="which-applications-work-with-conditional-access-policies"></a><span data-ttu-id="d61d5-104">조건부 액세스 정책이 적용되는 응용 프로그램은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d61d5-104">Which applications work with conditional access policies?</span></span>

<span data-ttu-id="d61d5-105">조건부 액세스 정책과 함께 작동하는 응용 프로그램에 대한 자세한 내용은 [Azure Active Directory에서 조건부 액세스 규칙을 사용하는 응용 프로그램 및 브라우저](active-directory-conditional-access-supported-apps.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d61d5-105">For information about applications that work with conditional access policies, see [Applications and browsers that use conditional access rules in Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span></span>

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a><span data-ttu-id="d61d5-106">B2B 공동 작업과 게스트 사용자에게 조건부 액세스 정책이 적용됩니까?</span><span class="sxs-lookup"><span data-stu-id="d61d5-106">Are conditional access policies enforced for B2B collaboration and guest users?</span></span>

<span data-ttu-id="d61d5-107">B2B(Business-to-Business) 공동 작업 사용자에 대한 정책이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-107">Policies are enforced for business-to-business (B2B) collaboration users.</span></span> <span data-ttu-id="d61d5-108">그러나 경우에 따라 사용자 아닐 수 toosatisfy hello 정책 요구 사항.</span><span class="sxs-lookup"><span data-stu-id="d61d5-108">However, in some cases, a user might not be able toosatisfy hello policy requirements.</span></span> <span data-ttu-id="d61d5-109">예를 들어 게스트 사용자의 조직이 다단계 인증을 지원하지 않는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-109">For example, a guest user's organization might not support multi-factor authentication.</span></span> 



## <a name="does-a-sharepoint-online-policy-also-apply-tooonedrive-for-business"></a><span data-ttu-id="d61d5-110">SharePoint Online 정책도 해당 tooOneDrive 비즈니스에 대 한?</span><span class="sxs-lookup"><span data-stu-id="d61d5-110">Does a SharePoint Online policy also apply tooOneDrive for Business?</span></span>

<span data-ttu-id="d61d5-111">예.</span><span class="sxs-lookup"><span data-stu-id="d61d5-111">Yes.</span></span> <span data-ttu-id="d61d5-112">SharePoint Online 정책 비즈니스용 tooOneDrive도 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-112">A SharePoint Online policy also applies tooOneDrive for Business.</span></span>


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a><span data-ttu-id="d61d5-113">Word나 Outlook 등의 클라이언트 앱에 정책을 설정할 수 없는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d61d5-113">Why can’t I set a policy on client apps, like Word or Outlook?</span></span>

<span data-ttu-id="d61d5-114">조건부 액세스 정책은 서비스 액세스 요구 사항을 설정하고,</span><span class="sxs-lookup"><span data-stu-id="d61d5-114">A conditional access policy sets requirements for accessing a service.</span></span> <span data-ttu-id="d61d5-115">인증 toothat 서비스 발생할 때 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-115">It's enforced when authentication toothat service occurs.</span></span> <span data-ttu-id="d61d5-116">클라이언트 응용 프로그램에서 직접 hello 정책 설정 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-116">hello policy is not set directly on a client application.</span></span> <span data-ttu-id="d61d5-117">클라이언트가 서비스를 호출할 때 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-117">Instead, it is applied when a client calls a service.</span></span> <span data-ttu-id="d61d5-118">예를 들어 SharePoint에서 설정한 정책 적용 tooclients SharePoint 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-118">For example, a policy set on SharePoint applies tooclients calling SharePoint.</span></span> <span data-ttu-id="d61d5-119">Exchange에서 설정한 정책 tooOutlook 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-119">A policy set on Exchange applies tooOutlook.</span></span>

## <a name="does-a-conditional-access-policy-apply-tooservice-accounts"></a><span data-ttu-id="d61d5-120">조건부 액세스 정책 tooservice 계정을 해당?</span><span class="sxs-lookup"><span data-stu-id="d61d5-120">Does a conditional access policy apply tooservice accounts?</span></span>

<span data-ttu-id="d61d5-121">조건부 액세스 정책은 tooall 사용자 계정을 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-121">Conditional access policies apply tooall user accounts.</span></span> <span data-ttu-id="d61d5-122">여기에는 서비스 계정으로 사용되는 사용자 계정이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-122">This includes user accounts that are used as service accounts.</span></span> <span data-ttu-id="d61d5-123">종종 무인 모드로 실행 되는 서비스 계정에는 조건부 액세스 정책 hello 요구 사항을 만족할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-123">Often, a service account that runs unattended can't satisfy hello requirements of a conditional access policy.</span></span> <span data-ttu-id="d61d5-124">예를 들어 다단계 인증이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-124">For example, multi-factor authentication might be required.</span></span> <span data-ttu-id="d61d5-125">조건부 액세스 정책 관리 설정을 사용하여 서비스 계정을 정책에서 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-125">Service accounts can be excluded from a policy by using conditional access policy management settings.</span></span> 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a><span data-ttu-id="d61d5-126">조건부 액세스 정책을 구성하는 데 Graph API를 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="d61d5-126">Are Graph APIs available for configuring conditional access policies?</span></span>

<span data-ttu-id="d61d5-127">현재는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-127">Currently, no.</span></span> 

## <a name="what-is-hello-default-exclusion-policy-for-unsupported-device-platforms"></a><span data-ttu-id="d61d5-128">지원 되지 않는 장치 플랫폼에 대 한 hello 기본 제외 정책 이란?</span><span class="sxs-lookup"><span data-stu-id="d61d5-128">What is hello default exclusion policy for unsupported device platforms?</span></span>

<span data-ttu-id="d61d5-129">현재 iOS 및 Android 장치의 사용자에 대해 선택적으로 조건부 액세스 정책이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-129">Currently, conditional access policies are selectively enforced on users of iOS and Android devices.</span></span> <span data-ttu-id="d61d5-130">다른 장치 플랫폼에서 응용 프로그램을 기본적으로 영향을 받지 않습니다 iOS 및 Android 장치에 대 한 hello 조건부 액세스 정책.</span><span class="sxs-lookup"><span data-stu-id="d61d5-130">Applications on other device platforms are, by default, not affected by hello conditional access policy for iOS and Android devices.</span></span> <span data-ttu-id="d61d5-131">테 넌 트 관리자는 지원 되지 않는 플랫폼에서 toooverride hello 글로벌 정책 toodisallow 액세스 toousers를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-131">A tenant admin can choose toooverride hello global policy toodisallow access toousers on platforms that are not supported.</span></span>


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a><span data-ttu-id="d61d5-132">Microsoft Teams에 대해 조건부 액세스 정책이 어떻게 작동하나요?</span><span class="sxs-lookup"><span data-stu-id="d61d5-132">How do conditional access policies work for Microsoft Teams?</span></span>  

<span data-ttu-id="d61d5-133">Microsoft Teams는 모임, 일정, 파일 공유 등의 핵심 생산성 시나리오를 위해 Exchange Online 및 SharePoint Online을 많이 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-133">Microsoft Teams relies heavily on Exchange Online and SharePoint Online for core productivity scenarios, like meetings, calendars, and file sharing.</span></span> <span data-ttu-id="d61d5-134">이러한 클라우드 앱에 대해 설정 된 조건부 액세스 정책은 사용자가 로그인 할 때 tooMicrosoft 팀을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-134">Conditional access policies that are set for these cloud apps apply tooMicrosoft Teams when a user signs in.</span></span>

<span data-ttu-id="d61d5-135">Microsoft Teams는 Azure Active Directory 조건부 액세스 정책에서 별도의 클라우드 앱으로도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-135">Microsoft Teams also is supported separately as a cloud app in Azure Active Directory conditional access policies.</span></span> <span data-ttu-id="d61d5-136">클라우드 앱에 대해 설정 된 인증서 기관 정책은 사용자가 로그인 할 때 tooMicrosoft 팀을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-136">Certificate authority policies that are set for a cloud app apply tooMicrosoft Teams when a user signs in.</span></span>

<span data-ttu-id="d61d5-137">Windows 및 Mac용 Microsoft Teams 데스크톱 클라이언트는 최신 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-137">Microsoft Teams desktop clients for Windows and Mac support modern authentication.</span></span> <span data-ttu-id="d61d5-138">최신 인증 로그인에 플랫폼 간에 hello Azure Active Directory 인증 라이브러리 (ADAL) tooMicrosoft Office 클라이언트 응용 프로그램에 따라 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d61d5-138">Modern authentication brings sign-in based on hello Azure Active Directory Authentication Library (ADAL) tooMicrosoft Office client applications across platforms.</span></span> 
