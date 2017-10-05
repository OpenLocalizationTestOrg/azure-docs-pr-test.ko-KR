---
title: "자습서: Azure Active Directory와 Zoho 통합 | Microsoft Docs"
description: "Azure Active Directory와 Zoho 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: f0688cb75584ada805b944d2ef5409d66ab37339
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a><span data-ttu-id="54f2a-103">자습서: Zoho와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="54f2a-103">Tutorial: Azure Active Directory integration with Zoho</span></span>

<span data-ttu-id="54f2a-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Zoho를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-104">In this tutorial, you learn how to integrate Zoho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="54f2a-105">Zoho를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-105">Integrating Zoho with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="54f2a-106">Zoho에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-106">You can control in Azure AD who has access to Zoho.</span></span>
- <span data-ttu-id="54f2a-107">사용자가 해당 Azure AD 계정으로 Zoho에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-107">You can enable your users to automatically get signed-on to Zoho (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="54f2a-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="54f2a-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54f2a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54f2a-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="54f2a-110">Prerequisites</span></span>

<span data-ttu-id="54f2a-111">Zoho와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-111">To configure Azure AD integration with Zoho, you need the following items:</span></span>

- <span data-ttu-id="54f2a-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="54f2a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="54f2a-113">Zoho Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="54f2a-113">A Zoho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="54f2a-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="54f2a-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="54f2a-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="54f2a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="54f2a-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="54f2a-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="54f2a-118">Scenario description</span></span>
<span data-ttu-id="54f2a-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="54f2a-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="54f2a-121">갤러리에서 Zoho 추가</span><span class="sxs-lookup"><span data-stu-id="54f2a-121">Adding Zoho from the gallery</span></span>
2. <span data-ttu-id="54f2a-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="54f2a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoho-from-the-gallery"></a><span data-ttu-id="54f2a-123">갤러리에서 Zoho 추가</span><span class="sxs-lookup"><span data-stu-id="54f2a-123">Adding Zoho from the gallery</span></span>
<span data-ttu-id="54f2a-124">Zoho의 Azure AD 통합을 구성하려면 갤러리의 Zoho를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-124">To configure the integration of Zoho into Azure AD, you need to add Zoho from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="54f2a-125">**갤러리에서 Zoho를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="54f2a-125">**To add Zoho from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="54f2a-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 단추][1]

2. <span data-ttu-id="54f2a-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="54f2a-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-129">Then go to **All applications**.</span></span>

    ![엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="54f2a-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![새 응용 프로그램 단추][3]

4. <span data-ttu-id="54f2a-133">검색 상자에 **Zoho**를 입력하고 결과 패널에서 **Zoho**를 선택한 후 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-133">In the search box, type **Zoho**, select **Zoho** from result panel then click **Add** button to add the application.</span></span>

    ![결과 목록의 Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="54f2a-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="54f2a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="54f2a-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Zoho에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-136">In this section, you configure and test Azure AD single sign-on with Zoho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="54f2a-137">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Zoho 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zoho is to a user in Azure AD.</span></span> <span data-ttu-id="54f2a-138">즉, Azure AD 사용자와 Zoho의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-138">In other words, a link relationship between an Azure AD user and the related user in Zoho needs to be established.</span></span>

<span data-ttu-id="54f2a-139">Zoho에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-139">In Zoho, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="54f2a-140">Zoho에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-140">To configure and test Azure AD single sign-on with Zoho, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="54f2a-141">**[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="54f2a-142">**[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="54f2a-143">**[Zoho 테스트 사용자 만들기](#create-a-zoho-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Zoho에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-143">**[Create a Zoho test user](#create-a-zoho-test-user)** - to have a counterpart of Britta Simon in Zoho that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="54f2a-144">**[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="54f2a-145">**[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="54f2a-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="54f2a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="54f2a-147">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Zoho 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zoho application.</span></span>

<span data-ttu-id="54f2a-148">**Zoho에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="54f2a-148">**To configure Azure AD single sign-on with Zoho, perform the following steps:**</span></span>

1. <span data-ttu-id="54f2a-149">Azure Portal의 **Zoho** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-149">In the Azure portal, on the **Zoho** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="54f2a-151">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. <span data-ttu-id="54f2a-153">**Zoho 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-153">On the **Zoho Domain and URLs** section, perform the following steps:</span></span>

    ![Zoho 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    <span data-ttu-id="54f2a-155">a.</span><span class="sxs-lookup"><span data-stu-id="54f2a-155">a.</span></span> <span data-ttu-id="54f2a-156">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<company name>.zohomail.com`</span><span class="sxs-lookup"><span data-stu-id="54f2a-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.zohomail.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="54f2a-157">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-157">This value is not real.</span></span> <span data-ttu-id="54f2a-158">이 값을 실제 로그온 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-158">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="54f2a-159">이 값을 얻으려면 [Zoho 클라이언트 지원 팀](https://www.zoho.com/mail/contact.html)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="54f2a-159">Contact [Zoho Client support team](https://www.zoho.com/mail/contact.html) to get this value.</span></span> 
 
4. <span data-ttu-id="54f2a-160">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-160">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![인증서 다운로드 링크](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. <span data-ttu-id="54f2a-162">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-162">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="54f2a-164">**Zoho 구성** 섹션에서 **Zoho 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-164">On the **Zoho Configuration** section, click **Configure Zoho** to open **Configure sign-on** window.</span></span> <span data-ttu-id="54f2a-165">**빠른 참조 섹션**에서 **로그아웃 URL, 암호 변경 URL 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-165">Copy the **Sign-Out URL, Change Password URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Zoho 구성](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. <span data-ttu-id="54f2a-167">다른 웹 브라우저 창에서 관리자 권한으로 Zoho Mail 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-167">In a different web browser window, log into your Zoho Mail company site as an administrator.</span></span>

8. <span data-ttu-id="54f2a-168">**제어판**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-168">Go to the **Control panel**.</span></span>
   
    <span data-ttu-id="54f2a-169">![제어판](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "제어판")</span><span class="sxs-lookup"><span data-stu-id="54f2a-169">![Control Panel](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Control Panel")</span></span>

9. <span data-ttu-id="54f2a-170">**SAML 인증** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-170">Click the **SAML Authentication** tab.</span></span>
   
    <span data-ttu-id="54f2a-171">![SAML 인증](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML 인증")</span><span class="sxs-lookup"><span data-stu-id="54f2a-171">![SAML Authentication](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML Authentication")</span></span>

10. <span data-ttu-id="54f2a-172">**SAML 인증 세부 정보** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-172">In the **SAML Authentication Details** section, perform the following steps:</span></span>
   
    <span data-ttu-id="54f2a-173">![SAML 인증 세부 정보](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML 인증 세부 정보")</span><span class="sxs-lookup"><span data-stu-id="54f2a-173">![SAML Authentication Details](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML Authentication Details")</span></span>
   
    <span data-ttu-id="54f2a-174">a.</span><span class="sxs-lookup"><span data-stu-id="54f2a-174">a.</span></span> <span data-ttu-id="54f2a-175">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL**을 **로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-175">In the **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="54f2a-176">b.</span><span class="sxs-lookup"><span data-stu-id="54f2a-176">b.</span></span> <span data-ttu-id="54f2a-177">Azure Portal에서 복사한 **로그아웃 URL**을 **Logout Page URL**(로그아웃 페이지 URL) 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-177">In the **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="54f2a-178">c.</span><span class="sxs-lookup"><span data-stu-id="54f2a-178">c.</span></span> <span data-ttu-id="54f2a-179">Azure Portal에서 복사한 **암호 변경 URL**을 **암호 변경 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-179">In the **Change Password URL** textbox, paste **Change Password URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="54f2a-180">d.</span><span class="sxs-lookup"><span data-stu-id="54f2a-180">d.</span></span> <span data-ttu-id="54f2a-181">Azure Portal에서 다운로드한 Base-64로 인코딩된 인증서를 메모장에서 열고, 콘텐츠를 클립보드에 복사한 다음, **PublicKey** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-181">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **PublicKey** textbox.</span></span>
   
    <span data-ttu-id="54f2a-182">e.</span><span class="sxs-lookup"><span data-stu-id="54f2a-182">e.</span></span> <span data-ttu-id="54f2a-183">**알고리즘**으로 **RSA**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-183">As **Algorithm**, select **RSA**.</span></span>
   
    <span data-ttu-id="54f2a-184">f.</span><span class="sxs-lookup"><span data-stu-id="54f2a-184">f.</span></span> <span data-ttu-id="54f2a-185">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-185">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="54f2a-186">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="54f2a-187">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="54f2a-188">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="54f2a-189">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="54f2a-189">Create an Azure AD test user</span></span>

<span data-ttu-id="54f2a-190">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="54f2a-192">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="54f2a-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="54f2a-193">Azure Portal의 왼쪽 창에서 **Azure Active Directory** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-193">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 단추](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="54f2a-195">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-195">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" 및 "모든 사용자" 링크](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="54f2a-197">**사용자** 대화 상자를 열려면 **모든 사용자** 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-197">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![추가 단추](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="54f2a-199">**사용자** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-199">In the **User** dialog box, perform the following steps:</span></span>

    ![사용자 대화 상자](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    <span data-ttu-id="54f2a-201">a.</span><span class="sxs-lookup"><span data-stu-id="54f2a-201">a.</span></span> <span data-ttu-id="54f2a-202">**이름** 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-202">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="54f2a-203">b.</span><span class="sxs-lookup"><span data-stu-id="54f2a-203">b.</span></span> <span data-ttu-id="54f2a-204">**사용자 이름** 상자에 사용자인 Britta Simon의 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-204">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="54f2a-205">c.</span><span class="sxs-lookup"><span data-stu-id="54f2a-205">c.</span></span> <span data-ttu-id="54f2a-206">**암호 표시** 확인란을 선택한 다음 **암호** 상자에 표시된 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-206">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="54f2a-207">d.</span><span class="sxs-lookup"><span data-stu-id="54f2a-207">d.</span></span> <span data-ttu-id="54f2a-208">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-208">Click **Create**.</span></span>
 
### <a name="create-a-zoho-test-user"></a><span data-ttu-id="54f2a-209">Zoho 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="54f2a-209">Create a Zoho test user</span></span>

<span data-ttu-id="54f2a-210">Azure AD 사용자가 Zoho mail에 로그인할 수 있도록 하려면 사용자 계정이 Zoho mail로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-210">In order to enable Azure AD users to log into Zoho Mail, they must be provisioned into Zoho Mail.</span></span> <span data-ttu-id="54f2a-211">Zoho mail의 경우, 수동으로 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-211">In the case of Zoho Mail, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="54f2a-212">다른 Zoho Mail 사용자 계정 생성 도구 또는 Zoho Mail에서 제공하는 APIs를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-212">You can use any other Zoho Mail user account creation tools or APIs provided by Zoho Mail to provision AAD user accounts.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="54f2a-213">사용자 계정을 프로비저닝하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-213">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="54f2a-214">**Zoho Mail** 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-214">Log in to your **Zoho Mail** company site as an administrator.</span></span>

2. <span data-ttu-id="54f2a-215">**제어판 \> 메일 & 문서**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-215">Go to **Control Panel \> Mail & Docs**.</span></span>

3. <span data-ttu-id="54f2a-216">**사용자 세부 정보 \> 사용자 추가**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-216">Go to **User Details \> Add User**.</span></span>
   
    <span data-ttu-id="54f2a-217">![사용자 추가](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="54f2a-217">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Add User")</span></span>

4. <span data-ttu-id="54f2a-218">**사용자 추가** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-218">On the **Add users** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="54f2a-219">![사용자 추가](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="54f2a-219">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Add User")</span></span>
   
    <span data-ttu-id="54f2a-220">a.</span><span class="sxs-lookup"><span data-stu-id="54f2a-220">a.</span></span> <span data-ttu-id="54f2a-221">**이름** 텍스트 상자에 사용자의 이름(예: **Britta**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-221">In the **First Name** textbox, type the first name of user like **Britta**.</span></span>

    <span data-ttu-id="54f2a-222">b.</span><span class="sxs-lookup"><span data-stu-id="54f2a-222">b.</span></span> <span data-ttu-id="54f2a-223">**성** 텍스트 상자에 사용자의 성(예: **Simon**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-223">In the **Last Name** textbox, type the last name of user like **Simon**.</span></span>

    <span data-ttu-id="54f2a-224">c.</span><span class="sxs-lookup"><span data-stu-id="54f2a-224">c.</span></span> <span data-ttu-id="54f2a-225">**전자 메일 ID** 텍스트 상자에 사용자의 전자 메일 ID(예: **brittasimon@contoso.com**)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-225">In the **Email ID** textbox, type the email id of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="54f2a-226">d.</span><span class="sxs-lookup"><span data-stu-id="54f2a-226">d.</span></span> <span data-ttu-id="54f2a-227">**암호** 텍스트 상자에 사용자 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-227">In the **Password** textbox, enter password of user.</span></span>
   
    <span data-ttu-id="54f2a-228">e.</span><span class="sxs-lookup"><span data-stu-id="54f2a-228">e.</span></span> <span data-ttu-id="54f2a-229">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-229">Click **OK**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="54f2a-230">Azure Active Directory 계정 소유자는 계정 활성화 전에 계정을 확인하는 링크가 포함된 이메일을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-230">The Azure Active Directory account holder will receive an email with a link to confirm the account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="54f2a-231">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="54f2a-231">Assign the Azure AD test user</span></span>

<span data-ttu-id="54f2a-232">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Zoho에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zoho.</span></span>

![사용자 역할 할당][200] 

<span data-ttu-id="54f2a-234">**Britta Simon을 Zoho에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="54f2a-234">**To assign Britta Simon to Zoho, perform the following steps:**</span></span>

1. <span data-ttu-id="54f2a-235">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="54f2a-237">응용 프로그램 목록에서 **Zoho**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-237">In the applications list, select **Zoho**.</span></span>

    ![응용 프로그램 목록의 Zoho 연결](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. <span data-ttu-id="54f2a-239">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-239">In the menu on the left, click **Users and groups**.</span></span>

    !["사용자 및 그룹" 링크][202]

4. <span data-ttu-id="54f2a-241">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-241">Click **Add** button.</span></span> <span data-ttu-id="54f2a-242">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![할당 추가 창][203]

5. <span data-ttu-id="54f2a-244">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="54f2a-245">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="54f2a-246">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="54f2a-247">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="54f2a-247">Test single sign-on</span></span>

<span data-ttu-id="54f2a-248">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="54f2a-249">액세스 패널에서 Zoho 타일을 클릭하면 Zoho 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="54f2a-249">When you click the Zoho tile in the Access Panel, you should get automatically signed-on to your Zoho application.</span></span>
<span data-ttu-id="54f2a-250">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54f2a-250">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="54f2a-251">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="54f2a-251">Additional resources</span></span>

* [<span data-ttu-id="54f2a-252">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="54f2a-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="54f2a-253">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="54f2a-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_203.png

