---
title: "로그인한 후 응용 프로그램 페이지의 오류 | Microsoft Docs"
description: "응용 프로그램 자체에서 오류를 내보내는 경우 Azure AD 로그인에서 발생한 문제를 해결하는 방법"
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
ms.openlocfilehash: a8cd93256f79ece268ec3411dfbdf590f4b24447
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a><span data-ttu-id="4a604-103">로그인한 후 응용 프로그램 페이지의 오류</span><span class="sxs-lookup"><span data-stu-id="4a604-103">Error on an application's page after signing in</span></span>

<span data-ttu-id="4a604-104">이 시나리오에서는 Azure AD에 로그인한 사용자가 있지만 응용 프로그램에서 사용자가 로그인 흐름을 성공적으로 완료할 수 없는 오류를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-104">In this scenario, Azure AD has signed the user in, but the application is displaying an error not allowing the user to successfully finish the sign in flow.</span></span> <span data-ttu-id="4a604-105">이 시나리오에서 응용 프로그램은 Azure AD에서 발생한 응답을 수락하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-105">In this scenario, the application is not accepting the response issue by Azure AD.</span></span>

<span data-ttu-id="4a604-106">응용 프로그램이 Azure AD의 응답을 수락하지 않은 이유에는 몇 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-106">There are some possible reasons why the application didn’t accept the response from Azure AD.</span></span> <span data-ttu-id="4a604-107">응용 프로그램의 오류가 응답에서 누락된 내용을 명확하게 파악하지 못한 경우, 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-107">If the error in the application is not clear enough to know what is missing in the response, then:</span></span>

-   <span data-ttu-id="4a604-108">응용 프로그램이 Azure AD 갤러리인 경우 [Azure Active Directory의 응용 프로그램에 SAML 기반 Single Sign-On을 디버깅하는 방법](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging) 문서에 있는 모든 단계를 수행했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-108">If the application is the Azure AD Gallery, verify you have followed all the steps in the article [How to debug SAML-based single sign-on to applications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span></span>

-   <span data-ttu-id="4a604-109">[Fiddler](http://www.telerik.com/fiddler)와 같은 도구를 사용하여 SAML 요청, SAML 응답 및 SAML 토큰을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-109">Use a tool like [Fiddler](http://www.telerik.com/fiddler) to capture SAML request, SAML response and SAML token.</span></span>

-   <span data-ttu-id="4a604-110">응용 프로그램 공급 업체와 함께 SAML 응답을 공유하여 누락된 내용을 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-110">Share the SAML response with the application vendor to know what is missing.</span></span>

## <a name="missing-attributes-in-the-saml-response"></a><span data-ttu-id="4a604-111">SAML 응답에서 누락된 특성</span><span class="sxs-lookup"><span data-stu-id="4a604-111">Missing attributes in the SAML response</span></span>

<span data-ttu-id="4a604-112">Azure AD 응답으로 보낼 Azure AD 구성의 특성을 추가하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-112">To add an attribute in the Azure AD configuration to be sent in the Azure AD response, follow the steps below:</span></span>

1.  <span data-ttu-id="4a604-113">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-113">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4a604-114">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-114">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4a604-115">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-115">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4a604-116">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-116">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4a604-117">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-117">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="4a604-118">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-118">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4a604-119">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-119">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="4a604-120">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-120">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4a604-121">**사용자 특성** 섹션**에서 다른 모든 사용자 특성 보기 및 편집**을 클릭하여 사용자가 로그인할 때 SAML 토큰을 통해 응용 프로그램으로 보낼 특성을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-121">click **View and edit all other user attributes under** the **User Attributes** section to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="4a604-122">특성을 추가하려면:</span><span class="sxs-lookup"><span data-stu-id="4a604-122">To add an attribute:</span></span>

   * <span data-ttu-id="4a604-123">**특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-123">click **Add attribute**.</span></span> <span data-ttu-id="4a604-124">**이름**을 입력하고 드롭다운에서 **값**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-124">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   * <span data-ttu-id="4a604-125">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-125">Click **Save.**</span></span> <span data-ttu-id="4a604-126">테이블에 새 특성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-126">You see the new attribute in the table.</span></span>

9.  <span data-ttu-id="4a604-127">구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-127">Save the configuration.</span></span>

<span data-ttu-id="4a604-128">다음 번에 사용자가 응용 프로그램에 로그인하면 Azure AD는 SAML 응답으로 새 특성을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-128">Next time the user signs in to the application, Azure AD send the new attribute in the SAML response.</span></span>

## <a name="the-application-expects-a-different-user-identifier-value-or-format"></a><span data-ttu-id="4a604-129">응용 프로그램에 필요한 다른 사용자 식별자 값 또는 형식</span><span class="sxs-lookup"><span data-stu-id="4a604-129">The application expects a different User Identifier value or format</span></span>

<span data-ttu-id="4a604-130">SAML 응답이 역할과 같은 특성을 누락하거나 응용 프로그램에 EntityID 특성에 대한 다른 형식이 필요하기 때문에 응용 프로그램에 대한 로그인이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-130">The sign-in to the application is failing because the SAML response is missing attributes such as roles or because the application is expecting a different format for the EntityID attribute.</span></span>

## <a name="add-an-attribute-in-the-azure-ad-application-configuration"></a><span data-ttu-id="4a604-131">Azure AD 응용 프로그램 구성에 특성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-131">Add an attribute in the Azure AD application configuration:</span></span>

<span data-ttu-id="4a604-132">사용자 식별자 값을 변경하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-132">To change the User Identifier value, follow the steps below:</span></span>

1.  <span data-ttu-id="4a604-133">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-133">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4a604-134">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-134">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4a604-135">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-135">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4a604-136">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-136">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4a604-137">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-137">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="4a604-138">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-138">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4a604-139">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-139">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="4a604-140">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-140">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4a604-141">**사용자 특성**의 **사용자 식별자** 드롭다운에서 사용자의 고유한 식별자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-141">Under the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

## <a name="change-entityid-user-identifier-format"></a><span data-ttu-id="4a604-142">EntityID(사용자 식별자) 형식 변경</span><span class="sxs-lookup"><span data-stu-id="4a604-142">Change EntityID (User Identifier) format</span></span>

<span data-ttu-id="4a604-143">응용 프로그램이 EntityID 특성에 대해 다른 형식을 필요로 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-143">If the application expects another format for the EntityID attribute.</span></span> <span data-ttu-id="4a604-144">사용자 인증 후에 Azure AD에서 응답을 통해 응용 프로그램으로 보내는 EntityID(사용자 식별자) 형식은 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-144">Then, you won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="4a604-145">Azure AD에서는 선택한 값 또는 SAML AuthRequest에서 응용 프로그램이 요청한 형식을 기반으로 NameID 특성(사용자 식별자)의 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-145">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="4a604-146">자세한 내용은 NameIDPolicy 섹션 아래의 [Single Sign-On SAML 프로토콜](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) 문서에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-146">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>

## <a name="the-application-expects-a-different-signature-method-for-the-saml-response"></a><span data-ttu-id="4a604-147">응용 프로그램은 SAML 응답에 대해 다른 시그니처 메서드를 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-147">The application expects a different signature method for the SAML response</span></span>

<span data-ttu-id="4a604-148">Azure Active Directory에서 디지털 방식으로 로그인한 SAML 토큰을 변경하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-148">To change what parts of the SAML token are digitally signed by Azure Active Directory.</span></span> <span data-ttu-id="4a604-149">다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="4a604-149">Follow the steps below:</span></span>

1.  <span data-ttu-id="4a604-150">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-150">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4a604-151">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-151">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4a604-152">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4a604-153">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-153">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4a604-154">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="4a604-155">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4a604-156">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-156">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="4a604-157">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-157">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4a604-158">**SAML 서명 인증서** 섹션에서 **고급 인증서 서명 설정 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-158">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="4a604-159">응용 프로그램에 필요한 적절한 **서명 옵션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-159">Select the appropriate **Signing Option** expected by the application:</span></span>

  * <span data-ttu-id="4a604-160">SAML 응답 서명</span><span class="sxs-lookup"><span data-stu-id="4a604-160">Sign SAML response</span></span>

  * <span data-ttu-id="4a604-161">SAML 응답 및 어설션 서명</span><span class="sxs-lookup"><span data-stu-id="4a604-161">Sign SAML response and assertion</span></span>

  * <span data-ttu-id="4a604-162">SAML 어설션 서명</span><span class="sxs-lookup"><span data-stu-id="4a604-162">Sign SAML assertion</span></span>

<span data-ttu-id="4a604-163">다음 번에 사용자가 응용 프로그램에 로그인하면 Azure AD는 선택한 SAML 응답의 일부를 서명합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-163">Next time the user signs in to the application, Azure AD sign the part of the SAML response selected.</span></span>

## <a name="the-application-expects-the-signing-algorithm-to-be-sha-1"></a><span data-ttu-id="4a604-164">응용 프로그램에 필요한 SHA-1이라는 서명 알고리즘</span><span class="sxs-lookup"><span data-stu-id="4a604-164">The application expects the signing algorithm to be SHA-1</span></span>

<span data-ttu-id="4a604-165">기본적으로 Azure AD는 대부분의 보안 알고리즘을 사용하여 SAML 토큰을 서명합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-165">By default, Azure AD signs the SAML token using the most security algorithm.</span></span> <span data-ttu-id="4a604-166">응용 프로그램에서 필요한 경우가 아니면 SHA-1로 서명 알고리즘을 변경하는 것을 권장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-166">Changing the sign algorithm to SHA-1 is not recommended unless required by the application.</span></span>

<span data-ttu-id="4a604-167">서명 알고리즘을 변경하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-167">To change the signing algorithm, follow the steps below:</span></span>

1.  <span data-ttu-id="4a604-168">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-168">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4a604-169">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-169">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4a604-170">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-170">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4a604-171">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-171">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4a604-172">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-172">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="4a604-173">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-173">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4a604-174">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-174">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="4a604-175">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-175">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4a604-176">**SAML 서명 인증서** 섹션에서 **고급 인증서 서명 설정 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-176">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="4a604-177">**서명 알고리즘**에서 SHA-1을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-177">Select SHA-1, in the **Signing Algorithm**.</span></span>

<span data-ttu-id="4a604-178">다음 번에 사용자가 응용 프로그램에 로그인하면 Azure AD는 SHA-1 알고리즘을 사용하여 SAML 토큰을 서명합니다.</span><span class="sxs-lookup"><span data-stu-id="4a604-178">Next time the user signs in to the application, Azure AD sign the SAML token using SHA-1 algorithm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a604-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4a604-179">Next steps</span></span>
[<span data-ttu-id="4a604-180">Azure Active Directory에서 SAML 기반 Single Sign-On을 응용 프로그램에 디버그하는 방법</span><span class="sxs-lookup"><span data-stu-id="4a604-180">How to debug SAML-based single sign-on to applications in Azure Active Directory</span></span>](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
