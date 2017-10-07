---
title: "자습서: Envoy와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Envoy 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 71f7afcc-1033-4098-9b7e-4f9f2b26f734
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 93add7c1f3cf1fc163acc505f11e34bd696c571c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-envoy"></a><span data-ttu-id="65ecd-103">자습서: Envoy와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="65ecd-103">Tutorial: Azure Active Directory integration with Envoy</span></span>

<span data-ttu-id="65ecd-104">이 자습서에 설명 어떻게 toointegrate Envoy와 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="65ecd-104">In this tutorial, you learn how toointegrate Envoy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65ecd-105">Azure AD와 Envoy 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-105">Integrating Envoy with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="65ecd-106">액세스 tooEnvoy을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-106">You can control in Azure AD who has access tooEnvoy.</span></span>
- <span data-ttu-id="65ecd-107">에 사용자가 tooautomatically get 로그온 tooEnvoy (Single Sign-on)는 Azure AD 계정으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-107">You can enable your users tooautomatically get signed-on tooEnvoy (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="65ecd-108">하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="65ecd-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65ecd-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="65ecd-110">Prerequisites</span></span>

<span data-ttu-id="65ecd-111">Envoy와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-111">tooconfigure Azure AD integration with Envoy, you need hello following items:</span></span>

- <span data-ttu-id="65ecd-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="65ecd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="65ecd-113">Envoy Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="65ecd-113">An Envoy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="65ecd-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="65ecd-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="65ecd-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="65ecd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="65ecd-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="65ecd-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="65ecd-118">Scenario description</span></span>
<span data-ttu-id="65ecd-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="65ecd-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65ecd-121">Envoy는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="65ecd-121">Adding Envoy from hello gallery</span></span>
2. <span data-ttu-id="65ecd-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="65ecd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-envoy-from-hello-gallery"></a><span data-ttu-id="65ecd-123">Envoy는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="65ecd-123">Adding Envoy from hello gallery</span></span>
<span data-ttu-id="65ecd-124">tooconfigure hello와의 통합 Envoy Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Envoy tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-124">tooconfigure hello integration of Envoy into Azure AD, you need tooadd Envoy from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="65ecd-125">**hello 갤러리에서 Envoy tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="65ecd-125">**tooadd Envoy from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="65ecd-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="65ecd-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="65ecd-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="65ecd-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="65ecd-133">Hello 검색 상자에 입력 **Envoy**선택, **Envoy** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-133">In hello search box, type **Envoy**, select **Envoy** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Envoy hello 결과 목록에서](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="65ecd-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="65ecd-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="65ecd-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Envoy에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-136">In this section, you configure and test Azure AD single sign-on with Envoy based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="65ecd-137">Single sign on toowork에 대 한 Azure AD는 tooknow Envoy에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Envoy is tooa user in Azure AD.</span></span> <span data-ttu-id="65ecd-138">즉, Azure AD 사용자와 Envoy에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-138">In other words, a link relationship between an Azure AD user and hello related user in Envoy needs toobe established.</span></span>

<span data-ttu-id="65ecd-139">Hello hello 값을 할당, Envoy에서 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-139">In Envoy, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="65ecd-140">tooconfigure와 Envoy와 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-140">tooconfigure and test Azure AD single sign-on with Envoy, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="65ecd-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="65ecd-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="65ecd-143">**[Envoy 테스트 사용자 만들기](#create-an-envoy-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Envoy에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-143">**[Create an Envoy test user](#create-an-envoy-test-user)** - toohave a counterpart of Britta Simon in Envoy that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="65ecd-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="65ecd-145">**[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="65ecd-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="65ecd-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="65ecd-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="65ecd-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Envoy 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Envoy application.</span></span>

<span data-ttu-id="65ecd-148">**Azure AD tooconfigure single sign on와 Envoy를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="65ecd-148">**tooconfigure Azure AD single sign-on with Envoy, perform hello following steps:**</span></span>

1. <span data-ttu-id="65ecd-149">Hello hello에 Azure 포털에서에서 **Envoy** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-149">In hello Azure portal, on hello **Envoy** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="65ecd-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_samlbase.png)

3. <span data-ttu-id="65ecd-153">Hello에 **Envoy 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-153">On hello **Envoy Domain and URLs** section, perform hello following steps:</span></span>

    ![Envoy 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_url.png)

    <span data-ttu-id="65ecd-155">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<tenant-name>.Envoy.com`</span><span class="sxs-lookup"><span data-stu-id="65ecd-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.Envoy.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="65ecd-156">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-156">This value is not real.</span></span> <span data-ttu-id="65ecd-157">Hello로이 값을 업데이트 합니다. 실제 로그온 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="65ecd-158">연락처 [Envoy 클라이언트 지원 팀](https://envoy.com/contact/) tooget이이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-158">Contact [Envoy Client support team](https://envoy.com/contact/) tooget this value.</span></span>

4. <span data-ttu-id="65ecd-159">Hello에 **SAML 서명 인증서** 섹션을 복사 hello **지문** 인증서의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-159">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate..</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_certificate.png) 

5. <span data-ttu-id="65ecd-161">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-161">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-envoy-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="65ecd-163">Hello에 **Envoy 구성** 섹션에서 클릭 **구성 Envoy** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="65ecd-163">On hello **Envoy Configuration** section, click **Configure Envoy** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="65ecd-164">복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="65ecd-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Envoy 구성](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_configure.png)

7. <span data-ttu-id="65ecd-166">다른 웹 브라우저 창에서 Envoy 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-166">In a different web browser window, log into your Envoy company site as an administrator.</span></span>

8. <span data-ttu-id="65ecd-167">도구 모음의 hello hello 위쪽에 클릭 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-167">In hello toolbar on hello top, click **Settings**.</span></span>

    <span data-ttu-id="65ecd-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span><span class="sxs-lookup"><span data-stu-id="65ecd-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span></span>

9. <span data-ttu-id="65ecd-169">**회사**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-169">Click **Company**.</span></span>

    <span data-ttu-id="65ecd-170">![회사](./media/active-directory-saas-envoy-tutorial/ic776783.png "회사")</span><span class="sxs-lookup"><span data-stu-id="65ecd-170">![Company](./media/active-directory-saas-envoy-tutorial/ic776783.png "Company")</span></span>

10. <span data-ttu-id="65ecd-171">**SAML**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-171">Click **SAML**.</span></span>

    <span data-ttu-id="65ecd-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="65ecd-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span></span>

11. <span data-ttu-id="65ecd-173">Hello에 **SAML 인증** 구성 섹션에서 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-173">In hello **SAML Authentication** configuration section, perform hello following steps:</span></span>

    <span data-ttu-id="65ecd-174">![SAML 인증](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML 인증")</span><span class="sxs-lookup"><span data-stu-id="65ecd-174">![SAML authentication](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML authentication")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="65ecd-175">hello hello HQ 위치 ID 점은 hello 응용 프로그램에 의해 자동으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-175">hello value for hello HQ location ID is auto generated by hello application.</span></span>
    
    <span data-ttu-id="65ecd-176">a.</span><span class="sxs-lookup"><span data-stu-id="65ecd-176">a.</span></span> <span data-ttu-id="65ecd-177">**지문** 텍스트 붙여넣기 hello **지문** Azure 포털에서 복사 되는 인증서의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-177">In **Fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="65ecd-178">b.</span><span class="sxs-lookup"><span data-stu-id="65ecd-178">b.</span></span> <span data-ttu-id="65ecd-179">붙여넣기 **SAML Single Sign-on 서비스 URL** 값으로, 복사한 형성 hello Azure hello에 포털 **ID 공급자 HTTP SAML URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-179">Paste **SAML Single Sign-On Service URL** value, which you have copied form hello Azure portal into hello **IDENTITY PROVIDER HTTP SAML URL** textbox.</span></span>
    
    <span data-ttu-id="65ecd-180">c.</span><span class="sxs-lookup"><span data-stu-id="65ecd-180">c.</span></span> <span data-ttu-id="65ecd-181">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-181">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="65ecd-182">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="65ecd-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="65ecd-183">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="65ecd-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="65ecd-184">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="65ecd-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="65ecd-185">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="65ecd-185">Create an Azure AD test user</span></span>

<span data-ttu-id="65ecd-186">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="65ecd-188">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="65ecd-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="65ecd-189">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-189">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-envoy-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="65ecd-191">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-191">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-envoy-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="65ecd-193">tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="65ecd-193">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello 추가 단추](./media/active-directory-saas-envoy-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="65ecd-195">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-195">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello 사용자 대화 상자](./media/active-directory-saas-envoy-tutorial/create_aaduser_04.png)

    <span data-ttu-id="65ecd-197">a.</span><span class="sxs-lookup"><span data-stu-id="65ecd-197">a.</span></span> <span data-ttu-id="65ecd-198">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-198">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65ecd-199">b.</span><span class="sxs-lookup"><span data-stu-id="65ecd-199">b.</span></span> <span data-ttu-id="65ecd-200">Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-200">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="65ecd-201">c.</span><span class="sxs-lookup"><span data-stu-id="65ecd-201">c.</span></span> <span data-ttu-id="65ecd-202">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-202">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="65ecd-203">d.</span><span class="sxs-lookup"><span data-stu-id="65ecd-203">d.</span></span> <span data-ttu-id="65ecd-204">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-204">Click **Create**.</span></span>
 
### <a name="create-an-envoy-test-user"></a><span data-ttu-id="65ecd-205">Envoy 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="65ecd-205">Create an Envoy test user</span></span>

<span data-ttu-id="65ecd-206">사용자에 대 한 있습니다 tooconfigure tooEnvoy 프로 비전 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-206">There is no action item for you tooconfigure user provisioning tooEnvoy.</span></span> <span data-ttu-id="65ecd-207">할당된 된 사용자 toolog hello 액세스 패널을 사용 하 여 Envoy에를 시도할 때 Envoy hello 사용자의 존재 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-207">When an assigned user tries toolog into Envoy using hello access panel, Envoy checks whether hello user exists.</span></span> <span data-ttu-id="65ecd-208">사용할 수 있는 사용자 계정이 없으면 자동으로 Envoy에 의해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-208">If there is no user account available yet, it is automatically created by Envoy.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="65ecd-209">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-209">Assign hello Azure AD test user</span></span>

<span data-ttu-id="65ecd-210">이 섹션에서는 tooEnvoy 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-210">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEnvoy.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="65ecd-212">**tooassign Britta Simon tooEnvoy hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="65ecd-212">**tooassign Britta Simon tooEnvoy, perform hello following steps:**</span></span>

1. <span data-ttu-id="65ecd-213">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-213">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="65ecd-215">Hello 응용 프로그램 목록에서 선택 **Envoy**합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-215">In hello applications list, select **Envoy**.</span></span>

    ![hello 응용 프로그램 목록에서 hello Envoy 링크](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_app.png)  

3. <span data-ttu-id="65ecd-217">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-217">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="65ecd-219">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-219">Click **Add** button.</span></span> <span data-ttu-id="65ecd-220">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="65ecd-222">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-222">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="65ecd-223">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="65ecd-224">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="65ecd-225">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="65ecd-225">Test single sign-on</span></span>

<span data-ttu-id="65ecd-226">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-226">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="65ecd-227">Hello 액세스 패널에서에서 hello Envoy 타일을 클릭할 때 자동으로 로그온 tooyour Envoy 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-227">When you click hello Envoy tile in hello Access Panel, you should get automatically signed-on tooyour Envoy application.</span></span>
<span data-ttu-id="65ecd-228">액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="65ecd-228">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="65ecd-229">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="65ecd-229">Additional resources</span></span>

* [<span data-ttu-id="65ecd-230">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="65ecd-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="65ecd-231">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="65ecd-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_203.png

