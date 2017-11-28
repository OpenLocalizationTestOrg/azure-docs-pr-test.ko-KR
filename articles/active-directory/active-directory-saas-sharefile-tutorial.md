---
title: "자습서: Citrix ShareFile과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Citrix ShareFile 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: d7eaf140e56c40f9f621062849dd8558588ffd1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a><span data-ttu-id="06de2-103">자습서: Citrix ShareFile과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="06de2-103">Tutorial: Azure Active Directory integration with Citrix ShareFile</span></span>

<span data-ttu-id="06de2-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 Citrix ShareFile 합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-104">In this tutorial, you learn how toointegrate Citrix ShareFile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="06de2-105">Azure AD와 Citrix ShareFile 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-105">Integrating Citrix ShareFile with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="06de2-106">액세스 tooCitrix ShareFile을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-106">You can control in Azure AD who has access tooCitrix ShareFile.</span></span>
- <span data-ttu-id="06de2-107">에 사용자가 tooautomatically get 로그온 tooCitrix ShareFile (Single Sign-on)는 Azure AD 계정으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-107">You can enable your users tooautomatically get signed-on tooCitrix ShareFile (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="06de2-108">하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="06de2-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06de2-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="06de2-110">Prerequisites</span></span>

<span data-ttu-id="06de2-111">Citrix ShareFile과 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-111">tooconfigure Azure AD integration with Citrix ShareFile, you need hello following items:</span></span>

- <span data-ttu-id="06de2-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="06de2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="06de2-113">Citrix ShareFile Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="06de2-113">A Citrix ShareFile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="06de2-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="06de2-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="06de2-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="06de2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="06de2-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="06de2-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="06de2-118">Scenario description</span></span>
<span data-ttu-id="06de2-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="06de2-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="06de2-121">Citrix ShareFile hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="06de2-121">Add Citrix ShareFile from hello gallery</span></span>
2. <span data-ttu-id="06de2-122">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="06de2-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-citrix-sharefile-from-hello-gallery"></a><span data-ttu-id="06de2-123">Citrix ShareFile hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="06de2-123">Add Citrix ShareFile from hello gallery</span></span>
<span data-ttu-id="06de2-124">tooconfigure hello와의 통합 Citrix ShareFile Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Citrix ShareFile tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-124">tooconfigure hello integration of Citrix ShareFile into Azure AD, you need tooadd Citrix ShareFile from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="06de2-125">**hello 갤러리에서 Citrix ShareFile tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="06de2-125">**tooadd Citrix ShareFile from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="06de2-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="06de2-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="06de2-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="06de2-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="06de2-133">Hello 검색 상자에 입력 **Citrix ShareFile**선택, **Citrix ShareFile** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-133">In hello search box, type **Citrix ShareFile**, select **Citrix ShareFile** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Citrix ShareFile hello에 결과 목록](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="06de2-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="06de2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="06de2-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Citrix ShareFile에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-136">In this section, you configure and test Azure AD single sign-on with Citrix ShareFile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="06de2-137">Single sign on toowork에 대 한 Azure AD는 tooknow Citrix ShareFile에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Citrix ShareFile is tooa user in Azure AD.</span></span> <span data-ttu-id="06de2-138">즉, Azure AD 사용자와 Citrix ShareFile에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-138">In other words, a link relationship between an Azure AD user and hello related user in Citrix ShareFile needs toobe established.</span></span>

<span data-ttu-id="06de2-139">Citrix ShareFile에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-139">In Citrix ShareFile, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="06de2-140">tooconfigure 및 Citrix ShareFile과 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-140">tooconfigure and test Azure AD single sign-on with Citrix ShareFile, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="06de2-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="06de2-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="06de2-143">**[Citrix ShareFile 테스트 사용자 만들기](#create-a-citrix-sharefile-test-user)**  -toohave Britta Simon 표현인 연결 된 toohello Azure AD 사용자의 Citrix ShareFile에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-143">**[Create a Citrix ShareFile test user](#create-a-citrix-sharefile-test-user)** - toohave a counterpart of Britta Simon in Citrix ShareFile that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="06de2-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="06de2-145">**[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="06de2-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="06de2-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="06de2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="06de2-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Citrix ShareFile 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Citrix ShareFile application.</span></span>

<span data-ttu-id="06de2-148">**Azure AD tooconfigure single sign on와 Citrix ShareFile hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="06de2-148">**tooconfigure Azure AD single sign-on with Citrix ShareFile, perform hello following steps:**</span></span>

1. <span data-ttu-id="06de2-149">Hello hello에 Azure 포털에서에서 **Citrix ShareFile** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-149">In hello Azure portal, on hello **Citrix ShareFile** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="06de2-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. <span data-ttu-id="06de2-153">Hello에 **Citrix ShareFile 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-153">On hello **Citrix ShareFile Domain and URLs** section, perform hello following steps:</span></span>

    ![Citrix ShareFile 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    <span data-ttu-id="06de2-155">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<tenant-name>.sharefile.com/saml/login`</span><span class="sxs-lookup"><span data-stu-id="06de2-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.sharefile.com/saml/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="06de2-156">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-156">This value is not real.</span></span> <span data-ttu-id="06de2-157">Hello로이 값을 업데이트 합니다. 실제 로그온 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="06de2-158">연락처 [Citrix ShareFile 클라이언트 지원 팀](https://www.citrix.co.in/products/sharefile/support.html) tooget이이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-158">Contact [Citrix ShareFile Client support team](https://www.citrix.co.in/products/sharefile/support.html) tooget this value.</span></span> 

4. <span data-ttu-id="06de2-159">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. <span data-ttu-id="06de2-161">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-161">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="06de2-163">Hello에 **Citrix ShareFile 구성** 섹션에서 클릭 **Citrix ShareFile 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="06de2-163">On hello **Citrix ShareFile Configuration** section, click **Configure Citrix ShareFile** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="06de2-164">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="06de2-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Citrix ShareFile 구성](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. <span data-ttu-id="06de2-166">다른 웹 브라우저 창에서 **Citrix ShareFile** 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-166">In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.</span></span>

8. <span data-ttu-id="06de2-167">도구 모음의 hello hello 위쪽에 클릭 **Admin**합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-167">In hello toolbar on hello top, click **Admin**.</span></span>

9. <span data-ttu-id="06de2-168">Hello 왼쪽된 탐색 창에서 선택 **구성 Single Sign-on**합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-168">In hello left navigation pane, select **Configure Single Sign-On**.</span></span>
   
    <span data-ttu-id="06de2-169">![계정 관리](./media/active-directory-saas-sharefile-tutorial/ic773627.png "계정 관리")</span><span class="sxs-lookup"><span data-stu-id="06de2-169">![Account Administration](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account Administration")</span></span>

10. <span data-ttu-id="06de2-170">Hello에 **Single Sign-on / SAML 2.0 구성** 대화 상자 페이지에서 **기본 설정**, hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-170">On hello **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform hello following steps:</span></span>
   
    <span data-ttu-id="06de2-171">![Single Sign-On](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="06de2-171">![Single sign-on](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Single sign-on")</span></span>
   
    <span data-ttu-id="06de2-172">a.</span><span class="sxs-lookup"><span data-stu-id="06de2-172">a.</span></span> <span data-ttu-id="06de2-173">**SAML 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-173">Click **Enable SAML**.</span></span>
    
    <span data-ttu-id="06de2-174">b.</span><span class="sxs-lookup"><span data-stu-id="06de2-174">b.</span></span> <span data-ttu-id="06de2-175">**IDP 발급자 / 엔터티 ID** 붙여넣기 hello 값의 텍스트 상자 **SAML 엔터티 ID** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-175">In **Your IDP Issuer/ Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="06de2-176">c.</span><span class="sxs-lookup"><span data-stu-id="06de2-176">c.</span></span> <span data-ttu-id="06de2-177">클릭 **변경** 다음 toohello **X.509 인증서** 필드에서 다운로드 한 hello 인증서를 업로드 한 다음 Azure 포털 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-177">Click **Change** next toohello **X.509 Certificate** field and then upload hello certificate you downloaded from hello Azure portal.</span></span>
    
    <span data-ttu-id="06de2-178">d.</span><span class="sxs-lookup"><span data-stu-id="06de2-178">d.</span></span> <span data-ttu-id="06de2-179">**로그인 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-179">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="06de2-180">e.</span><span class="sxs-lookup"><span data-stu-id="06de2-180">e.</span></span> <span data-ttu-id="06de2-181">**로그 아웃 URL** 붙여넣기 hello 값의 텍스트 상자 **Sign-Out URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-181">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

11. <span data-ttu-id="06de2-182">클릭 **저장** hello Citrix ShareFile 관리 포털에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-182">Click **Save** on hello Citrix ShareFile management portal.</span></span>

> [!TIP]
> <span data-ttu-id="06de2-183">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="06de2-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="06de2-184">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="06de2-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="06de2-185">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="06de2-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="06de2-186">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="06de2-186">Create an Azure AD test user</span></span>

<span data-ttu-id="06de2-187">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="06de2-189">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="06de2-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="06de2-190">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-190">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="06de2-192">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-192">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="06de2-194">tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="06de2-194">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello 추가 단추](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="06de2-196">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-196">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello 사용자 대화 상자](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    <span data-ttu-id="06de2-198">a.</span><span class="sxs-lookup"><span data-stu-id="06de2-198">a.</span></span> <span data-ttu-id="06de2-199">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-199">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="06de2-200">b.</span><span class="sxs-lookup"><span data-stu-id="06de2-200">b.</span></span> <span data-ttu-id="06de2-201">Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-201">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="06de2-202">c.</span><span class="sxs-lookup"><span data-stu-id="06de2-202">c.</span></span> <span data-ttu-id="06de2-203">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-203">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="06de2-204">d.</span><span class="sxs-lookup"><span data-stu-id="06de2-204">d.</span></span> <span data-ttu-id="06de2-205">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-205">Click **Create**.</span></span>
 
### <a name="create-a-citrix-sharefile-test-user"></a><span data-ttu-id="06de2-206">Citrix ShareFile 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="06de2-206">Create a Citrix ShareFile test user</span></span>

<span data-ttu-id="06de2-207">Tooenable Azure AD 사용자가 toolog Citrix ShareFile에 주문 하 고에서 Citrix ShareFile에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-207">In order tooenable Azure AD users toolog into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span></span> <span data-ttu-id="06de2-208">Hello Citrix ShareFile의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-208">In hello case of Citrix ShareFile, provisioning is a manual task.</span></span>

<span data-ttu-id="06de2-209">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="06de2-209">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="06de2-210">Tooyour 로그인 **Citrix ShareFile** 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-210">Log in tooyour **Citrix ShareFile** tenant.</span></span>

2. <span data-ttu-id="06de2-211">**사용자 관리 \> 사용자 홈 관리 \> + 직원 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-211">Click **Manage Users \> Manage Users Home \> + Create Employee**.</span></span>
   
   <span data-ttu-id="06de2-212">![직원 만들기](./media/active-directory-saas-sharefile-tutorial/IC781050.png "직원 만들기")</span><span class="sxs-lookup"><span data-stu-id="06de2-212">![Create Employee](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Create Employee")</span></span>

3. <span data-ttu-id="06de2-213">Hello에 **기본 정보** 섹션에서 아래 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-213">On hello **Basic Information** section, perform below steps:</span></span>
   
   <span data-ttu-id="06de2-214">![기본 정보](./media/active-directory-saas-sharefile-tutorial/IC799951.png "기본 정보")</span><span class="sxs-lookup"><span data-stu-id="06de2-214">![Basic Information](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Basic Information")</span></span>
   
   <span data-ttu-id="06de2-215">a.</span><span class="sxs-lookup"><span data-stu-id="06de2-215">a.</span></span> <span data-ttu-id="06de2-216">Hello에 **전자 메일 주소** textbox로 Britta Simon의 hello 전자 메일 주소를 입력  **brittasimon@contoso.com** 합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-216">In hello **Email Address** textbox, type hello email address of Britta Simon as **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="06de2-217">b.</span><span class="sxs-lookup"><span data-stu-id="06de2-217">b.</span></span> <span data-ttu-id="06de2-218">Hello에 **이름** 텍스트 상자에 **이름** 의 사용자에 게 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-218">In hello **First Name** textbox, type **first name** of user as **Britta**.</span></span>
   
   <span data-ttu-id="06de2-219">c.</span><span class="sxs-lookup"><span data-stu-id="06de2-219">c.</span></span> <span data-ttu-id="06de2-220">Hello에 **성** 텍스트 상자에 **성** 의 사용자에 게 **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-220">In hello **Last Name** textbox, type **last name** of user as **Simon**.</span></span>

4. <span data-ttu-id="06de2-221">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-221">Click **Add User**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="06de2-222">hello Azure AD 계정 보유자는 전자 메일을 받게 되 고 링크 tooconfirm 자신의 계정을 활성화 되기 전에 수행 됩니다. 다른 Citrix ShareFile 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 Azure AD 사용자 계정을 Citrix ShareFile tooprovision에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-222">hello Azure AD account holder will receive an email and follow a link tooconfirm their account before it becomes active.You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="06de2-223">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-223">Assign hello Azure AD test user</span></span>

<span data-ttu-id="06de2-224">이 섹션에서는 액세스 tooCitrix ShareFile을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCitrix ShareFile.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="06de2-226">**tooassign Britta Simon tooCitrix ShareFile hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="06de2-226">**tooassign Britta Simon tooCitrix ShareFile, perform hello following steps:**</span></span>

1. <span data-ttu-id="06de2-227">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="06de2-229">Hello 응용 프로그램 목록에서 선택 **Citrix ShareFile**합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-229">In hello applications list, select **Citrix ShareFile**.</span></span>

    ![hello hello 응용 프로그램 목록에서 Citrix ShareFile 링크](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. <span data-ttu-id="06de2-231">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="06de2-233">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-233">Click **Add** button.</span></span> <span data-ttu-id="06de2-234">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="06de2-236">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="06de2-237">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="06de2-238">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="06de2-239">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="06de2-239">Test single sign-on</span></span>

<span data-ttu-id="06de2-240">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="06de2-241">Hello Citrix ShareFile hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour Citrix ShareFile 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-241">When you click hello Citrix ShareFile tile in hello Access Panel, you should get automatically signed-on tooyour Citrix ShareFile application.</span></span>
<span data-ttu-id="06de2-242">액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="06de2-242">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="06de2-243">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="06de2-243">Additional resources</span></span>

* [<span data-ttu-id="06de2-244">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="06de2-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="06de2-245">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="06de2-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

