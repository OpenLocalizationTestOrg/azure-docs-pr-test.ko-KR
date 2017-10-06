---
title: "aaaHow 응용 프로그램의 동의 works | Microsoft Docs"
description: "자세한 내용을 보려면 hello Azure AD의 승인 프레임 워크 toosee 작동 하는 방법에 대 한 방법을 사용할 수 있습니다 Azure AD에서 응용 프로그램을 개발할 때는"
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
ms.openlocfilehash: 1b090c0c8d49320a012d8a06b7e9d35134a3ab43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-application-consent-works"></a><span data-ttu-id="e0e7a-103">응용 프로그램 동의 작동 원리</span><span class="sxs-lookup"><span data-stu-id="e0e7a-103">How application consent works</span></span>

<span data-ttu-id="e0e7a-104">이 문서는 toohelp 응용 프로그램을 보다 효율적으로 개발할 수 있도록 승인 프레임 워크 hello Azure AD의 작동 방식에 대해 자세히 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0e7a-104">This article is toohelp you learn more about how hello Azure AD consent framework works so you can develop applications more effectively.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="e0e7a-105">권장되는 문서</span><span class="sxs-lookup"><span data-stu-id="e0e7a-105">Recommended documents</span></span>

- <span data-ttu-id="e0e7a-106">기본적으로 이해 가져오기 [동의 허용 하는 방법을 리소스 소유자 toogovern 응용 프로그램의 액세스 tooresources](https://docs.microsoft.com/azure/active-directory/develop/active-directory-dev-glossary#consent)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e7a-106">Get a general understanding of [how consent allows a resource owner toogovern an application's access tooresources](https://docs.microsoft.com/azure/active-directory/develop/active-directory-dev-glossary#consent).</span></span>
- <span data-ttu-id="e0e7a-107">단계별 개요를 확인할 [hello Azure AD의 승인 프레임 워크의 동의 구현 하는 방법](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#overview-of-the-consent-framework)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e7a-107">Get a step-by-step overview of [how hello Azure AD consent framework implements consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#overview-of-the-consent-framework).</span></span>
- <span data-ttu-id="e0e7a-108">좀 더 깊이 대 한 자세한 내용은 [다중 테 넌 트 응용 hello 승인 프레임 워크를 사용 하는 방법도](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) 고급 다중 계층 응용 프로그램 패턴을 지 원하는 tooimplement "user" 및 "admin" 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e7a-108">For more depth, learn [how a multi-tenant application can use hello consent framework](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) tooimplement "user" and "admin" consent, supporting more advanced multi-tier application patterns.</span></span>
- <span data-ttu-id="e0e7a-109">좀 더 깊이 대 한 자세한 내용은 [어떻게 동의 hello 인증 코드 부여 흐름 중 hello OAuth 2.0 프로토콜 계층에서 지원 됩니다.](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code#request-an-authorization-code)</span><span class="sxs-lookup"><span data-stu-id="e0e7a-109">For more depth, learn [how consent is supported at hello OAuth 2.0 protocol layer during hello authorization code grant flow.](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code#request-an-authorization-code)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0e7a-110">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e0e7a-110">Next steps</span></span>
[<span data-ttu-id="e0e7a-111">AzureAD StackOverflow</span><span class="sxs-lookup"><span data-stu-id="e0e7a-111">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
