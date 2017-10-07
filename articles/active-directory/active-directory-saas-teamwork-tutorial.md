---
title: "자습서: Teamwork와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 팀 간의 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03760032-3d76-4b47-ab84-241f72fbd561
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f3a88a146f2a0a70de5ef58abd46f7f26b4104f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamwork"></a><span data-ttu-id="c02ed-103">자습서: Teamwork와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="c02ed-103">Tutorial: Azure Active Directory integration with Teamwork</span></span>

<span data-ttu-id="c02ed-104">이 자습서에 설명 어떻게 toointegrate Azure Active directory (Azure AD)는 팀입니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-104">In this tutorial, you learn how toointegrate Teamwork with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c02ed-105">다음 이점을 hello로 제공 팀 Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="c02ed-105">Integrating Teamwork with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c02ed-106">액세스 tooTeamwork을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-106">You can control in Azure AD who has access tooTeamwork</span></span>
- <span data-ttu-id="c02ed-107">프로그램 사용자 tooautomatically get 로그온 tooTeamwork (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-107">You can enable your users tooautomatically get signed-on tooTeamwork (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c02ed-108">하나의 중앙 위치-hello Azure 관리 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="c02ed-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c02ed-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c02ed-110">Prerequisites</span></span>

<span data-ttu-id="c02ed-111">팀과 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-111">tooconfigure Azure AD integration with Teamwork, you need hello following items:</span></span>

- <span data-ttu-id="c02ed-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="c02ed-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c02ed-113">Teamwork Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="c02ed-113">A Teamwork single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="c02ed-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="c02ed-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c02ed-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="c02ed-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="c02ed-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="c02ed-118">Scenario description</span></span>
<span data-ttu-id="c02ed-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c02ed-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c02ed-121">Hello 갤러리에서 팀을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-121">Adding Teamwork from hello gallery</span></span>
2. <span data-ttu-id="c02ed-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c02ed-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-teamwork-from-hello-gallery"></a><span data-ttu-id="c02ed-123">Hello 갤러리에서 팀을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-123">Adding Teamwork from hello gallery</span></span>
<span data-ttu-id="c02ed-124">tooconfigure hello 통합의 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 팀 tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-124">tooconfigure hello integration of Teamwork into Azure AD, you need tooadd Teamwork from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c02ed-125">**tooadd hello 갤러리에서 팀 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c02ed-125">**tooadd Teamwork from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c02ed-126">Hello에  **[Azure 관리 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c02ed-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c02ed-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="c02ed-131">클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="c02ed-133">Hello 검색 상자에 입력 **팀**합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-133">In hello search box, type **Teamwork**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_001.png)

5. <span data-ttu-id="c02ed-135">Hello 결과 패널에서 선택 **팀**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-135">In hello results panel, select **Teamwork**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c02ed-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c02ed-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c02ed-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Teamwork에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-138">In this section, you configure and test Azure AD single sign-on with Teamwork based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c02ed-139">Single sign on toowork에 대 한 Azure AD는 tooknow 팀에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Teamwork is tooa user in Azure AD.</span></span> <span data-ttu-id="c02ed-140">즉, Azure AD 사용자와 팀에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-140">In other words, a link relationship between an Azure AD user and hello related user in Teamwork needs toobe established.</span></span>

<span data-ttu-id="c02ed-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **사용자 이름** 팀에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Teamwork.</span></span>

<span data-ttu-id="c02ed-142">tooconfigure 및 팀을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-142">tooconfigure and test Azure AD single sign-on with Teamwork, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c02ed-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c02ed-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c02ed-145">**[팀 테스트 사용자 만들기](#creating-a-teamwork-test-user)**  -toohave Britta Simon 표현인 연결 된 Azure AD toohello 그녀의 팀에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-145">**[Creating a Teamwork test user](#creating-a-teamwork-test-user)** - toohave a counterpart of Britta Simon in Teamwork that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="c02ed-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c02ed-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="c02ed-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c02ed-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="c02ed-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c02ed-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 관리 포털에서 설정 및 팀 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Teamwork application.</span></span>

<span data-ttu-id="c02ed-150">**Azure AD tooconfigure single sign on, 팀으로 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c02ed-150">**tooconfigure Azure AD single sign-on with Teamwork, perform hello following steps:**</span></span>

1. <span data-ttu-id="c02ed-151">Hello에 hello Azure 관리 포털에서 **팀** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-151">In hello Azure Management portal, on hello **Teamwork** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="c02ed-153">Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_01.png)

3. <span data-ttu-id="c02ed-155">Hello에 **팀 도메인 및 Url** 섹션 hello **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<company name>.teamwork.com`</span><span class="sxs-lookup"><span data-stu-id="c02ed-155">On hello **Teamwork Domain and URLs** section, in hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company name>.teamwork.com`</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_02.png)

    > [!NOTE] 
    > <span data-ttu-id="c02ed-157">Hello 진정한 가치 아닌지 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c02ed-157">Please note that this is not hello real value.</span></span> <span data-ttu-id="c02ed-158">이 값을 실제 hello로 로그온 URL tooupdate를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-158">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="c02ed-159">연락처 [팀 지원 팀](mailto:support@teamwork.com) tooget이이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-159">Contact [Teamwork support team](mailto:support@teamwork.com) tooget this value.</span></span> 

4. <span data-ttu-id="c02ed-160">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **새 인증서 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-160">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_03.png)   

5. <span data-ttu-id="c02ed-162">Hello에 **새 인증서 만들기** 대화 상자에서 hello 달력 아이콘을 클릭 하 고 선택 된 **만료 날짜**합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-162">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="c02ed-163">그런 후 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-163">Then click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamwork-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="c02ed-165">Hello에 **SAML 서명 인증서** 섹션에서 **새 인증서를 활성화할** 클릭 **저장** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-165">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_04.png)

7. <span data-ttu-id="c02ed-167">Hello 팝업에서 **롤오버 인증서** 창 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-167">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamwork-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c02ed-169">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_05.png) 

9. <span data-ttu-id="c02ed-171">응용 프로그램에 tooget SSO 구성에 문의 하시기 바랍니다 [팀 지원 팀](mailto:support@teamwork.com) hello 다운로드로 제공 **메타 데이터**합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-171">tooget SSO configured for your application, contact [Teamwork support team](mailto:support@teamwork.com) and provide them with hello downloaded **metadata**.</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c02ed-172">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c02ed-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="c02ed-173">이 섹션의 hello 목표 toocreate Britta Simon 라는 hello Azure 관리 포털에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-173">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="c02ed-175">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c02ed-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c02ed-176">Hello에 **Azure 관리 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-176">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamwork-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c02ed-178">너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-178">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamwork-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c02ed-180">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="c02ed-180">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamwork-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c02ed-182">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-teamwork-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c02ed-184">a.</span><span class="sxs-lookup"><span data-stu-id="c02ed-184">a.</span></span> <span data-ttu-id="c02ed-185">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c02ed-186">b.</span><span class="sxs-lookup"><span data-stu-id="c02ed-186">b.</span></span> <span data-ttu-id="c02ed-187">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c02ed-188">c.</span><span class="sxs-lookup"><span data-stu-id="c02ed-188">c.</span></span> <span data-ttu-id="c02ed-189">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c02ed-190">d.</span><span class="sxs-lookup"><span data-stu-id="c02ed-190">d.</span></span> <span data-ttu-id="c02ed-191">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-191">Click **Create**.</span></span> 



### <a name="creating-a-teamwork-test-user"></a><span data-ttu-id="c02ed-192">Teamwork 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c02ed-192">Creating a Teamwork test user</span></span>

<span data-ttu-id="c02ed-193">이 섹션에서는 Teamwork에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-193">In this section, you create a user called Britta Simon in Teamwork.</span></span> <span data-ttu-id="c02ed-194">와 협력 하세요 [팀 지원 팀](mailto:support@teamwork.com) hello 팀 플랫폼의 tooadd hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-194">Please work with [Teamwork support team](mailto:support@teamwork.com) tooadd hello users in hello Teamwork platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c02ed-195">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c02ed-196">이 섹션에서는 액세스 tooTeamwork 그녀의 권한을 부여 하 여 Azure single sign on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooTeamwork.</span></span>

![사용자 할당][200] 

<span data-ttu-id="c02ed-198">**tooassign Britta Simon tooTeamwork hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c02ed-198">**tooassign Britta Simon tooTeamwork, perform hello following steps:**</span></span>

1. <span data-ttu-id="c02ed-199">Hello Azure 관리 포털에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-199">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="c02ed-201">Hello 응용 프로그램 목록에서 선택 **팀**합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-201">In hello applications list, select **Teamwork**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_50.png) 

3. <span data-ttu-id="c02ed-203">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="c02ed-205">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-205">Click **Add** button.</span></span> <span data-ttu-id="c02ed-206">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="c02ed-208">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c02ed-209">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c02ed-210">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="c02ed-211">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="c02ed-211">Testing single sign-on</span></span>

<span data-ttu-id="c02ed-212">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-212">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c02ed-213">Hello 액세스 패널에서에서 hello 팀 타일을 클릭할 때 자동으로 로그온 tooyour 팀 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c02ed-213">When you click hello Teamwork tile in hello Access Panel, you should get automatically signed-on tooyour Teamwork application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="c02ed-214">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="c02ed-214">Additional resources</span></span>

* [<span data-ttu-id="c02ed-215">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="c02ed-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c02ed-216">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="c02ed-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_203.png