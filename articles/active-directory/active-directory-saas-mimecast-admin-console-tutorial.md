---
title: "자습서: Azure Active Directory와 Mimecast 관리 콘솔의 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Mimecast Admin Console 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 5a04a5abd9ff30d484bce0a5c97a1d3e48b69e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a><span data-ttu-id="259c1-103">자습서: Azure Active Directory와 Mimecast 관리 콘솔의 통합</span><span class="sxs-lookup"><span data-stu-id="259c1-103">Tutorial: Azure Active Directory integration with Mimecast Admin Console</span></span>

<span data-ttu-id="259c1-104">배웁니다이 자습서에서는 Azure Active Directory (Azure AD)와 toointegrate Mimecast Admin 콘솔 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-104">In this tutorial, you learn how toointegrate Mimecast Admin Console with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="259c1-105">Azure AD와 Mimecast Admin Console 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-105">Integrating Mimecast Admin Console with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="259c1-106">TooMimecast 액세스 관리 콘솔을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-106">You can control in Azure AD who has access tooMimecast Admin Console.</span></span>
- <span data-ttu-id="259c1-107">Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooMimecast (Single Sign-on) 관리 콘솔을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-107">You can enable your users tooautomatically get signed-on tooMimecast Admin Console (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="259c1-108">하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="259c1-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="259c1-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="259c1-110">Prerequisites</span></span>

<span data-ttu-id="259c1-111">Mimecast Admin Console와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-111">tooconfigure Azure AD integration with Mimecast Admin Console, you need hello following items:</span></span>

- <span data-ttu-id="259c1-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="259c1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="259c1-113">Mimecast 관리 콘솔 Single Sign-On이 활성화된 구독</span><span class="sxs-lookup"><span data-stu-id="259c1-113">A Mimecast Admin Console single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="259c1-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="259c1-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="259c1-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="259c1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="259c1-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="259c1-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="259c1-118">Scenario description</span></span>
<span data-ttu-id="259c1-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="259c1-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="259c1-121">Mimecast Admin Console hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="259c1-121">Adding Mimecast Admin Console from hello gallery</span></span>
2. <span data-ttu-id="259c1-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="259c1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-admin-console-from-hello-gallery"></a><span data-ttu-id="259c1-123">Mimecast Admin Console hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="259c1-123">Adding Mimecast Admin Console from hello gallery</span></span>
<span data-ttu-id="259c1-124">tooconfigure hello와의 통합 Mimecast Admin Console Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Mimecast Admin Console tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-124">tooconfigure hello integration of Mimecast Admin Console into Azure AD, you need tooadd Mimecast Admin Console from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="259c1-125">**Mimecast Admin Console hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="259c1-125">**tooadd Mimecast Admin Console from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="259c1-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="259c1-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="259c1-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="259c1-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="259c1-133">Hello 검색 상자에 입력 **Mimecast Admin Console**선택, **Mimecast Admin Console** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-133">In hello search box, type **Mimecast Admin Console**, select **Mimecast Admin Console** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Mimecast Admin Console hello 결과 목록에서](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="259c1-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="259c1-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="259c1-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Mimecast 관리 콘솔에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-136">In this section, you configure and test Azure AD single sign-on with Mimecast Admin Console based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="259c1-137">Single sign on toowork에 대 한 Azure AD는 tooknow Mimecast Admin Console에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mimecast Admin Console is tooa user in Azure AD.</span></span> <span data-ttu-id="259c1-138">즉, Azure AD 사용자와 Mimecast Admin Console에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-138">In other words, a link relationship between an Azure AD user and hello related user in Mimecast Admin Console needs toobe established.</span></span>

<span data-ttu-id="259c1-139">Mimecast Admin Console에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-139">In Mimecast Admin Console, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="259c1-140">tooconfigure와 Mimecast Admin Console을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-140">tooconfigure and test Azure AD single sign-on with Mimecast Admin Console, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="259c1-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="259c1-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="259c1-143">**[Mimecast Admin Console 테스트 사용자 만들기](#create-a-mimecast-admin-console-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Mimecast Admin Console에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-143">**[Create a Mimecast Admin Console test user](#create-a-mimecast-admin-console-test-user)** - toohave a counterpart of Britta Simon in Mimecast Admin Console that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="259c1-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="259c1-145">**[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="259c1-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="259c1-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="259c1-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="259c1-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Mimecast Admin Console 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mimecast Admin Console application.</span></span>

<span data-ttu-id="259c1-148">**Azure AD에서 single sign-on와 Mimecast Admin Console tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="259c1-148">**tooconfigure Azure AD single sign-on with Mimecast Admin Console, perform hello following steps:**</span></span>

1. <span data-ttu-id="259c1-149">Hello hello에 Azure 포털에서에서 **Mimecast Admin Console** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-149">In hello Azure portal, on hello **Mimecast Admin Console** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="259c1-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. <span data-ttu-id="259c1-153">Hello에 **Mimecast Admin 콘솔 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-153">On hello **Mimecast Admin Console Domain and URLs** section, perform hello following steps:</span></span>

    ![Mimecast 관리 콘솔 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    <span data-ttu-id="259c1-155">Hello에 **로그온 URL** textbox hello URL 입력:</span><span class="sxs-lookup"><span data-stu-id="259c1-155">In hello **Sign-on URL** textbox, type hello URL:</span></span>
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > <span data-ttu-id="259c1-156">hello 로그온 URL은 지역별로 고유 합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-156">hello sign on URL is region specific.</span></span>

4. <span data-ttu-id="259c1-157">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. <span data-ttu-id="259c1-159">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-159">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="259c1-161">Hello에 **Mimecast Admin 콘솔 구성** 섹션에서 클릭 **Mimecast Admin Console 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="259c1-161">On hello **Mimecast Admin Console Configuration** section, click **Configure Mimecast Admin Console** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="259c1-162">복사 hello **SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="259c1-162">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Mimecast 관리 콘솔 구성](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. <span data-ttu-id="259c1-164">다른 웹 브라우저 창에서 Mimecast 관리 콘솔에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-164">In a different web browser window, log into your Mimecast Admin Console as an administrator.</span></span>

8. <span data-ttu-id="259c1-165">너무 이동**서비스 \> 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-165">Go too**Services \> Application**.</span></span>

    <span data-ttu-id="259c1-166">![서비스](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "서비스")</span><span class="sxs-lookup"><span data-stu-id="259c1-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services")</span></span>

9. <span data-ttu-id="259c1-167">**인증 프로필**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-167">Click **Authentication Profiles**.</span></span>

    <span data-ttu-id="259c1-168">![인증 프로필](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "인증 프로필")</span><span class="sxs-lookup"><span data-stu-id="259c1-168">![Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles")</span></span>
    
10. <span data-ttu-id="259c1-169">**새 인증 프로필**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-169">Click **New Authentication Profile**.</span></span>

    <span data-ttu-id="259c1-170">![새 인증 프로필](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "새 인증 프로필")</span><span class="sxs-lookup"><span data-stu-id="259c1-170">![New Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "New Authentication Profiles")</span></span>

11. <span data-ttu-id="259c1-171">Hello에 **인증 프로필** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-171">In hello **Authentication Profile** section, perform hello following steps:</span></span>

    <span data-ttu-id="259c1-172">![인증 프로필](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "인증 프로필")</span><span class="sxs-lookup"><span data-stu-id="259c1-172">![Authentication Profile](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication Profile")</span></span>
    
    <span data-ttu-id="259c1-173">a.</span><span class="sxs-lookup"><span data-stu-id="259c1-173">a.</span></span> <span data-ttu-id="259c1-174">Hello에 **설명** 텍스트 상자, 구성에 대 한 이름 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-174">In hello **Description** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="259c1-175">b.</span><span class="sxs-lookup"><span data-stu-id="259c1-175">b.</span></span> <span data-ttu-id="259c1-176">**Mimecast 관리 콘솔에 SAML 인증 적용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-176">Select **Enforce SAML Authentication for Mimecast Admin Console**.</span></span>
    
    <span data-ttu-id="259c1-177">c.</span><span class="sxs-lookup"><span data-stu-id="259c1-177">c.</span></span> <span data-ttu-id="259c1-178">**공급자**로 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-178">As **Provider**, select **Azure Active Directory**.</span></span>
    
    <span data-ttu-id="259c1-179">d.</span><span class="sxs-lookup"><span data-stu-id="259c1-179">d.</span></span> <span data-ttu-id="259c1-180">붙여넣기 **SAML 엔터티 ID**, hello에 hello Azure 포털에서에서 복사한 있는 **발급자 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-180">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **Issuer URL** textbox.</span></span>
    
    <span data-ttu-id="259c1-181">e.</span><span class="sxs-lookup"><span data-stu-id="259c1-181">e.</span></span> <span data-ttu-id="259c1-182">붙여넣기 **SAML Single Sign-on 서비스 URL**, hello에 hello Azure 포털에서에서 복사한 있는 **로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-182">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Login URL** textbox.</span></span>

    <span data-ttu-id="259c1-183">f.</span><span class="sxs-lookup"><span data-stu-id="259c1-183">f.</span></span> <span data-ttu-id="259c1-184">붙여넣기 **SAML Single Sign-on 서비스 URL**, hello에 hello Azure 포털에서에서 복사한 있는 **로그 아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-184">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Logout URL** textbox.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="259c1-185">hello 로그인 URL 값과 hello 로그 아웃 URL 값은 hello Mimecast Admin Console hello 동일에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-185">hello Login URL value and hello Logout URL value are for hello Mimecast Admin Console hello same.</span></span>
    
    <span data-ttu-id="259c1-186">g.</span><span class="sxs-lookup"><span data-stu-id="259c1-186">g.</span></span> <span data-ttu-id="259c1-187">메모장에서 Azure 포털에서 다운로드 한 base64 인증서 열기 제거 hello 첫 번째 줄 ("*--*")과 hello 마지막 줄 ("*--*"), 남은의 콘텐츠 복사 hello 클립보드에 복사한 후 toohello **Id 공급자 인증서 (메타 데이터)** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-187">Open your base-64 certificate downloaded from Azure portal in notepad, remove hello first line (“*--*“) and hello last line (“*--*“), copy hello remaining content of it into your clipboard, and then paste it toohello **Identity Provider Certificate (Metadata)** textbox.</span></span>
    
    <span data-ttu-id="259c1-188">h.</span><span class="sxs-lookup"><span data-stu-id="259c1-188">h.</span></span> <span data-ttu-id="259c1-189">**Single Sign-On 허용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-189">Select **Allow Single Sign On**.</span></span>
    
    <span data-ttu-id="259c1-190">i.</span><span class="sxs-lookup"><span data-stu-id="259c1-190">i.</span></span> <span data-ttu-id="259c1-191">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="259c1-192">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="259c1-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="259c1-193">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="259c1-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="259c1-194">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="259c1-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="259c1-195">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="259c1-195">Create an Azure AD test user</span></span>

<span data-ttu-id="259c1-196">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="259c1-198">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="259c1-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="259c1-199">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-199">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="259c1-201">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-201">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="259c1-203">tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="259c1-203">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello 추가 단추](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="259c1-205">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-205">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello 사용자 대화 상자](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    <span data-ttu-id="259c1-207">a.</span><span class="sxs-lookup"><span data-stu-id="259c1-207">a.</span></span> <span data-ttu-id="259c1-208">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-208">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="259c1-209">b.</span><span class="sxs-lookup"><span data-stu-id="259c1-209">b.</span></span> <span data-ttu-id="259c1-210">Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-210">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="259c1-211">c.</span><span class="sxs-lookup"><span data-stu-id="259c1-211">c.</span></span> <span data-ttu-id="259c1-212">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-212">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="259c1-213">d.</span><span class="sxs-lookup"><span data-stu-id="259c1-213">d.</span></span> <span data-ttu-id="259c1-214">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-214">Click **Create**.</span></span>
 
### <a name="create-a-mimecast-admin-console-test-user"></a><span data-ttu-id="259c1-215">Mimecast 관리 콘솔 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="259c1-215">Create a Mimecast Admin Console test user</span></span>

<span data-ttu-id="259c1-216">Tooenable Azure AD 사용자가 toolog Mimecast Admin Console에 주문 하 고에 Mimecast Admin Console에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-216">In order tooenable Azure AD users toolog into Mimecast Admin Console, they must be provisioned into Mimecast Admin Console.</span></span> <span data-ttu-id="259c1-217">Hello Mimecast Admin Console의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-217">In hello case of Mimecast Admin Console, provisioning is a manual task.</span></span>

* <span data-ttu-id="259c1-218">있어야만 tooregister 도메인 사용자를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-218">You need tooregister a domain before you can create users.</span></span>

<span data-ttu-id="259c1-219">**tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:**</span><span class="sxs-lookup"><span data-stu-id="259c1-219">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="259c1-220">Tooyour 로그온 **Mimecast Admin Console** 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-220">Sign on tooyour **Mimecast Admin Console** as administrator.</span></span>
2. <span data-ttu-id="259c1-221">너무 이동**디렉터리 \> 내부**합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-221">Go too**Directories \> Internal**.</span></span>
   
   <span data-ttu-id="259c1-222">![디렉터리](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "디렉터리")</span><span class="sxs-lookup"><span data-stu-id="259c1-222">![Directories](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directories")</span></span>
3. <span data-ttu-id="259c1-223">**새 도메인에 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-223">Click **Register New Domain**.</span></span>
   
   <span data-ttu-id="259c1-224">![새 도메인에 등록](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "새 도메인에 등록")</span><span class="sxs-lookup"><span data-stu-id="259c1-224">![Register New Domain](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Register New Domain")</span></span>
4. <span data-ttu-id="259c1-225">새 도메인을 만든 후 **새 주소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-225">After your new domain has been created, click **New Address**.</span></span>
   
   <span data-ttu-id="259c1-226">![새 주소](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "새 주소")</span><span class="sxs-lookup"><span data-stu-id="259c1-226">![New Address](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "New Address")</span></span>
5. <span data-ttu-id="259c1-227">새 주소 대화 hello hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-227">In hello new address dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="259c1-228">![저장](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "저장")</span><span class="sxs-lookup"><span data-stu-id="259c1-228">![Save](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Save")</span></span>
   
   <span data-ttu-id="259c1-229">a.</span><span class="sxs-lookup"><span data-stu-id="259c1-229">a.</span></span> <span data-ttu-id="259c1-230">형식 hello **전자 메일 주소**, **전역 이름**, **암호**, 및 **암호 확인** 특성 유효한 Azure AD의 계정을 원하는 hello에 tooprovision 관련 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-230">Type hello **Email Address**, **Global Name**, **Password**, and **Confirm Password** attributes of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span>

   <span data-ttu-id="259c1-231">b.</span><span class="sxs-lookup"><span data-stu-id="259c1-231">b.</span></span> <span data-ttu-id="259c1-232">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-232">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="259c1-233">다른 Mimecast Admin Console 사용자 계정 만들기 도구 또는 Mimecast Admin Console tooprovision Azure AD 사용자 계정에서 제공 된 Api를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-233">You can use any other Mimecast Admin Console user account creation tools or APIs provided by Mimecast Admin Console tooprovision Azure AD user accounts.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="259c1-234">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-234">Assign hello Azure AD test user</span></span>

<span data-ttu-id="259c1-235">이 섹션에서는 tooMimecast 액세스 관리 콘솔을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMimecast Admin Console.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="259c1-237">**tooassign Britta Simon tooMimecast 관리 콘솔을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="259c1-237">**tooassign Britta Simon tooMimecast Admin Console, perform hello following steps:**</span></span>

1. <span data-ttu-id="259c1-238">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="259c1-240">Hello 응용 프로그램 목록에서 선택 **Mimecast Admin Console**합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-240">In hello applications list, select **Mimecast Admin Console**.</span></span>

    ![hello 응용 프로그램 목록에서 hello Mimecast Admin Console 링크](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. <span data-ttu-id="259c1-242">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="259c1-244">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-244">Click **Add** button.</span></span> <span data-ttu-id="259c1-245">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="259c1-247">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="259c1-248">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="259c1-249">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="259c1-250">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="259c1-250">Test single sign-on</span></span>

<span data-ttu-id="259c1-251">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-251">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="259c1-252">Hello 액세스 패널에서에서 hello Mimecast Admin Console 타일을 클릭할 때 자동으로 로그온 tooyour Mimecast Admin Console 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-252">When you click hello Mimecast Admin Console tile in hello Access Panel, you should get automatically signed-on tooyour Mimecast Admin Console application.</span></span>
<span data-ttu-id="259c1-253">액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="259c1-253">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="259c1-254">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="259c1-254">Additional resources</span></span>

* [<span data-ttu-id="259c1-255">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="259c1-255">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="259c1-256">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="259c1-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png

