---
title: "자습서: 123ContactForm과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 123ContactForm 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5211910a-ab96-4709-959a-524c4d57c43e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 931255887845edd1aa7f53b9051a82a2f898e055
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-123contactform"></a><span data-ttu-id="c690c-103">자습서: 123ContactForm과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="c690c-103">Tutorial: Azure Active Directory integration with 123ContactForm</span></span>

<span data-ttu-id="c690c-104">이 자습서에 설명 어떻게 toointegrate 123ContactForm Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c690c-104">In this tutorial, you learn how toointegrate 123ContactForm with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c690c-105">다음 이점을 hello로 제공 123ContactForm Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="c690c-105">Integrating 123ContactForm with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c690c-106">액세스 too123ContactForm을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-106">You can control in Azure AD who has access too123ContactForm</span></span>
- <span data-ttu-id="c690c-107">에 사용자가 tooautomatically get 로그온 too123ContactForm 사용 하도록 설정할 수 있습니다 (Single Sign-on)는 Azure AD 계정을 사용</span><span class="sxs-lookup"><span data-stu-id="c690c-107">You can enable your users tooautomatically get signed-on too123ContactForm (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c690c-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c690c-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c690c-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c690c-110">Prerequisites</span></span>

<span data-ttu-id="c690c-111">다음 항목 hello가 필요 tooconfigure 123ContactForm와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-111">tooconfigure Azure AD integration with 123ContactForm, you need hello following items:</span></span>

- <span data-ttu-id="c690c-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="c690c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c690c-113">123ContactForm Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="c690c-113">A 123ContactForm single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c690c-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c690c-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c690c-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c690c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c690c-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c690c-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="c690c-118">Scenario description</span></span>
<span data-ttu-id="c690c-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c690c-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c690c-121">123ContactForm hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="c690c-121">Adding 123ContactForm from hello gallery</span></span>
2. <span data-ttu-id="c690c-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c690c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-123contactform-from-hello-gallery"></a><span data-ttu-id="c690c-123">123ContactForm hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="c690c-123">Adding 123ContactForm from hello gallery</span></span>
<span data-ttu-id="c690c-124">tooconfigure hello와의 통합 123ContactForm Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 tooadd 123ContactForm 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-124">tooconfigure hello integration of 123ContactForm into Azure AD, you need tooadd 123ContactForm from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c690c-125">**hello 갤러리에서 tooadd 123ContactForm hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c690c-125">**tooadd 123ContactForm from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c690c-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c690c-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c690c-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="c690c-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="c690c-133">Hello 검색 상자에 입력 **123ContactForm**합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-133">In hello search box, type **123ContactForm**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_search.png)

5. <span data-ttu-id="c690c-135">Hello 결과 패널에서 선택 **123ContactForm**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-135">In hello results panel, select **123ContactForm**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c690c-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c690c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c690c-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 123ContactForm에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-138">In this section, you configure and test Azure AD single sign-on with 123ContactForm based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c690c-139">Single sign on toowork에 대 한 Azure AD는 tooknow 123ContactForm에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 123ContactForm is tooa user in Azure AD.</span></span> <span data-ttu-id="c690c-140">즉, Azure AD 사용자 및 123ContactForm에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-140">In other words, a link relationship between an Azure AD user and hello related user in 123ContactForm needs toobe established.</span></span>

<span data-ttu-id="c690c-141">123ContactForm에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-141">In 123ContactForm, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c690c-142">tooconfigure 및 123ContactForm 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-142">tooconfigure and test Azure AD single sign-on with 123ContactForm, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c690c-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c690c-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c690c-145">**[123ContactForm 테스트 사용자 만들기](#creating-a-123contactform-test-user)**  -toohave에서 사용자의 연결 된 Azure AD toohello 표현인 123ContactForm Britta Simon 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-145">**[Creating a 123ContactForm test user](#creating-a-123contactform-test-user)** - toohave a counterpart of Britta Simon in 123ContactForm that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c690c-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c690c-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="c690c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c690c-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="c690c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c690c-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 123ContactForm 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 123ContactForm application.</span></span>

<span data-ttu-id="c690c-150">**tooconfigure Azure AD single sign on, 123ContactForm와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c690c-150">**tooconfigure Azure AD single sign-on with 123ContactForm, perform hello following steps:**</span></span>

1. <span data-ttu-id="c690c-151">Hello hello에 Azure 포털에서에서 **123ContactForm** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-151">In hello Azure portal, on hello **123ContactForm** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="c690c-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_samlbase.png)

3. <span data-ttu-id="c690c-155">Hello에 **123ContactForm 도메인 및 Url** 섹션 tooconfigure hello 응용 프로그램에 필요한 경우 **IDP 시작 모드**, hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-155">On hello **123ContactForm Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-123contactform-tutorial/url1.png)

    <span data-ttu-id="c690c-157">a.</span><span class="sxs-lookup"><span data-stu-id="c690c-157">a.</span></span> <span data-ttu-id="c690c-158">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span><span class="sxs-lookup"><span data-stu-id="c690c-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span></span>

    <span data-ttu-id="c690c-159">b.</span><span class="sxs-lookup"><span data-stu-id="c690c-159">b.</span></span> <span data-ttu-id="c690c-160">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span><span class="sxs-lookup"><span data-stu-id="c690c-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span></span>

4. <span data-ttu-id="c690c-161">Tooconfigure hello 응용 프로그램에 필요한 경우 **SP 시작 모드**, hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-161">If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-123contactform-tutorial/url2.png)

    <span data-ttu-id="c690c-163">a.</span><span class="sxs-lookup"><span data-stu-id="c690c-163">a.</span></span> <span data-ttu-id="c690c-164">Hello 클릭 **고급 URL 설정 표시** 옵션</span><span class="sxs-lookup"><span data-stu-id="c690c-164">Click hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="c690c-165">b.</span><span class="sxs-lookup"><span data-stu-id="c690c-165">b.</span></span> <span data-ttu-id="c690c-166">Hello에 **로그온 URL** 텍스트 상자에 다음 URL로:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span><span class="sxs-lookup"><span data-stu-id="c690c-166">In hello **Sign On URL** textbox, type a URL as: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c690c-167">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-167">These values are not real.</span></span> <span data-ttu-id="c690c-168">Tooupdate 실제 Url과 식별자 hello 자습서의 뒷부분에 설명 된이 값이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-168">You'll need tooupdate these value from actual URLs and Identifier which is explained later in hello tutorial.</span></span>
    
5. <span data-ttu-id="c690c-169">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_certificate.png) 

6. <span data-ttu-id="c690c-171">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-171">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-123contactform-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="c690c-173">tooconfigure single sign on에서 **123ContactForm** 쪽, 너무 이동[https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) hello 다음 단계를 수행:</span><span class="sxs-lookup"><span data-stu-id="c690c-173">tooconfigure single sign-on on **123ContactForm** side, go too[https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) and perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-123contactform-tutorial/submit.png) 

    <span data-ttu-id="c690c-175">a.</span><span class="sxs-lookup"><span data-stu-id="c690c-175">a.</span></span> <span data-ttu-id="c690c-176">Hello에 **전자 메일** hello 사용자 즉,의 형식 hello 전자 메일 텍스트 상자</span><span class="sxs-lookup"><span data-stu-id="c690c-176">In hello **Email** textbox, type hello email of hello user i.e</span></span> <span data-ttu-id="c690c-177">**BrittaSimon@Contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="c690c-177">**BrittaSimon@Contoso.com**.</span></span>

    <span data-ttu-id="c690c-178">b.</span><span class="sxs-lookup"><span data-stu-id="c690c-178">b.</span></span> <span data-ttu-id="c690c-179">클릭 **업로드** hello Azure 포털에서 다운로드 한 메타 데이터 XML 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-179">Click **Upload** and browse hello Metadata XML file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="c690c-180">c.</span><span class="sxs-lookup"><span data-stu-id="c690c-180">c.</span></span> <span data-ttu-id="c690c-181">**양식 제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-181">Click **SUBMIT FORM**.</span></span>

8. <span data-ttu-id="c690c-182">Hello에 **Microsoft Azure AD에서 Single sign on-응용 프로그램 설정 구성** hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-182">On hello **Microsoft Azure AD - Single sign-on - Configure App Settings** perform hello following steps:</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-123contactform-tutorial/url3.png)

    <span data-ttu-id="c690c-184">a.</span><span class="sxs-lookup"><span data-stu-id="c690c-184">a.</span></span> <span data-ttu-id="c690c-185">Tooconfigure hello 응용 프로그램에 필요한 경우 **IDP 시작 모드**, 복사 hello **식별자** 인스턴스에 대 한 값을 붙여 넣습니다 **식별자** 텍스트상자로**123ContactForm 도메인 및 Url** Azure 포털에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="c690c-185">If you wish tooconfigure hello application in **IDP initiated mode**, copy hello **IDENTIFIER** value for your instance and paste it in **Identifier** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="c690c-186">b.</span><span class="sxs-lookup"><span data-stu-id="c690c-186">b.</span></span> <span data-ttu-id="c690c-187">Tooconfigure hello 응용 프로그램에 필요한 경우 **IDP 시작 모드**, 복사 hello **회신 URL** 인스턴스에 대 한 값을 붙여 넣습니다 **회신 URL** 텍스트상자로**123ContactForm 도메인 및 Url** Azure 포털에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="c690c-187">If you wish tooconfigure hello application in **IDP initiated mode**, copy hello **REPLY URL** value for your instance and paste it in **Reply URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="c690c-188">c.</span><span class="sxs-lookup"><span data-stu-id="c690c-188">c.</span></span> <span data-ttu-id="c690c-189">Tooconfigure hello 응용 프로그램에 필요한 경우 **SP 시작 모드**, 복사 hello **SIGN ON URL** 인스턴스에 대 한 값을 붙여 넣습니다 **로그온 URL** 텍스트상자로**123ContactForm 도메인 및 Url** Azure 포털에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="c690c-189">If you wish tooconfigure hello application in **SP initiated mode**, copy hello **SIGN ON URL** value for your instance and paste it in **Sign On URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="c690c-190">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="c690c-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c690c-191">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="c690c-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c690c-192">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c690c-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c690c-193">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c690c-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="c690c-194">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="c690c-196">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c690c-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c690c-197">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-123contactform-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c690c-199">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-123contactform-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c690c-201">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-123contactform-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c690c-203">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-123contactform-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c690c-205">a.</span><span class="sxs-lookup"><span data-stu-id="c690c-205">a.</span></span> <span data-ttu-id="c690c-206">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c690c-207">b.</span><span class="sxs-lookup"><span data-stu-id="c690c-207">b.</span></span> <span data-ttu-id="c690c-208">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c690c-209">c.</span><span class="sxs-lookup"><span data-stu-id="c690c-209">c.</span></span> <span data-ttu-id="c690c-210">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c690c-211">d.</span><span class="sxs-lookup"><span data-stu-id="c690c-211">d.</span></span> <span data-ttu-id="c690c-212">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-212">Click **Create**.</span></span>
 
### <a name="creating-a-123contactform-test-user"></a><span data-ttu-id="c690c-213">123ContactForm 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c690c-213">Creating a 123ContactForm test user</span></span>

<span data-ttu-id="c690c-214">응용 프로그램 적시 사용자 프로 비전 및 인증 사용자 hello 응용 프로그램에서에 자동으로 생성 한 후 마법사를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-214">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c690c-215">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c690c-216">이 섹션에서는 too123ContactForm 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too123ContactForm.</span></span>

![사용자 할당][200] 

<span data-ttu-id="c690c-218">**tooassign Britta Simon too123ContactForm hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c690c-218">**tooassign Britta Simon too123ContactForm, perform hello following steps:**</span></span>

1. <span data-ttu-id="c690c-219">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="c690c-221">Hello 응용 프로그램 목록에서 선택 **123ContactForm**합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-221">In hello applications list, select **123ContactForm**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_app.png) 

3. <span data-ttu-id="c690c-223">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="c690c-225">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-225">Click **Add** button.</span></span> <span data-ttu-id="c690c-226">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="c690c-228">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c690c-229">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c690c-230">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c690c-231">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="c690c-231">Testing single sign-on</span></span>

<span data-ttu-id="c690c-232">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c690c-233">Hello 액세스 패널에서에서 hello 123ContactForm 타일을 클릭할 때 자동으로 로그온 tooyour 123ContactForm 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-233">When you click hello 123ContactForm tile in hello Access Panel, you should get automatically signed-on tooyour 123ContactForm application.</span></span>
<span data-ttu-id="c690c-234">액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c690c-234">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c690c-235">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="c690c-235">Additional resources</span></span>

* [<span data-ttu-id="c690c-236">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="c690c-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c690c-237">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="c690c-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_203.png

