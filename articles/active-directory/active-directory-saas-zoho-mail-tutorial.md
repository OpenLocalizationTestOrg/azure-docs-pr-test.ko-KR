---
title: "자습서: Azure Active Directory와 Zoho 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Zoho 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 5d1c196d3b97babab196f509ea68e7d61523a7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a><span data-ttu-id="9a823-103">자습서: Zoho와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="9a823-103">Tutorial: Azure Active Directory integration with Zoho</span></span>

<span data-ttu-id="9a823-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 Zoho 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-104">In this tutorial, you learn how toointegrate Zoho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9a823-105">다음 이점을 hello로 제공 Zoho Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="9a823-105">Integrating Zoho with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9a823-106">액세스 tooZoho을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-106">You can control in Azure AD who has access tooZoho.</span></span>
- <span data-ttu-id="9a823-107">에 사용자가 tooautomatically get 로그온 tooZoho (Single Sign-on)는 Azure AD 계정으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-107">You can enable your users tooautomatically get signed-on tooZoho (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9a823-108">하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="9a823-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a823-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9a823-110">Prerequisites</span></span>

<span data-ttu-id="9a823-111">Zoho와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-111">tooconfigure Azure AD integration with Zoho, you need hello following items:</span></span>

- <span data-ttu-id="9a823-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="9a823-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9a823-113">Zoho Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="9a823-113">A Zoho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9a823-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9a823-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9a823-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="9a823-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9a823-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9a823-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="9a823-118">Scenario description</span></span>
<span data-ttu-id="9a823-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9a823-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9a823-121">Zoho는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="9a823-121">Adding Zoho from hello gallery</span></span>
2. <span data-ttu-id="9a823-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="9a823-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoho-from-hello-gallery"></a><span data-ttu-id="9a823-123">Zoho는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="9a823-123">Adding Zoho from hello gallery</span></span>
<span data-ttu-id="9a823-124">tooconfigure hello와의 통합 Zoho Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Zoho tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-124">tooconfigure hello integration of Zoho into Azure AD, you need tooadd Zoho from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9a823-125">**hello 갤러리에서 Zoho tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9a823-125">**tooadd Zoho from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a823-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="9a823-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9a823-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="9a823-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="9a823-133">Hello 검색 상자에 입력 **Zoho**선택, **Zoho** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-133">In hello search box, type **Zoho**, select **Zoho** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Zoho hello 결과 목록에서](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9a823-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="9a823-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9a823-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Zoho에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-136">In this section, you configure and test Azure AD single sign-on with Zoho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9a823-137">Single sign on toowork에 대 한 Azure AD는 tooknow Zoho에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zoho is tooa user in Azure AD.</span></span> <span data-ttu-id="9a823-138">즉, Azure AD 사용자와 Zoho에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-138">In other words, a link relationship between an Azure AD user and hello related user in Zoho needs toobe established.</span></span>

<span data-ttu-id="9a823-139">Zoho에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-139">In Zoho, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9a823-140">tooconfigure 및 Zoho 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-140">tooconfigure and test Azure AD single sign-on with Zoho, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9a823-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9a823-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9a823-143">**[Zoho 테스트 사용자 만들기](#create-a-zoho-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Zoho에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-143">**[Create a Zoho test user](#create-a-zoho-test-user)** - toohave a counterpart of Britta Simon in Zoho that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9a823-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9a823-145">**[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="9a823-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9a823-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="9a823-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9a823-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Zoho 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zoho application.</span></span>

<span data-ttu-id="9a823-148">**tooconfigure Azure AD single sign on, Zoho와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9a823-148">**tooconfigure Azure AD single sign-on with Zoho, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a823-149">Hello hello에 Azure 포털에서에서 **Zoho** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-149">In hello Azure portal, on hello **Zoho** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="9a823-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. <span data-ttu-id="9a823-153">Hello에 **Zoho 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-153">On hello **Zoho Domain and URLs** section, perform hello following steps:</span></span>

    ![Zoho 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    <span data-ttu-id="9a823-155">a.</span><span class="sxs-lookup"><span data-stu-id="9a823-155">a.</span></span> <span data-ttu-id="9a823-156">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<company name>.zohomail.com`</span><span class="sxs-lookup"><span data-stu-id="9a823-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.zohomail.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9a823-157">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-157">This value is not real.</span></span> <span data-ttu-id="9a823-158">Hello로이 값을 업데이트 합니다. 실제 로그온 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-158">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="9a823-159">연락처 [Zoho 클라이언트 지원 팀](https://www.zoho.com/mail/contact.html) tooget이이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-159">Contact [Zoho Client support team](https://www.zoho.com/mail/contact.html) tooget this value.</span></span> 
 
4. <span data-ttu-id="9a823-160">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-160">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. <span data-ttu-id="9a823-162">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-162">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9a823-164">Hello에 **Zoho 구성** 섹션에서 클릭 **구성 Zoho** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="9a823-164">On hello **Zoho Configuration** section, click **Configure Zoho** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9a823-165">복사 hello **Sign-Out URL, 암호 변경 URL 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="9a823-165">Copy hello **Sign-Out URL, Change Password URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Zoho 구성](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. <span data-ttu-id="9a823-167">다른 웹 브라우저 창에서 관리자 권한으로 Zoho Mail 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-167">In a different web browser window, log into your Zoho Mail company site as an administrator.</span></span>

8. <span data-ttu-id="9a823-168">Toohello 이동 **제어판**합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-168">Go toohello **Control panel**.</span></span>
   
    <span data-ttu-id="9a823-169">![제어판](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "제어판")</span><span class="sxs-lookup"><span data-stu-id="9a823-169">![Control Panel](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Control Panel")</span></span>

9. <span data-ttu-id="9a823-170">Hello 클릭 **SAML 인증** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-170">Click hello **SAML Authentication** tab.</span></span>
   
    <span data-ttu-id="9a823-171">![SAML 인증](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML 인증")</span><span class="sxs-lookup"><span data-stu-id="9a823-171">![SAML Authentication](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML Authentication")</span></span>

10. <span data-ttu-id="9a823-172">Hello에 **SAML 인증 세부 정보** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-172">In hello **SAML Authentication Details** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="9a823-173">![SAML 인증 세부 정보](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML 인증 세부 정보")</span><span class="sxs-lookup"><span data-stu-id="9a823-173">![SAML Authentication Details](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML Authentication Details")</span></span>
   
    <span data-ttu-id="9a823-174">a.</span><span class="sxs-lookup"><span data-stu-id="9a823-174">a.</span></span> <span data-ttu-id="9a823-175">Hello에 **로그인 URL** 붙여넣습니다 **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-175">In hello **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="9a823-176">b.</span><span class="sxs-lookup"><span data-stu-id="9a823-176">b.</span></span> <span data-ttu-id="9a823-177">Hello에 **로그 아웃 URL** 붙여넣습니다 **Sign-Out URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-177">In hello **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="9a823-178">c.</span><span class="sxs-lookup"><span data-stu-id="9a823-178">c.</span></span> <span data-ttu-id="9a823-179">Hello에 **암호 변경 URL** 붙여넣습니다 **암호 변경 URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-179">In hello **Change Password URL** textbox, paste **Change Password URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="9a823-180">d.</span><span class="sxs-lookup"><span data-stu-id="9a823-180">d.</span></span> <span data-ttu-id="9a823-181">메모장에서 콘텐츠를 클립보드에 복사 hello Azure 포털에서 다운로드 한 base 64로 인코딩된 인증서를 열고 다음 toohello **PublicKey** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-181">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **PublicKey** textbox.</span></span>
   
    <span data-ttu-id="9a823-182">e.</span><span class="sxs-lookup"><span data-stu-id="9a823-182">e.</span></span> <span data-ttu-id="9a823-183">**알고리즘**으로 **RSA**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-183">As **Algorithm**, select **RSA**.</span></span>
   
    <span data-ttu-id="9a823-184">f.</span><span class="sxs-lookup"><span data-stu-id="9a823-184">f.</span></span> <span data-ttu-id="9a823-185">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-185">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="9a823-186">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="9a823-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9a823-187">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="9a823-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9a823-188">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9a823-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9a823-189">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="9a823-189">Create an Azure AD test user</span></span>

<span data-ttu-id="9a823-190">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="9a823-192">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9a823-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a823-193">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-193">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="9a823-195">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-195">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="9a823-197">tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="9a823-197">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello 추가 단추](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="9a823-199">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-199">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello 사용자 대화 상자](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9a823-201">a.</span><span class="sxs-lookup"><span data-stu-id="9a823-201">a.</span></span> <span data-ttu-id="9a823-202">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-202">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9a823-203">b.</span><span class="sxs-lookup"><span data-stu-id="9a823-203">b.</span></span> <span data-ttu-id="9a823-204">Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-204">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="9a823-205">c.</span><span class="sxs-lookup"><span data-stu-id="9a823-205">c.</span></span> <span data-ttu-id="9a823-206">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-206">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="9a823-207">d.</span><span class="sxs-lookup"><span data-stu-id="9a823-207">d.</span></span> <span data-ttu-id="9a823-208">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-208">Click **Create**.</span></span>
 
### <a name="create-a-zoho-test-user"></a><span data-ttu-id="9a823-209">Zoho 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="9a823-209">Create a Zoho test user</span></span>

<span data-ttu-id="9a823-210">Tooenable Azure AD 사용자가 toolog Zoho Mail에 주문 하 고에 Zoho Mail에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-210">In order tooenable Azure AD users toolog into Zoho Mail, they must be provisioned into Zoho Mail.</span></span> <span data-ttu-id="9a823-211">Hello Zoho Mail의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-211">In hello case of Zoho Mail, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="9a823-212">다른 Zoho Mail 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision Zoho Mail에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-212">You can use any other Zoho Mail user account creation tools or APIs provided by Zoho Mail tooprovision AAD user accounts.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="9a823-213">tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-213">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="9a823-214">Tooyour 로그인 **Zoho Mail** 회사 사이트에 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-214">Log in tooyour **Zoho Mail** company site as an administrator.</span></span>

2. <span data-ttu-id="9a823-215">너무 이동**제어판 \> 메일 및 문서**합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-215">Go too**Control Panel \> Mail & Docs**.</span></span>

3. <span data-ttu-id="9a823-216">너무 이동**사용자 세부 정보 \> 사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-216">Go too**User Details \> Add User**.</span></span>
   
    <span data-ttu-id="9a823-217">![사용자 추가](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="9a823-217">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Add User")</span></span>

4. <span data-ttu-id="9a823-218">Hello에 **사용자 추가** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-218">On hello **Add users** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="9a823-219">![사용자 추가](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="9a823-219">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Add User")</span></span>
   
    <span data-ttu-id="9a823-220">a.</span><span class="sxs-lookup"><span data-stu-id="9a823-220">a.</span></span> <span data-ttu-id="9a823-221">Hello에 **이름** 형식 처럼 사용자의 hello 이름 텍스트 상자 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-221">In hello **First Name** textbox, type hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="9a823-222">b.</span><span class="sxs-lookup"><span data-stu-id="9a823-222">b.</span></span> <span data-ttu-id="9a823-223">Hello에 **성** 형식 hello와 같은 사용자의 마지막 이름 텍스트 상자 **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-223">In hello **Last Name** textbox, type hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="9a823-224">c.</span><span class="sxs-lookup"><span data-stu-id="9a823-224">c.</span></span> <span data-ttu-id="9a823-225">Hello에 **전자 메일 ID** 텍스트 상자와 같은 사용자의 형식 hello 전자 메일 id  **brittasimon@contoso.com** 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-225">In hello **Email ID** textbox, type hello email id of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="9a823-226">d.</span><span class="sxs-lookup"><span data-stu-id="9a823-226">d.</span></span> <span data-ttu-id="9a823-227">Hello에 **암호** textbox를 사용자의 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-227">In hello **Password** textbox, enter password of user.</span></span>
   
    <span data-ttu-id="9a823-228">e.</span><span class="sxs-lookup"><span data-stu-id="9a823-228">e.</span></span> <span data-ttu-id="9a823-229">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-229">Click **OK**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="9a823-230">hello Azure Active Directory 계정 소유자는 데이터베이스가 활성화 전에 링크 tooconfirm hello 계정 사용 하 여 전자 메일을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-230">hello Azure Active Directory account holder will receive an email with a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="9a823-231">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-231">Assign hello Azure AD test user</span></span>

<span data-ttu-id="9a823-232">이 섹션에서는 tooZoho 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZoho.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="9a823-234">**tooassign Britta Simon tooZoho hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9a823-234">**tooassign Britta Simon tooZoho, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a823-235">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="9a823-237">Hello 응용 프로그램 목록에서 선택 **Zoho**합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-237">In hello applications list, select **Zoho**.</span></span>

    ![hello 응용 프로그램 목록에서 hello Zoho 링크](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. <span data-ttu-id="9a823-239">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="9a823-241">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-241">Click **Add** button.</span></span> <span data-ttu-id="9a823-242">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="9a823-244">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9a823-245">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9a823-246">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9a823-247">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="9a823-247">Test single sign-on</span></span>

<span data-ttu-id="9a823-248">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-248">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9a823-249">Hello 액세스 패널에서에서 hello Zoho 타일을 클릭할 때 자동으로 로그온 tooyour Zoho 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-249">When you click hello Zoho tile in hello Access Panel, you should get automatically signed-on tooyour Zoho application.</span></span>
<span data-ttu-id="9a823-250">액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a823-250">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9a823-251">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="9a823-251">Additional resources</span></span>

* [<span data-ttu-id="9a823-252">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="9a823-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9a823-253">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="9a823-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_203.png

