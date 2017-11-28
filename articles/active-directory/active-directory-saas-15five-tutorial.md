---
title: "자습서: 15Five와 Azure Active Directory 통합 | Microsoft 문서"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 15Five 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2fb301c2-7d7a-4046-8ee1-7dc9e7684806
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 9e531615c16331ce000e285d13d9adce13735a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-15five"></a><span data-ttu-id="4ba97-103">자습서: 15Five와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="4ba97-103">Tutorial: Azure Active Directory integration with 15Five</span></span>

<span data-ttu-id="4ba97-104">이 자습서에 설명 어떻게 toointegrate 15Five Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4ba97-104">In this tutorial, you learn how toointegrate 15Five with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4ba97-105">Azure AD와 15Five 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-105">Integrating 15Five with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4ba97-106">액세스 too15Five을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-106">You can control in Azure AD who has access too15Five</span></span>
- <span data-ttu-id="4ba97-107">에 사용자가 tooautomatically get 로그온 too15Five 사용 하도록 설정할 수 있습니다 (Single Sign-on)는 Azure AD 계정을 사용</span><span class="sxs-lookup"><span data-stu-id="4ba97-107">You can enable your users tooautomatically get signed-on too15Five (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4ba97-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4ba97-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ba97-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4ba97-110">Prerequisites</span></span>

<span data-ttu-id="4ba97-111">15Five와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-111">tooconfigure Azure AD integration with 15Five, you need hello following items:</span></span>

- <span data-ttu-id="4ba97-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="4ba97-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4ba97-113">15Five Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="4ba97-113">A 15Five single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4ba97-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4ba97-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4ba97-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="4ba97-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4ba97-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4ba97-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="4ba97-118">Scenario description</span></span>
<span data-ttu-id="4ba97-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4ba97-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4ba97-121">15Five hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="4ba97-121">Adding 15Five from hello gallery</span></span>
2. <span data-ttu-id="4ba97-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="4ba97-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-15five-from-hello-gallery"></a><span data-ttu-id="4ba97-123">15Five hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="4ba97-123">Adding 15Five from hello gallery</span></span>
<span data-ttu-id="4ba97-124">tooconfigure hello와의 통합 15Five Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 tooadd 15Five 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-124">tooconfigure hello integration of 15Five into Azure AD, you need tooadd 15Five from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4ba97-125">**hello 갤러리에서 tooadd 15Five hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4ba97-125">**tooadd 15Five from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ba97-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4ba97-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4ba97-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="4ba97-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="4ba97-133">Hello 검색 상자에 입력 **15Five**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-133">In hello search box, type **15Five**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-15five-tutorial/tutorial_15five_search.png)

5. <span data-ttu-id="4ba97-135">Hello 결과 패널에서 선택 **15Five**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-135">In hello results panel, select **15Five**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-15five-tutorial/tutorial_15five_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4ba97-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="4ba97-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4ba97-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 15Five에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-138">In this section, you configure and test Azure AD single sign-on with 15Five based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4ba97-139">Single sign on toowork에 대 한 Azure AD는 tooknow 15Five에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 15Five is tooa user in Azure AD.</span></span> <span data-ttu-id="4ba97-140">즉, Azure AD 사용자와 15Five에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-140">In other words, a link relationship between an Azure AD user and hello related user in 15Five needs toobe established.</span></span>

<span data-ttu-id="4ba97-141">15Five에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-141">In 15Five, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4ba97-142">tooconfigure와 15Five 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-142">tooconfigure and test Azure AD single sign-on with 15Five, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4ba97-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4ba97-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4ba97-145">**[15Five 테스트 사용자 만들기](#creating-a-15five-test-user)**  -toohave 사용자의 연결 된 Azure AD toohello 표현인 15Five에 Britta Simon 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-145">**[Creating a 15Five test user](#creating-a-15five-test-user)** - toohave a counterpart of Britta Simon in 15Five that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4ba97-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4ba97-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="4ba97-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4ba97-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="4ba97-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4ba97-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 15Five 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 15Five application.</span></span>

<span data-ttu-id="4ba97-150">**Azure AD tooconfigure single sign on와 15Five를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4ba97-150">**tooconfigure Azure AD single sign-on with 15Five, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ba97-151">Hello hello에 Azure 포털에서에서 **15Five** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-151">In hello Azure portal, on hello **15Five** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="4ba97-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-15five-tutorial/tutorial_15five_samlbase.png)

3. <span data-ttu-id="4ba97-155">Hello에 **15Five 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-155">On hello **15Five Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-15five-tutorial/tutorial_15five_url.png)

    <span data-ttu-id="4ba97-157">a.</span><span class="sxs-lookup"><span data-stu-id="4ba97-157">a.</span></span> <span data-ttu-id="4ba97-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.15five.com`</span><span class="sxs-lookup"><span data-stu-id="4ba97-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.15five.com`</span></span>

    <span data-ttu-id="4ba97-159">b.</span><span class="sxs-lookup"><span data-stu-id="4ba97-159">b.</span></span> <span data-ttu-id="4ba97-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.15five.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="4ba97-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.15five.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4ba97-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-161">These values are not real.</span></span> <span data-ttu-id="4ba97-162">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4ba97-163">연락처 [15Five 클라이언트 지원 팀](https://www.15five.com/contact/) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-163">Contact [15Five Client support team](https://www.15five.com/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="4ba97-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-15five-tutorial/tutorial_15five_certificate.png) 

5. <span data-ttu-id="4ba97-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-15five-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4ba97-168">tooconfigure single sign on에서 **15Five** toosend hello 다운로드 해야 쪽에서는 **메타 데이터 XML** 너무[15Five 지원 팀](https://www.15five.com/contact/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-168">tooconfigure single sign-on on **15Five** side, you need toosend hello downloaded **Metadata XML** too[15Five support team](https://www.15five.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="4ba97-169">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="4ba97-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4ba97-170">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="4ba97-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4ba97-171">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4ba97-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4ba97-172">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="4ba97-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="4ba97-173">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="4ba97-175">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4ba97-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ba97-176">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-15five-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4ba97-178">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-15five-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4ba97-180">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-15five-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4ba97-182">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-15five-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4ba97-184">a.</span><span class="sxs-lookup"><span data-stu-id="4ba97-184">a.</span></span> <span data-ttu-id="4ba97-185">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4ba97-186">b.</span><span class="sxs-lookup"><span data-stu-id="4ba97-186">b.</span></span> <span data-ttu-id="4ba97-187">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4ba97-188">c.</span><span class="sxs-lookup"><span data-stu-id="4ba97-188">c.</span></span> <span data-ttu-id="4ba97-189">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4ba97-190">d.</span><span class="sxs-lookup"><span data-stu-id="4ba97-190">d.</span></span> <span data-ttu-id="4ba97-191">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-191">Click **Create**.</span></span>
 
### <a name="creating-a-15five-test-user"></a><span data-ttu-id="4ba97-192">15Five 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="4ba97-192">Creating a 15Five test user</span></span>

<span data-ttu-id="4ba97-193">tooenable Azure AD 사용자가 toolog too15Five에서 프로 비전 해야 15Five에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-193">tooenable Azure AD users toolog in too15Five, they must be provisioned into 15Five.</span></span> <span data-ttu-id="4ba97-194">15Five의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-194">When 15Five, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="4ba97-195">tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:</span><span class="sxs-lookup"><span data-stu-id="4ba97-195">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="4ba97-196">Tooyour 로그인 **15Five** 회사 사이트에서 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-196">Log in tooyour **15Five** company site as administrator.</span></span>

2. <span data-ttu-id="4ba97-197">너무 이동**관리 회사**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-197">Go too**Manage Company**.</span></span>
   
    <span data-ttu-id="4ba97-198">![회사 관리](./media/active-directory-saas-15five-tutorial/IC784675.png "회사 관리")</span><span class="sxs-lookup"><span data-stu-id="4ba97-198">![Manage Company](./media/active-directory-saas-15five-tutorial/IC784675.png "Manage Company")</span></span>

3. <span data-ttu-id="4ba97-199">너무 이동**사람 \> 사람 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-199">Go too**People \> Add People**.</span></span>
   
    <span data-ttu-id="4ba97-200">![사람](./media/active-directory-saas-15five-tutorial/IC784676.png "사람")</span><span class="sxs-lookup"><span data-stu-id="4ba97-200">![People](./media/active-directory-saas-15five-tutorial/IC784676.png "People")</span></span>

4. <span data-ttu-id="4ba97-201">새로운 사람 추가 섹션 hello hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-201">In hello Add New Person section, perform hello following steps:</span></span>
   
    <span data-ttu-id="4ba97-202">![새 사람 추가](./media/active-directory-saas-15five-tutorial/IC784677.png "새 사람 추가")</span><span class="sxs-lookup"><span data-stu-id="4ba97-202">![Add New Person](./media/active-directory-saas-15five-tutorial/IC784677.png "Add New Person")</span></span>
   
    <span data-ttu-id="4ba97-203">a.</span><span class="sxs-lookup"><span data-stu-id="4ba97-203">a.</span></span> <span data-ttu-id="4ba97-204">형식 hello **이름**, **성**, **제목**, **전자 메일 주소** 원하는 tooprovision에 유효한 Azure Active Directory 계정의 hello 관련 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-204">Type hello **First Name**, **Last Name**, **Title**, **Email address** of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="4ba97-205">b.</span><span class="sxs-lookup"><span data-stu-id="4ba97-205">b.</span></span> <span data-ttu-id="4ba97-206">**Done**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-206">Click **Done**.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="4ba97-207">hello Azure AD 계정 보유자 수신 되기 전에 링크 tooconfirm hello 계정을 포함 하 여 전자 메일 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-207">hello Azure AD account holder receives an email including a link tooconfirm hello account before it becomes active.</span></span>
   
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4ba97-208">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4ba97-209">이 섹션에서는 too15Five 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too15Five.</span></span>

![사용자 할당][200] 

<span data-ttu-id="4ba97-211">**tooassign Britta Simon too15Five hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4ba97-211">**tooassign Britta Simon too15Five, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ba97-212">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="4ba97-214">Hello 응용 프로그램 목록에서 선택 **15Five**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-214">In hello applications list, select **15Five**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-15five-tutorial/tutorial_15five_app.png) 

3. <span data-ttu-id="4ba97-216">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="4ba97-218">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-218">Click **Add** button.</span></span> <span data-ttu-id="4ba97-219">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="4ba97-221">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4ba97-222">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4ba97-223">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4ba97-224">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="4ba97-224">Testing single sign-on</span></span>

<span data-ttu-id="4ba97-225">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4ba97-226">Hello 액세스 패널에서에서 hello 15Five 타일을 클릭할 때 15Five 응용 프로그램의 로그인 페이지를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-226">When you click hello 15Five tile in hello Access Panel, you should get login page of 15Five application.</span></span>
<span data-ttu-id="4ba97-227">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba97-227">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4ba97-228">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="4ba97-228">Additional resources</span></span>

* [<span data-ttu-id="4ba97-229">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="4ba97-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4ba97-230">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="4ba97-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-15five-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-15five-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-15five-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-15five-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-15five-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-15five-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-15five-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-15five-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-15five-tutorial/tutorial_general_203.png

