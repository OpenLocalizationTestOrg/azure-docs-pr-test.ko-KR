---
title: "자습서: Kintone과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Kintone 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 4f61fb95c643743504699b175beeff06e01c95c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a><span data-ttu-id="84aec-103">자습서: Kintone과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="84aec-103">Tutorial: Azure Active Directory integration with Kintone</span></span>

<span data-ttu-id="84aec-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 Kintone 합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-104">In this tutorial, you learn how toointegrate Kintone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="84aec-105">Azure AD와 Kintone 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-105">Integrating Kintone with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="84aec-106">액세스 tooKintone을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-106">You can control in Azure AD who has access tooKintone</span></span>
- <span data-ttu-id="84aec-107">프로그램 사용자 tooautomatically get 로그온 tooKintone (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-107">You can enable your users tooautomatically get signed-on tooKintone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="84aec-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="84aec-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84aec-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="84aec-110">Prerequisites</span></span>

<span data-ttu-id="84aec-111">Kintone와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-111">tooconfigure Azure AD integration with Kintone, you need hello following items:</span></span>

- <span data-ttu-id="84aec-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="84aec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="84aec-113">Kintone Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="84aec-113">A Kintone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="84aec-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="84aec-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="84aec-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="84aec-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="84aec-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="84aec-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="84aec-118">Scenario description</span></span>
<span data-ttu-id="84aec-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="84aec-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="84aec-121">Kintone는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="84aec-121">Adding Kintone from hello gallery</span></span>
2. <span data-ttu-id="84aec-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="84aec-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kintone-from-hello-gallery"></a><span data-ttu-id="84aec-123">Kintone는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="84aec-123">Adding Kintone from hello gallery</span></span>
<span data-ttu-id="84aec-124">tooconfigure hello와의 통합 Kintone Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Kintone tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-124">tooconfigure hello integration of Kintone into Azure AD, you need tooadd Kintone from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="84aec-125">**Kintone hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="84aec-125">**tooadd Kintone from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="84aec-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="84aec-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="84aec-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="84aec-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="84aec-133">Hello 검색 상자에 입력 **Kintone**합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-133">In hello search box, type **Kintone**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_search.png)

5. <span data-ttu-id="84aec-135">Hello 결과 패널에서 선택 **Kintone**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-135">In hello results panel, select **Kintone**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="84aec-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="84aec-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="84aec-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Kintone에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-138">In this section, you configure and test Azure AD single sign-on with Kintone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="84aec-139">Single sign on toowork에 대 한 Azure AD는 tooknow Kintone에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kintone is tooa user in Azure AD.</span></span> <span data-ttu-id="84aec-140">즉, Azure AD 사용자와 Kintone에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-140">In other words, a link relationship between an Azure AD user and hello related user in Kintone needs toobe established.</span></span>

<span data-ttu-id="84aec-141">Kintone에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-141">In Kintone, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="84aec-142">tooconfigure와 Kintone 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-142">tooconfigure and test Azure AD single sign-on with Kintone, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="84aec-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="84aec-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="84aec-145">**[Kintone 테스트 사용자 만들기](#creating-a-kintone-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Kintone에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-145">**[Creating a Kintone test user](#creating-a-kintone-test-user)** - toohave a counterpart of Britta Simon in Kintone that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="84aec-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="84aec-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="84aec-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="84aec-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="84aec-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="84aec-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Kintone 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kintone application.</span></span>

<span data-ttu-id="84aec-150">**Azure AD tooconfigure single sign on와 Kintone을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="84aec-150">**tooconfigure Azure AD single sign-on with Kintone, perform hello following steps:**</span></span>

1. <span data-ttu-id="84aec-151">Hello hello에 Azure 포털에서에서 **Kintone** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-151">In hello Azure portal, on hello **Kintone** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="84aec-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_samlbase.png)

3. <span data-ttu-id="84aec-155">Hello에 **Kintone 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-155">On hello **Kintone Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_url.png)

    <span data-ttu-id="84aec-157">a.</span><span class="sxs-lookup"><span data-stu-id="84aec-157">a.</span></span> <span data-ttu-id="84aec-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.kintone.com`</span><span class="sxs-lookup"><span data-stu-id="84aec-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.kintone.com`</span></span>

    <span data-ttu-id="84aec-159">b.</span><span class="sxs-lookup"><span data-stu-id="84aec-159">b.</span></span> <span data-ttu-id="84aec-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:</span><span class="sxs-lookup"><span data-stu-id="84aec-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.cybozu.com`|
    | `https://<companyname>.kintone.com`|

    > [!NOTE] 
    > <span data-ttu-id="84aec-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-161">These values are not real.</span></span> <span data-ttu-id="84aec-162">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="84aec-163">연락처 [Kintone 클라이언트 지원 팀](https://www.kintone.com/contact/) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-163">Contact [Kintone Client support team](https://www.kintone.com/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="84aec-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_certificate.png) 

5. <span data-ttu-id="84aec-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kintone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="84aec-168">Hello에 **Kintone 구성** 섹션에서 클릭 **구성 Kintone** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="84aec-168">On hello **Kintone Configuration** section, click **Configure Kintone** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="84aec-169">복사 hello **Sign-Out URL 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="84aec-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_configure.png) 

7. <span data-ttu-id="84aec-171">다른 웹 브라우저 창에서 **Kintone** 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-171">In a different web browser window, log into your **Kintone** company site as an administrator.</span></span>

8. <span data-ttu-id="84aec-172">**설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-172">Click **Settings**.</span></span>
   
    <span data-ttu-id="84aec-173">![설정](./media/active-directory-saas-kintone-tutorial/ic785879.png "설정")</span><span class="sxs-lookup"><span data-stu-id="84aec-173">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

9. <span data-ttu-id="84aec-174">**사용자 및 시스템 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-174">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="84aec-175">![사용자 및 시스템 관리](./media/active-directory-saas-kintone-tutorial/ic785880.png "사용자 및 시스템 관리")</span><span class="sxs-lookup"><span data-stu-id="84aec-175">![Users & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "Users & System Administration")</span></span>

10. <span data-ttu-id="84aec-176">**시스템 관리 \> 보안**에서 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-176">Under **System Administration \> Security** click **Login**.</span></span>
   
    <span data-ttu-id="84aec-177">![로그인](./media/active-directory-saas-kintone-tutorial/ic785881.png "로그인")</span><span class="sxs-lookup"><span data-stu-id="84aec-177">![Login](./media/active-directory-saas-kintone-tutorial/ic785881.png "Login")</span></span>

11. <span data-ttu-id="84aec-178">**SAML 인증 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-178">Click **Enable SAML authentication**.</span></span>
   
    <span data-ttu-id="84aec-179">![SAML 인증](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML 인증")</span><span class="sxs-lookup"><span data-stu-id="84aec-179">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML Authentication")</span></span>

12. <span data-ttu-id="84aec-180">Hello SAML 인증 섹션에서에서 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-180">In hello SAML Authentication section, perform hello following steps:</span></span>
    
    <span data-ttu-id="84aec-181">![SAML 인증](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML 인증")</span><span class="sxs-lookup"><span data-stu-id="84aec-181">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML Authentication")</span></span>
    
    <span data-ttu-id="84aec-182">a.</span><span class="sxs-lookup"><span data-stu-id="84aec-182">a.</span></span> <span data-ttu-id="84aec-183">Hello에 **로그인 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-183">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="84aec-184">b.</span><span class="sxs-lookup"><span data-stu-id="84aec-184">b.</span></span> <span data-ttu-id="84aec-185">Hello에 **로그 아웃 URL** 붙여넣기 hello 값의 텍스트 상자 **Sign-Out URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-185">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="84aec-186">c.</span><span class="sxs-lookup"><span data-stu-id="84aec-186">c.</span></span> <span data-ttu-id="84aec-187">클릭 **찾아보기** tooupload 다운로드 한 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-187">Click **Browse** tooupload your downloaded certificate.</span></span>
    
    <span data-ttu-id="84aec-188">d.</span><span class="sxs-lookup"><span data-stu-id="84aec-188">d.</span></span> <span data-ttu-id="84aec-189">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="84aec-190">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="84aec-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="84aec-191">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="84aec-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="84aec-192">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="84aec-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="84aec-193">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="84aec-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="84aec-194">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="84aec-196">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="84aec-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="84aec-197">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kintone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="84aec-199">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kintone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="84aec-201">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kintone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="84aec-203">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kintone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="84aec-205">a.</span><span class="sxs-lookup"><span data-stu-id="84aec-205">a.</span></span> <span data-ttu-id="84aec-206">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="84aec-207">b.</span><span class="sxs-lookup"><span data-stu-id="84aec-207">b.</span></span> <span data-ttu-id="84aec-208">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="84aec-209">c.</span><span class="sxs-lookup"><span data-stu-id="84aec-209">c.</span></span> <span data-ttu-id="84aec-210">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="84aec-211">d.</span><span class="sxs-lookup"><span data-stu-id="84aec-211">d.</span></span> <span data-ttu-id="84aec-212">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-212">Click **Create**.</span></span>
 
### <a name="creating-a-kintone-test-user"></a><span data-ttu-id="84aec-213">Kintone 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="84aec-213">Creating a Kintone test user</span></span>

<span data-ttu-id="84aec-214">tooenable Azure AD 사용자가 toolog tooKintone에서 프로 비전 해야 Kintone에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-214">tooenable Azure AD users toolog in tooKintone, they must be provisioned into Kintone.</span></span>  
<span data-ttu-id="84aec-215">Hello Kintone의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-215">In hello case of Kintone, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="84aec-216">tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-216">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="84aec-217">Tooyour 로그인 **Kintone** 회사 사이트에 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-217">Log in tooyour **Kintone** company site as an administrator.</span></span>

2. <span data-ttu-id="84aec-218">**설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-218">Click **Setting**.</span></span>
   
    <span data-ttu-id="84aec-219">![설정](./media/active-directory-saas-kintone-tutorial/ic785879.png "설정")</span><span class="sxs-lookup"><span data-stu-id="84aec-219">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

3. <span data-ttu-id="84aec-220">**사용자 및 시스템 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-220">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="84aec-221">![사용자 및 시스템 관리](./media/active-directory-saas-kintone-tutorial/ic785880.png "사용자 및 시스템 관리")</span><span class="sxs-lookup"><span data-stu-id="84aec-221">![User & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "User & System Administration")</span></span>

4. <span data-ttu-id="84aec-222">**사용자 관리**에서 **부서 및 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-222">Under **User Administration**, click **Departments & Users**.</span></span>
   
    <span data-ttu-id="84aec-223">![부서 및 사용자](./media/active-directory-saas-kintone-tutorial/ic785888.png "부서 및 사용자")</span><span class="sxs-lookup"><span data-stu-id="84aec-223">![Department & Users](./media/active-directory-saas-kintone-tutorial/ic785888.png "Department & Users")</span></span>

5. <span data-ttu-id="84aec-224">**새 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-224">Click **New User**.</span></span>
   
    <span data-ttu-id="84aec-225">![새 사용자](./media/active-directory-saas-kintone-tutorial/ic785889.png "새 사용자")</span><span class="sxs-lookup"><span data-stu-id="84aec-225">![New Users](./media/active-directory-saas-kintone-tutorial/ic785889.png "New Users")</span></span>

6. <span data-ttu-id="84aec-226">Hello에 **새 사용자** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-226">In hello **New User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="84aec-227">![새 사용자](./media/active-directory-saas-kintone-tutorial/ic785890.png "새 사용자")</span><span class="sxs-lookup"><span data-stu-id="84aec-227">![New Users](./media/active-directory-saas-kintone-tutorial/ic785890.png "New Users")</span></span>
   
    <span data-ttu-id="84aec-228">a.</span><span class="sxs-lookup"><span data-stu-id="84aec-228">a.</span></span> <span data-ttu-id="84aec-229">입력 **표시 이름**, **로그인 이름**, **새 암호**, **암호 확인**, **전자 메일 주소**, 및 tooprovision hello에 하려는 유효한 AAD 계정의 기타 세부 사항을 관련 텍스트 상자.</span><span class="sxs-lookup"><span data-stu-id="84aec-229">Type a **Display Name**, **Login Name**, **New Password**, **Confirm Password**, **E-mail Address**, and other details of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
 
    <span data-ttu-id="84aec-230">b.</span><span class="sxs-lookup"><span data-stu-id="84aec-230">b.</span></span> <span data-ttu-id="84aec-231">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-231">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="84aec-232">다른 Kintone 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision Kintone에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-232">You can use any other Kintone user account creation tools or APIs provided by Kintone tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="84aec-233">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="84aec-234">이 섹션에서는 tooKintone 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKintone.</span></span>

![사용자 할당][200] 

<span data-ttu-id="84aec-236">**tooassign Britta Simon tooKintone hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="84aec-236">**tooassign Britta Simon tooKintone, perform hello following steps:**</span></span>

1. <span data-ttu-id="84aec-237">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="84aec-239">Hello 응용 프로그램 목록에서 선택 **Kintone**합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-239">In hello applications list, select **Kintone**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_app.png) 

3. <span data-ttu-id="84aec-241">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="84aec-243">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-243">Click **Add** button.</span></span> <span data-ttu-id="84aec-244">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="84aec-246">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="84aec-247">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="84aec-248">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="84aec-249">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="84aec-249">Testing single sign-on</span></span>

<span data-ttu-id="84aec-250">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-250">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="84aec-251">Hello 액세스 패널에서에서 hello Kintone 타일을 클릭할 때 자동으로 로그온 tooyour Kintone 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84aec-251">When you click hello Kintone tile in hello Access Panel, you should get automatically signed-on tooyour Kintone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="84aec-252">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="84aec-252">Additional resources</span></span>

* [<span data-ttu-id="84aec-253">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="84aec-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="84aec-254">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="84aec-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_203.png

