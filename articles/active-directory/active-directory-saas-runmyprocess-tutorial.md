---
title: "자습서: RunMyProcess와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 RunMyProcess 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d31f7395-048b-4a61-9505-5acf9fc68d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f02acda015aeb8d131d8e3ef88bf50c4e8e94750
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-runmyprocess"></a><span data-ttu-id="5185f-103">자습서: RunMyProcess와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="5185f-103">Tutorial: Azure Active Directory integration with RunMyProcess</span></span>

<span data-ttu-id="5185f-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 RunMyProcess 합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-104">In this tutorial, you learn how toointegrate RunMyProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5185f-105">Azure AD와 RunMyProcess 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-105">Integrating RunMyProcess with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5185f-106">액세스 tooRunMyProcess을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-106">You can control in Azure AD who has access tooRunMyProcess</span></span>
- <span data-ttu-id="5185f-107">프로그램 사용자 tooautomatically get 로그온 tooRunMyProcess (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-107">You can enable your users tooautomatically get signed-on tooRunMyProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5185f-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5185f-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5185f-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5185f-110">Prerequisites</span></span>

<span data-ttu-id="5185f-111">RunMyProcess와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-111">tooconfigure Azure AD integration with RunMyProcess, you need hello following items:</span></span>

- <span data-ttu-id="5185f-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="5185f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5185f-113">RunMyProcess Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="5185f-113">A RunMyProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5185f-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5185f-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5185f-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5185f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5185f-117">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-117">If you don't have an Azure AD trial environment, you can get a one-month trial here:[Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5185f-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="5185f-118">Scenario description</span></span>
<span data-ttu-id="5185f-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5185f-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5185f-121">RunMyProcess는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="5185f-121">Adding RunMyProcess from hello gallery</span></span>
2. <span data-ttu-id="5185f-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5185f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-runmyprocess-from-hello-gallery"></a><span data-ttu-id="5185f-123">RunMyProcess는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="5185f-123">Adding RunMyProcess from hello gallery</span></span>
<span data-ttu-id="5185f-124">tooconfigure hello와의 통합 RunMyProcess Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 RunMyProcess tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-124">tooconfigure hello integration of RunMyProcess into Azure AD, you need tooadd RunMyProcess from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5185f-125">**hello 갤러리에서 RunMyProcess tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5185f-125">**tooadd RunMyProcess from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5185f-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5185f-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5185f-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="5185f-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="5185f-133">Hello 검색 상자에 입력 **RunMyProcess**합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-133">In hello search box, type **RunMyProcess**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_search.png)

5. <span data-ttu-id="5185f-135">Hello 결과 패널에서 선택 **RunMyProcess**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-135">In hello results panel, select **RunMyProcess**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5185f-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5185f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5185f-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 RunMyProcess에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-138">In this section, you configure and test Azure AD single sign-on with RunMyProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5185f-139">Single sign on toowork에 대 한 Azure AD는 tooknow RunMyProcess에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RunMyProcess is tooa user in Azure AD.</span></span> <span data-ttu-id="5185f-140">즉, Azure AD 사용자와 RunMyProcess에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-140">In other words, a link relationship between an Azure AD user and hello related user in RunMyProcess needs toobe established.</span></span>

<span data-ttu-id="5185f-141">RunMyProcess에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-141">In RunMyProcess, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5185f-142">tooconfigure와 RunMyProcess 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-142">tooconfigure and test Azure AD single sign-on with RunMyProcess, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5185f-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5185f-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5185f-145">**[RunMyProcess 테스트 사용자 만들기](#creating-a-runmyprocess-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 RunMyProcess에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-145">**[Creating a RunMyProcess test user](#creating-a-runmyprocess-test-user)** - toohave a counterpart of Britta Simon in RunMyProcess that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5185f-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5185f-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="5185f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5185f-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="5185f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5185f-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 RunMyProcess 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RunMyProcess application.</span></span>

<span data-ttu-id="5185f-150">**Azure AD tooconfigure single sign on와 RunMyProcess를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5185f-150">**tooconfigure Azure AD single sign-on with RunMyProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="5185f-151">Hello hello에 Azure 포털에서에서 **RunMyProcess** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-151">In hello Azure portal, on hello **RunMyProcess** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="5185f-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_samlbase.png)

3. <span data-ttu-id="5185f-155">Hello에 **RunMyProcess 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-155">On hello **RunMyProcess Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_url.png)

    <span data-ttu-id="5185f-157">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://live.runmyprocess.com/live/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="5185f-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://live.runmyprocess.com/live/<tenant id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5185f-158">hello 값이 실제 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-158">hello value is not real.</span></span> <span data-ttu-id="5185f-159">업데이트 hello 값과 실제 로그온 URL hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="5185f-160">연락처 [RunMyProcess 클라이언트 지원 팀](mailto:support@runmyprocess.com) tooget hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-160">Contact [RunMyProcess Client support team](mailto:support@runmyprocess.com) tooget hello value.</span></span> 

4. <span data-ttu-id="5185f-161">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_certificate.png) 

5. <span data-ttu-id="5185f-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5185f-165">Hello에 **RunMyProcess 구성** 섹션에서 클릭 **구성 RunMyProcess** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="5185f-165">On hello **RunMyProcess Configuration** section, click **Configure RunMyProcess** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5185f-166">복사 hello **Sign-Out URL 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="5185f-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_configure.png) 

7. <span data-ttu-id="5185f-168">다른 웹 브라우저 창에서 관리자 권한으로 로그온 tooyour RunMyProcess 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-168">In a different web browser window, sign-on tooyour RunMyProcess tenant as an administrator.</span></span>

8. <span data-ttu-id="5185f-169">왼쪽 탐색 패널에서 **계정**을 클릭하고 **구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-169">In left navigation panel, click **Account** and select **Configuration**.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_001.png)

9. <span data-ttu-id="5185f-171">너무 이동**인증 방법을** 섹션 및 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-171">Go too**Authentication method** section and perform below steps:</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_002.png)

    <span data-ttu-id="5185f-173">a.</span><span class="sxs-lookup"><span data-stu-id="5185f-173">a.</span></span> <span data-ttu-id="5185f-174">**메서드**로 **Samlv2를 사용한 SSO**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-174">As **Method**, select **SSO with Samlv2**.</span></span> 

    <span data-ttu-id="5185f-175">b.</span><span class="sxs-lookup"><span data-stu-id="5185f-175">b.</span></span> <span data-ttu-id="5185f-176">Hello에 **SSO 리디렉션** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-176">In hello **SSO redirect** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5185f-177">c.</span><span class="sxs-lookup"><span data-stu-id="5185f-177">c.</span></span> <span data-ttu-id="5185f-178">Hello에 **로그 아웃 리디렉션** 붙여넣기 hello 값의 텍스트 상자 **Sign-Out URL**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-178">In hello **Logout redirect** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5185f-179">d.</span><span class="sxs-lookup"><span data-stu-id="5185f-179">d.</span></span> <span data-ttu-id="5185f-180">Hello에 **이름 Id 형식** 형식 hello 값의 텍스트 상자 **이름 식별자 형식** 으로 **urn: oasis: 이름: tc: SAML:1.1:nameid-: emailAddress**합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-180">In hello **Name Id Format** textbox, type hello value of **Name Identifier Format** as **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="5185f-181">e.</span><span class="sxs-lookup"><span data-stu-id="5185f-181">e.</span></span> <span data-ttu-id="5185f-182">Hello 다운로드 한 인증서 파일의 hello 콘텐츠를 복사 하 고 hello에 붙여 넣습니다 **인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-182">Copy hello content of hello downloaded certificate file and then paste it into hello **Certificate** textbox.</span></span> 
 
    <span data-ttu-id="5185f-183">f.</span><span class="sxs-lookup"><span data-stu-id="5185f-183">f.</span></span> <span data-ttu-id="5185f-184">**저장** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-184">Click **Save** icon.</span></span>

> [!TIP]
> <span data-ttu-id="5185f-185">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="5185f-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5185f-186">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="5185f-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5185f-187">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5185f-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5185f-188">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5185f-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="5185f-189">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="5185f-191">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5185f-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5185f-192">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5185f-194">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5185f-196">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5185f-198">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5185f-200">a.</span><span class="sxs-lookup"><span data-stu-id="5185f-200">a.</span></span> <span data-ttu-id="5185f-201">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5185f-202">b.</span><span class="sxs-lookup"><span data-stu-id="5185f-202">b.</span></span> <span data-ttu-id="5185f-203">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5185f-204">c.</span><span class="sxs-lookup"><span data-stu-id="5185f-204">c.</span></span> <span data-ttu-id="5185f-205">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5185f-206">d.</span><span class="sxs-lookup"><span data-stu-id="5185f-206">d.</span></span> <span data-ttu-id="5185f-207">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-207">Click **Create**.</span></span>
 
### <a name="creating-a-runmyprocess-test-user"></a><span data-ttu-id="5185f-208">RunMyProcess 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5185f-208">Creating a RunMyProcess test user</span></span>

<span data-ttu-id="5185f-209">Tooenable Azure AD 사용자가 toolog tooRunMyProcess에 주문 하 고에서 RunMyProcess에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-209">In order tooenable Azure AD users toolog in tooRunMyProcess, they must be provisioned into RunMyProcess.</span></span> <span data-ttu-id="5185f-210">Hello RunMyProcess의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-210">In hello case of RunMyProcess, provisioning is a manual task.</span></span>

<span data-ttu-id="5185f-211">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5185f-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="5185f-212">관리자 권한으로 RunMyProcess 회사 사이트 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-212">Log in tooyour RunMyProcess company site as an administrator.</span></span>

2. <span data-ttu-id="5185f-213">왼쪽 탐색 패널에서 **계정**을 클릭하고 **사용자**를 선택한 다음 **새 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-213">Click **Account** and select **Users** in left navigation panel, then click **New User**.</span></span>
   
    <span data-ttu-id="5185f-214">![새 사용자](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "새 사용자")</span><span class="sxs-lookup"><span data-stu-id="5185f-214">![New User](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "New User")</span></span>

3. <span data-ttu-id="5185f-215">Hello에 **사용자 설정** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-215">In hello **User Settings** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="5185f-216">![프로필](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "프로필")</span><span class="sxs-lookup"><span data-stu-id="5185f-216">![Profile](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profile")</span></span> 
  
    <span data-ttu-id="5185f-217">a.</span><span class="sxs-lookup"><span data-stu-id="5185f-217">a.</span></span> <span data-ttu-id="5185f-218">형식 hello **이름** 및 **전자 메일** 유효한 Azure의 hello에 tooprovision 복원할 AD 계정의 관련 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-218">Type hello **Name** and **E-mail** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span> 

    <span data-ttu-id="5185f-219">b.</span><span class="sxs-lookup"><span data-stu-id="5185f-219">b.</span></span> <span data-ttu-id="5185f-220">**IDE 언어**, **언어** 및 **프로필**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-220">Select an **IDE language**, **Language**, and **Profile**.</span></span> 

    <span data-ttu-id="5185f-221">c.</span><span class="sxs-lookup"><span data-stu-id="5185f-221">c.</span></span> <span data-ttu-id="5185f-222">선택 **계정 만들기 전자 메일 toome 보낼**합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-222">Select **Send account creation e-mail toome**.</span></span> 

    <span data-ttu-id="5185f-223">d.</span><span class="sxs-lookup"><span data-stu-id="5185f-223">d.</span></span> <span data-ttu-id="5185f-224">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-224">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="5185f-225">다른 RunMyProcess 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 사용자 계정을 RunMyProcess tooprovision Azure Active Directory에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-225">You can use any other RunMyProcess user account creation tools or APIs provided by RunMyProcess tooprovision Azure Active Directory user accounts.</span></span> 
    > 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5185f-226">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5185f-227">이 섹션에서는 tooRunMyProcess 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRunMyProcess.</span></span>

![사용자 할당][200] 

<span data-ttu-id="5185f-229">**tooassign Britta Simon tooRunMyProcess hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5185f-229">**tooassign Britta Simon tooRunMyProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="5185f-230">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="5185f-232">Hello 응용 프로그램 목록에서 선택 **RunMyProcess**합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-232">In hello applications list, select **RunMyProcess**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_app.png) 

3. <span data-ttu-id="5185f-234">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="5185f-236">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-236">Click **Add** button.</span></span> <span data-ttu-id="5185f-237">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="5185f-239">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5185f-240">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5185f-241">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5185f-242">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="5185f-242">Testing single sign-on</span></span>

<span data-ttu-id="5185f-243">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD SSO 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-243">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="5185f-244">Hello RunMyProcess hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour RunMyProcess 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5185f-244">When you click hello RunMyProcess tile in hello Access Panel, you should get automatically signed-on tooyour RunMyProcess application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5185f-245">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5185f-245">Additional resources</span></span>

* [<span data-ttu-id="5185f-246">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="5185f-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5185f-247">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="5185f-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_203.png

