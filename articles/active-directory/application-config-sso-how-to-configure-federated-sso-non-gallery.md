---
title: "비갤러리 응용 프로그램에 대해 페더레이션된 Single Sign-On을 구성하는 방법 | Microsoft Docs"
description: "Azure AD와 통합할 사용자 지정 비갤러리 응용 프로그램에 대해 페더레이션된 Single Sign-On을 구성하는 방법"
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
ms.openlocfilehash: da7bc05c6452cde4d0236806f249559f178dd4e1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="9f550-103">비갤러리 응용 프로그램에 대해 페더레이션된 Single Sign-On을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="9f550-103">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="9f550-104">비갤러리 응용 프로그램을 구성하려면 Azure AD 프리미엄이 있어야 하며 응용 프로그램에서 SAML 2.0을 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-104">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="9f550-105">Azure AD 버전에 대한 자세한 내용은 [Azure AD 가격 책정](https://azure.microsoft.com/pricing/details/active-directory/)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-105">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="9f550-106">필요한 단계 개요</span><span class="sxs-lookup"><span data-stu-id="9f550-106">Overview of steps required</span></span>
<span data-ttu-id="9f550-107">다음은 비갤러리(예: 사용자 지정) 응용 프로그램에 대해 페더레이션된 Single Sign-On을 구성하는 데 필요한 단계를 요약한 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-107">Below is a high level overview of the steps required to configure federated single sign-on for a non-gallery (e.g., custom) application.</span></span>

-   [<span data-ttu-id="9f550-108">Azure AD에서 응용 프로그램의 메타데이터 값 구성(로그온 URL, 식별자, 회신 URL)</span><span class="sxs-lookup"><span data-stu-id="9f550-108">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="9f550-109">사용자 식별자를 선택하고 응용 프로그램에 보낼 사용자 특성 추가</span><span class="sxs-lookup"><span data-stu-id="9f550-109">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="9f550-110">Azure AD 메타데이터 및 인증서 검색</span><span class="sxs-lookup"><span data-stu-id="9f550-110">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="9f550-111">응용 프로그램에서 Azure AD 메타데이터 값 구성(로그온 URL, 발급자, 로그아웃 URL 및 인증서)</span><span class="sxs-lookup"><span data-stu-id="9f550-111">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="9f550-112">응용 프로그램에 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="9f550-112">Assign users to the application</span></span>](#_Assign_users_to_the_application)

## <a name="configuring-single-sign-on-to-non-gallery-applications"></a><span data-ttu-id="9f550-113">비갤러리 응용 프로그램에 Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="9f550-113">Configuring single sign-on to non-gallery applications</span></span>

<span data-ttu-id="9f550-114">Azure AD 갤러리에 없는 응용 프로그램에 대해 Single Sign-On을 구성하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-114">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="9f550-115">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-115">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9f550-116">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-116">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9f550-117">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-117">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9f550-118">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-118">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9f550-119">**엔터프라이즈 응용 프로그램** 블레이드의 오른쪽 위 모서리에서 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-119">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="9f550-120">**고유한 응용 프로그램 추가** 섹션에서 **비갤러리 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-120">click **Non-gallery application** in the **Add your own app** section</span></span>

7.  <span data-ttu-id="9f550-121">**이름** 텍스트 상자에 응용 프로그램 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-121">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="9f550-122">**추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-122">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="9f550-123">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-123">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="9f550-124">**모드** 드롭다운에서 **SAML 기반 로그온**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-124">Select **SAML-based Sign-on** in the **Mode** dropdown.</span></span>

11. <span data-ttu-id="9f550-125">**도메인 및 URL**에 필요한 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-125">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="9f550-126">이러한 값은 응용 프로그램 공급업체에서 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-126">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="9f550-127">응용 프로그램을 IdP에서 시작한 SSO로 구성하려면 회신 URL과 식별자를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-127">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

   2. <span data-ttu-id="9f550-128">**선택 사항:** 응용 프로그램을 SP에서 시작한 SSO로 구성하려면 로그온 URL 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-128">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="9f550-129">**사용자 특성**의 **사용자 식별자** 드롭다운에서 사용자의 고유한 식별자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-129">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="9f550-130">**선택 사항:** 사용자가 로그인할 때 SAML 토큰을 통해 응용 프로그램으로 보낼 특성을 편집하려면 **다른 모든 사용자 특성 보기 및 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-130">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="9f550-131">특성을 추가하려면:</span><span class="sxs-lookup"><span data-stu-id="9f550-131">To add an attribute:</span></span>

   1. <span data-ttu-id="9f550-132">**특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-132">click **Add attribute**.</span></span> <span data-ttu-id="9f550-133">**이름**을 입력하고 드롭다운에서 **값**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-133">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="9f550-134">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-134">Click **Save.**</span></span> <span data-ttu-id="9f550-135">테이블에 새 특성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-135">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="9f550-136">응용 프로그램의 Single Sign-On을 구성하는 방법에 관한 문서에 액세스하려면 **&lt;응용 프로그램 이름&gt; 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-136">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="9f550-137">또한 응용 프로그램에 필요한 Azure AD URL과 인증서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-137">Also, you has Azure AD URLs and certificate required for the application.</span></span>

15. [<span data-ttu-id="9f550-138">응용 프로그램에 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-138">Assign users to the application.</span></span>](#assign-users-to-the-application)

## <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="9f550-139">사용자 식별자를 선택하고 응용 프로그램에 보낼 사용자 특성 추가</span><span class="sxs-lookup"><span data-stu-id="9f550-139">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="9f550-140">사용자 식별자를 선택하거나 사용자 특성을 추가하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-140">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="9f550-141">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-141">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9f550-142">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-142">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9f550-143">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-143">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9f550-144">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-144">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9f550-145">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-145">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9f550-146">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-146">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9f550-147">Single Sign-On을 구성한 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-147">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="9f550-148">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-148">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9f550-149">**사용자 특성** 섹션 아래의 **사용자 식별자** 드롭다운에서 사용자의 고유한 식별자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-149">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="9f550-150">사용자를 인증하려면 선택한 옵션이 응용 프로그램의 예상 값과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-150">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

 ><span data-ttu-id="9f550-151">[!NOTE] Azure AD에서는 선택한 값 또는 SAML AuthRequest에서 응용 프로그램이 요청한 형식을 기반으로 NameID 특성(사용자 식별자)의 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-151">[!NOTE} Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="9f550-152">자세한 내용은 NameIDPolicy 섹션 아래의 [Single Sign-On SAML 프로토콜](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) 문서에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-152">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
 >
 >

9.  <span data-ttu-id="9f550-153">사용자 특성을 추가하려면 **다른 모든 사용자 특성 보기 및 편집**을 클릭하여 사용자가 로그인할 때 SAML 토큰을 통해 응용 프로그램으로 보낼 특성을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-153">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="9f550-154">특성을 추가하려면:</span><span class="sxs-lookup"><span data-stu-id="9f550-154">To add an attribute:</span></span>

   1. <span data-ttu-id="9f550-155">**특성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-155">click **Add attribute**.</span></span> <span data-ttu-id="9f550-156">**이름**을 입력하고 드롭다운에서 **값**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-156">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="9f550-157">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-157">Click **Save.**</span></span> <span data-ttu-id="9f550-158">테이블에 새 특성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-158">You see the new attribute in the table.</span></span>

## <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="9f550-159">Azure AD 메타데이터 또는 인증서 다운로드</span><span class="sxs-lookup"><span data-stu-id="9f550-159">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="9f550-160">Azure AD에서 응용 프로그램 메타데이터 또는 인증서를 다운로드하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-160">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="9f550-161">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-161">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9f550-162">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-162">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9f550-163">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-163">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9f550-164">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-164">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9f550-165">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-165">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="9f550-166">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-166">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9f550-167">Single Sign-On을 구성한 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-167">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="9f550-168">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-168">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9f550-169">**SAML 서명 인증서** 섹션으로 이동한 다음 **다운로드** 열 값을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-169">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="9f550-170">Single Sign-On을 구성해야 할 응용 프로그램에 따라 메타데이터 XML이나 인증서를 다운로드하는 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-170">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="9f550-171">Azure AD에서는 메타데이터를 가져오는 URL을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-171">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="9f550-172">메타데이터는 XML 파일로만 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-172">The metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-to-the-application"></a><span data-ttu-id="9f550-173">응용 프로그램에 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="9f550-173">Assign users to the application</span></span>

<span data-ttu-id="9f550-174">응용 프로그램에 하나 이상의 사용자를 직접 할당하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-174">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="9f550-175">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-175">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="9f550-176">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-176">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9f550-177">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-177">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9f550-178">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-178">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9f550-179">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-179">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9f550-180">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-180">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9f550-181">목록에서 사용자를 할당하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-181">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="9f550-182">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-182">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9f550-183">**사용자 및 그룹** 목록의 맨 위에서 **추가** 단추를 클릭하여 **할당 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-183">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="9f550-184">**할당 추가** 블레이드에서 **사용자 및 그룹** 선택기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-184">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="9f550-185">**이름 또는 전자 메일 주소로 검색** 검색 상자에 할당하려는 사용자의 **전체 이름** 또는 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-185">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="9f550-186">목록의 **사용자** 위로 마우스를 이동하여 **확인란**을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-186">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="9f550-187">사용자의 프로필 사진이나 로고 옆의 확인란을 클릭하여 사용자를 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-187">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="9f550-188">**선택 사항:** **둘 이상의 사용자를 추가**하려는 경우 **이름 또는 전자 메일 주소로 검색** 검색 상자에 다른 **전체 이름** 또는 **전자 메일 주소**를 입력하고 확인란을 클릭하여 이 사용자를 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-188">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="9f550-189">사용자 선택이 완료되면 **선택** 단추를 클릭하여 응용 프로그램에 할당되도록 사용자 및 그룹의 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-189">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="9f550-190">**선택 사항:** **할당 추가** 블레이드에서 **역할 선택** 선택기를 클릭하여 선택한 사용자에게 할당할 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-190">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="9f550-191">**할당** 단추를 클릭하여 선택한 사용자에게 응용 프로그램을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-191">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="9f550-192">잠시 후 선택한 사용자는 솔루션 설명 섹션에 설명된 메서드를 사용하여 이러한 응용 프로그램을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f550-192">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="9f550-193">응용 프로그램에 보낸 SAML 클레임 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="9f550-193">Customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="9f550-194">응용 프로그램에 전송된 SAML 특성 클레임을 사용자 지정하는 방법을 알아보려면 [Azure Active Directory의 클레임 매핑](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f550-194">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f550-195">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9f550-195">Next steps</span></span>
[<span data-ttu-id="9f550-196">응용 프로그램 프록시를 사용하여 앱에 Single Sign-On 제공</span><span class="sxs-lookup"><span data-stu-id="9f550-196">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
