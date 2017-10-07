---
title: "자습서: Lecorpio와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Lecorpio 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 963eb36678c589f942f63c7ab555161255324717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lecorpio"></a><span data-ttu-id="cb09a-103">자습서: Lecorpio와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="cb09a-103">Tutorial: Azure Active Directory integration with Lecorpio</span></span>

<span data-ttu-id="cb09a-104">이 자습서에 설명 어떻게 toointegrate Lecorpio Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cb09a-104">In this tutorial, you learn how toointegrate Lecorpio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cb09a-105">다음 이점을 hello로 제공 Lecorpio Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="cb09a-105">Integrating Lecorpio with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cb09a-106">액세스 tooLecorpio을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-106">You can control in Azure AD who has access tooLecorpio</span></span>
- <span data-ttu-id="cb09a-107">프로그램 사용자 tooautomatically get 로그온 tooLecorpio (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-107">You can enable your users tooautomatically get signed-on tooLecorpio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cb09a-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cb09a-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb09a-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cb09a-110">Prerequisites</span></span>

<span data-ttu-id="cb09a-111">다음 항목 hello가 필요 tooconfigure Lecorpio와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-111">tooconfigure Azure AD integration with Lecorpio, you need hello following items:</span></span>

- <span data-ttu-id="cb09a-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="cb09a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cb09a-113">Lecorpio Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="cb09a-113">A Lecorpio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cb09a-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cb09a-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cb09a-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="cb09a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cb09a-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cb09a-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="cb09a-118">Scenario description</span></span>
<span data-ttu-id="cb09a-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cb09a-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cb09a-121">Lecorpio는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="cb09a-121">Adding Lecorpio from hello gallery</span></span>
2. <span data-ttu-id="cb09a-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="cb09a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lecorpio-from-hello-gallery"></a><span data-ttu-id="cb09a-123">Lecorpio는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="cb09a-123">Adding Lecorpio from hello gallery</span></span>
<span data-ttu-id="cb09a-124">tooconfigure hello와의 통합 Lecorpio Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Lecorpio tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-124">tooconfigure hello integration of Lecorpio into Azure AD, you need tooadd Lecorpio from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cb09a-125">**hello 갤러리에서 Lecorpio tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cb09a-125">**tooadd Lecorpio from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb09a-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cb09a-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cb09a-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="cb09a-131">클릭 **새 응용 프로그램** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="cb09a-133">Hello 검색 상자에 입력 **Lecorpio**합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-133">In hello search box, type **Lecorpio**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_search.png)

5. <span data-ttu-id="cb09a-135">Hello 결과 패널에서 선택 **Lecorpio**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-135">In hello results panel, select **Lecorpio**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cb09a-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="cb09a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cb09a-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Lecorpio에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-138">In this section, you configure and test Azure AD single sign-on with Lecorpio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cb09a-139">Single sign on toowork에 대 한 Azure AD는 tooknow Lecorpio에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lecorpio is tooa user in Azure AD.</span></span> <span data-ttu-id="cb09a-140">즉, Azure AD 사용자 및 Lecorpio에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-140">In other words, a link relationship between an Azure AD user and hello related user in Lecorpio needs toobe established.</span></span>

<span data-ttu-id="cb09a-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Lecorpio에 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Lecorpio.</span></span>

<span data-ttu-id="cb09a-142">tooconfigure 및 Lecorpio 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-142">tooconfigure and test Azure AD single sign-on with Lecorpio, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cb09a-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cb09a-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cb09a-145">**[Lecorpio 테스트 사용자 만들기](#creating-a-lecorpio-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Lecorpio에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-145">**[Creating a Lecorpio test user](#creating-a-lecorpio-test-user)** - toohave a counterpart of Britta Simon in Lecorpio that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cb09a-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cb09a-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="cb09a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cb09a-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="cb09a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cb09a-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Lecorpio 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lecorpio application.</span></span>

<span data-ttu-id="cb09a-150">**tooconfigure Azure AD single sign on, Lecorpio와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cb09a-150">**tooconfigure Azure AD single sign-on with Lecorpio, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb09a-151">Hello hello에 Azure 포털에서에서 **Lecorpio** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-151">In hello Azure portal, on hello **Lecorpio** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="cb09a-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_samlbase.png)

3. <span data-ttu-id="cb09a-155">Hello에 **Lecorpio 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-155">On hello **Lecorpio Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_url.png)

    <span data-ttu-id="cb09a-157">a.</span><span class="sxs-lookup"><span data-stu-id="cb09a-157">a.</span></span> <span data-ttu-id="cb09a-158">Hello에 **로그온 URL** hello 패턴을 사용 하 여 형식 hello 값 텍스트 상자:`https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="cb09a-158">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    <span data-ttu-id="cb09a-159">b.</span><span class="sxs-lookup"><span data-stu-id="cb09a-159">b.</span></span> <span data-ttu-id="cb09a-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="cb09a-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cb09a-161">이러한 값은 실제 hello 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-161">These values are not hello real.</span></span> <span data-ttu-id="cb09a-162">Hello 실제 로그온 URL과 식별자와 이러한 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-162">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="cb09a-163">여기 있습니다 toouse hello의 고유 값을 hello 식별자의에서 문자열을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="cb09a-164">연락처 [Lecorpio 클라이언트 지원 팀](mailto:info@lecorpio.com) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-164">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="cb09a-165">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_certificate.png) 

5. <span data-ttu-id="cb09a-167">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-167">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lecorpio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cb09a-169">tooconfigure single sign on에서 **Lecorpio** toosend hello 다운로드 해야 쪽에서는 **메타 데이터 XML** 너무[Lecorpio 지원 팀](mailto:info@lecorpio.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-169">tooconfigure single sign-on on **Lecorpio** side, you need toosend hello downloaded **Metadata XML** too[Lecorpio support team](mailto:info@lecorpio.com).</span></span>

> [!TIP]
> <span data-ttu-id="cb09a-170">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="cb09a-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cb09a-171">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="cb09a-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cb09a-172">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cb09a-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cb09a-173">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="cb09a-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="cb09a-174">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="cb09a-176">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cb09a-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb09a-177">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cb09a-179">너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-179">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cb09a-181">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="cb09a-181">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cb09a-183">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cb09a-185">a.</span><span class="sxs-lookup"><span data-stu-id="cb09a-185">a.</span></span> <span data-ttu-id="cb09a-186">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cb09a-187">b.</span><span class="sxs-lookup"><span data-stu-id="cb09a-187">b.</span></span> <span data-ttu-id="cb09a-188">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cb09a-189">c.</span><span class="sxs-lookup"><span data-stu-id="cb09a-189">c.</span></span> <span data-ttu-id="cb09a-190">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cb09a-191">d.</span><span class="sxs-lookup"><span data-stu-id="cb09a-191">d.</span></span> <span data-ttu-id="cb09a-192">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-192">Click **Create**.</span></span>
 
### <a name="creating-a-lecorpio-test-user"></a><span data-ttu-id="cb09a-193">Lecorpio 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="cb09a-193">Creating a Lecorpio test user</span></span>

<span data-ttu-id="cb09a-194">이 섹션에서는 Lecorpio에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-194">In this section, you create a user called Britta Simon in Lecorpio.</span></span> 

<span data-ttu-id="cb09a-195">연락처 [Lecorpio 클라이언트 지원 팀](mailto:info@lecorpio.com) hello Lecorpio 응용 프로그램의에서 tooadd hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-195">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) tooadd hello users in hello Lecorpio application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cb09a-196">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cb09a-197">이 섹션에서는 tooLecorpio 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLecorpio.</span></span>

![사용자 할당][200] 

<span data-ttu-id="cb09a-199">**tooassign Britta Simon tooLecorpio hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="cb09a-199">**tooassign Britta Simon tooLecorpio, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb09a-200">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="cb09a-202">Hello 응용 프로그램 목록에서 선택 **Lecorpio**합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-202">In hello applications list, select **Lecorpio**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_app.png) 

3. <span data-ttu-id="cb09a-204">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="cb09a-206">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-206">Click **Add** button.</span></span> <span data-ttu-id="cb09a-207">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="cb09a-209">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cb09a-210">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cb09a-211">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cb09a-212">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="cb09a-212">Testing single sign-on</span></span>

<span data-ttu-id="cb09a-213">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cb09a-214">Hello 액세스 패널에서에서 hello Lecorpio 타일을 클릭할 때 자동으로 로그온 tooyour Lecorpio 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb09a-214">When you click hello Lecorpio tile in hello Access Panel, you should get automatically signed-on tooyour Lecorpio application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cb09a-215">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="cb09a-215">Additional resources</span></span>

* [<span data-ttu-id="cb09a-216">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="cb09a-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cb09a-217">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="cb09a-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_203.png

