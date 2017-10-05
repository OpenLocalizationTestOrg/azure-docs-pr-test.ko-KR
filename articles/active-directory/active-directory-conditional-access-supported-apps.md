---
title: "Azure Active Directory에서 조건부 액세스 규칙을 사용하는 응용 프로그램 및 브라우저 | Microsoft Docs"
description: "Azure Active Directory에서는 사용자를 인증할 때 조건부 액세스 제어를 통해 특정 조건을 확인하여 응용 프로그램에 대한 액세스를 허용합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 62349fba-3cc0-4ab5-babe-372b3389eff6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 8614660f7c98af7b4e6d50348775495c67ae1cc8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="applications-and-browsers-that-use-conditional-access-rules-in-azure-active-directory"></a><span data-ttu-id="cdc57-103">Azure Active Directory에서 조건부 액세스 규칙을 사용하는 응용 프로그램 및 브라우저</span><span class="sxs-lookup"><span data-stu-id="cdc57-103">Applications and browsers that use conditional access rules in Azure Active Directory</span></span>

<span data-ttu-id="cdc57-104">조건부 액세스 규칙은 Azure AD(Azure Active Directory) 연결 응용 프로그램, 페더레이션된 사전 통합 SaaS(Software as a Service) 응용 프로그램, 암호 SSO(Single Sign-On)를 사용하는 프로그램, LOB(기간 업무) 응용 프로그램 및 Azure AD 응용 프로그램 프록시를 사용하는 응용 프로그램에서 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-104">Conditional access rules are supported in Azure Active Directory (Azure AD)-connected applications, pre-integrated federated software as a service (SaaS) applications, applications that use password single sign-on (SSO), line-of-business applications, and applications that use Azure AD Application Proxy.</span></span> <span data-ttu-id="cdc57-105">조건부 액세스를 사용할 수 있는 응용 프로그램의 자세한 목록은 [조건부 액세스로 설정된 서비스](active-directory-conditional-access-technical-reference.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdc57-105">For a detailed list of applications for which you can use conditional access, see [Services enabled with conditional access](active-directory-conditional-access-technical-reference.md).</span></span> <span data-ttu-id="cdc57-106">조건부 액세스는 최신 인증을 사용하는 모바일과 데스크톱 응용 프로그램 모두에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-106">Conditional access works both with mobile and desktop applications that use modern authentication.</span></span> <span data-ttu-id="cdc57-107">이 문서에서는 모바일 및 데스크톱 앱에서 조건부 액세스가 작동되는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-107">In this article, we cover how conditional access works in mobile and desktop apps.</span></span>

<span data-ttu-id="cdc57-108">최신 인증을 사용하는 응용 프로그램에서 Azure AD 로그인 페이지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-108">You can use Azure AD sign-in pages in applications that use modern authentication.</span></span> <span data-ttu-id="cdc57-109">로그인 페이지에서는 사용자에게 다단계 인증을 요구하는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-109">With a sign-in page, a user is prompted for multi-factor authentication.</span></span> <span data-ttu-id="cdc57-110">사용자의 액세스가 차단되는 경우 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-110">A message is shown if the user's access is blocked.</span></span> <span data-ttu-id="cdc57-111">최신 인증은 Azure AD에서 장치를 인증하여 장치 기반 조건부 액세스 정책을 평가하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-111">Modern authentication is required for the device to authenticate with Azure AD, so that device-based conditional access policies are evaluated.</span></span>

<span data-ttu-id="cdc57-112">조건부 액세스 규칙을 사용할 수 있는 응용 프로그램과 다른 응용 프로그램 진입점을 보호하기 위해 수행해야 하는 조치를 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-112">It's important to know which applications can use conditional access rules, and the steps that you might need to take to secure other application entry points.</span></span>

## <a name="applications-that-use-modern-authentication"></a><span data-ttu-id="cdc57-113">최신 인증을 사용하는 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="cdc57-113">Applications that use modern authentication</span></span>
> [!NOTE]
> <span data-ttu-id="cdc57-114">Azure AD에 Office 365와 대등한 조건부 액세스 정책이 있는 경우 두 조건부 액세스 정책을 모두 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-114">If you have a conditional access policy in Azure AD that has an equivalent in Office 365, configure both conditional access policies.</span></span> <span data-ttu-id="cdc57-115">예를 들어 Exchange Online 또는 SharePoint Online에 대한 조건부 액세스 정책이 여기에 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-115">This would apply, for example, to conditional access policies for Exchange Online or SharePoint Online.</span></span>
>
>

<span data-ttu-id="cdc57-116">Office 365 및 기타 Azure AD 연결 서비스 응용 프로그램에 대한 조건부 액세스를 지원하는 응용 프로그램은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-116">The following applications support conditional access for Office 365 and other Azure AD-connected service applications:</span></span>


| <span data-ttu-id="cdc57-117">대상 서비스</span><span class="sxs-lookup"><span data-stu-id="cdc57-117">Target Service</span></span>| <span data-ttu-id="cdc57-118">플랫폼</span><span class="sxs-lookup"><span data-stu-id="cdc57-118">Platform</span></span>| <span data-ttu-id="cdc57-119">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="cdc57-119">Application</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cdc57-120">모든 My Apps 앱 서비스</span><span class="sxs-lookup"><span data-stu-id="cdc57-120">Any My Apps app service</span></span>| <span data-ttu-id="cdc57-121">Android 및 iOS</span><span class="sxs-lookup"><span data-stu-id="cdc57-121">Android and iOS</span></span>| <span data-ttu-id="cdc57-122">앱에 대한 MFA 및 위치 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-122">MFA and location policy for apps.</span></span> <span data-ttu-id="cdc57-123">장치 기반 정책은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-123">Device based policies are not supported.</span></span>|
| <span data-ttu-id="cdc57-124">Azure 원격 앱 서비스</span><span class="sxs-lookup"><span data-stu-id="cdc57-124">Azure Remote App service</span></span>| <span data-ttu-id="cdc57-125">Windows 10, Windows 8.1, Windows 7, iOS, Android 및 Mac OS X</span><span class="sxs-lookup"><span data-stu-id="cdc57-125">Windows 10, Windows 8.1, Windows 7, iOS, Android, and Mac OS X</span></span>| <span data-ttu-id="cdc57-126">Azure 원격 앱</span><span class="sxs-lookup"><span data-stu-id="cdc57-126">Azure Remote app</span></span>|
| <span data-ttu-id="cdc57-127">Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="cdc57-127">Dynamics CRM</span></span>| <span data-ttu-id="cdc57-128">Windows 10, Windows 8.1, Windows 7, iOS 및 Android</span><span class="sxs-lookup"><span data-stu-id="cdc57-128">Windows 10, Windows 8.1, Windows 7, iOS, and Android</span></span>| <span data-ttu-id="cdc57-129">Dynamics CRM 앱</span><span class="sxs-lookup"><span data-stu-id="cdc57-129">Dynamics CRM app</span></span>|
| <span data-ttu-id="cdc57-130">Microsoft 팀</span><span class="sxs-lookup"><span data-stu-id="cdc57-130">Microsoft Teams</span></span>| <span data-ttu-id="cdc57-131">Windows 10, Windows 8.1, Windows 7, iOS/Android 및 MAC OSX</span><span class="sxs-lookup"><span data-stu-id="cdc57-131">Windows 10, Windows 8.1, Windows 7, iOS/Android and MAC OSX</span></span>| <span data-ttu-id="cdc57-132">Microsoft Teams Services - Microsoft Teams 및 모든 클라이언트 앱(Windows 데스크톱, MAC OS X, iOS, Android, WP, 웹 클라이언트)을 지원하는 서비스를 모두 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-132">Microsoft Teams Services - this controls all services that support Microsoft Teams and all its Client Apps - Windows Desktop, MAC OS X, iOS, Android, WP, and web client</span></span>|
| <span data-ttu-id="cdc57-133">Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="cdc57-133">Office 365 Exchange Online</span></span>| <span data-ttu-id="cdc57-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="cdc57-134">Windows 10</span></span>| <span data-ttu-id="cdc57-135">메일/달력/인물 정보 앱, Outlook 2016, Outlook 2013(최신 인증 사용), 비즈니스용 Skype(최신 인증 사용)</span><span class="sxs-lookup"><span data-stu-id="cdc57-135">Mail/Calendar/People app, Outlook 2016, Outlook 2013 (with modern authentication), Skype for Business (with modern authentication)</span></span>|
| <span data-ttu-id="cdc57-136">Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="cdc57-136">Office 365 Exchange Online</span></span>| <span data-ttu-id="cdc57-137">Windows 8.1, Windows 7</span><span class="sxs-lookup"><span data-stu-id="cdc57-137">Windows 8.1, Windows 7</span></span>| <span data-ttu-id="cdc57-138">Outlook 2016, Outlook 2013(최신 인증 사용), 비즈니스용 Skype(최신 인증 사용)</span><span class="sxs-lookup"><span data-stu-id="cdc57-138">Outlook 2016, Outlook 2013 (with modern authentication), Skype for Business (with modern authentication)</span></span>|
| <span data-ttu-id="cdc57-139">Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="cdc57-139">Office 365 Exchange Online</span></span>| <span data-ttu-id="cdc57-140">iOS</span><span class="sxs-lookup"><span data-stu-id="cdc57-140">iOS</span></span>| <span data-ttu-id="cdc57-141">Outlook 모바일 앱</span><span class="sxs-lookup"><span data-stu-id="cdc57-141">Outlook mobile app</span></span>|
| <span data-ttu-id="cdc57-142">Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="cdc57-142">Office 365 Exchange Online</span></span>| <span data-ttu-id="cdc57-143">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="cdc57-143">Mac OS X</span></span>| <span data-ttu-id="cdc57-144">Outlook 2016(macOS용 Office)</span><span class="sxs-lookup"><span data-stu-id="cdc57-144">Outlook 2016 (Office for macOS)</span></span>|
| <span data-ttu-id="cdc57-145">Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="cdc57-145">Office 365 SharePoint Online</span></span>| <span data-ttu-id="cdc57-146">Windows 10</span><span class="sxs-lookup"><span data-stu-id="cdc57-146">Windows 10</span></span>| <span data-ttu-id="cdc57-147">Office 2016 앱, Universal Office 앱, Office 2013(최신 인증 사용), OneDrive 동기화 클라이언트([참고](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e)) 참조, 미래를 위해 계획된 Office 그룹 지원, 미래를 위해 계획된 SharePoint 앱 지원</span><span class="sxs-lookup"><span data-stu-id="cdc57-147">Office 2016 apps, Universal Office apps, Office 2013 (with modern authentication), OneDrive sync client (see [notes](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e)), Office Groups support planned for the future, SharePoint app support planned for the future</span></span>|
| <span data-ttu-id="cdc57-148">Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="cdc57-148">Office 365 SharePoint Online</span></span>| <span data-ttu-id="cdc57-149">Windows 8.1, Windows 7</span><span class="sxs-lookup"><span data-stu-id="cdc57-149">Windows 8.1, Windows 7</span></span>| <span data-ttu-id="cdc57-150">Office 2016 앱, Office 2013(최신 인증 사용), OneDrive 동기화 클라이언트([참고](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e) 참조)</span><span class="sxs-lookup"><span data-stu-id="cdc57-150">Office 2016 apps, Office 2013 (with modern authentication), OneDrive sync client (see [notes](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e))</span></span>|
| <span data-ttu-id="cdc57-151">Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="cdc57-151">Office 365 SharePoint Online</span></span>| <span data-ttu-id="cdc57-152">iOS, Android</span><span class="sxs-lookup"><span data-stu-id="cdc57-152">iOS, Android</span></span>| <span data-ttu-id="cdc57-153">Office 모바일 앱</span><span class="sxs-lookup"><span data-stu-id="cdc57-153">Office mobile apps</span></span>|
| <span data-ttu-id="cdc57-154">Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="cdc57-154">Office 365 SharePoint Online</span></span>| <span data-ttu-id="cdc57-155">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="cdc57-155">Mac OS X</span></span>| <span data-ttu-id="cdc57-156">macOS용 Office 2016(Word, Excel, PowerPoint, OneNote만 해당)</span><span class="sxs-lookup"><span data-stu-id="cdc57-156">Office 2016 for macOS (Word, Excel, PowerPoint, OneNote only).</span></span> <span data-ttu-id="cdc57-157">향후 제공될 예정인 비즈니스용 OneDrive 지원</span><span class="sxs-lookup"><span data-stu-id="cdc57-157">OneDrive for Business support planned for the future</span></span>|
| <span data-ttu-id="cdc57-158">Office 365 Yammer</span><span class="sxs-lookup"><span data-stu-id="cdc57-158">Office 365 Yammer</span></span>| <span data-ttu-id="cdc57-159">Windows 10, iOS, Android</span><span class="sxs-lookup"><span data-stu-id="cdc57-159">Windows 10, iOS, Android</span></span>| <span data-ttu-id="cdc57-160">Office Yammer 앱</span><span class="sxs-lookup"><span data-stu-id="cdc57-160">Office Yammer app</span></span>|
| <span data-ttu-id="cdc57-161">PowerBI 서비스</span><span class="sxs-lookup"><span data-stu-id="cdc57-161">PowerBI service</span></span>| <span data-ttu-id="cdc57-162">Windows 10, Windows 8.1, Windows 7 및 iOS</span><span class="sxs-lookup"><span data-stu-id="cdc57-162">Windows 10, Windows 8.1, Windows 7, and iOS</span></span>| <span data-ttu-id="cdc57-163">PowerBI 앱.</span><span class="sxs-lookup"><span data-stu-id="cdc57-163">PowerBI app.</span></span> <span data-ttu-id="cdc57-164">Android용 Power BI 앱은 장치 기반 조건부 액세스를 현재 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-164">The Power BI app for Android does not currently support device-based conditional access.</span></span>|
| <span data-ttu-id="cdc57-165">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="cdc57-165">Visual Studio Team Services</span></span>| <span data-ttu-id="cdc57-166">Windows 10, Windows 8.1, Windows 7, iOS 및 Android</span><span class="sxs-lookup"><span data-stu-id="cdc57-166">Windows 10, Windows 8.1, Windows 7, iOS, and Android</span></span>| <span data-ttu-id="cdc57-167">Visual Studio Team Services 앱</span><span class="sxs-lookup"><span data-stu-id="cdc57-167">Visual Studio Team Services app</span></span>|








## <a name="applications-that-do-not-use-modern-authentication"></a><span data-ttu-id="cdc57-168">최신 인증을 사용하지 않는 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="cdc57-168">Applications that do not use modern authentication</span></span>
<span data-ttu-id="cdc57-169">현재 최신 인증을 사용하지 않는 앱에 대한 액세스는 다른 방법을 사용하여 차단해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-169">Currently, you must use other methods to block access to apps that do not use modern authentication.</span></span> <span data-ttu-id="cdc57-170">최신 인증을 사용하지 않는 앱에 대한 액세스 규칙이 조건부 액세스를 통해 강제로 적용되지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-170">Access rules for apps that don't use modern authentication are not enforced by conditional access.</span></span> <span data-ttu-id="cdc57-171">이는 기본적으로 Exchange 및 SharePoint에 대한 액세스를 위한 고려 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-171">This primarily is a consideration for Exchange and SharePoint access.</span></span> <span data-ttu-id="cdc57-172">이전 버전의 앱은 대부분 이전 액세스 제어 프로토콜을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-172">Most earlier versions of apps use older access control protocols.</span></span>

### <a name="control-access-in-office-365-sharepoint-online"></a><span data-ttu-id="cdc57-173">Office 365 SharePoint Online 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="cdc57-173">Control access in Office 365 SharePoint Online</span></span>
<span data-ttu-id="cdc57-174">Set-SPOTenant cmdlet을 사용하여 SharePoint 액세스에 대한 레거시 프로토콜 사용을 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-174">You can disable legacy protocols for SharePoint access by using the Set-SPOTenant cmdlet.</span></span> <span data-ttu-id="cdc57-175">이 cmdlet을 사용하면 Office 클라이언트에서 오래된 인증 프로토콜로 SharePoint Online 리소스에 액세스할 수 없도록 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-175">Use this cmdlet to prevent Office clients that use non-modern authentication protocols from accessing SharePoint Online resources.</span></span>

<span data-ttu-id="cdc57-176">**예제 명령**: `Set-SPOTenant -LegacyAuthProtocolsEnabled $false`</span><span class="sxs-lookup"><span data-stu-id="cdc57-176">**Example command**: `Set-SPOTenant -LegacyAuthProtocolsEnabled $false`</span></span>

### <a name="control-access-in-office-365-exchange-online"></a><span data-ttu-id="cdc57-177">Office 365 Exchange Online 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="cdc57-177">Control access in Office 365 Exchange Online</span></span>
<span data-ttu-id="cdc57-178">Exchange에서는 중요한 두 가지 범주의 프로토콜을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-178">Exchange offers two main categories of protocols.</span></span> <span data-ttu-id="cdc57-179">다음 옵션을 검토한 후에 조직에 적합한 정책을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-179">Review the following options, and then select the policy that is right for your organization.</span></span>

* <span data-ttu-id="cdc57-180">**Exchange ActiveSync** -</span><span class="sxs-lookup"><span data-stu-id="cdc57-180">**Exchange ActiveSync**.</span></span> <span data-ttu-id="cdc57-181">기본적으로 다단계 인증 및 위치에 대한 조건부 액세스 정책은 Exchange ActiveSync에 강제로 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-181">By default, conditional access policies for multi-factor authentication and location are not enforced for Exchange ActiveSync.</span></span> <span data-ttu-id="cdc57-182">따라서 Exchange ActiveSync 정책을 직접 구성하거나 AD FS(Active Directory Federation Services) 규칙을 통해 Exchange ActiveSync를 차단함으로써 이러한 서비스에 대한 액세스를 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-182">You need to protect access to these services either by configuring Exchange ActiveSync policy directly, or by blocking Exchange ActiveSync by using Active Directory Federation Services (AD FS) rules.</span></span>
* <span data-ttu-id="cdc57-183">**레거시 프로토콜** -</span><span class="sxs-lookup"><span data-stu-id="cdc57-183">**Legacy protocols**.</span></span> <span data-ttu-id="cdc57-184">AD FS를 사용하면 레거시 프로토콜을 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-184">You can block legacy protocols with AD FS.</span></span> <span data-ttu-id="cdc57-185">이렇게 하면 최신 인증을 사용하지 않는 Office 2013 및 이전 버전의 Office와 같이 오래된 Office 클라이언트에 대한 액세스를 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-185">This blocks access to older Office clients, such as Office 2013 without modern authentication enabled, and earlier versions of Office.</span></span>

### <a name="use-ad-fs-to-block-legacy-protocol"></a><span data-ttu-id="cdc57-186">AD FS를 통한 레거시 프로토콜 차단</span><span class="sxs-lookup"><span data-stu-id="cdc57-186">Use AD FS to block legacy protocol</span></span>
<span data-ttu-id="cdc57-187">다음 예제 발급 권한 부여 규칙을 사용하면 AD FS 수준에서 레거시 프로토콜 액세스를 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-187">You can use the following example issuance authorization rules to block legacy protocol access at the AD FS level.</span></span> <span data-ttu-id="cdc57-188">일반적인 두 가지 구성에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-188">Choose from two common configurations.</span></span>

#### <a name="option-1-allow-exchange-activesync-and-allow-legacy-apps-but-only-on-the-intranet"></a><span data-ttu-id="cdc57-189">옵션 1: Exchange ActiveSync 허용 및 인트라넷에 있는 레거시 앱만 허용</span><span class="sxs-lookup"><span data-stu-id="cdc57-189">Option 1: Allow Exchange ActiveSync, and allow legacy apps, but only on the intranet</span></span>
<span data-ttu-id="cdc57-190">다음 세 가지 규칙을 Microsoft Office 365 ID 플랫폼의 AD FS 신뢰 당사자 트러스트에 적용하면 Exchange ActiveSync 트래픽과 브라우저 및 최신 인증 트래픽에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-190">By applying the following three rules to the AD FS relying party trust for Microsoft Office 365 Identity Platform, Exchange ActiveSync traffic, and browser and modern authentication traffic, have access.</span></span> <span data-ttu-id="cdc57-191">레거시 앱은 익스트라넷에서 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-191">Legacy apps are blocked from the extranet.</span></span>

##### <a name="rule-1"></a><span data-ttu-id="cdc57-192">규칙 1</span><span class="sxs-lookup"><span data-stu-id="cdc57-192">Rule 1</span></span>
    @RuleName = "Allow all intranet traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

##### <a name="rule-2"></a><span data-ttu-id="cdc57-193">규칙 2</span><span class="sxs-lookup"><span data-stu-id="cdc57-193">Rule 2</span></span>
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

##### <a name="rule-3"></a><span data-ttu-id="cdc57-194">규칙 3</span><span class="sxs-lookup"><span data-stu-id="cdc57-194">Rule 3</span></span>
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

#### <a name="option-2-allow-exchange-activesync-and-block-legacy-apps"></a><span data-ttu-id="cdc57-195">옵션 2: Exchange ActiveSync 허용 및 레거시 앱 차단</span><span class="sxs-lookup"><span data-stu-id="cdc57-195">Option 2: Allow Exchange ActiveSync, and block legacy apps</span></span>
<span data-ttu-id="cdc57-196">다음 세 가지 규칙을 Microsoft Office 365 ID 플랫폼의 AD FS 신뢰 당사자 트러스트에 적용하면 Exchange ActiveSync 트래픽과 브라우저 및 최신 인증 트래픽에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-196">By applying the following three rules to the AD FS relying party trust for Microsoft Office 365 Identity Platform, Exchange ActiveSync traffic, and browser and modern authentication traffic, have access.</span></span> <span data-ttu-id="cdc57-197">레거시 앱은 모든 위치에서 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-197">Legacy apps are blocked from any location.</span></span>

##### <a name="rule-1"></a><span data-ttu-id="cdc57-198">규칙 1</span><span class="sxs-lookup"><span data-stu-id="cdc57-198">Rule 1</span></span>
    @RuleName = "Allow all intranet traffic only for browser and modern authentication clients"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-2"></a><span data-ttu-id="cdc57-199">규칙 2</span><span class="sxs-lookup"><span data-stu-id="cdc57-199">Rule 2</span></span>
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-3"></a><span data-ttu-id="cdc57-200">규칙 3</span><span class="sxs-lookup"><span data-stu-id="cdc57-200">Rule 3</span></span>
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


## <a name="supported-browsers-for-device-based-policies"></a><span data-ttu-id="cdc57-201">장치 기반 정책에 대해 지원되는 브라우저</span><span class="sxs-lookup"><span data-stu-id="cdc57-201">Supported browsers for device based policies</span></span> 

<span data-ttu-id="cdc57-202">Azure AD가 장치를 식별하고 인증할 수 있는 경우 장치 준수 및 도메인 조인을 확인하는 장치 기반 정책에 대해서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-202">You can only get access for device based policies that check for device compliance and domain join when Azure AD can identify and authenticate the device.</span></span> <span data-ttu-id="cdc57-203">위치 및 MFA와 같은 대부분의 검사는 대부분의 장치 및 브라우저에서 작동하지만 장치 정책에는 아래에 나열된 OS 버전 및 브라우저가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-203">While most checks, like location and MFA work on most devices and browsers, device policies require of the OS version and browsers listed below.</span></span> <span data-ttu-id="cdc57-204">장치 정책이 설정되면 지원되지 않는 브라우저 또는 운영 체제에서 사용자에 대한 액세스가 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-204">Access is blocked for users on  unsupported browsers or the operating systems when a device policy is in place.</span></span> 

| <span data-ttu-id="cdc57-205">OS</span><span class="sxs-lookup"><span data-stu-id="cdc57-205">OS</span></span>                     | <span data-ttu-id="cdc57-206">브라우저</span><span class="sxs-lookup"><span data-stu-id="cdc57-206">Browsers</span></span>                 | <span data-ttu-id="cdc57-207">지원</span><span class="sxs-lookup"><span data-stu-id="cdc57-207">Support</span></span>     |
| :--                    | :--                      | :-:         |
| <span data-ttu-id="cdc57-208">Win 10</span><span class="sxs-lookup"><span data-stu-id="cdc57-208">Win 10</span></span>                 | <span data-ttu-id="cdc57-209">IE, Edge</span><span class="sxs-lookup"><span data-stu-id="cdc57-209">IE, Edge</span></span>                 | ![확인][1] |
| <span data-ttu-id="cdc57-211">Win 10</span><span class="sxs-lookup"><span data-stu-id="cdc57-211">Win 10</span></span>                 | <span data-ttu-id="cdc57-212">Chrome</span><span class="sxs-lookup"><span data-stu-id="cdc57-212">Chrome</span></span>                   | <span data-ttu-id="cdc57-213">미리 보기</span><span class="sxs-lookup"><span data-stu-id="cdc57-213">Preview</span></span>     |
| <span data-ttu-id="cdc57-214">Win 8 / 8.1</span><span class="sxs-lookup"><span data-stu-id="cdc57-214">Win 8 / 8.1</span></span>            | <span data-ttu-id="cdc57-215">IE, Chrome</span><span class="sxs-lookup"><span data-stu-id="cdc57-215">IE, Chrome</span></span>               | ![확인][1] |
| <span data-ttu-id="cdc57-217">Win 7</span><span class="sxs-lookup"><span data-stu-id="cdc57-217">Win 7</span></span>                  | <span data-ttu-id="cdc57-218">IE, Chrome</span><span class="sxs-lookup"><span data-stu-id="cdc57-218">IE, Chrome</span></span>               | ![확인][1] |
| <span data-ttu-id="cdc57-220">iOS</span><span class="sxs-lookup"><span data-stu-id="cdc57-220">iOS</span></span>                    | <span data-ttu-id="cdc57-221">Safari</span><span class="sxs-lookup"><span data-stu-id="cdc57-221">Safari</span></span>                   | ![확인][1] |
| <span data-ttu-id="cdc57-223">Android</span><span class="sxs-lookup"><span data-stu-id="cdc57-223">Android</span></span>                | <span data-ttu-id="cdc57-224">Chrome</span><span class="sxs-lookup"><span data-stu-id="cdc57-224">Chrome</span></span>                   | ![확인][1] |
| <span data-ttu-id="cdc57-226">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="cdc57-226">Windows Phone</span></span>          | <span data-ttu-id="cdc57-227">IE, Edge</span><span class="sxs-lookup"><span data-stu-id="cdc57-227">IE, Edge</span></span>                 | ![확인][1] |
| <span data-ttu-id="cdc57-229">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="cdc57-229">Windows Server 2016</span></span>    | <span data-ttu-id="cdc57-230">IE, Edge</span><span class="sxs-lookup"><span data-stu-id="cdc57-230">IE, Edge</span></span>                 | ![확인][1] |
| <span data-ttu-id="cdc57-232">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="cdc57-232">Windows Server 2016</span></span>    | <span data-ttu-id="cdc57-233">Chrome</span><span class="sxs-lookup"><span data-stu-id="cdc57-233">Chrome</span></span>                   | <span data-ttu-id="cdc57-234">서비스 예정</span><span class="sxs-lookup"><span data-stu-id="cdc57-234">Coming soon</span></span> |
| <span data-ttu-id="cdc57-235">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="cdc57-235">Windows Server 2012 R2</span></span> | <span data-ttu-id="cdc57-236">IE, Chrome</span><span class="sxs-lookup"><span data-stu-id="cdc57-236">IE, Chrome</span></span>               | ![확인][1] |
| <span data-ttu-id="cdc57-238">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="cdc57-238">Windows Server 2008 R2</span></span> | <span data-ttu-id="cdc57-239">IE, Chrome</span><span class="sxs-lookup"><span data-stu-id="cdc57-239">IE, Chrome</span></span>               | ![확인][1] |
| <span data-ttu-id="cdc57-241">Mac OS</span><span class="sxs-lookup"><span data-stu-id="cdc57-241">Mac OS</span></span>                 | <span data-ttu-id="cdc57-242">Safari</span><span class="sxs-lookup"><span data-stu-id="cdc57-242">Safari</span></span>                   | ![확인][1] |
| <span data-ttu-id="cdc57-244">Mac OS</span><span class="sxs-lookup"><span data-stu-id="cdc57-244">Mac OS</span></span>                 | <span data-ttu-id="cdc57-245">Chrome</span><span class="sxs-lookup"><span data-stu-id="cdc57-245">Chrome</span></span>                   | <span data-ttu-id="cdc57-246">서비스 예정</span><span class="sxs-lookup"><span data-stu-id="cdc57-246">Coming soon</span></span> |

> [!NOTE]
> <span data-ttu-id="cdc57-247">Chrome 지원의 경우 Windows 10 크리에이터 업데이트를 사용하고 [여기](https://chrome.google.com/webstore/detail/windows-10-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji)에 있는 확장을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc57-247">For Chrome support, you must be using Windows 10 Creators Update and install the extension found [here](https://chrome.google.com/webstore/detail/windows-10-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="cdc57-248">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cdc57-248">Next steps</span></span>

<span data-ttu-id="cdc57-249">자세한 내용은 [Azure Active Directory 조건부 액세스](active-directory-conditional-access.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdc57-249">For more details, see [Conditional access in Azure Active Directory](active-directory-conditional-access.md)</span></span>




<!--Image references-->
[1]: ./media/active-directory-conditional-access-supported-apps/ic195031.png


