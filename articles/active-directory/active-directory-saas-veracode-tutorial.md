---
title: "자습서: Veracode와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Veracode 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d17307b3864b7df8ee55f569d8f962e2e315b936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a><span data-ttu-id="10bd4-103">자습서: Veracode와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="10bd4-103">Tutorial: Azure Active Directory integration with Veracode</span></span>

<span data-ttu-id="10bd4-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 Veracode 합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-104">In this tutorial, you learn how toointegrate Veracode with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="10bd4-105">Azure AD와 Veracode 통합 hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-105">Integrating Veracode with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="10bd4-106">액세스 tooVeracode을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-106">You can control in Azure AD who has access tooVeracode.</span></span>
- <span data-ttu-id="10bd4-107">에 사용자가 tooautomatically get 로그온 tooVeracode (Single Sign-on)는 Azure AD 계정으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-107">You can enable your users tooautomatically get signed-on tooVeracode (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="10bd4-108">하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="10bd4-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10bd4-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="10bd4-110">Prerequisites</span></span>

<span data-ttu-id="10bd4-111">Azure AD 통합와 Veracode tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-111">tooconfigure Azure AD integration with Veracode, you need hello following items:</span></span>

- <span data-ttu-id="10bd4-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="10bd4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="10bd4-113">Veracode Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="10bd4-113">A Veracode single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="10bd4-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="10bd4-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="10bd4-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="10bd4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="10bd4-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="10bd4-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="10bd4-118">Scenario description</span></span>
<span data-ttu-id="10bd4-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="10bd4-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="10bd4-121">Veracode hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="10bd4-121">Add Veracode from hello gallery</span></span>
2. <span data-ttu-id="10bd4-122">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="10bd4-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-veracode-from-hello-gallery"></a><span data-ttu-id="10bd4-123">Veracode hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="10bd4-123">Add Veracode from hello gallery</span></span>
<span data-ttu-id="10bd4-124">tooconfigure hello와의 통합 Veracode Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Veracode tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-124">tooconfigure hello integration of Veracode into Azure AD, you need tooadd Veracode from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="10bd4-125">**hello 갤러리에서 Veracode tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="10bd4-125">**tooadd Veracode from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="10bd4-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="10bd4-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="10bd4-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="10bd4-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="10bd4-133">Hello 검색 상자에 입력 **Veracode**선택, **Veracode** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-133">In hello search box, type **Veracode**, select  **Veracode** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Veracode hello 결과 목록에서](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="10bd4-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="10bd4-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="10bd4-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Veracode에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-136">In this section, you configure and test Azure AD single sign-on with Veracode based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="10bd4-137">Single sign on toowork에 대 한 Azure AD는 tooknow Veracode에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Veracode is tooa user in Azure AD.</span></span> <span data-ttu-id="10bd4-138">즉, Azure AD 사용자와 Veracode에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-138">In other words, a link relationship between an Azure AD user and hello related user in Veracode needs toobe established.</span></span>

<span data-ttu-id="10bd4-139">Veracode에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-139">In Veracode, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="10bd4-140">tooconfigure 및 Azure AD에서 single sign-on와 Veracode 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-140">tooconfigure and test Azure AD single sign-on with Veracode, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="10bd4-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="10bd4-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="10bd4-143">**[Veracode 테스트 사용자 만들기](#create-a-veracode-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Veracode에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-143">**[Create a Veracode test user](#create-a-veracode-test-user)** - toohave a counterpart of Britta Simon in Veracode that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="10bd4-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="10bd4-145">**[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="10bd4-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="10bd4-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="10bd4-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="10bd4-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Veracode 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Veracode application.</span></span>

<span data-ttu-id="10bd4-148">**Azure AD tooconfigure single sign on와 Veracode, hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="10bd4-148">**tooconfigure Azure AD single sign-on with Veracode, perform hello following steps:**</span></span>

1. <span data-ttu-id="10bd4-149">Hello hello에 Azure 포털에서에서 **Veracode** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-149">In hello Azure portal, on hello **Veracode** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="10bd4-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. <span data-ttu-id="10bd4-153">Hello에 **Veracode 도메인 및 Url** 섹션에서 사용자 tooperform 모든 단계와 서로 hello 앱 Azure로 이미 사전 통합 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-153">On hello **Veracode Domain and URLs** section, the user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. <span data-ttu-id="10bd4-155">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-155">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. <span data-ttu-id="10bd4-157">hello이이 섹션의 목적은 toooutline 페더레이션을 사용 하 여 Azure AD에서 자신의 계정으로 tooenable 사용자 tooauthenticate tooVeracode hello SAML 프로토콜에 따라 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-157">hello objective of this section is toooutline how tooenable users tooauthenticate tooVeracode with their account in Azure AD using federation based on hello SAML protocol.</span></span>

    <span data-ttu-id="10bd4-158">Veracode 응용 프로그램에 사용자 지정 특성 매핑을 tooyour tooadd 요구 하는 특정 형식으로 hello SAML 어설션이 **saml 토큰 특성** 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-158">Your Veracode application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **saml token attributes** configuration.</span></span> <span data-ttu-id="10bd4-159">다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-159">hello following screenshot shows an example for this.</span></span>
    
    <span data-ttu-id="10bd4-160">![특성](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "특성")</span><span class="sxs-lookup"><span data-stu-id="10bd4-160">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Attributes")</span></span>

6. <span data-ttu-id="10bd4-161">tooadd hello 필요한 특성 매핑을 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-161">tooadd hello required attribute mappings, perform hello following steps:</span></span>

    | <span data-ttu-id="10bd4-162">특성 이름</span><span class="sxs-lookup"><span data-stu-id="10bd4-162">Attribute Name</span></span> | <span data-ttu-id="10bd4-163">특성 값</span><span class="sxs-lookup"><span data-stu-id="10bd4-163">Attribute Value</span></span> |
    |--- |--- |
    | <span data-ttu-id="10bd4-164">firstname</span><span class="sxs-lookup"><span data-stu-id="10bd4-164">firstname</span></span> |<span data-ttu-id="10bd4-165">User.givenname</span><span class="sxs-lookup"><span data-stu-id="10bd4-165">User.givenname</span></span> |
    | <span data-ttu-id="10bd4-166">lastname</span><span class="sxs-lookup"><span data-stu-id="10bd4-166">lastname</span></span> |<span data-ttu-id="10bd4-167">User.surname</span><span class="sxs-lookup"><span data-stu-id="10bd4-167">User.surname</span></span> |
    | <span data-ttu-id="10bd4-168">email</span><span class="sxs-lookup"><span data-stu-id="10bd4-168">email</span></span> |<span data-ttu-id="10bd4-169">User.mail</span><span class="sxs-lookup"><span data-stu-id="10bd4-169">User.mail</span></span> |
    
    <span data-ttu-id="10bd4-170">a.</span><span class="sxs-lookup"><span data-stu-id="10bd4-170">a.</span></span> <span data-ttu-id="10bd4-171">위의 hello 테이블의 각 데이터 행에 대 한 클릭 **사용자 특성 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-171">For each data row in hello table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="10bd4-172">![특성](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "특성")</span><span class="sxs-lookup"><span data-stu-id="10bd4-172">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Attributes")</span></span>
    
    <span data-ttu-id="10bd4-173">![특성](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "특성")</span><span class="sxs-lookup"><span data-stu-id="10bd4-173">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Attributes")</span></span>
    
    <span data-ttu-id="10bd4-174">b.</span><span class="sxs-lookup"><span data-stu-id="10bd4-174">b.</span></span> <span data-ttu-id="10bd4-175">Hello에 **특성 이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-175">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="10bd4-176">c.</span><span class="sxs-lookup"><span data-stu-id="10bd4-176">c.</span></span> <span data-ttu-id="10bd4-177">Hello에 **특성 값** textbox, 해당 행에 대해 표시 된 선택 hello 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-177">In hello **Attribute Value** textbox, select hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="10bd4-178">d.</span><span class="sxs-lookup"><span data-stu-id="10bd4-178">d.</span></span> <span data-ttu-id="10bd4-179">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-179">Click **Ok**.</span></span>

7. <span data-ttu-id="10bd4-180">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-180">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="10bd4-182">Hello에 **Veracode 구성** 섹션에서 클릭 **구성 Veracode** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="10bd4-182">On hello **Veracode Configuration** section, click **Configure Veracode** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="10bd4-183">복사 hello **SAML 엔터티 ID** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="10bd4-183">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Veracode 구성](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. <span data-ttu-id="10bd4-185">다른 웹 브라우저 창에서 Veracode 회사 사이트에 관리자 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-185">In a different web browser window, log into your Veracode company site as an administrator.</span></span>

10. <span data-ttu-id="10bd4-186">Hello 메뉴에서 hello 위에 표시를 클릭 **설정**, 클릭 하 고 **Admin**합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-186">In hello menu on hello top, click **Settings**, and then click **Admin**.</span></span>
   
    <span data-ttu-id="10bd4-187">![관리](./media/active-directory-saas-veracode-tutorial/ic802911.png "관리")</span><span class="sxs-lookup"><span data-stu-id="10bd4-187">![Administration](./media/active-directory-saas-veracode-tutorial/ic802911.png "Administration")</span></span>

11. <span data-ttu-id="10bd4-188">Hello 클릭 **SAML** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-188">Click hello **SAML** tab.</span></span>

12. <span data-ttu-id="10bd4-189">Hello에 **조직 SAML 설정** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-189">In hello **Organization SAML Settings** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="10bd4-190">![관리](./media/active-directory-saas-veracode-tutorial/ic802912.png "관리")</span><span class="sxs-lookup"><span data-stu-id="10bd4-190">![Administration](./media/active-directory-saas-veracode-tutorial/ic802912.png "Administration")</span></span>
   
    <span data-ttu-id="10bd4-191">a.</span><span class="sxs-lookup"><span data-stu-id="10bd4-191">a.</span></span>  <span data-ttu-id="10bd4-192">**발급자** 붙여넣기 hello 값의 텍스트 상자 **SAML 엔터티 ID** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-192">In  **Issuer** textbox, paste hello value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="10bd4-193">b.</span><span class="sxs-lookup"><span data-stu-id="10bd4-193">b.</span></span> <span data-ttu-id="10bd4-194">Azure 포털에서 다운로드 한 인증서를 클릭 tooupload **파일 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-194">tooupload your downloaded certificate from Azure portal, click **Choose File**.</span></span>
   
    <span data-ttu-id="10bd4-195">c.</span><span class="sxs-lookup"><span data-stu-id="10bd4-195">c.</span></span> <span data-ttu-id="10bd4-196">**자체 등록 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-196">Select **Enable Self Registration**.</span></span>

13. <span data-ttu-id="10bd4-197">Hello에 **셀프 등록 설정** 섹션에서 단계에 따라 hello를 수행 하 고 클릭 **저장**:</span><span class="sxs-lookup"><span data-stu-id="10bd4-197">In hello **Self Registration Settings** section, perform hello following steps, and then click **Save**:</span></span>
   
    <span data-ttu-id="10bd4-198">![관리](./media/active-directory-saas-veracode-tutorial/ic802913.png "관리")</span><span class="sxs-lookup"><span data-stu-id="10bd4-198">![Administration](./media/active-directory-saas-veracode-tutorial/ic802913.png "Administration")</span></span>
   
    <span data-ttu-id="10bd4-199">a.</span><span class="sxs-lookup"><span data-stu-id="10bd4-199">a.</span></span> <span data-ttu-id="10bd4-200">**새 사용자 활성화**에 대해 **활성화 필요 없음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-200">As **New User Activation**, select **No Activation Required**.</span></span>
   
    <span data-ttu-id="10bd4-201">b.</span><span class="sxs-lookup"><span data-stu-id="10bd4-201">b.</span></span> <span data-ttu-id="10bd4-202">**사용자 데이터 업데이트**에 대해 **기본 설정 Veracode 사용자 데이터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-202">As **User Data Updates**, select **Preference Veracode User Data**.</span></span>
   
    <span data-ttu-id="10bd4-203">c.</span><span class="sxs-lookup"><span data-stu-id="10bd4-203">c.</span></span> <span data-ttu-id="10bd4-204">에 대 한 **SAML 특성 세부 정보**, hello 다음을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-204">For **SAML Attribute Details**, select hello following:</span></span>
      * <span data-ttu-id="10bd4-205">**사용자 역할**</span><span class="sxs-lookup"><span data-stu-id="10bd4-205">**User Roles**</span></span>
      * <span data-ttu-id="10bd4-206">**정책 관리자**</span><span class="sxs-lookup"><span data-stu-id="10bd4-206">**Policy Administrator**</span></span>
      * <span data-ttu-id="10bd4-207">**검토자**</span><span class="sxs-lookup"><span data-stu-id="10bd4-207">**Reviewer**</span></span>
      * <span data-ttu-id="10bd4-208">**보안 팀장**</span><span class="sxs-lookup"><span data-stu-id="10bd4-208">**Security Lead**</span></span>
      * <span data-ttu-id="10bd4-209">**경영자**</span><span class="sxs-lookup"><span data-stu-id="10bd4-209">**Executive**</span></span>
      * <span data-ttu-id="10bd4-210">**제출자**</span><span class="sxs-lookup"><span data-stu-id="10bd4-210">**Submitter**</span></span>
      * <span data-ttu-id="10bd4-211">**작성자**</span><span class="sxs-lookup"><span data-stu-id="10bd4-211">**Creator**</span></span>
      * <span data-ttu-id="10bd4-212">**모든 검색 형식**</span><span class="sxs-lookup"><span data-stu-id="10bd4-212">**All Scan Types**</span></span>
      * <span data-ttu-id="10bd4-213">**팀 멤버 자격**</span><span class="sxs-lookup"><span data-stu-id="10bd4-213">**Team Memberships**</span></span>
      * <span data-ttu-id="10bd4-214">**기본 팀**</span><span class="sxs-lookup"><span data-stu-id="10bd4-214">**Default Team**</span></span>

> [!TIP]
> <span data-ttu-id="10bd4-215">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="10bd4-215">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="10bd4-216">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="10bd4-216">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="10bd4-217">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="10bd4-217">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="10bd4-218">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="10bd4-218">Create an Azure AD test user</span></span>

<span data-ttu-id="10bd4-219">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-219">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="10bd4-221">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="10bd4-221">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="10bd4-222">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-222">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="10bd4-224">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-224">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="10bd4-226">tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="10bd4-226">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello 추가 단추](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="10bd4-228">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-228">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello 사용자 대화 상자](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    <span data-ttu-id="10bd4-230">a.</span><span class="sxs-lookup"><span data-stu-id="10bd4-230">a.</span></span> <span data-ttu-id="10bd4-231">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-231">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="10bd4-232">b.</span><span class="sxs-lookup"><span data-stu-id="10bd4-232">b.</span></span> <span data-ttu-id="10bd4-233">Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-233">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="10bd4-234">c.</span><span class="sxs-lookup"><span data-stu-id="10bd4-234">c.</span></span> <span data-ttu-id="10bd4-235">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-235">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="10bd4-236">d.</span><span class="sxs-lookup"><span data-stu-id="10bd4-236">d.</span></span> <span data-ttu-id="10bd4-237">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-237">Click **Create**.</span></span>
 
### <a name="create-a-veracode-test-user"></a><span data-ttu-id="10bd4-238">Veracode 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="10bd4-238">Create a Veracode test user</span></span>
<span data-ttu-id="10bd4-239">Tooenable Azure AD 사용자가 toolog Veracode로 주문 하 고에 Veracode에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-239">In order tooenable Azure AD users toolog into Veracode, they must be provisioned into Veracode.</span></span> <span data-ttu-id="10bd4-240">Hello Veracode의 경우에서 프로 비전은 자동화 된 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-240">In hello case of Veracode, provisioning is an automated task.</span></span> <span data-ttu-id="10bd4-241">작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-241">There is no action item for you.</span></span> <span data-ttu-id="10bd4-242">사용자가 필요한 경우 hello 첫 번째 single sign on 시도 하는 동안 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-242">Users are automatically created if necessary during hello first single sign-on attempt.</span></span>

> [!NOTE]
> <span data-ttu-id="10bd4-243">다른 Veracode 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 Azure AD 사용자 계정을 Veracode tooprovision에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-243">You can use any other Veracode user account creation tools or APIs provided by Veracode tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="10bd4-244">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-244">Assign hello Azure AD test user</span></span>

<span data-ttu-id="10bd4-245">이 섹션에서는 tooVeracode 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooVeracode.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="10bd4-247">**tooassign Britta Simon tooVeracode hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="10bd4-247">**tooassign Britta Simon tooVeracode, perform hello following steps:**</span></span>

1. <span data-ttu-id="10bd4-248">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="10bd4-250">Hello 응용 프로그램 목록에서 선택 **Veracode**합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-250">In hello applications list, select **Veracode**.</span></span>

    ![hello 응용 프로그램 목록에서 hello Veracode 링크](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. <span data-ttu-id="10bd4-252">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="10bd4-254">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-254">Click **Add** button.</span></span> <span data-ttu-id="10bd4-255">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="10bd4-257">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="10bd4-258">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="10bd4-259">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="10bd4-260">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="10bd4-260">Test single sign-on</span></span>

<span data-ttu-id="10bd4-261">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="10bd4-262">Hello 액세스 패널에서에서 hello Veracode 타일을 클릭할 때 자동으로 로그온 tooyour Veracode 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-262">When you click hello Veracode tile in hello Access Panel, you should get automatically signed-on tooyour Veracode application.</span></span>
<span data-ttu-id="10bd4-263">액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="10bd4-263">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="10bd4-264">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="10bd4-264">Additional resources</span></span>

* [<span data-ttu-id="10bd4-265">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="10bd4-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="10bd4-266">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="10bd4-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png

