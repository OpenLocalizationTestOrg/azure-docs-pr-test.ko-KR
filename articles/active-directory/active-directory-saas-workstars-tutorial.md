---
title: "자습서: Workstars와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Workstars 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 51a4a4e4-ff60-4971-b3f8-a0367b70d220
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 86250d7538f058d2a821ded7dda0b2fc185d80df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workstars"></a><span data-ttu-id="a1231-103">자습서: Workstars와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="a1231-103">Tutorial: Azure Active Directory integration with Workstars</span></span>

<span data-ttu-id="a1231-104">이 자습서에 설명 어떻게 toointegrate Workstars Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a1231-104">In this tutorial, you learn how toointegrate Workstars with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a1231-105">다음 이점을 hello로 제공 Workstars Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="a1231-105">Integrating Workstars with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a1231-106">액세스 tooWorkstars을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-106">You can control in Azure AD who has access tooWorkstars.</span></span>
- <span data-ttu-id="a1231-107">에 사용자가 tooautomatically get 로그온 tooWorkstars (Single Sign-on)는 Azure AD 계정으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-107">You can enable your users tooautomatically get signed-on tooWorkstars (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a1231-108">하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="a1231-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1231-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a1231-110">Prerequisites</span></span>

<span data-ttu-id="a1231-111">다음 항목 hello가 필요 tooconfigure Workstars와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-111">tooconfigure Azure AD integration with Workstars, you need hello following items:</span></span>

- <span data-ttu-id="a1231-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="a1231-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a1231-113">Workstars Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="a1231-113">A Workstars single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a1231-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a1231-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a1231-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a1231-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a1231-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a1231-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="a1231-118">Scenario description</span></span>
<span data-ttu-id="a1231-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a1231-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a1231-121">Workstars는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="a1231-121">Adding Workstars from hello gallery</span></span>
2. <span data-ttu-id="a1231-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a1231-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workstars-from-hello-gallery"></a><span data-ttu-id="a1231-123">Workstars는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="a1231-123">Adding Workstars from hello gallery</span></span>
<span data-ttu-id="a1231-124">tooconfigure hello와의 통합 Workstars Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Workstars tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-124">tooconfigure hello integration of Workstars into Azure AD, you need tooadd Workstars from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a1231-125">**hello 갤러리에서 Workstars tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a1231-125">**tooadd Workstars from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1231-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="a1231-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a1231-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="a1231-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="a1231-133">Hello 검색 상자에 입력 **Workstars**선택, **Workstars** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-133">In hello search box, type **Workstars**, select **Workstars** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Workstars hello 결과 목록에서](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a1231-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a1231-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a1231-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Workstars에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-136">In this section, you configure and test Azure AD single sign-on with Workstars based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a1231-137">Single sign on toowork에 대 한 Azure AD는 tooknow Workstars에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workstars is tooa user in Azure AD.</span></span> <span data-ttu-id="a1231-138">즉, Azure AD 사용자 및 Workstars에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-138">In other words, a link relationship between an Azure AD user and hello related user in Workstars needs toobe established.</span></span>

<span data-ttu-id="a1231-139">Workstars에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-139">In Workstars, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a1231-140">tooconfigure 및 Workstars 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-140">tooconfigure and test Azure AD single sign-on with Workstars, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a1231-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a1231-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a1231-143">**[Workstars 테스트 사용자 만들기](#create-a-workstars-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Workstars에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-143">**[Create a Workstars test user](#create-a-workstars-test-user)** - toohave a counterpart of Britta Simon in Workstars that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a1231-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a1231-145">**[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="a1231-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a1231-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="a1231-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a1231-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Workstars 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workstars application.</span></span>

<span data-ttu-id="a1231-148">**tooconfigure Azure AD single sign on, Workstars와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a1231-148">**tooconfigure Azure AD single sign-on with Workstars, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1231-149">Hello hello에 Azure 포털에서에서 **Workstars** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-149">In hello Azure portal, on hello **Workstars** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="a1231-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_samlbase.png)

3. <span data-ttu-id="a1231-153">Hello에 **Workstars 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-153">On hello **Workstars Domain and URLs** section, perform hello following steps:</span></span>

    ![Workstars 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_url.png)

    <span data-ttu-id="a1231-155">a.</span><span class="sxs-lookup"><span data-stu-id="a1231-155">a.</span></span> <span data-ttu-id="a1231-156">Hello에 **식별자** textbox hello URL 입력:`https://workstars.com`</span><span class="sxs-lookup"><span data-stu-id="a1231-156">In hello **Identifier** textbox, type hello URL: `https://workstars.com`</span></span>

    <span data-ttu-id="a1231-157">b.</span><span class="sxs-lookup"><span data-stu-id="a1231-157">b.</span></span> <span data-ttu-id="a1231-158">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.workstars.com/saml/login_check`</span><span class="sxs-lookup"><span data-stu-id="a1231-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.workstars.com/saml/login_check`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a1231-159">hello 값이 실제 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-159">hello value is not real.</span></span> <span data-ttu-id="a1231-160">업데이트 hello 값과 실제 회신 URL hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-160">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="a1231-161">연락처 [Workstars 지원 팀](https://support.workstars.com) tooget hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-161">Contact [Workstars support team](https://support.workstars.com) tooget hello value.</span></span>
 
4. <span data-ttu-id="a1231-162">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_certificate.png) 

5. <span data-ttu-id="a1231-164">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-164">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-workstars-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a1231-166">Hello에 **Workstars 구성** 섹션에서 클릭 **구성 Workstars** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="a1231-166">On hello **Workstars Configuration** section, click **Configure Workstars** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a1231-167">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="a1231-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Workstars 구성](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_configure.png) 

7. <span data-ttu-id="a1231-169">다른 브라우저 창에서 관리자 권한으로 tooyour Workstars 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-169">In another browser window, sign on tooyour Workstars company site as an administrator.</span></span>

8. <span data-ttu-id="a1231-170">Hello 주 도구 모음에서 클릭 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-170">In hello main toolbar, click **Settings**.</span></span>

    ![Workstars 설정](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_sett.png)

9. <span data-ttu-id="a1231-172">너무 이동**Sign On** > **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-172">Go too**Sign On** > **Settings**.</span></span>

    ![Workstars 로그온](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_signon.png)

    ![Workstars 설정](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_settings.png)

10. <span data-ttu-id="a1231-175">Hello에 **Single Sign에 (SAML)-설정** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-175">On hello **Single Sign On (SAML) - Settings** page, perform hello following steps:</span></span>
    
    ![Workstars saml](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_saml.png)

    <span data-ttu-id="a1231-177">a.</span><span class="sxs-lookup"><span data-stu-id="a1231-177">a.</span></span> <span data-ttu-id="a1231-178">**ID 공급자 이름** 텍스트 상자에 **Office 365**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-178">In **Identity Provider Name** textbox, type **Office 365**.</span></span>

    <span data-ttu-id="a1231-179">b.</span><span class="sxs-lookup"><span data-stu-id="a1231-179">b.</span></span> <span data-ttu-id="a1231-180">Hello에 **Id 공급자 엔터티 ID** 붙여넣기 hello 값의 텍스트 상자 **SAML 엔터티 ID**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-180">In hello **Identity Provider Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a1231-181">c.</span><span class="sxs-lookup"><span data-stu-id="a1231-181">c.</span></span> <span data-ttu-id="a1231-182">메모장에서 hello 다운로드 한 인증서 파일의 hello 콘텐츠를 복사 하 고 hello에 붙여 넣습니다 **x509 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-182">Copy hello content of hello downloaded certificate file in notepad, and then paste it into hello **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="a1231-183">d.</span><span class="sxs-lookup"><span data-stu-id="a1231-183">d.</span></span> <span data-ttu-id="a1231-184">Hello에 **SAML SSO URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-184">In hello **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="a1231-185">e.</span><span class="sxs-lookup"><span data-stu-id="a1231-185">e.</span></span> <span data-ttu-id="a1231-186">Hello에 **원격 로그 아웃 URL** 붙여넣기 hello 값의 텍스트 상자 **Sign-Out URL**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-186">In hello **Remote Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="a1231-187">f.</span><span class="sxs-lookup"><span data-stu-id="a1231-187">f.</span></span> <span data-ttu-id="a1231-188">**전자 메일(기본값)**로 **이름 ID**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-188">select **Name ID** as **Email (Default)**.</span></span>

    <span data-ttu-id="a1231-189">g.</span><span class="sxs-lookup"><span data-stu-id="a1231-189">g.</span></span> <span data-ttu-id="a1231-190">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-190">Click **Confirm**.</span></span>
    
> [!TIP]
> <span data-ttu-id="a1231-191">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="a1231-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a1231-192">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="a1231-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a1231-193">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a1231-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a1231-194">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a1231-194">Create an Azure AD test user</span></span>

<span data-ttu-id="a1231-195">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="a1231-197">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a1231-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1231-198">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-198">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-workstars-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="a1231-200">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-200">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-workstars-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="a1231-202">tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="a1231-202">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello 추가 단추](./media/active-directory-saas-workstars-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="a1231-204">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-204">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello 사용자 대화 상자](./media/active-directory-saas-workstars-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a1231-206">a.</span><span class="sxs-lookup"><span data-stu-id="a1231-206">a.</span></span> <span data-ttu-id="a1231-207">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-207">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a1231-208">b.</span><span class="sxs-lookup"><span data-stu-id="a1231-208">b.</span></span> <span data-ttu-id="a1231-209">Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-209">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="a1231-210">c.</span><span class="sxs-lookup"><span data-stu-id="a1231-210">c.</span></span> <span data-ttu-id="a1231-211">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-211">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="a1231-212">d.</span><span class="sxs-lookup"><span data-stu-id="a1231-212">d.</span></span> <span data-ttu-id="a1231-213">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-213">Click **Create**.</span></span>
  
### <a name="create-a-workstars-test-user"></a><span data-ttu-id="a1231-214">Workstars 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a1231-214">Create a Workstars test user</span></span>

<span data-ttu-id="a1231-215">이 섹션에서는 Workstars에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-215">In this section, you create a user called Britta Simon in Workstars.</span></span> <span data-ttu-id="a1231-216">작업할 [Workstars 지원 팀](https://support.workstars.com) hello Workstars 플랫폼의 tooadd hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-216">Work with [Workstars support team](https://support.workstars.com) tooadd hello users in hello Workstars platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="a1231-217">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-217">Assign hello Azure AD test user</span></span>

<span data-ttu-id="a1231-218">이 섹션에서는 tooWorkstars 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-218">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkstars.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="a1231-220">**tooassign Britta Simon tooWorkstars hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a1231-220">**tooassign Britta Simon tooWorkstars, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1231-221">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-221">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="a1231-223">Hello 응용 프로그램 목록에서 선택 **Workstars**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-223">In hello applications list, select **Workstars**.</span></span>

    ![hello 응용 프로그램 목록에서 hello Workstars 링크](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_app.png)  

3. <span data-ttu-id="a1231-225">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-225">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="a1231-227">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-227">Click **Add** button.</span></span> <span data-ttu-id="a1231-228">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="a1231-230">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-230">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a1231-231">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a1231-232">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a1231-233">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="a1231-233">Test single sign-on</span></span>

<span data-ttu-id="a1231-234">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-234">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a1231-235">Hello Workstars hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour Workstars 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-235">When you click hello Workstars tile in hello Access Panel, you should get automatically signed-on tooyour Workstars application.</span></span>
<span data-ttu-id="a1231-236">액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a1231-236">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a1231-237">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a1231-237">Additional resources</span></span>

* [<span data-ttu-id="a1231-238">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="a1231-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a1231-239">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="a1231-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_203.png

