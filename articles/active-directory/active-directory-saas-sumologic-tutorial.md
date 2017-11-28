---
title: "자습서: SumoLogic과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 SumoLogic 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 2ef1bd329f5db8899f0b57744e4c0f6eed1c532f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a><span data-ttu-id="1d58b-103">자습서: SumoLogic과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="1d58b-103">Tutorial: Azure Active Directory integration with SumoLogic</span></span>

<span data-ttu-id="1d58b-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 SumoLogic 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-104">In this tutorial, you learn how toointegrate SumoLogic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1d58b-105">Azure AD와 SumoLogic를 통합 hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-105">Integrating SumoLogic with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1d58b-106">액세스 tooSumoLogic을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-106">You can control in Azure AD who has access tooSumoLogic</span></span>
- <span data-ttu-id="1d58b-107">프로그램 사용자 tooautomatically get 로그온 tooSumoLogic (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-107">You can enable your users tooautomatically get signed-on tooSumoLogic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1d58b-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1d58b-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d58b-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1d58b-110">Prerequisites</span></span>

<span data-ttu-id="1d58b-111">Azure AD 및 SumoLogic 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-111">tooconfigure Azure AD integration with SumoLogic, you need hello following items:</span></span>

- <span data-ttu-id="1d58b-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="1d58b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1d58b-113">SumoLogic Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="1d58b-113">A SumoLogic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1d58b-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1d58b-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1d58b-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="1d58b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1d58b-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1d58b-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="1d58b-118">Scenario description</span></span>
<span data-ttu-id="1d58b-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1d58b-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1d58b-121">SumoLogic는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="1d58b-121">Adding SumoLogic from hello gallery</span></span>
2. <span data-ttu-id="1d58b-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1d58b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sumologic-from-hello-gallery"></a><span data-ttu-id="1d58b-123">SumoLogic는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="1d58b-123">Adding SumoLogic from hello gallery</span></span>
<span data-ttu-id="1d58b-124">tooconfigure hello와의 통합 SumoLogic Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 SumoLogic tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-124">tooconfigure hello integration of SumoLogic into Azure AD, you need tooadd SumoLogic from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1d58b-125">**hello 갤러리에서 SumoLogic tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1d58b-125">**tooadd SumoLogic from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1d58b-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1d58b-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1d58b-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="1d58b-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="1d58b-133">Hello 검색 상자에 입력 **SumoLogic**합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-133">In hello search box, type **SumoLogic**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_search.png)

5. <span data-ttu-id="1d58b-135">Hello 결과 패널에서 선택 **SumoLogic**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-135">In hello results panel, select **SumoLogic**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1d58b-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1d58b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1d58b-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 SumoLogic에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-138">In this section, you configure and test Azure AD single sign-on with SumoLogic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1d58b-139">Single sign on toowork에 대 한 Azure AD는 tooknow SumoLogic에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SumoLogic is tooa user in Azure AD.</span></span> <span data-ttu-id="1d58b-140">즉, Azure AD 사용자와 SumoLogic에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-140">In other words, a link relationship between an Azure AD user and hello related user in SumoLogic needs toobe established.</span></span>

<span data-ttu-id="1d58b-141">SumoLogic에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-141">In SumoLogic, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1d58b-142">tooconfigure와 SumoLogic 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-142">tooconfigure and test Azure AD single sign-on with SumoLogic, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1d58b-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1d58b-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1d58b-145">**[SumoLogic 테스트 사용자 만들기](#creating-a-sumologic-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 SumoLogic에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-145">**[Creating a SumoLogic test user](#creating-a-sumologic-test-user)** - toohave a counterpart of Britta Simon in SumoLogic that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1d58b-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1d58b-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="1d58b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1d58b-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="1d58b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1d58b-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 SumoLogic 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SumoLogic application.</span></span>

<span data-ttu-id="1d58b-150">**Azure AD tooconfigure single sign on와 SumoLogic를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1d58b-150">**tooconfigure Azure AD single sign-on with SumoLogic, perform hello following steps:**</span></span>

1. <span data-ttu-id="1d58b-151">Hello hello에 Azure 포털에서에서 **SumoLogic** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-151">In hello Azure portal, on hello **SumoLogic** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="1d58b-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_samlbase.png)

3. <span data-ttu-id="1d58b-155">Hello에 **SumoLogic 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-155">On hello **SumoLogic Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_url.png)

    <span data-ttu-id="1d58b-157">a.</span><span class="sxs-lookup"><span data-stu-id="1d58b-157">a.</span></span> <span data-ttu-id="1d58b-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<tenantname>.SumoLogic.com`</span><span class="sxs-lookup"><span data-stu-id="1d58b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.SumoLogic.com`</span></span>

    <span data-ttu-id="1d58b-159">b.</span><span class="sxs-lookup"><span data-stu-id="1d58b-159">b.</span></span> <span data-ttu-id="1d58b-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:</span><span class="sxs-lookup"><span data-stu-id="1d58b-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.au.sumologic.com` |

    > [!NOTE] 
    > <span data-ttu-id="1d58b-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-161">These values are not real.</span></span> <span data-ttu-id="1d58b-162">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1d58b-163">연락처 [SumoLogic 클라이언트 지원 팀](https://www.sumologic.com/contact-us/) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-163">Contact [SumoLogic Client support team](https://www.sumologic.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="1d58b-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_certificate.png) 

5. <span data-ttu-id="1d58b-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sumologic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1d58b-168">Hello에 **SumoLogic 구성** 섹션에서 클릭 **구성 SumoLogic** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="1d58b-168">On hello **SumoLogic Configuration** section, click **Configure SumoLogic** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1d58b-169">복사 hello **SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="1d58b-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_configure.png) 

7. <span data-ttu-id="1d58b-171">다른 웹 브라우저 창에서 관리자 권한으로 tooyour SumoLogic 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-171">In a different web browser window, log in tooyour SumoLogic company site as an administrator.</span></span>

8. <span data-ttu-id="1d58b-172">너무 이동**관리 \> 보안**합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-172">Go too**Manage \> Security**.</span></span>
   
    <span data-ttu-id="1d58b-173">![관리](./media/active-directory-saas-sumologic-tutorial/ic778556.png "관리")</span><span class="sxs-lookup"><span data-stu-id="1d58b-173">![Manage](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Manage")</span></span>

9. <span data-ttu-id="1d58b-174">**SAML**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-174">Click **SAML**.</span></span>
   
    <span data-ttu-id="1d58b-175">![전역 보안 설정](./media/active-directory-saas-sumologic-tutorial/ic778557.png "전역 보안 설정")</span><span class="sxs-lookup"><span data-stu-id="1d58b-175">![Global security settings](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Global security settings")</span></span>

10. <span data-ttu-id="1d58b-176">Hello에서 **구성을 선택 하거나 새로 만들** 목록에서 선택 **Azure AD**, 클릭 하 고 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-176">From hello **Select a configuration or create a new one** list, select **Azure AD**, and then click **Configure**.</span></span>
   
    <span data-ttu-id="1d58b-177">![SAML 2.0 구성](./media/active-directory-saas-sumologic-tutorial/ic778558.png "SAML 2.0 구성")</span><span class="sxs-lookup"><span data-stu-id="1d58b-177">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configure SAML 2.0")</span></span>

11. <span data-ttu-id="1d58b-178">Hello에 **SAML 2.0 구성** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-178">On hello **Configure SAML 2.0** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="1d58b-179">![SAML 2.0 구성](./media/active-directory-saas-sumologic-tutorial/ic778559.png "SAML 2.0 구성")</span><span class="sxs-lookup"><span data-stu-id="1d58b-179">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configure SAML 2.0")</span></span>
   
    <span data-ttu-id="1d58b-180">a.</span><span class="sxs-lookup"><span data-stu-id="1d58b-180">a.</span></span> <span data-ttu-id="1d58b-181">Hello에 **구성 이름** 텍스트 상자에 **Azure AD**합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-181">In hello **Configuration Name** textbox, type **Azure AD**.</span></span> 

    <span data-ttu-id="1d58b-182">b.</span><span class="sxs-lookup"><span data-stu-id="1d58b-182">b.</span></span> <span data-ttu-id="1d58b-183">**디버그 모드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-183">Select **Debug Mode**.</span></span>

    <span data-ttu-id="1d58b-184">c.</span><span class="sxs-lookup"><span data-stu-id="1d58b-184">c.</span></span> <span data-ttu-id="1d58b-185">Hello에 **발급자** 붙여넣기 hello 값의 텍스트 상자 **SAML 엔터티 ID**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-185">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="1d58b-186">d.</span><span class="sxs-lookup"><span data-stu-id="1d58b-186">d.</span></span> <span data-ttu-id="1d58b-187">Hello에 **인증 요청 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-187">In hello **Authn Request URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1d58b-188">e.</span><span class="sxs-lookup"><span data-stu-id="1d58b-188">e.</span></span> <span data-ttu-id="1d58b-189">E-64로 인코딩된 인증서 내용을 클립보드의 콘텐츠 복사 hello 메모장에서 열고 후 전체 인증서를 hello **X.509 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-189">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>

    <span data-ttu-id="1d58b-190">f.</span><span class="sxs-lookup"><span data-stu-id="1d58b-190">f.</span></span> <span data-ttu-id="1d58b-191">**이메일 속성**에서는 **SAML 제목 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-191">As **Email Attribute**, select **Use SAML subject**.</span></span>  

    <span data-ttu-id="1d58b-192">g.</span><span class="sxs-lookup"><span data-stu-id="1d58b-192">g.</span></span> <span data-ttu-id="1d58b-193">**SP 시작 로그인 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-193">Select **SP initiated Login Configuration**.</span></span>

    <span data-ttu-id="1d58b-194">h.</span><span class="sxs-lookup"><span data-stu-id="1d58b-194">h.</span></span> <span data-ttu-id="1d58b-195">Hello에 **로그인 경로** 텍스트 상자에 **Azure** 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-195">In hello **Login Path** textbox, type **Azure** and click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="1d58b-196">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="1d58b-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1d58b-197">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="1d58b-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1d58b-198">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1d58b-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1d58b-199">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1d58b-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="1d58b-200">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="1d58b-202">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1d58b-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1d58b-203">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sumologic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1d58b-205">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sumologic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1d58b-207">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sumologic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1d58b-209">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sumologic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1d58b-211">a.</span><span class="sxs-lookup"><span data-stu-id="1d58b-211">a.</span></span> <span data-ttu-id="1d58b-212">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1d58b-213">b.</span><span class="sxs-lookup"><span data-stu-id="1d58b-213">b.</span></span> <span data-ttu-id="1d58b-214">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1d58b-215">c.</span><span class="sxs-lookup"><span data-stu-id="1d58b-215">c.</span></span> <span data-ttu-id="1d58b-216">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1d58b-217">d.</span><span class="sxs-lookup"><span data-stu-id="1d58b-217">d.</span></span> <span data-ttu-id="1d58b-218">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-218">Click **Create**.</span></span>
 
### <a name="creating-a-sumologic-test-user"></a><span data-ttu-id="1d58b-219">SumoLogic 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1d58b-219">Creating a SumoLogic test user</span></span>

<span data-ttu-id="1d58b-220">Tooenable Azure AD 사용자가 toolog tooSumoLogic에 주문 하 고에 프로 비전 된 tooSumoLogic 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-220">In order tooenable Azure AD users toolog in tooSumoLogic, they must be provisioned tooSumoLogic.</span></span>  

* <span data-ttu-id="1d58b-221">Hello SumoLogic의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-221">In hello case of SumoLogic, provisioning is a manual task.</span></span>

<span data-ttu-id="1d58b-222">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1d58b-222">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="1d58b-223">Tooyour 로그인 **SumoLogic** 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-223">Log in tooyour **SumoLogic** tenant.</span></span>

2. <span data-ttu-id="1d58b-224">너무 이동**관리 \> 사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-224">Go too**Manage \> Users**.</span></span>
   
    <span data-ttu-id="1d58b-225">![사용자](./media/active-directory-saas-sumologic-tutorial/ic778561.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="1d58b-225">![Users](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Users")</span></span>

3. <span data-ttu-id="1d58b-226">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-226">Click **Add**.</span></span>
   
    <span data-ttu-id="1d58b-227">![사용자](./media/active-directory-saas-sumologic-tutorial/ic778562.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="1d58b-227">![Users](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Users")</span></span>

4. <span data-ttu-id="1d58b-228">Hello에 **새 사용자** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-228">On hello **New User** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="1d58b-229">![새 사용자](./media/active-directory-saas-sumologic-tutorial/ic778563.png "새 사용자")</span><span class="sxs-lookup"><span data-stu-id="1d58b-229">![New User](./media/active-directory-saas-sumologic-tutorial/ic778563.png "New User")</span></span> 
 
    <span data-ttu-id="1d58b-230">a.</span><span class="sxs-lookup"><span data-stu-id="1d58b-230">a.</span></span> <span data-ttu-id="1d58b-231">형식 hello tooprovision hello에 원하는 hello Azure AD 계정의 정보를 관련 **이름**, **성**, 및 **전자 메일** 입력란입니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-231">Type hello related information of hello Azure AD account you want tooprovision into hello **First Name**, **Last Name**, and **Email** textboxes.</span></span>
  
    <span data-ttu-id="1d58b-232">b.</span><span class="sxs-lookup"><span data-stu-id="1d58b-232">b.</span></span> <span data-ttu-id="1d58b-233">원하는 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-233">Select a role.</span></span>
  
    <span data-ttu-id="1d58b-234">c.</span><span class="sxs-lookup"><span data-stu-id="1d58b-234">c.</span></span> <span data-ttu-id="1d58b-235">**상태**는 **활성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-235">As **Status**, select **Active**.</span></span>
  
    <span data-ttu-id="1d58b-236">ㄹ.</span><span class="sxs-lookup"><span data-stu-id="1d58b-236">d.</span></span> <span data-ttu-id="1d58b-237">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-237">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="1d58b-238">다른 SumoLogic 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision SumoLogic에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-238">You can use any other SumoLogic user account creation tools or APIs provided by SumoLogic tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1d58b-239">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1d58b-240">이 섹션에서는 tooSumoLogic 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSumoLogic.</span></span>

![사용자 할당][200] 

<span data-ttu-id="1d58b-242">**tooassign Britta Simon tooSumoLogic hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1d58b-242">**tooassign Britta Simon tooSumoLogic, perform hello following steps:**</span></span>

1. <span data-ttu-id="1d58b-243">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="1d58b-245">Hello 응용 프로그램 목록에서 선택 **SumoLogic**합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-245">In hello applications list, select **SumoLogic**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_app.png) 

3. <span data-ttu-id="1d58b-247">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="1d58b-249">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-249">Click **Add** button.</span></span> <span data-ttu-id="1d58b-250">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="1d58b-252">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1d58b-253">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1d58b-254">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1d58b-255">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="1d58b-255">Testing single sign-on</span></span>

<span data-ttu-id="1d58b-256">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-256">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1d58b-257">Hello 액세스 패널에서에서 hello SumoLogic 타일을 클릭할 때 자동으로 로그온 tooyour SumoLogic 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d58b-257">When you click hello SumoLogic tile in hello Access Panel, you should get automatically signed-on tooyour SumoLogic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1d58b-258">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1d58b-258">Additional resources</span></span>

* [<span data-ttu-id="1d58b-259">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="1d58b-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1d58b-260">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="1d58b-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_203.png

