---
title: "자습서: ScaleX Enterprise와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory와 ScaleX 엔터프라이즈 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: e398b98d9e0957b5f92c82359651c345d22c3a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a><span data-ttu-id="866f8-103">자습서: ScaleX Enterprise와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="866f8-103">Tutorial: Azure Active Directory integration with ScaleX Enterprise</span></span>

<span data-ttu-id="866f8-104">이 자습서에 설명 어떻게 toointegrate ScaleX Enterprise와 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="866f8-104">In this tutorial, you learn how toointegrate ScaleX Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="866f8-105">Azure AD와 ScaleX 엔터프라이즈 통합 이점을 다음 hello 제공:</span><span class="sxs-lookup"><span data-stu-id="866f8-105">Integrating ScaleX Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="866f8-106">액세스 tooScaleX Enterprise을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-106">You can control in Azure AD who has access tooScaleX Enterprise</span></span>
- <span data-ttu-id="866f8-107">에 사용자가 tooautomatically get 로그온 tooScaleX (Single Sign-on)는 엔터프라이즈 자신의 Azure AD 계정으로 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-107">You can enable your users tooautomatically get signed-on tooScaleX Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="866f8-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="866f8-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 참조 tooknow 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="866f8-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="866f8-110">[Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="866f8-110">What is application access and single sign-on with [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="866f8-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="866f8-111">Prerequisites</span></span>

<span data-ttu-id="866f8-112">다음 항목 hello가 필요 tooconfigure ScaleX Enterprise와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-112">tooconfigure Azure AD integration with ScaleX Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="866f8-113">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="866f8-113">An Azure AD subscription</span></span>
- <span data-ttu-id="866f8-114">ScaleX Enterprise Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="866f8-114">A ScaleX Enterprise single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="866f8-115">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="866f8-116">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="866f8-117">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="866f8-117">Do not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="866f8-118">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="866f8-119">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="866f8-119">Scenario description</span></span>
<span data-ttu-id="866f8-120">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="866f8-121">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="866f8-122">ScaleX 엔터프라이즈 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="866f8-122">Adding ScaleX Enterprise from hello gallery</span></span>
2. <span data-ttu-id="866f8-123">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="866f8-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scalex-enterprise-from-hello-gallery"></a><span data-ttu-id="866f8-124">ScaleX 엔터프라이즈 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="866f8-124">Adding ScaleX Enterprise from hello gallery</span></span>
<span data-ttu-id="866f8-125">tooconfigure hello와의 통합 ScaleX 엔터프라이즈 tooAzure AD에서에서 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 ScaleX 엔터프라이즈 tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-125">tooconfigure hello integration of ScaleX Enterprise in tooAzure AD, you need tooadd ScaleX Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="866f8-126">**hello 갤러리에서 ScaleX 엔터프라이즈 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="866f8-126">**tooadd ScaleX Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="866f8-127">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="866f8-129">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="866f8-130">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-130">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="866f8-132">클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-132">Click **Add** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="866f8-134">Hello 검색 상자에 입력 **ScaleX 엔터프라이즈**합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-134">In hello search box, type **ScaleX Enterprise**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. <span data-ttu-id="866f8-136">Hello 결과 패널에서 선택 **ScaleX 엔터프라이즈**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-136">In hello results panel, select **ScaleX Enterprise**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="866f8-138">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="866f8-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="866f8-139">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 ScaleX Enterprise에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-139">In this section, you configure and test Azure AD single sign-on with ScaleX Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="866f8-140">Single sign on toowork에 대 한 Azure AD는 tooknow ScaleX 기업에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ScaleX Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="866f8-141">즉, Azure AD 사용자 및 ScaleX 기업의 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-141">In other words, a link relationship between an Azure AD user and hello related user in ScaleX Enterprise needs toobe established.</span></span>

<span data-ttu-id="866f8-142">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** ScaleX 기업에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ScaleX Enterprise.</span></span>

<span data-ttu-id="866f8-143">tooconfigure 및 ScaleX Enterprise를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-143">tooconfigure and test Azure AD single sign-on with ScaleX Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="866f8-144">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="866f8-145">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="866f8-146">**[ScaleX Enterprise 테스트 사용자 만들기](#creating-a-scalex-enterprise-test-user)**  -toohave 사용자의 연결 된 Azure AD toohello 표현인 ScaleX enterprise Britta Simon의 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-146">**[Creating a ScaleX Enterprise test user](#creating-a-scalex-enterprise-test-user)** - toohave a counterpart of Britta Simon in ScaleX Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="866f8-147">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="866f8-148">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="866f8-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="866f8-149">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="866f8-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="866f8-150">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 ScaleX 엔터프라이즈 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ScaleX Enterprise application.</span></span>

<span data-ttu-id="866f8-151">**Azure AD tooconfigure single sign on ScaleX 엔터프라이즈와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="866f8-151">**tooconfigure Azure AD single sign-on with ScaleX Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="866f8-152">Hello hello에 Azure 포털에서에서 **ScaleX 엔터프라이즈** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-152">In hello Azure portal, on hello **ScaleX Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="866f8-154">Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-154">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. <span data-ttu-id="866f8-156">Hello에 **ScaleX 엔터프라이즈 도메인 및 Url** 섹션를 hello tooconfigure hello 응용 프로그램에 필요한 경우 다음 단계를 수행 **IDP** 시작 모드:</span><span class="sxs-lookup"><span data-stu-id="866f8-156">On hello **ScaleX Enterprise Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    <span data-ttu-id="866f8-158">a.</span><span class="sxs-lookup"><span data-stu-id="866f8-158">a.</span></span> <span data-ttu-id="866f8-159">Hello에 **식별자** hello 패턴을 사용 하 여 형식 hello 값 텍스트 상자:`https://platform.rescale.com/saml2/<company id>/`</span><span class="sxs-lookup"><span data-stu-id="866f8-159">In hello **Identifier** textbox, type hello value using hello following pattern: `https://platform.rescale.com/saml2/<company id>/`</span></span>

    <span data-ttu-id="866f8-160">b.</span><span class="sxs-lookup"><span data-stu-id="866f8-160">b.</span></span> <span data-ttu-id="866f8-161">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://platform.rescale.com/saml2/<company id>/acs/`</span><span class="sxs-lookup"><span data-stu-id="866f8-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://platform.rescale.com/saml2/<company id>/acs/`</span></span>

4. <span data-ttu-id="866f8-162">확인 **고급 URL 설정 표시**tooconfigure hello 응용 프로그램에 필요한 경우, **SP** 시작 모드:</span><span class="sxs-lookup"><span data-stu-id="866f8-162">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    <span data-ttu-id="866f8-164">Hello에 **로그온 URL** hello 패턴을 사용 하 여 형식 hello 값 텍스트 상자:`https://platform.rescale.com/saml2/<company id>/sso/`</span><span class="sxs-lookup"><span data-stu-id="866f8-164">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://platform.rescale.com/saml2/<company id>/sso/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="866f8-165">이들은 hello 실제 값입니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-165">These are not hello real values.</span></span> <span data-ttu-id="866f8-166">실제 식별자, 회신 URL 또는 로그온 URL hello로 이러한 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-166">Update these values with hello actual Identifier, Reply URL or Sign-On URL.</span></span> <span data-ttu-id="866f8-167">연락처 [ScaleX 엔터프라이즈 클라이언트 지원 팀](http://info.rescale.com/contact_sales) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-167">Contact [ScaleX Enterprise Client support team](http://info.rescale.com/contact_sales) tooget these values.</span></span> 

5. <span data-ttu-id="866f8-168">ScaleX 응용 프로그램의 구성을 수행 해야 하면 toomodify 사용자 지정 특성 매핑을 tooyour SAML 토큰 특성을 특정 형식에서 hello SAML 어설션이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-168">Your ScaleX application expects hello SAML assertions in a specific format, which requires you toomodify custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="866f8-169">클릭 **보기 및 다른 모든 사용자 특성 편집** 확인란 tooopen hello 사용자 지정 특성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-169">Click **View and edit all other user attributes** checkbox tooopen hello custom attributes settings.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    <span data-ttu-id="866f8-171">a.</span><span class="sxs-lookup"><span data-stu-id="866f8-171">a.</span></span> <span data-ttu-id="866f8-172">Hello 특성을 마우스 오른쪽 단추로 클릭 **이름** 고 삭제를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-172">Right click hello attribute **name** and click delete.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    <span data-ttu-id="866f8-174">b.</span><span class="sxs-lookup"><span data-stu-id="866f8-174">b.</span></span> <span data-ttu-id="866f8-175">클릭 **emailaddress** 특성 tooopen hello 특성 편집 창.</span><span class="sxs-lookup"><span data-stu-id="866f8-175">Click **emailaddress** attribute tooopen hello Edit Attribute window.</span></span> <span data-ttu-id="866f8-176">해당 값에서 변경 **user.mail** 너무**user.userprincipalname** 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-176">Change its value from **user.mail** too**user.userprincipalname** and click Ok.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. <span data-ttu-id="866f8-178">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-178">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. <span data-ttu-id="866f8-180">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-180">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="866f8-182">Hello에 **ScaleX 엔터프라이즈 구성** 섹션에서 클릭 **ScaleX 엔터프라이즈 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="866f8-182">On hello **ScaleX Enterprise Configuration** section, click **Configure ScaleX Enterprise** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="866f8-183">복사 hello **SAML 엔터티 ID** 및 **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="866f8-183">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. <span data-ttu-id="866f8-185">tooconfigure single sign on에서 **ScaleX 엔터프라이즈** 쪽, 로그인 toohello ScaleX Enterprise 회사 웹 사이트를 관리자로 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-185">tooconfigure single sign-on on **ScaleX Enterprise** side, login toohello ScaleX Enterprise company website as an administrator.</span></span>

9. <span data-ttu-id="866f8-186">오른쪽 위 hello에 hello 메뉴를 클릭 하 고 선택 **Contoso 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-186">Click hello menu in hello upper right and select **Contoso Administration**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="866f8-187">Contoso는 예일뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-187">Contoso is just an example.</span></span> <span data-ttu-id="866f8-188">이 값은 실제 회사 이름이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-188">This should be your actual Company Name.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. <span data-ttu-id="866f8-190">선택 **통합** hello 최상위 메뉴와 선택에서 **Single Sign On**합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-190">Select **Integrations** from hello top menu and select **Single Sign-On**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. <span data-ttu-id="866f8-192">다음과 같이 hello 양식을 작성 하 여:</span><span class="sxs-lookup"><span data-stu-id="866f8-192">Complete hello form as follows:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    <span data-ttu-id="866f8-194">a.</span><span class="sxs-lookup"><span data-stu-id="866f8-194">a.</span></span> <span data-ttu-id="866f8-195">**“Create any user who can authenticate with SSO.”(SSO로 인증할 수 있는 사용자 만들기)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-195">Select **“Create any user who can authenticate with SSO.”**</span></span>

    <span data-ttu-id="866f8-196">b.</span><span class="sxs-lookup"><span data-stu-id="866f8-196">b.</span></span> <span data-ttu-id="866f8-197">**서비스 공급자 saml**: hello 값을 붙여 ***urn: oasis: 이름: tc: SAML:2.0:nameid-형식: 영구***</span><span class="sxs-lookup"><span data-stu-id="866f8-197">**Service Provider saml**: Paste hello value ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span></span>

    <span data-ttu-id="866f8-198">c.</span><span class="sxs-lookup"><span data-stu-id="866f8-198">c.</span></span> <span data-ttu-id="866f8-199">**ACS 응답에 전자 메일 필드 Id 공급자의 이름**: hello 값을 붙여 넣습니다.`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="866f8-199">**Name of Identity Provider email field in ACS response**: Paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>

    <span data-ttu-id="866f8-200">d.</span><span class="sxs-lookup"><span data-stu-id="866f8-200">d.</span></span> <span data-ttu-id="866f8-201">**Id 공급자 EntityDescriptor 엔터티 ID:** 붙여넣기 hello **SAML 엔터티 ID** 값 hello Azure 포털에서에서 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-201">**Identity Provider EntityDescriptor Entity ID:** Paste hello **SAML Entity ID** value copied from hello Azure portal.</span></span>

    <span data-ttu-id="866f8-202">e.</span><span class="sxs-lookup"><span data-stu-id="866f8-202">e.</span></span> <span data-ttu-id="866f8-203">**Id 공급자 SingleSignOnService URL:** 붙여넣기 hello **SAML Single Sign-on 서비스 URL** hello Azure 포털에서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-203">**Identity Provider SingleSignOnService URL:** Paste hello **SAML Single Sign-On Service URL** from hello Azure portal.</span></span>

    <span data-ttu-id="866f8-204">f.</span><span class="sxs-lookup"><span data-stu-id="866f8-204">f.</span></span> <span data-ttu-id="866f8-205">**Id 공급자 공용 X509 인증서:** 열려 hello X509 인증서가이 상자에서 메모장 및 붙여넣기 hello 내용에 hello Azure에서에서 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-205">**Identity Provider public X509 certificate:** Open hello X509 certificate downloaded from hello Azure in notepad and paste hello contents in this box.</span></span> <span data-ttu-id="866f8-206">없는에서 줄 바꿈 hello hello 인증서 내용의 중간 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="866f8-206">Ensure there are no line breaks in hello middle of hello certificate contents.</span></span>
    
    <span data-ttu-id="866f8-207">g.</span><span class="sxs-lookup"><span data-stu-id="866f8-207">g.</span></span> <span data-ttu-id="866f8-208">다음 확인란을 선택 하는 hello 확인: **Enabled, NameID 암호화 및 서명 AuthnRequests 합니다.**</span><span class="sxs-lookup"><span data-stu-id="866f8-208">Check hello following checkboxes: **Enabled, Encrypt NameID and Sign AuthnRequests.**</span></span>

    <span data-ttu-id="866f8-209">h.</span><span class="sxs-lookup"><span data-stu-id="866f8-209">h.</span></span> <span data-ttu-id="866f8-210">클릭 **업데이트 SSO 설정** toosave hello 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-210">Click **Update SSO Settings** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="866f8-211">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="866f8-211">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="866f8-212">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="866f8-212">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="866f8-213">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="866f8-213">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="866f8-214">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="866f8-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="866f8-215">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="866f8-217">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="866f8-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="866f8-218">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="866f8-220">너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-220">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="866f8-222">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="866f8-222">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="866f8-224">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="866f8-226">a.</span><span class="sxs-lookup"><span data-stu-id="866f8-226">a.</span></span> <span data-ttu-id="866f8-227">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="866f8-228">b.</span><span class="sxs-lookup"><span data-stu-id="866f8-228">b.</span></span> <span data-ttu-id="866f8-229">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="866f8-230">c.</span><span class="sxs-lookup"><span data-stu-id="866f8-230">c.</span></span> <span data-ttu-id="866f8-231">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="866f8-232">d.</span><span class="sxs-lookup"><span data-stu-id="866f8-232">d.</span></span> <span data-ttu-id="866f8-233">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-233">Click **Create**.</span></span>
 
### <a name="creating-a-scalex-enterprise-test-user"></a><span data-ttu-id="866f8-234">ScaleX Enterprise 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="866f8-234">Creating a ScaleX Enterprise test user</span></span>

<span data-ttu-id="866f8-235">tooenable Azure AD 사용자가 toolog tooScaleX Enterprise에서에서 제공 되어야은 tooScaleX 엔터프라이즈에서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-235">tooenable Azure AD users toolog in tooScaleX Enterprise, they must be provisioned in tooScaleX Enterprise.</span></span> <span data-ttu-id="866f8-236">Hello ScaleX Enterprise의 경우에서 프로 비전은 자동 작업 하 고 어떤 수동 단계도 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-236">In hello case of ScaleX Enterprise, provisioning is an automatic task and no manual steps are required.</span></span> <span data-ttu-id="866f8-237">Hello ScaleX 측에서 SSO 자격 증명으로 인증할 수 있는 모든 사용자를 자동으로 프로 비전 됩니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-237">Any user who can successfully authenticate with SSO credentials will be automatically provisioned on hello ScaleX side.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="866f8-238">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-238">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="866f8-239">이 섹션에서는 사용자 액세스 tooScaleX 엔터프라이즈를 부여 하 여 Britta Simon toouse Azure single sign on을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting user access tooScaleX Enterprise.</span></span>

![사용자 할당][200] 

<span data-ttu-id="866f8-241">**tooassign Britta Simon tooScaleX 엔터프라이즈 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="866f8-241">**tooassign Britta Simon tooScaleX Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="866f8-242">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="866f8-244">Hello 응용 프로그램 목록에서 선택 **ScaleX 엔터프라이즈**합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-244">In hello applications list, select **ScaleX Enterprise**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. <span data-ttu-id="866f8-246">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="866f8-248">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-248">Click **Add** button.</span></span> <span data-ttu-id="866f8-249">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="866f8-251">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="866f8-252">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="866f8-253">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-253">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="866f8-254">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="866f8-254">Testing single sign-on</span></span>

<span data-ttu-id="866f8-255">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-255">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="866f8-256">Hello ScaleX 엔터프라이즈 hello 액세스 패널에서에서 타일을 클릭 합니다. 자동으로 로그온 tooyour ScaleX 엔터프라이즈 응용 프로그램을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-256">Click hello ScaleX Enterprise tile in hello Access Panel, you will get automatically signed-on tooyour ScaleX Enterprise application.</span></span> <span data-ttu-id="866f8-257">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](https://msdn.microsoft.com/library/dn308586)합니다.</span><span class="sxs-lookup"><span data-stu-id="866f8-257">For more information about hello Access Panel, see [Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="866f8-258">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="866f8-258">Additional resources</span></span>

* [<span data-ttu-id="866f8-259">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="866f8-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="866f8-260">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="866f8-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

