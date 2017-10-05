---
title: "Azure Active Directory의 B2B 공동 작업 사용자 클레임 매핑 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업에 대한 클레임 매핑 참조"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 5f8559450b24effd40a38879aeae3a8dd03944a3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a><span data-ttu-id="1d0cf-103">Azure Active Directory의 B2B 공동 작업 사용자 클레임 매핑</span><span class="sxs-lookup"><span data-stu-id="1d0cf-103">B2B collaboration user claims mapping in Azure Active Directory</span></span>

<span data-ttu-id="1d0cf-104">Azure AD(Azure Active Directory)에서는 B2B 공동 작업 사용자에 대해 SAML 토큰에 발급된 클레임을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d0cf-104">Azure Active Directory (Azure AD) supports customizing the claims issued in the SAML token for B2B collaboration users.</span></span> <span data-ttu-id="1d0cf-105">사용자가 응용 프로그램에 인증할 때 Azure AD는 고유하게 식별하는 사용자에 대한 정보(또는 클레임)를 포함하는 앱에 SAML 토큰을 발급합니다.</span><span class="sxs-lookup"><span data-stu-id="1d0cf-105">When a user authenticates to the application, Azure AD issues a SAML token to the app that contains information (or claims) about the user that uniquely identifies them.</span></span> <span data-ttu-id="1d0cf-106">기본적으로 사용자의 사용자 이름, 전자 메일 주소, 이름 및 성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1d0cf-106">By default, this includes the user's user name, email address, first name, and last name.</span></span> <span data-ttu-id="1d0cf-107">특성 탭에서 응용 프로그램의 SAML 토큰에 전송된 클레임을 보거나 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d0cf-107">You can view or edit the claims sent in the SAML token to the application under the Attributes tab.</span></span>

<span data-ttu-id="1d0cf-108">SAML 토큰에 발급된 클레임을 편집해야 하는 두 가지 가능한 이유는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1d0cf-108">There are two possible reasons why you might need to edit the claims issued in the SAML token.</span></span>

1. <span data-ttu-id="1d0cf-109">응용 프로그램이 다른 클레임 URI 또는 클레임 값 집합을 요구하도록 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1d0cf-109">The application has been written to require a different set of claim URIs or claim values</span></span>

2. <span data-ttu-id="1d0cf-110">응용 프로그램이 Azure Active Directory에 저장된 사용자 계정 이름 이외의 NameIdentifier 클레임을 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="1d0cf-110">Your application requires the NameIdentifier claim to be something other than the user principal name stored in Azure Active Directory.</span></span>

  ![SAML 토큰의 클레임 보기](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

<span data-ttu-id="1d0cf-112">클레임 추가 및 편집 방법에 대한 자세한 내용은 클레임 사용자 지정에 대한 [Azure Active Directory의 사전 통합된 앱에 대한 SAML 토큰에서 발급된 클레임 사용자 지정](develop/active-directory-saml-claims-customization.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d0cf-112">For information on how to add and edit claims, check out this article on claims customization, [Customizing claims issued in the SAML token for pre-integrated apps in Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span></span> <span data-ttu-id="1d0cf-113">B2B 공동 작업 사용자의 경우 보안상의 이유로 테넌트 간 NameID 및 UPN 매핑이 금지됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d0cf-113">For B2B collaboration users, mapping NameID and UPN cross-tenant are prevented for security reasons.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1d0cf-114">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1d0cf-114">Next steps</span></span>

<span data-ttu-id="1d0cf-115">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="1d0cf-115">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="1d0cf-116">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="1d0cf-116">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="1d0cf-117">B2B 공동 작업 사용자 속성</span><span class="sxs-lookup"><span data-stu-id="1d0cf-117">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="1d0cf-118">역할에 B2B 공동 작업 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="1d0cf-118">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="1d0cf-119">B2B 공동 작업 초대 위임</span><span class="sxs-lookup"><span data-stu-id="1d0cf-119">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="1d0cf-120">동적 그룹 및 B2B 공동 작업</span><span class="sxs-lookup"><span data-stu-id="1d0cf-120">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="1d0cf-121">B2B 공동 작업 코드 및 PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="1d0cf-121">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="1d0cf-122">B2B 공동 작업용 SaaS 앱 구성</span><span class="sxs-lookup"><span data-stu-id="1d0cf-122">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="1d0cf-123">Office 365 외부 공유</span><span class="sxs-lookup"><span data-stu-id="1d0cf-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="1d0cf-124">B2B 공동 작업 사용자 토큰</span><span class="sxs-lookup"><span data-stu-id="1d0cf-124">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="1d0cf-125">B2B 공동 작업 현재 제한</span><span class="sxs-lookup"><span data-stu-id="1d0cf-125">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
