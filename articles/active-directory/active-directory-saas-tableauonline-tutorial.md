---
title: "Tableau Online와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Tableau Online 합니다."
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
ms.openlocfilehash: 590b2674270c340b4750c7b6feeaf4f0df4bf853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a><span data-ttu-id="4652a-103">Tableau Online와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="4652a-103">Tutorial: Azure Active Directory integration with Tableau Online</span></span>

<span data-ttu-id="4652a-104">이 자습서에 설명 어떻게 toointegrate Tableau 온라인 Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4652a-104">In this tutorial, you learn how toointegrate Tableau Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4652a-105">다음 이점을 hello로 제공 Tableau 온라인 Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="4652a-105">Integrating Tableau Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4652a-106">온라인 액세스 tooTableau을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-106">You can control in Azure AD who has access tooTableau Online</span></span>
- <span data-ttu-id="4652a-107">프로그램 사용자 tooautomatically get 로그온 tooTableau 온라인 (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-107">You can enable your users tooautomatically get signed-on tooTableau Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4652a-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4652a-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4652a-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4652a-110">Prerequisites</span></span>

<span data-ttu-id="4652a-111">Tableau 온라인와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-111">tooconfigure Azure AD integration with Tableau Online, you need hello following items:</span></span>

- <span data-ttu-id="4652a-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="4652a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4652a-113">Tableau Online Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="4652a-113">A Tableau Online single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4652a-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4652a-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4652a-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="4652a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4652a-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4652a-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="4652a-118">Scenario description</span></span>
<span data-ttu-id="4652a-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4652a-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4652a-121">Tableau 온라인 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="4652a-121">Adding Tableau Online from hello gallery</span></span>
2. <span data-ttu-id="4652a-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="4652a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-online-from-hello-gallery"></a><span data-ttu-id="4652a-123">Tableau 온라인 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="4652a-123">Adding Tableau Online from hello gallery</span></span>
<span data-ttu-id="4652a-124">tooconfigure hello와의 통합 Tableau 온라인 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Tableau 온라인 tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-124">tooconfigure hello integration of Tableau Online into Azure AD, you need tooadd Tableau Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4652a-125">**Tableau 온라인 hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4652a-125">**tooadd Tableau Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4652a-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4652a-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4652a-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="4652a-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="4652a-133">Hello 검색 상자에 입력 **Tableau 온라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-133">In hello search box, type **Tableau Online**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. <span data-ttu-id="4652a-135">Hello 결과 패널에서 선택 **Tableau 온라인**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-135">In hello results panel, select **Tableau Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4652a-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="4652a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4652a-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Tableau Online에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-138">In this section, you configure and test Azure AD single sign-on with Tableau Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4652a-139">Single sign on toowork에 대 한 Azure AD는 tooknow Tableau 온라인에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tableau Online is tooa user in Azure AD.</span></span> <span data-ttu-id="4652a-140">즉, Azure AD 사용자 및 hello Tableau 온라인의 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-140">In other words, a link relationship between an Azure AD user and hello related user in Tableau Online needs toobe established.</span></span>

<span data-ttu-id="4652a-141">Tableau 온라인에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-141">In Tableau Online, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4652a-142">tooconfigure 및 Tableau 온라인를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-142">tooconfigure and test Azure AD single sign-on with Tableau Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4652a-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4652a-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4652a-145">**[Tableau 온라인 테스트 사용자 만들기](#creating-a-tableau-online-test-user)**  -toohave Britta Simon Tableau 온라인 표현인 연결 된 toohello Azure AD의 사용자에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-145">**[Creating a Tableau Online test user](#creating-a-tableau-online-test-user)** - toohave a counterpart of Britta Simon in Tableau Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4652a-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4652a-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="4652a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4652a-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="4652a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4652a-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Tableau 온라인 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tableau Online application.</span></span>

<span data-ttu-id="4652a-150">**tooconfigure Azure AD single sign on Tableau Online과 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4652a-150">**tooconfigure Azure AD single sign-on with Tableau Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="4652a-151">Hello hello에 Azure 포털에서에서 **Tableau 온라인** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-151">In hello Azure portal, on hello **Tableau Online** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="4652a-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. <span data-ttu-id="4652a-155">Hello에 **Tableau 온라인 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-155">On hello **Tableau Online Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    <span data-ttu-id="4652a-157">a.</span><span class="sxs-lookup"><span data-stu-id="4652a-157">a.</span></span> <span data-ttu-id="4652a-158">Hello에 **로그온 URL** textbox hello URL 입력:`https://sso.online.tableau.com`</span><span class="sxs-lookup"><span data-stu-id="4652a-158">In hello **Sign-on URL** textbox, type hello URL: `https://sso.online.tableau.com`</span></span>

    <span data-ttu-id="4652a-159">b.</span><span class="sxs-lookup"><span data-stu-id="4652a-159">b.</span></span> <span data-ttu-id="4652a-160">Hello에 **식별자** textbox hello URL 입력:`https://sso.online.tableau.com/public/sp/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="4652a-160">In hello **Identifier** textbox, type hello URL: `https://sso.online.tableau.com/public/sp/<instancename>`</span></span>

4. <span data-ttu-id="4652a-161">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. <span data-ttu-id="4652a-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4652a-165">다른 브라우저 창에서 로그온 tooyour Tableau 온라인 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-165">In a different browser window, sign-on tooyour Tableau Online application.</span></span> <span data-ttu-id="4652a-166">너무 이동**설정** 차례로 **인증**합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-166">Go too**Settings** and then **Authentication**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. <span data-ttu-id="4652a-168">SAML tooenable 아래 **인증 유형을** 섹션.</span><span class="sxs-lookup"><span data-stu-id="4652a-168">tooenable SAML, Under **Authentication Types** section.</span></span> <span data-ttu-id="4652a-169">Hello 확인 **Single sign on saml** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-169">Check hello **Single sign-on with SAML** checkbox.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. <span data-ttu-id="4652a-171">**Tableau Online으로 메타데이터 파일 가져오기** 섹션까지 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-171">Scroll down until **Import metadata file into Tableau Online** section.</span></span>  <span data-ttu-id="4652a-172">찾아보기를 클릭 하 고 Azure AD에서 다운로드 한 hello 메타 데이터 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-172">Click Browse and import hello metadata file you have downloaded from Azure AD.</span></span> <span data-ttu-id="4652a-173">그런 후 **Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-173">Then, click **Apply**.</span></span>
   
   ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. <span data-ttu-id="4652a-175">Hello에 **어설션을 일치** 섹션에서 hello 해당 Id 공급자 어설션 이름에 대 한 삽입 **전자 메일 주소**, **이름**, 및 **성** .</span><span class="sxs-lookup"><span data-stu-id="4652a-175">In hello **Match assertions** section, insert hello corresponding Identity Provider assertion name for **email address**, **first name**, and **last name**.</span></span> <span data-ttu-id="4652a-176">tooget Azure AD에서이 정보:</span><span class="sxs-lookup"><span data-stu-id="4652a-176">tooget this information from Azure AD:</span></span> 
  
    <span data-ttu-id="4652a-177">a.</span><span class="sxs-lookup"><span data-stu-id="4652a-177">a.</span></span> <span data-ttu-id="4652a-178">Hello Azure 포털에서 hello에 **Tableau 온라인** 응용 프로그램 통합 페이지.</span><span class="sxs-lookup"><span data-stu-id="4652a-178">In hello Azure portal, go on hello **Tableau Online** application integration page.</span></span>
    
    <span data-ttu-id="4652a-179">b.</span><span class="sxs-lookup"><span data-stu-id="4652a-179">b.</span></span> <span data-ttu-id="4652a-180">Hello 특성 섹션에서 선택 hello **"보기 및 다른 모든 사용자 속성을 편집할"** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-180">In hello attributes section, Select hello **"view and edit all other user attributes"** checkbox.</span></span> 
    
   ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    <span data-ttu-id="4652a-182">c.</span><span class="sxs-lookup"><span data-stu-id="4652a-182">c.</span></span> <span data-ttu-id="4652a-183">이러한 특성에 대 한 hello 네임 스페이스 값을 복사: givenname, 전자 메일 및 surname를 사용 하 여 다음 단계 hello:</span><span class="sxs-lookup"><span data-stu-id="4652a-183">Copy hello namespace value for these attributes: givenname, email and surname by using hello following steps:</span></span>

   ![Azure AD Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    <span data-ttu-id="4652a-185">d.</span><span class="sxs-lookup"><span data-stu-id="4652a-185">d.</span></span> <span data-ttu-id="4652a-186">**user.givenname** 값을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-186">Click **user.givenname** value</span></span> 
    
    <span data-ttu-id="4652a-187">e.</span><span class="sxs-lookup"><span data-stu-id="4652a-187">e.</span></span> <span data-ttu-id="4652a-188">Hello에서 hello 값 복사 **네임 스페이스** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-188">Copy hello value from hello **namespace** textbox.</span></span>

   ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    <span data-ttu-id="4652a-190">f.</span><span class="sxs-lookup"><span data-stu-id="4652a-190">f.</span></span> <span data-ttu-id="4652a-191">hello 전자 메일 및 surname toocopy hello 네임 스페이스 값 hello 이전 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-191">toocopy hello namesapce values for hello email and surname follow hello preceding steps.</span></span>

    <span data-ttu-id="4652a-192">g.</span><span class="sxs-lookup"><span data-stu-id="4652a-192">g.</span></span> <span data-ttu-id="4652a-193">Toohello Tableau 온라인 응용 프로그램 전환 다음 hello 설정 **Tableau 온라인 특성** 다음과 같은 섹션:</span><span class="sxs-lookup"><span data-stu-id="4652a-193">Switch toohello Tableau Online application, then set hello **Tableau Online Attributes** section as follows:</span></span>
     * <span data-ttu-id="4652a-194">전자 메일: **메일** 또는 **userprincipalname**</span><span class="sxs-lookup"><span data-stu-id="4652a-194">Email: **mail** or **userprincipalname**</span></span>
     * <span data-ttu-id="4652a-195">이름: **givenname**</span><span class="sxs-lookup"><span data-stu-id="4652a-195">First name: **givenname**</span></span>
     * <span data-ttu-id="4652a-196">성: **surname**</span><span class="sxs-lookup"><span data-stu-id="4652a-196">Last name: **surname**</span></span>
   
   ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> <span data-ttu-id="4652a-198">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="4652a-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4652a-199">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="4652a-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4652a-200">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4652a-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4652a-201">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="4652a-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="4652a-202">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="4652a-204">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4652a-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4652a-205">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4652a-207">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4652a-209">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4652a-211">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4652a-213">a.</span><span class="sxs-lookup"><span data-stu-id="4652a-213">a.</span></span> <span data-ttu-id="4652a-214">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4652a-215">b.</span><span class="sxs-lookup"><span data-stu-id="4652a-215">b.</span></span> <span data-ttu-id="4652a-216">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4652a-217">c.</span><span class="sxs-lookup"><span data-stu-id="4652a-217">c.</span></span> <span data-ttu-id="4652a-218">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4652a-219">d.</span><span class="sxs-lookup"><span data-stu-id="4652a-219">d.</span></span> <span data-ttu-id="4652a-220">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-220">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-online-test-user"></a><span data-ttu-id="4652a-221">Tableau Online 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="4652a-221">Creating a Tableau Online test user</span></span>

<span data-ttu-id="4652a-222">이 섹션에서는 Tableau Online에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-222">In this section, you create a user called Britta Simon in Tableau Online.</span></span>

1. <span data-ttu-id="4652a-223">**Tableau Online**에서 **설정**을 클릭한 후 **인증** 섹션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-223">On **Tableau Online**, click **Settings** and then **Authentication** section.</span></span> <span data-ttu-id="4652a-224">너무 아래로 스크롤하여**사용자 선택** 섹션.</span><span class="sxs-lookup"><span data-stu-id="4652a-224">Scroll down too**Select Users** section.</span></span> <span data-ttu-id="4652a-225">**사용자 추가**를 클릭하고 **이메일 주소 입력**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-225">Click **Add Users** and then **Enter Email Addresses**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. <span data-ttu-id="4652a-227">**SSO(Single Sign-On) 인증에 대한 사용자 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-227">Select **Add users for single sign-on (SSO) authentication**.</span></span> <span data-ttu-id="4652a-228">Hello에 **전자 메일 주소 입력** textbox 추가britta.simon@contoso.com</span><span class="sxs-lookup"><span data-stu-id="4652a-228">In hello **Enter Email Addresses** textbox add britta.simon@contoso.com</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. <span data-ttu-id="4652a-230">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-230">Click **Create**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4652a-231">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4652a-232">이 섹션에서는 액세스 tooTableau 온라인 권한을 부여 하 여 Britta Simon toouse Azure single sign on을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTableau Online.</span></span>

![사용자 할당][200] 

<span data-ttu-id="4652a-234">**tooassign Britta Simon tooTableau 온라인으로 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4652a-234">**tooassign Britta Simon tooTableau Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="4652a-235">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="4652a-237">Hello 응용 프로그램 목록에서 선택 **Tableau 온라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-237">In hello applications list, select **Tableau Online**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. <span data-ttu-id="4652a-239">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="4652a-241">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-241">Click **Add** button.</span></span> <span data-ttu-id="4652a-242">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="4652a-244">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4652a-245">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4652a-246">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4652a-247">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="4652a-247">Testing single sign-on</span></span>

<span data-ttu-id="4652a-248">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD SSO 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="4652a-249">Hello 액세스 패널에서에서 hello Tableau 온라인 타일을 클릭할 때 자동으로 로그온 tooyour Tableau 온라인 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4652a-249">When you click hello Tableau Online tile in hello Access Panel, you should get automatically signed-on tooyour Tableau Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4652a-250">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="4652a-250">Additional resources</span></span>

* [<span data-ttu-id="4652a-251">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="4652a-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4652a-252">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="4652a-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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

