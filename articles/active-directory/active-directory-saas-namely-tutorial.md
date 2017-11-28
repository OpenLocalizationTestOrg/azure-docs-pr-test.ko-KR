---
title: "자습서: Namely와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory 간의 및 즉 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9541d5c4-4c82-4b5b-b01a-6a3f75a2b7a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: b0477ca6fa52a21abea7de458f8a99a01e8c25c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-namely"></a><span data-ttu-id="d8220-103">자습서: Namely와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="d8220-103">Tutorial: Azure Active Directory integration with Namely</span></span>

<span data-ttu-id="d8220-104">이 자습서에 설명 어떻게 Azure Active Directory (Azure AD)와 즉 toointegrate 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-104">In this tutorial, you learn how toointegrate Namely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d8220-105">다음 이점을 hello로 제공 즉 Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="d8220-105">Integrating Namely with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d8220-106">액세스 tooNamely을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-106">You can control in Azure AD who has access tooNamely</span></span>
- <span data-ttu-id="d8220-107">프로그램 사용자 tooautomatically get 로그온 tooNamely (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-107">You can enable your users tooautomatically get signed-on tooNamely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d8220-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d8220-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8220-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d8220-110">Prerequisites</span></span>

<span data-ttu-id="d8220-111">즉, 사용자와 Azure AD tooconfigure 통합 hello 다음 항목을 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-111">tooconfigure Azure AD integration with Namely, you need hello following items:</span></span>

- <span data-ttu-id="d8220-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="d8220-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d8220-113">Namely Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="d8220-113">A Namely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d8220-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d8220-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d8220-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="d8220-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d8220-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d8220-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="d8220-118">Scenario description</span></span>
<span data-ttu-id="d8220-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d8220-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d8220-121">즉 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="d8220-121">Adding Namely from hello gallery</span></span>
2. <span data-ttu-id="d8220-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d8220-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-namely-from-hello-gallery"></a><span data-ttu-id="d8220-123">즉 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="d8220-123">Adding Namely from hello gallery</span></span>
<span data-ttu-id="d8220-124">tooconfigure hello와의 통합 즉 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 즉 tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-124">tooconfigure hello integration of Namely into Azure AD, you need tooadd Namely from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d8220-125">**hello 갤러리에서 즉 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d8220-125">**tooadd Namely from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8220-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d8220-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d8220-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="d8220-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="d8220-133">Hello 검색 상자에 입력 **즉**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-133">In hello search box, type **Namely**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-namely-tutorial/tutorial_namely_search.png)

5. <span data-ttu-id="d8220-135">Hello 결과 패널에서 선택 **즉**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-135">In hello results panel, select **Namely**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-namely-tutorial/tutorial_namely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d8220-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d8220-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d8220-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Namely에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-138">In this section, you configure and test Azure AD single sign-on with Namely based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d8220-139">Single sign on toowork에 대 한 Azure AD는 tooknow에 Azure AD에서 즉가 tooa 사용자 어떤 hello 테이블에 해당 사용자에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Namely is tooa user in Azure AD.</span></span> <span data-ttu-id="d8220-140">즉, Azure AD 사용자 및 hello에 관련 된 사용자 간 링크 관계를 설정할 toobe 즉 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-140">In other words, a link relationship between an Azure AD user and hello related user in Namely needs toobe established.</span></span>

<span data-ttu-id="d8220-141">hello hello 값 즉, 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-141">In Namely, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d8220-142">즉, 사용자와 Azure AD에서 single sign-on 테스트 및 tooconfigure toocomplete hello 빌딩 블록을 다음 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-142">tooconfigure and test Azure AD single sign-on with Namely, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d8220-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d8220-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d8220-145">**[만들기는 즉 테스트 사용자](#creating-a-namely-test-user)**  -toohave 즉 즉 연결 된 toohello 사용자의 Azure AD 표현에서에서 Britta Simon 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-145">**[Creating a Namely test user](#creating-a-namely-test-user)** - toohave a counterpart of Britta Simon in Namely that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d8220-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d8220-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="d8220-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d8220-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="d8220-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d8220-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 프로그램 즉 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Namely application.</span></span>

<span data-ttu-id="d8220-150">**tooconfigure Azure AD single sign on으로 다시 말해 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d8220-150">**tooconfigure Azure AD single sign-on with Namely, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8220-151">Hello hello에 Azure 포털에서에서 **즉** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-151">In hello Azure portal, on hello **Namely** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="d8220-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_namely_samlbase.png)

3. <span data-ttu-id="d8220-155">Hello에 **즉 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-155">On hello **Namely Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_namely_url.png)

    <span data-ttu-id="d8220-157">a.</span><span class="sxs-lookup"><span data-stu-id="d8220-157">a.</span></span> <span data-ttu-id="d8220-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.namely.com`</span><span class="sxs-lookup"><span data-stu-id="d8220-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.namely.com`</span></span>

    <span data-ttu-id="d8220-159">b.</span><span class="sxs-lookup"><span data-stu-id="d8220-159">b.</span></span> <span data-ttu-id="d8220-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.namely.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="d8220-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.namely.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d8220-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-161">These values are not real.</span></span> <span data-ttu-id="d8220-162">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d8220-163">연락처 [즉 클라이언트 지원 팀](https://www.namely.com/contact/) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-163">Contact [Namely Client support team](https://www.namely.com/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="d8220-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_namely_certificate.png) 

5. <span data-ttu-id="d8220-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d8220-168">Hello에 **구성 즉** 섹션에서 클릭 **구성 즉** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="d8220-168">On hello **Namely Configuration** section, click **Configure Namely** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d8220-169">복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="d8220-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_namely_configure.png) 

7. <span data-ttu-id="d8220-171">다른 브라우저 창에서 로그인 tooyour 즉 회사 사이트에 관리자로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-171">In another browser window, sign on tooyour Namely company site as an administrator.</span></span>

8. <span data-ttu-id="d8220-172">도구 모음의 hello hello 위쪽에 클릭 **회사**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-172">In hello toolbar on hello top, click **Company**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_namely_06.png) 

9. <span data-ttu-id="d8220-174">Hello 클릭 **설정을** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-174">Click hello **Settings** tab.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_namely_07.png) 

10. <span data-ttu-id="d8220-176">**SAML**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-176">Click **SAML**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_namely_08.png) 

11. <span data-ttu-id="d8220-178">Hello에 **SAML 설정** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-178">On hello **SAML Settings** page, perform hello following steps:</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_namely_09.png)
 
    <span data-ttu-id="d8220-180">a.</span><span class="sxs-lookup"><span data-stu-id="d8220-180">a.</span></span> <span data-ttu-id="d8220-181">**SAML 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-181">Click **Enable SAML**.</span></span> 

    <span data-ttu-id="d8220-182">b.</span><span class="sxs-lookup"><span data-stu-id="d8220-182">b.</span></span> <span data-ttu-id="d8220-183">Hello에 **Id 공급자 SSO url** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-183">In hello **Identity provider SSO url** textbox,  paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="d8220-184">c.</span><span class="sxs-lookup"><span data-stu-id="d8220-184">c.</span></span> <span data-ttu-id="d8220-185">콘텐츠 복사 hello 메모장에서 다운로드 한 인증서를 열고 hello에 붙여 넣습니다 **Id 공급자 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-185">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **Identity provider certificate** textbox.</span></span>
     
    <span data-ttu-id="d8220-186">d.</span><span class="sxs-lookup"><span data-stu-id="d8220-186">d.</span></span> <span data-ttu-id="d8220-187">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d8220-188">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="d8220-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d8220-189">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="d8220-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d8220-190">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d8220-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d8220-191">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d8220-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="d8220-192">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="d8220-194">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d8220-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8220-195">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-namely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d8220-197">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-namely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d8220-199">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-namely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d8220-201">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-namely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d8220-203">a.</span><span class="sxs-lookup"><span data-stu-id="d8220-203">a.</span></span> <span data-ttu-id="d8220-204">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d8220-205">b.</span><span class="sxs-lookup"><span data-stu-id="d8220-205">b.</span></span> <span data-ttu-id="d8220-206">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d8220-207">c.</span><span class="sxs-lookup"><span data-stu-id="d8220-207">c.</span></span> <span data-ttu-id="d8220-208">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d8220-209">d.</span><span class="sxs-lookup"><span data-stu-id="d8220-209">d.</span></span> <span data-ttu-id="d8220-210">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-210">Click **Create**.</span></span>
 
### <a name="creating-a-namely-test-user"></a><span data-ttu-id="d8220-211">Namely 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d8220-211">Creating a Namely test user</span></span>

<span data-ttu-id="d8220-212">hello이이 섹션의 목적은 toocreate 즉 Britta Simon 호출 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-212">hello objective of this section is toocreate a user called Britta Simon in Namely.</span></span>

<span data-ttu-id="d8220-213">**즉, Britta Simon 라는 사용자를 만들면 toocreate 단계를 수행 하는 hello를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d8220-213">**toocreate a user called Britta Simon in Namely, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8220-214">즉 로그온 tooyour 관리자로 서 사이트를 회사입니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-214">Sign-on tooyour Namely company site as an administrator.</span></span>

2. <span data-ttu-id="d8220-215">도구 모음의 hello hello 위쪽에 클릭 **사람**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-215">In hello toolbar on hello top, click **People**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_namely_10.png) 

3. <span data-ttu-id="d8220-217">Hello 클릭 **디렉터리** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-217">Click hello **Directory** tab.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_namely_11.png) 

4. <span data-ttu-id="d8220-219">**새 사람 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-219">Click **Add New Person**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_namely_12.png)

5. <span data-ttu-id="d8220-221">Hello에 **새로운 사람 추가** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-221">On hello **Add New Person** dialog, perform hello following steps:</span></span>

    <span data-ttu-id="d8220-222">a.</span><span class="sxs-lookup"><span data-stu-id="d8220-222">a.</span></span> <span data-ttu-id="d8220-223">Hello에 **이름** 텍스트 상자에 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-223">In hello **First name** textbox, type **Britta**.</span></span>

    <span data-ttu-id="d8220-224">b.</span><span class="sxs-lookup"><span data-stu-id="d8220-224">b.</span></span> <span data-ttu-id="d8220-225">Hello에 **성** 텍스트 상자에 **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-225">In hello **Last name** textbox, type **Simon**.</span></span>

    <span data-ttu-id="d8220-226">c.</span><span class="sxs-lookup"><span data-stu-id="d8220-226">c.</span></span> <span data-ttu-id="d8220-227">Hello에 **전자 메일** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-227">In hello **Email** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d8220-228">d.</span><span class="sxs-lookup"><span data-stu-id="d8220-228">d.</span></span> <span data-ttu-id="d8220-229">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-229">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d8220-230">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d8220-231">이 섹션에서는 tooNamely 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNamely.</span></span>

![사용자 할당][200] 

<span data-ttu-id="d8220-233">**tooassign Britta Simon tooNamely hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d8220-233">**tooassign Britta Simon tooNamely, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8220-234">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="d8220-236">Hello 응용 프로그램 목록에서 선택 **즉**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-236">In hello applications list, select **Namely**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-namely-tutorial/tutorial_namely_app.png) 

3. <span data-ttu-id="d8220-238">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="d8220-240">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-240">Click **Add** button.</span></span> <span data-ttu-id="d8220-241">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="d8220-243">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d8220-244">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d8220-245">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d8220-246">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="d8220-246">Testing single sign-on</span></span>

<span data-ttu-id="d8220-247">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD SSO 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8220-247">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="d8220-248">Hello를 클릭할 때 hello 액세스 패널에서에서 타일 즉, 받아야 하며 자동으로 로그온 tooyour 즉 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d8220-248">When you click hello Namely tile in hello Access Panel, you should get automatically signed-on tooyour Namely application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d8220-249">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d8220-249">Additional resources</span></span>

* [<span data-ttu-id="d8220-250">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="d8220-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d8220-251">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d8220-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-namely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-namely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-namely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-namely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-namely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-namely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-namely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-namely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-namely-tutorial/tutorial_general_203.png

