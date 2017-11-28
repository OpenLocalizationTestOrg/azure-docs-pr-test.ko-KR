---
title: "자습서: Menlo Security와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Menlo 보안 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9e63fe6b-0ad0-405d-9e41-6a1a40a41df8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: jeedes
ms.openlocfilehash: 193d12eedf31f4f08e1d141936d6e918c36a2109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-menlo-security"></a><span data-ttu-id="798d5-103">자습서: Menlo Security와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="798d5-103">Tutorial: Azure Active Directory integration with Menlo Security</span></span>

<span data-ttu-id="798d5-104">이 자습서에 설명 어떻게 toointegrate Menlo 보안 Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="798d5-104">In this tutorial, you learn how toointegrate Menlo Security with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="798d5-105">다음 이점을 hello로 제공 Menlo 보안 Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="798d5-105">Integrating Menlo Security with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="798d5-106">액세스 tooMenlo 보안을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-106">You can control in Azure AD who has access tooMenlo Security</span></span>
- <span data-ttu-id="798d5-107">에 사용자가 tooautomatically get 로그온 tooMenlo (Single Sign-on) 보안으로는 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-107">You can enable your users tooautomatically get signed-on tooMenlo Security (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="798d5-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="798d5-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 참조 tooknow 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="798d5-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="798d5-110">[Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="798d5-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="798d5-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="798d5-111">Prerequisites</span></span>

<span data-ttu-id="798d5-112">다음 항목 hello가 필요 tooconfigure Menlo 보안이 포함 된 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-112">tooconfigure Azure AD integration with Menlo Security, you need hello following items:</span></span>

- <span data-ttu-id="798d5-113">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="798d5-113">An Azure AD subscription</span></span>
- <span data-ttu-id="798d5-114">Menlo Security Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="798d5-114">A Menlo Security single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="798d5-115">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="798d5-116">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="798d5-117">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="798d5-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="798d5-118">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="798d5-119">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="798d5-119">Scenario description</span></span>
<span data-ttu-id="798d5-120">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="798d5-121">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="798d5-122">Menlo 보안 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="798d5-122">Adding Menlo Security from hello gallery</span></span>
2. <span data-ttu-id="798d5-123">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="798d5-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-menlo-security-from-hello-gallery"></a><span data-ttu-id="798d5-124">Menlo 보안 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="798d5-124">Adding Menlo Security from hello gallery</span></span>
<span data-ttu-id="798d5-125">tooconfigure hello와의 통합 Menlo 보안 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Menlo 보안 tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-125">tooconfigure hello integration of Menlo Security into Azure AD, you need tooadd Menlo Security from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="798d5-126">**tooadd hello 갤러리에서 Menlo 보안 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="798d5-126">**tooadd Menlo Security from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="798d5-127">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="798d5-129">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="798d5-130">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-130">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="798d5-132">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="798d5-134">Hello 검색 상자에 입력 **Menlo 보안**합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-134">In hello search box, type **Menlo Security**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_search.png)

5. <span data-ttu-id="798d5-136">Hello 결과 패널에서 선택 **Menlo 보안**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-136">In hello results panel, select **Menlo Security**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="798d5-138">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="798d5-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="798d5-139">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Menlo Security에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-139">In this section, you configure and test Azure AD single sign-on with Menlo Security based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="798d5-140">Single sign on toowork에 대 한 Azure AD는 tooknow Menlo 보안에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Menlo Security is tooa user in Azure AD.</span></span> <span data-ttu-id="798d5-141">즉, Azure AD 사용자 및 hello Menlo 보안에서 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-141">In other words, a link relationship between an Azure AD user and hello related user in Menlo Security needs toobe established.</span></span>

<span data-ttu-id="798d5-142">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Menlo 보안에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Menlo Security.</span></span>

<span data-ttu-id="798d5-143">tooconfigure 및 Menlo 보안을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-143">tooconfigure and test Azure AD single sign-on with Menlo Security, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="798d5-144">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="798d5-145">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="798d5-146">**[Menlo 보안 테스트 사용자 만들기](#creating-a-menlo-security-test-user)**  -toohave 사용자의 연결 된 Azure AD toohello 표현인 Menlo 보안 Britta Simon의 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-146">**[Creating a Menlo Security test user](#creating-a-menlo-security-test-user)** - toohave a counterpart of Britta Simon in Menlo Security that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="798d5-147">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="798d5-148">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="798d5-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="798d5-149">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="798d5-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="798d5-150">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Menlo 보안 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Menlo Security application.</span></span>

<span data-ttu-id="798d5-151">**Azure AD tooconfigure single sign on Menlo 보안이 포함 된 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="798d5-151">**tooconfigure Azure AD single sign-on with Menlo Security, perform hello following steps:**</span></span>

1. <span data-ttu-id="798d5-152">Hello hello에 Azure 포털에서에서 **Menlo 보안** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-152">In hello Azure portal, on hello **Menlo Security** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="798d5-154">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_samlbase.png)

3. <span data-ttu-id="798d5-156">Hello에 **Menlo 보안 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-156">On hello **Menlo Security Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_url.png)

    <span data-ttu-id="798d5-158">a.</span><span class="sxs-lookup"><span data-stu-id="798d5-158">a.</span></span> <span data-ttu-id="798d5-159">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.menlosecurity.com/account/login`</span><span class="sxs-lookup"><span data-stu-id="798d5-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.menlosecurity.com/account/login`</span></span>

    <span data-ttu-id="798d5-160">b.</span><span class="sxs-lookup"><span data-stu-id="798d5-160">b.</span></span> <span data-ttu-id="798d5-161">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="798d5-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="798d5-162">이러한 값은 실제 hello 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-162">These values are not hello real.</span></span> <span data-ttu-id="798d5-163">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="798d5-164">연락처 [Menlo 보안 클라이언트 지원 팀](https://www.menlosecurity.com/menlo-contact) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-164">Contact [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="798d5-165">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_certificate.png) 

5. <span data-ttu-id="798d5-167">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-167">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="798d5-169">Hello에 **Menlo 보안 구성** 섹션에서 클릭 **Menlo 보안 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="798d5-169">On hello **Menlo Security Configuration** section, click **Configure Menlo Security** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="798d5-170">복사 hello **SAML 엔터티 ID**, 및 **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="798d5-170">Copy hello **SAML Entity ID**, and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_configure.png) 

7. <span data-ttu-id="798d5-172">tooconfigure single sign on에서 **Menlo 보안** 쪽, 로그인 toohello **Menlo 보안** 관리자 권한으로 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-172">tooconfigure single sign-on on **Menlo Security** side, login toohello **Menlo Security** website as an administrator.</span></span>

8. <span data-ttu-id="798d5-173">아래 **설정** 너무 이동**인증** 하 고 다음 작업 수행:</span><span class="sxs-lookup"><span data-stu-id="798d5-173">Under **Settings** go too**Authentication** and perform following actions:</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-menlosecurity-tutorial/menlo_user_setup.png)

    <span data-ttu-id="798d5-175">a.</span><span class="sxs-lookup"><span data-stu-id="798d5-175">a.</span></span> <span data-ttu-id="798d5-176">Hello 확인란 눈금 **SAML을 사용 하 여 사용자 인증 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-176">Tick hello checkbox **Enable user authentication using SAML**.</span></span>

    <span data-ttu-id="798d5-177">b.</span><span class="sxs-lookup"><span data-stu-id="798d5-177">b.</span></span> <span data-ttu-id="798d5-178">선택 **외부 액세스를 허용** 너무**예**합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-178">Select **Allow External Access** too**Yes**.</span></span>

    <span data-ttu-id="798d5-179">c.</span><span class="sxs-lookup"><span data-stu-id="798d5-179">c.</span></span> <span data-ttu-id="798d5-180">**SAML Provider(SAML 공급자)**에서 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-180">Under **SAML Provider**, select **Azure Active Directory**.</span></span>

    <span data-ttu-id="798d5-181">d.</span><span class="sxs-lookup"><span data-stu-id="798d5-181">d.</span></span> <span data-ttu-id="798d5-182">**SAML 2.0 끝점** : 붙여넣기 hello **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-182">**SAML 2.0 Endpoint** : Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="798d5-183">e.</span><span class="sxs-lookup"><span data-stu-id="798d5-183">e.</span></span> <span data-ttu-id="798d5-184">**서비스 Id (발급자)** : 붙여넣기 hello **SAML 엔터티 ID** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-184">**Service Identifier (Issuer)** : Paste hello **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="798d5-185">f.</span><span class="sxs-lookup"><span data-stu-id="798d5-185">f.</span></span> <span data-ttu-id="798d5-186">**X.509 인증서** : 열기 hello **인증서 (Base64)** 메모장에서 hello Azure 포털에서에서 다운로드 하 고이 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-186">**X.509 Certificate** : Open hello **Certificate (Base64)** downloaded from hello Azure Portal in notepad and paste it in this box.</span></span>

    <span data-ttu-id="798d5-187">g.</span><span class="sxs-lookup"><span data-stu-id="798d5-187">g.</span></span> <span data-ttu-id="798d5-188">클릭 **저장** toosave hello 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-188">Click **Save** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="798d5-189">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="798d5-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="798d5-190">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="798d5-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="798d5-191">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="798d5-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="798d5-192">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="798d5-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="798d5-193">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="798d5-195">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="798d5-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="798d5-196">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="798d5-198">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="798d5-200">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="798d5-202">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="798d5-204">a.</span><span class="sxs-lookup"><span data-stu-id="798d5-204">a.</span></span> <span data-ttu-id="798d5-205">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="798d5-206">b.</span><span class="sxs-lookup"><span data-stu-id="798d5-206">b.</span></span> <span data-ttu-id="798d5-207">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="798d5-208">c.</span><span class="sxs-lookup"><span data-stu-id="798d5-208">c.</span></span> <span data-ttu-id="798d5-209">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="798d5-210">d.</span><span class="sxs-lookup"><span data-stu-id="798d5-210">d.</span></span> <span data-ttu-id="798d5-211">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-211">Click **Create**.</span></span>
 
### <a name="creating-a-menlo-security-test-user"></a><span data-ttu-id="798d5-212">Menlo Security 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="798d5-212">Creating a Menlo Security test user</span></span>
 
<span data-ttu-id="798d5-213">이 섹션에서는 Menlo Security에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-213">In this section, you create a user called Britta Simon in Menlo Security.</span></span> <span data-ttu-id="798d5-214">작업할 [Menlo 보안 클라이언트 지원 팀](https://www.menlosecurity.com/menlo-contact) hello Menlo 보안 플랫폼의 tooadd hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-214">Work with [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) tooadd hello users in hello Menlo Security platform.</span></span> <span data-ttu-id="798d5-215">Single Sign-On을 사용하려면 먼저 사용자를 만들고 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-215">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="798d5-216">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="798d5-217">이 섹션에서는 액세스 tooMenlo 보안 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMenlo Security.</span></span>

![사용자 할당][200] 

<span data-ttu-id="798d5-219">**tooassign Britta Simon tooMenlo 보안을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="798d5-219">**tooassign Britta Simon tooMenlo Security, perform hello following steps:**</span></span>

1. <span data-ttu-id="798d5-220">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="798d5-222">Hello 응용 프로그램 목록에서 선택 **Menlo 보안**합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-222">In hello applications list, select **Menlo Security**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_app.png) 

3. <span data-ttu-id="798d5-224">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="798d5-226">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-226">Click **Add** button.</span></span> <span data-ttu-id="798d5-227">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="798d5-229">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="798d5-230">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="798d5-231">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="798d5-232">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="798d5-232">Testing single sign-on</span></span>

<span data-ttu-id="798d5-233">이 섹션에서는 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-233">In this section, you test your Azure AD single sign-on configuration.</span></span>

<span data-ttu-id="798d5-234">"InPrivate" 또는 "Incognito" 모드 tootrigger 새 인증에서에서 브라우저 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-234">Open a browser window in an "InPrivate" or "Incognito" mode tootrigger a new authentication.</span></span>  <span data-ttu-id="798d5-235">Internet Explorer에서는 Ctrl+Shift+P를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-235">In Internet Explorer, use Ctrl+Shift+P.</span></span>  <span data-ttu-id="798d5-236">Chrome에서는 Ctrl+Shift+N을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-236">In Chrome, use Ctrl+Shift+N.</span></span>  <span data-ttu-id="798d5-237">Hello 개인 탐색 창에서 찾아보기 tooa 보호 된 리소스 하 고 Azure AD 로그인을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-237">In hello private browsing window, browse tooa protected resource and perform an Azure AD login.</span></span>  <span data-ttu-id="798d5-238">로그인을 하면 격리 세션에서 가져왔으면된 toohello 요청 된 사이트 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="798d5-238">Upon successful login, you will be taken toohello requested site in an isolation session.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="798d5-239">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="798d5-239">Additional resources</span></span>

* [<span data-ttu-id="798d5-240">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="798d5-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="798d5-241">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="798d5-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_203.png

