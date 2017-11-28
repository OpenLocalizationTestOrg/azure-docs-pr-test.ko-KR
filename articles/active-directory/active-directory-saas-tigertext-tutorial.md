---
title: "자습서: TigerText Secure Messenger와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory와 TigerText Secure Messenger 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03f1e128-5bcb-4e49-b6a3-fe22eedc6d5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: a3d7bb9598658c75c567c15751740d885fe4fc27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tigertext-secure-messenger"></a><span data-ttu-id="49212-103">자습서: TigerText Secure Messenger와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="49212-103">Tutorial: Azure Active Directory integration with TigerText Secure Messenger</span></span>

<span data-ttu-id="49212-104">배웁니다이 자습서에서는 Azure Active Directory (Azure AD)와 toointegrate TigerText Secure 메신저 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="49212-104">In this tutorial, you learn how toointegrate TigerText Secure Messenger with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="49212-105">이점 다음 hello로 제공 TigerText Secure 메신저 Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="49212-105">Integrating TigerText Secure Messenger with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="49212-106">보안 메신저 액세스 tooTigerText을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49212-106">You can control in Azure AD who has access tooTigerText Secure Messenger</span></span>
- <span data-ttu-id="49212-107">에 사용자가 tooautomatically get 로그온 tooTigerText 사용 하도록 설정할 수는 Azure AD 계정와 Secure 메신저 (Single Sign-on)</span><span class="sxs-lookup"><span data-stu-id="49212-107">You can enable your users tooautomatically get signed-on tooTigerText Secure Messenger (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="49212-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49212-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="49212-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49212-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="49212-110">Prerequisites</span></span>

<span data-ttu-id="49212-111">다음 항목 hello가 필요 tooconfigure TigerText Secure Messenger와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-111">tooconfigure Azure AD integration with TigerText Secure Messenger, you need hello following items:</span></span>

- <span data-ttu-id="49212-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="49212-112">An Azure AD subscription</span></span>
- <span data-ttu-id="49212-113">TigerText Secure Messenger Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="49212-113">A TigerText Secure Messenger single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="49212-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="49212-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="49212-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="49212-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="49212-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49212-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="49212-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="49212-118">Scenario description</span></span>
<span data-ttu-id="49212-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="49212-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49212-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="49212-121">Hello 갤러리에서 TigerText Secure Messenger를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-121">Add TigerText Secure Messenger from hello gallery</span></span>
2. <span data-ttu-id="49212-122">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="49212-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tigertext-secure-messenger-from-hello-gallery"></a><span data-ttu-id="49212-123">Hello 갤러리에서 TigerText Secure Messenger를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-123">Add TigerText Secure Messenger from hello gallery</span></span>
<span data-ttu-id="49212-124">tooconfigure hello와의 통합 TigerText Secure 메신저 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Secure Messenger TigerText tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-124">tooconfigure hello integration of TigerText Secure Messenger into Azure AD, you need tooadd TigerText Secure Messenger from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="49212-125">**hello 갤러리에서 TigerText Secure Messenger tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="49212-125">**tooadd TigerText Secure Messenger from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="49212-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="49212-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="49212-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="49212-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="49212-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="49212-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="49212-133">Hello 검색 상자에 입력 **TigerText Secure 메신저**선택, **TigerText Secure 메신저** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="49212-133">In hello search box, type **TigerText Secure Messenger**, select **TigerText Secure Messenger** from result panel then click **Add** button tooadd hello application.</span></span>

    ![갤러리에서 추가](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="49212-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="49212-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="49212-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 하여 TigerText Secure Messenger에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-136">In this section, you configure and test Azure AD single sign-on with TigerText Secure Messenger based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="49212-137">Single sign on toowork에 대 한 Azure AD는 tooknow TigerText Secure Messenger에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TigerText Secure Messenger is tooa user in Azure AD.</span></span> <span data-ttu-id="49212-138">즉, Azure AD 사용자 및 hello TigerText Secure Messenger의 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-138">In other words, a link relationship between an Azure AD user and hello related user in TigerText Secure Messenger needs toobe established.</span></span>

<span data-ttu-id="49212-139">TigerText Secure Messenger의 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="49212-139">In TigerText Secure Messenger, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="49212-140">tooconfigure 및 TigerText Secure Messenger를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-140">tooconfigure and test Azure AD single sign-on with TigerText Secure Messenger, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="49212-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="49212-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="49212-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="49212-143">**[TigerText Secure 메신저 테스트 사용자 만들기](#create-a-tigertext-secure-messenger-test-user)**  -toohave Britta Simon 표현인 연결 된 toohello Azure AD 사용자의 TigerText Secure Messenger에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="49212-143">**[Create a TigerText Secure Messenger test user](#create-a-tigertext-secure-messenger-test-user)** - toohave a counterpart of Britta Simon in TigerText Secure Messenger that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="49212-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="49212-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="49212-145">**[Single Sign-on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="49212-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="49212-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="49212-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="49212-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 및 보안 메신저 TigerText 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TigerText Secure Messenger application.</span></span>

<span data-ttu-id="49212-148">**TigerText Secure Messenger와 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="49212-148">**tooconfigure Azure AD single sign-on with TigerText Secure Messenger, perform hello following steps:**</span></span>

1. <span data-ttu-id="49212-149">Hello hello에 Azure 포털에서에서 **TigerText Secure 메신저** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-149">In hello Azure portal, on hello **TigerText Secure Messenger** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="49212-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="49212-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![SAML 기반 로그온](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_samlbase.png)

3. <span data-ttu-id="49212-153">Hello에 **TigerText 보안 메신저 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-153">On hello **TigerText Secure Messenger Domain and URLs** section, perform hello following steps:</span></span>

    ![TigerText Secure Messenger 도메인 및 URL 섹션](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_url.png)

    <span data-ttu-id="49212-155">a.</span><span class="sxs-lookup"><span data-stu-id="49212-155">a.</span></span> <span data-ttu-id="49212-156">Hello에 **로그온 URL** textbox로 URL 입력:`https://home.tigertext.com`</span><span class="sxs-lookup"><span data-stu-id="49212-156">In hello **Sign-on URL** textbox, type URL as: `https://home.tigertext.com`</span></span>

    <span data-ttu-id="49212-157">b.</span><span class="sxs-lookup"><span data-stu-id="49212-157">b.</span></span> <span data-ttu-id="49212-158">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span><span class="sxs-lookup"><span data-stu-id="49212-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="49212-159">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="49212-159">This value is not real.</span></span> <span data-ttu-id="49212-160">Hello로이 값을 업데이트 합니다. 실제 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="49212-160">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="49212-161">연락처 [TigerText Secure 메신저 클라이언트 지원 팀](mailTo:prosupport@tigertext.com) tooget이이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="49212-161">Contact [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="49212-162">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![SAML 서명 인증서 섹션](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_certificate.png) 

5. <span data-ttu-id="49212-164">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-164">Click **Save** button.</span></span>

    ![저장 단추](./media/active-directory-saas-tigertext-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="49212-166">tooget single sign on 연락처 응용 프로그램에 대해 구성 된 [TigerText Secure 메신저 지원 팀](mailTo:prosupport@tigertext.com) hello 제공 **다운로드 한 메타 데이터**합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-166">tooget single sign-on configured for your application, contact [TigerText Secure Messenger support team](mailTo:prosupport@tigertext.com) and provide them hello **Downloaded metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="49212-167">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="49212-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="49212-168">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="49212-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="49212-169">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="49212-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="49212-170">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="49212-170">Create an Azure AD test user</span></span>
<span data-ttu-id="49212-171">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="49212-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="49212-173">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="49212-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="49212-174">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="49212-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tigertext-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="49212-176">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![사용자 및 그룹 -> 모든 사용자](./media/active-directory-saas-tigertext-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="49212-178">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![추가 단추](./media/active-directory-saas-tigertext-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="49212-180">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![사용자 대화 상자](./media/active-directory-saas-tigertext-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="49212-182">a.</span><span class="sxs-lookup"><span data-stu-id="49212-182">a.</span></span> <span data-ttu-id="49212-183">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="49212-184">b.</span><span class="sxs-lookup"><span data-stu-id="49212-184">b.</span></span> <span data-ttu-id="49212-185">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="49212-186">c.</span><span class="sxs-lookup"><span data-stu-id="49212-186">c.</span></span> <span data-ttu-id="49212-187">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="49212-188">d.</span><span class="sxs-lookup"><span data-stu-id="49212-188">d.</span></span> <span data-ttu-id="49212-189">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-189">Click **Create**.</span></span>
 
### <a name="create-a-tigertext-secure-messenger-test-user"></a><span data-ttu-id="49212-190">TigerText Secure Messenger 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="49212-190">Create a TigerText Secure Messenger test user</span></span>

<span data-ttu-id="49212-191">이 섹션에서는 TigerText에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="49212-191">In this section, you create a user called Britta Simon in TigerText.</span></span> <span data-ttu-id="49212-192">에 게 연락 하세요 너무[TigerText Secure 메신저 클라이언트 지원 팀](mailTo:prosupport@tigertext.com) hello TigerText 플랫폼의 tooadd hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="49212-192">Please reach out too[TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) tooadd hello users in hello TigerText platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="49212-193">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-193">Assign hello Azure AD test user</span></span>

<span data-ttu-id="49212-194">이 섹션에서는 사용 하도록 설정 하면 Azure에서 single sign-on Britta Simon toouse tooTigerText 액세스 권한을 부여 하 여 Messenger 보안을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTigerText Secure Messenger.</span></span>

![사용자 할당][200] 

<span data-ttu-id="49212-196">**tooassign Britta Simon tooTigerText Secure Messenger hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="49212-196">**tooassign Britta Simon tooTigerText Secure Messenger, perform hello following steps:**</span></span>

1. <span data-ttu-id="49212-197">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="49212-199">Hello 응용 프로그램 목록에서 선택 **TigerText Secure 메신저**합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-199">In hello applications list, select **TigerText Secure Messenger**.</span></span>

    ![응용 프로그램 목록의 TigerText Secure Messenger](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_app.png) 

3. <span data-ttu-id="49212-201">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="49212-203">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-203">Click **Add** button.</span></span> <span data-ttu-id="49212-204">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="49212-206">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49212-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="49212-207">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="49212-208">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="49212-209">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="49212-209">Test single sign-on</span></span>

<span data-ttu-id="49212-210">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49212-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="49212-211">Hello 액세스 패널에서에서 hello TigerText 타일을 클릭할 때 자동으로 로그온 tooyour TigerText 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-211">When you click hello TigerText tile in hello Access Panel, you should get automatically signed-on tooyour TigerText application.</span></span> <span data-ttu-id="49212-212">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="49212-212">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="49212-213">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="49212-213">Additional resources</span></span>

* [<span data-ttu-id="49212-214">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="49212-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="49212-215">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="49212-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_203.png

