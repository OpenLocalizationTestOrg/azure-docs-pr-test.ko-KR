---
title: "자습서: Litmos와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Litmos 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: jeedes
ms.assetid: cfaae4bb-e8e5-41d1-ac88-8cc369653036
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 026fd10058760f2d63d185ef4aa9d7de3b82525e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-litmos"></a><span data-ttu-id="4e2b4-103">자습서: Litmos와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="4e2b4-103">Tutorial: Azure Active Directory integration with Litmos</span></span>

<span data-ttu-id="4e2b4-104">이 자습서에 설명 어떻게 toointegrate Litmos Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4e2b4-104">In this tutorial, you learn how toointegrate Litmos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4e2b4-105">다음 이점을 hello로 제공 Litmos Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="4e2b4-105">Integrating Litmos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4e2b4-106">액세스 tooLitmos을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-106">You can control in Azure AD who has access tooLitmos.</span></span>
- <span data-ttu-id="4e2b4-107">에 사용자가 tooautomatically get 로그온 tooLitmos (Single Sign-on)는 Azure AD 계정으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-107">You can enable your users tooautomatically get signed-on tooLitmos (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4e2b4-108">하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="4e2b4-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e2b4-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4e2b4-110">Prerequisites</span></span>

<span data-ttu-id="4e2b4-111">다음 항목 hello가 필요 tooconfigure Litmos와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-111">tooconfigure Azure AD integration with Litmos, you need hello following items:</span></span>

- <span data-ttu-id="4e2b4-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="4e2b4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4e2b4-113">Litmos Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="4e2b4-113">A Litmos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4e2b4-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4e2b4-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4e2b4-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4e2b4-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4e2b4-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="4e2b4-118">Scenario description</span></span>
<span data-ttu-id="4e2b4-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4e2b4-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4e2b4-121">Litmos는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="4e2b4-121">Adding Litmos from hello gallery</span></span>
2. <span data-ttu-id="4e2b4-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="4e2b4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-litmos-from-hello-gallery"></a><span data-ttu-id="4e2b4-123">Litmos는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="4e2b4-123">Adding Litmos from hello gallery</span></span>
<span data-ttu-id="4e2b4-124">tooconfigure hello와의 통합 Litmos Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Litmos tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-124">tooconfigure hello integration of Litmos into Azure AD, you need tooadd Litmos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4e2b4-125">**hello 갤러리에서 Litmos tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4e2b4-125">**tooadd Litmos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e2b4-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="4e2b4-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4e2b4-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="4e2b4-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="4e2b4-133">Hello 검색 상자에 입력 **Litmos**선택, **Litmos** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-133">In hello search box, type **Litmos**, select **Litmos** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Litmos hello 결과 목록에서](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4e2b4-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="4e2b4-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4e2b4-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 Litmos에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-136">In this section, you configure and test Azure AD single sign-on with Litmos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4e2b4-137">Single sign on toowork에 대 한 Azure AD는 tooknow Litmos에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Litmos is tooa user in Azure AD.</span></span> <span data-ttu-id="4e2b4-138">즉, Azure AD 사용자 및 Litmos에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-138">In other words, a link relationship between an Azure AD user and hello related user in Litmos needs toobe established.</span></span>

<span data-ttu-id="4e2b4-139">Litmos에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-139">In Litmos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4e2b4-140">tooconfigure 및 Litmos 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-140">tooconfigure and test Azure AD single sign-on with Litmos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4e2b4-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4e2b4-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4e2b4-143">**[Litmos 테스트 사용자 만들기](#create-a-litmos-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Litmos에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-143">**[Create a Litmos test user](#create-a-litmos-test-user)** - toohave a counterpart of Britta Simon in Litmos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4e2b4-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4e2b4-145">**[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4e2b4-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="4e2b4-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4e2b4-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Litmos 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Litmos application.</span></span>

<span data-ttu-id="4e2b4-148">**tooconfigure Azure AD single sign on, Litmos와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4e2b4-148">**tooconfigure Azure AD single sign-on with Litmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e2b4-149">Hello hello에 Azure 포털에서에서 **Litmos** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-149">In hello Azure portal, on hello **Litmos** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="4e2b4-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_samlbase.png)

3. <span data-ttu-id="4e2b4-153">Hello에 **Litmos 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-153">On hello **Litmos Domain and URLs** section, perform hello following steps:</span></span>

    ![Litmos 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_url.png)

    <span data-ttu-id="4e2b4-155">a.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-155">a.</span></span> <span data-ttu-id="4e2b4-156">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.litmos.com/account/Login`</span><span class="sxs-lookup"><span data-stu-id="4e2b4-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.litmos.com/account/Login`</span></span>

    <span data-ttu-id="4e2b4-157">b.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-157">b.</span></span> <span data-ttu-id="4e2b4-158">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.litmos.com/integration/samllogin`</span><span class="sxs-lookup"><span data-stu-id="4e2b4-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.litmos.com/integration/samllogin`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4e2b4-159">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-159">These values are not real.</span></span> <span data-ttu-id="4e2b4-160">자습서 또는 연락처의 뒷부분에 설명 된 hello 실제 식별자 및 회신 URL을으로 이러한 값을 업데이트 [Litmos 지원 팀](https://www.litmos.com/contact-us/) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-160">Update these values with hello actual Identifier and Reply URL, which are explained later in tutorial or contact [Litmos support team](https://www.litmos.com/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="4e2b4-161">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_certificate.png)

5. <span data-ttu-id="4e2b4-163">Hello 구성의 일부로 toocustomize hello 해야 **SAML 토큰 특성** Litmos 응용 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-163">As part of hello configuration, you need toocustomize hello **SAML Token Attributes** for your Litmos application.</span></span>

    ![특성 섹션](./media/active-directory-saas-litmos-tutorial/tutorial_attribute.png)
           
    | <span data-ttu-id="4e2b4-165">특성 이름</span><span class="sxs-lookup"><span data-stu-id="4e2b4-165">Attribute Name</span></span>   | <span data-ttu-id="4e2b4-166">특성 값</span><span class="sxs-lookup"><span data-stu-id="4e2b4-166">Attribute Value</span></span> |   
    | ---------------  | ----------------|
    | <span data-ttu-id="4e2b4-167">FirstName</span><span class="sxs-lookup"><span data-stu-id="4e2b4-167">FirstName</span></span> |<span data-ttu-id="4e2b4-168">user.givenname</span><span class="sxs-lookup"><span data-stu-id="4e2b4-168">user.givenname</span></span> |
    | <span data-ttu-id="4e2b4-169">LastName</span><span class="sxs-lookup"><span data-stu-id="4e2b4-169">LastName</span></span>  |<span data-ttu-id="4e2b4-170">user.surname</span><span class="sxs-lookup"><span data-stu-id="4e2b4-170">user.surname</span></span> |
    | <span data-ttu-id="4e2b4-171">Email</span><span class="sxs-lookup"><span data-stu-id="4e2b4-171">Email</span></span> |<span data-ttu-id="4e2b4-172">user.mail</span><span class="sxs-lookup"><span data-stu-id="4e2b4-172">user.mail</span></span> |

    <span data-ttu-id="4e2b4-173">a.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-173">a.</span></span> <span data-ttu-id="4e2b4-174">클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-174">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![특성 추가](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_04.png)

    ![특성 추가 대화 상자](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="4e2b4-177">b.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-177">b.</span></span> <span data-ttu-id="4e2b4-178">Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="4e2b4-179">c.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-179">c.</span></span> <span data-ttu-id="4e2b4-180">Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-180">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="4e2b4-181">d.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-181">d.</span></span> <span data-ttu-id="4e2b4-182">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-182">Click **Ok**.</span></span>     

6. <span data-ttu-id="4e2b4-183">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-183">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-litmos-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="4e2b4-185">다른 브라우저 창에서 관리자 권한으로 로그온 tooyour Litmos 회사 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-185">In a different browser window, sign-on tooyour Litmos company site as administrator.</span></span>

8. <span data-ttu-id="4e2b4-186">Hello 왼쪽에 hello 탐색 모음에서 **계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-186">In hello navigation bar on hello left side, click **Accounts**.</span></span>
   
    ![앱 쪽의 계정 섹션][22] 

9. <span data-ttu-id="4e2b4-188">Hello 클릭 **통합** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-188">Click hello **Integrations** tab.</span></span>
   
    ![통합 탭][23] 

10. <span data-ttu-id="4e2b4-190">Hello에 **통합** 탭, 너무 아래로 스크롤하여**3rd 파티 통합**, 클릭 하 고 **SAML 2.0** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-190">On hello **Integrations** tab, scroll down too**3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0 섹션][24] 

11. <span data-ttu-id="4e2b4-192">Hello 값에서 복사 **litmos에 대 한 SAML 끝점 hello:** hello에 붙여 넣습니다 **회신 URL** hello 텍스트 상자로 **Litmos 도메인 및 Url** Azure 포털에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-192">Copy hello value under **hello SAML endpoint for litmos is:** and paste it into hello **Reply URL** textbox in hello **Litmos Domain and URLs** section in Azure portal.</span></span> 
   
    ![SAML 끝점][26] 

12. <span data-ttu-id="4e2b4-194">사용자 **Litmos** 응용 프로그램을 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-194">In your **Litmos** application, perform hello following steps:</span></span>
    
     ![Litmos 응용 프로그램][25] 
     
     <span data-ttu-id="4e2b4-196">a.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-196">a.</span></span> <span data-ttu-id="4e2b4-197">**SAML 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-197">Click **Enable SAML**.</span></span>
    
     <span data-ttu-id="4e2b4-198">b.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-198">b.</span></span> <span data-ttu-id="4e2b4-199">콘텐츠를 클립보드에 복사 hello 메모장에서 e-64로 인코딩된 인증서를 열고 toohello 붙여 **SAML X.509 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-199">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **SAML X.509 Certificate** textbox.</span></span>
     
     <span data-ttu-id="4e2b4-200">c.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-200">c.</span></span> <span data-ttu-id="4e2b4-201">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-201">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="4e2b4-202">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="4e2b4-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4e2b4-203">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4e2b4-204">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4e2b4-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4e2b4-205">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="4e2b4-205">Create an Azure AD test user</span></span>

<span data-ttu-id="4e2b4-206">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="4e2b4-208">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4e2b4-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e2b4-209">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-litmos-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="4e2b4-211">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-litmos-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="4e2b4-213">tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello 추가 단추](./media/active-directory-saas-litmos-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="4e2b4-215">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello 사용자 대화 상자](./media/active-directory-saas-litmos-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4e2b4-217">a.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-217">a.</span></span> <span data-ttu-id="4e2b4-218">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4e2b4-219">b.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-219">b.</span></span> <span data-ttu-id="4e2b4-220">Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="4e2b4-221">c.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-221">c.</span></span> <span data-ttu-id="4e2b4-222">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="4e2b4-223">d.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-223">d.</span></span> <span data-ttu-id="4e2b4-224">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-224">Click **Create**.</span></span>
  
### <a name="create-a-litmos-test-user"></a><span data-ttu-id="4e2b4-225">Litmos 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="4e2b4-225">Create a Litmos test user</span></span>

<span data-ttu-id="4e2b4-226">hello이이 섹션의 목적은 toocreate Britta Simon Litmos에서 호출 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-226">hello objective of this section is toocreate a user called Britta Simon in Litmos.</span></span>  
<span data-ttu-id="4e2b4-227">hello Litmos 응용 프로그램 지원 Just in Time 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-227">hello Litmos application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="4e2b4-228">이 즉, 사용자 계정 하면 hello 액세스 패널을 사용 하는 시도 tooaccess hello 적용 하는 동안 필요한 경우 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-228">This means, a user account is automatically created if necessary during an attempt tooaccess hello application using hello Access Panel.</span></span>

<span data-ttu-id="4e2b4-229">**toocreate Britta Simon Litmos의 라는 사용자를 만들면 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4e2b4-229">**toocreate a user called Britta Simon in Litmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e2b4-230">다른 브라우저 창에서 관리자 권한으로 로그온 tooyour Litmos 회사 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-230">In a different browser window, sign-on tooyour Litmos company site as administrator.</span></span>

2. <span data-ttu-id="4e2b4-231">Hello 왼쪽에 hello 탐색 모음에서 **계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-231">In hello navigation bar on hello left side, click **Accounts**.</span></span>
   
    ![앱 쪽의 계정 섹션][22] 

3. <span data-ttu-id="4e2b4-233">Hello 클릭 **통합** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-233">Click hello **Integrations** tab.</span></span>
   
    ![통합 탭][23] 

4. <span data-ttu-id="4e2b4-235">Hello에 **통합** 탭, 너무 아래로 스크롤하여**3rd 파티 통합**, 클릭 하 고 **SAML 2.0** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-235">On hello **Integrations** tab, scroll down too**3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0][24] 
    
5. <span data-ttu-id="4e2b4-237">**Autogenerate Users**(사용자 자동 생성)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-237">Select **Autogenerate Users**</span></span>
   
    ![사용자 자동 생성][27] 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="4e2b4-239">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-239">Assign hello Azure AD test user</span></span>

<span data-ttu-id="4e2b4-240">이 섹션에서는 tooLitmos 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLitmos.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="4e2b4-242">**tooassign Britta Simon tooLitmos hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4e2b4-242">**tooassign Britta Simon tooLitmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e2b4-243">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="4e2b4-245">Hello 응용 프로그램 목록에서 선택 **Litmos**합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-245">In hello applications list, select **Litmos**.</span></span>

    ![hello 응용 프로그램 목록에서 hello Litmos 링크](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_app.png)  

3. <span data-ttu-id="4e2b4-247">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="4e2b4-249">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-249">Click **Add** button.</span></span> <span data-ttu-id="4e2b4-250">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="4e2b4-252">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4e2b4-253">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4e2b4-254">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4e2b4-255">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="4e2b4-255">Test single sign-on</span></span>

<span data-ttu-id="4e2b4-256">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-256">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="4e2b4-257">Hello Litmos hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour Litmos 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e2b4-257">When you click hello Litmos tile in hello Access Panel, you should get automatically signed-on tooyour Litmos application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4e2b4-258">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="4e2b4-258">Additional resources</span></span>

* [<span data-ttu-id="4e2b4-259">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="4e2b4-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4e2b4-260">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="4e2b4-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_04.png
[21]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_60.png
[22]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_61.png
[23]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_62.png
[24]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_63.png
[25]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_64.png
[26]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_65.png
[27]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_66.png

[100]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_203.png

