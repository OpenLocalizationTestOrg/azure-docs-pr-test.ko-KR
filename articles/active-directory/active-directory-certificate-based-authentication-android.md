---
title: "Android에서 Azure Active Directory 인증서 기반 인증 | Microsoft Docs"
description: "Android 장치에서 솔루션의 인증서 기반 인증을 구성하는 데 지원되는 시나리오 및 요구 사항에 대한 자세한 정보"
services: active-directory
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/28/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 8005bfe821fea25539c84efdccf6c49bd5f1f8ee
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-android"></a><span data-ttu-id="6d6bb-103">Android에서 Azure Active Directory 인증서 기반 인증</span><span class="sxs-lookup"><span data-stu-id="6d6bb-103">Azure Active Directory certificate-based authentication on Android</span></span>


<span data-ttu-id="6d6bb-104">CBA(인증서 기반 인증)를 사용하면 Exchange Online 계정을 다음에 연결할 때 Windows, Android 또는 iOS 장치의 클라이언트 인증서를 사용하여 Azure Active Directory에서 인증을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6bb-104">Certificate-based authentication (CBA) enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="6d6bb-105">Microsoft Outlook 및 Microsoft Word와 같은 Office 모바일 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="6d6bb-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="6d6bb-106">EAS(Exchange ActiveSync) 클라이언트</span><span class="sxs-lookup"><span data-stu-id="6d6bb-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="6d6bb-107">이 기능을 구성하면 모바일 장치의 특정 메일 및 Microsoft Office 응용 프로그램에 사용자 이름 및 암호 조합을 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6bb-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="6d6bb-108">이 항목에서는 Office 365 Enterprise, Business, Education, 미국 정부, 중국 및 독일 계획의 테넌트 사용자를 위해 iOS(Android) 장치에서 CBA를 구성하기 위한 요구 사항 및 지원되는 시나리오를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6bb-108">This topic provides you with the requirements and the supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>



<span data-ttu-id="6d6bb-109">이 기능은 Office 365 미국 국방부 및 연방 정부 계획에서 미리 보기 상태로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6bb-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>


## <a name="office-mobile-applications-support"></a><span data-ttu-id="6d6bb-110">Office 모바일 응용 프로그램 지원</span><span class="sxs-lookup"><span data-stu-id="6d6bb-110">Office mobile applications support</span></span>
| <span data-ttu-id="6d6bb-111">앱</span><span class="sxs-lookup"><span data-stu-id="6d6bb-111">Apps</span></span> | <span data-ttu-id="6d6bb-112">지원</span><span class="sxs-lookup"><span data-stu-id="6d6bb-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="6d6bb-113">Azure Information Protection 앱</span><span class="sxs-lookup"><span data-stu-id="6d6bb-113">Azure Information Protection app</span></span> |![확인][1] |
| <span data-ttu-id="6d6bb-115">Microsoft 팀</span><span class="sxs-lookup"><span data-stu-id="6d6bb-115">Microsoft Teams</span></span> |![확인][1] |
| <span data-ttu-id="6d6bb-117">OneNote</span><span class="sxs-lookup"><span data-stu-id="6d6bb-117">OneNote</span></span> |![확인][1] |
| <span data-ttu-id="6d6bb-119">OneDrive</span><span class="sxs-lookup"><span data-stu-id="6d6bb-119">OneDrive</span></span> |![확인][1] |
| <span data-ttu-id="6d6bb-121">Outlook</span><span class="sxs-lookup"><span data-stu-id="6d6bb-121">Outlook</span></span> |![확인][1] |
| <span data-ttu-id="6d6bb-123">Power BI 모바일 앱</span><span class="sxs-lookup"><span data-stu-id="6d6bb-123">Power BI mobile apps</span></span> |![확인][1] |
| <span data-ttu-id="6d6bb-125">비즈니스용 Skype</span><span class="sxs-lookup"><span data-stu-id="6d6bb-125">Skype for Business</span></span> |![확인][1] |
| <span data-ttu-id="6d6bb-127">Word / Excel / PowerPoint</span><span class="sxs-lookup"><span data-stu-id="6d6bb-127">Word / Excel / PowerPoint</span></span> |![확인][1] |
| <span data-ttu-id="6d6bb-129">Yammer</span><span class="sxs-lookup"><span data-stu-id="6d6bb-129">Yammer</span></span> |![확인][1] |


### <a name="implementation-requirements"></a><span data-ttu-id="6d6bb-131">구현 요구 사항</span><span class="sxs-lookup"><span data-stu-id="6d6bb-131">Implementation requirements</span></span>

<span data-ttu-id="6d6bb-132">장치 OS 버전은 Android 5.0(Lollipop) 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6bb-132">The device OS version must be Android 5.0 (Lollipop) and above.</span></span> 

<span data-ttu-id="6d6bb-133">페더레이션 서버가 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6bb-133">A federation server must be configured.</span></span>  

<span data-ttu-id="6d6bb-134">Azure Active Directory에서 클라이언트 인증서를 해지하려면 ADFS 토큰에 다음 클레임이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6bb-134">For Azure Active Directory to revoke a client certificate, the ADFS token must have the following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="6d6bb-135">(클라이언트 인증서의 일련 번호)</span><span class="sxs-lookup"><span data-stu-id="6d6bb-135">(The serial number of the client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="6d6bb-136">(클라이언트 인증서 발급자에 대한 문자열)</span><span class="sxs-lookup"><span data-stu-id="6d6bb-136">(The string for the issuer of the client certificate)</span></span> 

<span data-ttu-id="6d6bb-137">Azure Active Directory는 이러한 클레임이 ADFS 토큰(또는 다른 SAML 토큰)에서 사용 가능한 경우 새로 고침 토큰에 이러한 클레임을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6bb-137">Azure Active Directory adds these claims to the refresh token if they are available in the ADFS token (or any other SAML token).</span></span> <span data-ttu-id="6d6bb-138">새로 고침 토큰의 유효성을 검사해야 하는 경우 이 정보가 해지를 확인하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6bb-138">When the refresh token needs to be validated, this information is used to check the revocation.</span></span> 

<span data-ttu-id="6d6bb-139">ADFS 오류 페이지를 사용자 인증서를 가져오는 방법에 대한 지침으로 업데이트하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6bb-139">As a best practice, you should update the ADFS error pages with instructions on how to get a user certificate.</span></span>  
<span data-ttu-id="6d6bb-140">자세한 내용은 [AD FS 로그인 페이지 사용자 지정](https://technet.microsoft.com/library/dn280950.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d6bb-140">For more details, see [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>  

<span data-ttu-id="6d6bb-141">일부 Office 앱(최신 인증 사용)은 요청 시 Azure AD에 '*prompt=login*'을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6d6bb-141">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ to Azure AD in their request.</span></span> <span data-ttu-id="6d6bb-142">기본적으로 Azure AD는 ADFS에 대한 요청 시 이를 '*wauth=usernamepassworduri*'(ADFS에 U/P 인증을 수행하도록 요청함) 및 '*wfresh=0*'(ADFS에 SSO 상태를 무시하고 새 인증을 수행하도록 요청함)으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6bb-142">By default, Azure AD translates this in the request to ADFS to ‘*wauth=usernamepassworduri*’ (asks ADFS to do U/P auth) and ‘*wfresh=0*’ (asks ADFS to ignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="6d6bb-143">이러한 앱에 인증서 기반 인증을 사용하려면 기본 Azure AD 동작을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d6bb-143">If you want to enable certificate-based authentication for these apps, you need to modify the default Azure AD behavior.</span></span> <span data-ttu-id="6d6bb-144">페더레이션된 도메인 설정에서 '*PromptLoginBehavior*'를 '*Disabled*'로 설정만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6bb-144">Just set the ‘*PromptLoginBehavior*’ in your federated domain settings to ‘*Disabled*‘.</span></span> <span data-ttu-id="6d6bb-145">다음과 같은 [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet을 사용하면 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d6bb-145">You can use the [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet to perform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`



## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="6d6bb-146">Exchange ActiveSync 클라이언트 지원</span><span class="sxs-lookup"><span data-stu-id="6d6bb-146">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="6d6bb-147">Android 5.0(Lollipop) 이상의 특정 Exchange ActiveSync 응용 프로그램은 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d6bb-147">Certain Exchange ActiveSync applications on Android 5.0 (Lollipop) or later are supported.</span></span> <span data-ttu-id="6d6bb-148">전자 메일 응용 프로그램에서 이 기능을 지원하는지 확인하려면 응용 프로그램 개발자에게 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="6d6bb-148">To determine if your email application does support this feature, please contact your application developer.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="6d6bb-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6d6bb-149">Next steps</span></span>

<span data-ttu-id="6d6bb-150">사용자 환경에서 인증서 기반 인증을 구성하는 방법에 대한 자세한 내용은 [Android에서 인증서 기반 인증 시작](active-directory-certificate-based-authentication-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d6bb-150">If you want to configure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>

<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-android/ic195031.png
