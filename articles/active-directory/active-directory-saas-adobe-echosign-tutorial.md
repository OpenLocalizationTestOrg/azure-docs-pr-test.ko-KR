---
title: "자습서: Adobe Sign과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Adobe 기호 사이 로그온 tooconfigure single 하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b4b07907f30a0890003554a02a76d968400b43ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a><span data-ttu-id="69d0c-103">자습서: Adobe Sign과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="69d0c-103">Tutorial: Azure Active Directory integration with Adobe Sign</span></span>

<span data-ttu-id="69d0c-104">이 자습서에 설명 toointegrate Adobe Azure Active Directory (Azure AD)에 서명 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-104">In this tutorial, you learn how toointegrate Adobe Sign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="69d0c-105">Adobe 기호 Azure AD와 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-105">Integrating Adobe Sign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="69d0c-106">Azure ad 액세스 tooAdobe 기호를 가진 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-106">You can control in Azure AD who has access tooAdobe Sign</span></span>
- <span data-ttu-id="69d0c-107">에 사용자가 tooautomatically get 로그온 tooAdobe 기호 (Single Sign-on)는 Azure AD 계정 사용을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-107">You can enable your users tooautomatically get signed-on tooAdobe Sign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="69d0c-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="69d0c-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="69d0c-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="69d0c-110">Prerequisites</span></span>

<span data-ttu-id="69d0c-111">Azure AD 통합 Adobe 기호로 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-111">tooconfigure Azure AD integration with Adobe Sign, you need hello following items:</span></span>

- <span data-ttu-id="69d0c-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="69d0c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="69d0c-113">Adobe Sign Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="69d0c-113">An Adobe Sign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="69d0c-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="69d0c-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="69d0c-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="69d0c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="69d0c-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="69d0c-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="69d0c-118">Scenario description</span></span>
<span data-ttu-id="69d0c-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="69d0c-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="69d0c-121">Hello 갤러리에서 Adobe 기호 추가</span><span class="sxs-lookup"><span data-stu-id="69d0c-121">Adding Adobe Sign from hello gallery</span></span>
2. <span data-ttu-id="69d0c-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="69d0c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-sign-from-hello-gallery"></a><span data-ttu-id="69d0c-123">Hello 갤러리에서 Adobe 기호 추가</span><span class="sxs-lookup"><span data-stu-id="69d0c-123">Adding Adobe Sign from hello gallery</span></span>
<span data-ttu-id="69d0c-124">tooconfigure hello와의 통합 Adobe 기호 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 tooadd Adobe 로그인 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-124">tooconfigure hello integration of Adobe Sign into Azure AD, you need tooadd Adobe Sign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="69d0c-125">**hello 갤러리에서 Adobe 기호 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="69d0c-125">**tooadd Adobe Sign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="69d0c-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="69d0c-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="69d0c-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="69d0c-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="69d0c-133">Hello 검색 상자에 입력 **Adobe 기호**합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-133">In hello search box, type **Adobe Sign**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. <span data-ttu-id="69d0c-135">Hello 결과 패널에서 선택 **Adobe 기호**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-135">In hello results panel, select **Adobe Sign**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="69d0c-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="69d0c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="69d0c-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Adobe Sign에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-138">In this section, you configure and test Azure AD single sign-on with Adobe Sign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="69d0c-139">Single sign on toowork에 대 한 Azure AD는 tooknow Adobe 부호의 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adobe Sign is tooa user in Azure AD.</span></span> <span data-ttu-id="69d0c-140">즉, Azure AD 사용자 및 Adobe 부호의 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-140">In other words, a link relationship between an Azure AD user and hello related user in Adobe Sign needs toobe established.</span></span>

<span data-ttu-id="69d0c-141">Adobe 부호의 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-141">In Adobe Sign, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="69d0c-142">tooconfigure 및 Adobe 기호를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-142">tooconfigure and test Azure AD single sign-on with Adobe Sign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="69d0c-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="69d0c-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="69d0c-145">**[Adobe 기호 테스트 사용자 만들기](#creating-an-adobe-sign-test-user)**  -toohave Britta Simon 표현인 연결 된 toohello Azure AD 사용자의 Adobe 기호에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-145">**[Creating an Adobe Sign test user](#creating-an-adobe-sign-test-user)** - toohave a counterpart of Britta Simon in Adobe Sign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="69d0c-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="69d0c-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="69d0c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="69d0c-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="69d0c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="69d0c-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 및 Adobe 기호 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Adobe Sign application.</span></span>

<span data-ttu-id="69d0c-150">**tooconfigure Azure AD single sign on Adobe 기호가 있는 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="69d0c-150">**tooconfigure Azure AD single sign-on with Adobe Sign, perform hello following steps:**</span></span>

1. <span data-ttu-id="69d0c-151">Hello hello에 Azure 포털에서에서 **Adobe 기호** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-151">In hello Azure portal, on hello **Adobe Sign** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="69d0c-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. <span data-ttu-id="69d0c-155">Hello에 **Adobe 기호 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-155">On hello **Adobe Sign Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    <span data-ttu-id="69d0c-157">a.</span><span class="sxs-lookup"><span data-stu-id="69d0c-157">a.</span></span> <span data-ttu-id="69d0c-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.echosign.com/`</span><span class="sxs-lookup"><span data-stu-id="69d0c-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.echosign.com/`</span></span>

    <span data-ttu-id="69d0c-159">b.</span><span class="sxs-lookup"><span data-stu-id="69d0c-159">b.</span></span> <span data-ttu-id="69d0c-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.echosign.com`</span><span class="sxs-lookup"><span data-stu-id="69d0c-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.echosign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="69d0c-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-161">These values are not real.</span></span> <span data-ttu-id="69d0c-162">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="69d0c-163">연락처 [Adobe 기호 클라이언트 지원 팀](https://helpx.adobe.com/in/contact/support.html) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-163">Contact [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) tooget these values.</span></span> 
 
4. <span data-ttu-id="69d0c-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. <span data-ttu-id="69d0c-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="69d0c-168">Hello에 **Adobe 기호 구성** 섹션에서 클릭 **Adobe 기호 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="69d0c-168">On hello **Adobe Sign Configuration** section, click **Configure Adobe Sign** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="69d0c-169">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="69d0c-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. <span data-ttu-id="69d0c-171">다른 웹 브라우저 창에서 관리자 권한으로 tooyour Adobe 기호 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-171">In a different web browser window, log in tooyour Adobe Sign company site as an administrator.</span></span>

8. <span data-ttu-id="69d0c-172">Hello 메뉴에서 hello 위에 표시를 클릭 **계정**, hello 왼쪽에 hello 탐색 창에서을 클릭 하 고 **SAML 설정** 아래 **계정 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-172">In hello menu on hello top, click **Account**, and then, in hello navigation pane on hello left side, click **SAML Settings** under **Account Settings**.</span></span>
   
   <span data-ttu-id="69d0c-173">![계정](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "계정")</span><span class="sxs-lookup"><span data-stu-id="69d0c-173">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Account")</span></span>

9. <span data-ttu-id="69d0c-174">Hello SAML 설정 섹션에서에서 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-174">In hello SAML Settings section, perform hello following steps:</span></span>
   
   <span data-ttu-id="69d0c-175">![SAML 설정](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML 설정")</span><span class="sxs-lookup"><span data-stu-id="69d0c-175">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML Settings")</span></span>
   
   <span data-ttu-id="69d0c-176">a.</span><span class="sxs-lookup"><span data-stu-id="69d0c-176">a.</span></span> <span data-ttu-id="69d0c-177">**SAML 모드**로 **SAML 필수**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-177">As **SAML Mode**, select **SAML Mandatory**.</span></span>
   
   <span data-ttu-id="69d0c-178">b.</span><span class="sxs-lookup"><span data-stu-id="69d0c-178">b.</span></span> <span data-ttu-id="69d0c-179">선택 **EchoSign 자격 증명을 사용 하 여 EchoSign 계정 관리자가 허용 toolog**합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-179">Select **Allow EchoSign Account Administrators toolog in using their EchoSign Credentials**.</span></span>
   
   <span data-ttu-id="69d0c-180">c.</span><span class="sxs-lookup"><span data-stu-id="69d0c-180">c.</span></span> <span data-ttu-id="69d0c-181">**사용자 만들기**로 **SAML을 통해 인증된 사용자를 자동으로 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-181">As **User Creation**, select **Automatically add users authenticated through SAML**.</span></span>

10. <span data-ttu-id="69d0c-182">이동, 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-182">Move on, performing hello following steps:</span></span>

       <span data-ttu-id="69d0c-183">![SAML 설정](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML 설정")</span><span class="sxs-lookup"><span data-stu-id="69d0c-183">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML Settings")</span></span>

    <span data-ttu-id="69d0c-184">a.</span><span class="sxs-lookup"><span data-stu-id="69d0c-184">a.</span></span> <span data-ttu-id="69d0c-185">붙여넣기 **SAML 엔터티 ID**, hello에 Azure 포털에서 복사한 있는 **IdP 엔터티 ID** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-185">Paste **SAML Entity ID**, which you have copied from Azure portal into hello **IdP Entity ID** textbox.</span></span>
    
    <span data-ttu-id="69d0c-186">b.</span><span class="sxs-lookup"><span data-stu-id="69d0c-186">b.</span></span> <span data-ttu-id="69d0c-187">붙여넣기 **SAML Single Sign-on 서비스 URL**, hello에 Azure 포털에서 복사한 있는 **IdP 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-187">Paste **SAML Single Sign-On Service URL**, which you have copied from Azure portal into hello **IdP Login URL** textbox.</span></span>
   
    <span data-ttu-id="69d0c-188">c.</span><span class="sxs-lookup"><span data-stu-id="69d0c-188">c.</span></span> <span data-ttu-id="69d0c-189">붙여넣기 **Sign-Out URL**, hello에 Azure 포털에서 복사한 있는 **IdP 로그 아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-189">Paste **Sign-Out URL**, which you have copied from Azure portal into hello **IdP Logout URL** textbox.</span></span>

    <span data-ttu-id="69d0c-190">d.</span><span class="sxs-lookup"><span data-stu-id="69d0c-190">d.</span></span> <span data-ttu-id="69d0c-191">프로그램 다운로드 한 열고 **Certificate(Base64)** 내용을 클립보드의 콘텐츠 복사 hello 메모장에서 파일을 붙여넣을 toohello **IdP 인증서** textbox</span><span class="sxs-lookup"><span data-stu-id="69d0c-191">Open your downloaded **Certificate(Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Certificate** textbox</span></span>

    <span data-ttu-id="69d0c-192">e.</span><span class="sxs-lookup"><span data-stu-id="69d0c-192">e.</span></span> <span data-ttu-id="69d0c-193">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-193">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="69d0c-194">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="69d0c-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="69d0c-195">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="69d0c-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="69d0c-196">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="69d0c-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="69d0c-197">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="69d0c-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="69d0c-198">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="69d0c-200">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="69d0c-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="69d0c-201">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="69d0c-203">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="69d0c-205">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="69d0c-207">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="69d0c-209">a.</span><span class="sxs-lookup"><span data-stu-id="69d0c-209">a.</span></span> <span data-ttu-id="69d0c-210">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="69d0c-211">b.</span><span class="sxs-lookup"><span data-stu-id="69d0c-211">b.</span></span> <span data-ttu-id="69d0c-212">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="69d0c-213">c.</span><span class="sxs-lookup"><span data-stu-id="69d0c-213">c.</span></span> <span data-ttu-id="69d0c-214">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="69d0c-215">d.</span><span class="sxs-lookup"><span data-stu-id="69d0c-215">d.</span></span> <span data-ttu-id="69d0c-216">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-216">Click **Create**.</span></span>
 
### <a name="creating-an-adobe-sign-test-user"></a><span data-ttu-id="69d0c-217">Adobe Sign 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="69d0c-217">Creating an Adobe Sign test user</span></span>

<span data-ttu-id="69d0c-218">tooenable Azure AD 사용자가 toolog tooAdobe 기호에서에서 이러한 해야에 프로 비전 Adobe 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-218">tooenable Azure AD users toolog in tooAdobe Sign, they must be provisioned into Adobe Sign.</span></span> <span data-ttu-id="69d0c-219">Hello Adobe 로그인의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-219">In hello case of Adobe Sign, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="69d0c-220">다른 Adobe 기호 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 Adobe 기호 tooprovision에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-220">You can use any other Adobe Sign user account creation tools or APIs provided by Adobe Sign tooprovision AAD user accounts.</span></span> 

<span data-ttu-id="69d0c-221">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="69d0c-221">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="69d0c-222">Tooyour 로그인 **Adobe 기호** 회사 사이트에서 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-222">Log in tooyour **Adobe Sign** company site as administrator.</span></span>

2. <span data-ttu-id="69d0c-223">Hello 메뉴에서 hello 위에 표시를 클릭 **계정**, hello 왼쪽에 hello 탐색 창에서을 클릭 하 고 **사용자 및 그룹**를 클릭 하 고 **새 사용자를 만드는**합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-223">In hello menu on hello top, click **Account**, and then, in hello navigation pane on hello left side, click **Users & Groups**, and then, click **Create a new user**.</span></span>
   
   <span data-ttu-id="69d0c-224">![계정](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "계정")</span><span class="sxs-lookup"><span data-stu-id="69d0c-224">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Account")</span></span>
   
3. <span data-ttu-id="69d0c-225">Hello에 **새 사용자 만들기** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-225">In hello **Create New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="69d0c-226">![사용자 만들기](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "사용자 만들기")</span><span class="sxs-lookup"><span data-stu-id="69d0c-226">![Create User](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Create User")</span></span>
   
   <span data-ttu-id="69d0c-227">a.</span><span class="sxs-lookup"><span data-stu-id="69d0c-227">a.</span></span> <span data-ttu-id="69d0c-228">형식 hello **전자 메일 주소**, **이름**, 및 **성** 의 hello에 tooprovision 하려는 유효한 AAD 계정의 관련 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-228">Type hello **Email Address**, **First Name**, and **Last Name** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
   
   <span data-ttu-id="69d0c-229">b.</span><span class="sxs-lookup"><span data-stu-id="69d0c-229">b.</span></span> <span data-ttu-id="69d0c-230">**사용자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-230">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="69d0c-231">hello Azure Active Directory 계정 소유자는 데이터베이스가 활성화 전에 tooconfirm hello 계정 연결을 포함 하는 전자 메일을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-231">hello Azure Active Directory account holder receives an email that includes a link tooconfirm hello account before it becomes active.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="69d0c-232">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="69d0c-233">이 섹션에서는 액세스 tooAdobe 로그인 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAdobe Sign.</span></span>

![사용자 할당][200] 

<span data-ttu-id="69d0c-235">**tooassign Britta Simon tooAdobe 기호 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="69d0c-235">**tooassign Britta Simon tooAdobe Sign, perform hello following steps:**</span></span>

1. <span data-ttu-id="69d0c-236">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="69d0c-238">Hello 응용 프로그램 목록에서 선택 **Adobe 기호**합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-238">In hello applications list, select **Adobe Sign**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. <span data-ttu-id="69d0c-240">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="69d0c-242">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-242">Click **Add** button.</span></span> <span data-ttu-id="69d0c-243">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="69d0c-245">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="69d0c-246">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="69d0c-247">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="69d0c-248">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="69d0c-248">Testing single sign-on</span></span>

<span data-ttu-id="69d0c-249">Hello Adobe 기호 hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour Adobe 기호 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-249">When you click hello Adobe Sign tile in hello Access Panel, you should get automatically signed-on tooyour Adobe Sign application.</span></span>
<span data-ttu-id="69d0c-250">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="69d0c-250">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="69d0c-251">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="69d0c-251">Additional resources</span></span>

* [<span data-ttu-id="69d0c-252">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="69d0c-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="69d0c-253">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="69d0c-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

