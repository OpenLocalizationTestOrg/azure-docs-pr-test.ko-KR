---
title: "자습서: Jitbit Helpdesk와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Jitbit Helpdesk 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f6c837bbb910c1e84f7ed9da676c5ab40f75338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a><span data-ttu-id="5c898-103">자습서: Jitbit Helpdesk와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="5c898-103">Tutorial: Azure Active Directory integration with Jitbit Helpdesk</span></span>

<span data-ttu-id="5c898-104">이 자습서에 설명 어떻게 toointegrate Jitbit Helpdesk와 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5c898-104">In this tutorial, you learn how toointegrate Jitbit Helpdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5c898-105">Azure AD와 Jitbit Helpdesk 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-105">Integrating Jitbit Helpdesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5c898-106">액세스 tooJitbit 기술 지원팀에 게 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-106">You can control in Azure AD who has access tooJitbit Helpdesk</span></span>
- <span data-ttu-id="5c898-107">에 사용자가 tooautomatically get 로그온 tooJitbit (Single Sign-on) 기술 지원팀 자신의 Azure AD 계정으로 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-107">You can enable your users tooautomatically get signed-on tooJitbit Helpdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5c898-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5c898-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c898-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5c898-110">Prerequisites</span></span>

<span data-ttu-id="5c898-111">Jitbit Helpdesk와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-111">tooconfigure Azure AD integration with Jitbit Helpdesk, you need hello following items:</span></span>

- <span data-ttu-id="5c898-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="5c898-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5c898-113">Jitbit Helpdesk Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="5c898-113">A Jitbit Helpdesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5c898-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5c898-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5c898-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5c898-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5c898-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5c898-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="5c898-118">Scenario description</span></span>
<span data-ttu-id="5c898-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5c898-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5c898-121">Jitbit Helpdesk hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="5c898-121">Adding Jitbit Helpdesk from hello gallery</span></span>
2. <span data-ttu-id="5c898-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5c898-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jitbit-helpdesk-from-hello-gallery"></a><span data-ttu-id="5c898-123">Jitbit Helpdesk hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="5c898-123">Adding Jitbit Helpdesk from hello gallery</span></span>
<span data-ttu-id="5c898-124">tooconfigure hello와의 통합 Jitbit Helpdesk Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Jitbit Helpdesk tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-124">tooconfigure hello integration of Jitbit Helpdesk into Azure AD, you need tooadd Jitbit Helpdesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5c898-125">**Jitbit Helpdesk hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5c898-125">**tooadd Jitbit Helpdesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c898-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5c898-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5c898-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="5c898-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="5c898-133">Hello 검색 상자에 입력 **Jitbit Helpdesk**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-133">In hello search box, type **Jitbit Helpdesk**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

5. <span data-ttu-id="5c898-135">Hello 결과 패널에서 선택 **Jitbit Helpdesk**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-135">In hello results panel, select **Jitbit Helpdesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5c898-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5c898-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5c898-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Jitbit Helpdesk에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-138">In this section, you configure and test Azure AD single sign-on with Jitbit Helpdesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5c898-139">Single sign on toowork에 대 한 Azure AD는 tooknow Jitbit Helpdesk에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jitbit Helpdesk is tooa user in Azure AD.</span></span> <span data-ttu-id="5c898-140">즉, Azure AD 사용자 및 Jitbit Helpdesk에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-140">In other words, a link relationship between an Azure AD user and hello related user in Jitbit Helpdesk needs toobe established.</span></span>

<span data-ttu-id="5c898-141">Jitbit Helpdesk에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-141">In Jitbit Helpdesk, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5c898-142">tooconfigure 및 Jitbit Helpdesk와 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-142">tooconfigure and test Azure AD single sign-on with Jitbit Helpdesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5c898-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5c898-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5c898-145">**[Jitbit Helpdesk 테스트 사용자 만들기](#creating-a-jitbit-helpdesk-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Jitbit Helpdesk에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-145">**[Creating a Jitbit Helpdesk test user](#creating-a-jitbit-helpdesk-test-user)** - toohave a counterpart of Britta Simon in Jitbit Helpdesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5c898-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5c898-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="5c898-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5c898-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="5c898-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5c898-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Jitbit Helpdesk 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jitbit Helpdesk application.</span></span>

<span data-ttu-id="5c898-150">**Azure AD tooconfigure single sign on Jitbit Helpdesk와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5c898-150">**tooconfigure Azure AD single sign-on with Jitbit Helpdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c898-151">Hello hello에 Azure 포털에서에서 **Jitbit Helpdesk** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-151">In hello Azure portal, on hello **Jitbit Helpdesk** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="5c898-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

3. <span data-ttu-id="5c898-155">Hello에 **Jitbit Helpdesk 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-155">On hello **Jitbit Helpdesk Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    <span data-ttu-id="5c898-157">a.</span><span class="sxs-lookup"><span data-stu-id="5c898-157">a.</span></span> <span data-ttu-id="5c898-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:</span><span class="sxs-lookup"><span data-stu-id="5c898-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > <span data-ttu-id="5c898-159">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-159">This value is not real.</span></span> <span data-ttu-id="5c898-160">Hello로이 값을 업데이트 합니다. 실제 로그온 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-160">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="5c898-161">연락처 [Jitbit Helpdesk 클라이언트 지원 팀](https://www.jitbit.com/support/) tooget이이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-161">Contact [Jitbit Helpdesk Client support team](https://www.jitbit.com/support/) tooget this value.</span></span> 
    
    <span data-ttu-id="5c898-162">b.</span><span class="sxs-lookup"><span data-stu-id="5c898-162">b.</span></span>  <span data-ttu-id="5c898-163">Hello에 **식별자** 텍스트 상자에, 다음과 같이 URL 입력:`https://www.jitbit.com/web-helpdesk/`</span><span class="sxs-lookup"><span data-stu-id="5c898-163">In hello **Identifier** textbox, type a URL as following: `https://www.jitbit.com/web-helpdesk/`</span></span>

    
 


4. <span data-ttu-id="5c898-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

5. <span data-ttu-id="5c898-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5c898-168">Hello에 **Jitbit Helpdesk 구성** 섹션에서 클릭 **Jitbit Helpdesk 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="5c898-168">On hello **Jitbit Helpdesk Configuration** section, click **Configure Jitbit Helpdesk** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5c898-169">복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="5c898-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

7. <span data-ttu-id="5c898-171">다른 웹 브라우저 창에서 Jitbit Helpdesk 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-171">In a different web browser window, log into your Jitbit Helpdesk company site as an administrator.</span></span>

8. <span data-ttu-id="5c898-172">도구 모음의 hello hello 위쪽에 클릭 **관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-172">In hello toolbar on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="5c898-173">![관리](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "관리")</span><span class="sxs-lookup"><span data-stu-id="5c898-173">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

9. <span data-ttu-id="5c898-174">**일반 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-174">Click **General settings**.</span></span>
   
    <span data-ttu-id="5c898-175">![사용자, 회사 및 권한](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "사용자, 회사 및 권한")</span><span class="sxs-lookup"><span data-stu-id="5c898-175">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Users, companies, and permissions")</span></span>

10. <span data-ttu-id="5c898-176">Hello에 **인증 설정** 구성 섹션에서 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-176">In hello **Authentication settings** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="5c898-177">![인증 설정](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "인증 설정")</span><span class="sxs-lookup"><span data-stu-id="5c898-177">![Authentication settings](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")</span></span>
    
    <span data-ttu-id="5c898-178">a.</span><span class="sxs-lookup"><span data-stu-id="5c898-178">a.</span></span> <span data-ttu-id="5c898-179">선택 **사용 SAML 2.0를 single sign-on**와 Single Sign-on (SSO)를 사용 하 여 toosign **OneLogin**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-179">Select **Enable SAML 2.0 single sign on**, toosign in using Single Sign-On (SSO), with **OneLogin**.</span></span>

    <span data-ttu-id="5c898-180">b.</span><span class="sxs-lookup"><span data-stu-id="5c898-180">b.</span></span> <span data-ttu-id="5c898-181">Hello에 **끝점 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-181">In hello **EndPoint URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5c898-182">c.</span><span class="sxs-lookup"><span data-stu-id="5c898-182">c.</span></span> <span data-ttu-id="5c898-183">Open 프로그램 **e-64** 로 인코딩된 인증서를 메모장에 복사 hello 내용을 클립보드의 내용에 복사한 후 toohello **X.509 인증서** textbox</span><span class="sxs-lookup"><span data-stu-id="5c898-183">Open your **base-64** encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>

    <span data-ttu-id="5c898-184">d.</span><span class="sxs-lookup"><span data-stu-id="5c898-184">d.</span></span> <span data-ttu-id="5c898-185">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-185">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="5c898-186">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="5c898-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5c898-187">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="5c898-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5c898-188">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5c898-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5c898-189">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5c898-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="5c898-190">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="5c898-192">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5c898-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c898-193">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5c898-195">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5c898-197">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5c898-199">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5c898-201">a.</span><span class="sxs-lookup"><span data-stu-id="5c898-201">a.</span></span> <span data-ttu-id="5c898-202">Hello에 **이름** 으로 유형 이름 텍스트 상자 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-202">In hello **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="5c898-203">b.</span><span class="sxs-lookup"><span data-stu-id="5c898-203">b.</span></span> <span data-ttu-id="5c898-204">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5c898-205">c.</span><span class="sxs-lookup"><span data-stu-id="5c898-205">c.</span></span> <span data-ttu-id="5c898-206">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5c898-207">d.</span><span class="sxs-lookup"><span data-stu-id="5c898-207">d.</span></span> <span data-ttu-id="5c898-208">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-208">Click **Create**.</span></span>
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a><span data-ttu-id="5c898-209">Jitbit Helpdesk 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5c898-209">Creating a Jitbit Helpdesk test user</span></span>

<span data-ttu-id="5c898-210">Tooenable Azure AD 사용자가 toolog Jitbit Helpdesk에 주문 하 고에 Jitbit Helpdesk에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-210">In order tooenable Azure AD users toolog into Jitbit Helpdesk, they must be provisioned into Jitbit Helpdesk.</span></span>  <span data-ttu-id="5c898-211">Hello Jitbit Helpdesk의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-211">In hello case of Jitbit Helpdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="5c898-212">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5c898-212">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c898-213">Tooyour 로그인 **Jitbit Helpdesk** 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-213">Log in tooyour **Jitbit Helpdesk** tenant.</span></span>

2. <span data-ttu-id="5c898-214">Hello 메뉴에서 hello 위에 표시를 클릭 **관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-214">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="5c898-215">![관리](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "관리")</span><span class="sxs-lookup"><span data-stu-id="5c898-215">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

3. <span data-ttu-id="5c898-216">**사용자, 회사 및 사용 권한**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-216">Click **Users, companies and permissions**.</span></span>
   
    <span data-ttu-id="5c898-217">![사용자, 회사 및 권한](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "사용자, 회사 및 권한")</span><span class="sxs-lookup"><span data-stu-id="5c898-217">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Users, companies, and permissions")</span></span>

4. <span data-ttu-id="5c898-218">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-218">Click **Add user**.</span></span>
   
    <span data-ttu-id="5c898-219">![사용자 추가](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="5c898-219">![Add user](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Add user")</span></span>
   
5. <span data-ttu-id="5c898-220">만들기 섹션 hello tooprovision를 다음과 같이 원하는 hello Azure AD 계정의 hello 데이터를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-220">In hello Create section, type hello data of hello Azure AD account you want tooprovision as follows:</span></span>

    <span data-ttu-id="5c898-221">![만들기](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "만들기")</span><span class="sxs-lookup"><span data-stu-id="5c898-221">![Create](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Create")</span></span>
   
   <span data-ttu-id="5c898-222">a.</span><span class="sxs-lookup"><span data-stu-id="5c898-222">a.</span></span> <span data-ttu-id="5c898-223">Hello에 **Username** 텍스트 상자에 **BrittaSimon**, hello Azure 포털에서와 같이 hello 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-223">In hello **Username** textbox, type **BrittaSimon**, hello user name as in hello Azure portal.</span></span>

   <span data-ttu-id="5c898-224">b.</span><span class="sxs-lookup"><span data-stu-id="5c898-224">b.</span></span> <span data-ttu-id="5c898-225">Hello에 **전자 메일** textbox hello 사용자의 전자 메일 형식 같은  **BrittaSimon@contoso.com** 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-225">In hello **Email** textbox, type email of hello user like **BrittaSimon@contoso.com**.</span></span>

   <span data-ttu-id="5c898-226">c.</span><span class="sxs-lookup"><span data-stu-id="5c898-226">c.</span></span> <span data-ttu-id="5c898-227">Hello에 **이름** 같은 hello 사용자의 형식 이름 텍스트 상자 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-227">In hello **First Name** textbox, type first name of hello user like **Britta**.</span></span>

   <span data-ttu-id="5c898-228">d.</span><span class="sxs-lookup"><span data-stu-id="5c898-228">d.</span></span> <span data-ttu-id="5c898-229">Hello에 **성** 텍스트 상자와 같은 hello 사용자의 성 형식 **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-229">In hello **Last Name** textbox, type last name of hello user like **Simon**.</span></span>
   
   <span data-ttu-id="5c898-230">e.</span><span class="sxs-lookup"><span data-stu-id="5c898-230">e.</span></span> <span data-ttu-id="5c898-231">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-231">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="5c898-232">다른 Jitbit Helpdesk 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 Azure AD 사용자 계정을 Jitbit Helpdesk tooprovision에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-232">You can use any other Jitbit Helpdesk user account creation tools or APIs provided by Jitbit Helpdesk tooprovision Azure AD user accounts.</span></span>
> 
        

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5c898-233">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5c898-234">이 섹션에서는 액세스 tooJitbit 헬프 데스크를 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJitbit Helpdesk.</span></span>

![사용자 할당][200] 

<span data-ttu-id="5c898-236">**tooassign Britta Simon tooJitbit Helpdesk hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5c898-236">**tooassign Britta Simon tooJitbit Helpdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c898-237">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="5c898-239">Hello 응용 프로그램 목록에서 선택 **Jitbit Helpdesk**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-239">In hello applications list, select **Jitbit Helpdesk**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

3. <span data-ttu-id="5c898-241">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="5c898-243">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-243">Click **Add** button.</span></span> <span data-ttu-id="5c898-244">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="5c898-246">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5c898-247">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5c898-248">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5c898-249">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="5c898-249">Testing single sign-on</span></span>

<span data-ttu-id="5c898-250">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5c898-251">Hello Jitbit Helpdesk hello 액세스 패널에서에서 타일을 클릭할 때 Jitbit Helpdesk 응용 프로그램의 로그인 페이지를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-251">When you click hello Jitbit Helpdesk tile in hello Access Panel, you should get login page of Jitbit Helpdesk application.</span></span>
<span data-ttu-id="5c898-252">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5c898-252">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5c898-253">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5c898-253">Additional resources</span></span>

* [<span data-ttu-id="5c898-254">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="5c898-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5c898-255">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="5c898-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_203.png

