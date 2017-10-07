---
title: "자습서: Fuze와 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Fuze 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9780b4bf-1fd1-48c1-9ceb-f750225ae08a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: d0ea8c6456824e348301ed8bf1f5e00f4bfa8121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuze"></a><span data-ttu-id="391ff-103">자습서: Fuze와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="391ff-103">Tutorial: Azure Active Directory integration with Fuze</span></span>

<span data-ttu-id="391ff-104">이 자습서에 설명 toointegrate Azure Active Directory (Azure AD)와 Fuze 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-104">In this tutorial, you learn how toointegrate Fuze with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="391ff-105">다음 이점을 hello로 제공 Fuze Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="391ff-105">Integrating Fuze with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="391ff-106">액세스 tooFuze을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-106">You can control in Azure AD who has access tooFuze</span></span>
- <span data-ttu-id="391ff-107">프로그램 사용자 tooautomatically get 로그온 tooFuze (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-107">You can enable your users tooautomatically get signed-on tooFuze (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="391ff-108">하나의 중앙 위치-hello Azure 관리 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="391ff-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="391ff-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="391ff-110">Prerequisites</span></span>

<span data-ttu-id="391ff-111">다음 항목 hello가 필요 tooconfigure Fuze와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-111">tooconfigure Azure AD integration with Fuze, you need hello following items:</span></span>

- <span data-ttu-id="391ff-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="391ff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="391ff-113">Fuze Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="391ff-113">A Fuze single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="391ff-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="391ff-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="391ff-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="391ff-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="391ff-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="391ff-118">Scenario description</span></span>
<span data-ttu-id="391ff-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="391ff-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="391ff-121">Fuze는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="391ff-121">Adding Fuze from hello gallery</span></span>
2. <span data-ttu-id="391ff-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="391ff-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-fuze-from-hello-gallery"></a><span data-ttu-id="391ff-123">Fuze는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="391ff-123">Adding Fuze from hello gallery</span></span>
<span data-ttu-id="391ff-124">tooconfigure hello와의 통합 Fuze Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Fuze tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-124">tooconfigure hello integration of Fuze into Azure AD, you need tooadd Fuze from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="391ff-125">**hello 갤러리에서 Fuze tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="391ff-125">**tooadd Fuze from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="391ff-126">Hello에  **[Azure 관리 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="391ff-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="391ff-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="391ff-131">클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="391ff-133">Hello 검색 상자에 입력 **Fuze**합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-133">In hello search box, type **Fuze**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_000.png)

5. <span data-ttu-id="391ff-135">Hello 결과 패널에서 선택 **Fuze**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-135">In hello results panel, select **Fuze**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="391ff-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="391ff-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="391ff-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Fuze에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-138">In this section, you configure and test Azure AD single sign-on with Fuze based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="391ff-139">Single sign on toowork에 대 한 Azure AD는 tooknow Fuze에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Fuze is tooa user in Azure AD.</span></span> <span data-ttu-id="391ff-140">즉, Azure AD 사용자 및 Fuze에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-140">In other words, a link relationship between an Azure AD user and hello related user in Fuze needs toobe established.</span></span>

<span data-ttu-id="391ff-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Fuze에 합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Fuze.</span></span>

<span data-ttu-id="391ff-142">tooconfigure 및 Fuze 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-142">tooconfigure and test Azure AD single sign-on with Fuze, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="391ff-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="391ff-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="391ff-145">**[Fuze 테스트 사용자 만들기](#creating-a-fuze-test-user)**  -toohave Britta Simon 그녀의 연결 된 Azure AD toohello 표현인 Fuze에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-145">**[Creating a Fuze test user](#creating-a-fuze-test-user)** - toohave a counterpart of Britta Simon in Fuze that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="391ff-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="391ff-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="391ff-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="391ff-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="391ff-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="391ff-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 관리 포털에서 설정 및 Fuze 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Fuze application.</span></span>

<span data-ttu-id="391ff-150">**tooconfigure Azure AD single sign on, Fuze와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="391ff-150">**tooconfigure Azure AD single sign-on with Fuze, perform hello following steps:**</span></span>

1. <span data-ttu-id="391ff-151">Hello에 hello Azure 관리 포털에서 **Fuze** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-151">In hello Azure Management portal, on hello **Fuze** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="391ff-153">Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_01.png)

3. <span data-ttu-id="391ff-155">Hello에 **Fuze 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-155">On hello **Fuze Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_020.png)
    
    <span data-ttu-id="391ff-157">Hello에 **로그온 URL** textbox로 hello 로그온 URL 입력:`https://www.thinkingphones.com/jetspeed/portal/`</span><span class="sxs-lookup"><span data-stu-id="391ff-157">In hello **Sign on URL** textbox, type hello Sign-on URL as: `https://www.thinkingphones.com/jetspeed/portal/`</span></span>

4.  <span data-ttu-id="391ff-158">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-158">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-fuze-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="391ff-160">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello xml 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-160">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello xml file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_05.png) 

6. <span data-ttu-id="391ff-162">tooconfigure single sign on에서 **Fuze** toosend hello 다운로드 해야 쪽에서는 **메타 데이터 XML** 너무[Fuze 지원 팀](https://www.fuze.com/support)합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-162">tooconfigure single sign-on on **Fuze** side, you need toosend hello downloaded **Metadata XML** too[Fuze support team](https://www.fuze.com/support).</span></span> <span data-ttu-id="391ff-163">순서 toohave hello SAML SSO 연결 양쪽 모두에 제대로 설정에서 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-163">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="391ff-164">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="391ff-164">Creating an Azure AD test user</span></span>
<span data-ttu-id="391ff-165">이 섹션의 hello 목표 toocreate Britta Simon 라는 hello Azure 관리 포털에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-165">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="391ff-167">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="391ff-167">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="391ff-168">Hello에 **Azure 관리 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-168">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-fuze-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="391ff-170">너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-170">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-fuze-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="391ff-172">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="391ff-172">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-fuze-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="391ff-174">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-174">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-fuze-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="391ff-176">a.</span><span class="sxs-lookup"><span data-stu-id="391ff-176">a.</span></span> <span data-ttu-id="391ff-177">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-177">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="391ff-178">b.</span><span class="sxs-lookup"><span data-stu-id="391ff-178">b.</span></span> <span data-ttu-id="391ff-179">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-179">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="391ff-180">c.</span><span class="sxs-lookup"><span data-stu-id="391ff-180">c.</span></span> <span data-ttu-id="391ff-181">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-181">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="391ff-182">d.</span><span class="sxs-lookup"><span data-stu-id="391ff-182">d.</span></span> <span data-ttu-id="391ff-183">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-183">Click **Create**.</span></span> 


### <a name="creating-a-fuze-test-user"></a><span data-ttu-id="391ff-184">Fuze 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="391ff-184">Creating a Fuze test user</span></span>

<span data-ttu-id="391ff-185">Fuze 응용 프로그램은 사용자가 로그인하면 자동으로 생성될 수 있도록 전체 Just-in-time 프로비전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-185">Fuze application supports full Just in time user provision, so users will get created automatically when they sign-in.</span></span> <span data-ttu-id="391ff-186">다른 자세한 설명은 Fuze [지원](https://www.fuze.com/support)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="391ff-186">For any other clarification, please contact Fuze [support](https://www.fuze.com/support).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="391ff-187">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-187">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="391ff-188">이 섹션에서는 액세스 tooFuze 그녀의 권한을 부여 하 여 Azure single sign on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-188">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFuze.</span></span>

![사용자 할당][200] 

<span data-ttu-id="391ff-190">**tooassign Britta Simon tooFuze hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="391ff-190">**tooassign Britta Simon tooFuze, perform hello following steps:**</span></span>

1. <span data-ttu-id="391ff-191">Hello Azure 관리 포털에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-191">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="391ff-193">Hello 응용 프로그램 목록에서 선택 **Fuze**합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-193">In hello applications list, select **Fuze**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_50.png) 

3. <span data-ttu-id="391ff-195">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-195">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="391ff-197">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-197">Click **Add** button.</span></span> <span data-ttu-id="391ff-198">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-198">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="391ff-200">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-200">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="391ff-201">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-201">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="391ff-202">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-202">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="testing-single-sign-on"></a><span data-ttu-id="391ff-203">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="391ff-203">Testing single sign-on</span></span>

<span data-ttu-id="391ff-204">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-204">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="391ff-205">Hello 액세스 패널에서에서 hello Fuze 타일을 클릭할 때 자동으로 로그온 tooyour Fuze 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="391ff-205">When you click hello Fuze tile in hello Access Panel, you should get automatically signed-on tooyour Fuze application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="391ff-206">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="391ff-206">Additional resources</span></span>

* [<span data-ttu-id="391ff-207">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="391ff-207">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="391ff-208">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="391ff-208">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_203.png