---
title: "자습서: Intralinks와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Intralinks 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 6fa49c932d0c48d4b48e04fe91af9fc86a0c1cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a><span data-ttu-id="b9995-103">자습서: Intralinks와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="b9995-103">Tutorial: Azure Active Directory integration with Intralinks</span></span>

<span data-ttu-id="b9995-104">이 자습서에 설명 어떻게 toointegrate Intralinks Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b9995-104">In this tutorial, you learn how toointegrate Intralinks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b9995-105">다음 이점을 hello로 제공 Intralinks Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="b9995-105">Integrating Intralinks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b9995-106">액세스 tooIntralinks을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-106">You can control in Azure AD who has access tooIntralinks</span></span>
- <span data-ttu-id="b9995-107">프로그램 사용자 tooautomatically get 로그온 tooIntralinks (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-107">You can enable your users tooautomatically get signed-on tooIntralinks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b9995-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b9995-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9995-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b9995-110">Prerequisites</span></span>

<span data-ttu-id="b9995-111">다음 항목 hello가 필요 tooconfigure Intralinks와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-111">tooconfigure Azure AD integration with Intralinks, you need hello following items:</span></span>

- <span data-ttu-id="b9995-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="b9995-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b9995-113">Intralinks Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="b9995-113">An Intralinks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b9995-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b9995-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b9995-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b9995-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b9995-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b9995-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="b9995-118">Scenario description</span></span>
<span data-ttu-id="b9995-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b9995-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b9995-121">Intralinks는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="b9995-121">Adding Intralinks from hello gallery</span></span>
2. <span data-ttu-id="b9995-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b9995-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intralinks-from-hello-gallery"></a><span data-ttu-id="b9995-123">Intralinks는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="b9995-123">Adding Intralinks from hello gallery</span></span>
<span data-ttu-id="b9995-124">tooconfigure hello와의 통합 Intralinks Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Intralinks tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-124">tooconfigure hello integration of Intralinks into Azure AD, you need tooadd Intralinks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b9995-125">**hello 갤러리에서 Intralinks tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b9995-125">**tooadd Intralinks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9995-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b9995-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b9995-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="b9995-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="b9995-133">Hello 검색 상자에 입력 **Intralinks**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-133">In hello search box, type **Intralinks**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="b9995-135">Hello 결과 패널에서 선택 **Intralinks**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-135">In hello results panel, select **Intralinks**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b9995-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b9995-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b9995-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Intralinks에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-138">In this section, you configure and test Azure AD single sign-on with Intralinks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b9995-139">Single sign on toowork에 대 한 Azure AD는 tooknow Intralinks에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Intralinks is tooa user in Azure AD.</span></span> <span data-ttu-id="b9995-140">즉, Azure AD 사용자 및 Intralinks에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-140">In other words, a link relationship between an Azure AD user and hello related user in Intralinks needs toobe established.</span></span>

<span data-ttu-id="b9995-141">Intralinks에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-141">In Intralinks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b9995-142">tooconfigure 및 Intralinks 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-142">tooconfigure and test Azure AD single sign-on with Intralinks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b9995-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b9995-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b9995-145">**[Intralinks 테스트 사용자 만들기](#creating-an-intralinks-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Intralinks에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-145">**[Creating an Intralinks test user](#creating-an-intralinks-test-user)** - toohave a counterpart of Britta Simon in Intralinks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b9995-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b9995-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="b9995-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b9995-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="b9995-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b9995-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Intralinks 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Intralinks application.</span></span>

<span data-ttu-id="b9995-150">**tooconfigure Azure AD single sign on, Intralinks와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b9995-150">**tooconfigure Azure AD single sign-on with Intralinks, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9995-151">Hello hello에 Azure 포털에서에서 **Intralinks** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-151">In hello Azure portal, on hello **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="b9995-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_samlbase.png)

3. <span data-ttu-id="b9995-155">Hello에 **Intralinks 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-155">On hello **Intralinks Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_url.png)

    <span data-ttu-id="b9995-157">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span><span class="sxs-lookup"><span data-stu-id="b9995-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:  `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b9995-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-158">This value is not real.</span></span> <span data-ttu-id="b9995-159">Hello로이 값을 업데이트 합니다. 실제 로그온 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="b9995-160">연락처 [Intralinks 클라이언트 지원 팀](https://www.intralinks.com/contact-1) tooget이이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-160">Contact [Intralinks Client support team](https://www.intralinks.com/contact-1) tooget this value.</span></span> 
 
4. <span data-ttu-id="b9995-161">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_certificate.png) 

5. <span data-ttu-id="b9995-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b9995-165">tooconfigure single sign on에서 **Intralinks** toosend hello 다운로드 해야 쪽에서는 **메타 데이터 XML** [Intralinks 지원 팀](https://www.intralinks.com/contact-1)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-165">tooconfigure single sign-on on **Intralinks** side, you need toosend hello downloaded **Metadata XML** [Intralinks support team](https://www.intralinks.com/contact-1).</span></span> <span data-ttu-id="b9995-166">이 설정은 toohave hello 양쪽 모두에 제대로 설정 하는 SAML SSO 연결 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="b9995-167">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="b9995-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b9995-168">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="b9995-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b9995-169">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b9995-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b9995-170">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b9995-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="b9995-171">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="b9995-173">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b9995-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9995-174">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-intralinks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b9995-176">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-intralinks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b9995-178">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b9995-180">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b9995-182">a.</span><span class="sxs-lookup"><span data-stu-id="b9995-182">a.</span></span> <span data-ttu-id="b9995-183">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b9995-184">b.</span><span class="sxs-lookup"><span data-stu-id="b9995-184">b.</span></span> <span data-ttu-id="b9995-185">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b9995-186">c.</span><span class="sxs-lookup"><span data-stu-id="b9995-186">c.</span></span> <span data-ttu-id="b9995-187">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b9995-188">d.</span><span class="sxs-lookup"><span data-stu-id="b9995-188">d.</span></span> <span data-ttu-id="b9995-189">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-189">Click **Create**.</span></span>
 
### <a name="creating-an-intralinks-test-user"></a><span data-ttu-id="b9995-190">Intralinks 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b9995-190">Creating an Intralinks test user</span></span>

<span data-ttu-id="b9995-191">이 섹션에서는 Intralinks에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-191">In this section, you create a user called Britta Simon in Intralinks.</span></span> <span data-ttu-id="b9995-192">와 협력 하세요 [Intralinks 지원 팀](https://www.intralinks.com/contact-1) hello Intralinks 플랫폼의 tooadd hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-192">Please work with [Intralinks support team](https://www.intralinks.com/contact-1) tooadd hello users in hello Intralinks platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b9995-193">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-193">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b9995-194">이 섹션에서는 tooIntralinks 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIntralinks.</span></span>

![사용자 할당][200] 

<span data-ttu-id="b9995-196">**tooassign Britta Simon tooIntralinks hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b9995-196">**tooassign Britta Simon tooIntralinks, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9995-197">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="b9995-199">Hello 응용 프로그램 목록에서 선택 **Intralinks**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-199">In hello applications list, select **Intralinks**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_app.png) 

3. <span data-ttu-id="b9995-201">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="b9995-203">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-203">Click **Add** button.</span></span> <span data-ttu-id="b9995-204">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="b9995-206">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b9995-207">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b9995-208">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-208">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="add-intralinks-via-or-elite-application"></a><span data-ttu-id="b9995-209">Intralinks VIA 또는 Elite 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="b9995-209">Add Intralinks VIA or Elite application</span></span>

<span data-ttu-id="b9995-210">Intralinks 사용 하 여 hello 다른 Intralinks 제외한 모든 응용 프로그램 거래 Nexus 응용 프로그램에 대 한 동일한 SSO id 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-210">Intralinks uses hello same SSO identity platform for all other Intralinks applications excluding Deal Nexus application.</span></span> <span data-ttu-id="b9995-211">따라서 toouse Intralinks 응용 프로그램을 계획 하는 경우 먼저 이름을 제공 해야 위에서 설명한 hello 절차를 사용 하 여 하나의 기본 Intralinks 응용 프로그램에 대 한 SSO tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="b9995-211">So if you plan toouse any other Intralinks application then first you have tooconfigure SSO for one Primary Intralinks application using hello procedure described above.</span></span>

<span data-ttu-id="b9995-212">그 후 SSO에 대 한이 기본 응용 프로그램을 활용할 수 있는 테 넌 트에서 프로시저 tooadd 아래 hello에 다른 Intralinks 응용 프로그램을 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-212">After that you can follow hello below procedure tooadd another Intralinks application in your tenant which can leverage this primary application for SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="b9995-213">이 기능을 사용할 수 있는 유일한 tooAzure AD Premium SKU 고객 및 고객 무료 또는 기본 SKU에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-213">This feature is available only tooAzure AD Premium SKU Customers and not available for Free or Basic SKU customers.</span></span>

1. <span data-ttu-id="b9995-214">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-214">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]


2. <span data-ttu-id="b9995-216">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-216">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b9995-217">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-217">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="b9995-219">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-219">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="b9995-221">Hello 검색 상자에 입력 **Intralinks**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-221">In hello search box, type **Intralinks**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="b9995-223">**앱 Intralinks 추가** hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-223">On **Intralinks Add app** perform hello following steps:</span></span>

    ![Intralinks VIA 또는 Elite 응용 프로그램 추가](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addapp.png)

    <span data-ttu-id="b9995-225">a.</span><span class="sxs-lookup"><span data-stu-id="b9995-225">a.</span></span> <span data-ttu-id="b9995-226">**이름** textbox hello 응용 프로그램의 적절 한 이름을 입력 합니다. **Intralinks 정예**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-226">In **Name** textbox, enter appropriate name of hello application e.g. **Intralinks Elite**.</span></span>

    <span data-ttu-id="b9995-227">b.</span><span class="sxs-lookup"><span data-stu-id="b9995-227">b.</span></span> <span data-ttu-id="b9995-228">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-228">Click **Add** button.</span></span>

6.  <span data-ttu-id="b9995-229">Hello hello에 Azure 포털에서에서 **Intralinks** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-229">In hello Azure portal, on hello **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

7. <span data-ttu-id="b9995-231">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **연결 된 로그온**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-231">On hello **Single sign-on** dialog, select **Mode** as   **Linked Sign-on**.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

8. <span data-ttu-id="b9995-233">Hello hello SP 시작 SSO URL에서 가져오기 [Intralinks 팀](https://www.intralinks.com/contact-1) 에 입력 하 고 hello 다른 Intralinks 응용 프로그램에 대 한 **로그온 URL 구성** 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-233">Get hello hello SP Initiated SSO URL from [Intralinks team](https://www.intralinks.com/contact-1) for hello other Intralinks application and enter it in **Configure Sign-on URL** as shown below.</span></span> 
    
     ![Single Sign-on 구성](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     <span data-ttu-id="b9995-235">Hello 로그온 URL 텍스트 상자에 패턴 hello를 사용 하 여 사용자에 대 한 toosign tooyour Intralinks 응용 프로그램에서 사용 하는 hello URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-235">In hello Sign On URL textbox, type hello URL used by your users toosign-on tooyour Intralinks application using hello following pattern:</span></span>
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

9. <span data-ttu-id="b9995-236">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-236">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="b9995-238">Hello 섹션에 나와 있는 것 처럼 응용 프로그램 toouser hello 또는 그룹에 할당할  **[할당 hello Azure AD 테스트 사용자](#assigning-the-azure-ad-test-user)**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-238">Assign hello application toouser or groups as shown in hello section **[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)**.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="b9995-239">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="b9995-239">Testing single sign-on</span></span>

<span data-ttu-id="b9995-240">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b9995-241">Hello Intralinks hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour Intralinks 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-241">When you click hello Intralinks tile in hello Access Panel, you should get automatically signed-on tooyour Intralinks application.</span></span>
<span data-ttu-id="b9995-242">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9995-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b9995-243">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b9995-243">Additional resources</span></span>

* [<span data-ttu-id="b9995-244">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="b9995-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b9995-245">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b9995-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png

