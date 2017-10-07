---
title: "자습서: Voyance와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Voyance 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: e2cb9eb6b20e8611a9f6e8529b7c85a8d86ec3e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a><span data-ttu-id="34c2f-103">자습서: Azure Active Directory와 Voyance 통합</span><span class="sxs-lookup"><span data-stu-id="34c2f-103">Tutorial: Azure Active Directory integration with Voyance</span></span>

<span data-ttu-id="34c2f-104">이 자습서에 설명 어떻게 toointegrate Voyance Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="34c2f-104">In this tutorial, you learn how toointegrate Voyance with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="34c2f-105">다음 이점을 hello로 제공 Voyance Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="34c2f-105">Integrating Voyance with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="34c2f-106">액세스 tooVoyance을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-106">You can control in Azure AD who has access tooVoyance</span></span>
- <span data-ttu-id="34c2f-107">프로그램 사용자 tooautomatically get 로그온 tooVoyance (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-107">You can enable your users tooautomatically get signed-on tooVoyance (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="34c2f-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="34c2f-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34c2f-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="34c2f-110">Prerequisites</span></span>

<span data-ttu-id="34c2f-111">다음 항목 hello가 필요 tooconfigure Voyance와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-111">tooconfigure Azure AD integration with Voyance, you need hello following items:</span></span>

- <span data-ttu-id="34c2f-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="34c2f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="34c2f-113">Voyance Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="34c2f-113">A Voyance single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="34c2f-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="34c2f-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="34c2f-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="34c2f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="34c2f-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="34c2f-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="34c2f-118">Scenario description</span></span>
<span data-ttu-id="34c2f-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="34c2f-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="34c2f-121">Voyance는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="34c2f-121">Adding Voyance from hello gallery</span></span>
2. <span data-ttu-id="34c2f-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="34c2f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-voyance-from-hello-gallery"></a><span data-ttu-id="34c2f-123">Voyance는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="34c2f-123">Adding Voyance from hello gallery</span></span>
<span data-ttu-id="34c2f-124">tooconfigure hello와의 통합 Voyance Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Voyance tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-124">tooconfigure hello integration of Voyance into Azure AD, you need tooadd Voyance from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="34c2f-125">**hello 갤러리에서 Voyance tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="34c2f-125">**tooadd Voyance from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="34c2f-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="34c2f-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="34c2f-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="34c2f-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="34c2f-133">Hello 검색 상자에 입력 **Voyance**선택, **Voyance** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-133">In hello search box, type **Voyance**, select  **Voyance**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Voyance hello 결과 목록에서](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="34c2f-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="34c2f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="34c2f-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Voyance에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-136">In this section, you configure and test Azure AD single sign-on with Voyance based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="34c2f-137">Single sign on toowork에 대 한 Azure AD는 tooknow Voyance에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Voyance is tooa user in Azure AD.</span></span> <span data-ttu-id="34c2f-138">즉, Azure AD 사용자 및 Voyance에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-138">In other words, a link relationship between an Azure AD user and hello related user in Voyance needs toobe established.</span></span>

<span data-ttu-id="34c2f-139">Voyance에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-139">In Voyance, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="34c2f-140">tooconfigure 및 Voyance 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-140">tooconfigure and test Azure AD single sign-on with Voyance, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="34c2f-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="34c2f-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="34c2f-143">**[Voyance 테스트 사용자 만들기](#create-a-voyance-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Voyance에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-143">**[Create a Voyance test user](#create-a-voyance-test-user)** - toohave a counterpart of Britta Simon in Voyance that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="34c2f-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="34c2f-145">**[Single Sign-on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="34c2f-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="34c2f-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="34c2f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="34c2f-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Voyance 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Voyance application.</span></span>

<span data-ttu-id="34c2f-148">**tooconfigure Azure AD single sign on, Voyance와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="34c2f-148">**tooconfigure Azure AD single sign-on with Voyance, perform hello following steps:**</span></span>

1. <span data-ttu-id="34c2f-149">Hello hello에 Azure 포털에서에서 **Voyance** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-149">In hello Azure portal, on hello **Voyance** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="34c2f-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_samlbase.png)

3. <span data-ttu-id="34c2f-153">Hello에 **Voyance 도메인 및 Url** 섹션를 hello tooconfigure hello 응용 프로그램에 필요한 경우 다음 단계를 수행 **IDP** 시작 모드:</span><span class="sxs-lookup"><span data-stu-id="34c2f-153">On hello **Voyance Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![IDP에 대한 Voyance 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url1.png)

    <span data-ttu-id="34c2f-155">a.</span><span class="sxs-lookup"><span data-stu-id="34c2f-155">a.</span></span> <span data-ttu-id="34c2f-156">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.nyansa.com`</span><span class="sxs-lookup"><span data-stu-id="34c2f-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com`</span></span>

    <span data-ttu-id="34c2f-157">b.</span><span class="sxs-lookup"><span data-stu-id="34c2f-157">b.</span></span> <span data-ttu-id="34c2f-158">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.nyansa.com/saml/create/`</span><span class="sxs-lookup"><span data-stu-id="34c2f-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com/saml/create/`</span></span>

4. <span data-ttu-id="34c2f-159">확인 **고급 URL 설정 표시** hello tooconfigure hello 응용 프로그램에 필요한 경우 단계를 다음을 수행 하 고 **SP** 시작 모드:</span><span class="sxs-lookup"><span data-stu-id="34c2f-159">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![SP에 대한 Voyance 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url2.png)

    <span data-ttu-id="34c2f-161">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.nyansa.com/`</span><span class="sxs-lookup"><span data-stu-id="34c2f-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="34c2f-162">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-162">These values are not real.</span></span> <span data-ttu-id="34c2f-163">이러한 항목을 업데이트 식별자, 회신 URL 및 로그온 URL 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="34c2f-164">연락처 [Voyance 클라이언트 지원 팀](mailto:support@nyansa.com) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-164">Contact [Voyance Client support team](mailto:support@nyansa.com) tooget these values.</span></span> 

5. <span data-ttu-id="34c2f-165">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_certificate.png) 

6. <span data-ttu-id="34c2f-167">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-167">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-voyance-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="34c2f-169">Hello에 **Voyance 구성** 섹션에서 클릭 **구성 Voyance** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="34c2f-169">On hello **Voyance Configuration** section, click **Configure Voyance** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="34c2f-170">복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="34c2f-170">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Voyance 구성](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_configure.png) 

8. <span data-ttu-id="34c2f-172">다른 웹 브라우저 창에서 관리자 권한으로 로그온 tooyour Voyance 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-172">In a different web browser window, sign-on tooyour Voyance tenant as an administrator.</span></span>

9. <span data-ttu-id="34c2f-173">Toohello의 오른쪽 위 모서리 hello 탐색 모음을 이동 하 고 알리는 hello 드롭다운 목록에서 클릭 "**Acme 대학**"입니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-173">Go toohello top right corner of hello navigation bar and click on hello drop-down that says "**Acme University**".</span></span>
    
    ![앱 쪽에서 Single Sign-On 구성 Acme University](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

10. <span data-ttu-id="34c2f-175">"**관리 설정**"을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-175">Click "**Admin Settings**".</span></span>

    ![앱 쪽에서 Single Sign-On 구성 관리 설정](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

11. <span data-ttu-id="34c2f-177">"**사용자 액세스**" 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-177">Click "**User Access**" tab.</span></span>

    ![앱 쪽에서 Single Sign-On 구성 사용자 액세스](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

12. <span data-ttu-id="34c2f-179">Hello 클릭 "**SSO 사용 되지 않는지**" 단추 tooconfigure Azure AD SAML 2.0을 사용 하는 IdP로 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-179">Click hello "**SSO is disabled**" button tooconfigure Azure AD as an IdP using SAML 2.0.</span></span>

    ![앱 쪽에서 Single Sign-On 구성 SSO가 비활성화됨 단추](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

13. <span data-ttu-id="34c2f-181">너무 이동**SAML v2** 섹션 및 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-181">Go too**SAML v2** section and perform below steps:</span></span>

    ![앱 쪽에서 Single Sign-On 구성 SAML v2](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
    
    <span data-ttu-id="34c2f-183">a.</span><span class="sxs-lookup"><span data-stu-id="34c2f-183">a.</span></span> <span data-ttu-id="34c2f-184">**사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-184">Select **Enabled**.</span></span>
    
    <span data-ttu-id="34c2f-185">b.</span><span class="sxs-lookup"><span data-stu-id="34c2f-185">b.</span></span> <span data-ttu-id="34c2f-186">붙여넣기 **SAML Single Sign-on 서비스 URL**, hello에 hello Azure 포털에서에서 복사한 있는 **IdP 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-186">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal Into hello **IdP Login URL** textbox.</span></span>

    <span data-ttu-id="34c2f-187">c.</span><span class="sxs-lookup"><span data-stu-id="34c2f-187">c.</span></span> <span data-ttu-id="34c2f-188">콘텐츠를 클립보드에 복사 hello 메모장에서 다운로드 한 Base64 인코딩 인증서를 열고 toohello 붙여 **IdP 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-188">Open your downloaded Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Cert** textbox.</span></span>
    
    <span data-ttu-id="34c2f-189">d.</span><span class="sxs-lookup"><span data-stu-id="34c2f-189">d.</span></span> <span data-ttu-id="34c2f-190">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="34c2f-191">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="34c2f-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="34c2f-192">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="34c2f-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="34c2f-193">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="34c2f-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="34c2f-194">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="34c2f-194">Create an Azure AD test user</span></span>

<span data-ttu-id="34c2f-195">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="34c2f-197">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="34c2f-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="34c2f-198">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-voyance-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="34c2f-200">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-voyance-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="34c2f-202">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![hello 추가 단추](./media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="34c2f-204">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![hello 사용자 대화 상자](./media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="34c2f-206">a.</span><span class="sxs-lookup"><span data-stu-id="34c2f-206">a.</span></span> <span data-ttu-id="34c2f-207">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="34c2f-208">b.</span><span class="sxs-lookup"><span data-stu-id="34c2f-208">b.</span></span> <span data-ttu-id="34c2f-209">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="34c2f-210">c.</span><span class="sxs-lookup"><span data-stu-id="34c2f-210">c.</span></span> <span data-ttu-id="34c2f-211">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="34c2f-212">d.</span><span class="sxs-lookup"><span data-stu-id="34c2f-212">d.</span></span> <span data-ttu-id="34c2f-213">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-213">Click **Create**.</span></span>
 
### <a name="create-a-voyance-test-user"></a><span data-ttu-id="34c2f-214">Voyance 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="34c2f-214">Create a Voyance test user</span></span>

<span data-ttu-id="34c2f-215">hello이이 섹션의 목적은 toocreate Britta Simon Voyance에서 호출 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-215">hello objective of this section is toocreate a user called Britta Simon in Voyance.</span></span> <span data-ttu-id="34c2f-216">Voyance는 적시에 프로비전을 지원하며 기본적으로 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-216">Voyance supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="34c2f-217">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-217">There is no action item for you in this section.</span></span> <span data-ttu-id="34c2f-218">새 사용자는 아직 존재 하지 않는 경우 시도 tooaccess Voyance 중 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-218">A new user is created during an attempt tooaccess Voyance if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="34c2f-219">Toocontact toocreate 사용자를 수동으로 필요한 경우 필요한 [Voyance 지원 팀](maiLto:support@nyansa.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-219">If you need toocreate a user manually, you need toocontact [Voyance support team](maiLto:support@nyansa.com).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="34c2f-220">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-220">Assign hello Azure AD test user</span></span>

<span data-ttu-id="34c2f-221">이 섹션에서는 tooVoyance 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooVoyance.</span></span>

![Hello 사용자 역할 할당][200]

<span data-ttu-id="34c2f-223">**tooassign Britta Simon tooVoyance hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="34c2f-223">**tooassign Britta Simon tooVoyance, perform hello following steps:**</span></span>

1. <span data-ttu-id="34c2f-224">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="34c2f-226">Hello 응용 프로그램 목록에서 선택 **Voyance**합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-226">In hello applications list, select **Voyance**.</span></span>

    ![hello 응용 프로그램 목록에서 hello Voyance 링크](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_app.png) 

3. <span data-ttu-id="34c2f-228">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="34c2f-230">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-230">Click **Add** button.</span></span> <span data-ttu-id="34c2f-231">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="34c2f-233">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="34c2f-234">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="34c2f-235">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="34c2f-236">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="34c2f-236">Test single sign-on</span></span>

<span data-ttu-id="34c2f-237">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="34c2f-238">Hello 액세스 패널에서에서 hello Voyance 타일을 클릭할 때 자동으로 로그온 tooyour Voyance 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c2f-238">When you click hello Voyance tile in hello Access Panel, you should get automatically signed-on tooyour Voyance application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="34c2f-239">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="34c2f-239">Additional resources</span></span>

* [<span data-ttu-id="34c2f-240">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="34c2f-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="34c2f-241">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="34c2f-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_203.png

