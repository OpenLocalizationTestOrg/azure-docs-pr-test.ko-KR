---
title: "자습서: Birst Agile Business Analytics와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Birst Agile 비즈니스 분석 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 677183b1-5348-4302-88cc-5c8ab63a3c6c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: f007edcec0fb8ece215ab69f7ec7ca59ca34bddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-birst-agile-business-analytics"></a><span data-ttu-id="ad40d-103">자습서: Birst Agile Business Analytics와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="ad40d-103">Tutorial: Azure Active Directory integration with Birst Agile Business Analytics</span></span>

<span data-ttu-id="ad40d-104">이 자습서에 설명 어떻게 toointegrate Birst Azure Active Directory (Azure AD)와 Agile 비즈니스 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-104">In this tutorial, you learn how toointegrate Birst Agile Business Analytics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ad40d-105">이점 다음 hello로 제공 Birst Agile 비즈니스 분석을 Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="ad40d-105">Integrating Birst Agile Business Analytics with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ad40d-106">액세스 tooBirst Agile 비즈니스 분석을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-106">You can control in Azure AD who has access tooBirst Agile Business Analytics</span></span>
- <span data-ttu-id="ad40d-107">Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooBirst Agile 비즈니스 분석 (Single Sign-on)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-107">You can enable your users tooautomatically get signed-on tooBirst Agile Business Analytics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ad40d-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ad40d-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad40d-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ad40d-110">Prerequisites</span></span>

<span data-ttu-id="ad40d-111">Agile 비즈니스 분석 Birst와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-111">tooconfigure Azure AD integration with Birst Agile Business Analytics, you need hello following items:</span></span>

- <span data-ttu-id="ad40d-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="ad40d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ad40d-113">Birst Agile Business Analytics Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="ad40d-113">A Birst Agile Business Analytics single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ad40d-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ad40d-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ad40d-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ad40d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ad40d-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ad40d-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="ad40d-118">Scenario description</span></span>
<span data-ttu-id="ad40d-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ad40d-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ad40d-121">Hello 갤러리에서 Birst Agile 비즈니스 분석을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-121">Adding Birst Agile Business Analytics from hello gallery</span></span>
2. <span data-ttu-id="ad40d-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="ad40d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-birst-agile-business-analytics-from-hello-gallery"></a><span data-ttu-id="ad40d-123">Hello 갤러리에서 Birst Agile 비즈니스 분석을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-123">Adding Birst Agile Business Analytics from hello gallery</span></span>
<span data-ttu-id="ad40d-124">tooconfigure hello와의 통합 Birst Agile 비즈니스 분석 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 tooadd Birst Agile 비즈니스 분석 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-124">tooconfigure hello integration of Birst Agile Business Analytics into Azure AD, you need tooadd Birst Agile Business Analytics from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ad40d-125">**tooadd hello 갤러리에서 Agile 비즈니스 분석 Birst hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="ad40d-125">**tooadd Birst Agile Business Analytics from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad40d-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ad40d-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ad40d-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="ad40d-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="ad40d-133">Hello 검색 상자에 입력 **Birst Agile 비즈니스 분석**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-133">In hello search box, type **Birst Agile Business Analytics**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-birst-tutorial/tutorial_birst_search.png)

5. <span data-ttu-id="ad40d-135">Hello 결과 패널에서 선택 **Birst Agile 비즈니스 분석**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-135">In hello results panel, select **Birst Agile Business Analytics**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-birst-tutorial/tutorial_birst_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ad40d-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="ad40d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ad40d-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Birst Agile Business Analytics에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-138">In this section, you configure and test Azure AD single sign-on with Birst Agile Business Analytics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ad40d-139">Single sign on toowork에 대 한 Azure AD는 tooknow Birst Agile 비즈니스 분석에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Birst Agile Business Analytics is tooa user in Azure AD.</span></span> <span data-ttu-id="ad40d-140">즉, Azure AD 사용자 및 hello Birst Agile 비즈니스 분석의 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-140">In other words, a link relationship between an Azure AD user and hello related user in Birst Agile Business Analytics needs toobe established.</span></span>

<span data-ttu-id="ad40d-141">비즈니스 분석을 Agile Birst에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **사용자 이름** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-141">In Birst Agile Business Analytics, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ad40d-142">tooconfigure 및 Birst Agile 비즈니스 분석을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-142">tooconfigure and test Azure AD single sign-on with Birst Agile Business Analytics, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ad40d-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ad40d-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ad40d-145">**[비즈니스 분석을 Agile Birst 테스트 사용자 만들기](#creating-a-birst-agile-business-analytics-test-user)**  -toohave Britta Simon 표현인 연결 된 toohello Azure AD 사용자의 Birst Agile 비즈니스 분석에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-145">**[Creating a Birst Agile Business Analytics test user](#creating-a-birst-agile-business-analytics-test-user)** - toohave a counterpart of Britta Simon in Birst Agile Business Analytics that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ad40d-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ad40d-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="ad40d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ad40d-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="ad40d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ad40d-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 및 Birst Agile 비즈니스 분석 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Birst Agile Business Analytics application.</span></span>

<span data-ttu-id="ad40d-150">**Birst 민첩 하는 비즈니스 분석을 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="ad40d-150">**tooconfigure Azure AD single sign-on with Birst Agile Business Analytics, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad40d-151">Hello hello에 Azure 포털에서에서 **Birst Agile 비즈니스 분석** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-151">In hello Azure portal, on hello **Birst Agile Business Analytics** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="ad40d-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-birst-tutorial/tutorial_birst_samlbase.png)

3. <span data-ttu-id="ad40d-155">Hello에 **Birst Agile 비즈니스 분석 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-155">On hello **Birst Agile Business Analytics Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-birst-tutorial/tutorial_birst_url.png)

     <span data-ttu-id="ad40d-157">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="ad40d-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

     <span data-ttu-id="ad40d-158">hello URL hello 데이터 센터 Birst 계정이 있는 인지에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-158">hello URL depends on hello datacenter that your Birst account is located:</span></span> 

     * <span data-ttu-id="ad40d-159">미국 datacenter 사용할 hello 패턴:`https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="ad40d-159">For US datacenter use following hello pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span> 

     * <span data-ttu-id="ad40d-160">Europe에 대 한 데이터 센터 패턴 hello를 사용 합니다.`https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="ad40d-160">For Europe datacenter use hello following pattern: `https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ad40d-161">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-161">This value is not real.</span></span> <span data-ttu-id="ad40d-162">업데이트 hello 값과 실제 로그온 URL hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-162">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="ad40d-163">연락처 [Birst Agile 비즈니스 분석 클라이언트 지원 팀](mailto:info@birst.com) tooget hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-163">Contact [Birst Agile Business Analytics Client support team](mailto:info@birst.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="ad40d-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-birst-tutorial/tutorial_birst_certificate.png) 

5. <span data-ttu-id="ad40d-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-birst-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ad40d-168">Hello에 **Birst Agile 비즈니스 분석 구성** 섹션에서 클릭 **구성 Birst Agile 비즈니스 분석** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="ad40d-168">On hello **Birst Agile Business Analytics Configuration** section, click **Configure Birst Agile Business Analytics** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ad40d-169">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="ad40d-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-birst-tutorial/tutorial_birst_configure.png) 

7. <span data-ttu-id="ad40d-171">tooconfigure single sign on에서 **Birst Agile 비즈니스 분석** toosend hello 다운로드 해야 쪽에서는 **인증서 (Base64)**, **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** 너무[Birst Agile 비즈니스 분석 지원 팀](mailto:info@birst.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-171">tooconfigure single sign-on on **Birst Agile Business Analytics** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Birst Agile Business Analytics support team](mailto:info@birst.com).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="ad40d-172">TooBirst 팀이이 통합 SHA256 알고리즘을 해야 함을 알려주십시오 (SHA1 지원 되지 것입니다)와 같은 적절 한 서버 hello에 hello SSO를 설정할 수 있습니다 **app2101** 등입니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-172">Mention tooBirst team that this integration needs SHA256 Algorithm (SHA1 will not be supported) so that they can set hello SSO on hello appropriate server like **app2101** etc.</span></span>
  

> [!TIP]
> <span data-ttu-id="ad40d-173">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="ad40d-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ad40d-174">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="ad40d-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ad40d-175">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ad40d-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ad40d-176">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="ad40d-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="ad40d-177">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="ad40d-179">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="ad40d-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad40d-180">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-birst-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ad40d-182">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-birst-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ad40d-184">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-birst-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ad40d-186">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-birst-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ad40d-188">a.</span><span class="sxs-lookup"><span data-stu-id="ad40d-188">a.</span></span> <span data-ttu-id="ad40d-189">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ad40d-190">b.</span><span class="sxs-lookup"><span data-stu-id="ad40d-190">b.</span></span> <span data-ttu-id="ad40d-191">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ad40d-192">c.</span><span class="sxs-lookup"><span data-stu-id="ad40d-192">c.</span></span> <span data-ttu-id="ad40d-193">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ad40d-194">d.</span><span class="sxs-lookup"><span data-stu-id="ad40d-194">d.</span></span> <span data-ttu-id="ad40d-195">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-195">Click **Create**.</span></span>
 
### <a name="creating-a-birst-agile-business-analytics-test-user"></a><span data-ttu-id="ad40d-196">Birst Agile Business Analytics 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="ad40d-196">Creating a Birst Agile Business Analytics test user</span></span>

<span data-ttu-id="ad40d-197">hello이이 섹션의 목적은 toocreate Britta Simon Birst Agile 비즈니스 분석에서 호출 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-197">hello objective of this section is toocreate a user called Britta Simon in Birst Agile Business Analytics.</span></span> <span data-ttu-id="ad40d-198">작업할 [Birst Agile 비즈니스 분석 지원 팀](mailto:info@birst.com) hello Birst 계정에서에서 tooadd hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-198">Work with [Birst Agile Business Analytics support team](mailto:info@birst.com) tooadd hello users in hello Birst account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ad40d-199">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ad40d-200">이 섹션에서는 액세스 tooBirst Agile 비즈니스 분석을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBirst Agile Business Analytics.</span></span>

![사용자 할당][200] 

<span data-ttu-id="ad40d-202">**tooassign Britta Simon tooBirst Agile 비즈니스 분석 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="ad40d-202">**tooassign Britta Simon tooBirst Agile Business Analytics, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad40d-203">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="ad40d-205">Hello 응용 프로그램 목록에서 선택 **Birst Agile 비즈니스 분석**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-205">In hello applications list, select **Birst Agile Business Analytics**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-birst-tutorial/tutorial_birst_app.png) 

3. <span data-ttu-id="ad40d-207">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="ad40d-209">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-209">Click **Add** button.</span></span> <span data-ttu-id="ad40d-210">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="ad40d-212">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ad40d-213">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ad40d-214">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ad40d-215">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="ad40d-215">Testing single sign-on</span></span>

<span data-ttu-id="ad40d-216">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD SSO 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-216">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="ad40d-217">Hello Birst Agile 비즈니스 분석 hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour Birst Agile 비즈니스 분석 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40d-217">When you click hello Birst Agile Business Analytics tile in hello Access Panel, you should get automatically signed-on tooyour Birst Agile Business Analytics application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ad40d-218">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="ad40d-218">Additional resources</span></span>

* [<span data-ttu-id="ad40d-219">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="ad40d-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ad40d-220">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="ad40d-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-birst-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-birst-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-birst-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-birst-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-birst-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-birst-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-birst-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-birst-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-birst-tutorial/tutorial_general_203.png

