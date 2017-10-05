---
title: "페더레이션된 Single Sign-On에 대해 구성된 비갤러리 응용 프로그램에 로그인하는 문제 | Microsoft Docs"
description: "Azure AD에서 SAML 기반 페더레이션된 Single Sign-On에 대해 구성된 응용 프로그램에 로그인할 때 직면할 수 있는 특정 문제에 대한 지침"
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
ms.openlocfilehash: 3afc7bca878caef424d3fa3c64aa17df0fda7de5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-a-non-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="83456-103">페더레이션된 Single Sign-On에 대해 구성된 비갤러리 응용 프로그램에 로그인하는 문제</span><span class="sxs-lookup"><span data-stu-id="83456-103">Problems signing in to a non-gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="83456-104">문제를 해결하려면 다음과 같이 Azure AD에서 응용 프로그램 구성을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-104">To troubleshoot your problem, you need to verify the application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="83456-105">Azure AD 갤러리 응용 프로그램의 모든 구성 단계를 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="83456-105">You have followed all the configuration steps for the Azure AD gallery application.</span></span>

-   <span data-ttu-id="83456-106">Azure AD에 구성된 식별자 및 회신 URL은 응용 프로그램에 있는 예상 값과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-106">The Identifier and Reply URL configured in AAD match they expected values in the application</span></span>

-   <span data-ttu-id="83456-107">응용 프로그램에 사용자를 할당했습니다.</span><span class="sxs-lookup"><span data-stu-id="83456-107">You have assigned users to the application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="83456-108">응용 프로그램을 디렉터리에서 찾을 수 없습니다</span><span class="sxs-lookup"><span data-stu-id="83456-108">Application not found in directory</span></span>

<span data-ttu-id="83456-109">*오류 AADSTS70001: ‘https://contoso.com’ 식별자를 가진 응용 프로그램이 디렉터리에 없습니다*.</span><span class="sxs-lookup"><span data-stu-id="83456-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in the directory*.</span></span>

<span data-ttu-id="83456-110">**가능한 원인**</span><span class="sxs-lookup"><span data-stu-id="83456-110">**Possible cause**</span></span>

<span data-ttu-id="83456-111">SAML 요청의 응용 프로그램에서 Azure AD로 보내진 발급자 특성은 Azure AD 응용 프로그램에서 구성된 식별자 값과 일치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="83456-111">The Issuer attribute sends from the application to Azure AD in the SAML request doesn’t match the Identifier value configured in the application Azure AD.</span></span>

<span data-ttu-id="83456-112">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="83456-112">**Resolution**</span></span>

<span data-ttu-id="83456-113">SAML 요청의 발급자 특성이 Azure AD에서 구성된 식별자 값과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-113">Ensure that the Issuer attribute in the SAML request it’s matching the Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="83456-114">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-114">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="83456-115">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="83456-115">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="83456-116">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-116">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="83456-117">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-117">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="83456-118">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="83456-118">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="83456-119">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-119">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="83456-120">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-120">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="83456-121">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-121">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="83456-122"><span id="_Hlk477190042" class="anchor"></span>**도메인 및 URL** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-122"><span id="_Hlk477190042" class="anchor"></span>Go to **Domain and URLs** section.</span></span> <span data-ttu-id="83456-123">식별자 텍스트 상자의 값이 오류 메시지에 표시되는 식별자 값과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-123">Verify that the value in the Identifier textbox is matching the value for the identifier value displayed in the error.</span></span>

<span data-ttu-id="83456-124">Azure AD에서 식별자 값을 업데이트하고 SAML 요청에서 응용 프로그램에 의해 일치하는 값이 전송된 후에 응용 프로그램에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-124">After you have updated the Identifier value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="the-reply-address-does-not-match-the-reply-addresses-configured-for-the-application"></a><span data-ttu-id="83456-125">회신 주소가 응용 프로그램에 대해 구성된 회신 주소와 일치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="83456-125">The reply address does not match the reply addresses configured for the application.</span></span> 

<span data-ttu-id="83456-126">*오류 AADSTS50011: 회신 주소 'https://contoso.com' 은 응용 프로그램에 대해 구성된 회신 주소와 일치하지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="83456-126">*Error AADSTS50011: The reply address ‘https://contoso.com’ does not match the reply addresses configured for the application*</span></span> 

<span data-ttu-id="83456-127">**가능한 원인**</span><span class="sxs-lookup"><span data-stu-id="83456-127">**Possible cause**</span></span> 

<span data-ttu-id="83456-128">SAML 요청에서 AssertionConsumerServiceURL 값은 회신 URL 값 또는 Azure AD에 구성된 패턴과 일치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="83456-128">The AssertionConsumerServiceURL value in the SAML request doesn't match the Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="83456-129">SAML 요청에서 AssertionConsumerServiceURL 값은 오류에서 확인할 수 있는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="83456-129">The AssertionConsumerServiceURL value in the SAML request is the URL you see in the error.</span></span> 

<span data-ttu-id="83456-130">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="83456-130">**Resolution**</span></span> 

<span data-ttu-id="83456-131">SAML 요청에서 AssertionConsumerServiceURL 값이 Azure AD에 구성된 회신 URL 값과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-131">Ensure that the AssertionConsumerServiceURL value in the SAML request it's matching the Reply URL value configured in Azure AD.</span></span> 
 
1.  <span data-ttu-id="83456-132">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-132">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span> 

2.  <span data-ttu-id="83456-133">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="83456-133">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span> 

3.  <span data-ttu-id="83456-134">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-134">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span> 

4.  <span data-ttu-id="83456-135">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-135">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span> 

5.  <span data-ttu-id="83456-136">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="83456-136">click **All Applications** to view a list of all your applications.</span></span> 

  * <span data-ttu-id="83456-137">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-137">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and       set the **Show** option to **All Applications.**</span></span>
  
6.  <span data-ttu-id="83456-138">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-138">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="83456-139">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-139">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="83456-140">**도메인 및 URL** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-140">Go to **Domain and URLs** section.</span></span> <span data-ttu-id="83456-141">SAML 요청에 있는 AssertionConsumerServiceURL 값과 일치하도록 회신 URL 텍스트 상자의 값을 확인하고 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-141">Verify or update the value in the Reply URL textbox to match the AssertionConsumerServiceURL value in the SAML request.</span></span>

  * <span data-ttu-id="83456-142">회신 URL 텍스트 상자에 표시되지 않으면 **고급 URL 설정 표시** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-142">If you don't see the Reply URL textbox, select the **Show advanced URL settings** checkbox.</span></span> 

<span data-ttu-id="83456-143">Azure AD에서 회신 URL 값을 업데이트하고 SAML 요청에서 응용 프로그램에 의해 일치하는 값이 전송된 후에 응용 프로그램에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-143">After you have updated the Reply URL value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="83456-144">역할이 지정되지 않은 사용자</span><span class="sxs-lookup"><span data-stu-id="83456-144">User not assigned a role</span></span>

<span data-ttu-id="83456-145">*오류 AADSTS50105: 로그인한 사용자 'brian@contoso.com'는 응용 프로그램의 역할에 할당되지 않았습니다*.</span><span class="sxs-lookup"><span data-stu-id="83456-145">*Error AADSTS50105: The signed in user 'brian@contoso.com' is not assigned to a role for the application*</span></span>

<span data-ttu-id="83456-146">**가능한 원인**</span><span class="sxs-lookup"><span data-stu-id="83456-146">**Possible cause**</span></span>

<span data-ttu-id="83456-147">사용자는 Azure AD에서 응용 프로그램에 대한 액세스 권한을 부여받지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="83456-147">The user has not been granted access to the application in Azure AD.</span></span>

<span data-ttu-id="83456-148">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="83456-148">**Resolution**</span></span>

<span data-ttu-id="83456-149">응용 프로그램에 하나 이상의 사용자를 직접 할당하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-149">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="83456-150">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-150">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="83456-151">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="83456-151">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="83456-152">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="83456-153">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-153">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="83456-154">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="83456-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="83456-155">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="83456-156">목록에서 사용자를 할당하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-156">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="83456-157">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-157">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="83456-158">**사용자 및 그룹** 목록의 맨 위에서 **추가** 단추를 클릭하여 **할당 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="83456-158">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="83456-159">**할당 추가** 블레이드에서 **사용자 및 그룹** 선택기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-159">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="83456-160">**이름 또는 전자 메일 주소로 검색** 검색 상자에 할당하려는 사용자의 **전체 이름** 또는 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-160">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="83456-161">목록의 **사용자** 위로 마우스를 이동하여 **확인란**을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-161">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="83456-162">사용자의 프로필 사진이나 로고 옆의 확인란을 클릭하여 사용자를 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-162">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="83456-163">**선택 사항:** **둘 이상의 사용자를 추가**하려는 경우 **이름 또는 전자 메일 주소로 검색** 검색 상자에 다른 **전체 이름** 또는 **전자 메일 주소**를 입력하고 확인란을 클릭하여 이 사용자를 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-163">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="83456-164">사용자 선택이 완료되면 **선택** 단추를 클릭하여 응용 프로그램에 할당되도록 사용자 및 그룹의 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-164">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="83456-165">**선택 사항:** **할당 추가** 블레이드에서 **역할 선택** 선택기를 클릭하여 선택한 사용자에게 할당할 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-165">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="83456-166">**할당** 단추를 클릭하여 선택한 사용자에게 응용 프로그램을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-166">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="83456-167">잠시 후 선택한 사용자는 솔루션 설명 섹션에 설명된 메서드를 사용하여 이러한 응용 프로그램을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83456-167">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="83456-168">유효한 SAML 요청이 아님</span><span class="sxs-lookup"><span data-stu-id="83456-168">Not a valid SAML Request</span></span>

<span data-ttu-id="83456-169">*오류 AADSTS75005: 요청이 유효한 Saml2 프로토콜 메시지가 아닙니다.*</span><span class="sxs-lookup"><span data-stu-id="83456-169">*Error AADSTS75005: The request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="83456-170">**가능한 원인**</span><span class="sxs-lookup"><span data-stu-id="83456-170">**Possible cause**</span></span>

<span data-ttu-id="83456-171">Azure AD에서는 Single Sign-On의 응용 프로그램에서 보낸 SAML 요청을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="83456-171">Azure AD doesn’t support the SAML Request sent by the application for Single Sign-on.</span></span> <span data-ttu-id="83456-172">일반적인 문제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="83456-172">Some common issues are:</span></span>

-   <span data-ttu-id="83456-173">SAML 요청에서 필수 필드 누락</span><span class="sxs-lookup"><span data-stu-id="83456-173">Missing required fields in the SAML request</span></span>

-   <span data-ttu-id="83456-174">SAML 요청 인코딩 방법</span><span class="sxs-lookup"><span data-stu-id="83456-174">SAML request encoded method</span></span>

<span data-ttu-id="83456-175">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="83456-175">**Resolution**</span></span>

1.  <span data-ttu-id="83456-176">SAML 요청을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-176">Capture SAML request.</span></span> <span data-ttu-id="83456-177">[Azure AD에서 SAML 기반 Single Sign-On 응용 프로그램을 디버깅하는 방법](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)에 대한 자습서에 따라 SAML 요청을 캡처하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="83456-177">follow the tutorial on [how to debug SAML-based single sign-on to applications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) to learn how to capture the SAML request.</span></span>

2.  <span data-ttu-id="83456-178">응용 프로그램 공급 업체와 공유에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="83456-178">Contact the application vendor and share:</span></span>

    -   <span data-ttu-id="83456-179">SAML 요청</span><span class="sxs-lookup"><span data-stu-id="83456-179">SAML request</span></span>

    -   [<span data-ttu-id="83456-180">Azure AD Single Sign-On SAML 프로토콜 요구 사항</span><span class="sxs-lookup"><span data-stu-id="83456-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="83456-181">Single Sign-On에 Azure AD SAML 구현을 지원하는지 유효성을 검사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-181">They should validate they support the Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="83456-182">requiredResourceAccess 목록에 리소스 없음</span><span class="sxs-lookup"><span data-stu-id="83456-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="83456-183">*오류 AADSTS65005: 클라이언트 응용 프로그램은 리소스 '00000002-0000-0000-c000-000000000000'에 대한 액세스 권한을 요청했습니다. 클라이언트가 해당 requiredResourceAccess 목록*에 이 리소스를 지정하지 않았기 때문에 이 요청이 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="83456-183">*Error AADSTS65005: The client application has requested access to resource '00000002-0000-0000-c000-000000000000'. This request has failed because the client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="83456-184">**가능한 원인**</span><span class="sxs-lookup"><span data-stu-id="83456-184">**Possible cause**</span></span>

<span data-ttu-id="83456-185">응용 프로그램 개체에 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83456-185">The application object is corrupted.</span></span>

<span data-ttu-id="83456-186">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="83456-186">**Resolution**</span></span>

<span data-ttu-id="83456-187">이 문제를 해결하려면 디렉터리에서 응용 프로그램을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-187">To solve the problem, remove the application from the directory.</span></span> <span data-ttu-id="83456-188">그런 다음 응용 프로그램을 추가 및 다시 구성하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-188">Then, add and reconfigure the application, follow the steps below:</span></span>

1.  <span data-ttu-id="83456-189">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-189">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="83456-190">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="83456-190">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="83456-191">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-191">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="83456-192">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-192">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="83456-193">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="83456-193">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="83456-194">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-194">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="83456-195">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-195">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="83456-196">응용 프로그램 **개요** 블레이드의 맨 왼쪽에서 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-196">Click **Delete** at the top-left of the application **Overview** blade.</span></span>

8.  <span data-ttu-id="83456-197">Azure AD를 새로 고치고 Azure AD 갤러리에서 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-197">Refresh Azure AD and Add the application from the Azure AD gallery.</span></span> <span data-ttu-id="83456-198">그런 다음 응용 프로그램을 다시 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-198">Then, Configure the application again.</span></span>

<span data-ttu-id="83456-199">응용 프로그램을 다시 구성한 후에 응용 프로그램에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83456-199">After reconfiguring the application, you should be able to sign in to the application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="83456-200">인증서 또는 키가 구성되지 않음</span><span class="sxs-lookup"><span data-stu-id="83456-200">Certificate or key not configured</span></span>

<span data-ttu-id="83456-201">오류 AADSTS50003: 서명 키가 구성되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="83456-201">Error AADSTS50003: No signing key configured.</span></span>

<span data-ttu-id="83456-202">**가능한 원인**</span><span class="sxs-lookup"><span data-stu-id="83456-202">**Possible cause**</span></span>

<span data-ttu-id="83456-203">응용 프로그램 개체가 손상되어 Azure AD에서 응용 프로그램에 대해 구성된 인증서를 인식하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-203">The application object is corrupted and Azure AD doesn’t recognize the certificate configured for the application.</span></span>

<span data-ttu-id="83456-204">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="83456-204">**Resolution**</span></span>

<span data-ttu-id="83456-205">기존 인증서를 삭제하고 새 인증서를 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-205">To delete and create a new certificate, follow the steps below:</span></span>

1.  <span data-ttu-id="83456-206">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-206">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="83456-207">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="83456-207">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="83456-208">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-208">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="83456-209">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-209">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="83456-210">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="83456-210">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="83456-211">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-211">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="83456-212">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-212">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="83456-213">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-213">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="83456-214">**SAML 서명 인증서** 섹션에서 **새 인증서 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-214">click **Create new certificate** under the **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="83456-215">[만료 날짜]를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-215">Select Expiration date.</span></span> <span data-ttu-id="83456-216">그런 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-216">Then, click **Save.**</span></span>

10. <span data-ttu-id="83456-217">**새 인증서 활성화**를 선택하여 활성 인증서를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-217">Check **Make new certificate active** to override the active certificate.</span></span> <span data-ttu-id="83456-218">그런 다음 블레이드 맨 위에 있는 **저장**을 클릭하고 롤오버 인증서를 활성화하도록 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-218">Then, click **Save** at the top of the blade and accept to activate the rollover certificate.</span></span>

11. <span data-ttu-id="83456-219">**SAML 서명 인증서** 섹션에서 **제거**를 클릭하여 **사용하지 않는** 인증서를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="83456-219">Under the **SAML Signing Certificate** section, click **remove** to remove the **Unused** certificate.</span></span>

## <a name="problem-when-customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="83456-220">응용 프로그램에 전송된 SAML 클레임을 사용자 지정할 때 발생하는 문제</span><span class="sxs-lookup"><span data-stu-id="83456-220">Problem when customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="83456-221">응용 프로그램에 전송된 SAML 특성 클레임을 사용자 지정하는 방법을 알아보려면 [Azure Active Directory의 클레임 매핑](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83456-221">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83456-222">다음 단계</span><span class="sxs-lookup"><span data-stu-id="83456-222">Next steps</span></span>
[<span data-ttu-id="83456-223">Azure AD Single Sign-On SAML 프로토콜 요구 사항</span><span class="sxs-lookup"><span data-stu-id="83456-223">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)
