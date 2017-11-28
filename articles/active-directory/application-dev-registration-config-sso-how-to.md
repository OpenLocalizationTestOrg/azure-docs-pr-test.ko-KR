---
title: "새 다중 테넌트 응용 프로그램을 구성하는 방법 | Microsoft Docs"
description: "Azure AD로 개발 및 등록 중인 사용자 지정 응용 프로그램에 대해 Single Sign-On을 구성하는 방법."
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
ms.openlocfilehash: 0fdc58d82d9cd2e7edac33cc5af4b98d2fd06c56
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-a-new-multi-tenant-application"></a><span data-ttu-id="49220-103">새 다중 테넌트 응용 프로그램을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="49220-103">How to configure a new multi-tenant application</span></span>

<span data-ttu-id="49220-104">앱에서 페더레이션된 SSO(Single Sign-On) 사용은 OpenID Connect, SAML 2.0 또는 WS-Fed에 대해 Azure AD를 통해 페더레이션할 때 자동으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="49220-104">Enabling federated single sign-on (SSO) in your app is automatically enabled when federating through Azure AD for OpenID Connect, SAML 2.0, or WS-Fed.</span></span> <span data-ttu-id="49220-105">Azure AD에 기존 세션이 이미 있음에도 불구하고 최종 사용자가 로그인해야 하는 경우 앱이 잘못 구성되었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49220-105">If your end users are having to sign in despite already having an existing session with Azure AD, it’s likely your app may be misconfigured.</span></span>

* <span data-ttu-id="49220-106">ADAL/MSAL을 사용하는 경우 **PromptBehavior**를 **항상**이 아니라 **자동**으로 설정했는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="49220-106">If you’re using ADAL/MSAL, make sure you have **PromptBehavior** set to **Auto** rather than **Always**.</span></span>

* <span data-ttu-id="49220-107">모바일 앱을 빌드하는 경우 조정되었거나 조정되지 않은 SSO를 사용하려면 추가 구성이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49220-107">If you’re building a mobile app, you may need additional configurations to enable brokered or non-brokered SSO.</span></span>

<span data-ttu-id="49220-108">Android의 경우 [Android에서 앱 간 SSO를 사용하도록 설정](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49220-108">For Android, see [Enabling Cross App SSO in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span></span><br>

<span data-ttu-id="49220-109">iOS의 경우 [iOS에서 앱 간 SSO를 사용하도록 설정](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49220-109">For iOS, see [Enabling Cross App SSO in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span></span>

## <a name="next-steps"></a><span data-ttu-id="49220-110">다음 단계</span><span class="sxs-lookup"><span data-stu-id="49220-110">Next steps</span></span>

[<span data-ttu-id="49220-111">Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="49220-111">Azure AD SSO</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[<span data-ttu-id="49220-112">Android에서 앱 간 SSO를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="49220-112">Enabling Cross App SSO in Android</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[<span data-ttu-id="49220-113">iOS에서 앱 간 SSO를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="49220-113">Enabling Cross App SSO in iOS</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[<span data-ttu-id="49220-114">AzureAD와 앱 통합</span><span class="sxs-lookup"><span data-stu-id="49220-114">Integrating Apps to AzureAD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

[<span data-ttu-id="49220-115">AzureAD v2.0 수렴형 앱에 대한 동의 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="49220-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="49220-116">AzureAD StackOverflow</span><span class="sxs-lookup"><span data-stu-id="49220-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
