---
title: "자습서: Egnyte와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Egnyte 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: d86fa28a1e7b23474cb76c08aef8539acadaf24d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a><span data-ttu-id="7667d-103">자습서: Egnyte와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="7667d-103">Tutorial: Azure Active Directory integration with Egnyte</span></span>

<span data-ttu-id="7667d-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 Egnyte 합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-104">In this tutorial, you learn how toointegrate Egnyte with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7667d-105">Azure AD와 Egnyte 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-105">Integrating Egnyte with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7667d-106">액세스 tooEgnyte을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-106">You can control in Azure AD who has access tooEgnyte</span></span>
- <span data-ttu-id="7667d-107">프로그램 사용자 tooautomatically get 로그온 tooEgnyte (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-107">You can enable your users tooautomatically get signed-on tooEgnyte (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7667d-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7667d-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7667d-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7667d-110">Prerequisites</span></span>

<span data-ttu-id="7667d-111">Egnyte와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-111">tooconfigure Azure AD integration with Egnyte, you need hello following items:</span></span>

- <span data-ttu-id="7667d-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="7667d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7667d-113">Egnyte Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="7667d-113">An Egnyte single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7667d-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7667d-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7667d-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="7667d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7667d-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7667d-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="7667d-118">Scenario description</span></span>
<span data-ttu-id="7667d-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7667d-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7667d-121">Egnyte는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="7667d-121">Adding Egnyte from hello gallery</span></span>
2. <span data-ttu-id="7667d-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="7667d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-egnyte-from-hello-gallery"></a><span data-ttu-id="7667d-123">Egnyte는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="7667d-123">Adding Egnyte from hello gallery</span></span>
<span data-ttu-id="7667d-124">tooconfigure hello와의 통합 Egnyte Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Egnyte tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-124">tooconfigure hello integration of Egnyte into Azure AD, you need tooadd Egnyte from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7667d-125">**Egnyte hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="7667d-125">**tooadd Egnyte from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7667d-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7667d-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7667d-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="7667d-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="7667d-133">Hello 검색 상자에 입력 **Egnyte**합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-133">In hello search box, type **Egnyte**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. <span data-ttu-id="7667d-135">Hello 결과 패널에서 선택 **Egnyte**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-135">In hello results panel, select **Egnyte**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7667d-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="7667d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7667d-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Egnyte에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-138">In this section, you configure and test Azure AD single sign-on with Egnyte based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7667d-139">Single sign on toowork에 대 한 Azure AD는 tooknow Egnyte에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Egnyte is tooa user in Azure AD.</span></span> <span data-ttu-id="7667d-140">즉, Azure AD 사용자와 Egnyte에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-140">In other words, a link relationship between an Azure AD user and hello related user in Egnyte needs toobe established.</span></span>

<span data-ttu-id="7667d-141">Egnyte에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-141">In Egnyte, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7667d-142">tooconfigure와 Egnyte 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-142">tooconfigure and test Azure AD single sign-on with Egnyte, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7667d-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7667d-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7667d-145">**[Egnyte 테스트 사용자 만들기](#creating-an-egnyte-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Egnyte에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-145">**[Creating an Egnyte test user](#creating-an-egnyte-test-user)** - toohave a counterpart of Britta Simon in Egnyte that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7667d-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7667d-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="7667d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7667d-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="7667d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7667d-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Egnyte 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Egnyte application.</span></span>

<span data-ttu-id="7667d-150">**Azure AD tooconfigure single sign on와 Egnyte를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="7667d-150">**tooconfigure Azure AD single sign-on with Egnyte, perform hello following steps:**</span></span>

1. <span data-ttu-id="7667d-151">Hello hello에 Azure 포털에서에서 **Egnyte** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-151">In hello Azure portal, on hello **Egnyte** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="7667d-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. <span data-ttu-id="7667d-155">Hello에 **Egnyte 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-155">On hello **Egnyte Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    <span data-ttu-id="7667d-157">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.egnyte.com`</span><span class="sxs-lookup"><span data-stu-id="7667d-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.egnyte.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7667d-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-158">This value is not real.</span></span> <span data-ttu-id="7667d-159">Hello로이 값을 업데이트 합니다. 실제 로그온 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="7667d-160">연락처 [Egnyte 클라이언트 지원 팀](https://www.egnyte.com/corp/contact_egnyte.html) tooget이이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-160">Contact [Egnyte Client support team](https://www.egnyte.com/corp/contact_egnyte.html) tooget this value.</span></span> 
 
4. <span data-ttu-id="7667d-161">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. <span data-ttu-id="7667d-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7667d-165">Hello에 **Egnyte 구성** 섹션에서 클릭 **구성 Egnyte** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="7667d-165">On hello **Egnyte Configuration** section, click **Configure Egnyte** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7667d-166">복사 hello **SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="7667d-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. <span data-ttu-id="7667d-168">다른 웹 브라우저 창에서 관리자 권한으로 tooyour Egnyte 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-168">In a different web browser window, log in tooyour Egnyte company site as an administrator.</span></span>

8. <span data-ttu-id="7667d-169">**설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-169">Click **Settings**.</span></span>
   
   <span data-ttu-id="7667d-170">![설정](./media/active-directory-saas-egnyte-tutorial/ic787819.png "설정")</span><span class="sxs-lookup"><span data-stu-id="7667d-170">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Settings")</span></span>

9. <span data-ttu-id="7667d-171">Hello 메뉴에서 클릭 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-171">In hello menu, click **Settings**.</span></span>

   <span data-ttu-id="7667d-172">![설정](./media/active-directory-saas-egnyte-tutorial/ic787820.png "설정")</span><span class="sxs-lookup"><span data-stu-id="7667d-172">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Settings")</span></span>

10. <span data-ttu-id="7667d-173">Hello 클릭 **구성** 탭을 클릭 한 다음 **보안**합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-173">Click hello **Configuration** tab, and then click **Security**.</span></span>

    <span data-ttu-id="7667d-174">![보안](./media/active-directory-saas-egnyte-tutorial/ic787821.png "보안")</span><span class="sxs-lookup"><span data-stu-id="7667d-174">![Security](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Security")</span></span>

11. <span data-ttu-id="7667d-175">Hello에 **Single Sign On 인증** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-175">In hello **Single Sign-On Authentication** section, perform hello following steps:</span></span>

    <span data-ttu-id="7667d-176">![Single Sign On 인증](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Single Sign On 인증")</span><span class="sxs-lookup"><span data-stu-id="7667d-176">![Single Sign On Authentication](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Single Sign On Authentication")</span></span>   
    
    <span data-ttu-id="7667d-177">a.</span><span class="sxs-lookup"><span data-stu-id="7667d-177">a.</span></span> <span data-ttu-id="7667d-178">**Single sign-on 인증**으로 **SAML 2.0**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-178">As **Single sign-on authentication**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="7667d-179">b.</span><span class="sxs-lookup"><span data-stu-id="7667d-179">b.</span></span> <span data-ttu-id="7667d-180">**ID 공급자**로 **AzureAD**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-180">As **Identity provider**, select **AzureAD**.</span></span>
   
    <span data-ttu-id="7667d-181">c.</span><span class="sxs-lookup"><span data-stu-id="7667d-181">c.</span></span> <span data-ttu-id="7667d-182">붙여넣기 **SAML Single Sign-on 서비스 URL** hello에 Azure 포털에서 복사 **Id 공급자 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-182">Paste **SAML Single Sign-On Service URL** copied from Azure portal into hello **Identity provider login URL** textbox.</span></span>
   
    <span data-ttu-id="7667d-183">d.</span><span class="sxs-lookup"><span data-stu-id="7667d-183">d.</span></span> <span data-ttu-id="7667d-184">붙여넣기 **SAML 엔터티 ID** hello에 Azure 포털에서 복사한 있는 **Id 공급자 엔터티 ID** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-184">Paste **SAML Entity ID** which you have copied from Azure portal into hello **Identity provider entity ID** textbox.</span></span>
      
    <span data-ttu-id="7667d-185">e.</span><span class="sxs-lookup"><span data-stu-id="7667d-185">e.</span></span> <span data-ttu-id="7667d-186">콘텐츠를 클립보드에 복사 hello Azure 포털에서 다운로드 한 메모장에서 e-64로 인코딩된 인증서를 열고 toohello 붙여 **Id 공급자 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Identity provider certificate** textbox.</span></span>
   
    <span data-ttu-id="7667d-187">f.</span><span class="sxs-lookup"><span data-stu-id="7667d-187">f.</span></span> <span data-ttu-id="7667d-188">**기본 사용자 매핑**으로 **전자 메일 주소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-188">As **Default user mapping**, select **Email address**.</span></span>
   
    <span data-ttu-id="7667d-189">g.</span><span class="sxs-lookup"><span data-stu-id="7667d-189">g.</span></span> <span data-ttu-id="7667d-190">**도메인 특정 발급자 값 사용**을 **비활성화**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-190">As **Use domain-specific issuer value**, select **disabled**.</span></span>
   
    <span data-ttu-id="7667d-191">h.</span><span class="sxs-lookup"><span data-stu-id="7667d-191">h.</span></span> <span data-ttu-id="7667d-192">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-192">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7667d-193">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="7667d-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7667d-194">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="7667d-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7667d-195">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7667d-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7667d-196">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="7667d-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="7667d-197">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="7667d-199">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="7667d-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7667d-200">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7667d-202">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7667d-204">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7667d-206">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7667d-208">a.</span><span class="sxs-lookup"><span data-stu-id="7667d-208">a.</span></span> <span data-ttu-id="7667d-209">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7667d-210">b.</span><span class="sxs-lookup"><span data-stu-id="7667d-210">b.</span></span> <span data-ttu-id="7667d-211">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7667d-212">c.</span><span class="sxs-lookup"><span data-stu-id="7667d-212">c.</span></span> <span data-ttu-id="7667d-213">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7667d-214">d.</span><span class="sxs-lookup"><span data-stu-id="7667d-214">d.</span></span> <span data-ttu-id="7667d-215">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-215">Click **Create**.</span></span>
 
### <a name="creating-an-egnyte-test-user"></a><span data-ttu-id="7667d-216">Egnyte 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="7667d-216">Creating an Egnyte test user</span></span>

<span data-ttu-id="7667d-217">tooenable Azure AD 사용자가 toolog tooEgnyte에서 프로 비전 해야 Egnyte에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-217">tooenable Azure AD users toolog in tooEgnyte, they must be provisioned into Egnyte.</span></span> <span data-ttu-id="7667d-218">Hello Egnyte의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-218">In hello case of Egnyte, provisioning is a manual task.</span></span>

<span data-ttu-id="7667d-219">**사용자 계정 수행 tooprovision hello 다음 단계:**</span><span class="sxs-lookup"><span data-stu-id="7667d-219">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="7667d-220">Tooyour 로그인 **Egnyte** 회사 사이트에서 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-220">Log in tooyour **Egnyte** company site as administrator.</span></span>

2. <span data-ttu-id="7667d-221">너무 이동**설정 \> 사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-221">Go too**Settings \> Users & Groups**.</span></span>

3. <span data-ttu-id="7667d-222">클릭 **새 사용자 추가**, 다음 hello 유형을 선택 하 고 원하는 tooadd 사용자의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-222">Click **Add New User**, and then select hello type of user you want tooadd.</span></span>
   
   <span data-ttu-id="7667d-223">![사용자](./media/active-directory-saas-egnyte-tutorial/ic787824.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="7667d-223">![Users](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Users")</span></span>

4. <span data-ttu-id="7667d-224">Hello에 **새 표준 사용자** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-224">In hello **New Standard User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="7667d-225">![새 표준 사용자](./media/active-directory-saas-egnyte-tutorial/ic787825.png "새 표준 사용자")</span><span class="sxs-lookup"><span data-stu-id="7667d-225">![New Standard User](./media/active-directory-saas-egnyte-tutorial/ic787825.png "New Standard User")</span></span>   

   <span data-ttu-id="7667d-226">a.</span><span class="sxs-lookup"><span data-stu-id="7667d-226">a.</span></span> <span data-ttu-id="7667d-227">형식 hello **전자 메일**, **Username**, 및 tooprovision 하려는 유효한 Azure Active Directory 계정의 기타 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-227">Type hello **Email**, **Username**, and other details of a valid Azure Active Directory account you want tooprovision.</span></span>
   
   <span data-ttu-id="7667d-228">b.</span><span class="sxs-lookup"><span data-stu-id="7667d-228">b.</span></span> <span data-ttu-id="7667d-229">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-229">Click **Save**.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="7667d-230">hello Azure Active Directory 계정 소유자는 알림 메일을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-230">hello Azure Active Directory account holder will receive a notification email.</span></span>
    >

>[!NOTE]
><span data-ttu-id="7667d-231">다른 Egnyte 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision Egnyte에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-231">You can use any other Egnyte user account creation tools or APIs provided by Egnyte tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7667d-232">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7667d-233">이 섹션에서는 tooEgnyte 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEgnyte.</span></span>

![사용자 할당][200] 

<span data-ttu-id="7667d-235">**tooassign Britta Simon tooEgnyte hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="7667d-235">**tooassign Britta Simon tooEgnyte, perform hello following steps:**</span></span>

1. <span data-ttu-id="7667d-236">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="7667d-238">Hello 응용 프로그램 목록에서 선택 **Egnyte**합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-238">In hello applications list, select **Egnyte**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. <span data-ttu-id="7667d-240">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="7667d-242">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-242">Click **Add** button.</span></span> <span data-ttu-id="7667d-243">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="7667d-245">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7667d-246">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7667d-247">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7667d-248">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="7667d-248">Testing single sign-on</span></span>

<span data-ttu-id="7667d-249">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7667d-250">Hello 액세스 패널에서에서 hello Egnyte 타일을 클릭할 때 자동으로 로그온 tooyour Egnyte 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-250">When you click hello Egnyte tile in hello Access Panel, you should get automatically signed-on tooyour Egnyte application.</span></span>
<span data-ttu-id="7667d-251">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7667d-251">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7667d-252">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="7667d-252">Additional resources</span></span>

* [<span data-ttu-id="7667d-253">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="7667d-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7667d-254">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="7667d-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_203.png

