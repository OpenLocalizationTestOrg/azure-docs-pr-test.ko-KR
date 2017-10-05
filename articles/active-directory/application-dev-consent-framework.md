---
title: "응용 프로그램 동의 작동 원리 | Microsoft Docs"
description: "Azure AD 동의 프레임워크 작동 원리를 이해하여 Azure AD에서 응용 프로그램을 개발할 때 이러한 프레임워크를 사용하는 방법 알아보기"
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
ms.openlocfilehash: 5abddf3a8698e3eb39f118f54eeac62ce68fed39
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-application-consent-works"></a><span data-ttu-id="899ad-103">응용 프로그램 동의 작동 원리</span><span class="sxs-lookup"><span data-stu-id="899ad-103">How application consent works</span></span>

<span data-ttu-id="899ad-104">이 문서는 Azure AD 동의 프레임워크의 작동 방식을 이해하여 응용 프로그램을 보다 효과적으로 개발할 수 있도록 지원하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="899ad-104">This article is to help you learn more about how the Azure AD consent framework works so you can develop applications more effectively.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="899ad-105">권장되는 문서</span><span class="sxs-lookup"><span data-stu-id="899ad-105">Recommended documents</span></span>

- <span data-ttu-id="899ad-106">[동의를 통해 리소스 소유자가 리소스에 대한 응용 프로그램 액세스를 제어하는 방법](https://docs.microsoft.com/azure/active-directory/develop/active-directory-dev-glossary#consent) 이해</span><span class="sxs-lookup"><span data-stu-id="899ad-106">Get a general understanding of [how consent allows a resource owner to govern an application's access to resources](https://docs.microsoft.com/azure/active-directory/develop/active-directory-dev-glossary#consent).</span></span>
- <span data-ttu-id="899ad-107">[Azure AD 동의 프레임워크가 동의를 구현하는 방법](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#overview-of-the-consent-framework)에 대한 단계별 개요 확인</span><span class="sxs-lookup"><span data-stu-id="899ad-107">Get a step-by-step overview of [how the Azure AD consent framework implements consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#overview-of-the-consent-framework).</span></span>
- <span data-ttu-id="899ad-108">좀 더 깊이 있는 이해를 위해 [다중 테넌트 응용 프로그램이 동의 프레임워크를 사용하여](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) "user" 및 "admin" 동의를 구현하고 좀 더 수준 높은 다중 계층 응용 프로그램 패턴을 지원하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="899ad-108">For more depth, learn [how a multi-tenant application can use the consent framework](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to implement "user" and "admin" consent, supporting more advanced multi-tier application patterns.</span></span>
- <span data-ttu-id="899ad-109">좀 더 깊이 있는 이해를 위해 [인증 코드 권한 부여 흐름 동안 OAuth 2.0 프로토콜 계층에서 동의가 지원되는 방식](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code#request-an-authorization-code) 알아보기</span><span class="sxs-lookup"><span data-stu-id="899ad-109">For more depth, learn [how consent is supported at the OAuth 2.0 protocol layer during the authorization code grant flow.](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code#request-an-authorization-code)</span></span>

## <a name="next-steps"></a><span data-ttu-id="899ad-110">다음 단계</span><span class="sxs-lookup"><span data-stu-id="899ad-110">Next steps</span></span>
[<span data-ttu-id="899ad-111">AzureAD StackOverflow</span><span class="sxs-lookup"><span data-stu-id="899ad-111">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
