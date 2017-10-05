---
title: "자습서: UserVoice와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 UserVoice 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 684a405b-8932-46f6-b43a-4d97a42b6b87
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: fcfda1c2ecb162fb93b70574a18bd745b72ee4db
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-uservoice"></a><span data-ttu-id="d46f2-103">자습서: UserVoice와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="d46f2-103">Tutorial: Azure Active Directory integration with UserVoice</span></span>

<span data-ttu-id="d46f2-104">이 자습서에서는 Azure AD(Azure Active Directory)와 UserVoice를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-104">In this tutorial, you learn how to integrate UserVoice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d46f2-105">UserVoice를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-105">Integrating UserVoice with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d46f2-106">UserVoice에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-106">You can control in Azure AD who has access to UserVoice.</span></span>
- <span data-ttu-id="d46f2-107">사용자가 해당 Azure AD 계정으로 UserVoice에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-107">You can enable your users to automatically get signed-on to UserVoice (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d46f2-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="d46f2-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d46f2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d46f2-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d46f2-110">Prerequisites</span></span>

<span data-ttu-id="d46f2-111">UserVoice와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-111">To configure Azure AD integration with UserVoice, you need the following items:</span></span>

- <span data-ttu-id="d46f2-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="d46f2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d46f2-113">UserVoice Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="d46f2-113">A UserVoice single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d46f2-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d46f2-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d46f2-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="d46f2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d46f2-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d46f2-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="d46f2-118">Scenario description</span></span>
<span data-ttu-id="d46f2-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d46f2-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d46f2-121">갤러리에서 UserVoice 추가</span><span class="sxs-lookup"><span data-stu-id="d46f2-121">Adding UserVoice from the gallery</span></span>
2. <span data-ttu-id="d46f2-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d46f2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-uservoice-from-the-gallery"></a><span data-ttu-id="d46f2-123">갤러리에서 UserVoice 추가</span><span class="sxs-lookup"><span data-stu-id="d46f2-123">Adding UserVoice from the gallery</span></span>
<span data-ttu-id="d46f2-124">UserVoice의 Azure AD 통합을 구성하려면 갤러리의 UserVoice를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-124">To configure the integration of UserVoice into Azure AD, you need to add UserVoice from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d46f2-125">**갤러리에서 UserVoice를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d46f2-125">**To add UserVoice from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d46f2-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="d46f2-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d46f2-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="d46f2-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="d46f2-133">검색 상자에 **UserVoice**를 입력하고 결과 패널에서 **UserVoice**를 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-133">In the search box, type **UserVoice**, select **UserVoice** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d46f2-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d46f2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d46f2-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 UserVoice에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-136">In this section, you configure and test Azure AD single sign-on with UserVoice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d46f2-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 UserVoice 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in UserVoice is to a user in Azure AD.</span></span> <span data-ttu-id="d46f2-138">즉, Azure AD 사용자와 UserVoice의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-138">In other words, a link relationship between an Azure AD user and the related user in UserVoice needs to be established.</span></span>

<span data-ttu-id="d46f2-139">UserVoice에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-139">In UserVoice, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d46f2-140">UserVoice에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-140">To configure and test Azure AD single sign-on with UserVoice, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d46f2-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d46f2-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d46f2-143">**[UserVoice 테스트 사용자 만들기](#create-a-uservoice-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 UserVoice에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-143">**[Create a UserVoice test user](#create-a-uservoice-test-user)** - to have a counterpart of Britta Simon in UserVoice that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d46f2-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d46f2-145">**[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d46f2-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="d46f2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d46f2-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 UserVoice 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UserVoice application.</span></span>

<span data-ttu-id="d46f2-148">**UserVoice에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d46f2-148">**To configure Azure AD single sign-on with UserVoice, perform the following steps:**</span></span>

1. <span data-ttu-id="d46f2-149">Azure Portal의 **UserVoice** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-149">In the Azure portal, on the **UserVoice** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="d46f2-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_samlbase.png)

3. <span data-ttu-id="d46f2-153">**UserVoice 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-153">On the **UserVoice Domain and URLs** section, perform the following steps:</span></span>

    ![UserVoice 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_url.png)

    <span data-ttu-id="d46f2-155">a.</span><span class="sxs-lookup"><span data-stu-id="d46f2-155">a.</span></span> <span data-ttu-id="d46f2-156">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="d46f2-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    <span data-ttu-id="d46f2-157">b.</span><span class="sxs-lookup"><span data-stu-id="d46f2-157">b.</span></span> <span data-ttu-id="d46f2-158">**식별자** 텍스트 상자에서 `https://<tenantname>.UserVoice.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d46f2-159">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-159">These values are not real.</span></span> <span data-ttu-id="d46f2-160">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d46f2-161">이러한 값을 얻으려면 [UserVoice 클라이언트 지원 팀](https://www.uservoice.com/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="d46f2-161">Contact [UserVoice Client support team](https://www.uservoice.com/) to get these values.</span></span>

4. <span data-ttu-id="d46f2-162">**SAML 서명 인증서** 섹션에서 인증서의 **지문** 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-162">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_certificate.png) 

5. <span data-ttu-id="d46f2-164">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-164">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-uservoice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d46f2-166">**UserVoice 구성** 섹션에서 **UserVoice 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-166">On the **UserVoice Configuration** section, click **Configure UserVoice** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d46f2-167">**빠른 참조 섹션**에서 **로그아웃 URL 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-167">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![UserVoice 구성](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_configure.png) 

7. <span data-ttu-id="d46f2-169">다른 웹 브라우저 창에서 UserVoice 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-169">In a different web browser window, log in to your UserVoice company site as an administrator.</span></span>

8. <span data-ttu-id="d46f2-170">위쪽에 있는 도구 모음에서 **설정**을 클릭한 다음 메뉴에서 **웹 포털**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-170">In the toolbar on the top, click **Settings**, and then select **Web portal** from the menu.</span></span>
   
    <span data-ttu-id="d46f2-171">![앱 쪽의 설정 섹션](./media/active-directory-saas-uservoice-tutorial/ic777519.png "설정")</span><span class="sxs-lookup"><span data-stu-id="d46f2-171">![Settings Section On App Side](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Settings")</span></span>

9. <span data-ttu-id="d46f2-172">**웹 포털** 탭의 **사용자 인증** 섹션에서 **편집**을 클릭해 **사용자 인증 편집** 대화 상자 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-172">On the **Web portal** tab, in the **User authentication** section, click **Edit** to open the **Edit User Authentication** dialog page.</span></span>
   
    <span data-ttu-id="d46f2-173">![웹 포털 탭](./media/active-directory-saas-uservoice-tutorial/ic777520.png "웹 포털")</span><span class="sxs-lookup"><span data-stu-id="d46f2-173">![Web portal Tab](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web portal")</span></span>

10. <span data-ttu-id="d46f2-174">**사용자 인증 편집** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-174">On the **Edit User Authentication** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="d46f2-175">![사용자 인증 편집](./media/active-directory-saas-uservoice-tutorial/ic777521.png "편집 사용자 인증")</span><span class="sxs-lookup"><span data-stu-id="d46f2-175">![Edit user authentication](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Edit user authentication")</span></span>
   
    <span data-ttu-id="d46f2-176">a.</span><span class="sxs-lookup"><span data-stu-id="d46f2-176">a.</span></span> <span data-ttu-id="d46f2-177">**SSO(Single Sign-On)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-177">Click **Single Sign-On (SSO)**.</span></span>
 
    <span data-ttu-id="d46f2-178">b.</span><span class="sxs-lookup"><span data-stu-id="d46f2-178">b.</span></span> <span data-ttu-id="d46f2-179">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **SSO 원격 로그인** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-179">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **SSO Remote Sign-In** textbox.</span></span>

    <span data-ttu-id="d46f2-180">c.</span><span class="sxs-lookup"><span data-stu-id="d46f2-180">c.</span></span> <span data-ttu-id="d46f2-181">Azure Portal에서 복사한 **로그아웃 URL** 값을 **SSO 원격 로그아웃** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-181">Paste the **Sign-Out URL** value, which you have copied from the Azure portal into the **SSO Remote Sign-Out textbox**.</span></span>
 
    <span data-ttu-id="d46f2-182">d.</span><span class="sxs-lookup"><span data-stu-id="d46f2-182">d.</span></span> <span data-ttu-id="d46f2-183">Azure Portal에서 복사한 **지문** 값을 **현재 인증서 SHA1 지문** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-183">Paste the **Thumbprint** value , which you have copied from Azure portal  into the **Current certificate SHA1 fingerprint** textbox.</span></span>
    
    <span data-ttu-id="d46f2-184">e.</span><span class="sxs-lookup"><span data-stu-id="d46f2-184">e.</span></span> <span data-ttu-id="d46f2-185">**인증 설정 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-185">Click **Save authentication settings**.</span></span>

> [!TIP]
> <span data-ttu-id="d46f2-186">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d46f2-187">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d46f2-188">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d46f2-189">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d46f2-189">Create an Azure AD test user</span></span>

<span data-ttu-id="d46f2-190">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="d46f2-192">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="d46f2-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d46f2-193">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-193">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-uservoice-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="d46f2-195">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-195">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-uservoice-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="d46f2-197">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-197">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![추가 단추](./media/active-directory-saas-uservoice-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="d46f2-199">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-199">In the **User** dialog box, perform the following steps:</span></span>

    ![사용자 대화 상자](./media/active-directory-saas-uservoice-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d46f2-201">a.</span><span class="sxs-lookup"><span data-stu-id="d46f2-201">a.</span></span> <span data-ttu-id="d46f2-202">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-202">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d46f2-203">b.</span><span class="sxs-lookup"><span data-stu-id="d46f2-203">b.</span></span> <span data-ttu-id="d46f2-204">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-204">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="d46f2-205">c.</span><span class="sxs-lookup"><span data-stu-id="d46f2-205">c.</span></span> <span data-ttu-id="d46f2-206">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-206">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="d46f2-207">d.</span><span class="sxs-lookup"><span data-stu-id="d46f2-207">d.</span></span> <span data-ttu-id="d46f2-208">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-208">Click **Create**.</span></span>
 
### <a name="create-a-uservoice-test-user"></a><span data-ttu-id="d46f2-209">UserVoice 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d46f2-209">Create a UserVoice test user</span></span>

<span data-ttu-id="d46f2-210">Azure AD 사용자가 UserVoice에 로그인할 수 있도록 하려면 UserVoice로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-210">To enable Azure AD users to log in to UserVoice, they must be provisioned into UserVoice.</span></span> <span data-ttu-id="d46f2-211">UserVoice의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-211">In the case of UserVoice, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="d46f2-212">사용자 계정을 프로비저닝하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-212">To provision a user account, perform the following steps:</span></span>
1. <span data-ttu-id="d46f2-213">**UserVoice** 테넌트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-213">Log in to your **UserVoice** tenant.</span></span>

2. <span data-ttu-id="d46f2-214">**설정**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-214">Go to **Settings**.</span></span>
   
    <span data-ttu-id="d46f2-215">![설정](./media/active-directory-saas-uservoice-tutorial/ic777811.png "설정")</span><span class="sxs-lookup"><span data-stu-id="d46f2-215">![Settings](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Settings")</span></span>

3. <span data-ttu-id="d46f2-216">**일반**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-216">Click **General**.</span></span>

4. <span data-ttu-id="d46f2-217">**에이전트 및 권한**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-217">Click **Agents and permissions**.</span></span>
   
    <span data-ttu-id="d46f2-218">![에이전트 및 권한](./media/active-directory-saas-uservoice-tutorial/ic777812.png "에이전트 및 권한")</span><span class="sxs-lookup"><span data-stu-id="d46f2-218">![Agents and permissions](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agents and permissions")</span></span>

5. <span data-ttu-id="d46f2-219">**관리자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-219">Click **Add admins**.</span></span>
   
    <span data-ttu-id="d46f2-220">![관리자 추가](./media/active-directory-saas-uservoice-tutorial/ic777813.png "관리자 추가")</span><span class="sxs-lookup"><span data-stu-id="d46f2-220">![Add admins](./media/active-directory-saas-uservoice-tutorial/ic777813.png "Add admins")</span></span>

6. <span data-ttu-id="d46f2-221">**관리자 초대** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-221">On the **Invite admins** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="d46f2-222">![관리자 초대](./media/active-directory-saas-uservoice-tutorial/ic777814.png "관리자 초대")</span><span class="sxs-lookup"><span data-stu-id="d46f2-222">![Invite admins](./media/active-directory-saas-uservoice-tutorial/ic777814.png "Invite admins")</span></span>
   
    <span data-ttu-id="d46f2-223">a.</span><span class="sxs-lookup"><span data-stu-id="d46f2-223">a.</span></span> <span data-ttu-id="d46f2-224">이메일 텍스트 상자에 프로비전하려는 계정의 이메일 주소를 입력하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-224">In the Emails textbox, type the email address of the account you want to provision, and then click **Add**.</span></span>
   
    <span data-ttu-id="d46f2-225">b.</span><span class="sxs-lookup"><span data-stu-id="d46f2-225">b.</span></span> <span data-ttu-id="d46f2-226">**초대**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-226">Click **Invite**.</span></span>

> [!NOTE]
> <span data-ttu-id="d46f2-227">다른 UserVoice 사용자 계정 생성 도구 또는 UserVoice가 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-227">You can use any other UserVoice user account creation tools or APIs provided by UserVoice to provision AAD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d46f2-228">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="d46f2-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="d46f2-229">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 UserVoice에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UserVoice.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="d46f2-231">**Britta Simon을 UserVoice에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="d46f2-231">**To assign Britta Simon to UserVoice, perform the following steps:**</span></span>

1. <span data-ttu-id="d46f2-232">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="d46f2-234">응용 프로그램 목록에서 **UserVoice**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-234">In the applications list, select **UserVoice**.</span></span>

    ![응용 프로그램 목록의 UserVoice 연결](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_app.png)  

3. <span data-ttu-id="d46f2-236">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-236">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="d46f2-238">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-238">Click **Add** button.</span></span> <span data-ttu-id="d46f2-239">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="d46f2-241">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d46f2-242">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d46f2-243">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d46f2-244">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="d46f2-244">Test single sign-on</span></span>

<span data-ttu-id="d46f2-245">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d46f2-246">액세스 패널에서 UserVoice 타일을 클릭하면 UserVoice 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="d46f2-246">When you click the UserVoice tile in the Access Panel, you should get automatically signed-on to your UserVoice application.</span></span>
<span data-ttu-id="d46f2-247">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d46f2-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d46f2-248">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d46f2-248">Additional resources</span></span>

* [<span data-ttu-id="d46f2-249">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="d46f2-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d46f2-250">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d46f2-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_203.png

