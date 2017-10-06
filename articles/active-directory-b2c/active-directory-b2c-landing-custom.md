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
ms.openlocfilehash: 28a39f282488b81fc9e2ab7841b5f2cb4cd58715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-up-and-sign-in-consumers-in-your-applications-using-custom-policies"></a><span data-ttu-id="b09a1-103">Azure Active Directory B2C: 사용자 지정 정책을 사용하여 응용 프로그램에 소비자 등록 및 로그인</span><span class="sxs-lookup"><span data-stu-id="b09a1-103">Azure Active Directory B2C: Sign up and sign in consumers in your applications using custom policies</span></span>
<span data-ttu-id="b09a1-104">사용자 지정 정책은 Azure AD B2C 테 넌 트의 hello 동작을 정의 하는 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b09a1-104">Custom policies are configuration files that define hello behavior of your Azure AD B2C tenant.</span></span> <span data-ttu-id="b09a1-105">될 수 있습니다 거의 무제한 작업 수가 identity 개발자 toocomplete가 완벽 하 게 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="b09a1-105">They can be fully edited by an identity developer toocomplete a near unlimited number of tasks.</span></span>

## <a name="how-tooarticles"></a><span data-ttu-id="b09a1-106">Tooarticles 방법</span><span class="sxs-lookup"><span data-stu-id="b09a1-106">How-tooarticles</span></span>
<span data-ttu-id="b09a1-107">자세한 내용은 방법 toouse 특정 Azure Active Directory B2C 기능:</span><span class="sxs-lookup"><span data-stu-id="b09a1-107">Learn how toouse specific Azure Active Directory B2C features:</span></span>

* [<span data-ttu-id="b09a1-108">시작</span><span class="sxs-lookup"><span data-stu-id="b09a1-108">Get Started</span></span>](active-directory-b2c-overview-custom.md)
* <span data-ttu-id="b09a1-109">[Azure AD](active-directory-b2c-setup-aad-custom.md)와 같은 OIDC 공급자를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b09a1-109">Configure OIDC Providers such as [Azure AD](active-directory-b2c-setup-aad-custom.md).</span></span>
* <span data-ttu-id="b09a1-110">[Salesforce](active-directory-b2c-setup-sf-app-custom.md)와 같은 SAML 공급자를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b09a1-110">Configure SAML Providers such as [Salesforce](active-directory-b2c-setup-sf-app-custom.md).</span></span>
* <span data-ttu-id="b09a1-111">RESTful API 통합:</span><span class="sxs-lookup"><span data-stu-id="b09a1-111">Integrate RESTful APIs:</span></span>
    * <span data-ttu-id="b09a1-112">[추가 클레임을 가져옵니다](active-directory-b2c-rest-api-step-custom.md).</span><span class="sxs-lookup"><span data-stu-id="b09a1-112">[Obtain additional claims](active-directory-b2c-rest-api-step-custom.md).</span></span>
    * <span data-ttu-id="b09a1-113">[사용자 입력 유효성을 검사합니다](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="b09a1-113">[Validate user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>
* <span data-ttu-id="b09a1-114">로그인 사용자 지정:</span><span class="sxs-lookup"><span data-stu-id="b09a1-114">Customize Login:</span></span>
    * [<span data-ttu-id="b09a1-115">사용자 입력 구성</span><span class="sxs-lookup"><span data-stu-id="b09a1-115">Configure User Input</span></span>](active-directory-b2c-configure-signup-self-asserted-custom.md)
    * [<span data-ttu-id="b09a1-116">UI 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="b09a1-116">Customize UI</span></span>](active-directory-b2c-ui-customization-custom.md)
    * [<span data-ttu-id="b09a1-117">토큰 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="b09a1-117">Customize Token</span></span>](active-directory-b2c-reference-manage-sso-and-token-configuration.md)
* <span data-ttu-id="b09a1-118">[Application Insights를 사용하여 로그를 수집](active-directory-b2c-troubleshoot-custom.md)하여 문제 해결.</span><span class="sxs-lookup"><span data-stu-id="b09a1-118">Troubleshoot by [collecting logs using Application Insights](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="whats-new"></a><span data-ttu-id="b09a1-119">새로운 기능</span><span class="sxs-lookup"><span data-stu-id="b09a1-119">What's new</span></span>
<span data-ttu-id="b09a1-120">나중에 변경 내용 toohello Azure Active Directory B2C에 대 한 toolearn 자주 다시 여기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b09a1-120">Check back here often toolearn about future changes toohello Azure Active Directory B2C.</span></span> <span data-ttu-id="b09a1-121">또한 @AzureAD를 사용하여 업데이트에 대해 트윗합니다.</span><span class="sxs-lookup"><span data-stu-id="b09a1-121">We'll also tweet about any updates by using @AzureAD.</span></span>



