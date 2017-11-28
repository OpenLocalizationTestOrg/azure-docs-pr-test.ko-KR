---
title: "자습서: Alcumus 정보 교환과 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Alcumus 정보 Exchange 간의 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d26034b8-f0d5-4f65-aa56-0fc168ceec8c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 4ef9f4d654b6c451db44f929bdad1016304168b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-alcumus-info-exchange"></a><span data-ttu-id="0dd35-103">자습서: Alcumus 정보 교환과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="0dd35-103">Tutorial: Azure Active Directory integration with Alcumus Info Exchange</span></span>

<span data-ttu-id="0dd35-104">이 자습서에 설명 toointegrate Alcumus 정보를 Azure Active Directory (Azure AD)와 교환 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-104">In this tutorial, you learn how toointegrate Alcumus Info Exchange with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0dd35-105">다음 이점을 hello로 제공 Alcumus 정보 Exchange Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="0dd35-105">Integrating Alcumus Info Exchange with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0dd35-106">Azure ad 액세스 tooAlcumus 정보 Exchange가 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-106">You can control in Azure AD who has access tooAlcumus Info Exchange</span></span>
- <span data-ttu-id="0dd35-107">Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooAlcumus 정보 교환 (Single Sign-on)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-107">You can enable your users tooautomatically get signed-on tooAlcumus Info Exchange (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0dd35-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0dd35-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0dd35-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0dd35-110">Prerequisites</span></span>

<span data-ttu-id="0dd35-111">다음 항목 hello가 필요 tooconfigure Alcumus 정보 Exchange와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-111">tooconfigure Azure AD integration with Alcumus Info Exchange, you need hello following items:</span></span>

- <span data-ttu-id="0dd35-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="0dd35-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0dd35-113">Alcumus Info Exchange Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="0dd35-113">An Alcumus Info Exchange single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0dd35-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0dd35-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0dd35-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="0dd35-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0dd35-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0dd35-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="0dd35-118">Scenario description</span></span>
<span data-ttu-id="0dd35-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0dd35-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0dd35-121">Alcumus 정보 Exchange hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="0dd35-121">Adding Alcumus Info Exchange from hello gallery</span></span>
2. <span data-ttu-id="0dd35-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="0dd35-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-alcumus-info-exchange-from-hello-gallery"></a><span data-ttu-id="0dd35-123">Alcumus 정보 Exchange hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="0dd35-123">Adding Alcumus Info Exchange from hello gallery</span></span>
<span data-ttu-id="0dd35-124">tooconfigure hello와의 통합 Alcumus 정보 Exchange Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 tooadd Alcumus 정보 교환 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-124">tooconfigure hello integration of Alcumus Info Exchange into Azure AD, you need tooadd Alcumus Info Exchange from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0dd35-125">**hello 갤러리에서 Alcumus 정보 Exchange tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0dd35-125">**tooadd Alcumus Info Exchange from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dd35-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0dd35-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0dd35-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="0dd35-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="0dd35-133">Hello 검색 상자에 입력 **Alcumus 정보 Exchange**합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-133">In hello search box, type **Alcumus Info Exchange**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_search.png)

5. <span data-ttu-id="0dd35-135">Hello 결과 패널에서 선택 **Alcumus 정보 Exchange**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-135">In hello results panel, select **Alcumus Info Exchange**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0dd35-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="0dd35-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0dd35-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Alcumus Info Exchange에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-138">In this section, you configure and test Azure AD single sign-on with Alcumus Info Exchange based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0dd35-139">Single sign on toowork에 대 한 Azure AD는 tooknow Alcumus 정보 교환에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Alcumus Info Exchange is tooa user in Azure AD.</span></span> <span data-ttu-id="0dd35-140">즉, Azure AD 사용자 및 Alcumus 정보 교환에서 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-140">In other words, a link relationship between an Azure AD user and hello related user in Alcumus Info Exchange needs toobe established.</span></span>

<span data-ttu-id="0dd35-141">Alcumus 정보 교환에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-141">In Alcumus Info Exchange, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0dd35-142">tooconfigure 및 Alcumus 정보 Exchange를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-142">tooconfigure and test Azure AD single sign-on with Alcumus Info Exchange, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0dd35-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0dd35-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0dd35-145">**[Alcumus 정보 Exchange 테스트 사용자 만들기](#creating-an-alcumus-info-exchange-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Alcumus 정보 교환에서 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-145">**[Creating an Alcumus Info Exchange test user](#creating-an-alcumus-info-exchange-test-user)** - toohave a counterpart of Britta Simon in Alcumus Info Exchange that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0dd35-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0dd35-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="0dd35-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0dd35-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="0dd35-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0dd35-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Alcumus 정보 Exchange 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Alcumus Info Exchange application.</span></span>

<span data-ttu-id="0dd35-150">**Alcumus 정보 Exchange와 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0dd35-150">**tooconfigure Azure AD single sign-on with Alcumus Info Exchange, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dd35-151">Hello hello에 Azure 포털에서에서 **Alcumus 정보 Exchange** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-151">In hello Azure portal, on hello **Alcumus Info Exchange** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="0dd35-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_samlbase.png)

3. <span data-ttu-id="0dd35-155">Hello에 **Alcumus 정보 Exchange 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-155">On hello **Alcumus Info Exchange Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_url.png)

    <span data-ttu-id="0dd35-157">a.</span><span class="sxs-lookup"><span data-stu-id="0dd35-157">a.</span></span> <span data-ttu-id="0dd35-158">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.info-exchange.com`</span><span class="sxs-lookup"><span data-stu-id="0dd35-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.info-exchange.com`</span></span>

    <span data-ttu-id="0dd35-159">b.</span><span class="sxs-lookup"><span data-stu-id="0dd35-159">b.</span></span> <span data-ttu-id="0dd35-160">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.info-exchange.com/Auth/`</span><span class="sxs-lookup"><span data-stu-id="0dd35-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.info-exchange.com/Auth/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0dd35-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-161">These values are not real.</span></span> <span data-ttu-id="0dd35-162">Hello 실제 식별자 및 회신 URL로이 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="0dd35-163">연락처 [Alcumus 정보 Exchange 지원 팀](mailto:helpdesk@alcumusgroup.com) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-163">Contact [Alcumus Info Exchange support team](mailto:helpdesk@alcumusgroup.com) tooget these values.</span></span>
 
4. <span data-ttu-id="0dd35-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_certificate.png) 

5. <span data-ttu-id="0dd35-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0dd35-168">tooconfigure single sign on에서 **Alcumus 정보 Exchange** toosend hello 다운로드 해야 쪽에서는 **메타 데이터 XML** 너무[Alcumus 정보 Exchange 지원 팀](mailto:helpdesk@alcumusgroup.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-168">tooconfigure single sign-on on **Alcumus Info Exchange** side, you need toosend hello downloaded **Metadata XML** too[Alcumus Info Exchange support team](mailto:helpdesk@alcumusgroup.com).</span></span>

> [!TIP]
> <span data-ttu-id="0dd35-169">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="0dd35-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0dd35-170">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="0dd35-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0dd35-171">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0dd35-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0dd35-172">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="0dd35-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="0dd35-173">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="0dd35-175">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0dd35-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dd35-176">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0dd35-178">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0dd35-180">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0dd35-182">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0dd35-184">a.</span><span class="sxs-lookup"><span data-stu-id="0dd35-184">a.</span></span> <span data-ttu-id="0dd35-185">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0dd35-186">b.</span><span class="sxs-lookup"><span data-stu-id="0dd35-186">b.</span></span> <span data-ttu-id="0dd35-187">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0dd35-188">c.</span><span class="sxs-lookup"><span data-stu-id="0dd35-188">c.</span></span> <span data-ttu-id="0dd35-189">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0dd35-190">d.</span><span class="sxs-lookup"><span data-stu-id="0dd35-190">d.</span></span> <span data-ttu-id="0dd35-191">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-191">Click **Create**.</span></span>
 
### <a name="creating-an-alcumus-info-exchange-test-user"></a><span data-ttu-id="0dd35-192">Alcumus Info Exchange 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="0dd35-192">Creating an Alcumus Info Exchange test user</span></span>

<span data-ttu-id="0dd35-193">hello이이 섹션의 목적은 toocreate Alcumus 정보 교환에서 Britta Simon 라고 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-193">hello objective of this section is toocreate a user called Britta Simon in Alcumus Info Exchange.</span></span>

<span data-ttu-id="0dd35-194">toocreate Britta Simon Alcumus 정보 exchange에서 연락처 hello 라는 사용자를 만들면 [Alcumus 정보 Exchange 지원 팀](mailto:helpdesk@alcumusgroup.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-194">toocreate a user called Britta Simon in Alcumus Info Exchange, Contact hello [Alcumus Info Exchange support team](mailto:helpdesk@alcumusgroup.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0dd35-195">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0dd35-196">이 섹션에서는 액세스 tooAlcumus 정보 Exchange 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAlcumus Info Exchange.</span></span>

![사용자 할당][200] 

<span data-ttu-id="0dd35-198">**tooassign Britta Simon tooAlcumus 정보 Exchange hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0dd35-198">**tooassign Britta Simon tooAlcumus Info Exchange, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dd35-199">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-199">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="0dd35-201">Hello 응용 프로그램 목록에서 선택 **Alcumus 정보 Exchange**합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-201">In hello applications list, select **Alcumus Info Exchange**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_app.png) 

3. <span data-ttu-id="0dd35-203">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="0dd35-205">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-205">Click **Add** button.</span></span> <span data-ttu-id="0dd35-206">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="0dd35-208">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0dd35-209">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0dd35-210">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0dd35-211">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="0dd35-211">Testing single sign-on</span></span>

<span data-ttu-id="0dd35-212">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-212">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="0dd35-213">Hello 액세스 패널에서에서 hello Alcumus 정보 Exchange 타일을 클릭할 때 자동으로 로그온 tooyour Alcumus 정보 Exchange 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dd35-213">When you click hello Alcumus Info Exchange tile in hello Access Panel, you should get automatically signed-on tooyour Alcumus Info Exchange application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0dd35-214">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="0dd35-214">Additional resources</span></span>

* [<span data-ttu-id="0dd35-215">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="0dd35-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0dd35-216">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="0dd35-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_203.png

