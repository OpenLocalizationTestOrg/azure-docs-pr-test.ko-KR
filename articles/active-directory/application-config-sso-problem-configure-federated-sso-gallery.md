---
title: "Azure AD 갤러리 응용 프로그램에 대해 페더레이션된 Single Sign-On을 구성할 때 발생하는 문제 | Microsoft Docs"
description: "Azure AD 응용 프로그램 갤러리에 나열된 응용 프로그램의 SAML을 사용하여 페더레이션된 Single Sign-On을 구성할 때 발생하는 일반적인 문제 몇 가지를 해결"
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
ms.openlocfilehash: 290ca66048281de5e031b0404919bed84ab19ffa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="c59ba-103">Azure AD 갤러리 응용 프로그램에 대해 페더레이션된 Single Sign-On을 구성할 때 발생하는 문제</span><span class="sxs-lookup"><span data-stu-id="c59ba-103">Problem configuring federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="c59ba-104">응용 프로그램을 구성할 때 문제가 발생 할 경우.</span><span class="sxs-lookup"><span data-stu-id="c59ba-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="c59ba-105">응용 프로그램의 자습서에 있는 단계를 모두 수행했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-105">Verify you have followed all the steps in the tutorial for the application.</span></span> <span data-ttu-id="c59ba-106">응용 프로그램의 구성에는 응용 프로그램 구성 방법에 관한 인라인 설명서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-106">In the application’s configuration, you have inline documentation on how to configure the application.</span></span> <span data-ttu-id="c59ba-107">또한 [Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/)에 액세스하면 자세한 단계별 지침을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-107">Also, you can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

## <a name="cant-add-another-instance-of-the-application"></a><span data-ttu-id="c59ba-108">응용 프로그램의 다른 인스턴스를 추가할 수 없음</span><span class="sxs-lookup"><span data-stu-id="c59ba-108">Can’t add another instance of the application</span></span>

<span data-ttu-id="c59ba-109">응용 프로그램의 두 번째 인스턴스를 추가하려면 다음을 수행할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-109">To add a second instance of an application, you need to be able to:</span></span>

-   <span data-ttu-id="c59ba-110">두 번째 인스턴스에 대한 고유 식별자를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-110">Configure a unique identifier for the second instance.</span></span> <span data-ttu-id="c59ba-111">첫 번째 인스턴스에 대해 사용한 것과 동일한 식별자를 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-111">You won’t be able to configure the same identifier used for the first instance.</span></span>

-   <span data-ttu-id="c59ba-112">첫 번째 인스턴스에 대해 사용한 것과 다른 인증서를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-112">Configure a different certificate than the one used for the first instance.</span></span>

<span data-ttu-id="c59ba-113">응용 프로그램에서 위 사항 중에서 어느 것도 지원하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="c59ba-113">If the application doesn’t support any of the above.</span></span> <span data-ttu-id="c59ba-114">두 번째 인스턴스를 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-114">Then, you won’t be able to configure a second instance.</span></span>

## <a name="cant-add-the-identifier-or-the-reply-url"></a><span data-ttu-id="c59ba-115">식별자 또는 회신 URL을 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-115">Can’t add the Identifier or the Reply URL</span></span>

<span data-ttu-id="c59ba-116">식별자 또는 회신 URL을 구성할 수 없는 경우는 식별자 및 회신 URL 값이 응용 프로그램에 대해 미리 구성된 패턴과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-116">If you’re not able to configure the Identifier or the Reply URL, confirm the Identifier and Reply URL values match the patterns pre-configured for the application.</span></span>

<span data-ttu-id="c59ba-117">응용 프로그램에 대해 미리 구성된 패턴을 알려면:</span><span class="sxs-lookup"><span data-stu-id="c59ba-117">To know the patterns pre-configured for the application:</span></span>

1.  <span data-ttu-id="c59ba-118">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span> <span data-ttu-id="c59ba-119">7단계로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-119">Go to step 7.</span></span> <span data-ttu-id="c59ba-120">이미 Azure AD의 응용 프로그램 구성 블레이드에 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="c59ba-120">If you are already in the application configuration blade on Azure AD.</span></span>

2.  <span data-ttu-id="c59ba-121">왼쪽 주 탐색 메뉴의 맨 아래에서 **더 많은 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-121">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c59ba-122">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-122">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c59ba-123">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-123">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c59ba-124">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-124">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="c59ba-125">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-125">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="c59ba-126">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-126">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="c59ba-127">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-127">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c59ba-128">**모드** 드롭다운에서 **SAML 기반 로그온**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-128">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="c59ba-129">**도메인 및 URL 섹션** 아래의 **식별자** 또는 **회신 URL** 텍스트 상자로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-129">Go to the **Identifier** or **Reply URL** textbox, under the **Domain and URLs section.**</span></span>

10. <span data-ttu-id="c59ba-130">응용 프로그램에 대해 지원되는 패턴을 아는 방법은 세 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-130">There are three ways to know the supported patterns for the application:</span></span>

   * <span data-ttu-id="c59ba-131">텍스트 상자에서 지원되는 패턴이 자리 표시자로 표시됩니다. *예:* <https://contoso.com>.</span><span class="sxs-lookup"><span data-stu-id="c59ba-131">In the textbox, you see the supported pattern(s) as a placeholder *Example:* <https://contoso.com>.</span></span>

   * <span data-ttu-id="c59ba-132">패턴이 지원되지 않으면 텍스트 상자에 값을 입력하려 할 때 빨간색 느낌표가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-132">if the pattern is not supported, you see a red exclamation mark when you try to enter the value in the textbox.</span></span> <span data-ttu-id="c59ba-133">빨간색 느낌표 위에 마우스를 놓으면 지원되는 패턴이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-133">If you hover your mouse over the red exclamation mark, you see the supported patterns.</span></span>

   * <span data-ttu-id="c59ba-134">응용 프로그램의 자습서에서 지원되는 패턴에 대한 정보를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-134">In the tutorial for the application, you can also get information about the supported patterns.</span></span> <span data-ttu-id="c59ba-135">**Azure AD Single Sign-On 구성** 섹션 아래.</span><span class="sxs-lookup"><span data-stu-id="c59ba-135">Under the **Configure Azure AD single sign-on** section.</span></span> <span data-ttu-id="c59ba-136">**도메인 및 URL** 섹션 아래의 값 구성 단계로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-136">Go to the step for configured the values under the **Domain and URLs** section.</span></span>

<span data-ttu-id="c59ba-137">값이 Azure AD에 미리 구성된 패턴과 일치하지 않을 경우.</span><span class="sxs-lookup"><span data-stu-id="c59ba-137">If the values don’t match with the patterns pre-configured on Azure AD.</span></span> <span data-ttu-id="c59ba-138">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-138">You can:</span></span>

-   <span data-ttu-id="c59ba-139">응용 프로그램 공급업체의 도움을 받아 Azure AD에 미리 구성된 패턴과 일치하는 값을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-139">Work with the application vendor to get values that match the pattern pre-configured on Azure AD</span></span>

-   <span data-ttu-id="c59ba-140">또는 <aadapprequest@microsoft.com>으로 Azure AD 팀에 문의하거나 자습서에 응용 프로그램에서 지원되는 패턴으로 업데이트해 달라는 요청을 남길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-140">Or, you can contact Azure AD team at <aadapprequest@microsoft.com> or leave a comment in the tutorial to request the update of the supported patterns for the application</span></span>

## <a name="where-do-i-set-the-entityid-user-identifier-format"></a><span data-ttu-id="c59ba-141">EntityID(사용자 식별자) 형식을 설정하는 위치</span><span class="sxs-lookup"><span data-stu-id="c59ba-141">Where do I set the EntityID (User Identifier) format</span></span>

<span data-ttu-id="c59ba-142">사용자 인증 후에 Azure AD에서 응답을 통해 응용 프로그램으로 보내는 EntityID(사용자 식별자) 형식은 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-142">You won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="c59ba-143">Azure AD에서는 선택한 값 또는 SAML AuthRequest에서 응용 프로그램이 요청한 형식을 기반으로 NameID 특성(사용자 식별자)의 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-143">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="c59ba-144">자세한 내용은 NameIDPolicy 섹션 아래의 [Single Sign-On SAML 프로토콜](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) 문서에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-144">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy,</span></span>

## <a name="cant-find-the-azure-ad-metadata-to-complete-the-configuration-with-the-application"></a><span data-ttu-id="c59ba-145">Azure AD 메타데이터를 찾아서 응용 프로그램 구성을 완료할 수 없음</span><span class="sxs-lookup"><span data-stu-id="c59ba-145">Can’t find the Azure AD metadata to complete the configuration with the application</span></span>

<span data-ttu-id="c59ba-146">Azure AD에서 응용 프로그램 메타데이터 또는 인증서를 다운로드하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-146">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="c59ba-147">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-147">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c59ba-148">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-148">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c59ba-149">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-149">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c59ba-150">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-150">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c59ba-151">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-151">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="c59ba-152">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-152">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="c59ba-153">Single Sign-On을 구성한 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-153">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="c59ba-154">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-154">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c59ba-155">**SAML 서명 인증서** 섹션으로 이동한 다음 **다운로드** 열 값을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-155">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="c59ba-156">Single Sign-On을 구성해야 할 응용 프로그램에 따라 메타데이터 XML이나 인증서를 다운로드하는 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-156">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="c59ba-157">Azure AD에서는 메타데이터를 가져오는 URL을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-157">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="c59ba-158">메타데이터는 XML 파일로만 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c59ba-158">The metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-to-customize-saml-claims-sent-to-an-application"></a><span data-ttu-id="c59ba-159">응용 프로그램에 전송된 SAML 클레임을 사용자 지정하는 방법을 알 수 없음</span><span class="sxs-lookup"><span data-stu-id="c59ba-159">Don't know how to customize SAML claims sent to an application</span></span>

<span data-ttu-id="c59ba-160">응용 프로그램에 전송된 SAML 특성 클레임을 사용자 지정하는 방법을 알아보려면 [Azure Active Directory의 클레임 매핑](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c59ba-160">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c59ba-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c59ba-161">Next steps</span></span>
[<span data-ttu-id="c59ba-162">Azure Active Directory로 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="c59ba-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
