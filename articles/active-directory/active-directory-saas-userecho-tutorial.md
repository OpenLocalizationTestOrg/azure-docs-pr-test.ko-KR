---
title: "자습서: UserEcho와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 UserEcho 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bedd916b-8f69-4b50-9b8d-56f4ee3bd3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2d824d8d5eb8a25db128397b908a126bd87213ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-userecho"></a><span data-ttu-id="51d1f-103">자습서: UserEcho와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="51d1f-103">Tutorial: Azure Active Directory integration with UserEcho</span></span>

<span data-ttu-id="51d1f-104">이 자습서에서는 Azure AD(Azure Active Directory)와 UserEcho를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-104">In this tutorial, you learn how to integrate UserEcho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="51d1f-105">UserEcho를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-105">Integrating UserEcho with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="51d1f-106">UserEcho에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-106">You can control in Azure AD who has access to UserEcho</span></span>
- <span data-ttu-id="51d1f-107">사용자가 해당 Azure AD 계정으로 UserEcho에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-107">You can enable your users to automatically get signed-on to UserEcho (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="51d1f-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="51d1f-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51d1f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51d1f-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="51d1f-110">Prerequisites</span></span>

<span data-ttu-id="51d1f-111">UserEcho와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-111">To configure Azure AD integration with UserEcho, you need the following items:</span></span>

- <span data-ttu-id="51d1f-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="51d1f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="51d1f-113">UserEcho Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="51d1f-113">A UserEcho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="51d1f-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="51d1f-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="51d1f-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="51d1f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="51d1f-117">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="51d1f-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="51d1f-118">Scenario description</span></span>
<span data-ttu-id="51d1f-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="51d1f-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="51d1f-121">갤러리에서 UserEcho 추가</span><span class="sxs-lookup"><span data-stu-id="51d1f-121">Adding UserEcho from the gallery</span></span>
2. <span data-ttu-id="51d1f-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="51d1f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-userecho-from-the-gallery"></a><span data-ttu-id="51d1f-123">갤러리에서 UserEcho 추가</span><span class="sxs-lookup"><span data-stu-id="51d1f-123">Adding UserEcho from the gallery</span></span>
<span data-ttu-id="51d1f-124">UserEcho의 Azure AD 통합을 구성하려면 갤러리의 UserEcho를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-124">To configure the integration of UserEcho into Azure AD, you need to add UserEcho from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="51d1f-125">**갤러리에서 UserEcho를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="51d1f-125">**To add UserEcho from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="51d1f-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="51d1f-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="51d1f-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="51d1f-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="51d1f-133">검색 상자에 **UserEcho**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-133">In the search box, type **UserEcho**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_search.png)

5. <span data-ttu-id="51d1f-135">결과 패널에서 **UserEcho**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-135">In the results panel, select **UserEcho**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="51d1f-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="51d1f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="51d1f-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 UserEcho에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-138">In this section, you configure and test Azure AD single sign-on with UserEcho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="51d1f-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 UserEcho 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in UserEcho is to a user in Azure AD.</span></span> <span data-ttu-id="51d1f-140">즉, Azure AD 사용자와 UserEcho의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-140">In other words, a link relationship between an Azure AD user and the related user in UserEcho needs to be established.</span></span>

<span data-ttu-id="51d1f-141">UserEcho에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-141">In UserEcho, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="51d1f-142">UserEcho에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-142">To configure and test Azure AD single sign-on with UserEcho, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="51d1f-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="51d1f-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="51d1f-145">**[UserEcho 테스트 사용자 만들기](#creating-a-userecho-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 UserEcho에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-145">**[Creating a UserEcho test user](#creating-a-userecho-test-user)** - to have a counterpart of Britta Simon in UserEcho that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="51d1f-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="51d1f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="51d1f-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="51d1f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="51d1f-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 UserEcho 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UserEcho application.</span></span>

<span data-ttu-id="51d1f-150">**UserEcho에서 Azure AD Single Sign-on을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="51d1f-150">**To configure Azure AD single sign-on with UserEcho, perform the following steps:**</span></span>

1. <span data-ttu-id="51d1f-151">Azure Portal의 **UserEcho** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-151">In the Azure portal, on the **UserEcho** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="51d1f-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_samlbase.png)

3. <span data-ttu-id="51d1f-155">**UserEcho 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-155">On the **UserEcho Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_url.png)

    <span data-ttu-id="51d1f-157">a.</span><span class="sxs-lookup"><span data-stu-id="51d1f-157">a.</span></span> <span data-ttu-id="51d1f-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<companyname>.userecho.com/`</span><span class="sxs-lookup"><span data-stu-id="51d1f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.userecho.com/`</span></span>

    <span data-ttu-id="51d1f-159">b.</span><span class="sxs-lookup"><span data-stu-id="51d1f-159">b.</span></span> <span data-ttu-id="51d1f-160">**식별자** 텍스트 상자에서 `https://<companyname>.userecho.com/saml/metadata/` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.userecho.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="51d1f-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-161">These values are not real.</span></span> <span data-ttu-id="51d1f-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="51d1f-163">이러한 값을 얻으려면 [UserEcho 클라이언트 지원 팀](https://feedback.userecho.com/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="51d1f-163">Contact [UserEcho Client support team](https://feedback.userecho.com/) to get these values.</span></span> 

4. <span data-ttu-id="51d1f-164">**SAML 서명 인증서** 섹션에서 **인증서(Base64)**를 클릭한 후 컴퓨터에 인증서 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_certificate.png) 

5. <span data-ttu-id="51d1f-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-userecho-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="51d1f-168">**UserEcho 구성** 섹션에서 **UserEcho 구성**을 클릭하여 **로그온 구성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-168">On the **UserEcho Configuration** section, click **Configure UserEcho** to open **Configure sign-on** window.</span></span> <span data-ttu-id="51d1f-169">**빠른 참조 섹션**에서 **로그아웃 URL 및 SAML Single Sign-On 서비스 URL**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-169">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_configure.png) 

7. <span data-ttu-id="51d1f-171">다른 웹 브라우저 창에서 UserEcho 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-171">In another browser window, sign on to your UserEcho company site as an administrator.</span></span>

8. <span data-ttu-id="51d1f-172">위쪽 도구 모음에서 메뉴를 확장하려면 사용자 이름을 클릭한 다음 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-172">In the toolbar on the top, click your user name to expand the menu, and then click **Setup**.</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png) 

9. <span data-ttu-id="51d1f-174">**통합**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-174">Click **Integrations**.</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_07.png) 

10. <span data-ttu-id="51d1f-176">**웹 사이트**를 클릭한 다음 **Single Sign-On(SAML2)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-176">Click **Website**, and then click **Single sign-on (SAML2)**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_08.png) 

11. <span data-ttu-id="51d1f-178">**Single Sign-On(SAML)** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-178">On the **Single sign-on (SAML)** page, perform the following steps:</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_09.png)
    
    <span data-ttu-id="51d1f-180">a.</span><span class="sxs-lookup"><span data-stu-id="51d1f-180">a.</span></span> <span data-ttu-id="51d1f-181">**SAML 사용**을 **예**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-181">As **SAML-enabled**, select **Yes**.</span></span>
    
    <span data-ttu-id="51d1f-182">b.</span><span class="sxs-lookup"><span data-stu-id="51d1f-182">b.</span></span> <span data-ttu-id="51d1f-183">Azure Portal에서 복사한 **SAML Single Sign-On 서비스 URL**을 **SAML SSO URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-183">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **SAML SSO URL** textbox.</span></span>
    
    <span data-ttu-id="51d1f-184">c.</span><span class="sxs-lookup"><span data-stu-id="51d1f-184">c.</span></span> <span data-ttu-id="51d1f-185">Azure Portal에서 복사한 **로그아웃 URL**을 **원격 로그아웃 URL** 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-185">Paste **Sign-Out URL**, which you have copied from the Azure portal into the **Remote logoout URL** textbox.</span></span>
    
    <span data-ttu-id="51d1f-186">d.</span><span class="sxs-lookup"><span data-stu-id="51d1f-186">d.</span></span> <span data-ttu-id="51d1f-187">다운로드한 인증서를 메모장에서 열고, 내용을 복사한 다음 전체 인증서를 **X.509 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-187">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **X.509 Certificate** textbox.</span></span>
    
    <span data-ttu-id="51d1f-188">e.</span><span class="sxs-lookup"><span data-stu-id="51d1f-188">e.</span></span> <span data-ttu-id="51d1f-189">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="51d1f-190">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="51d1f-191">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="51d1f-192">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="51d1f-193">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="51d1f-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="51d1f-194">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="51d1f-196">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="51d1f-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="51d1f-197">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-userecho-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="51d1f-199">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-userecho-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="51d1f-201">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-userecho-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="51d1f-203">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-userecho-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="51d1f-205">a.</span><span class="sxs-lookup"><span data-stu-id="51d1f-205">a.</span></span> <span data-ttu-id="51d1f-206">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="51d1f-207">b.</span><span class="sxs-lookup"><span data-stu-id="51d1f-207">b.</span></span> <span data-ttu-id="51d1f-208">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="51d1f-209">c.</span><span class="sxs-lookup"><span data-stu-id="51d1f-209">c.</span></span> <span data-ttu-id="51d1f-210">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="51d1f-211">d.</span><span class="sxs-lookup"><span data-stu-id="51d1f-211">d.</span></span> <span data-ttu-id="51d1f-212">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-212">Click **Create**.</span></span>
 
### <a name="creating-a-userecho-test-user"></a><span data-ttu-id="51d1f-213">UserEcho 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="51d1f-213">Creating a UserEcho test user</span></span>

<span data-ttu-id="51d1f-214">이 섹션은 UserEcho에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-214">The objective of this section is to create a user called Britta Simon in UserEcho.</span></span>

<span data-ttu-id="51d1f-215">**UserEcho에서 Britta Simon이라는 사용자를 만들려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="51d1f-215">**To create a user called Britta Simon in UserEcho, perform the following steps:**</span></span>

1. <span data-ttu-id="51d1f-216">UserEcho 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-216">Sign-on to your UserEcho company site as an administrator.</span></span>

2. <span data-ttu-id="51d1f-217">위쪽 도구 모음에서 메뉴를 확장하려면 사용자 이름을 클릭한 다음 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-217">In the toolbar on the top, click your user name to expand the menu, and then click **Setup**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png)

3. <span data-ttu-id="51d1f-219">**사용자**를 클릭하여 **사용자** 섹션을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-219">Click **Users**, to expand the **Users** section.</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_10.png)

4. <span data-ttu-id="51d1f-221">**사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-221">Click **Users**.</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_11.png)

5. <span data-ttu-id="51d1f-223">**새 사용자 초대**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-223">Click **Invite a new user**.</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_12.png)

6. <span data-ttu-id="51d1f-225">**새 사용자 초대** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-225">On the **Invite a new user** dialog, perform the following steps:</span></span>
   
    ![Single Sign-On 구성](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_13.png)

    <span data-ttu-id="51d1f-227">a.</span><span class="sxs-lookup"><span data-stu-id="51d1f-227">a.</span></span> <span data-ttu-id="51d1f-228">**이름** 텍스트 상자에 사용자 이름(예: Britta Simon)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-228">In the **Name** textbox, type name of the user like Britta Simon.</span></span>
    
    <span data-ttu-id="51d1f-229">b.</span><span class="sxs-lookup"><span data-stu-id="51d1f-229">b.</span></span>  <span data-ttu-id="51d1f-230">**전자 메일** 텍스트 상자에서 Brittasimon@contoso.com과 같은 사용자의 이메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-230">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="51d1f-231">c.</span><span class="sxs-lookup"><span data-stu-id="51d1f-231">c.</span></span> <span data-ttu-id="51d1f-232">**초대**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-232">Click **Invite**.</span></span>

<span data-ttu-id="51d1f-233">UserEcho를 사용하여 시작할 수 있는 초대장이 Britta에게 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-233">An invitation is sent to Britta, which enables her to start using UserEcho.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="51d1f-234">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="51d1f-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="51d1f-235">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 UserEcho에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UserEcho.</span></span>

![사용자 할당][200] 

<span data-ttu-id="51d1f-237">**Britta Simon을 UserEcho에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="51d1f-237">**To assign Britta Simon to UserEcho, perform the following steps:**</span></span>

1. <span data-ttu-id="51d1f-238">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="51d1f-240">응용 프로그램 목록에서 **UserEcho**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-240">In the applications list, select **UserEcho**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_app.png) 

3. <span data-ttu-id="51d1f-242">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-242">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="51d1f-244">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-244">Click **Add** button.</span></span> <span data-ttu-id="51d1f-245">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="51d1f-247">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="51d1f-248">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="51d1f-249">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="51d1f-250">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="51d1f-250">Testing single sign-on</span></span>

<span data-ttu-id="51d1f-251">이 섹션은 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-251">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="51d1f-252">액세스 패널에서 UserEcho 타일을 클릭하면 UserEcho 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d1f-252">When you click the UserEcho tile in the Access Panel, you should get automatically signed-on to your UserEcho application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="51d1f-253">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="51d1f-253">Additional resources</span></span>

* [<span data-ttu-id="51d1f-254">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="51d1f-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="51d1f-255">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="51d1f-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_203.png

