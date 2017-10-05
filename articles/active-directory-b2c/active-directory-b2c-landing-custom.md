---
title: "Azure Active Directory B2C: 사용자 지정 정책 방문 페이지 | Microsoft Docs"
description: "사용자 지정 정책을 사용하여 Azure Active Directory B2C에서 소비자 지향 응용 프로그램 개발"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f2079f53-a637-4f2d-b3a0-61a9647ad433
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 5/06/2017
ms.author: parakhj
ms.openlocfilehash: cb7a9f01e43d41eb7315cb37a41e69f044ce5566
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-sign-up-and-sign-in-consumers-in-your-applications-using-custom-policies"></a><span data-ttu-id="8c215-103">Azure Active Directory B2C: 사용자 지정 정책을 사용하여 응용 프로그램에 소비자 등록 및 로그인</span><span class="sxs-lookup"><span data-stu-id="8c215-103">Azure Active Directory B2C: Sign up and sign in consumers in your applications using custom policies</span></span>
<span data-ttu-id="8c215-104">사용자 지정 정책은 Azure AD B2C 테넌트의 동작을 정의하는 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8c215-104">Custom policies are configuration files that define the behavior of your Azure AD B2C tenant.</span></span> <span data-ttu-id="8c215-105">ID 개발자가 완전히 편집하여 거의 무제한의 작업을 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c215-105">They can be fully edited by an identity developer to complete a near unlimited number of tasks.</span></span>

## <a name="how-to-articles"></a><span data-ttu-id="8c215-106">방법 문서</span><span class="sxs-lookup"><span data-stu-id="8c215-106">How-to articles</span></span>
<span data-ttu-id="8c215-107">특정 Azure Active Directory B2C 기능을 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8c215-107">Learn how to use specific Azure Active Directory B2C features:</span></span>

* [<span data-ttu-id="8c215-108">시작</span><span class="sxs-lookup"><span data-stu-id="8c215-108">Get Started</span></span>](active-directory-b2c-overview-custom.md)
* <span data-ttu-id="8c215-109">[Azure AD](active-directory-b2c-setup-aad-custom.md)와 같은 OIDC 공급자를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8c215-109">Configure OIDC Providers such as [Azure AD](active-directory-b2c-setup-aad-custom.md).</span></span>
* <span data-ttu-id="8c215-110">[Salesforce](active-directory-b2c-setup-sf-app-custom.md)와 같은 SAML 공급자를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8c215-110">Configure SAML Providers such as [Salesforce](active-directory-b2c-setup-sf-app-custom.md).</span></span>
* <span data-ttu-id="8c215-111">RESTful API 통합:</span><span class="sxs-lookup"><span data-stu-id="8c215-111">Integrate RESTful APIs:</span></span>
    * <span data-ttu-id="8c215-112">[추가 클레임을 가져옵니다](active-directory-b2c-rest-api-step-custom.md).</span><span class="sxs-lookup"><span data-stu-id="8c215-112">[Obtain additional claims](active-directory-b2c-rest-api-step-custom.md).</span></span>
    * <span data-ttu-id="8c215-113">[사용자 입력 유효성을 검사합니다](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="8c215-113">[Validate user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>
* <span data-ttu-id="8c215-114">로그인 사용자 지정:</span><span class="sxs-lookup"><span data-stu-id="8c215-114">Customize Login:</span></span>
    * [<span data-ttu-id="8c215-115">사용자 입력 구성</span><span class="sxs-lookup"><span data-stu-id="8c215-115">Configure User Input</span></span>](active-directory-b2c-configure-signup-self-asserted-custom.md)
    * [<span data-ttu-id="8c215-116">UI 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="8c215-116">Customize UI</span></span>](active-directory-b2c-ui-customization-custom.md)
    * [<span data-ttu-id="8c215-117">토큰 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="8c215-117">Customize Token</span></span>](active-directory-b2c-reference-manage-sso-and-token-configuration.md)
* <span data-ttu-id="8c215-118">[Application Insights를 사용하여 로그를 수집](active-directory-b2c-troubleshoot-custom.md)하여 문제 해결.</span><span class="sxs-lookup"><span data-stu-id="8c215-118">Troubleshoot by [collecting logs using Application Insights](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="whats-new"></a><span data-ttu-id="8c215-119">새로운 기능</span><span class="sxs-lookup"><span data-stu-id="8c215-119">What's new</span></span>
<span data-ttu-id="8c215-120">여기를 다시 종종 확인하여 Azure Active Directory B2C에 대한 이후 변경 내용을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8c215-120">Check back here often to learn about future changes to the Azure Active Directory B2C.</span></span> <span data-ttu-id="8c215-121">또한 @AzureAD를 사용하여 업데이트에 대해 트윗합니다.</span><span class="sxs-lookup"><span data-stu-id="8c215-121">We'll also tweet about any updates by using @AzureAD.</span></span>



