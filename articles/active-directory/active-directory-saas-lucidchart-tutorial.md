---
title: "자습서: Lucidchart와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Lucidchart 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1068d364-11f3-43b5-bd6d-26f00ecd5baa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 774e5f423097650a3cae8e8ca13b2c65b8470736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lucidchart"></a><span data-ttu-id="814de-103">자습서: Lucidchart와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="814de-103">Tutorial: Azure Active Directory integration with Lucidchart</span></span>

<span data-ttu-id="814de-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 Lucidchart 합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-104">In this tutorial, you learn how toointegrate Lucidchart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="814de-105">Azure AD와 Lucidchart 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-105">Integrating Lucidchart with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="814de-106">액세스 tooLucidchart을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="814de-106">You can control in Azure AD who has access tooLucidchart</span></span>
- <span data-ttu-id="814de-107">프로그램 사용자 tooautomatically get 로그온 tooLucidchart (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="814de-107">You can enable your users tooautomatically get signed-on tooLucidchart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="814de-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="814de-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="814de-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="814de-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="814de-110">Prerequisites</span></span>

<span data-ttu-id="814de-111">Lucidchart와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-111">tooconfigure Azure AD integration with Lucidchart, you need hello following items:</span></span>

- <span data-ttu-id="814de-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="814de-112">An Azure AD subscription</span></span>
- <span data-ttu-id="814de-113">Lucidchart Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="814de-113">A Lucidchart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="814de-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="814de-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="814de-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="814de-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="814de-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="814de-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="814de-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="814de-118">Scenario description</span></span>
<span data-ttu-id="814de-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="814de-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="814de-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="814de-121">Lucidchart는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="814de-121">Adding Lucidchart from hello gallery</span></span>
2. <span data-ttu-id="814de-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="814de-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lucidchart-from-hello-gallery"></a><span data-ttu-id="814de-123">Lucidchart는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="814de-123">Adding Lucidchart from hello gallery</span></span>
<span data-ttu-id="814de-124">tooconfigure hello와의 통합 Lucidchart Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Lucidchart tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-124">tooconfigure hello integration of Lucidchart into Azure AD, you need tooadd Lucidchart from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="814de-125">**hello 갤러리에서 Lucidchart tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="814de-125">**tooadd Lucidchart from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="814de-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="814de-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="814de-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="814de-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="814de-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="814de-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="814de-133">Hello 검색 상자에 입력 **Lucidchart**합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-133">In hello search box, type **Lucidchart**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_search.png)

5. <span data-ttu-id="814de-135">Hello 결과 패널에서 선택 **Lucidchart**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="814de-135">In hello results panel, select **Lucidchart**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="814de-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="814de-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="814de-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Lucidchart에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-138">In this section, you configure and test Azure AD single sign-on with Lucidchart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="814de-139">Single sign on toowork에 대 한 Azure AD는 tooknow Lucidchart에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lucidchart is tooa user in Azure AD.</span></span> <span data-ttu-id="814de-140">즉, Azure AD 사용자와 Lucidchart에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-140">In other words, a link relationship between an Azure AD user and hello related user in Lucidchart needs toobe established.</span></span>

<span data-ttu-id="814de-141">Hello hello 값을 할당, Lucidchart에서 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="814de-141">In Lucidchart, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="814de-142">tooconfigure와 Lucidchart 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-142">tooconfigure and test Azure AD single sign-on with Lucidchart, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="814de-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="814de-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="814de-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="814de-145">**[Lucidchart 테스트 사용자 만들기](#creating-a-lucidchart-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Lucidchart에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="814de-145">**[Creating a Lucidchart test user](#creating-a-lucidchart-test-user)** - toohave a counterpart of Britta Simon in Lucidchart that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="814de-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="814de-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="814de-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="814de-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="814de-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="814de-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="814de-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Lucidchart 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lucidchart application.</span></span>

<span data-ttu-id="814de-150">**Azure AD tooconfigure single sign on와 Lucidchart를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="814de-150">**tooconfigure Azure AD single sign-on with Lucidchart, perform hello following steps:**</span></span>

1. <span data-ttu-id="814de-151">Hello hello에 Azure 포털에서에서 **Lucidchart** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-151">In hello Azure portal, on hello **Lucidchart** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="814de-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="814de-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_samlbase.png)

3. <span data-ttu-id="814de-155">Hello에 **Lucidchart 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-155">On hello **Lucidchart Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_url.png)

    <span data-ttu-id="814de-157">Hello에 **로그온 URL** 텍스트 상자에 다음 URL로:`https://chart2.office.lucidchart.com/saml/sso/azure`</span><span class="sxs-lookup"><span data-stu-id="814de-157">In hello **Sign-on URL** textbox, type a URL as: `https://chart2.office.lucidchart.com/saml/sso/azure`</span></span>

4. <span data-ttu-id="814de-158">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-158">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_certificate.png) 

5. <span data-ttu-id="814de-160">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-160">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lucidchart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="814de-162">다른 웹 브라우저 창에서 Lucidchart 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-162">In a different web browser window, log into your Lucidchart company site as an administrator.</span></span>

7. <span data-ttu-id="814de-163">Hello 메뉴에서 hello 위에 표시를 클릭 **팀**합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-163">In hello menu on hello top, click **Team**.</span></span>
   
    <span data-ttu-id="814de-164">![팀](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "팀")</span><span class="sxs-lookup"><span data-stu-id="814de-164">![Team](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Team")</span></span>

8. <span data-ttu-id="814de-165">**응용 프로그램 \> SAML 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-165">Click **Applications \> Manage SAML**.</span></span>
   
    <span data-ttu-id="814de-166">![SAML 관리](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "SAML 관리")</span><span class="sxs-lookup"><span data-stu-id="814de-166">![Manage SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Manage SAML")</span></span>

9. <span data-ttu-id="814de-167">Hello에 **SAML 인증 설정** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-167">On hello **SAML Authentication Settings** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="814de-168">a.</span><span class="sxs-lookup"><span data-stu-id="814de-168">a.</span></span> <span data-ttu-id="814de-169">**SAML 인증 사용**을 선택한 다음 **옵션**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-169">Select **Enable SAML Authentication**, and then click **Optional**.</span></span>

    <span data-ttu-id="814de-170">![SAML 인증 설정](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML 인증 설정")</span><span class="sxs-lookup"><span data-stu-id="814de-170">![SAML Authentication Settings](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML Authentication Settings")</span></span>
 
    <span data-ttu-id="814de-171">b.</span><span class="sxs-lookup"><span data-stu-id="814de-171">b.</span></span> <span data-ttu-id="814de-172">Hello에 **도메인** 텍스트 상자에 도메인을 입력 한 다음 클릭 **인증서 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-172">In hello **Domain** textbox, type your domain, and then click **Change Certificate**.</span></span>

    <span data-ttu-id="814de-173">![인증서 변경](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "인증서 변경")</span><span class="sxs-lookup"><span data-stu-id="814de-173">![Change Certificate](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Change Certificate")</span></span>
 
    <span data-ttu-id="814de-174">c.</span><span class="sxs-lookup"><span data-stu-id="814de-174">c.</span></span> <span data-ttu-id="814de-175">다운로드 한 메타 데이터 파일, 콘텐츠를 복사 hello를 연 다음 hello에 붙여 넣을 **메타 데이터 업로드** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="814de-175">Open your downloaded metadata file, copy hello content, and then paste it into hello **Upload Metadata** textbox.</span></span>

    <span data-ttu-id="814de-176">![메타데이터 업로드](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "메타데이터 업로드")</span><span class="sxs-lookup"><span data-stu-id="814de-176">![Upload Metadata](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Upload Metadata")</span></span>
 
    <span data-ttu-id="814de-177">d.</span><span class="sxs-lookup"><span data-stu-id="814de-177">d.</span></span> <span data-ttu-id="814de-178">선택 **새 사용자 toohello 팀 자동으로 추가**, 클릭 하 고 **ब ा ळ**합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-178">Select **Automatically Add new users toohello team**, and then click **Save changes**.</span></span>

    <span data-ttu-id="814de-179">![변경 내용 저장](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "변경 내용 저장")</span><span class="sxs-lookup"><span data-stu-id="814de-179">![Save Changes](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Save Changes")</span></span>

> [!TIP]
> <span data-ttu-id="814de-180">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="814de-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="814de-181">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="814de-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="814de-182">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="814de-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="814de-183">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="814de-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="814de-184">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="814de-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="814de-186">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="814de-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="814de-187">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="814de-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="814de-189">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="814de-191">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="814de-193">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="814de-195">a.</span><span class="sxs-lookup"><span data-stu-id="814de-195">a.</span></span> <span data-ttu-id="814de-196">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="814de-197">b.</span><span class="sxs-lookup"><span data-stu-id="814de-197">b.</span></span> <span data-ttu-id="814de-198">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="814de-199">c.</span><span class="sxs-lookup"><span data-stu-id="814de-199">c.</span></span> <span data-ttu-id="814de-200">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="814de-201">d.</span><span class="sxs-lookup"><span data-stu-id="814de-201">d.</span></span> <span data-ttu-id="814de-202">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-202">Click **Create**.</span></span>
 
### <a name="creating-a-lucidchart-test-user"></a><span data-ttu-id="814de-203">Lucidchart 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="814de-203">Creating a Lucidchart test user</span></span>

<span data-ttu-id="814de-204">사용자에 대 한 있습니다 tooconfigure tooLucidchart 프로 비전 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="814de-204">There is no action item for you tooconfigure user provisioning tooLucidchart.</span></span>  <span data-ttu-id="814de-205">Toolog hello 액세스 패널을 사용 하 여 Lucidchart에 시도 하는 할당된 된 사용자, Lucidchart hello 사용자의 존재 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-205">When an assigned user tries toolog into Lucidchart using hello access panel, Lucidchart checks whether hello user exists.</span></span>  

<span data-ttu-id="814de-206">사용할 수 있는 사용자 계정이 없으면 자동으로 Lucidchart에 의해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="814de-206">If there is no user account available yet, it is automatically created by Lucidchart.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="814de-207">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="814de-208">이 섹션에서는 tooLucidchart 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLucidchart.</span></span>

![사용자 할당][200] 

<span data-ttu-id="814de-210">**tooassign Britta Simon tooLucidchart hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="814de-210">**tooassign Britta Simon tooLucidchart, perform hello following steps:**</span></span>

1. <span data-ttu-id="814de-211">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="814de-213">Hello 응용 프로그램 목록에서 선택 **Lucidchart**합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-213">In hello applications list, select **Lucidchart**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_app.png) 

3. <span data-ttu-id="814de-215">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="814de-217">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-217">Click **Add** button.</span></span> <span data-ttu-id="814de-218">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="814de-220">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="814de-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="814de-221">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="814de-222">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="814de-223">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="814de-223">Testing single sign-on</span></span>

<span data-ttu-id="814de-224">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="814de-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="814de-225">Hello 액세스 패널에서에서 hello Lucidchart 타일을 클릭할 때 자동으로 로그온 tooyour Lucidchart 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-225">When you click hello Lucidchart tile in hello Access Panel, you should get automatically signed-on tooyour Lucidchart application.</span></span>
<span data-ttu-id="814de-226">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="814de-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="814de-227">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="814de-227">Additional resources</span></span>

* [<span data-ttu-id="814de-228">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="814de-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="814de-229">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="814de-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_203.png

