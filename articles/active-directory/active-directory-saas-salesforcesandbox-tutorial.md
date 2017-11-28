---
title: "자습서: Salesforce Sandbox와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Salesforce 샌드박스 간의 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7539f08356568a17ebfcee2764bbbefa129b0553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="59952-103">자습서: Salesforce Sandbox와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="59952-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="59952-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 Salesforce 샌드박스 합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-104">In this tutorial, you learn how toointegrate Salesforce Sandbox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="59952-105">Azure AD와 Salesforce Sandbox 통합 hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-105">Integrating Salesforce Sandbox with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="59952-106">Azure ad 액세스 tooSalesforce 샌드박스를 가진 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59952-106">You can control in Azure AD who has access tooSalesforce Sandbox</span></span>
- <span data-ttu-id="59952-107">에 사용자가 tooautomatically get 로그온 tooSalesforce (Single Sign-on) 샌드박스 자신의 Azure AD 계정으로 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59952-107">You can enable your users tooautomatically get signed-on tooSalesforce Sandbox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="59952-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59952-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="59952-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59952-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="59952-110">Prerequisites</span></span>

<span data-ttu-id="59952-111">Azure AD 및 Salesforce Sandbox 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-111">tooconfigure Azure AD integration with Salesforce Sandbox, you need hello following items:</span></span>

- <span data-ttu-id="59952-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="59952-112">An Azure AD subscription</span></span>
- <span data-ttu-id="59952-113">Salesforce Sandbox Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="59952-113">A Salesforce Sandbox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="59952-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="59952-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="59952-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="59952-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="59952-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59952-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="59952-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="59952-118">Scenario description</span></span>
<span data-ttu-id="59952-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="59952-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59952-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="59952-121">Salesforce Sandbox hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="59952-121">Adding Salesforce Sandbox from hello gallery</span></span>
2. <span data-ttu-id="59952-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="59952-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-sandbox-from-hello-gallery"></a><span data-ttu-id="59952-123">Salesforce Sandbox hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="59952-123">Adding Salesforce Sandbox from hello gallery</span></span>
<span data-ttu-id="59952-124">tooconfigure hello와의 통합 Salesforce Sandbox Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Salesforce Sandbox tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-124">tooconfigure hello integration of Salesforce Sandbox into Azure AD, you need tooadd Salesforce Sandbox from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="59952-125">**hello 갤러리에서 Salesforce Sandbox tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="59952-125">**tooadd Salesforce Sandbox from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="59952-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="59952-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="59952-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="59952-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="59952-131">클릭 **새 응용 프로그램** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="59952-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="59952-133">Hello 검색 상자에 입력 **Salesforce Sandbox**합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-133">In hello search box, type **Salesforce Sandbox**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. <span data-ttu-id="59952-135">Hello 결과 패널에서 선택 **Salesforce Sandbox**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="59952-135">In hello results panel, select **Salesforce Sandbox**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="59952-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="59952-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="59952-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Salesforce Sandbox에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-138">In this section, you configure and test Azure AD single sign-on with Salesforce Sandbox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="59952-139">Single sign on toowork에 대 한 Azure AD는 tooknow에 Azure AD에서 Salesforce Sandbox에 어떤 hello 테이블에 해당 사용자가 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Salesforce Sandbox is tooa user in Azure AD.</span></span> <span data-ttu-id="59952-140">즉, Azure AD 사용자 및 Salesforce Sandbox에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-140">In other words, a link relationship between an Azure AD user and hello related user in Salesforce Sandbox needs toobe established.</span></span>

<span data-ttu-id="59952-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Salesforce Sandbox에 합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Salesforce Sandbox.</span></span>

<span data-ttu-id="59952-142">tooconfigure 및 Salesforce Sandbox를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-142">tooconfigure and test Azure AD single sign-on with Salesforce Sandbox, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="59952-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="59952-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="59952-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="59952-145">**[Salesforce Sandbox 테스트 사용자 만들기](#creating-a-salesforce-sandbox-test-user)**  -toohave Britta Simon 표현인 연결 된 toohello Azure AD 사용자의 Salesforce Sandbox에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="59952-145">**[Creating a Salesforce Sandbox test user](#creating-a-salesforce-sandbox-test-user)** - toohave a counterpart of Britta Simon in Salesforce Sandbox that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="59952-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="59952-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="59952-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="59952-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="59952-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="59952-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="59952-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Salesforce 샌드박스에 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Salesforce Sandbox application.</span></span>

<span data-ttu-id="59952-150">**Azure AD tooconfigure single sign on와 Salesforce Sandbox hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="59952-150">**tooconfigure Azure AD single sign-on with Salesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="59952-151">Hello hello에 Azure 포털에서에서 **Salesforce Sandbox** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-151">In hello Azure portal, on hello **Salesforce Sandbox** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="59952-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="59952-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. <span data-ttu-id="59952-155">Hello에 **Salesforce 샌드박스 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-155">On hello **Salesforce Sandbox Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     <span data-ttu-id="59952-157">Hello에 **로그온 URL** hello 패턴을 사용 하 여 형식 hello 값 텍스트 상자:`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="59952-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<subdomain>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="59952-158">이 값은 실제 hello 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="59952-158">This value is not hello real.</span></span> <span data-ttu-id="59952-159">Hello 실제 로그온 url을이 값을 업데이트 합니다. 연락처 [Salesforce 샌드박스 클라이언트 지원 팀](https://help.salesforce.com/support) tooget이이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="59952-159">Update this value with hello actual Sign-on URL.Contact [Salesforce Sandbox Client support team](https://help.salesforce.com/support) tooget this value.</span></span>


4. <span data-ttu-id="59952-160">이미 구성한 single sign on 다른 Salesforce Sandbox 인스턴스 디렉터리의 경우 hello 구성도 해야 **식별자** toohave hello hello와 같은 값 **로그온 URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-160">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure hello **Identifier** toohave hello same value as hello **Sign on URL**.</span></span> 
    
    >[!Note]
    ><span data-ttu-id="59952-161">hello **식별자** hello를 확인 하 여 필드를 찾을 수 **고급 설정 표시** hello에 확인란 **앱 URL 구성** hello 대화 상자 페이지</span><span class="sxs-lookup"><span data-stu-id="59952-161">hello **Identifier** field can be found by checking hello **Show advanced settings** checkbox on hello **Configure App URL** page of hello dialog</span></span> 


5. <span data-ttu-id="59952-162">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-162">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. <span data-ttu-id="59952-164">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-164">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="59952-166">Hello에 **Salesforce 샌드박스 구성** 섹션에서 클릭 **Salesforce 샌드박스 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="59952-166">On hello **Salesforce Sandbox Configuration** section, click **Configure Salesforce Sandbox** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="59952-167">복사 hello **SAML Single Sign-on 서비스 URL 및 엔터티 ID가 SAML** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="59952-167">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="59952-168">![Single Sign-On 구성](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="59952-168">![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span></span>
8. <span data-ttu-id="59952-169">브라우저에서 새 탭을 열고 tooyour Salesforce Sandbox 관리자 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-169">Open a new tab in your browser and log in tooyour Salesforce Sandbox administrator account.</span></span>

9. <span data-ttu-id="59952-170">Hello 메뉴에서 hello 위에 표시를 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-170">In hello menu on hello top, click **Setup**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. <span data-ttu-id="59952-172">Hello hello 왼쪽의 탐색 창에서 클릭 **보안 제어**, 클릭 하 고 **Single Sign On 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-172">In hello navigation pane on hello left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. <span data-ttu-id="59952-174">Hello Single Sign-on 설정 섹션에서 단계를 수행 하는 hello 수행: ![구성 Single Sign-on](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span><span class="sxs-lookup"><span data-stu-id="59952-174">On hello Single Sign-On Settings section, perform hello following steps:  ![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span></span>
     
     <span data-ttu-id="59952-175">a.</span><span class="sxs-lookup"><span data-stu-id="59952-175">a.</span></span>  <span data-ttu-id="59952-176">**SAML 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-176">Select **SAML Enabled**.</span></span> 

     <span data-ttu-id="59952-177">b.</span><span class="sxs-lookup"><span data-stu-id="59952-177">b.</span></span>  <span data-ttu-id="59952-178">**새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-178">Click **New**.</span></span>

12. <span data-ttu-id="59952-179">SAML Single Sign-on 설정 섹션 hello hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-179">On hello SAML Single Sign-On Settings section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    <span data-ttu-id="59952-181">a.In hello 이름 텍스트 상자, hello 구성의 형식 hello 이름 (예:: *SPSSOWAAD\_테스트*).</span><span class="sxs-lookup"><span data-stu-id="59952-181">a.In hello Name textbox, type hello name of hello configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 

    <span data-ttu-id="59952-182">b.</span><span class="sxs-lookup"><span data-stu-id="59952-182">b.</span></span> <span data-ttu-id="59952-183">붙여넣기 **SMAL 엔터티 ID** hello에 값 **발급자** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="59952-183">Paste **SMAL Entity ID** value into hello **Issuer** textbox.</span></span>

    <span data-ttu-id="59952-184">c.</span><span class="sxs-lookup"><span data-stu-id="59952-184">c.</span></span> <span data-ttu-id="59952-185">Hello에 **엔터티 Id** 텍스트 상자에 **https://test.salesforce.com** hello 첫 번째 Salesforce Sandbox 인스턴스 tooyour 디렉터리 추가 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="59952-185">In hello **Entity Id** textbox, type **https://test.salesforce.com** if it is hello first Salesforce Sandbox instance that you are adding tooyour directory.</span></span> <span data-ttu-id="59952-186">Hello에 대 한 한 다음 Salesforce Sandbox의 인스턴스를 이미 추가한 경우 **엔터티 ID** hello에서 형식을 **로그온 URL**를이 형식에:`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="59952-186">If you have already added an instance of Salesforce Sandbox, then for hello **Entity ID** type in hello **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>  
 
    <span data-ttu-id="59952-187">d.</span><span class="sxs-lookup"><span data-stu-id="59952-187">d.</span></span> <span data-ttu-id="59952-188">클릭 **찾아보기** tooupload hello 인증서를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-188">Click **Browse** tooupload hello downloaded certificate.</span></span>  

    <span data-ttu-id="59952-189">e.</span><span class="sxs-lookup"><span data-stu-id="59952-189">e.</span></span> <span data-ttu-id="59952-190">으로 **SAML Id 유형**선택, **어설션 hello 사용자 개체에서 hello 페더레이션 ID가 포함 되어**합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-190">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>
 
    <span data-ttu-id="59952-191">f.</span><span class="sxs-lookup"><span data-stu-id="59952-191">f.</span></span> <span data-ttu-id="59952-192">으로 **SAML Id 위치**선택, **hello hello Subject 문의 NameIdentifier 요소에 Id가**합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-192">As **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>

    <span data-ttu-id="59952-193">g.</span><span class="sxs-lookup"><span data-stu-id="59952-193">g.</span></span> <span data-ttu-id="59952-194">붙여넣기 **Single Sign-on 서비스 URL** hello에 **Id 공급자 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="59952-194">Paste **Single Sign-On Service URL** into hello **Identity Provider Login URL** textbox.</span></span> 

    <span data-ttu-id="59952-195">h.</span><span class="sxs-lookup"><span data-stu-id="59952-195">h.</span></span> <span data-ttu-id="59952-196">SFDC는 SAML 로그아웃을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="59952-196">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="59952-197">문제를 해결 붙여 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' hello로 **Identity Provider Logout URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="59952-197">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="59952-198">i.</span><span class="sxs-lookup"><span data-stu-id="59952-198">i.</span></span> <span data-ttu-id="59952-199">**서비스 공급자가 시작한 요청 바인딩**에서 **HTTP Post**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-199">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 

    <span data-ttu-id="59952-200">j.</span><span class="sxs-lookup"><span data-stu-id="59952-200">j.</span></span> <span data-ttu-id="59952-201">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-201">Click **Save**.</span></span>

### <a name="enable-your-domain"></a><span data-ttu-id="59952-202">도메인 활성화</span><span class="sxs-lookup"><span data-stu-id="59952-202">Enable your domain</span></span>
<span data-ttu-id="59952-203">이 섹션에서는 이미 도메인을 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-203">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="59952-204">자세한 내용은 [도메인 이름 정의](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59952-204">For more information, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="59952-205">**tooenable 해당 도메인을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="59952-205">**tooenable your domain, perform hello following steps:**</span></span>

1. <span data-ttu-id="59952-206">Hello 왼쪽된 탐색 창에서 클릭 **도메인 관리**, 클릭 하 고 **내 도메인입니다.**</span><span class="sxs-lookup"><span data-stu-id="59952-206">In hello left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
     ![Single Sign-on 구성](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   ><span data-ttu-id="59952-208">도메인이 올바르게 구성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-208">Please make sure that your domain has been configured correctly.</span></span> 

2. <span data-ttu-id="59952-209">Hello에 **로그인 페이지 설정** 섹션에서 클릭 **편집**,으로 다음 **인증 서비스**선택, 이전 hello에서 hello SAML Single Sign-on 설정의 hello 이름 섹션을 마지막으로 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-209">In hello **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select hello name of hello SAML Single Sign-On Setting from hello previous section, and finally click **Save**.</span></span>
   
   ![Single Sign-on 구성](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

<span data-ttu-id="59952-211">구성 된 도메인이 되는 즉시 사용자가 hello 도메인 URL toologin toohello Salesforce sandbox를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-211">As soon as you have a domain configured, your users should use hello domain URL toologin toohello Salesforce sandbox.</span></span>  

<span data-ttu-id="59952-212">hello URL tooget hello 값 hello 이전 섹션에서 만든 hello SSO 프로필을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-212">tooget hello value of hello URL, click hello SSO profile you have created in hello previous section.</span></span>    

> [!TIP]
> <span data-ttu-id="59952-213">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="59952-213">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="59952-214">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="59952-214">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="59952-215">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="59952-215">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="59952-216">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="59952-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="59952-217">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="59952-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="59952-219">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="59952-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="59952-220">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="59952-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="59952-222">사용자의 toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-222">toodisplay hello list of users go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="59952-224">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="59952-224">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="59952-226">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="59952-228">a.</span><span class="sxs-lookup"><span data-stu-id="59952-228">a.</span></span> <span data-ttu-id="59952-229">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="59952-230">b.</span><span class="sxs-lookup"><span data-stu-id="59952-230">b.</span></span> <span data-ttu-id="59952-231">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="59952-232">c.</span><span class="sxs-lookup"><span data-stu-id="59952-232">c.</span></span> <span data-ttu-id="59952-233">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="59952-234">d.</span><span class="sxs-lookup"><span data-stu-id="59952-234">d.</span></span> <span data-ttu-id="59952-235">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-235">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-sandbox-test-user"></a><span data-ttu-id="59952-236">Salesforce Sandbox 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="59952-236">Creating a Salesforce Sandbox test user</span></span>

<span data-ttu-id="59952-237">이 섹션에서는 Salesforce Sandbox에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59952-237">In this section, a user called Britta Simon is created in Salesforce Sandbox.</span></span> <span data-ttu-id="59952-238">Salesforce Sandbox는 기본적으로 설정되는 Just-In-Time 프로비전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-238">Salesforce Sandbox supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="59952-239">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59952-239">There is no action item for you in this section.</span></span> <span data-ttu-id="59952-240">Salesforce Sandbox에 사용자 없으면 새 tooaccess Salesforce Sandbox를 시도할 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="59952-240">If a user doesn't already exist in Salesforce Sandbox, a new one is created when you attempt tooaccess Salesforce Sandbox.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="59952-241">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="59952-242">이 섹션에서는 액세스 tooSalesforce 샌드박스를 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSalesforce Sandbox.</span></span>

![사용자 할당][200] 

<span data-ttu-id="59952-244">**tooassign Britta Simon tooSalesforce 샌드박스 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="59952-244">**tooassign Britta Simon tooSalesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="59952-245">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="59952-247">Hello 응용 프로그램 목록에서 선택 **Salesforce Sandbox**합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-247">In hello applications list, select **Salesforce Sandbox**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. <span data-ttu-id="59952-249">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="59952-251">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-251">Click **Add** button.</span></span> <span data-ttu-id="59952-252">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="59952-254">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59952-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="59952-255">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="59952-256">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="59952-257">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="59952-257">Testing single sign-on</span></span>

<span data-ttu-id="59952-258">SSO 설정 tootest 원하는 hello 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="59952-258">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="59952-259">액세스 패널 hello에 대 한 자세한 내용은 참조 하십시오. [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="59952-259">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="59952-260">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="59952-260">Additional resources</span></span>

* [<span data-ttu-id="59952-261">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="59952-261">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="59952-262">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="59952-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="59952-263">사용자 프로비저닝 구성</span><span class="sxs-lookup"><span data-stu-id="59952-263">Configure User Provisioning</span></span>](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

