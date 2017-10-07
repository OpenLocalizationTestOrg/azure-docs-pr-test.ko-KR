---
title: "aaaRegister hello 포털을 사용 하 여 Azure AD hello v2.0 끝점으로 응용 프로그램 | Microsoft Docs"
description: "Hello v2.0 끝점을 사용 하 여 tooregister Microsoft에서 로그인을 사용 하도록 설정 하 고 Microsoft에 액세스를 사용 하 여 앱을 서비스 하는 방법"
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
ms.openlocfilehash: c56c98906656062435516e820cb318a04c03149c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooregister-an-app-with-hello-v20-endpoint"></a><span data-ttu-id="58937-103">어떻게 tooregister hello v2.0 끝점을 사용 하 여 앱</span><span class="sxs-lookup"><span data-stu-id="58937-103">How tooregister an app with hello v2.0 endpoint</span></span>
<span data-ttu-id="58937-104">toobuild MSA 및 Azure AD를 모두 허용 하는 응용 프로그램 로그인을 처음 해야 tooregister Microsoft와 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="58937-104">toobuild an app that accepts both MSA & Azure AD sign-in, you'll first need tooregister an app with Microsoft.</span></span>  <span data-ttu-id="58937-105">지금은 없습니다 수 toouse Azure AD와 모든 기존 앱 수 또는 MSA-toocreate 브랜드 새 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="58937-105">At this time, you won't be able toouse any existing apps you may have with Azure AD or MSA - you'll need toocreate a brand new one.</span></span>

> [!NOTE]
> <span data-ttu-id="58937-106">모든 Azure Active Directory 시나리오 및 기능 hello v2.0 끝점에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58937-106">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="58937-107">에 대해 알아보세요 hello v2.0 끝점을 사용 해야 하는 경우 toodetermine [v2.0 제한](active-directory-v2-limitations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="58937-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="visit-hello-microsoft-app-registration-portal"></a><span data-ttu-id="58937-108">Hello Microsoft 응용 프로그램 등록 포털을 방문</span><span class="sxs-lookup"><span data-stu-id="58937-108">Visit hello Microsoft app registration portal</span></span>
<span data-ttu-id="58937-109">중요 한 정보는 처음-너무 이동[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)합니다.</span><span class="sxs-lookup"><span data-stu-id="58937-109">First things first - navigate too[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span></span>  <span data-ttu-id="58937-110">이곳은 Microsoft 앱을 관리할 수 있는 새로운 앱 등록 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="58937-110">This is a new app registration portal where you can manage your Microsoft apps.</span></span>

<span data-ttu-id="58937-111">개인, 직장 또는 학교 Microsoft 계정 중 하나로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="58937-111">Sign in with either a personal or work or school Microsoft account.</span></span>  <span data-ttu-id="58937-112">계정이 하나라도 없다면, 새로운 개인 계정을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="58937-112">If you don't have either, sign up for a new personal account.</span></span> <span data-ttu-id="58937-113">그렇게 오래 걸리지 않으니 등록하세요 - 기다리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="58937-113">Go ahead, it won't take long - we'll wait here.</span></span>

<span data-ttu-id="58937-114">등록했나요?</span><span class="sxs-lookup"><span data-stu-id="58937-114">Done?</span></span> <span data-ttu-id="58937-115">아마도 비어있을 Microsoft 앱의 목록을 보고 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="58937-115">You should now be looking at your list of Microsoft apps, which is probably empty.</span></span>  <span data-ttu-id="58937-116">변경을 시작해봅시다.</span><span class="sxs-lookup"><span data-stu-id="58937-116">Let's change that.</span></span>

<span data-ttu-id="58937-117">**앱 추가**를 클릭하여 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="58937-117">Click **Add an app**, and give it a name.</span></span>  <span data-ttu-id="58937-118">hello 포털 앱 코드에서 사용할는 전역적으로 고유한 응용 프로그램 Id를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="58937-118">hello portal will assign your app a globally unique  Application Id that you'll use later in your code.</span></span>  <span data-ttu-id="58937-119">Api 호출에 대 한 액세스 토큰 해야 하는 응용 프로그램 서버 측 구성 요소를 포함 하는 경우 (생각: Office, Azure 또는 고유한 web API)를 toocreate 합니다는 **응용 프로그램 암호** 여기에도 합니다.</span><span class="sxs-lookup"><span data-stu-id="58937-119">If your app includes a server-side component that needs access tokens for calling APIs (think: Office, Azure, or your own web API), you'll want toocreate an **Application Secret** here as well.</span></span>

<span data-ttu-id="58937-120">Hello 플랫폼 앱에서 사용할 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="58937-120">Next, add hello Platforms that your app will use.</span></span>

* <span data-ttu-id="58937-121">웹 기반 앱의 경우 로그인 메시지를 보낼 수 있는 **리디렉션 URI** 를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="58937-121">For web based apps, provide a **Redirect URI** where sign-in messages can be sent.</span></span>
* <span data-ttu-id="58937-122">모바일 앱에 대 한 hello 기본 아래로 복사 리디렉션 자동으로 생성 하는 uri입니다.</span><span class="sxs-lookup"><span data-stu-id="58937-122">For mobile apps, copy down hello default redirect uri automatically created for you.</span></span>

<span data-ttu-id="58937-123">필요에 따라 hello 프로필 섹션에서에서 로그인 페이지의 hello 모양과 느낌을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58937-123">Optionally, you can customize hello look and feel of your sign-in page in hello Profile section.</span></span>  <span data-ttu-id="58937-124">있는지 tooclick 확인 **저장** 넘어가기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="58937-124">Make sure tooclick **Save** before moving on.</span></span>

> [!NOTE]
> <span data-ttu-id="58937-125">사용 하 여 응용 프로그램을 만들 때 [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), toosign hello 포털을 사용 하는 hello 계정의 hello 홈 테 넌 트에서 hello 응용 프로그램 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58937-125">When you create an application using [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), hello application will be registered in hello home tenant of hello account that you use toosign into hello portal.</span></span>  <span data-ttu-id="58937-126">즉, 개인 Microsoft 계정을 사용하여 Azure AD 테넌트에 응용 프로그램을 등록할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="58937-126">This means that you can not register an application in your Azure AD tenant using a personal Microsoft account.</span></span>  <span data-ttu-id="58937-127">명시적으로 원할 경우 tooregister 응용 프로그램 특정 테 넌 트에 해당 테 넌 트에서 만든 원래 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="58937-127">If you explicitly wish tooregister an application in a particular tenant, sign in with an account originally created in that tenant.</span></span>
> 
> 

## <a name="build-a-quick-start-app"></a><span data-ttu-id="58937-128">빠른 시작 앱 빌드하기</span><span class="sxs-lookup"><span data-stu-id="58937-128">Build a quick start app</span></span>
<span data-ttu-id="58937-129">이제 Microsoft 앱을 가지고 있으므로 v2.0 빠른 시작 자습서 중 하나를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58937-129">Now that you have a Microsoft app, you can complete one of our v2.0 quick start tutorials.</span></span>  <span data-ttu-id="58937-130">몇가지 권장 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="58937-130">Here are a few recommendations:</span></span>

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

