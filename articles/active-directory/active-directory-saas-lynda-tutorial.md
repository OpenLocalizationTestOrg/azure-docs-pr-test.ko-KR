---
title: "자습서: Lynda.com과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Lynda.com 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6c92789-8b64-4049-bac9-8cb928398433
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: fb8d7824e5121da79e9248393b0cbcb0efaffec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lyndacom"></a><span data-ttu-id="a2fd9-103">자습서: Lynda.com과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="a2fd9-103">Tutorial: Azure Active Directory integration with Lynda.com</span></span>

<span data-ttu-id="a2fd9-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 Lynda.com 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-104">In this tutorial, you learn how toointegrate Lynda.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a2fd9-105">Azure AD와 Lynda.com을 통합 hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-105">Integrating Lynda.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a2fd9-106">액세스 tooLynda.com을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-106">You can control in Azure AD who has access tooLynda.com</span></span>
- <span data-ttu-id="a2fd9-107">프로그램 사용자 tooautomatically get 로그온 tooLynda.com (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-107">You can enable your users tooautomatically get signed-on tooLynda.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a2fd9-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a2fd9-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2fd9-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a2fd9-110">Prerequisites</span></span>

<span data-ttu-id="a2fd9-111">Lynda.com과 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-111">tooconfigure Azure AD integration with Lynda.com, you need hello following items:</span></span>

- <span data-ttu-id="a2fd9-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="a2fd9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a2fd9-113">Lynda.com Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="a2fd9-113">A Lynda.com single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a2fd9-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a2fd9-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a2fd9-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a2fd9-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a2fd9-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="a2fd9-118">Scenario description</span></span>
<span data-ttu-id="a2fd9-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a2fd9-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a2fd9-121">Lynda.com은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="a2fd9-121">Adding Lynda.com from hello gallery</span></span>
2. <span data-ttu-id="a2fd9-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a2fd9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lyndacom-from-hello-gallery"></a><span data-ttu-id="a2fd9-123">Lynda.com은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="a2fd9-123">Adding Lynda.com from hello gallery</span></span>
<span data-ttu-id="a2fd9-124">tooconfigure hello와의 통합 Lynda.com Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Lynda.com tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-124">tooconfigure hello integration of Lynda.com into Azure AD, you need tooadd Lynda.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a2fd9-125">**Lynda.com hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a2fd9-125">**tooadd Lynda.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2fd9-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a2fd9-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a2fd9-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="a2fd9-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="a2fd9-133">Hello 검색 상자에 입력 **Lynda.com**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-133">In hello search box, type **Lynda.com**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_search.png)

5. <span data-ttu-id="a2fd9-135">Hello 결과 패널에서 선택 **Lynda.com**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-135">In hello results panel, select **Lynda.com**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a2fd9-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a2fd9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a2fd9-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Lynda.com에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-138">In this section, you configure and test Azure AD single sign-on with Lynda.com based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a2fd9-139">Single sign on toowork에 대 한 Azure AD는 tooknow Lynda.com에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lynda.com is tooa user in Azure AD.</span></span> <span data-ttu-id="a2fd9-140">즉, Azure AD 사용자와 Lynda.com에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-140">In other words, a link relationship between an Azure AD user and hello related user in Lynda.com needs toobe established.</span></span>

<span data-ttu-id="a2fd9-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Lynda.com에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Lynda.com.</span></span>

<span data-ttu-id="a2fd9-142">tooconfigure 및 Lynda.com과 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-142">tooconfigure and test Azure AD single sign-on with Lynda.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a2fd9-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a2fd9-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a2fd9-145">**[Lynda.com 테스트 사용자 만들기](#creating-a-lyndacom-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Lynda.com에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-145">**[Creating a Lynda.com test user](#creating-a-lyndacom-test-user)** - toohave a counterpart of Britta Simon in Lynda.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a2fd9-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a2fd9-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a2fd9-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="a2fd9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a2fd9-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Lynda.com 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lynda.com application.</span></span>

<span data-ttu-id="a2fd9-150">**Azure AD tooconfigure single sign on와 Lynda.com을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a2fd9-150">**tooconfigure Azure AD single sign-on with Lynda.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2fd9-151">Hello hello에 Azure 포털에서에서 **Lynda.com** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-151">In hello Azure portal, on hello **Lynda.com** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="a2fd9-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_samlbase.png)

3. <span data-ttu-id="a2fd9-155">Hello에 **Lynda.com 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-155">On hello **Lynda.com Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_url.png)

    <span data-ttu-id="a2fd9-157">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span><span class="sxs-lookup"><span data-stu-id="a2fd9-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a2fd9-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-158">This value is not real.</span></span> <span data-ttu-id="a2fd9-159">Hello로이 값을 업데이트 합니다. 실제 로그온 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="a2fd9-160">연락처 [클라이언트 Lynda.com 지원 팀](https://www.linkedin.com/help/lynda/ask) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-160">Contact [Lynda.com Client support team](https://www.linkedin.com/help/lynda/ask) tooget these values.</span></span> 
 
4. <span data-ttu-id="a2fd9-161">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello XML 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_certificate.png) 

5. <span data-ttu-id="a2fd9-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lynda-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a2fd9-165">tooconfigure single sign on에서 **Lynda.com** toosend hello 다운로드 해야 쪽에서는 **메타 데이터 XML** [Lynda.com 지원](https://www.linkedin.com/help/lynda/ask)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-165">tooconfigure single sign-on on **Lynda.com** side, you need toosend hello downloaded **Metadata XML** [Lynda.com support](https://www.linkedin.com/help/lynda/ask).</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a2fd9-166">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a2fd9-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="a2fd9-167">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-167">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="a2fd9-169">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a2fd9-169">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2fd9-170">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-170">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lynda-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a2fd9-172">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-172">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lynda-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a2fd9-174">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-174">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lynda-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a2fd9-176">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-176">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lynda-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a2fd9-178">a.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-178">a.</span></span> <span data-ttu-id="a2fd9-179">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-179">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a2fd9-180">b.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-180">b.</span></span> <span data-ttu-id="a2fd9-181">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-181">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a2fd9-182">c.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-182">c.</span></span> <span data-ttu-id="a2fd9-183">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-183">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a2fd9-184">d.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-184">d.</span></span> <span data-ttu-id="a2fd9-185">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-185">Click **Create**.</span></span>
 
### <a name="creating-a-lyndacom-test-user"></a><span data-ttu-id="a2fd9-186">Lynda.com 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a2fd9-186">Creating a Lynda.com test user</span></span>

<span data-ttu-id="a2fd9-187">사용자에 대 한 있습니다 tooconfigure tooLynda.com 프로 비전 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-187">There is no action item for you tooconfigure user provisioning tooLynda.com.</span></span>  
<span data-ttu-id="a2fd9-188">할당된 된 사용자의 hello 액세스 패널을 사용 하 여 tooLynda.com toolog를 시도할 때 Lynda.com hello 사용자의 존재 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-188">When an assigned user tries toolog in tooLynda.com using hello access panel, Lynda.com checks whether hello user exists.</span></span>  

<span data-ttu-id="a2fd9-189">사용할 수 있는 사용자 계정이 없으면 자동으로 Lynda.com에 의해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-189">If there is no user account available yet, it is automatically created by Lynda.com.</span></span>

>[!NOTE]
><span data-ttu-id="a2fd9-190">다른 Lynda.com 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision Lynda.com에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-190">You can use any other Lynda.com user account creation tools or APIs provided by Lynda.com tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a2fd9-191">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-191">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a2fd9-192">이 섹션에서는 tooLynda.com 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-192">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLynda.com.</span></span>

![사용자 할당][200] 

<span data-ttu-id="a2fd9-194">**tooassign Britta Simon tooLynda.com hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a2fd9-194">**tooassign Britta Simon tooLynda.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2fd9-195">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-195">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="a2fd9-197">Hello 응용 프로그램 목록에서 선택 **Lynda.com**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-197">In hello applications list, select **Lynda.com**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_app.png) 

3. <span data-ttu-id="a2fd9-199">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-199">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="a2fd9-201">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-201">Click **Add** button.</span></span> <span data-ttu-id="a2fd9-202">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="a2fd9-204">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-204">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a2fd9-205">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a2fd9-206">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a2fd9-207">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="a2fd9-207">Testing single sign-on</span></span>

<span data-ttu-id="a2fd9-208">Single Sign-On 설정을 테스트하려면 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-208">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="a2fd9-209">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a2fd9-209">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a2fd9-210">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a2fd9-210">Additional resources</span></span>

* [<span data-ttu-id="a2fd9-211">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="a2fd9-211">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a2fd9-212">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="a2fd9-212">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_203.png

