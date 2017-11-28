---
title: "자습서: Velpic SAML과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Velpic SAML 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 613947d8fe95113382a2cdc0f79ce9eda85a0127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a><span data-ttu-id="38a01-103">자습서: Velpic SAML과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="38a01-103">Tutorial: Azure Active Directory integration with Velpic SAML</span></span>

<span data-ttu-id="38a01-104">이 자습서에 설명 어떻게 toointegrate Velpic SAML Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="38a01-104">In this tutorial, you learn how toointegrate Velpic SAML with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="38a01-105">다음 이점을 hello로 제공 Velpic SAML Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="38a01-105">Integrating Velpic SAML with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="38a01-106">액세스 tooVelpic SAML을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-106">You can control in Azure AD who has access tooVelpic SAML</span></span>
- <span data-ttu-id="38a01-107">에 사용자가 tooautomatically get 로그온 tooVelpic (Single Sign-on)는 SAML 자신의 Azure AD 계정으로 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-107">You can enable your users tooautomatically get signed-on tooVelpic SAML (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="38a01-108">하나의 중앙 위치-hello Azure 관리 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="38a01-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38a01-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="38a01-110">Prerequisites</span></span>

<span data-ttu-id="38a01-111">다음 항목 hello가 필요 tooconfigure Velpic SAML와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-111">tooconfigure Azure AD integration with Velpic SAML, you need hello following items:</span></span>

- <span data-ttu-id="38a01-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="38a01-112">An Azure AD subscription</span></span>
- <span data-ttu-id="38a01-113">Velpic SAML Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="38a01-113">A Velpic SAML single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="38a01-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="38a01-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="38a01-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="38a01-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="38a01-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="38a01-118">Scenario description</span></span>
<span data-ttu-id="38a01-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="38a01-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="38a01-121">Hello 갤러리에서 Velpic SAML 추가</span><span class="sxs-lookup"><span data-stu-id="38a01-121">Adding Velpic SAML from hello gallery</span></span>
2. <span data-ttu-id="38a01-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="38a01-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-velpic-saml-from-hello-gallery"></a><span data-ttu-id="38a01-123">Hello 갤러리에서 Velpic SAML 추가</span><span class="sxs-lookup"><span data-stu-id="38a01-123">Adding Velpic SAML from hello gallery</span></span>
<span data-ttu-id="38a01-124">tooconfigure hello와의 통합 Velpic SAML Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Velpic SAML tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-124">tooconfigure hello integration of Velpic SAML into Azure AD, you need tooadd Velpic SAML from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="38a01-125">**hello 갤러리에서 Velpic SAML tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="38a01-125">**tooadd Velpic SAML from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="38a01-126">Hello에  **[Azure 관리 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="38a01-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="38a01-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="38a01-131">클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="38a01-133">Hello 검색 상자에 입력 **Velpic SAML**합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-133">In hello search box, type **Velpic SAML**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. <span data-ttu-id="38a01-135">Hello 결과 패널에서 선택 **Velpic SAML**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-135">In hello results panel, select **Velpic SAML**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="38a01-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="38a01-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="38a01-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Velpic SAML에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-138">In this section, you configure and test Azure AD single sign-on with Velpic SAML based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="38a01-139">Single sign on toowork에 대 한 Azure AD는 tooknow Velpic saml에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Velpic SAML is tooa user in Azure AD.</span></span> <span data-ttu-id="38a01-140">즉, Azure AD 사용자 및 Velpic saml에서 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-140">In other words, a link relationship between an Azure AD user and hello related user in Velpic SAML needs toobe established.</span></span>

<span data-ttu-id="38a01-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Velpic saml에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Velpic SAML.</span></span>

<span data-ttu-id="38a01-142">tooconfigure 및 Velpic SAML을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-142">tooconfigure and test Azure AD single sign-on with Velpic SAML, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="38a01-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="38a01-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="38a01-145">**[Velpic SAML 테스트 사용자 만들기](#creating-a-velpic-saml-test-user)**  -toohave 그녀의 연결 된 Azure AD toohello 표현인 Velpic saml Britta Simon의 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-145">**[Creating a Velpic SAML test user](#creating-a-velpic-saml-test-user)** - toohave a counterpart of Britta Simon in Velpic SAML that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="38a01-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="38a01-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="38a01-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="38a01-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="38a01-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="38a01-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 관리 포털에서 설정 및 Velpic SAML 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Velpic SAML application.</span></span>

<span data-ttu-id="38a01-150">**Azure AD tooconfigure single sign on Velpic saml hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="38a01-150">**tooconfigure Azure AD single sign-on with Velpic SAML, perform hello following steps:**</span></span>

1. <span data-ttu-id="38a01-151">Hello에 hello Azure 관리 포털에서 **Velpic SAML** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-151">In hello Azure Management portal, on hello **Velpic SAML** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="38a01-153">Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. <span data-ttu-id="38a01-155">Hello에 hello 세부 사항을 입력 **Velpic SAML 도메인 및 Url** 섹션-</span><span class="sxs-lookup"><span data-stu-id="38a01-155">Enter hello details in hello **Velpic SAML Domain and URLs** section-</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    <span data-ttu-id="38a01-157">a.</span><span class="sxs-lookup"><span data-stu-id="38a01-157">a.</span></span> <span data-ttu-id="38a01-158">Hello에 **로그온 URL** 형식 hello 값으로 텍스트 상자:`https://<sub-domain>.velpicsaml.net`</span><span class="sxs-lookup"><span data-stu-id="38a01-158">In hello **Sign-on URL** textbox, type hello value as: `https://<sub-domain>.velpicsaml.net`</span></span>

    <span data-ttu-id="38a01-159">b.</span><span class="sxs-lookup"><span data-stu-id="38a01-159">b.</span></span> <span data-ttu-id="38a01-160">Hello에 **식별자** 텍스트 붙여넣기 hello **'Single sign on URL'** 값`https://auth.velpic.com/saml/v2/<entity-id>/login`</span><span class="sxs-lookup"><span data-stu-id="38a01-160">In hello **Identifier** textbox, paste hello **‘Single sign on URL’** value `https://auth.velpic.com/saml/v2/<entity-id>/login`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="38a01-161">Hello Velpic SAML 팀이 hello 로그온 URL 제공 하 고 Velpic SAML 쪽 hello SSO 플러그 인을 구성할 때 식별자 값에 사용할 수 있습니다 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="38a01-161">Please note that hello Sign on URL will be provided by hello Velpic SAML team and Identifier value will be available when you configure hello SSO Plugin on Velpic SAML side.</span></span> <span data-ttu-id="38a01-162">Toocopy Velpic SAML 응용 프로그램 페이지에서 값는 여기에 붙여 넣이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-162">You need toocopy that value from Velpic SAML application  page and paste it here.</span></span>

4. <span data-ttu-id="38a01-163">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello XML 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. <span data-ttu-id="38a01-165">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-165">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="38a01-167">Hello Velpic SAML 구성 섹션에서 창 로그온 Velpic SAML 구성 tooopen 구성을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-167">On hello Velpic SAML Configuration section, click Configure Velpic SAML tooopen Configure sign-on window.</span></span> <span data-ttu-id="38a01-168">Hello 빠른 참조 섹션에서에서 hello SAML 엔터티 ID를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-168">Copy hello SAML Entity ID from hello Quick Reference section.</span></span>

7. <span data-ttu-id="38a01-169">다른 웹 브라우저 창에서 Velpic SAML 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-169">In a different web browser window, log into your Velpic SAML company site as an administrator.</span></span>

8. <span data-ttu-id="38a01-170">클릭 **관리** 탭 하 고 이동 너무**통합** 에 tooclick 해야 하는 섹션 **플러그 인** 단추 toocreate 새 플러그 인 로그인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-170">Click on **Manage** tab and go too**Integration** section where you need tooclick on **Plugins** button toocreate new plugin for Sign-In.</span></span>

    ![플러그 인](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. <span data-ttu-id="38a01-172">Hello 클릭 **'플러그 인을 추가 합니다.'** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-172">Click on hello **‘Add plugin’** button.</span></span>
    
    ![플러그 인](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. <span data-ttu-id="38a01-174">Hello 클릭 **SAML** hello 플러그 인 추가 페이지에 바둑판식으로 배열 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-174">Click on hello **SAML** tile in hello Add Plugin page.</span></span>
    
    ![플러그 인](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. <span data-ttu-id="38a01-176">Hello 새 SAML 플러그 인의 hello 이름을 입력 하 고 hello 클릭 **'Add'** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-176">Enter hello name of hello new SAML plugin and click hello **‘Add’** button.</span></span>

    ![플러그 인](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. <span data-ttu-id="38a01-178">다음과 같이 hello 세부 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-178">Enter hello details as follows:</span></span>

    ![플러그 인](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    <span data-ttu-id="38a01-180">a.</span><span class="sxs-lookup"><span data-stu-id="38a01-180">a.</span></span> <span data-ttu-id="38a01-181">Hello에 **이름** SAML 플러그 인의 형식 hello 이름 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-181">In hello **Name** textbox, type hello name of SAML plugin.</span></span>

    <span data-ttu-id="38a01-182">b.</span><span class="sxs-lookup"><span data-stu-id="38a01-182">b.</span></span> <span data-ttu-id="38a01-183">Hello에 **발급자 URL** 텍스트 붙여넣기 hello **SAML 엔터티 ID** hello에서 복사한 **sign on 구성** hello Azure 포털의 창.</span><span class="sxs-lookup"><span data-stu-id="38a01-183">In hello **Issuer URL** textbox, paste hello **SAML Entity ID** you copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

    <span data-ttu-id="38a01-184">c.</span><span class="sxs-lookup"><span data-stu-id="38a01-184">c.</span></span> <span data-ttu-id="38a01-185">Hello에 **공급자 메타 데이터 구성** hello Azure 포털에서 다운로드 한 메타 데이터 XML 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-185">In hello **Provider Metadata Config** upload hello Metadata XML file which you downloaded from Azure portal.</span></span>

    <span data-ttu-id="38a01-186">d.</span><span class="sxs-lookup"><span data-stu-id="38a01-186">d.</span></span> <span data-ttu-id="38a01-187">Hello를 사용 하 여 프로 비전 시간에만 있는 tooenable SAML을 선택할 수도 있습니다 **'자동 새 사용자를 만들고'** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-187">You can also choose tooenable SAML just in time provisioning by enabling hello **‘Auto create new users’** checkbox.</span></span> <span data-ttu-id="38a01-188">사용자 Velpic에 존재 하지 않는 경우이 플래그는 해제 되어 Azure의 hello 로그인 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-188">If a user doesn’t exist in Velpic and this flag is not enabled, hello login from Azure will fail.</span></span> <span data-ttu-id="38a01-189">Hello 플래그는 활성화 된 hello 사용자가 자동으로 하는 경우에 프로 비전 Velpic hello 시 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-189">If hello flag is enabled hello user will automatically be provisioned into Velpic at hello time of login.</span></span> 

    <span data-ttu-id="38a01-190">e.</span><span class="sxs-lookup"><span data-stu-id="38a01-190">e.</span></span> <span data-ttu-id="38a01-191">복사 hello **Single sign-on URL** Azure 포털에서 hello hello 텍스트 상자 및 붙여넣기 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-191">Copy hello **Single sign on URL** from hello text box and paste it in hello Azure portal.</span></span>
    
    <span data-ttu-id="38a01-192">f.</span><span class="sxs-lookup"><span data-stu-id="38a01-192">f.</span></span> <span data-ttu-id="38a01-193">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-193">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="38a01-194">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="38a01-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="38a01-195">이 섹션의 hello 목표 toocreate Britta Simon 라는 hello Azure 관리 포털에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-195">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="38a01-197">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="38a01-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="38a01-198">Hello에 **Azure 관리 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-198">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="38a01-200">너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-200">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="38a01-202">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="38a01-202">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="38a01-204">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="38a01-206">a.</span><span class="sxs-lookup"><span data-stu-id="38a01-206">a.</span></span> <span data-ttu-id="38a01-207">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="38a01-208">b.</span><span class="sxs-lookup"><span data-stu-id="38a01-208">b.</span></span> <span data-ttu-id="38a01-209">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="38a01-210">c.</span><span class="sxs-lookup"><span data-stu-id="38a01-210">c.</span></span> <span data-ttu-id="38a01-211">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="38a01-212">d.</span><span class="sxs-lookup"><span data-stu-id="38a01-212">d.</span></span> <span data-ttu-id="38a01-213">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-213">Click **Create**.</span></span>
 
### <a name="creating-a-velpic-saml-test-user"></a><span data-ttu-id="38a01-214">Velpic SAML 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="38a01-214">Creating a Velpic SAML test user</span></span>

<span data-ttu-id="38a01-215">이 단계는 일반적으로 하지 않습니다 필요한 hello 응용 프로그램은 적시 사용자 프로 비전만 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-215">This step is usually not required as hello application supports just in time user provisioning.</span></span> <span data-ttu-id="38a01-216">Hello 자동 사용자 프로비저닝을 사용 하지 않는 경우 다음 수동 사용자 만들기 가능 아래에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-216">If hello automatic user provisioning is not enabled then manual user creation can be done as described below.</span></span>

<span data-ttu-id="38a01-217">Velpic SAML 회사 사이트에 관리자 권한으로 로그인하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-217">Log into your Velpic SAML company site as an administrator and perform following steps:</span></span>
    
1. <span data-ttu-id="38a01-218">관리 탭 및 tooUsers 섹션 이동 클릭 한 다음 새 단추 tooadd 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-218">Click on Manage tab and go tooUsers section, then click on New button tooadd users.</span></span>

    ![사용자 추가](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. <span data-ttu-id="38a01-220">Hello에 **"새 사용자 만들기"** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-220">On hello **“Create New User”** dialog page, perform hello following steps.</span></span>

    ![사용자](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    <span data-ttu-id="38a01-222">a.</span><span class="sxs-lookup"><span data-stu-id="38a01-222">a.</span></span> <span data-ttu-id="38a01-223">Hello에 **이름** 형식 Britta Simon의 hello 이름 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-223">In hello **First Name** textbox, type hello first name of Britta Simon.</span></span>

    <span data-ttu-id="38a01-224">b.</span><span class="sxs-lookup"><span data-stu-id="38a01-224">b.</span></span> <span data-ttu-id="38a01-225">Hello에 **성** Britta Simon의 형식 hello 마지막 이름 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-225">In hello **Last Name** textbox, type hello last name of Britta Simon.</span></span>

    <span data-ttu-id="38a01-226">c.</span><span class="sxs-lookup"><span data-stu-id="38a01-226">c.</span></span> <span data-ttu-id="38a01-227">Hello에 **사용자 이름** textbox Britta Simon의 hello 사용자 이름 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-227">In hello **User Name** textbox, type hello user name of Britta Simon.</span></span>

    <span data-ttu-id="38a01-228">d.</span><span class="sxs-lookup"><span data-stu-id="38a01-228">d.</span></span> <span data-ttu-id="38a01-229">Hello에 **전자 메일** textbox Britta Simon 계정의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-229">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="38a01-230">e.</span><span class="sxs-lookup"><span data-stu-id="38a01-230">e.</span></span> <span data-ttu-id="38a01-231">나머지 hello 정보는 선택 사항이 고 필요한 경우를 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-231">Rest of hello information is optional, you can fill it if needed.</span></span>
    
    <span data-ttu-id="38a01-232">f.</span><span class="sxs-lookup"><span data-stu-id="38a01-232">f.</span></span> <span data-ttu-id="38a01-233">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-233">Click **SAVE**.</span></span>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="38a01-234">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="38a01-235">이 섹션에서는 그녀의 액세스 tooVelpic SAML을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooVelpic SAML.</span></span>

![사용자 할당][200] 

<span data-ttu-id="38a01-237">**tooassign Britta Simon tooVelpic SAML hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="38a01-237">**tooassign Britta Simon tooVelpic SAML, perform hello following steps:**</span></span>

1. <span data-ttu-id="38a01-238">Hello Azure 관리 포털에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-238">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="38a01-240">Hello 응용 프로그램 목록에서 선택 **Velpic SAML**합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-240">In hello applications list, select **Velpic SAML**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. <span data-ttu-id="38a01-242">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="38a01-244">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-244">Click **Add** button.</span></span> <span data-ttu-id="38a01-245">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="38a01-247">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="38a01-248">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="38a01-249">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="38a01-250">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="38a01-250">Testing single sign-on</span></span>

<span data-ttu-id="38a01-251">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-251">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="38a01-252">Hello Velpic SAML hello 액세스 패널에서에서 타일을 클릭할 때 Velpic SAML 응용 프로그램의 로그인 페이지를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-252">When you click hello Velpic SAML tile in hello Access Panel, you should get login page of Velpic SAML application.</span></span> <span data-ttu-id="38a01-253">Hello 표시 되어야 **'Azure AD 로그인'** hello 로그인 페이지에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-253">You should see hello **‘Log In With Azure AD’** button on hello sign in page.</span></span>

    ![플러그 인](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. <span data-ttu-id="38a01-255">Hello 클릭 **'Azure AD 로그인'** 에 Azure AD 계정을 사용 하 여 tooVelpic 단추 toolog 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a01-255">Click on hello **‘Log In With Azure AD’** button toolog in tooVelpic using your Azure AD account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="38a01-256">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="38a01-256">Additional resources</span></span>

* [<span data-ttu-id="38a01-257">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="38a01-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="38a01-258">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="38a01-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

