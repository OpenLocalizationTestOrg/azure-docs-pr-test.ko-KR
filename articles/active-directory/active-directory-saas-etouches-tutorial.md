---
title: "etouches와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 etouches 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 76cccaa8-859c-4c16-9d1d-8a6496fc7520
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 5f3ff7550e660b0fc52612140ca55061504b5edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-etouches"></a><span data-ttu-id="0edce-103">자습서: etouches와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="0edce-103">Tutorial: Azure Active Directory integration with etouches</span></span>

<span data-ttu-id="0edce-104">이 자습서에 설명 어떻게 toointegrate etouches Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0edce-104">In this tutorial, you learn how toointegrate etouches with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0edce-105">다음 이점을 hello로 제공 etouches Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="0edce-105">Integrating etouches with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0edce-106">액세스 tooetouches을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-106">You can control in Azure AD who has access tooetouches</span></span>
- <span data-ttu-id="0edce-107">프로그램 사용자 tooautomatically get 로그온 tooetouches (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-107">You can enable your users tooautomatically get signed-on tooetouches (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0edce-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0edce-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0edce-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0edce-110">Prerequisites</span></span>

<span data-ttu-id="0edce-111">다음 항목 hello가 필요 tooconfigure etouches와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-111">tooconfigure Azure AD integration with etouches, you need hello following items:</span></span>

- <span data-ttu-id="0edce-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="0edce-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0edce-113">etouches Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="0edce-113">An etouches single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0edce-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0edce-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0edce-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="0edce-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0edce-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0edce-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="0edce-118">Scenario description</span></span>
<span data-ttu-id="0edce-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0edce-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0edce-121">Etouches hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="0edce-121">Adding etouches from hello gallery</span></span>
2. <span data-ttu-id="0edce-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="0edce-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-etouches-from-hello-gallery"></a><span data-ttu-id="0edce-123">Etouches hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="0edce-123">Adding etouches from hello gallery</span></span>
<span data-ttu-id="0edce-124">tooconfigure hello와의 통합 etouches Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 tooadd etouches가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-124">tooconfigure hello integration of etouches into Azure AD, you need tooadd etouches from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0edce-125">**hello 갤러리에서 tooadd etouches hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0edce-125">**tooadd etouches from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0edce-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="0edce-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0edce-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="0edce-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="0edce-133">Hello 검색 상자에 입력 **etouches**선택, **etouches** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-133">In hello search box, type **etouches**, select **etouches** from result panel then click **Add** button tooadd hello application.</span></span>

    ![etouches hello 결과 목록에서](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0edce-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="0edce-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="0edce-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 etouches에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-136">In this section, you configure and test Azure AD single sign-on with etouches based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0edce-137">Single sign on toowork에 대 한 Azure AD는 tooknow etouches에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in etouches is tooa user in Azure AD.</span></span> <span data-ttu-id="0edce-138">즉, Azure AD 사용자 및 etouches에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-138">In other words, a link relationship between an Azure AD user and hello related user in etouches needs toobe established.</span></span>

<span data-ttu-id="0edce-139">Etouches에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-139">In etouches, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0edce-140">tooconfigure 및 etouches 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-140">tooconfigure and test Azure AD single sign-on with etouches, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0edce-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0edce-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0edce-143">**[Etouches 테스트 사용자 만들기](#create-an-etouches-test-user)**  -toohave에서 사용자의 연결 된 Azure AD toohello 표현인 etouches Britta Simon 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-143">**[Create an etouches test user](#create-an-etouches-test-user)** - toohave a counterpart of Britta Simon in etouches that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0edce-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0edce-145">**[Single Sign-on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="0edce-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0edce-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="0edce-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0edce-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 etouches 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your etouches application.</span></span>

<span data-ttu-id="0edce-148">**tooconfigure Azure AD single sign on, etouches와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0edce-148">**tooconfigure Azure AD single sign-on with etouches, perform hello following steps:**</span></span>

1. <span data-ttu-id="0edce-149">Hello hello에 Azure 포털에서에서 **etouches** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-149">In hello Azure portal, on hello **etouches** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="0edce-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_samlbase.png)

3. <span data-ttu-id="0edce-153">Hello에 **도메인 및 Url etouches** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-153">On hello **etouches Domain and URLs** section, perform hello following steps:</span></span>

    ![etouches 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_url.png)

    <span data-ttu-id="0edce-155">a.</span><span class="sxs-lookup"><span data-stu-id="0edce-155">a.</span></span> <span data-ttu-id="0edce-156">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span><span class="sxs-lookup"><span data-stu-id="0edce-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span></span>

    <span data-ttu-id="0edce-157">b.</span><span class="sxs-lookup"><span data-stu-id="0edce-157">b.</span></span> <span data-ttu-id="0edce-158">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://www.eiseverywhere.com/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="0edce-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.eiseverywhere.com/<instance name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0edce-159">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-159">These values are not real.</span></span> <span data-ttu-id="0edce-160">실제 hello로 hello 값을 업데이트 하면 로그인 URL과 식별자 hello 자습서의 뒷부분에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-160">You update hello value with hello actual Sign on URL and Identifier, which is explained later in hello tutorial.</span></span>
    > 

4. <span data-ttu-id="0edce-161">etouches 응용 프로그램에는 특정 형식의 hello SAML 어설션 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-161">etouches application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="0edce-162">이 응용 프로그램에 대 한 클레임을 따라 hello를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-162">Configure hello following claims for this application.</span></span> <span data-ttu-id="0edce-163">Hello에서 이러한 특성의 hello 값을 관리할 수 있습니다 **사용자 특성** hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-163">You can manage hello values of these attributes from hello **User Attribute** of hello application.</span></span> <span data-ttu-id="0edce-164">다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-164">hello following screenshot shows an example for this.</span></span> 

    ![사용자 특성](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_attribute.png) 

5. <span data-ttu-id="0edce-166">Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 hello 이미지에 나와 있는 것 처럼 SAML 토큰 특성을 구성 하 고 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-166">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="0edce-167">특성 이름</span><span class="sxs-lookup"><span data-stu-id="0edce-167">Attribute Name</span></span> | <span data-ttu-id="0edce-168">특성 값</span><span class="sxs-lookup"><span data-stu-id="0edce-168">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="0edce-169">Email</span><span class="sxs-lookup"><span data-stu-id="0edce-169">Email</span></span> | <span data-ttu-id="0edce-170">user.mail</span><span class="sxs-lookup"><span data-stu-id="0edce-170">user.mail</span></span> |    
    
    <span data-ttu-id="0edce-171">a.</span><span class="sxs-lookup"><span data-stu-id="0edce-171">a.</span></span> <span data-ttu-id="0edce-172">클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="0edce-172">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![특성 추가](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_04.png)

    ![특성 추가 대화 상자](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="0edce-175">b.</span><span class="sxs-lookup"><span data-stu-id="0edce-175">b.</span></span> <span data-ttu-id="0edce-176">Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-176">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="0edce-177">c.</span><span class="sxs-lookup"><span data-stu-id="0edce-177">c.</span></span> <span data-ttu-id="0edce-178">Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-178">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="0edce-179">d.</span><span class="sxs-lookup"><span data-stu-id="0edce-179">d.</span></span> <span data-ttu-id="0edce-180">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-180">Click **Ok**.</span></span> 

6. <span data-ttu-id="0edce-181">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-181">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_certificate.png) 

7. <span data-ttu-id="0edce-183">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-183">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-etouches-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="0edce-185">tooget SSO 응용 프로그램에 대해 구성 된 hello hello etouches 응용 프로그램의 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-185">tooget SSO configured for your application, perform hello following steps in hello etouches application:</span></span> 

    ![etouches 구성](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_06.png) 

    <span data-ttu-id="0edce-187">a.</span><span class="sxs-lookup"><span data-stu-id="0edce-187">a.</span></span> <span data-ttu-id="0edce-188">로그인 너무**etouches** hello 관리 권한을 사용 하 여 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-188">Login too**etouches** application using hello Admin rights.</span></span>
   
    <span data-ttu-id="0edce-189">b.</span><span class="sxs-lookup"><span data-stu-id="0edce-189">b.</span></span> <span data-ttu-id="0edce-190">Toohello 이동 **SAML** 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-190">Go toohello **SAML** Configuration.</span></span>

    <span data-ttu-id="0edce-191">c.</span><span class="sxs-lookup"><span data-stu-id="0edce-191">c.</span></span> <span data-ttu-id="0edce-192">Hello에 **일반 설정** 섹션 메모장에서 콘텐츠를 복사 hello Azure 포털에서 다운로드 한 인증서를 열고 마우스 hello IDP 메타 데이터의 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-192">In hello **General Settings** section, open your downloaded certificate from Azure portal in notepad, copy hello content, and then paste it into hello IDP metadata textbox.</span></span> 

    <span data-ttu-id="0edce-193">d.</span><span class="sxs-lookup"><span data-stu-id="0edce-193">d.</span></span> <span data-ttu-id="0edce-194">Hello 클릭 **저장 및 유지** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-194">Click on hello **Save & Stay** button.</span></span>
  
    <span data-ttu-id="0edce-195">e.</span><span class="sxs-lookup"><span data-stu-id="0edce-195">e.</span></span> <span data-ttu-id="0edce-196">Hello 클릭 **업데이트 메타 데이터** hello SAML 메타 데이터 섹션에에서는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-196">Click on hello **Update Metadata** button in hello SAML Metadata section.</span></span> 

    <span data-ttu-id="0edce-197">f.</span><span class="sxs-lookup"><span data-stu-id="0edce-197">f.</span></span> <span data-ttu-id="0edce-198">이 페이지 hello 열리고 SSO를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-198">This opens hello page and perform SSO.</span></span> <span data-ttu-id="0edce-199">한 번 hello SSO 작동 hello username를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-199">Once hello SSO is working then you can set up hello username.</span></span>

    <span data-ttu-id="0edce-200">g.</span><span class="sxs-lookup"><span data-stu-id="0edce-200">g.</span></span> <span data-ttu-id="0edce-201">Hello 사용자 이름 필드에서 선택 hello **emailaddress** hello 이미지 아래에 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-201">In hello Username field, select hello **emailaddress** as shown in hello image below.</span></span> 

    <span data-ttu-id="0edce-202">h.</span><span class="sxs-lookup"><span data-stu-id="0edce-202">h.</span></span> <span data-ttu-id="0edce-203">복사 hello **엔터티 ID가 SP** 값 및 hello에 붙여 **식별자** 텍스트 상자에 있는 **etouches 도메인 및 Url** Azure 포털에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="0edce-203">Copy hello **SP entity ID** value and paste it into hello **Identifier**  textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="0edce-204">i.</span><span class="sxs-lookup"><span data-stu-id="0edce-204">i.</span></span> <span data-ttu-id="0edce-205">복사 hello **SSO URL / ACS** 값 및 hello에 붙여 **로그온 URL** 텍스트 상자에 있는 **도메인 및 Url etouches** Azure 포털에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="0edce-205">Copy hello **SSO URL / ACS** value and paste it into hello **Sign on URL** textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>
   
> [!TIP]
> <span data-ttu-id="0edce-206">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="0edce-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0edce-207">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="0edce-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0edce-208">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0edce-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0edce-209">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="0edce-209">Create an Azure AD test user</span></span>
<span data-ttu-id="0edce-210">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="0edce-212">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0edce-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0edce-213">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-213">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-etouches-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0edce-215">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-215">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-etouches-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0edce-217">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-217">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![hello 추가 단추](./media/active-directory-saas-etouches-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0edce-219">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-219">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![hello 사용자 대화 상자](./media/active-directory-saas-etouches-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0edce-221">a.</span><span class="sxs-lookup"><span data-stu-id="0edce-221">a.</span></span> <span data-ttu-id="0edce-222">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-222">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0edce-223">b.</span><span class="sxs-lookup"><span data-stu-id="0edce-223">b.</span></span> <span data-ttu-id="0edce-224">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-224">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0edce-225">c.</span><span class="sxs-lookup"><span data-stu-id="0edce-225">c.</span></span> <span data-ttu-id="0edce-226">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-226">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0edce-227">d.</span><span class="sxs-lookup"><span data-stu-id="0edce-227">d.</span></span> <span data-ttu-id="0edce-228">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-228">Click **Create**.</span></span>
 
### <a name="create-an-etouches-test-user"></a><span data-ttu-id="0edce-229">etouches 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="0edce-229">Create an etouches test user</span></span>

<span data-ttu-id="0edce-230">이 섹션에서는 etouches에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-230">In this section, you create a user called Britta Simon in etouches.</span></span> <span data-ttu-id="0edce-231">작업할 [etouches 클라이언트 지원 팀](https://www.etouches.com/event-software/support/customer-support/) hello etouches 플랫폼의 tooadd hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-231">Work with [etouches Client support team](https://www.etouches.com/event-software/support/customer-support/) tooadd hello users in hello etouches platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="0edce-232">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-232">Assign hello Azure AD test user</span></span>

<span data-ttu-id="0edce-233">이 섹션에서는 tooetouches 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooetouches.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="0edce-235">**tooassign Britta Simon tooetouches hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0edce-235">**tooassign Britta Simon tooetouches, perform hello following steps:**</span></span>

1. <span data-ttu-id="0edce-236">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="0edce-238">Hello 응용 프로그램 목록에서 선택 **etouches**합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-238">In hello applications list, select **etouches**.</span></span>

    ![hello 응용 프로그램 목록에서 hello etouches 링크](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_app.png) 

3. <span data-ttu-id="0edce-240">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202] 

4. <span data-ttu-id="0edce-242">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-242">Click **Add** button.</span></span> <span data-ttu-id="0edce-243">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="0edce-245">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0edce-246">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0edce-247">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0edce-248">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="0edce-248">Test single sign-on</span></span>


<span data-ttu-id="0edce-249">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-249">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0edce-250">Hello etouches hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour etouches 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0edce-250">When you click hello etouches tile in hello Access Panel, you should get automatically signed-on tooyour etouches application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0edce-251">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="0edce-251">Additional resources</span></span>

* [<span data-ttu-id="0edce-252">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="0edce-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0edce-253">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="0edce-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_203.png

