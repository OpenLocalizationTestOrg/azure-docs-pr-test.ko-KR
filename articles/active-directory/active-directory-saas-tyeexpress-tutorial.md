---
title: "자습서: T&E Express와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory 및 T E Express 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 9a568ace8dbc75fadbf37554996b1b597a813d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a><span data-ttu-id="64804-103">자습서: T&E Express와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="64804-103">Tutorial: Azure Active Directory integration with T&E Express</span></span>

<span data-ttu-id="64804-104">이 자습서에 설명 어떻게 toointegrate & Azure Active Directory (Azure AD)와 E Express입니다.</span><span class="sxs-lookup"><span data-stu-id="64804-104">In this tutorial, you learn how toointegrate T&E Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="64804-105">& 전자 Express Azure AD와 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-105">Integrating T&E Express with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="64804-106">Azure AD 액세스 tooT 가진 및 E Express에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64804-106">You can control in Azure AD who has access tooT&E Express</span></span>
- <span data-ttu-id="64804-107">Azure AD 계정을와 tooT 로그온 사용자 tooautomatically get 및 E Express (Single Sign-on)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64804-107">You can enable your users tooautomatically get signed-on tooT&E Express (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="64804-108">하나의 중앙 위치-hello Azure 관리 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64804-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="64804-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64804-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="64804-110">Prerequisites</span></span>

<span data-ttu-id="64804-111">t& E Express와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-111">tooconfigure Azure AD integration with T&E Express, you need hello following items:</span></span>

- <span data-ttu-id="64804-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="64804-112">An Azure AD subscription</span></span>
- <span data-ttu-id="64804-113">T&E Express Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="64804-113">A T&E Express single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="64804-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="64804-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="64804-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="64804-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64804-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="64804-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="64804-118">Scenario description</span></span>
<span data-ttu-id="64804-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="64804-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64804-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="64804-121">& 전자 Express hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="64804-121">Adding T&E Express from hello gallery</span></span>
2. <span data-ttu-id="64804-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="64804-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-te-express-from-hello-gallery"></a><span data-ttu-id="64804-123">& 전자 Express hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="64804-123">Adding T&E Express from hello gallery</span></span>
<span data-ttu-id="64804-124">tooconfigure hello와의 통합 & 전자 Express Azure AD로 관리 되는 SaaS 앱 목록이 갤러리 tooyour hello에서 tooadd T 및 E Express 필요한 합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-124">tooconfigure hello integration of T&E Express into Azure AD, you need tooadd T&E Express from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="64804-125">**tooadd T & hello 갤러리, 전자 Express hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="64804-125">**tooadd T&E Express from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="64804-126">Hello에  **[Azure 관리 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="64804-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="64804-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="64804-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="64804-131">클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="64804-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="64804-133">Hello 검색 상자에 입력 **t& E Express**합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-133">In hello search box, type **T&E Express**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. <span data-ttu-id="64804-135">Hello 결과 패널에서 선택 **t& E Express**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="64804-135">In hello results panel, select **T&E Express**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="64804-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="64804-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="64804-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 T&E Express에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-138">In this section, you configure and test Azure AD single sign-on with T&E Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="64804-139">Single sign on toowork에 대 한 Azure AD는 tooknow t& E Express에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in T&E Express is tooa user in Azure AD.</span></span> <span data-ttu-id="64804-140">즉, Azure AD 사용자 및 설정 t& E Express 요구 toobe에 hello 관련된 사용자 간 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="64804-140">In other words, a link relationship between an Azure AD user and hello related user in T&E Express needs toobe established.</span></span>

<span data-ttu-id="64804-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **사용자 이름** t& E Express에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in T&E Express.</span></span>

<span data-ttu-id="64804-142">tooconfigure 및 t& E Express를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-142">tooconfigure and test Azure AD single sign-on with T&E Express, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="64804-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="64804-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="64804-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="64804-145">**[T& E Express 테스트 사용자 만들기](#creating-a-te-express-test-user)**  -toohave Britta Simon & 표현인 연결 된 Azure AD toohello 그녀는 E Express에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="64804-145">**[Creating a T&E Express test user](#creating-a-te-express-test-user)** - toohave a counterpart of Britta Simon in T&E Express that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="64804-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="64804-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="64804-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="64804-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="64804-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="64804-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="64804-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 관리 포털에서 사용 하도록 설정 및 t& E Express 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your T&E Express application.</span></span>

<span data-ttu-id="64804-150">**T 및 E Express, Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="64804-150">**tooconfigure Azure AD single sign-on with T&E Express, perform hello following steps:**</span></span>

1. <span data-ttu-id="64804-151">Hello에 hello Azure 관리 포털에서 **t& E Express** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-151">In hello Azure Management portal, on hello **T&E Express** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="64804-153">Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="64804-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. <span data-ttu-id="64804-155">Hello에 **T 및 E Express 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-155">On hello **T&E Express Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    <span data-ttu-id="64804-157">a.</span><span class="sxs-lookup"><span data-stu-id="64804-157">a.</span></span> <span data-ttu-id="64804-158">Hello에 **식별자** 형식 hello 값으로 텍스트 상자:`https://<domain>.tyeexpress.com`</span><span class="sxs-lookup"><span data-stu-id="64804-158">In hello **Identifier** textbox, type hello value as: `https://<domain>.tyeexpress.com`</span></span>

    <span data-ttu-id="64804-159">b.</span><span class="sxs-lookup"><span data-stu-id="64804-159">b.</span></span> <span data-ttu-id="64804-160">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span><span class="sxs-lookup"><span data-stu-id="64804-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="64804-161">이러한 없는지 hello 실제 값 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="64804-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="64804-162">Tooupdate hello 실제 식별자와 회신 URL 사용 하 여 이러한 값 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="64804-163">여기 있습니다 toouse hello의 고유 값을 hello 식별자의에서 문자열을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="64804-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="64804-164">연락처 [& Express E 지원 팀](http://www.tyeexpress.com/contacto.aspx) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="64804-164">Contact [T&E Express support team](http://www.tyeexpress.com/contacto.aspx) tooget these values.</span></span>

5. <span data-ttu-id="64804-165">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello XML 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. <span data-ttu-id="64804-167">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-167">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="64804-169">tooconfigure single sign on에서 **t& E Express** 쪽, 로그인 toohello T 및 SAML 없이 E 빠른 응용 프로그램에 대 한 single sign-on이 관리자 자격 증명을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-169">tooconfigure single sign-on on **T&E Express** side, login toohello T&E express application without SAML single sign on using admin credentials.</span></span>

9. <span data-ttu-id="64804-170">Hello에서 **Admin** 탭을 클릭 **SAML 도메인** tooOpen hello SAML 설정 페이지.</span><span class="sxs-lookup"><span data-stu-id="64804-170">Under hello **Admin** Tab, Click on **SAML domain** tooOpen hello SAML settings page.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tyeexpress-tutorial/tye-SAML.png)

10. <span data-ttu-id="64804-172">선택 hello **Activar(Activate)** 옵션에서 **아니요** 너무**SI(Yes)**합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-172">Select hello **Activar(Activate)** option from **No** too**SI(Yes)**.</span></span> <span data-ttu-id="64804-173">Hello에 **Id 공급자 메타 데이터** 텍스트 붙여넣기 hello 메타 데이터 XML이 있는 Azure 포털에서 donwloaded 합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-173">In hello **Identity Provider Metadata** textbox, paste hello metadata XML which you have donwloaded from Azure portal.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tyeexpress-tutorial/tyeAdmin.png)

11. <span data-ttu-id="64804-175">Hello 클릭 **Guardar(Save)** 단추 toosave hello 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-175">Click on hello **Guardar(Save)** button toosave hello settings.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="64804-176">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="64804-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="64804-177">이 섹션의 hello 목표 toocreate Britta Simon 라는 hello Azure 관리 포털에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="64804-177">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="64804-179">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="64804-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="64804-180">Hello에 **Azure 관리 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="64804-180">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="64804-182">너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="64804-182">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="64804-184">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="64804-184">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="64804-186">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="64804-188">a.</span><span class="sxs-lookup"><span data-stu-id="64804-188">a.</span></span> <span data-ttu-id="64804-189">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="64804-190">b.</span><span class="sxs-lookup"><span data-stu-id="64804-190">b.</span></span> <span data-ttu-id="64804-191">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="64804-192">c.</span><span class="sxs-lookup"><span data-stu-id="64804-192">c.</span></span> <span data-ttu-id="64804-193">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="64804-194">d.</span><span class="sxs-lookup"><span data-stu-id="64804-194">d.</span></span> <span data-ttu-id="64804-195">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-195">Click **Create**.</span></span>
 
### <a name="creating-a-te-express-test-user"></a><span data-ttu-id="64804-196">T&E Express 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="64804-196">Creating a T&E Express test user</span></span>

<span data-ttu-id="64804-197">Tooenable Azure AD 사용자가 toolog E Express T로 주문 하 고에 t& E Express에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-197">In order tooenable Azure AD users toolog into T&E Express, they must be provisioned into T&E Express.</span></span>  
<span data-ttu-id="64804-198">T&E Express의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="64804-198">In case of T&E Express, provisioning is a manual task.</span></span>

<span data-ttu-id="64804-199">**사용자 계정 수행 tooprovision hello 다음 단계:**</span><span class="sxs-lookup"><span data-stu-id="64804-199">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="64804-200">관리자 권한으로 tooyour T 및 E Express 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-200">Log in tooyour T&E Express company site as an administrator.</span></span>

2. <span data-ttu-id="64804-201">Admin 태그 아래 사용자 tooopen hello 사용자가 마스터 페이지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-201">Under Admin tag, click on Users tooopen hello Users master page.</span></span>

    ![직원 추가](./media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. <span data-ttu-id="64804-203">Hello 홈 페이지에서 클릭  **+**  tooadd hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="64804-203">On hello home page, click on **+** tooadd hello users.</span></span>

    ![직원 추가](./media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. <span data-ttu-id="64804-205">Hello 형태로 요청 하는 대로 모든 hello 필수 세부 정보를 입력 하 고 hello 단추 toosave hello 세부 정보 저장을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-205">Enter all hello mandatory details as asked in hello form and click hello save button toosave hello details.</span></span>

    ![직원 추가](./media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![직원 추가](./media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="64804-208">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="64804-209">이 섹션에서는 그녀의 액세스 tooT 및 E Express 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooT&E Express.</span></span>

![사용자 할당][200] 

<span data-ttu-id="64804-211">**tooassign Britta Simon tooT 및 E Express hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="64804-211">**tooassign Britta Simon tooT&E Express, perform hello following steps:**</span></span>

1. <span data-ttu-id="64804-212">Hello Azure 관리 포털에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-212">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="64804-214">Hello 응용 프로그램 목록에서 선택 **t& E Express**합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-214">In hello applications list, select **T&E Express**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. <span data-ttu-id="64804-216">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="64804-218">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-218">Click **Add** button.</span></span> <span data-ttu-id="64804-219">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="64804-221">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64804-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="64804-222">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="64804-223">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64804-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="64804-224">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="64804-224">Testing single sign-on</span></span>

<span data-ttu-id="64804-225">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64804-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="64804-226">간단한 T & hello 액세스 패널에서에서 E Express 타일을 클릭할 때 자동으로 로그온 tooyour T 및 E Express 응용 프로그램을 구하십시오.</span><span class="sxs-lookup"><span data-stu-id="64804-226">When you click hello T&E Express tile in hello Access Panel, you should get automatically signed-on tooyour T&E Express application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="64804-227">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="64804-227">Additional resources</span></span>

* [<span data-ttu-id="64804-228">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="64804-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="64804-229">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="64804-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png

