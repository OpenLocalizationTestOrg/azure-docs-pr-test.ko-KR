---
title: "aaaHow tooconfigure 새 다중 테 넌 트 응용 프로그램 | Microsoft Docs"
description: "어떻게 tooconfigure single sign on 사용자 지정 응용 프로그램에 대 한 개발 및 Azure AD 등록 합니다."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4d3499d8885933516d6597fa9f87bcf88cd5a428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-a-new-multi-tenant-application"></a><span data-ttu-id="599e7-103">어떻게 tooconfigure 새 다중 테 넌 트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="599e7-103">How tooconfigure a new multi-tenant application</span></span>

<span data-ttu-id="599e7-104">앱에서 페더레이션된 SSO(Single Sign-On) 사용은 OpenID Connect, SAML 2.0 또는 WS-Fed에 대해 Azure AD를 통해 페더레이션할 때 자동으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="599e7-104">Enabling federated single sign-on (SSO) in your app is automatically enabled when federating through Azure AD for OpenID Connect, SAML 2.0, or WS-Fed.</span></span> <span data-ttu-id="599e7-105">최종 사용자가 toosign 되더라도 응용 프로그램 이미 Azure AD와 기존 세션에 없으면 될 응용 프로그램에 잘못 구성 되었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="599e7-105">If your end users are having toosign in despite already having an existing session with Azure AD, it’s likely your app may be misconfigured.</span></span>

* <span data-ttu-id="599e7-106">ADAL/MSAL를 사용 하 여 했는지 확인 **PromptBehavior** 도**자동** 대신 **항상**합니다.</span><span class="sxs-lookup"><span data-stu-id="599e7-106">If you’re using ADAL/MSAL, make sure you have **PromptBehavior** set too**Auto** rather than **Always**.</span></span>

* <span data-ttu-id="599e7-107">모바일 앱을 빌드하는 경우 tooenable 브로커 또는 비 브로커 SSO 구성 작업을 추가로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="599e7-107">If you’re building a mobile app, you may need additional configurations tooenable brokered or non-brokered SSO.</span></span>

<span data-ttu-id="599e7-108">Android의 경우 [Android에서 앱 간 SSO를 사용하도록 설정](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="599e7-108">For Android, see [Enabling Cross App SSO in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span></span><br>

<span data-ttu-id="599e7-109">iOS의 경우 [iOS에서 앱 간 SSO를 사용하도록 설정](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="599e7-109">For iOS, see [Enabling Cross App SSO in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span></span>

## <a name="next-steps"></a><span data-ttu-id="599e7-110">다음 단계</span><span class="sxs-lookup"><span data-stu-id="599e7-110">Next steps</span></span>

[<span data-ttu-id="599e7-111">Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="599e7-111">Azure AD SSO</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[<span data-ttu-id="599e7-112">Android에서 앱 간 SSO를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="599e7-112">Enabling Cross App SSO in Android</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[<span data-ttu-id="599e7-113">iOS에서 앱 간 SSO를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="599e7-113">Enabling Cross App SSO in iOS</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[<span data-ttu-id="599e7-114">앱 tooAzureAD 통합</span><span class="sxs-lookup"><span data-stu-id="599e7-114">Integrating Apps tooAzureAD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

[<span data-ttu-id="599e7-115">AzureAD v2.0 수렴형 앱에 대한 동의 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="599e7-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="599e7-116">AzureAD StackOverflow</span><span class="sxs-lookup"><span data-stu-id="599e7-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
