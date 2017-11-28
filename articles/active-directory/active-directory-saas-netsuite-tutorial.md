---
title: "자습서: Netsuite와 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Netsuite 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7cf205d5bda5333872fb589e57f4779a8670b595
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a><span data-ttu-id="2397e-103">자습서: Netsuite와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="2397e-103">Tutorial: Azure Active Directory integration with Netsuite</span></span>

<span data-ttu-id="2397e-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 Netsuite 합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-104">In this tutorial, you learn how toointegrate Netsuite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2397e-105">Azure AD와 Netsuite 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-105">Integrating Netsuite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2397e-106">액세스 tooNetsuite을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-106">You can control in Azure AD who has access tooNetsuite</span></span>
- <span data-ttu-id="2397e-107">프로그램 사용자 tooautomatically get 로그온 tooNetsuite (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-107">You can enable your users tooautomatically get signed-on tooNetsuite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2397e-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2397e-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2397e-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2397e-110">Prerequisites</span></span>

<span data-ttu-id="2397e-111">Netsuite와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-111">tooconfigure Azure AD integration with Netsuite, you need hello following items:</span></span>

- <span data-ttu-id="2397e-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="2397e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2397e-113">Netsuite Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="2397e-113">A Netsuite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2397e-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2397e-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2397e-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="2397e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2397e-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2397e-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="2397e-118">Scenario description</span></span>
<span data-ttu-id="2397e-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2397e-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2397e-121">Netsuite는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="2397e-121">Adding Netsuite from hello gallery</span></span>
2. <span data-ttu-id="2397e-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2397e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netsuite-from-hello-gallery"></a><span data-ttu-id="2397e-123">Netsuite는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="2397e-123">Adding Netsuite from hello gallery</span></span>
<span data-ttu-id="2397e-124">tooconfigure hello와의 통합 Netsuite Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Netsuite tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-124">tooconfigure hello integration of Netsuite into Azure AD, you need tooadd Netsuite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2397e-125">**hello 갤러리에서 Netsuite tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2397e-125">**tooadd Netsuite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2397e-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2397e-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2397e-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="2397e-131">클릭 **새 응용 프로그램** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="2397e-133">Hello 검색 상자에 입력 **Netsuite**합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-133">In hello search box, type **Netsuite**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. <span data-ttu-id="2397e-135">Hello 결과 패널에서 선택 **Netsuite**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-135">In hello results panel, select **Netsuite**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2397e-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2397e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2397e-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 Netsuite에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-138">In this section, you configure and test Azure AD single sign-on with Netsuite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2397e-139">Single sign on toowork에 대 한 Azure AD는 tooknow에 Azure AD에서 Netsuite에 어떤 hello 테이블에 해당 사용자가 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Netsuite is tooa user in Azure AD.</span></span> <span data-ttu-id="2397e-140">즉, Azure AD 사용자와 Netsuite에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-140">In other words, a link relationship between an Azure AD user and hello related user in Netsuite needs toobe established.</span></span>

<span data-ttu-id="2397e-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Netsuite에 합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Netsuite.</span></span>

<span data-ttu-id="2397e-142">tooconfigure와 Netsuite 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-142">tooconfigure and test Azure AD single sign-on with Netsuite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2397e-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2397e-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2397e-145">**[Netsuite 테스트 사용자 만들기](#creating-a-netsuite-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Netsuite에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-145">**[Creating a Netsuite test user](#creating-a-netsuite-test-user)** - toohave a counterpart of Britta Simon in Netsuite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2397e-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2397e-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="2397e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2397e-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="2397e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2397e-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Netsuite 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Netsuite application.</span></span>

<span data-ttu-id="2397e-150">**Azure AD tooconfigure single sign on와 Netsuite를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2397e-150">**tooconfigure Azure AD single sign-on with Netsuite, perform hello following steps:**</span></span>

1. <span data-ttu-id="2397e-151">Hello hello에 Azure 포털에서에서 **Netsuite** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-151">In hello Azure portal, on hello **Netsuite** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="2397e-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. <span data-ttu-id="2397e-155">Hello에 **Netsuite 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-155">On hello **Netsuite Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    <span data-ttu-id="2397e-157">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs``https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span><span class="sxs-lookup"><span data-stu-id="2397e-157">In hello **Reply URL** textbox, type a URL using hello following pattern:   `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2397e-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-158">This value is not real value.</span></span> <span data-ttu-id="2397e-159">업데이트 hello 값과 실제 회신 URL hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-159">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="2397e-160">연락처 [Netsuite 지원 팀](http://www.netsuite.com/portal/services/support.shtml) tooget이이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-160">Contact [Netsuite support team](http://www.netsuite.com/portal/services/support.shtml) tooget this value.</span></span>
 
4. <span data-ttu-id="2397e-161">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello XML 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. <span data-ttu-id="2397e-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2397e-165">Hello에 **Netsuite 구성** 섹션에서 클릭 **구성 Netsuite** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="2397e-165">On hello **Netsuite Configuration** section, click **Configure Netsuite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2397e-166">복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="2397e-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. <span data-ttu-id="2397e-168">브라우저에서 새 탭을 열고 관리자 권한으로 Netsuite 회사 사이트에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-168">Open a new tab in your browser, and sign into your Netsuite company site as an administrator.</span></span>

8. <span data-ttu-id="2397e-169">도구 모음의 hello hello hello 페이지 위쪽에 클릭 **설치**, 클릭 **설치 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-169">In hello toolbar at hello top of hello page, click **Setup**, then click **Setup Manager**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. <span data-ttu-id="2397e-171">Hello에서 **설정 작업** 목록에서 **통합**합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-171">From hello **Setup Tasks** list, select **Integration**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. <span data-ttu-id="2397e-173">Hello에 **인증 관리** 섹션에서 클릭 **SAML Single Sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-173">In hello **Manage Authentication** section, click **SAML Single Sign-on**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. <span data-ttu-id="2397e-175">Hello에 **SAML 설정** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-175">On hello **SAML Setup** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="2397e-176">a.</span><span class="sxs-lookup"><span data-stu-id="2397e-176">a.</span></span> <span data-ttu-id="2397e-177">복사 hello **SAML Single Sign-on 서비스 URL** 에서 값 **빠른 참조** 섹션 **sign on 구성** hello에 붙여 넣습니다 **Id 공급자 로그인 페이지** 필드 Netsuite에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-177">Copy hello **SAML Single Sign-On Service URL** value from **Quick Reference** section of **Configure sign-on** and paste it into hello **Identity Provider Login Page** field in Netsuite.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    <span data-ttu-id="2397e-179">b.</span><span class="sxs-lookup"><span data-stu-id="2397e-179">b.</span></span> <span data-ttu-id="2397e-180">[Netsuite 설치]에서 **기본 인증 방법**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-180">In Netsuite, select **Primary Authentication Method**.</span></span>

    <span data-ttu-id="2397e-181">c.</span><span class="sxs-lookup"><span data-stu-id="2397e-181">c.</span></span> <span data-ttu-id="2397e-182">레이블이 지정 된 hello 필드에 대 한 **SAMLV2 Id 공급자 메타 데이터**선택, **IDP 메타 데이터 파일 업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-182">For hello field labeled **SAMLV2 Identity Provider Metadata**, select **Upload IDP Metadata File**.</span></span> <span data-ttu-id="2397e-183">클릭 **찾아보기** tooupload hello 메타 데이터 파일을 Azure 포털에서 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-183">Then click **Browse** tooupload hello metadata file that you downloaded from Azure portal.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    <span data-ttu-id="2397e-185">d.</span><span class="sxs-lookup"><span data-stu-id="2397e-185">d.</span></span> <span data-ttu-id="2397e-186">**제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-186">Click **Submit**.</span></span>

12. <span data-ttu-id="2397e-187">Azure AD에서 **기타 모든 사용자 특성 보기 및 편집** 확인란을 클릭하고 특성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-187">In Azure AD, Click on **View and edit all other user attributes** check-box and add attribute.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. <span data-ttu-id="2397e-189">Hello에 대 한 **특성 이름** 필드에 입력을 `account`합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-189">For hello **Attribute Name** field, type in `account`.</span></span> <span data-ttu-id="2397e-190">Hello에 대 한 **특성 값** 필드 Netsuite 계정 ID에 입력 합니다 이 값은 상수 및 계정 변경</span><span class="sxs-lookup"><span data-stu-id="2397e-190">For hello **Attribute Value** field, type in your Netsuite account ID.This value is constant and change with account.</span></span> <span data-ttu-id="2397e-191">방법은 toofind 계정 ID 아래에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-191">Instructions on how toofind your account ID are included below:</span></span>

      ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    <span data-ttu-id="2397e-193">a.</span><span class="sxs-lookup"><span data-stu-id="2397e-193">a.</span></span> <span data-ttu-id="2397e-194">Netsuite, 클릭 **설치** hello 위쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-194">In Netsuite, click **Setup** from hello top navigation menu.</span></span>

    <span data-ttu-id="2397e-195">b.</span><span class="sxs-lookup"><span data-stu-id="2397e-195">b.</span></span> <span data-ttu-id="2397e-196">Hello 아래를 클릭 한 다음 **설정 작업** hello 왼쪽된 탐색 메뉴에서 선택 hello의 섹션 **통합** 섹션을 클릭 하 여 **웹 서비스 기본**합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-196">Then click under hello **Setup Tasks** section of hello left navigation menu, select hello **Integration** section, and click **Web Services Preferences**.</span></span>

    <span data-ttu-id="2397e-197">c.</span><span class="sxs-lookup"><span data-stu-id="2397e-197">c.</span></span> <span data-ttu-id="2397e-198">Netsuite 계정 ID를 복사 하 고 hello에 붙여 **특성 값** Azure AD의 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-198">Copy your Netsuite Account ID and paste it into hello **Attribute Value** field in Azure AD.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. <span data-ttu-id="2397e-200">사용자는 single sign-on Netsuite로 수행할 수 있습니다, 전에 먼저 할당 해야 Netsuite에서 적절 한 권한은 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-200">Before users can perform single sign-on into Netsuite, they must first be assigned hello appropriate permissions in Netsuite.</span></span> <span data-ttu-id="2397e-201">이러한 사용 권한을 tooassign 아래 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-201">Follow hello instructions below tooassign these permissions.</span></span>

    <span data-ttu-id="2397e-202">a.</span><span class="sxs-lookup"><span data-stu-id="2397e-202">a.</span></span> <span data-ttu-id="2397e-203">Hello 위쪽 탐색 메뉴를 클릭 **설치**, 클릭 **설치 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-203">On hello top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
      ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="2397e-205">b.</span><span class="sxs-lookup"><span data-stu-id="2397e-205">b.</span></span> <span data-ttu-id="2397e-206">Hello 왼쪽된 탐색 메뉴에서 선택 **사용자/역할**, 클릭 **역할 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-206">On hello left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span></span>
      
      ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    <span data-ttu-id="2397e-208">c.</span><span class="sxs-lookup"><span data-stu-id="2397e-208">c.</span></span> <span data-ttu-id="2397e-209">**새 역할**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-209">Click **New Role**.</span></span>

    <span data-ttu-id="2397e-210">d.</span><span class="sxs-lookup"><span data-stu-id="2397e-210">d.</span></span> <span data-ttu-id="2397e-211">에 입력 한 **이름** 새 역할 및 선택 hello에 대 한 **Single Sign-on만** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-211">Type in a **Name** for your new role, and select hello **Single Sign-On Only** checkbox.</span></span>
      
      ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    <span data-ttu-id="2397e-213">e.</span><span class="sxs-lookup"><span data-stu-id="2397e-213">e.</span></span> <span data-ttu-id="2397e-214">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-214">Click **Save**.</span></span>

    <span data-ttu-id="2397e-215">f.</span><span class="sxs-lookup"><span data-stu-id="2397e-215">f.</span></span> <span data-ttu-id="2397e-216">Hello 메뉴에서 hello 위에 표시를 클릭 **권한을**합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-216">In hello menu on hello top, click **Permissions**.</span></span> <span data-ttu-id="2397e-217">**설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-217">Then click **Setup**.</span></span>
      
       ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    <span data-ttu-id="2397e-219">g.</span><span class="sxs-lookup"><span data-stu-id="2397e-219">g.</span></span> <span data-ttu-id="2397e-220">**SAM Single Sign-On 설치**를 선택한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-220">Select **Set Up SAM Single Sign-on**, and then click **Add**.</span></span>

    <span data-ttu-id="2397e-221">h.</span><span class="sxs-lookup"><span data-stu-id="2397e-221">h.</span></span> <span data-ttu-id="2397e-222">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-222">Click **Save**.</span></span>

    <span data-ttu-id="2397e-223">i.</span><span class="sxs-lookup"><span data-stu-id="2397e-223">i.</span></span> <span data-ttu-id="2397e-224">Hello 위쪽 탐색 메뉴를 클릭 **설치**, 클릭 **설치 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-224">On hello top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
       ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="2397e-226">j.</span><span class="sxs-lookup"><span data-stu-id="2397e-226">j.</span></span> <span data-ttu-id="2397e-227">Hello 왼쪽된 탐색 메뉴에서 선택 **사용자/역할**, 클릭 **사용자 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-227">On hello left navigation menu, select **Users/Roles**, then click **Manage Users**.</span></span>
      
       ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    <span data-ttu-id="2397e-229">k.</span><span class="sxs-lookup"><span data-stu-id="2397e-229">k.</span></span> <span data-ttu-id="2397e-230">테스트 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-230">Select a test user.</span></span> <span data-ttu-id="2397e-231">**편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-231">Then click **Edit**.</span></span>
      
       ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    <span data-ttu-id="2397e-233">l.</span><span class="sxs-lookup"><span data-stu-id="2397e-233">l.</span></span> <span data-ttu-id="2397e-234">Hello 역할 대화 상자에서 만든 하 고를 클릭 하는 hello 역할 선택 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-234">On hello Roles dialog, select hello role that you have created and click **Add**.</span></span>
      
       ![Single Sign-on 구성](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    <span data-ttu-id="2397e-236">m.</span><span class="sxs-lookup"><span data-stu-id="2397e-236">m.</span></span> <span data-ttu-id="2397e-237">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-237">Click **Save**.</span></span>
    
> [!TIP]
> <span data-ttu-id="2397e-238">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="2397e-238">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2397e-239">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="2397e-239">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2397e-240">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2397e-240">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2397e-241">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2397e-241">Creating an Azure AD test user</span></span>
<span data-ttu-id="2397e-242">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-242">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="2397e-244">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2397e-244">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2397e-245">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-245">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="2397e-247">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-247">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2397e-249">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="2397e-249">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2397e-251">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-251">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2397e-253">a.</span><span class="sxs-lookup"><span data-stu-id="2397e-253">a.</span></span> <span data-ttu-id="2397e-254">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-254">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2397e-255">b.</span><span class="sxs-lookup"><span data-stu-id="2397e-255">b.</span></span> <span data-ttu-id="2397e-256">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-256">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2397e-257">c.</span><span class="sxs-lookup"><span data-stu-id="2397e-257">c.</span></span> <span data-ttu-id="2397e-258">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-258">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2397e-259">d.</span><span class="sxs-lookup"><span data-stu-id="2397e-259">d.</span></span> <span data-ttu-id="2397e-260">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-260">Click **Create**.</span></span> 

### <a name="creating-a-netsuite-test-user"></a><span data-ttu-id="2397e-261">Netsuite 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2397e-261">Creating a Netsuite test user</span></span>

<span data-ttu-id="2397e-262">이 섹션에서는 Netsuite에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-262">In this section, a user called Britta Simon is created in Netsuite.</span></span> <span data-ttu-id="2397e-263">Netsuite는 Just-In-Time 프로비전을 지원하며, 이 프로비전은 기본적으로 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-263">Netsuite supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="2397e-264">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-264">There is no action item for you in this section.</span></span> <span data-ttu-id="2397e-265">사용자는 Netsuite에 존재 하지 않는, 경우에 새 tooaccess Netsuite를 시도할 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-265">If a user doesn't already exist in Netsuite, a new one is created when you attempt tooaccess Netsuite.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2397e-266">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-266">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2397e-267">이 섹션에서는 tooNetsuite 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-267">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNetsuite.</span></span>

![사용자 할당][200] 

<span data-ttu-id="2397e-269">**tooassign Britta Simon tooNetsuite hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2397e-269">**tooassign Britta Simon tooNetsuite, perform hello following steps:**</span></span>

1. <span data-ttu-id="2397e-270">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-270">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="2397e-272">Hello 응용 프로그램 목록에서 선택 **Netsuite**합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-272">In hello applications list, select **Netsuite**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. <span data-ttu-id="2397e-274">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-274">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="2397e-276">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-276">Click **Add** button.</span></span> <span data-ttu-id="2397e-277">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="2397e-279">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-279">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2397e-280">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2397e-281">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2397e-282">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="2397e-282">Testing single sign-on</span></span>

<span data-ttu-id="2397e-283">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-283">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2397e-284">tootest single sign on 설정에 열기 hello 액세스 패널에 [https://myapps.microsoft.com](https://myapps.microsoft.com/)hello 테스트 계정에 로그인 하 고 클릭 **Netsuite**합니다.</span><span class="sxs-lookup"><span data-stu-id="2397e-284">tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into hello test account, and click **Netsuite**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2397e-285">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="2397e-285">Additional resources</span></span>

* [<span data-ttu-id="2397e-286">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="2397e-286">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2397e-287">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2397e-287">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="2397e-288">사용자 프로비저닝 구성</span><span class="sxs-lookup"><span data-stu-id="2397e-288">Configure User Provisioning</span></span>](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

