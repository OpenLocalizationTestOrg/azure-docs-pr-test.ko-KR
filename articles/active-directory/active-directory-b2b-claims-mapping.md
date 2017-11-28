---
title: "aaaB2B 공동 작업 사용자 클레임에서 Azure Active Directory로의 매핑을 | Microsoft Docs"
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
ms.openlocfilehash: 9e26085e91a6004b2f11286ae9c1df133bd47341
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a><span data-ttu-id="306fc-103">Azure Active Directory의 B2B 공동 작업 사용자 클레임 매핑</span><span class="sxs-lookup"><span data-stu-id="306fc-103">B2B collaboration user claims mapping in Azure Active Directory</span></span>

<span data-ttu-id="306fc-104">Azure Active Directory (Azure AD) 지원 B2B 공동 작업 사용자에 대 한 hello SAML 토큰에서 발급 된 hello 클레임을 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="306fc-104">Azure Active Directory (Azure AD) supports customizing hello claims issued in hello SAML token for B2B collaboration users.</span></span> <span data-ttu-id="306fc-105">Toohello 응용 프로그램을 인증 하는 사용자를 Azure AD는 고유 하 게 식별 하는 hello 사용자에 대 한 정보 (또는 클레임)를 포함 하는 SAML 토큰 toohello 앱을 발급 합니다.</span><span class="sxs-lookup"><span data-stu-id="306fc-105">When a user authenticates toohello application, Azure AD issues a SAML token toohello app that contains information (or claims) about hello user that uniquely identifies them.</span></span> <span data-ttu-id="306fc-106">기본적으로 여기에 hello 사용자의 사용자 이름, 전자 메일 주소, 이름 및 성입니다.</span><span class="sxs-lookup"><span data-stu-id="306fc-106">By default, this includes hello user's user name, email address, first name, and last name.</span></span> <span data-ttu-id="306fc-107">있습니다 수 보거나 편집 hello 클레임 hello hello 특성 탭에서 SAML 토큰 toohello 응용 프로그램에에서 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="306fc-107">You can view or edit hello claims sent in hello SAML token toohello application under hello Attributes tab.</span></span>

<span data-ttu-id="306fc-108">다음 두 가지 가능한 hello SAML 토큰에서 발급 된 tooedit hello 클레임 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="306fc-108">There are two possible reasons why you might need tooedit hello claims issued in hello SAML token.</span></span>

1. <span data-ttu-id="306fc-109">hello 응용 프로그램을 썼는지 toorequire 다른 클레임 Uri의 설정 또는 클레임 값</span><span class="sxs-lookup"><span data-stu-id="306fc-109">hello application has been written toorequire a different set of claim URIs or claim values</span></span>

2. <span data-ttu-id="306fc-110">응용 프로그램에 Azure Active Directory에 저장 된 hello 사용자 계정 이름 이외의 hello NameIdentifier 클레임 toobe 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="306fc-110">Your application requires hello NameIdentifier claim toobe something other than hello user principal name stored in Azure Active Directory.</span></span>

  ![SAML 토큰의 클레임 보기](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

<span data-ttu-id="306fc-112">이 문서에 사용자 지정 클레임, 클레임을 tooadd 및 편집 하는 방법에 대 한 내용은 확인해 [Azure Active Directory에 사전 통합된 앱에 대 한 hello SAML 토큰에서 발급 된 클레임을 사용자 지정](develop/active-directory-saml-claims-customization.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="306fc-112">For information on how tooadd and edit claims, check out this article on claims customization, [Customizing claims issued in hello SAML token for pre-integrated apps in Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span></span> <span data-ttu-id="306fc-113">B2B 공동 작업 사용자의 경우 보안상의 이유로 테넌트 간 NameID 및 UPN 매핑이 금지됩니다.</span><span class="sxs-lookup"><span data-stu-id="306fc-113">For B2B collaboration users, mapping NameID and UPN cross-tenant are prevented for security reasons.</span></span>


## <a name="next-steps"></a><span data-ttu-id="306fc-114">다음 단계</span><span class="sxs-lookup"><span data-stu-id="306fc-114">Next steps</span></span>

<span data-ttu-id="306fc-115">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="306fc-115">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="306fc-116">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="306fc-116">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="306fc-117">B2B 공동 작업 사용자 속성</span><span class="sxs-lookup"><span data-stu-id="306fc-117">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="306fc-118">B2B 공동 작업 사용자 tooa 역할 추가</span><span class="sxs-lookup"><span data-stu-id="306fc-118">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="306fc-119">B2B 공동 작업 초대 위임</span><span class="sxs-lookup"><span data-stu-id="306fc-119">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="306fc-120">동적 그룹 및 B2B 공동 작업</span><span class="sxs-lookup"><span data-stu-id="306fc-120">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="306fc-121">B2B 공동 작업 코드 및 PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="306fc-121">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="306fc-122">B2B 공동 작업용 SaaS 앱 구성</span><span class="sxs-lookup"><span data-stu-id="306fc-122">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="306fc-123">Office 365 외부 공유</span><span class="sxs-lookup"><span data-stu-id="306fc-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="306fc-124">B2B 공동 작업 사용자 토큰</span><span class="sxs-lookup"><span data-stu-id="306fc-124">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="306fc-125">B2B 공동 작업 현재 제한</span><span class="sxs-lookup"><span data-stu-id="306fc-125">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
