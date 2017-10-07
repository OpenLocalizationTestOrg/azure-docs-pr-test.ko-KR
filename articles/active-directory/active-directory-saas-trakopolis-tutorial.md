---
title: "자습서: Trakopolis와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Trakopolis 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 73d67c3e-4b4b-4d3b-aa58-6699ea1ccea3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 00f9b21c0a837d1d9fbbd9135367fae4b02db934
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trakopolis"></a><span data-ttu-id="c0f33-103">자습서: Trakopolis와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="c0f33-103">Tutorial: Azure Active Directory integration with Trakopolis</span></span>

<span data-ttu-id="c0f33-104">이 자습서에 설명 어떻게 toointegrate Trakopolis Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c0f33-104">In this tutorial, you learn how toointegrate Trakopolis with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c0f33-105">다음 이점을 hello로 제공 Trakopolis Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="c0f33-105">Integrating Trakopolis with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c0f33-106">액세스 tooTrakopolis을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-106">You can control in Azure AD who has access tooTrakopolis</span></span>
- <span data-ttu-id="c0f33-107">프로그램 사용자 tooautomatically get 로그온 tooTrakopolis (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-107">You can enable your users tooautomatically get signed-on tooTrakopolis (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c0f33-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c0f33-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0f33-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c0f33-110">Prerequisites</span></span>

<span data-ttu-id="c0f33-111">다음 항목 hello가 필요 tooconfigure Trakopolis와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-111">tooconfigure Azure AD integration with Trakopolis, you need hello following items:</span></span>

- <span data-ttu-id="c0f33-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="c0f33-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c0f33-113">Trakopolis Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="c0f33-113">A Trakopolis single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c0f33-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c0f33-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c0f33-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c0f33-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c0f33-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c0f33-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="c0f33-118">Scenario description</span></span>
<span data-ttu-id="c0f33-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c0f33-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c0f33-121">Trakopolis는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="c0f33-121">Adding Trakopolis from hello gallery</span></span>
2. <span data-ttu-id="c0f33-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c0f33-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trakopolis-from-hello-gallery"></a><span data-ttu-id="c0f33-123">Trakopolis는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="c0f33-123">Adding Trakopolis from hello gallery</span></span>
<span data-ttu-id="c0f33-124">tooconfigure hello와의 통합 Trakopolis Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Trakopolis tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-124">tooconfigure hello integration of Trakopolis into Azure AD, you need tooadd Trakopolis from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c0f33-125">**hello 갤러리에서 Trakopolis tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c0f33-125">**tooadd Trakopolis from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0f33-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c0f33-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c0f33-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="c0f33-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="c0f33-133">Hello 검색 상자에 입력 **Trakopolis**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-133">In hello search box, type **Trakopolis**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_search.png)

5. <span data-ttu-id="c0f33-135">Hello 결과 패널에서 선택 **Trakopolis**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-135">In hello results panel, select **Trakopolis**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c0f33-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c0f33-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c0f33-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Trakopolis에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-138">In this section, you configure and test Azure AD single sign-on with Trakopolis based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c0f33-139">Single sign on toowork에 대 한 Azure AD는 tooknow Trakopolis에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Trakopolis is tooa user in Azure AD.</span></span> <span data-ttu-id="c0f33-140">즉, Azure AD 사용자 및 Trakopolis에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-140">In other words, a link relationship between an Azure AD user and hello related user in Trakopolis needs toobe established.</span></span>

<span data-ttu-id="c0f33-141">Trakopolis에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-141">In Trakopolis, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c0f33-142">tooconfigure 및 Trakopolis 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-142">tooconfigure and test Azure AD single sign-on with Trakopolis, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c0f33-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c0f33-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c0f33-145">**[Trakopolis 테스트 사용자 만들기](#creating-a-trakopolis-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Trakopolis에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-145">**[Creating a Trakopolis test user](#creating-a-trakopolis-test-user)** - toohave a counterpart of Britta Simon in Trakopolis that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c0f33-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c0f33-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="c0f33-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c0f33-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="c0f33-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c0f33-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Trakopolis 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Trakopolis application.</span></span>

<span data-ttu-id="c0f33-150">**tooconfigure Azure AD single sign on, Trakopolis와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c0f33-150">**tooconfigure Azure AD single sign-on with Trakopolis, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0f33-151">Hello hello에 Azure 포털에서에서 **Trakopolis** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-151">In hello Azure portal, on hello **Trakopolis** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="c0f33-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_samlbase.png)

3. <span data-ttu-id="c0f33-155">Hello에 **Trakopolis 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-155">On hello **Trakopolis Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_url.png)

    <span data-ttu-id="c0f33-157">a.</span><span class="sxs-lookup"><span data-stu-id="c0f33-157">a.</span></span> <span data-ttu-id="c0f33-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<company name>.trakopolis.com/`</span><span class="sxs-lookup"><span data-stu-id="c0f33-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.trakopolis.com/`</span></span>

    <span data-ttu-id="c0f33-159">b.</span><span class="sxs-lookup"><span data-stu-id="c0f33-159">b.</span></span> <span data-ttu-id="c0f33-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<company name>.trakopolis.com`</span><span class="sxs-lookup"><span data-stu-id="c0f33-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.trakopolis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c0f33-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-161">These values are not real.</span></span> <span data-ttu-id="c0f33-162">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c0f33-163">연락처 [Trakopolis 클라이언트 지원 팀](mailto:support@cantelematics.com) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-163">Contact [Trakopolis Client support team](mailto:support@cantelematics.com) tooget these values.</span></span> 

4. <span data-ttu-id="c0f33-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_certificate.png) 

5. <span data-ttu-id="c0f33-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-trakopolis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c0f33-168">Hello에 **Trakopolis 구성** 섹션에서 클릭 **구성 Trakopolis** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="c0f33-168">On hello **Trakopolis Configuration** section, click **Configure Trakopolis** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c0f33-169">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="c0f33-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_configure.png) 

7. <span data-ttu-id="c0f33-171">tooconfigure single sign on에서 **Trakopolis** toosend hello 다운로드 해야 쪽에서는 **메타 데이터 XML, 로그 아웃 URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** 너무[Trakopolis 지원 팀](mailto:support@cantelematics.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-171">tooconfigure single sign-on on **Trakopolis** side, you need toosend hello downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Trakopolis support team](mailto:support@cantelematics.com).</span></span> <span data-ttu-id="c0f33-172">이 설정은 toohave hello 양쪽 모두에 제대로 설정 하는 SAML SSO 연결 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c0f33-173">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="c0f33-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c0f33-174">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="c0f33-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c0f33-175">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c0f33-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c0f33-176">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c0f33-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="c0f33-177">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="c0f33-179">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c0f33-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0f33-180">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c0f33-182">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c0f33-184">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c0f33-186">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c0f33-188">a.</span><span class="sxs-lookup"><span data-stu-id="c0f33-188">a.</span></span> <span data-ttu-id="c0f33-189">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c0f33-190">b.</span><span class="sxs-lookup"><span data-stu-id="c0f33-190">b.</span></span> <span data-ttu-id="c0f33-191">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c0f33-192">c.</span><span class="sxs-lookup"><span data-stu-id="c0f33-192">c.</span></span> <span data-ttu-id="c0f33-193">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c0f33-194">d.</span><span class="sxs-lookup"><span data-stu-id="c0f33-194">d.</span></span> <span data-ttu-id="c0f33-195">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-195">Click **Create**.</span></span>
 
### <a name="creating-a-trakopolis-test-user"></a><span data-ttu-id="c0f33-196">Trakopolis 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c0f33-196">Creating a Trakopolis test user</span></span>

<span data-ttu-id="c0f33-197">이 섹션에서는 Trakopolis에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-197">In this section, you create a user called Britta Simon in Trakopolis.</span></span> <span data-ttu-id="c0f33-198">작업할 [Trakopolis 지원 팀](mailto:support@cantelematics.com) hello 사용자 hello Trakopolis 플랫폼을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-198">Work with [Trakopolis support team](mailto:support@cantelematics.com) to add hello users in hello Trakopolis platform.</span></span> <span data-ttu-id="c0f33-199">Single Sign-On을 사용하려면 먼저 사용자를 만들고 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-199">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c0f33-200">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c0f33-201">이 섹션에서는 tooTrakopolis 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTrakopolis.</span></span>

![사용자 할당][200] 

<span data-ttu-id="c0f33-203">**tooassign Britta Simon tooTrakopolis hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c0f33-203">**tooassign Britta Simon tooTrakopolis, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0f33-204">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="c0f33-206">Hello 응용 프로그램 목록에서 선택 **Trakopolis**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-206">In hello applications list, select **Trakopolis**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_app.png) 

3. <span data-ttu-id="c0f33-208">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="c0f33-210">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-210">Click **Add** button.</span></span> <span data-ttu-id="c0f33-211">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="c0f33-213">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c0f33-214">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c0f33-215">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c0f33-216">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="c0f33-216">Testing single sign-on</span></span>

<span data-ttu-id="c0f33-217">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-217">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="c0f33-218">Hello Trakopolis hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour Trakopolis 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0f33-218">When you click hello Trakopolis tile in hello Access Panel, you should get automatically signed-on tooyour Trakopolis application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c0f33-219">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="c0f33-219">Additional resources</span></span>

* [<span data-ttu-id="c0f33-220">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="c0f33-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c0f33-221">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="c0f33-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_203.png

