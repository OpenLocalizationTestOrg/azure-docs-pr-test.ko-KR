---
title: "자습서: Wdesk와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Wdesk 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 2c278a5e4f50cc362663efc0f826ff0c0fcf6e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a><span data-ttu-id="1f70a-103">자습서: Wdesk와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="1f70a-103">Tutorial: Azure Active Directory integration with Wdesk</span></span>

<span data-ttu-id="1f70a-104">이 자습서에 설명 어떻게 toointegrate Wdesk Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1f70a-104">In this tutorial, you learn how toointegrate Wdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1f70a-105">다음 이점을 hello로 제공 Wdesk Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="1f70a-105">Integrating Wdesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1f70a-106">액세스 tooWdesk을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-106">You can control in Azure AD who has access tooWdesk</span></span>
- <span data-ttu-id="1f70a-107">프로그램 사용자 tooautomatically get 로그온 tooWdesk (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-107">You can enable your users tooautomatically get signed-on tooWdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1f70a-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1f70a-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 참조 tooknow 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="1f70a-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="1f70a-110">[Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f70a-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f70a-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1f70a-111">Prerequisites</span></span>

<span data-ttu-id="1f70a-112">다음 항목 hello가 필요 tooconfigure Wdesk와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-112">tooconfigure Azure AD integration with Wdesk, you need hello following items:</span></span>

- <span data-ttu-id="1f70a-113">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="1f70a-113">An Azure AD subscription</span></span>
- <span data-ttu-id="1f70a-114">Wdesk Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="1f70a-114">A Wdesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1f70a-115">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1f70a-116">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1f70a-117">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="1f70a-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1f70a-118">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1f70a-119">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="1f70a-119">Scenario description</span></span>
<span data-ttu-id="1f70a-120">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1f70a-121">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1f70a-122">Wdesk은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="1f70a-122">Adding Wdesk from hello gallery</span></span>
2. <span data-ttu-id="1f70a-123">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1f70a-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wdesk-from-hello-gallery"></a><span data-ttu-id="1f70a-124">Wdesk은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="1f70a-124">Adding Wdesk from hello gallery</span></span>
<span data-ttu-id="1f70a-125">tooconfigure hello와의 통합 Wdesk Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Wdesk tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-125">tooconfigure hello integration of Wdesk into Azure AD, you need tooadd Wdesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1f70a-126">**hello 갤러리에서 Wdesk tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1f70a-126">**tooadd Wdesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f70a-127">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1f70a-129">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1f70a-130">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-130">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="1f70a-132">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="1f70a-134">Hello 검색 상자에 입력 **Wdesk**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-134">In hello search box, type **Wdesk**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. <span data-ttu-id="1f70a-136">Hello 결과 패널에서 선택 **Wdesk**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-136">In hello results panel, select **Wdesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1f70a-138">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1f70a-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1f70a-139">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Wdesk에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-139">In this section, you configure and test Azure AD single sign-on with Wdesk based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1f70a-140">Single sign on toowork에 대 한 Azure AD는 tooknow Wdesk에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Wdesk is tooa user in Azure AD.</span></span> <span data-ttu-id="1f70a-141">즉, Azure AD 사용자 및 Wdesk에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-141">In other words, a link relationship between an Azure AD user and hello related user in Wdesk needs toobe established.</span></span>

<span data-ttu-id="1f70a-142">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Wdesk에 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Wdesk.</span></span>

<span data-ttu-id="1f70a-143">tooconfigure 및 Wdesk 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-143">tooconfigure and test Azure AD single sign-on with Wdesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1f70a-144">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1f70a-145">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1f70a-146">**[Wdesk 테스트 사용자 만들기](#creating-a-wdesk-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Wdesk에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-146">**[Creating a Wdesk test user](#creating-a-wdesk-test-user)** - toohave a counterpart of Britta Simon in Wdesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1f70a-147">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1f70a-148">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="1f70a-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1f70a-149">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="1f70a-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1f70a-150">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Wdesk 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Wdesk application.</span></span>

<span data-ttu-id="1f70a-151">**tooconfigure Azure AD single sign on, Wdesk와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1f70a-151">**tooconfigure Azure AD single sign-on with Wdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f70a-152">Hello hello에 Azure 포털에서에서 **Wdesk** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-152">In hello Azure portal, on hello **Wdesk** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="1f70a-154">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. <span data-ttu-id="1f70a-156">Hello에 **Wdesk 도메인 및 Url** tooconfigure hello 응용 프로그램에 필요한 경우 섹션 **IDP** 시작된 모드 hello 다음 단계를 수행:</span><span class="sxs-lookup"><span data-stu-id="1f70a-156">On hello **Wdesk Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    <span data-ttu-id="1f70a-158">a.</span><span class="sxs-lookup"><span data-stu-id="1f70a-158">a.</span></span> <span data-ttu-id="1f70a-159">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="1f70a-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span></span>

    <span data-ttu-id="1f70a-160">b.</span><span class="sxs-lookup"><span data-stu-id="1f70a-160">b.</span></span> <span data-ttu-id="1f70a-161">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="1f70a-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span></span>

4. <span data-ttu-id="1f70a-162">**고급 URL 설정 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="1f70a-163">Tooconfigure hello 응용 프로그램에 필요한 경우 **SP** 시작 모드를 hello 단계 다음에 수행:</span><span class="sxs-lookup"><span data-stu-id="1f70a-163">If you wish tooconfigure hello application in **SP** initiated mode, perform hello following step:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    <span data-ttu-id="1f70a-165">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="1f70a-165">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="1f70a-166">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-166">These values are not real.</span></span> <span data-ttu-id="1f70a-167">이러한 항목을 업데이트 식별자, 회신 URL 및 로그온 URL 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-167">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="1f70a-168">Hello SSO를 구성할 때 WDesk 포털에서 이러한 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-168">You get these values from WDesk portal when you configure hello SSO.</span></span> 
  
5. <span data-ttu-id="1f70a-169">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. <span data-ttu-id="1f70a-171">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-171">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="1f70a-173">다른 웹 브라우저 창에서 로그인 tooWdesk 보안 관리자는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-173">In a different web browser window, login tooWdesk as a Security Administrator.</span></span>

8. <span data-ttu-id="1f70a-174">Hello 아래 왼쪽에서 클릭 **Admin** 선택 **계정 관리자**:</span><span class="sxs-lookup"><span data-stu-id="1f70a-174">In hello bottom left, click **Admin** and choose **Account Admin**:</span></span>
 
     ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. <span data-ttu-id="1f70a-176">너무 Wdesk Admin 이동**보안**, 다음 **SAML** > **SAML 설정**:</span><span class="sxs-lookup"><span data-stu-id="1f70a-176">In Wdesk Admin, navigate too**Security**, then **SAML** > **SAML Settings**:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. <span data-ttu-id="1f70a-178">아래 **일반 설정**, hello 확인 **사용 SAML Single Sign On**:</span><span class="sxs-lookup"><span data-stu-id="1f70a-178">Under **General Settings**, check hello **Enable SAML Single Sign On**:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. <span data-ttu-id="1f70a-180">아래 **서비스 공급자 세부 정보**, hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-180">Under **Service Provider Details**, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      <span data-ttu-id="1f70a-182">a.</span><span class="sxs-lookup"><span data-stu-id="1f70a-182">a.</span></span> <span data-ttu-id="1f70a-183">복사 hello **로그인 URL** 붙여 넣습니다 **로그온 Url** Azure 포털에서 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-183">Copy hello **Login URL** and paste it in **Sign-on Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="1f70a-184">b.</span><span class="sxs-lookup"><span data-stu-id="1f70a-184">b.</span></span> <span data-ttu-id="1f70a-185">복사 hello **메타 데이터 Url** 붙여 넣습니다 **식별자** Azure 포털에서 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-185">Copy hello **Metadata Url** and paste it in **Identifier** textbox on Azure portal.</span></span>
       
      <span data-ttu-id="1f70a-186">c.</span><span class="sxs-lookup"><span data-stu-id="1f70a-186">c.</span></span> <span data-ttu-id="1f70a-187">복사 hello **소비자 url** 붙여 넣습니다 **회신 Url** Azure 포털에서 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-187">Copy hello **Consumer url** and paste it in **Reply Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="1f70a-188">d.</span><span class="sxs-lookup"><span data-stu-id="1f70a-188">d.</span></span> <span data-ttu-id="1f70a-189">클릭 **저장** Azure 포털 toosave hello 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-189">Click **Save** on Azure portal toosave hello changes.</span></span>      

12. <span data-ttu-id="1f70a-190">클릭 **IdP 설정 구성** tooopen **IdP 설정 편집** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="1f70a-190">Click **Configure IdP Settings** tooopen **Edit IdP Settings** dialog.</span></span> <span data-ttu-id="1f70a-191">클릭 **파일 선택** toolocate hello **Metadata.xml** 저장 한 파일을 Azure 포털에서 다음 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-191">Click **Choose File** toolocate hello **Metadata.xml** file you saved from Azure portal, then upload it.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. <span data-ttu-id="1f70a-193">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-193">Click **Save changes**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> <span data-ttu-id="1f70a-195">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="1f70a-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1f70a-196">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="1f70a-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1f70a-197">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1f70a-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1f70a-198">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1f70a-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="1f70a-199">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="1f70a-201">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1f70a-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f70a-202">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1f70a-204">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1f70a-206">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-206">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1f70a-208">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1f70a-210">a.</span><span class="sxs-lookup"><span data-stu-id="1f70a-210">a.</span></span> <span data-ttu-id="1f70a-211">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1f70a-212">b.</span><span class="sxs-lookup"><span data-stu-id="1f70a-212">b.</span></span> <span data-ttu-id="1f70a-213">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1f70a-214">c.</span><span class="sxs-lookup"><span data-stu-id="1f70a-214">c.</span></span> <span data-ttu-id="1f70a-215">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1f70a-216">d.</span><span class="sxs-lookup"><span data-stu-id="1f70a-216">d.</span></span> <span data-ttu-id="1f70a-217">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-217">Click **Create**.</span></span>
 
### <a name="creating-a-wdesk-test-user"></a><span data-ttu-id="1f70a-218">Wdesk 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1f70a-218">Creating a Wdesk test user</span></span>

<span data-ttu-id="1f70a-219">tooenable Azure AD 사용자가 toolog tooWdesk에서 이러한 해야에 프로 비전 Wdesk 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-219">tooenable Azure AD users toolog in tooWdesk, they must be provisioned into Wdesk.</span></span> <span data-ttu-id="1f70a-220">Wdesk의 경우, 수동으로 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-220">In Wdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="1f70a-221">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1f70a-221">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f70a-222">보안 관리자는 tooWdesk에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-222">Log in tooWdesk as a Security Administrator.</span></span>
2. <span data-ttu-id="1f70a-223">너무 이동**Admin** > **계정 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-223">Navigate too**Admin** > **Account Admin**.</span></span>

     ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. <span data-ttu-id="1f70a-225">**피플** 아래에서 **구성원**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-225">Click **Members** under **People**.</span></span>

4. <span data-ttu-id="1f70a-226">클릭 하 여 지금 **멤버 추가** tooopen **멤버 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="1f70a-226">Now click **Add Member** tooopen **Add Member** dialog box.</span></span> 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. <span data-ttu-id="1f70a-228">**사용자** 텍스트 상자와 같은 사용자의 hello 사용자 이름을 입력 합니다  **brittasimon@contoso.com**  클릭 **계속** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-228">In **User** text box, enter hello username of user like **brittasimon@contoso.com** and click **Continue** button.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  <span data-ttu-id="1f70a-230">아래와 같이 hello 세부 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-230">Enter hello details as shown below:</span></span>
  
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    <span data-ttu-id="1f70a-232">a.</span><span class="sxs-lookup"><span data-stu-id="1f70a-232">a.</span></span> <span data-ttu-id="1f70a-233">**전자 메일** 텍스트 상자에 입력와 같은 사용자의 전자 메일 hello  **brittasimon@contoso.com** 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-233">In **E-mail** text box, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="1f70a-234">b.</span><span class="sxs-lookup"><span data-stu-id="1f70a-234">b.</span></span> <span data-ttu-id="1f70a-235">**이름** 텍스트 상자에 hello와 같은 사용자 이름을 입력 합니다 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-235">In **First Name** text box, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="1f70a-236">c.</span><span class="sxs-lookup"><span data-stu-id="1f70a-236">c.</span></span> <span data-ttu-id="1f70a-237">**성** 텍스트 상자에서 hello와 같은 사용자의 성을 입력 **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-237">In **Last Name** text box, enter hello last name of user like **Simon**.</span></span>

7. <span data-ttu-id="1f70a-238">**구성원 저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-238">Click **Save Member** button.</span></span>  

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1f70a-240">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-240">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1f70a-241">이 섹션에서는 tooWdesk 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-241">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWdesk.</span></span>

![사용자 할당][200] 

<span data-ttu-id="1f70a-243">**tooassign Britta Simon tooWdesk hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1f70a-243">**tooassign Britta Simon tooWdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f70a-244">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-244">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="1f70a-246">Hello 응용 프로그램 목록에서 선택 **Wdesk**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-246">In hello applications list, select **Wdesk**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. <span data-ttu-id="1f70a-248">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-248">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="1f70a-250">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-250">Click **Add** button.</span></span> <span data-ttu-id="1f70a-251">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="1f70a-253">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-253">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1f70a-254">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1f70a-255">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1f70a-256">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="1f70a-256">Testing single sign-on</span></span>

<span data-ttu-id="1f70a-257">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-257">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1f70a-258">Hello 액세스 패널에서에서 hello Wdesk 타일을 클릭할 때 자동으로 로그온 tooyour Wdesk 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f70a-258">When you click hello Wdesk tile in hello Access Panel, you should get automatically signed-on tooyour Wdesk application.</span></span>
<span data-ttu-id="1f70a-259">액세스 패널에 대한 자세한 내용은 [Azure 시작](active-directory-saas-access-panel-introduction.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f70a-259">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="1f70a-260">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1f70a-260">Additional resources</span></span>

* [<span data-ttu-id="1f70a-261">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="1f70a-261">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1f70a-262">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="1f70a-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png

