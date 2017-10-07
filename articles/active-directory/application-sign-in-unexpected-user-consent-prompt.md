---
title: "aaaUnexpected 동의 확인 프롬프트 tooan 응용 프로그램에 로그인 할 때 | Microsoft Docs"
description: "어떻게 응용 프로그램에 대 한 동의 확인 프롬프트를 표시 하는 경우 tootroubleshoot 통합 한 예기치 않은 Azure AD와"
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
ms.openlocfilehash: 32b7a5e6256faee0dcfe2e1644da3d3428812d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-tooan-application"></a><span data-ttu-id="c3bd5-103">Tooan 응용 프로그램에 로그인 할 때 예기치 않은 동의 확인 프롬프트</span><span class="sxs-lookup"><span data-stu-id="c3bd5-103">Unexpected consent prompt when signing in tooan application</span></span>

<span data-ttu-id="c3bd5-104">Azure Active Directory와 통합 하는 많은 응용 프로그램 사용 권한 toovarious 리소스 순서 toorun에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3bd5-104">Many applications that integrate with Azure Active Directory require permissions toovarious resources in order toorun.</span></span> <span data-ttu-id="c3bd5-105">이러한 리소스는 Azure Active Directory와도 통합 되어 때 hello Azure AD를 사용 하 여 요청에 사용 권한을 tooaccess 동의 프레임 워크 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c3bd5-105">When these resources are also integrated with Azure Active Directory, permissions tooaccess them is requested using hello Azure AD consent framework.</span></span> 

<span data-ttu-id="c3bd5-106">따라서 표시 된 hello 처음으로 응용 프로그램을 사용 하는 한 번 종종 동의 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3bd5-106">This results in a consent prompt being shown hello first time an application is used, which is often a one-time operation.</span></span> 

## <a name="scenarios-in-which-users-see-consent-prompts"></a><span data-ttu-id="c3bd5-107">사용자에게 동의 확인 프롬프트를 표시하는 시나리오</span><span class="sxs-lookup"><span data-stu-id="c3bd5-107">Scenarios in which users see consent prompts</span></span>

<span data-ttu-id="c3bd5-108">다양한 시나리오에서 추가 프롬프트를 예상할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3bd5-108">Additional prompts can be expected in various scenarios:</span></span>

* <span data-ttu-id="c3bd5-109">hello hello 응용 프로그램에 필요한 사용 권한 집합이 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c3bd5-109">hello set of permissions required by hello application have changed.</span></span>

* <span data-ttu-id="c3bd5-110">이제 다른 (비관리자) 사용자가 사용 하는 hello 응용 프로그램 hello에 대 한 처음으로 사용할 수 없어서 관리자로 hello 동의한 사용자에 원래 toohello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="c3bd5-110">hello user who originally consented toohello application was not an administrator, and now a different (non-admin) User is using hello application for hello first time.</span></span>

* <span data-ttu-id="c3bd5-111">hello 동의한 사용자에 원래 toohello 응용 프로그램 관리자는 했지만에-를 대신 하 여 hello 전체 조직을 동의 하지 않을 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="c3bd5-111">hello user who originally consented toohello application was an administrator, but they did not consent on-behalf of hello entire organization.</span></span>

* <span data-ttu-id="c3bd5-112">hello 응용 프로그램을 사용 하 여 [증분 및 동적 동의](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) 승인을 처음 후 toorequest 추가 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3bd5-112">hello application is using [incremental and dynamic consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest additional permissions after consent was initially granted.</span></span> <span data-ttu-id="c3bd5-113">이것은 추가 응용 프로그램의 선택적 기능이 초기 기능에 필요한 것 이상의 권한을 필요로 할 경우에 종종 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3bd5-113">This is often used when optional features of an application additional require permissions beyond those required for baseline functionality.</span></span>

* <span data-ttu-id="c3bd5-114">동의가 처음에 부여된 후에 해지되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c3bd5-114">Consent was revoked after being granted initially.</span></span>

* <span data-ttu-id="c3bd5-115">hello 개발자가 사용 될 때마다 hello 응용 프로그램 toorequire 동의 확인 프롬프트를 구성 (참고:이 가장 좋은 방법은).</span><span class="sxs-lookup"><span data-stu-id="c3bd5-115">hello developer has configured hello application toorequire a consent prompt every time it is used (note: this is not best practice).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3bd5-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c3bd5-116">Next steps</span></span>

-   [<span data-ttu-id="c3bd5-117">Azure Active Directory에서 앱, 사용 권한 및 동의(v1.0 끝점)</span><span class="sxs-lookup"><span data-stu-id="c3bd5-117">Apps, permissions, and consent in Azure Active Directory (v1.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [<span data-ttu-id="c3bd5-118">범위, 권한 및 hello Azure Active Directory (v2.0 끝점)에 동의</span><span class="sxs-lookup"><span data-stu-id="c3bd5-118">Scopes, permissions, and consent in hello Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


