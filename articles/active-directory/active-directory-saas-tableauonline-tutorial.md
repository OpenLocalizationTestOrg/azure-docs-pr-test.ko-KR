---
title: "Tableau Online와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Tableau Online 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 443fab1198a91a4d5749e6421f7b8603fc75a81e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a><span data-ttu-id="09755-103">Tableau Online와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="09755-103">Tutorial: Azure Active Directory integration with Tableau Online</span></span>

<span data-ttu-id="09755-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Tableau Online을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="09755-104">In this tutorial, you learn how to integrate Tableau Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="09755-105">Tableau Server를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="09755-105">Integrating Tableau Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="09755-106">Tableau Online에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09755-106">You can control in Azure AD who has access to Tableau Online</span></span>
- <span data-ttu-id="09755-107">사용자가 해당 Azure AD 계정으로 Tableau Online에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09755-107">You can enable your users to automatically get signed-on to Tableau Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="09755-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09755-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="09755-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09755-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09755-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="09755-110">Prerequisites</span></span>

<span data-ttu-id="09755-111">Tableau Online과의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-111">To configure Azure AD integration with Tableau Online, you need the following items:</span></span>

- <span data-ttu-id="09755-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="09755-112">An Azure AD subscription</span></span>
- <span data-ttu-id="09755-113">Tableau Online Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="09755-113">A Tableau Online single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="09755-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="09755-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="09755-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="09755-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="09755-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="09755-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09755-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="09755-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="09755-118">Scenario description</span></span>
<span data-ttu-id="09755-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="09755-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09755-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="09755-121">갤러리에서 Tableau Online 추가</span><span class="sxs-lookup"><span data-stu-id="09755-121">Adding Tableau Online from the gallery</span></span>
2. <span data-ttu-id="09755-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="09755-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-online-from-the-gallery"></a><span data-ttu-id="09755-123">갤러리에서 Tableau Online 추가</span><span class="sxs-lookup"><span data-stu-id="09755-123">Adding Tableau Online from the gallery</span></span>
<span data-ttu-id="09755-124">Tableau Online의 Azure AD 통합을 구성하려면 갤러리의 Tableau Online을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-124">To configure the integration of Tableau Online into Azure AD, you need to add Tableau Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="09755-125">**갤러리에서 Tableau Online을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="09755-125">**To add Tableau Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="09755-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="09755-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="09755-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="09755-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="09755-133">검색 상자에 **Tableau Online**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-133">In the search box, type **Tableau Online**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. <span data-ttu-id="09755-135">결과 창에서 **Tableau Online**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-135">In the results panel, select **Tableau Online**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="09755-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="09755-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="09755-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Tableau Online에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-138">In this section, you configure and test Azure AD single sign-on with Tableau Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="09755-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Tableau Online 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tableau Online is to a user in Azure AD.</span></span> <span data-ttu-id="09755-140">즉, Azure AD 사용자와 Tableau Online의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-140">In other words, a link relationship between an Azure AD user and the related user in Tableau Online needs to be established.</span></span>

<span data-ttu-id="09755-141">Tableau Online에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 연결 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-141">In Tableau Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="09755-142">Tableau Online에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-142">To configure and test Azure AD single sign-on with Tableau Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="09755-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="09755-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="09755-145">**[Tableau Online 테스트 사용자 만들기](#creating-a-tableau-online-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Tableau Online에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09755-145">**[Creating a Tableau Online test user](#creating-a-tableau-online-test-user)** - to have a counterpart of Britta Simon in Tableau Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="09755-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="09755-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="09755-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="09755-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="09755-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Tableau Online 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tableau Online application.</span></span>

<span data-ttu-id="09755-150">**Tableau Online에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="09755-150">**To configure Azure AD single sign-on with Tableau Online, perform the following steps:**</span></span>

1. <span data-ttu-id="09755-151">Azure Portal의 **Tableau Online** 응용 프로그램 통합 페이지에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-151">In the Azure portal, on the **Tableau Online** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="09755-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. <span data-ttu-id="09755-155">**Tableau Online 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-155">On the **Tableau Online Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    <span data-ttu-id="09755-157">a.</span><span class="sxs-lookup"><span data-stu-id="09755-157">a.</span></span> <span data-ttu-id="09755-158">**로그온 URL** 텍스트 상자에서 URL `https://sso.online.tableau.com`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-158">In the **Sign-on URL** textbox, type the URL: `https://sso.online.tableau.com`</span></span>

    <span data-ttu-id="09755-159">b.</span><span class="sxs-lookup"><span data-stu-id="09755-159">b.</span></span> <span data-ttu-id="09755-160">**식별자** 텍스트 상자에 URL `https://sso.online.tableau.com/public/sp/<instancename>`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-160">In the **Identifier** textbox, type the URL: `https://sso.online.tableau.com/public/sp/<instancename>`</span></span>

4. <span data-ttu-id="09755-161">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. <span data-ttu-id="09755-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="09755-165">다른 브라우저 창에서 Tableau Online 응용 프로그램에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-165">In a different browser window, sign-on to your Tableau Online application.</span></span> <span data-ttu-id="09755-166">**설정** 및 **인증**에 차례로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-166">Go to **Settings** and then **Authentication**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. <span data-ttu-id="09755-168">SAML을 사용하도록 설정하려면 **인증 유형** 섹션 아래에서</span><span class="sxs-lookup"><span data-stu-id="09755-168">To enable SAML, Under **Authentication Types** section.</span></span> <span data-ttu-id="09755-169">**SAML로 Single Sign-On** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-169">Check the **Single sign-on with SAML** checkbox.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. <span data-ttu-id="09755-171">**Tableau Online으로 메타데이터 파일 가져오기** 섹션까지 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-171">Scroll down until **Import metadata file into Tableau Online** section.</span></span>  <span data-ttu-id="09755-172">찾아보기를 클릭하여 Azure AD에서 다운로드한 메타데이터 파일을 가져오기합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-172">Click Browse and import the metadata file you have downloaded from Azure AD.</span></span> <span data-ttu-id="09755-173">그런 후 **Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-173">Then, click **Apply**.</span></span>
   
   ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. <span data-ttu-id="09755-175">**어설션 일치** 섹션에서 **이메일 주소**, **이름** 및 **성**에 대한 해당 ID 공급자 어설션 이름을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-175">In the **Match assertions** section, insert the corresponding Identity Provider assertion name for **email address**, **first name**, and **last name**.</span></span> <span data-ttu-id="09755-176">Azure Ad에서 이 정보 얻으려면</span><span class="sxs-lookup"><span data-stu-id="09755-176">To get this information from Azure AD:</span></span> 
  
    <span data-ttu-id="09755-177">a.</span><span class="sxs-lookup"><span data-stu-id="09755-177">a.</span></span> <span data-ttu-id="09755-178">Azure Portal에서 **Tableau Online** 응용 프로그램 통합 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-178">In the Azure portal, go on the **Tableau Online** application integration page.</span></span>
    
    <span data-ttu-id="09755-179">b.</span><span class="sxs-lookup"><span data-stu-id="09755-179">b.</span></span> <span data-ttu-id="09755-180">특성 섹션에서 **"기타 모든 사용자 특성 보기 및 편집"** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-180">In the attributes section, Select the **"view and edit all other user attributes"** checkbox.</span></span> 
    
   ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    <span data-ttu-id="09755-182">c.</span><span class="sxs-lookup"><span data-stu-id="09755-182">c.</span></span> <span data-ttu-id="09755-183">다음 단계에 따라 givenname, email, surname 특성의 네임스페이스 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-183">Copy the namespace value for these attributes: givenname, email and surname by using the following steps:</span></span>

   ![Azure AD Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    <span data-ttu-id="09755-185">d.</span><span class="sxs-lookup"><span data-stu-id="09755-185">d.</span></span> <span data-ttu-id="09755-186">**user.givenname** 값을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-186">Click **user.givenname** value</span></span> 
    
    <span data-ttu-id="09755-187">e.</span><span class="sxs-lookup"><span data-stu-id="09755-187">e.</span></span> <span data-ttu-id="09755-188">**네임스페이스** 텍스트 상자의 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-188">Copy the value from the **namespace** textbox.</span></span>

   ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    <span data-ttu-id="09755-190">f.</span><span class="sxs-lookup"><span data-stu-id="09755-190">f.</span></span> <span data-ttu-id="09755-191">email 및 surname에 대한 네임스페이스 값을 복사하려면 이전 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="09755-191">To copy the namesapce values for the email and surname follow the preceding steps.</span></span>

    <span data-ttu-id="09755-192">g.</span><span class="sxs-lookup"><span data-stu-id="09755-192">g.</span></span> <span data-ttu-id="09755-193">Tableau Onlin 응용 프로그램으로 전환한 후 **Tableau Online 특성** 섹션을 다음과 같이 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-193">Switch to the Tableau Online application, then set the **Tableau Online Attributes** section as follows:</span></span>
     * <span data-ttu-id="09755-194">전자 메일: **메일** 또는 **userprincipalname**</span><span class="sxs-lookup"><span data-stu-id="09755-194">Email: **mail** or **userprincipalname**</span></span>
     * <span data-ttu-id="09755-195">이름: **givenname**</span><span class="sxs-lookup"><span data-stu-id="09755-195">First name: **givenname**</span></span>
     * <span data-ttu-id="09755-196">성: **surname**</span><span class="sxs-lookup"><span data-stu-id="09755-196">Last name: **surname**</span></span>
   
   ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> <span data-ttu-id="09755-198">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09755-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="09755-199">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09755-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="09755-200">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09755-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="09755-201">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="09755-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="09755-202">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="09755-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="09755-204">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="09755-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="09755-205">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="09755-207">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="09755-209">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="09755-211">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="09755-213">a.</span><span class="sxs-lookup"><span data-stu-id="09755-213">a.</span></span> <span data-ttu-id="09755-214">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="09755-215">b.</span><span class="sxs-lookup"><span data-stu-id="09755-215">b.</span></span> <span data-ttu-id="09755-216">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="09755-217">c.</span><span class="sxs-lookup"><span data-stu-id="09755-217">c.</span></span> <span data-ttu-id="09755-218">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="09755-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="09755-219">d.</span><span class="sxs-lookup"><span data-stu-id="09755-219">d.</span></span> <span data-ttu-id="09755-220">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-220">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-online-test-user"></a><span data-ttu-id="09755-221">Tableau Online 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="09755-221">Creating a Tableau Online test user</span></span>

<span data-ttu-id="09755-222">이 섹션에서는 Tableau Online에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09755-222">In this section, you create a user called Britta Simon in Tableau Online.</span></span>

1. <span data-ttu-id="09755-223">**Tableau Online**에서 **설정**을 클릭한 후 **인증** 섹션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-223">On **Tableau Online**, click **Settings** and then **Authentication** section.</span></span> <span data-ttu-id="09755-224">**사용자 선택** 섹션으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-224">Scroll down to **Select Users** section.</span></span> <span data-ttu-id="09755-225">**사용자 추가**를 클릭하고 **이메일 주소 입력**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-225">Click **Add Users** and then **Enter Email Addresses**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. <span data-ttu-id="09755-227">**SSO(Single Sign-On) 인증에 대한 사용자 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-227">Select **Add users for single sign-on (SSO) authentication**.</span></span> <span data-ttu-id="09755-228">**전자 메일 주소 입력** 텍스트 상자에 britta.simon@contoso.com을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-228">In the **Enter Email Addresses** textbox add britta.simon@contoso.com</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. <span data-ttu-id="09755-230">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-230">Click **Create**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="09755-231">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="09755-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="09755-232">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Tableau Online에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tableau Online.</span></span>

![사용자 할당][200] 

<span data-ttu-id="09755-234">**Britta Simon을 Tableau Online에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="09755-234">**To assign Britta Simon to Tableau Online, perform the following steps:**</span></span>

1. <span data-ttu-id="09755-235">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="09755-237">응용 프로그램 목록에서 **Tableau Online**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-237">In the applications list, select **Tableau Online**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. <span data-ttu-id="09755-239">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-239">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="09755-241">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-241">Click **Add** button.</span></span> <span data-ttu-id="09755-242">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="09755-244">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="09755-245">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="09755-246">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09755-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="09755-247">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="09755-247">Testing single sign-on</span></span>

<span data-ttu-id="09755-248">이 섹션은 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="09755-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="09755-249">액세스 패널에서 Tableau Online 타일을 클릭하면 Tableau Online 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="09755-249">When you click the Tableau Online tile in the Access Panel, you should get automatically signed-on to your Tableau Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="09755-250">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="09755-250">Additional resources</span></span>

* [<span data-ttu-id="09755-251">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="09755-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="09755-252">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="09755-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

