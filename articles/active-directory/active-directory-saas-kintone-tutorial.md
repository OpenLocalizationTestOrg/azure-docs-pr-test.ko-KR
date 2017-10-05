---
title: "자습서: Kintone과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Kintone 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: e5e847c12cba3611ce7ea2c3e956dbd55b1e0cac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a><span data-ttu-id="98255-103">자습서: Kintone과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="98255-103">Tutorial: Azure Active Directory integration with Kintone</span></span>

<span data-ttu-id="98255-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Kintone을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="98255-104">In this tutorial, you learn how to integrate Kintone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="98255-105">Kintone을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="98255-105">Integrating Kintone with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="98255-106">Kintone에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98255-106">You can control in Azure AD who has access to Kintone</span></span>
- <span data-ttu-id="98255-107">사용자가 해당 Azure AD 계정으로 Kintone에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98255-107">You can enable your users to automatically get signed-on to Kintone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="98255-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98255-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="98255-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98255-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98255-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="98255-110">Prerequisites</span></span>

<span data-ttu-id="98255-111">Kintone과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-111">To configure Azure AD integration with Kintone, you need the following items:</span></span>

- <span data-ttu-id="98255-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="98255-112">An Azure AD subscription</span></span>
- <span data-ttu-id="98255-113">Kintone Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="98255-113">A Kintone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="98255-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98255-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="98255-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="98255-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="98255-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="98255-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98255-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="98255-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="98255-118">Scenario description</span></span>
<span data-ttu-id="98255-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="98255-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98255-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="98255-121">갤러리에서 Kintone 추가</span><span class="sxs-lookup"><span data-stu-id="98255-121">Adding Kintone from the gallery</span></span>
2. <span data-ttu-id="98255-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="98255-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kintone-from-the-gallery"></a><span data-ttu-id="98255-123">갤러리에서 Kintone 추가</span><span class="sxs-lookup"><span data-stu-id="98255-123">Adding Kintone from the gallery</span></span>
<span data-ttu-id="98255-124">Kintone의 Azure AD 통합을 구성하려면 갤러리의 Kintone을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-124">To configure the integration of Kintone into Azure AD, you need to add Kintone from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="98255-125">**갤러리에서 Kintone을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="98255-125">**To add Kintone from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="98255-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="98255-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="98255-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="98255-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="98255-133">검색 상자에 **Kintone**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-133">In the search box, type **Kintone**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_search.png)

5. <span data-ttu-id="98255-135">결과 패널에서 **Kintone**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-135">In the results panel, select **Kintone**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="98255-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="98255-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="98255-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Kintone에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-138">In this section, you configure and test Azure AD single sign-on with Kintone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="98255-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Kintone 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kintone is to a user in Azure AD.</span></span> <span data-ttu-id="98255-140">즉, Azure AD 사용자와 Kintone의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-140">In other words, a link relationship between an Azure AD user and the related user in Kintone needs to be established.</span></span>

<span data-ttu-id="98255-141">Kintone에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-141">In Kintone, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="98255-142">Kintone에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-142">To configure and test Azure AD single sign-on with Kintone, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="98255-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="98255-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="98255-145">**[Kintone 테스트 사용자 만들기](#creating-a-kintone-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Kintone에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98255-145">**[Creating a Kintone test user](#creating-a-kintone-test-user)** - to have a counterpart of Britta Simon in Kintone that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="98255-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="98255-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="98255-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="98255-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="98255-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Kintone 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kintone application.</span></span>

<span data-ttu-id="98255-150">**Kintone에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="98255-150">**To configure Azure AD single sign-on with Kintone, perform the following steps:**</span></span>

1. <span data-ttu-id="98255-151">Azure Portal의 **Kintone** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-151">In the Azure portal, on the **Kintone** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="98255-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_samlbase.png)

3. <span data-ttu-id="98255-155">**Kintone 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-155">On the **Kintone Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_url.png)

    <span data-ttu-id="98255-157">a.</span><span class="sxs-lookup"><span data-stu-id="98255-157">a.</span></span> <span data-ttu-id="98255-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<companyname>.kintone.com`</span><span class="sxs-lookup"><span data-stu-id="98255-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.kintone.com`</span></span>

    <span data-ttu-id="98255-159">b.</span><span class="sxs-lookup"><span data-stu-id="98255-159">b.</span></span> <span data-ttu-id="98255-160">**식별자** 텍스트 상자에서 다음 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.cybozu.com`|
    | `https://<companyname>.kintone.com`|

    > [!NOTE] 
    > <span data-ttu-id="98255-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="98255-161">These values are not real.</span></span> <span data-ttu-id="98255-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="98255-163">이러한 값을 얻으려면 [Kintone 클라이언트 지원 팀](https://www.kintone.com/contact/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="98255-163">Contact [Kintone Client support team](https://www.kintone.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="98255-164">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_certificate.png) 

5. <span data-ttu-id="98255-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kintone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="98255-168">**Kintone 구성** 섹션에서 **Kintone 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="98255-168">On the **Kintone Configuration** section, click **Configure Kintone** to open **Configure sign-on** window.</span></span> <span data-ttu-id="98255-169">**빠른 참조 섹션**에서 **로그아웃 URL 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_configure.png) 

7. <span data-ttu-id="98255-171">다른 웹 브라우저 창에서 **Kintone** 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-171">In a different web browser window, log into your **Kintone** company site as an administrator.</span></span>

8. <span data-ttu-id="98255-172">**설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-172">Click **Settings**.</span></span>
   
    <span data-ttu-id="98255-173">![설정](./media/active-directory-saas-kintone-tutorial/ic785879.png "설정")</span><span class="sxs-lookup"><span data-stu-id="98255-173">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

9. <span data-ttu-id="98255-174">**사용자 및 시스템 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-174">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="98255-175">![사용자 및 시스템 관리](./media/active-directory-saas-kintone-tutorial/ic785880.png "사용자 및 시스템 관리")</span><span class="sxs-lookup"><span data-stu-id="98255-175">![Users & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "Users & System Administration")</span></span>

10. <span data-ttu-id="98255-176">**시스템 관리 \> 보안**에서 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-176">Under **System Administration \> Security** click **Login**.</span></span>
   
    <span data-ttu-id="98255-177">![로그인](./media/active-directory-saas-kintone-tutorial/ic785881.png "로그인")</span><span class="sxs-lookup"><span data-stu-id="98255-177">![Login](./media/active-directory-saas-kintone-tutorial/ic785881.png "Login")</span></span>

11. <span data-ttu-id="98255-178">**SAML 인증 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-178">Click **Enable SAML authentication**.</span></span>
   
    <span data-ttu-id="98255-179">![SAML 인증](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML 인증")</span><span class="sxs-lookup"><span data-stu-id="98255-179">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML Authentication")</span></span>

12. <span data-ttu-id="98255-180">SAML Authentication 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-180">In the SAML Authentication section, perform the following steps:</span></span>
    
    <span data-ttu-id="98255-181">![SAML 인증](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML 인증")</span><span class="sxs-lookup"><span data-stu-id="98255-181">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML Authentication")</span></span>
    
    <span data-ttu-id="98255-182">a.</span><span class="sxs-lookup"><span data-stu-id="98255-182">a.</span></span> <span data-ttu-id="98255-183">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL** 값을 **로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="98255-183">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="98255-184">b.</span><span class="sxs-lookup"><span data-stu-id="98255-184">b.</span></span> <span data-ttu-id="98255-185">Azure Portal에서 복사한 **로그아웃 URL** 값을 **로그아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="98255-185">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="98255-186">c.</span><span class="sxs-lookup"><span data-stu-id="98255-186">c.</span></span> <span data-ttu-id="98255-187">다운로드한 인증서를 업로드하려면 **찾아보기** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-187">Click **Browse** to upload your downloaded certificate.</span></span>
    
    <span data-ttu-id="98255-188">d.</span><span class="sxs-lookup"><span data-stu-id="98255-188">d.</span></span> <span data-ttu-id="98255-189">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="98255-190">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98255-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="98255-191">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98255-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="98255-192">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98255-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="98255-193">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="98255-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="98255-194">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="98255-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="98255-196">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="98255-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="98255-197">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kintone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="98255-199">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kintone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="98255-201">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kintone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="98255-203">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kintone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="98255-205">a.</span><span class="sxs-lookup"><span data-stu-id="98255-205">a.</span></span> <span data-ttu-id="98255-206">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="98255-207">b.</span><span class="sxs-lookup"><span data-stu-id="98255-207">b.</span></span> <span data-ttu-id="98255-208">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="98255-209">c.</span><span class="sxs-lookup"><span data-stu-id="98255-209">c.</span></span> <span data-ttu-id="98255-210">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="98255-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="98255-211">d.</span><span class="sxs-lookup"><span data-stu-id="98255-211">d.</span></span> <span data-ttu-id="98255-212">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-212">Click **Create**.</span></span>
 
### <a name="creating-a-kintone-test-user"></a><span data-ttu-id="98255-213">Kintone 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="98255-213">Creating a Kintone test user</span></span>

<span data-ttu-id="98255-214">Azure AD 사용자가 Kintone에 로그인할 수 있도록 하려면 Kintone으로 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-214">To enable Azure AD users to log in to Kintone, they must be provisioned into Kintone.</span></span>  
<span data-ttu-id="98255-215">Kintone의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="98255-215">In the case of Kintone, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="98255-216">사용자 계정을 프로비저닝하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-216">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="98255-217">**Kintone** 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-217">Log in to your **Kintone** company site as an administrator.</span></span>

2. <span data-ttu-id="98255-218">**설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-218">Click **Setting**.</span></span>
   
    <span data-ttu-id="98255-219">![설정](./media/active-directory-saas-kintone-tutorial/ic785879.png "설정")</span><span class="sxs-lookup"><span data-stu-id="98255-219">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

3. <span data-ttu-id="98255-220">**사용자 및 시스템 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-220">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="98255-221">![사용자 및 시스템 관리](./media/active-directory-saas-kintone-tutorial/ic785880.png "사용자 및 시스템 관리")</span><span class="sxs-lookup"><span data-stu-id="98255-221">![User & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "User & System Administration")</span></span>

4. <span data-ttu-id="98255-222">**사용자 관리**에서 **부서 및 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-222">Under **User Administration**, click **Departments & Users**.</span></span>
   
    <span data-ttu-id="98255-223">![부서 및 사용자](./media/active-directory-saas-kintone-tutorial/ic785888.png "부서 및 사용자")</span><span class="sxs-lookup"><span data-stu-id="98255-223">![Department & Users](./media/active-directory-saas-kintone-tutorial/ic785888.png "Department & Users")</span></span>

5. <span data-ttu-id="98255-224">**새 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-224">Click **New User**.</span></span>
   
    <span data-ttu-id="98255-225">![새 사용자](./media/active-directory-saas-kintone-tutorial/ic785889.png "새 사용자")</span><span class="sxs-lookup"><span data-stu-id="98255-225">![New Users](./media/active-directory-saas-kintone-tutorial/ic785889.png "New Users")</span></span>

6. <span data-ttu-id="98255-226">**새 사용자** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-226">In the **New User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="98255-227">![새 사용자](./media/active-directory-saas-kintone-tutorial/ic785890.png "새 사용자")</span><span class="sxs-lookup"><span data-stu-id="98255-227">![New Users](./media/active-directory-saas-kintone-tutorial/ic785890.png "New Users")</span></span>
   
    <span data-ttu-id="98255-228">a.</span><span class="sxs-lookup"><span data-stu-id="98255-228">a.</span></span> <span data-ttu-id="98255-229">프로비전할 유효한 AAD 계정의 **표시 이름**, **로그인 이름**, **새 암호**, **암호 확인**, **이메일 주소** 및 세부 정보를 관련 텍스트 상자에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-229">Type a **Display Name**, **Login Name**, **New Password**, **Confirm Password**, **E-mail Address**, and other details of a valid AAD account you want to provision into the related textboxes.</span></span>
 
    <span data-ttu-id="98255-230">b.</span><span class="sxs-lookup"><span data-stu-id="98255-230">b.</span></span> <span data-ttu-id="98255-231">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-231">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="98255-232">다른 Kintone 사용자 계정 생성 도구 또는 Kintone가 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98255-232">You can use any other Kintone user account creation tools or APIs provided by Kintone to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="98255-233">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="98255-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="98255-234">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Kintone에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kintone.</span></span>

![사용자 할당][200] 

<span data-ttu-id="98255-236">**Britta Simon을 Kintone에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="98255-236">**To assign Britta Simon to Kintone, perform the following steps:**</span></span>

1. <span data-ttu-id="98255-237">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="98255-239">응용 프로그램 목록에서 **Kintone**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-239">In the applications list, select **Kintone**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_app.png) 

3. <span data-ttu-id="98255-241">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-241">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="98255-243">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-243">Click **Add** button.</span></span> <span data-ttu-id="98255-244">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="98255-246">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="98255-247">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="98255-248">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98255-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="98255-249">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="98255-249">Testing single sign-on</span></span>

<span data-ttu-id="98255-250">이 섹션은 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="98255-250">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="98255-251">액세스 패널에서 Kintone 타일을 클릭하면 Kintone 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="98255-251">When you click the Kintone tile in the Access Panel, you should get automatically signed-on to your Kintone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="98255-252">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="98255-252">Additional resources</span></span>

* [<span data-ttu-id="98255-253">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="98255-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="98255-254">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="98255-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_203.png

