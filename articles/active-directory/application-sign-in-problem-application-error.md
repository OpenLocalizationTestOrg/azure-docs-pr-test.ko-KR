---
title: "응용 프로그램의 페이지에 로그인 한 후에 aaaError | Microsoft Docs"
description: "Azure AD와 tooresolve 문제 로그인 방법 hello 응용 프로그램 자체에서 오류를 내보낼 때"
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
ms.openlocfilehash: 317b6f8e6417520ead80ae4e26c591ba6b134683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a><span data-ttu-id="0ff99-103">로그인한 후 응용 프로그램 페이지의 오류</span><span class="sxs-lookup"><span data-stu-id="0ff99-103">Error on an application's page after signing in</span></span>

<span data-ttu-id="0ff99-104">이 시나리오에서는 Azure AD의 사용자에 hello 체결 하지만 hello 응용 프로그램 흐름의 hello 사용자 toosuccessfully 마침 hello 로그인을 허용 하지 않도록 오류를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-104">In this scenario, Azure AD has signed hello user in, but hello application is displaying an error not allowing hello user toosuccessfully finish hello sign in flow.</span></span> <span data-ttu-id="0ff99-105">이 시나리오에서는 hello 응용 프로그램이 Azure AD를 통해 hello 응답 문제를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-105">In this scenario, hello application is not accepting hello response issue by Azure AD.</span></span>

<span data-ttu-id="0ff99-106">몇 가지 가능한 이유와 이유 hello 응용 프로그램에서 Azure AD hello 응답을 수락 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-106">There are some possible reasons why hello application didn’t accept hello response from Azure AD.</span></span> <span data-ttu-id="0ff99-107">Hello hello 응용 프로그램의에서 오류 충분히 명확 tooknow 아닌 경우 누락 된 항목과 hello 응답으로 다음:</span><span class="sxs-lookup"><span data-stu-id="0ff99-107">If hello error in hello application is not clear enough tooknow what is missing in hello response, then:</span></span>

-   <span data-ttu-id="0ff99-108">Azure AD hello 갤러리 hello 응용 프로그램을 사용 하는 경우 hello 문서의 모든 hello 단계를 따랐는지 확인 [어떻게 toodebug SAML 기반 single sign on tooapplications Azure Active Directory에서](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-108">If hello application is hello Azure AD Gallery, verify you have followed all hello steps in hello article [How toodebug SAML-based single sign-on tooapplications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span></span>

-   <span data-ttu-id="0ff99-109">와 같은 도구를 사용 하 여 [Fiddler](http://www.telerik.com/fiddler) toocapture SAML SAML 응답 및 SAML 토큰을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-109">Use a tool like [Fiddler](http://www.telerik.com/fiddler) toocapture SAML request, SAML response and SAML token.</span></span>

-   <span data-ttu-id="0ff99-110">무엇이 누락 hello 응용 프로그램 공급 업체 tooknow을 hello SAML 응답을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-110">Share hello SAML response with hello application vendor tooknow what is missing.</span></span>

## <a name="missing-attributes-in-hello-saml-response"></a><span data-ttu-id="0ff99-111">Hello SAML 응답의에서 누락 된 특성</span><span class="sxs-lookup"><span data-stu-id="0ff99-111">Missing attributes in hello SAML response</span></span>

<span data-ttu-id="0ff99-112">아래의 hello 단계를 수행 하는 tooadd hello Azure AD에 대 한 응답을 전송 하는 hello Azure AD 구성 toobe 특성:</span><span class="sxs-lookup"><span data-stu-id="0ff99-112">tooadd an attribute in hello Azure AD configuration toobe sent in hello Azure AD response, follow hello steps below:</span></span>

1.  <span data-ttu-id="0ff99-113">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="0ff99-113">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="0ff99-114">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-114">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0ff99-115">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-115">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0ff99-116">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-116">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0ff99-117">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-117">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="0ff99-118">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="0ff99-118">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="0ff99-119">Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-119">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="0ff99-120">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-120">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="0ff99-121">클릭 **보기 및 편집에서 다른 모든 사용자 특성** hello **사용자 특성** 섹션 tooedit hello 사용자가 로그인 할 때 hello SAML 토큰에서 보낸 toobe toohello 응용 프로그램 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-121">click **View and edit all other user attributes under** hello **User Attributes** section tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="0ff99-122">tooadd 특성:</span><span class="sxs-lookup"><span data-stu-id="0ff99-122">tooadd an attribute:</span></span>

   * <span data-ttu-id="0ff99-123">**특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-123">click **Add attribute**.</span></span> <span data-ttu-id="0ff99-124">Hello 입력 **이름** 및 hello 선택 hello **값** hello 드롭다운에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-124">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   * <span data-ttu-id="0ff99-125">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-125">Click **Save.**</span></span> <span data-ttu-id="0ff99-126">Hello 테이블에 새 특성을 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-126">You see hello new attribute in hello table.</span></span>

9.  <span data-ttu-id="0ff99-127">Hello 구성을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-127">Save hello configuration.</span></span>

<span data-ttu-id="0ff99-128">Hello 사용자 toohello 응용 프로그램에 로그인 하는 다음에 Azure AD hello 새 특성을 hello SAML 응답에에서 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-128">Next time hello user signs in toohello application, Azure AD send hello new attribute in hello SAML response.</span></span>

## <a name="hello-application-expects-a-different-user-identifier-value-or-format"></a><span data-ttu-id="0ff99-129">hello 응용 프로그램에서는 다른 사용자의 Id 값 또는 형식</span><span class="sxs-lookup"><span data-stu-id="0ff99-129">hello application expects a different User Identifier value or format</span></span>

<span data-ttu-id="0ff99-130">hello 로그인 toohello 응용 프로그램은 실패에 hello SAML 응답에는 역할 등의 특성 없기 때문에 또는 hello 응용 프로그램 hello EntityID 특성에 대 한 다른 형식 것 이기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-130">hello sign-in toohello application is failing because hello SAML response is missing attributes such as roles or because hello application is expecting a different format for hello EntityID attribute.</span></span>

## <a name="add-an-attribute-in-hello-azure-ad-application-configuration"></a><span data-ttu-id="0ff99-131">Hello Azure AD 응용 프로그램 구성에서 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-131">Add an attribute in hello Azure AD application configuration:</span></span>

<span data-ttu-id="0ff99-132">아래의 hello 단계를 수행 하는 사용자 식별자 값 toochange hello:</span><span class="sxs-lookup"><span data-stu-id="0ff99-132">toochange hello User Identifier value, follow hello steps below:</span></span>

1.  <span data-ttu-id="0ff99-133">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="0ff99-133">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="0ff99-134">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-134">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0ff99-135">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-135">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0ff99-136">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-136">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0ff99-137">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-137">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="0ff99-138">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="0ff99-138">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="0ff99-139">Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-139">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="0ff99-140">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-140">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="0ff99-141">Hello에서 **사용자 특성**, 선택 hello에 있는 사용자에 대 한 고유 식별자를 hello **사용자 식별자** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-141">Under hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

## <a name="change-entityid-user-identifier-format"></a><span data-ttu-id="0ff99-142">EntityID(사용자 식별자) 형식 변경</span><span class="sxs-lookup"><span data-stu-id="0ff99-142">Change EntityID (User Identifier) format</span></span>

<span data-ttu-id="0ff99-143">Hello 응용 프로그램으로 hello EntityID 특성에 대 한 다른 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-143">If hello application expects another format for hello EntityID attribute.</span></span> <span data-ttu-id="0ff99-144">그런 다음 Azure AD는 hello에 대 한 응답 toohello 응용 프로그램 사용자 인증 후 보냅니다 수 tooselect hello EntityID (사용자 식별자) 형식 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-144">Then, you won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="0ff99-145">Hello NameID 특성 (사용자 식별자)에 대 한 azure AD 선택 hello 형식 선택한 hello 값에 따라 또는 hello SAML AuthRequest hello에 hello 응용 프로그램에서 요청한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-145">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="0ff99-146">자세한 내용은 방문 hello 문서 [Single Sign On SAML 프로토콜](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) hello에서 NameIDPolicy 섹션.</span><span class="sxs-lookup"><span data-stu-id="0ff99-146">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>

## <a name="hello-application-expects-a-different-signature-method-for-hello-saml-response"></a><span data-ttu-id="0ff99-147">hello 응용 프로그램에서는 hello SAML 응답에 대 한 다른 서명 메서드</span><span class="sxs-lookup"><span data-stu-id="0ff99-147">hello application expects a different signature method for hello SAML response</span></span>

<span data-ttu-id="0ff99-148">toochange hello SAML 토큰의 어떤 부분은 Azure Active Directory에서 디지털 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-148">toochange what parts of hello SAML token are digitally signed by Azure Active Directory.</span></span> <span data-ttu-id="0ff99-149">아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-149">Follow hello steps below:</span></span>

1.  <span data-ttu-id="0ff99-150">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="0ff99-150">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="0ff99-151">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-151">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0ff99-152">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-152">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0ff99-153">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-153">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0ff99-154">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-154">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="0ff99-155">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="0ff99-155">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="0ff99-156">Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-156">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="0ff99-157">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-157">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="0ff99-158">클릭 **고급 인증서 서명 설정이 표시** hello에서 **SAML 서명 인증서** 섹션.</span><span class="sxs-lookup"><span data-stu-id="0ff99-158">click **Show advanced certificate signing settings** under hello **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="0ff99-159">적절 한 선택 hello **서명 옵션** hello 응용 프로그램에서 예상:</span><span class="sxs-lookup"><span data-stu-id="0ff99-159">Select hello appropriate **Signing Option** expected by hello application:</span></span>

  * <span data-ttu-id="0ff99-160">SAML 응답 서명</span><span class="sxs-lookup"><span data-stu-id="0ff99-160">Sign SAML response</span></span>

  * <span data-ttu-id="0ff99-161">SAML 응답 및 어설션 서명</span><span class="sxs-lookup"><span data-stu-id="0ff99-161">Sign SAML response and assertion</span></span>

  * <span data-ttu-id="0ff99-162">SAML 어설션 서명</span><span class="sxs-lookup"><span data-stu-id="0ff99-162">Sign SAML assertion</span></span>

<span data-ttu-id="0ff99-163">Hello 사용자 toohello 응용 프로그램에 로그인 하는 다음에 Azure AD 로그인 hello 선택한 hello SAML 응답의 일부분입니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-163">Next time hello user signs in toohello application, Azure AD sign hello part of hello SAML response selected.</span></span>

## <a name="hello-application-expects-hello-signing-algorithm-toobe-sha-1"></a><span data-ttu-id="0ff99-164">hello 응용 프로그램에서는 hello 서명 알고리즘 toobe s h A-1</span><span class="sxs-lookup"><span data-stu-id="0ff99-164">hello application expects hello signing algorithm toobe SHA-1</span></span>

<span data-ttu-id="0ff99-165">기본적으로 Azure AD 보안 알고리즘 대부분 hello를 사용 하 여 hello SAML 토큰에 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-165">By default, Azure AD signs hello SAML token using hello most security algorithm.</span></span> <span data-ttu-id="0ff99-166">Hello 서명 알고리즘 tooSHA-1을 변경 해도 hello 응용 프로그램에서 필요로 하지 않는 경우는 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-166">Changing hello sign algorithm tooSHA-1 is not recommended unless required by hello application.</span></span>

<span data-ttu-id="0ff99-167">toochange hello 서명 알고리즘, 아래 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-167">toochange hello signing algorithm, follow hello steps below:</span></span>

1.  <span data-ttu-id="0ff99-168">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="0ff99-168">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="0ff99-169">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-169">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0ff99-170">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-170">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0ff99-171">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-171">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0ff99-172">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-172">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="0ff99-173">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="0ff99-173">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="0ff99-174">Tooconfigure single sign on 원하는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-174">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="0ff99-175">Hello 응용 프로그램 로드 되 면 클릭 hello **Single sign on** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-175">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="0ff99-176">클릭 **고급 인증서 서명 설정이 표시** hello에서 **SAML 서명 인증서** 섹션.</span><span class="sxs-lookup"><span data-stu-id="0ff99-176">click **Show advanced certificate signing settings** under hello **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="0ff99-177">Hello에 s h A-1을 선택 **서명 알고리즘**합니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-177">Select SHA-1, in hello **Signing Algorithm**.</span></span>

<span data-ttu-id="0ff99-178">다음 번 hello toohello 응용 프로그램에서 사용자가 로그인, Azure AD 로그인 hello sha-1 알고리즘을 사용 하는 SAML 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="0ff99-178">Next time hello user signs in toohello application, Azure AD sign hello SAML token using SHA-1 algorithm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ff99-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0ff99-179">Next steps</span></span>
[<span data-ttu-id="0ff99-180">어떻게 toodebug SAML 기반 single sign on tooapplications Azure Active Directory에</span><span class="sxs-lookup"><span data-stu-id="0ff99-180">How toodebug SAML-based single sign-on tooapplications in Azure Active Directory</span></span>](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
