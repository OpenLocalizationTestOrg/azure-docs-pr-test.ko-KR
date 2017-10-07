---
title: "자습서: TimeOffManager와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 TimeOffManager 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: c871257bfb49883e31b1c4860a9d7faa70e9ab48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a><span data-ttu-id="68ac7-103">자습서: TimeOffManager와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="68ac7-103">Tutorial: Azure Active Directory integration with TimeOffManager</span></span>

<span data-ttu-id="68ac7-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 TimeOffManager 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-104">In this tutorial, you learn how toointegrate TimeOffManager with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="68ac7-105">Azure AD와 TimeOffManager 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-105">Integrating TimeOffManager with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="68ac7-106">액세스 tooTimeOffManager을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-106">You can control in Azure AD who has access tooTimeOffManager</span></span>
- <span data-ttu-id="68ac7-107">프로그램 사용자 tooautomatically get 로그온 tooTimeOffManager (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-107">You can enable your users tooautomatically get signed-on tooTimeOffManager (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="68ac7-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="68ac7-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68ac7-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="68ac7-110">Prerequisites</span></span>

<span data-ttu-id="68ac7-111">TimeOffManager와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-111">tooconfigure Azure AD integration with TimeOffManager, you need hello following items:</span></span>

- <span data-ttu-id="68ac7-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="68ac7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="68ac7-113">TimeOffManager Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="68ac7-113">A TimeOffManager single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="68ac7-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="68ac7-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="68ac7-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="68ac7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="68ac7-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="68ac7-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="68ac7-118">Scenario description</span></span>
<span data-ttu-id="68ac7-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="68ac7-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="68ac7-121">TimeOffManager hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="68ac7-121">Add TimeOffManager from hello gallery</span></span>
2. <span data-ttu-id="68ac7-122">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="68ac7-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-timeoffmanager-from-hello-gallery"></a><span data-ttu-id="68ac7-123">TimeOffManager hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="68ac7-123">Add TimeOffManager from hello gallery</span></span>
<span data-ttu-id="68ac7-124">tooconfigure hello와의 통합 TimeOffManager Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 TimeOffManager tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-124">tooconfigure hello integration of TimeOffManager into Azure AD, you need tooadd TimeOffManager from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="68ac7-125">**hello 갤러리에서 TimeOffManager tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="68ac7-125">**tooadd TimeOffManager from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="68ac7-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="68ac7-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="68ac7-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="68ac7-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="68ac7-133">Hello 검색 상자에 입력 **TimeOffManager**선택, **TimeOffManager** 결과 패널에서 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-133">In hello search box, type **TimeOffManager**, select **TimeOffManager** from result panel and then click **Add** button tooadd hello application.</span></span>

    ![갤러리에서 추가](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="68ac7-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="68ac7-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="68ac7-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 TimeOffManager에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-136">In this section, you configure and test Azure AD single sign-on with TimeOffManager based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="68ac7-137">Single sign on toowork에 대 한 Azure AD는 tooknow TimeOffManager에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TimeOffManager is tooa user in Azure AD.</span></span> <span data-ttu-id="68ac7-138">즉, Azure AD 사용자와 TimeOffManager에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-138">In other words, a link relationship between an Azure AD user and hello related user in TimeOffManager needs toobe established.</span></span>

<span data-ttu-id="68ac7-139">Hello hello 값을 할당, TimeOffManager에 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-139">In TimeOffManager, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="68ac7-140">tooconfigure와 TimeOffManager 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-140">tooconfigure and test Azure AD single sign-on with TimeOffManager, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="68ac7-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="68ac7-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="68ac7-143">**[TimeOffManager 테스트 사용자 만들기](#create-a-timeoffmanager-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 TimeOffManager에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-143">**[Create a TimeOffManager test user](#create-a-timeoffmanager-test-user)** - toohave a counterpart of Britta Simon in TimeOffManager that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="68ac7-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="68ac7-145">**[Single Sign-on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="68ac7-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="68ac7-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="68ac7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="68ac7-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 TimeOffManager 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TimeOffManager application.</span></span>

<span data-ttu-id="68ac7-148">**Azure AD tooconfigure single sign on와 TimeOffManager를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="68ac7-148">**tooconfigure Azure AD single sign-on with TimeOffManager, perform hello following steps:**</span></span>

1. <span data-ttu-id="68ac7-149">Hello hello에 Azure 포털에서에서 **TimeOffManager** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-149">In hello Azure portal, on hello **TimeOffManager** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="68ac7-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![SAML 기반 로그온](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. <span data-ttu-id="68ac7-153">Hello에 **TimeOffManager 도메인 및 Url** 섹션에서 hello 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-153">On hello **TimeOffManager Domain and URLs** section, perform hello following:</span></span>

     ![TimeOffManager 도메인 및 URL 섹션](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    <span data-ttu-id="68ac7-155">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span><span class="sxs-lookup"><span data-stu-id="68ac7-155">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="68ac7-156">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-156">This value is not real.</span></span> <span data-ttu-id="68ac7-157">Hello 실제 회신 URL로이 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-157">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="68ac7-158">이 값을 얻을 수 **Single Sign on 설정 페이지** hello 자습서 또는 연락처의 뒷부분에 설명 되어 있는 [TimeOffManager 지원 팀](http://www.timeoffmanager.com/contact-us.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-158">You can get this value from **Single Sign on settings page** which is explained later in hello tutorial or Contact [TimeOffManager support team](http://www.timeoffmanager.com/contact-us.aspx).</span></span>
 
4. <span data-ttu-id="68ac7-159">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![SAML 서명 인증서 섹션](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. <span data-ttu-id="68ac7-161">hello이이 섹션의 목적은 toooutline 페더레이션을 사용 하 여 Azure AD에서 자신의 계정으로 tooenable 사용자 tooauthenticate tooTimeOffManger hello SAML 프로토콜에 따라 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-161">hello objective of this section is toooutline how tooenable users tooauthenticate tooTimeOffManger with their account in Azure AD using federation based on hello SAML protocol.</span></span>
    
    <span data-ttu-id="68ac7-162">TimeOffManger 응용 프로그램의 구성을 수행 해야 하면 tooadd 사용자 지정 특성 매핑을 tooyour SAML 토큰 특성을 특정 형식에서 hello SAML 어설션이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-162">Your TimeOffManger application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="68ac7-163">다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-163">hello following screenshot shows an example for this.</span></span>

    <span data-ttu-id="68ac7-164">![SAML 토큰 특성](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "SAML 토큰 특성")</span><span class="sxs-lookup"><span data-stu-id="68ac7-164">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml token attributes")</span></span>
    
    | <span data-ttu-id="68ac7-165">특성 이름</span><span class="sxs-lookup"><span data-stu-id="68ac7-165">Attribute Name</span></span> | <span data-ttu-id="68ac7-166">특성 값</span><span class="sxs-lookup"><span data-stu-id="68ac7-166">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="68ac7-167">firstname</span><span class="sxs-lookup"><span data-stu-id="68ac7-167">Firstname</span></span> |<span data-ttu-id="68ac7-168">User.givenname</span><span class="sxs-lookup"><span data-stu-id="68ac7-168">User.givenname</span></span> |
    | <span data-ttu-id="68ac7-169">Lastname</span><span class="sxs-lookup"><span data-stu-id="68ac7-169">Lastname</span></span> |<span data-ttu-id="68ac7-170">User.surname</span><span class="sxs-lookup"><span data-stu-id="68ac7-170">User.surname</span></span> |
    | <span data-ttu-id="68ac7-171">Email</span><span class="sxs-lookup"><span data-stu-id="68ac7-171">Email</span></span> |<span data-ttu-id="68ac7-172">User.mail</span><span class="sxs-lookup"><span data-stu-id="68ac7-172">User.mail</span></span> |
    
    <span data-ttu-id="68ac7-173">a.</span><span class="sxs-lookup"><span data-stu-id="68ac7-173">a.</span></span>  <span data-ttu-id="68ac7-174">위의 hello 테이블의 각 데이터 행에 대 한 클릭 **사용자 특성 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-174">For each data row in hello table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="68ac7-175">![SAML 토큰 특성](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "SAML 토큰 특성")</span><span class="sxs-lookup"><span data-stu-id="68ac7-175">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml token attributes")</span></span>
    
    <span data-ttu-id="68ac7-176">![SAML 토큰 특성](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "SAML 토큰 특성")</span><span class="sxs-lookup"><span data-stu-id="68ac7-176">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml token attributes")</span></span>
    
    <span data-ttu-id="68ac7-177">b.</span><span class="sxs-lookup"><span data-stu-id="68ac7-177">b.</span></span>  <span data-ttu-id="68ac7-178">Hello에 **특성 이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-178">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="68ac7-179">c.</span><span class="sxs-lookup"><span data-stu-id="68ac7-179">c.</span></span>  <span data-ttu-id="68ac7-180">Hello에 **특성 값** textbox, 해당 행에 대해 표시 된 선택 hello 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-180">In hello **Attribute Value** textbox, select hello attribute  value shown for that row.</span></span>
    
    <span data-ttu-id="68ac7-181">d.</span><span class="sxs-lookup"><span data-stu-id="68ac7-181">d.</span></span>  <span data-ttu-id="68ac7-182">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-182">Click **Ok**.</span></span>
    
6. <span data-ttu-id="68ac7-183">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-183">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="68ac7-185">Hello에 **TimeOffManager 구성** 섹션에서 클릭 **구성 TimeOffManager** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="68ac7-185">On hello **TimeOffManager Configuration** section, click **Configure TimeOffManager** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="68ac7-186">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="68ac7-186">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![TimeOffManager 구성 섹션](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. <span data-ttu-id="68ac7-188">다른 웹 브라우저 창에서 TimeOffManager 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-188">In a different web browser window, log into your TimeOffManager company site as an administrator.</span></span>

9. <span data-ttu-id="68ac7-189">너무 이동**계정 \> 계정 옵션 \> Single Sign On 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-189">Go too**Account \> Account Options \> Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="68ac7-190">![Single Sign-On 설정](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Single Sign-On 설정")</span><span class="sxs-lookup"><span data-stu-id="68ac7-190">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Single Sign-On Settings")</span></span>
7. <span data-ttu-id="68ac7-191">Hello에 **Single Sign On 설정** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-191">In hello **Single Sign-On Settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="68ac7-192">![Single Sign-On 설정](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Single Sign-On 설정")</span><span class="sxs-lookup"><span data-stu-id="68ac7-192">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="68ac7-193">a.</span><span class="sxs-lookup"><span data-stu-id="68ac7-193">a.</span></span> <span data-ttu-id="68ac7-194">E-64로 인코딩된 인증서 내용을 클립보드의 콘텐츠 복사 hello 메모장에서 열고 후 전체 인증서를 hello **X.509 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-194">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>
   
   <span data-ttu-id="68ac7-195">b.</span><span class="sxs-lookup"><span data-stu-id="68ac7-195">b.</span></span> <span data-ttu-id="68ac7-196">**Idp 발급자** 붙여넣기 hello 값의 텍스트 상자 **SAML 엔터티 ID** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-196">In **Idp Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="68ac7-197">c.</span><span class="sxs-lookup"><span data-stu-id="68ac7-197">c.</span></span> <span data-ttu-id="68ac7-198">**IdP 끝점 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-198">In **IdP Endpoint URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="68ac7-199">d.</span><span class="sxs-lookup"><span data-stu-id="68ac7-199">d.</span></span> <span data-ttu-id="68ac7-200">**SAML 적용**에서는 **아니요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-200">As **Enforce SAML**, select **No**.</span></span>
   
   <span data-ttu-id="68ac7-201">e.</span><span class="sxs-lookup"><span data-stu-id="68ac7-201">e.</span></span> <span data-ttu-id="68ac7-202">**사용자 자동 생성**의 경우 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-202">As **Auto-Create Users**, select **Yes**.</span></span>
   
   <span data-ttu-id="68ac7-203">f.</span><span class="sxs-lookup"><span data-stu-id="68ac7-203">f.</span></span> <span data-ttu-id="68ac7-204">**로그 아웃 URL** 붙여넣기 hello 값의 텍스트 상자 **Sign-Out URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-204">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="68ac7-205">g.</span><span class="sxs-lookup"><span data-stu-id="68ac7-205">g.</span></span> <span data-ttu-id="68ac7-206">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-206">click **Save Changes**.</span></span>

11. <span data-ttu-id="68ac7-207">**Single Sign on 설정** 페이지의 hello 값 복사 **어설션 소비자 서비스 URL** hello에 붙여 넣을 **회신 URL** 아래 텍스트 상자 **TimeOffManager 도메인 및 Url** Azure 포털에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="68ac7-207">In **Single Sign on settings** page, copy hello value of **Assertion Consumer Service URL** and paste it in hello **Reply URL** text box under **TimeOffManager Domain and URLs** section in Azure portal.</span></span> 

      <span data-ttu-id="68ac7-208">![Single Sign-On 설정](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Single Sign-On 설정")</span><span class="sxs-lookup"><span data-stu-id="68ac7-208">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Single Sign-On Settings")</span></span>

> [!TIP]
> <span data-ttu-id="68ac7-209">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="68ac7-209">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="68ac7-210">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="68ac7-210">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="68ac7-211">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="68ac7-211">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="68ac7-212">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="68ac7-212">Create an Azure AD test user</span></span>
<span data-ttu-id="68ac7-213">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-213">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="68ac7-215">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="68ac7-215">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="68ac7-216">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-216">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="68ac7-218">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-218">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![사용자 및 그룹 --> 모든 사용자](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="68ac7-220">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-220">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![추가 단추](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="68ac7-222">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-222">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![사용자 대화 상자 페이지](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="68ac7-224">a.</span><span class="sxs-lookup"><span data-stu-id="68ac7-224">a.</span></span> <span data-ttu-id="68ac7-225">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-225">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="68ac7-226">b.</span><span class="sxs-lookup"><span data-stu-id="68ac7-226">b.</span></span> <span data-ttu-id="68ac7-227">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-227">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="68ac7-228">c.</span><span class="sxs-lookup"><span data-stu-id="68ac7-228">c.</span></span> <span data-ttu-id="68ac7-229">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-229">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="68ac7-230">d.</span><span class="sxs-lookup"><span data-stu-id="68ac7-230">d.</span></span> <span data-ttu-id="68ac7-231">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-231">Click **Create**.</span></span>
 
### <a name="create-a-timeoffmanager-test-user"></a><span data-ttu-id="68ac7-232">TimeOffManager 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="68ac7-232">Create a TimeOffManager test user</span></span>

<span data-ttu-id="68ac7-233">Tooenable Azure AD 사용자가 toolog TimeOffManager에 주문 하 고에 프로 비전 된 tooTimeOffManager 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-233">In order tooenable Azure AD users toolog into TimeOffManager, they must be provisioned tooTimeOffManager.</span></span>  

<span data-ttu-id="68ac7-234">TimeOffManager는 사용자 프로비전 시간에만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-234">TimeOffManager supports just in time user provisioning.</span></span> <span data-ttu-id="68ac7-235">작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-235">There is no action item for you.</span></span>  

<span data-ttu-id="68ac7-236">hello 사용자에 단일 로그인을 사용 하 여 hello 첫 번째 로그인 시 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-236">hello users are added automatically during hello first login using single sign on.</span></span>

>[!NOTE]
><span data-ttu-id="68ac7-237">다른 TimeOffManager 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 Azure AD 사용자 계정을 tooprovision TimeOffManager에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-237">You can use any other TimeOffManager user account creation tools or APIs provided by TimeOffManager tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="68ac7-238">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-238">Assign hello Azure AD test user</span></span>

<span data-ttu-id="68ac7-239">이 섹션에서는 tooTimeOffManager 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTimeOffManager.</span></span>

![사용자 할당][200] 

<span data-ttu-id="68ac7-241">**tooassign Britta Simon tooTimeOffManager hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="68ac7-241">**tooassign Britta Simon tooTimeOffManager, perform hello following steps:**</span></span>

1. <span data-ttu-id="68ac7-242">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="68ac7-244">Hello 응용 프로그램 목록에서 선택 **TimeOffManager**합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-244">In hello applications list, select **TimeOffManager**.</span></span>

    ![앱 목록의 TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. <span data-ttu-id="68ac7-246">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="68ac7-248">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-248">Click **Add** button.</span></span> <span data-ttu-id="68ac7-249">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="68ac7-251">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="68ac7-252">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="68ac7-253">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="68ac7-254">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="68ac7-254">Test single sign-on</span></span>

<span data-ttu-id="68ac7-255">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-255">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="68ac7-256">Hello 액세스 패널에서에서 hello TimeOffManager 타일을 클릭할 때 자동으로 로그온 tooyour TimeOffManager 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-256">When you click hello TimeOffManager tile in hello Access Panel, you should get automatically signed-on tooyour TimeOffManager application.</span></span> <span data-ttu-id="68ac7-257">액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="68ac7-257">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="68ac7-258">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="68ac7-258">Additional resources</span></span>

* [<span data-ttu-id="68ac7-259">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="68ac7-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="68ac7-260">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="68ac7-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

