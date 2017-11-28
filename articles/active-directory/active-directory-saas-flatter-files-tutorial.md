---
title: "자습서: Flatter Files와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 볼록한 파일 및 Azure Active Directory 간의 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f86fe5e3-0e91-40d6-869c-3df6912d27ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 73ca2613b7bbaf9992ecf624ff5defabaa44f7a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-flatter-files"></a><span data-ttu-id="c564c-103">자습서: Flatter Files와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="c564c-103">Tutorial: Azure Active Directory integration with Flatter Files</span></span>

<span data-ttu-id="c564c-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)를 사용 하 여 일반적인 방법 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-104">In this tutorial, you learn how toointegrate Flatter Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c564c-105">다음 이점을 hello로 제공 볼록한 파일을 Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="c564c-105">Integrating Flatter Files with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c564c-106">액세스할 수 있는 Azure AD에서 제어할 수 있습니다 tooFlatter 파일</span><span class="sxs-lookup"><span data-stu-id="c564c-106">You can control in Azure AD who has access tooFlatter Files</span></span>
- <span data-ttu-id="c564c-107">사용자가 tooautomatically 사용 하도록 설정할 수 있습니다 (Single Sign-on)는 Azure AD 계정 로그온 tooFlatter 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="c564c-107">You can enable your users tooautomatically get signed-on tooFlatter Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c564c-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c564c-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c564c-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c564c-110">Prerequisites</span></span>

<span data-ttu-id="c564c-111">일반적인 방법 파일와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-111">tooconfigure Azure AD integration with Flatter Files, you need hello following items:</span></span>

- <span data-ttu-id="c564c-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="c564c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c564c-113">Flatter Files Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="c564c-113">A Flatter Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c564c-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c564c-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c564c-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c564c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c564c-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c564c-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="c564c-118">Scenario description</span></span>
<span data-ttu-id="c564c-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c564c-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c564c-121">Hello 갤러리에서 볼록한 파일 추가</span><span class="sxs-lookup"><span data-stu-id="c564c-121">Adding Flatter Files from hello gallery</span></span>
2. <span data-ttu-id="c564c-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c564c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-flatter-files-from-hello-gallery"></a><span data-ttu-id="c564c-123">Hello 갤러리에서 볼록한 파일 추가</span><span class="sxs-lookup"><span data-stu-id="c564c-123">Adding Flatter Files from hello gallery</span></span>
<span data-ttu-id="c564c-124">tooconfigure hello 통합 볼록한 파일의 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 볼록한 파일 tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-124">tooconfigure hello integration of Flatter Files into Azure AD, you need tooadd Flatter Files from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c564c-125">**tooadd hello 갤러리에서 볼록한 파일 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c564c-125">**tooadd Flatter Files from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c564c-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c564c-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c564c-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="c564c-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="c564c-133">Hello 검색 상자에 입력 **볼록한 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-133">In hello search box, type **Flatter Files**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_search.png)

5. <span data-ttu-id="c564c-135">Hello 결과 패널에서 선택 **볼록한 파일**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-135">In hello results panel, select **Flatter Files**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c564c-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c564c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c564c-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Flatter Files에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-138">In this section, you configure and test Azure AD single sign-on with Flatter Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c564c-139">Single sign on toowork에 대 한 Azure AD는 tooknow에 볼록한 파일에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Flatter Files is tooa user in Azure AD.</span></span> <span data-ttu-id="c564c-140">즉, Azure AD 사용자 및 hello 볼록한 파일에서 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-140">In other words, a link relationship between an Azure AD user and hello related user in Flatter Files needs toobe established.</span></span>

<span data-ttu-id="c564c-141">볼록한 파일에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-141">In Flatter Files, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c564c-142">tooconfigure 및 볼록한 파일을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-142">tooconfigure and test Azure AD single sign-on with Flatter Files, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c564c-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c564c-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c564c-145">**[일반적인 방법 파일 테스트 사용자 만들기](#creating-a-flatter-files-test-user)**  -toohave Britta Simon는 사용자의 연결 된 Azure AD toohello 표현 하는 일반적인 방법 파일에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-145">**[Creating a Flatter Files test user](#creating-a-flatter-files-test-user)** - toohave a counterpart of Britta Simon in Flatter Files that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c564c-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c564c-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="c564c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c564c-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="c564c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c564c-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 및 적용 파일 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Flatter Files application.</span></span>

<span data-ttu-id="c564c-150">**tooconfigure Azure AD single sign on 볼록한 파일과 함께 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c564c-150">**tooconfigure Azure AD single sign-on with Flatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="c564c-151">Hello hello에 Azure 포털에서에서 **볼록한 파일** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-151">In hello Azure portal, on hello **Flatter Files** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="c564c-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_samlbase.png)

3. <span data-ttu-id="c564c-155">Hello에 **볼록한 파일 도메인 및 Url** 섹션에서 hello 사용자 tooperform 모든 단계와 서로 hello 앱 Azure로 이미 사전 통합 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-155">On hello **Flatter Files Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_url.png)
 
4. <span data-ttu-id="c564c-157">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_certificate.png) 

5. <span data-ttu-id="c564c-159">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-159">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-flatter-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c564c-161">Hello에 **볼록한 파일 구성** 섹션에서 클릭 **볼록한 파일 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="c564c-161">On hello **Flatter Files Configuration** section, click **Configure Flatter Files** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c564c-162">복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="c564c-162">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_configure.png) 

7. <span data-ttu-id="c564c-164">로그온 tooyour 관리자 권한으로 응용 프로그램 파일을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-164">Sign-on tooyour Flatter Files application as an administrator.</span></span>

8. <span data-ttu-id="c564c-165">**대시보드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-165">Click **DASHBOARD**.</span></span> 
   
    ![Single Sign-on 구성](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_05.png)  

9. <span data-ttu-id="c564c-167">클릭 **설정**, 다음에 나오는 단계에 따라 hello hello 수행 **회사** 탭:</span><span class="sxs-lookup"><span data-stu-id="c564c-167">Click **Settings**, and then perform hello following steps on hello **Company** tab:</span></span> 
   
    ![Single Sign-on 구성](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_06.png)  
    
    <span data-ttu-id="c564c-169">a.</span><span class="sxs-lookup"><span data-stu-id="c564c-169">a.</span></span> <span data-ttu-id="c564c-170">**인증에 SAML 2.0 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-170">Select **Use SAML 2.0 for Authentication**.</span></span>
    
    <span data-ttu-id="c564c-171">b.</span><span class="sxs-lookup"><span data-stu-id="c564c-171">b.</span></span> <span data-ttu-id="c564c-172">**SAML 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-172">Click **Configure SAML**.</span></span>

8. <span data-ttu-id="c564c-173">Hello에 **SAML 구성** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-173">On hello **SAML Configuration** dialog, perform hello following steps:</span></span> 
   
    ![Single Sign-on 구성](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_08.png)  
   
    <span data-ttu-id="c564c-175">a.</span><span class="sxs-lookup"><span data-stu-id="c564c-175">a.</span></span> <span data-ttu-id="c564c-176">Hello에 **도메인** 텍스트 상자에 등록 된 도메인을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-176">In hello **Domain** textbox, type your registered domain.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="c564c-177">등록된 도메인이 아직 없는 경우 [support@flatterfiles.com](mailto:support@flatterfiles.com)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c564c-177">If you don't have a registered domain yet, contact your Flatter Files support team via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span></span> 
    
    <span data-ttu-id="c564c-178">b.</span><span class="sxs-lookup"><span data-stu-id="c564c-178">b.</span></span> <span data-ttu-id="c564c-179">**Id 공급자 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL** 복사한는 Azure 포털을 형성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-179">In **Identity Provider URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied form Azure portal.</span></span>
   
    <span data-ttu-id="c564c-180">c.</span><span class="sxs-lookup"><span data-stu-id="c564c-180">c.</span></span>  <span data-ttu-id="c564c-181">콘텐츠를 클립보드에 복사 hello 메모장에서 e-64로 인코딩된 인증서를 열고 toohello 붙여 **Id 공급자 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-181">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="c564c-182">d.</span><span class="sxs-lookup"><span data-stu-id="c564c-182">d.</span></span> <span data-ttu-id="c564c-183">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-183">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="c564c-184">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="c564c-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c564c-185">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="c564c-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c564c-186">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c564c-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c564c-187">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c564c-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="c564c-188">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="c564c-190">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c564c-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c564c-191">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c564c-193">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c564c-195">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c564c-197">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c564c-199">a.</span><span class="sxs-lookup"><span data-stu-id="c564c-199">a.</span></span> <span data-ttu-id="c564c-200">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c564c-201">b.</span><span class="sxs-lookup"><span data-stu-id="c564c-201">b.</span></span> <span data-ttu-id="c564c-202">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c564c-203">c.</span><span class="sxs-lookup"><span data-stu-id="c564c-203">c.</span></span> <span data-ttu-id="c564c-204">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c564c-205">d.</span><span class="sxs-lookup"><span data-stu-id="c564c-205">d.</span></span> <span data-ttu-id="c564c-206">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-206">Click **Create**.</span></span>
 
### <a name="creating-a-flatter-files-test-user"></a><span data-ttu-id="c564c-207">Flatter Files 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c564c-207">Creating a Flatter Files test user</span></span>

<span data-ttu-id="c564c-208">hello이이 섹션의 목적은 toocreate Britta Simon 볼록한 파일에서 호출 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-208">hello objective of this section is toocreate a user called Britta Simon in Flatter Files.</span></span>

<span data-ttu-id="c564c-209">**toocreate Britta Simon 볼록한 파일에 라는 사용자를 만들면 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c564c-209">**toocreate a user called Britta Simon in Flatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="c564c-210">Tooyour 로그온 **볼록한 파일** 회사 사이트에서 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-210">Sign on tooyour **Flatter Files** company site as administrator.</span></span>

2. <span data-ttu-id="c564c-211">Hello hello 왼쪽의 탐색 창에서 클릭 **설정**, hello를 클릭 한 다음 **사용자** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-211">In hello navigation pane on hello left, click **Settings**, and then click hello **Users** tab.</span></span>
   
    ![Flatter Files 사용자 만들기](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_09.png)

3. <span data-ttu-id="c564c-213">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-213">Click **Add User**.</span></span> 

4. <span data-ttu-id="c564c-214">Hello에 **사용자 추가** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-214">On hello **Add User** dialog, perform hello following steps:</span></span>
   
    ![Flatter Files 사용자 만들기](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_10.png)

    <span data-ttu-id="c564c-216">a.</span><span class="sxs-lookup"><span data-stu-id="c564c-216">a.</span></span> <span data-ttu-id="c564c-217">Hello에 **이름** 텍스트 상자에 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-217">In hello **First Name** textbox, type **Britta**.</span></span>
   
    <span data-ttu-id="c564c-218">b.</span><span class="sxs-lookup"><span data-stu-id="c564c-218">b.</span></span> <span data-ttu-id="c564c-219">Hello에 **성** 텍스트 상자에 **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-219">In hello **Last Name** textbox, type **Simon**.</span></span> 
   
    <span data-ttu-id="c564c-220">c.</span><span class="sxs-lookup"><span data-stu-id="c564c-220">c.</span></span> <span data-ttu-id="c564c-221">Hello에 **전자 메일 주소** textbox hello Azure 포털에에서 Britta의 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-221">In hello **Email Address** textbox, type Britta's email address in hello Azure portal.</span></span>
   
    <span data-ttu-id="c564c-222">d.</span><span class="sxs-lookup"><span data-stu-id="c564c-222">d.</span></span> <span data-ttu-id="c564c-223">**제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-223">Click **Submit**.</span></span>   


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c564c-224">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c564c-225">이 섹션에서는 사용 하도록 설정 하면 Britta Simon 권한을 부여 하 여 Azure에서 single sign-on toouse tooFlatter 파일에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFlatter Files.</span></span>

![사용자 할당][200] 

<span data-ttu-id="c564c-227">**tooassign Britta Simon tooFlatter 파일 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c564c-227">**tooassign Britta Simon tooFlatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="c564c-228">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="c564c-230">Hello 응용 프로그램 목록에서 선택 **볼록한 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-230">In hello applications list, select **Flatter Files**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_app.png) 

3. <span data-ttu-id="c564c-232">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="c564c-234">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-234">Click **Add** button.</span></span> <span data-ttu-id="c564c-235">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="c564c-237">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c564c-238">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c564c-239">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c564c-240">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="c564c-240">Testing single sign-on</span></span>

<span data-ttu-id="c564c-241">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c564c-242">Hello 볼록한 파일 hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour 볼록한 파일 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-242">When you click hello Flatter Files tile in hello Access Panel, you should get automatically signed-on tooyour Flatter Files application.</span></span>
<span data-ttu-id="c564c-243">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c564c-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c564c-244">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="c564c-244">Additional resources</span></span>

* [<span data-ttu-id="c564c-245">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="c564c-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c564c-246">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="c564c-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_203.png

