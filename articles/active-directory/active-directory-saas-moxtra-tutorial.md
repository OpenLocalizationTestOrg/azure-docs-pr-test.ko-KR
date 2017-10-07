---
title: "자습서: Moxtra와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Moxtra 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 82e2fcc390ba508e86a3992ec1c81d0a0ffed96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a><span data-ttu-id="604fc-103">자습서: Moxtra와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="604fc-103">Tutorial: Azure Active Directory integration with Moxtra</span></span>

<span data-ttu-id="604fc-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 Moxtra 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-104">In this tutorial, you learn how toointegrate Moxtra with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="604fc-105">Azure AD와 Moxtra 통합 hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-105">Integrating Moxtra with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="604fc-106">액세스 tooMoxtra을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-106">You can control in Azure AD who has access tooMoxtra</span></span>
- <span data-ttu-id="604fc-107">프로그램 사용자 tooautomatically get 로그온 tooMoxtra (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-107">You can enable your users tooautomatically get signed-on tooMoxtra (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="604fc-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="604fc-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="604fc-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="604fc-110">Prerequisites</span></span>

<span data-ttu-id="604fc-111">Azure AD 통합와 Moxtra tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-111">tooconfigure Azure AD integration with Moxtra, you need hello following items:</span></span>

- <span data-ttu-id="604fc-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="604fc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="604fc-113">Moxtra Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="604fc-113">A Moxtra single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="604fc-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="604fc-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="604fc-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="604fc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="604fc-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="604fc-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="604fc-118">Scenario description</span></span>
<span data-ttu-id="604fc-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="604fc-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="604fc-121">Moxtra는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="604fc-121">Adding Moxtra from hello gallery</span></span>
2. <span data-ttu-id="604fc-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="604fc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxtra-from-hello-gallery"></a><span data-ttu-id="604fc-123">Moxtra는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="604fc-123">Adding Moxtra from hello gallery</span></span>
<span data-ttu-id="604fc-124">tooconfigure hello와의 통합 Moxtra Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Moxtra tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-124">tooconfigure hello integration of Moxtra into Azure AD, you need tooadd Moxtra from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="604fc-125">**hello 갤러리에서 Moxtra tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="604fc-125">**tooadd Moxtra from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="604fc-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="604fc-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="604fc-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="604fc-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="604fc-133">Hello 검색 상자에 입력 **Moxtra**합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-133">In hello search box, type **Moxtra**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. <span data-ttu-id="604fc-135">Hello 결과 패널에서 선택 **Moxtra**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-135">In hello results panel, select **Moxtra**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="604fc-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="604fc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="604fc-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Moxtra에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-138">In this section, you configure and test Azure AD single sign-on with Moxtra based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="604fc-139">Single sign on toowork에 대 한 Azure AD는 tooknow Moxtra에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Moxtra is tooa user in Azure AD.</span></span> <span data-ttu-id="604fc-140">즉, Azure AD 사용자와 Moxtra에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-140">In other words, a link relationship between an Azure AD user and hello related user in Moxtra needs toobe established.</span></span>

<span data-ttu-id="604fc-141">Moxtra에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-141">In Moxtra, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="604fc-142">tooconfigure 및 Azure AD에서 single sign-on와 Moxtra 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-142">tooconfigure and test Azure AD single sign-on with Moxtra, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="604fc-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="604fc-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="604fc-145">**[Moxtra 테스트 사용자 만들기](#creating-a-moxtra-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Moxtra에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-145">**[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - toohave a counterpart of Britta Simon in Moxtra that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="604fc-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="604fc-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="604fc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="604fc-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="604fc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="604fc-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Moxtra 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Moxtra application.</span></span>

<span data-ttu-id="604fc-150">**Azure AD tooconfigure single sign on와 Moxtra, hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="604fc-150">**tooconfigure Azure AD single sign-on with Moxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="604fc-151">Hello hello에 Azure 포털에서에서 **Moxtra** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-151">In hello Azure portal, on hello **Moxtra** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="604fc-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. <span data-ttu-id="604fc-155">Hello에 **Moxtra 도메인 및 Url** 섹션에서 단계 다음에 나오는 hello 수행:</span><span class="sxs-lookup"><span data-stu-id="604fc-155">On hello **Moxtra Domain and URLs** section, perform hello following step:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    <span data-ttu-id="604fc-157">Hello에 **로그온 URL** 텍스트 상자에 다음 URL로:`https://www.moxtra.com/service/#login`</span><span class="sxs-lookup"><span data-stu-id="604fc-157">In hello **Sign-on URL** textbox, type a URL as: `https://www.moxtra.com/service/#login`</span></span>

4. <span data-ttu-id="604fc-158">Moxtra 응용 프로그램에는 특정 형식의 hello SAML 어설션 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-158">Moxtra application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="604fc-159">이 응용 프로그램에 대 한 클레임을 따라 hello를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-159">Configure hello following claims for this application.</span></span> <span data-ttu-id="604fc-160">Hello에서 이러한 특성의 hello 값을 관리할 수 있습니다 "**사용자 특성**" 응용 프로그램 통합 페이지에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="604fc-160">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="604fc-161">hello 스크린 샷 뒤에이 구성에 대 한 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-161">hello following screenshot shows an example for this configuration.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. <span data-ttu-id="604fc-163">Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 hello 이미지에 나와 있는 것 처럼 SAML 토큰 특성을 구성 하 고 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-163">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="604fc-164">특성 이름</span><span class="sxs-lookup"><span data-stu-id="604fc-164">Attribute Name</span></span> | <span data-ttu-id="604fc-165">특성 값</span><span class="sxs-lookup"><span data-stu-id="604fc-165">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="604fc-166">firstname</span><span class="sxs-lookup"><span data-stu-id="604fc-166">firstname</span></span> | <span data-ttu-id="604fc-167">user.givenname</span><span class="sxs-lookup"><span data-stu-id="604fc-167">user.givenname</span></span> |
    | <span data-ttu-id="604fc-168">lastname</span><span class="sxs-lookup"><span data-stu-id="604fc-168">lastname</span></span> | <span data-ttu-id="604fc-169">user.surname</span><span class="sxs-lookup"><span data-stu-id="604fc-169">user.surname</span></span> |
    | <span data-ttu-id="604fc-170">idpid</span><span class="sxs-lookup"><span data-stu-id="604fc-170">idpid</span></span>    | <span data-ttu-id="604fc-171">< SAML 엔터티 ID ></span><span class="sxs-lookup"><span data-stu-id="604fc-171">< SAML Entity ID ></span></span> 

    > [!Note]
    > <span data-ttu-id="604fc-172">값을 hello **idpid** 특성이 실제있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-172">hello value of **idpid** attribute is not real.</span></span> <span data-ttu-id="604fc-173">hello 실제 값을 얻을 수 **빠른 참조** 섹션 아래 **Moxtra 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-173">You can get hello actual value from **Quick reference** section under **Moxtra Configuration**.</span></span>
    
    <span data-ttu-id="604fc-174">a.</span><span class="sxs-lookup"><span data-stu-id="604fc-174">a.</span></span> <span data-ttu-id="604fc-175">클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="604fc-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="604fc-177">b.</span><span class="sxs-lookup"><span data-stu-id="604fc-177">b.</span></span> <span data-ttu-id="604fc-178">Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="604fc-180">c.</span><span class="sxs-lookup"><span data-stu-id="604fc-180">c.</span></span> <span data-ttu-id="604fc-181">Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-181">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="604fc-182">d.</span><span class="sxs-lookup"><span data-stu-id="604fc-182">d.</span></span> <span data-ttu-id="604fc-183">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-183">Click **Ok**.</span></span>
    
5. <span data-ttu-id="604fc-184">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-184">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. <span data-ttu-id="604fc-186">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-186">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="604fc-188">Hello에 **Moxtra 구성** 섹션에서 클릭 **구성 Moxtra** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="604fc-188">On hello **Moxtra Configuration** section, click **Configure Moxtra** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="604fc-189">복사 hello **SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="604fc-189">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. <span data-ttu-id="604fc-191">다른 브라우저 창에서 관리자 권한으로 tooyour Moxtra 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-191">In another browser window, sign on tooyour Moxtra company site as an administrator.</span></span>

9. <span data-ttu-id="604fc-192">Hello 왼쪽에 hello 도구 모음에서 클릭 **관리 콘솔 > SAML Single Sign on**, 클릭 하 고 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-192">In hello toolbar on hello left, click **Admin Console > SAML Single Sign-on**, and then click **New**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. <span data-ttu-id="604fc-194">Hello에 **SAML** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-194">On hello **SAML** page, perform hello following steps:</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    <span data-ttu-id="604fc-196">a.</span><span class="sxs-lookup"><span data-stu-id="604fc-196">a.</span></span> <span data-ttu-id="604fc-197">Hello에 **이름** 텍스트 상자 구성 이름 입력 합니다 (예:: *SAML*).</span><span class="sxs-lookup"><span data-stu-id="604fc-197">In hello **Name** textbox, type a name for your configuration (e.g.: *SAML*).</span></span> 
  
    <span data-ttu-id="604fc-198">b.</span><span class="sxs-lookup"><span data-stu-id="604fc-198">b.</span></span> <span data-ttu-id="604fc-199">Hello에 **IdP 엔터티 ID** 붙여넣기 hello 값의 텍스트 상자 **SAML 엔터티 ID** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-199">In hello **IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="604fc-200">c.</span><span class="sxs-lookup"><span data-stu-id="604fc-200">c.</span></span> <span data-ttu-id="604fc-201">**로그인 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-201">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="604fc-202">d.</span><span class="sxs-lookup"><span data-stu-id="604fc-202">d.</span></span> <span data-ttu-id="604fc-203">Hello에 **AuthnContextClassRef** 텍스트 상자에 **urn: oasis: 이름: tc: SAML:2.0:ac:classes:Password**합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-203">In hello **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span> 
 
    <span data-ttu-id="604fc-204">e.</span><span class="sxs-lookup"><span data-stu-id="604fc-204">e.</span></span> <span data-ttu-id="604fc-205">Hello에 **NameID 형식** 텍스트 상자에 **urn: oasis: 이름: tc: SAML:1.1:nameid-: emailAddress**합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-205">In hello **NameID Format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span> 
 
    <span data-ttu-id="604fc-206">f.</span><span class="sxs-lookup"><span data-stu-id="604fc-206">f.</span></span> <span data-ttu-id="604fc-207">메모장에서 Azure 포털에서 다운로드 한 인증서 열기 hello 내용을 복사 하 고 hello에 붙여 넣습니다 **인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-207">Open certificate which you have downloaded from Azure portal in notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span>    
 
    <span data-ttu-id="604fc-208">g.</span><span class="sxs-lookup"><span data-stu-id="604fc-208">g.</span></span> <span data-ttu-id="604fc-209">Hello SAML 전자 메일 도메인 텍스트 상자에 SAML 전자 메일 도메인을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-209">In hello SAML email domain textbox, type your SAML email domain.</span></span>    
  
    >[!NOTE]
    ><span data-ttu-id="604fc-210">toosee hello 단계 tooverify hello 도메인 hello 클릭 "**i**" 아래 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-210">toosee hello steps tooverify hello domain, click hello "**i**" below.</span></span>

    <span data-ttu-id="604fc-211">h.</span><span class="sxs-lookup"><span data-stu-id="604fc-211">h.</span></span> <span data-ttu-id="604fc-212">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-212">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="604fc-213">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="604fc-213">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="604fc-214">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="604fc-214">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="604fc-215">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="604fc-215">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="604fc-216">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="604fc-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="604fc-217">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="604fc-219">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="604fc-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="604fc-220">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="604fc-222">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="604fc-224">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="604fc-226">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="604fc-228">a.</span><span class="sxs-lookup"><span data-stu-id="604fc-228">a.</span></span> <span data-ttu-id="604fc-229">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="604fc-230">b.</span><span class="sxs-lookup"><span data-stu-id="604fc-230">b.</span></span> <span data-ttu-id="604fc-231">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="604fc-232">c.</span><span class="sxs-lookup"><span data-stu-id="604fc-232">c.</span></span> <span data-ttu-id="604fc-233">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="604fc-234">d.</span><span class="sxs-lookup"><span data-stu-id="604fc-234">d.</span></span> <span data-ttu-id="604fc-235">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-235">Click **Create**.</span></span>
 
### <a name="creating-a-moxtra-test-user"></a><span data-ttu-id="604fc-236">Moxtra 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="604fc-236">Creating a Moxtra test user</span></span>

<span data-ttu-id="604fc-237">hello이이 섹션의 목적은 toocreate Britta Simon Moxtra에서 호출 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-237">hello objective of this section is toocreate a user called Britta Simon in Moxtra.</span></span>

<span data-ttu-id="604fc-238">**toocreate Britta Simon Moxtra의 라는 사용자를 만들면 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="604fc-238">**toocreate a user called Britta Simon in Moxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="604fc-239">관리자 권한으로 Moxtra 회사 사이트 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-239">Sign on tooyour Moxtra company site as an administrator.</span></span>

2. <span data-ttu-id="604fc-240">Hello 왼쪽에 hello 도구 모음에서 클릭 **관리 콘솔 > 사용자 관리**, 차례로 **사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-240">In hello toolbar on hello left, click **Admin Console > User Management**, and then **Add User**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. <span data-ttu-id="604fc-242">Hello에 **사용자 추가** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-242">On hello **Add User** dialog, perform hello following steps:</span></span>
  
    <span data-ttu-id="604fc-243">a.</span><span class="sxs-lookup"><span data-stu-id="604fc-243">a.</span></span> <span data-ttu-id="604fc-244">Hello에 **이름** 텍스트 상자에 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-244">In hello **First Name** textbox, type **Britta**.</span></span>
  
    <span data-ttu-id="604fc-245">b.</span><span class="sxs-lookup"><span data-stu-id="604fc-245">b.</span></span> <span data-ttu-id="604fc-246">Hello에 **성** 텍스트 상자에 **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-246">In hello **Last Name** textbox, type **Simon**.</span></span>
  
    <span data-ttu-id="604fc-247">c.</span><span class="sxs-lookup"><span data-stu-id="604fc-247">c.</span></span> <span data-ttu-id="604fc-248">Hello에 **전자 메일** 텍스트 상자에 Britta의 전자 메일 주소 Azure 포털에서와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-248">In hello **Email** textbox, type Britta's email address same as on Azure portal.</span></span>
  
    <span data-ttu-id="604fc-249">d.</span><span class="sxs-lookup"><span data-stu-id="604fc-249">d.</span></span> <span data-ttu-id="604fc-250">Hello에 **나누기** 텍스트 상자에 **Dev**합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-250">In hello **Division** textbox, type **Dev**.</span></span>
  
    <span data-ttu-id="604fc-251">e.</span><span class="sxs-lookup"><span data-stu-id="604fc-251">e.</span></span> <span data-ttu-id="604fc-252">Hello에 **부서** 텍스트 상자에 **IT**합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-252">In hello **Department** textbox, type **IT**.</span></span>
  
    <span data-ttu-id="604fc-253">f.</span><span class="sxs-lookup"><span data-stu-id="604fc-253">f.</span></span> <span data-ttu-id="604fc-254">**관리자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-254">Select **Administrator**.</span></span>
  
    <span data-ttu-id="604fc-255">g.</span><span class="sxs-lookup"><span data-stu-id="604fc-255">g.</span></span> <span data-ttu-id="604fc-256">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-256">Click **Add**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="604fc-257">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="604fc-258">이 섹션에서는 tooMoxtra 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMoxtra.</span></span>

![사용자 할당][200] 

<span data-ttu-id="604fc-260">**tooassign Britta Simon tooMoxtra hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="604fc-260">**tooassign Britta Simon tooMoxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="604fc-261">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="604fc-263">Hello 응용 프로그램 목록에서 선택 **Moxtra**합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-263">In hello applications list, select **Moxtra**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. <span data-ttu-id="604fc-265">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="604fc-267">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-267">Click **Add** button.</span></span> <span data-ttu-id="604fc-268">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="604fc-270">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="604fc-271">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="604fc-272">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="604fc-273">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="604fc-273">Testing single sign-on</span></span>

<span data-ttu-id="604fc-274">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-274">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="604fc-275">Hello 액세스 패널에서에서 hello Moxtra 타일을 클릭할 때 자동으로 로그온 tooyour Moxtra 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-275">When you click hello Moxtra tile in hello Access Panel, you should get automatically signed-on tooyour Moxtra application.</span></span>
<span data-ttu-id="604fc-276">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="604fc-276">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="604fc-277">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="604fc-277">Additional resources</span></span>

* [<span data-ttu-id="604fc-278">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="604fc-278">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="604fc-279">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="604fc-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

