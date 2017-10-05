---
title: "포털을 사용하는 Azure AD v2.0 끝점에 응용 프로그램 등록 | Microsoft Docs"
description: "v2.0 끝점을 사용하여 Microsoft 서비스 로그인 및 액세스를 사용하도록 설정하기 위해 Microsoft에 앱을 등록하는 방법"
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: bb2f701f-3bc3-4759-94a5-8b9d53a8a0b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: e6202aa8665c906382666fe08a561421e50e0a8d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-register-an-app-with-the-v20-endpoint"></a><span data-ttu-id="5d32c-103">v2.0 끝점을 사용하여 앱을 등록하는 방법</span><span class="sxs-lookup"><span data-stu-id="5d32c-103">How to register an app with the v2.0 endpoint</span></span>
<span data-ttu-id="5d32c-104">MSA 와 Azure AD 로그인 모두를 허용하는 앱을 빌드하려면, 먼저 Microsoft에 앱을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d32c-104">To build an app that accepts both MSA & Azure AD sign-in, you'll first need to register an app with Microsoft.</span></span>  <span data-ttu-id="5d32c-105">지금은 Azure AD나 MSA를 사용하여 가지고 있는 기존의 앱은 사용할 수 없습니다. - 새 앱을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d32c-105">At this time, you won't be able to use any existing apps you may have with Azure AD or MSA - you'll need to create a brand new one.</span></span>

> [!NOTE]
> <span data-ttu-id="5d32c-106">일부 Azure Active Directory 시나리오 및 기능만 v2.0 끝점에서 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5d32c-106">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="5d32c-107">v2.0 끝점을 사용해야 하는지 확인하려면 [v2.0 제한 사항](active-directory-v2-limitations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d32c-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="visit-the-microsoft-app-registration-portal"></a><span data-ttu-id="5d32c-108">Microsoft 앱 등록 포털 방문</span><span class="sxs-lookup"><span data-stu-id="5d32c-108">Visit the Microsoft app registration portal</span></span>
<span data-ttu-id="5d32c-109">가장 먼저 해야 할 일입니다. - [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5d32c-109">First things first - navigate to [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span></span>  <span data-ttu-id="5d32c-110">이곳은 Microsoft 앱을 관리할 수 있는 새로운 앱 등록 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="5d32c-110">This is a new app registration portal where you can manage your Microsoft apps.</span></span>

<span data-ttu-id="5d32c-111">개인, 직장 또는 학교 Microsoft 계정 중 하나로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d32c-111">Sign in with either a personal or work or school Microsoft account.</span></span>  <span data-ttu-id="5d32c-112">계정이 하나라도 없다면, 새로운 개인 계정을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="5d32c-112">If you don't have either, sign up for a new personal account.</span></span> <span data-ttu-id="5d32c-113">그렇게 오래 걸리지 않으니 등록하세요 - 기다리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5d32c-113">Go ahead, it won't take long - we'll wait here.</span></span>

<span data-ttu-id="5d32c-114">등록했나요?</span><span class="sxs-lookup"><span data-stu-id="5d32c-114">Done?</span></span> <span data-ttu-id="5d32c-115">아마도 비어있을 Microsoft 앱의 목록을 보고 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5d32c-115">You should now be looking at your list of Microsoft apps, which is probably empty.</span></span>  <span data-ttu-id="5d32c-116">변경을 시작해봅시다.</span><span class="sxs-lookup"><span data-stu-id="5d32c-116">Let's change that.</span></span>

<span data-ttu-id="5d32c-117">**앱 추가**를 클릭하여 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d32c-117">Click **Add an app**, and give it a name.</span></span>  <span data-ttu-id="5d32c-118">포털은 코드에서 나중에 사용하는 전역적으로 고유한 응용 프로그램 ID를 앱에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="5d32c-118">The portal will assign your app a globally unique  Application Id that you'll use later in your code.</span></span>  <span data-ttu-id="5d32c-119">앱이 API(예: Office, Azure 또는 사용자의 고유한 웹 API)를 호출하는 액세스 토큰이 필요한 서버 측 구성 요소를 포함한 경우, **응용 프로그램 암호** 또한 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d32c-119">If your app includes a server-side component that needs access tokens for calling APIs (think: Office, Azure, or your own web API), you'll want to create an **Application Secret** here as well.</span></span>

<span data-ttu-id="5d32c-120">다음으로, 앱에서 사용할 플랫폼을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5d32c-120">Next, add the Platforms that your app will use.</span></span>

* <span data-ttu-id="5d32c-121">웹 기반 앱의 경우 로그인 메시지를 보낼 수 있는 **리디렉션 URI** 를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5d32c-121">For web based apps, provide a **Redirect URI** where sign-in messages can be sent.</span></span>
* <span data-ttu-id="5d32c-122">모바일 앱의 경우 자동으로 만들어진 기본 리디렉션 URI를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="5d32c-122">For mobile apps, copy down the default redirect uri automatically created for you.</span></span>

<span data-ttu-id="5d32c-123">필요에 따라 프로필 섹션에서 로그인 페이지의 디자인을 사용자 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d32c-123">Optionally, you can customize the look and feel of your sign-in page in the Profile section.</span></span>  <span data-ttu-id="5d32c-124">다음 단계로 넘어가기 전에 **저장** 을 클릭하십시오.</span><span class="sxs-lookup"><span data-stu-id="5d32c-124">Make sure to click **Save** before moving on.</span></span>

> [!NOTE]
> <span data-ttu-id="5d32c-125">[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)를 사용하여 응용 프로그램을 만드는 경우 응용 프로그램은 포털에 로그인하는 데 사용하는 계정의 홈 테넌트에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d32c-125">When you create an application using [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), the application will be registered in the home tenant of the account that you use to sign into the portal.</span></span>  <span data-ttu-id="5d32c-126">즉, 개인 Microsoft 계정을 사용하여 Azure AD 테넌트에 응용 프로그램을 등록할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5d32c-126">This means that you can not register an application in your Azure AD tenant using a personal Microsoft account.</span></span>  <span data-ttu-id="5d32c-127">응용 프로그램을 특정 테넌트에 명시적으로 등록하려면 해당 테넌트에 원래 만든 계정을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5d32c-127">If you explicitly wish to register an application in a particular tenant, sign in with an account originally created in that tenant.</span></span>
> 
> 

## <a name="build-a-quick-start-app"></a><span data-ttu-id="5d32c-128">빠른 시작 앱 빌드하기</span><span class="sxs-lookup"><span data-stu-id="5d32c-128">Build a quick start app</span></span>
<span data-ttu-id="5d32c-129">이제 Microsoft 앱을 가지고 있으므로 v2.0 빠른 시작 자습서 중 하나를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d32c-129">Now that you have a Microsoft app, you can complete one of our v2.0 quick start tutorials.</span></span>  <span data-ttu-id="5d32c-130">몇가지 권장 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5d32c-130">Here are a few recommendations:</span></span>

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

