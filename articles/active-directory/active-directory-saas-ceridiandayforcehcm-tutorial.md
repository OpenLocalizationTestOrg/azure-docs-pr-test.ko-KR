---
title: "자습서: Ceridian Dayforce HCM과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Ceridian Dayforce HCM 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7adf1eb3-d063-45d6-96a8-fd53b329b3f3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 4d72f29b4e5e30ef8881806d789f6676fc541e2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a><span data-ttu-id="b41d4-103">자습서: Ceridian Dayforce HCM과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="b41d4-103">Tutorial: Azure Active Directory integration with Ceridian Dayforce HCM</span></span>

<span data-ttu-id="b41d4-104">이 자습서에 설명 어떻게 toointegrate Ceridian Dayforce HCM Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b41d4-104">In this tutorial, you learn how toointegrate Ceridian Dayforce HCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b41d4-105">다음 이점을 hello로 제공 Ceridian Dayforce HCM Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="b41d4-105">Integrating Ceridian Dayforce HCM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b41d4-106">액세스 tooCeridian Dayforce HCM 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-106">You can control in Azure AD who has access tooCeridian Dayforce HCM.</span></span>
- <span data-ttu-id="b41d4-107">Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooCeridian Dayforce HCM (Single Sign-on)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-107">You can enable your users tooautomatically get signed-on tooCeridian Dayforce HCM (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b41d4-108">하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="b41d4-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b41d4-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b41d4-110">Prerequisites</span></span>

<span data-ttu-id="b41d4-111">다음 항목 hello가 필요 tooconfigure Ceridian Dayforce HCM와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-111">tooconfigure Azure AD integration with Ceridian Dayforce HCM, you need hello following items:</span></span>

- <span data-ttu-id="b41d4-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="b41d4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b41d4-113">Ceridian Dayforce HCM Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="b41d4-113">A Ceridian Dayforce HCM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b41d4-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b41d4-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b41d4-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b41d4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b41d4-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b41d4-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="b41d4-118">Scenario description</span></span>
<span data-ttu-id="b41d4-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b41d4-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b41d4-121">Ceridian Dayforce HCM hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="b41d4-121">Adding Ceridian Dayforce HCM from hello gallery</span></span>
2. <span data-ttu-id="b41d4-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b41d4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ceridian-dayforce-hcm-from-hello-gallery"></a><span data-ttu-id="b41d4-123">Ceridian Dayforce HCM hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="b41d4-123">Adding Ceridian Dayforce HCM from hello gallery</span></span>
<span data-ttu-id="b41d4-124">tooconfigure hello와의 통합 Ceridian Dayforce HCM Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Ceridian Dayforce HCM tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-124">tooconfigure hello integration of Ceridian Dayforce HCM into Azure AD, you need tooadd Ceridian Dayforce HCM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b41d4-125">**tooadd hello 갤러리에서 Ceridian Dayforce HCM hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b41d4-125">**tooadd Ceridian Dayforce HCM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b41d4-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="b41d4-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b41d4-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="b41d4-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="b41d4-133">Hello 검색 상자에 입력 **Ceridian Dayforce HCM**선택, **Ceridian Dayforce HCM** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-133">In hello search box, type **Ceridian Dayforce HCM**, select **Ceridian Dayforce HCM** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Ceridian Dayforce HCM hello 결과 목록에서](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b41d4-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b41d4-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b41d4-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Ceridian Dayforce HCM에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-136">In this section, you configure and test Azure AD single sign-on with Ceridian Dayforce HCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b41d4-137">Single sign on toowork에 대 한 Azure AD는 tooknow Ceridian Dayforce HCM에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Ceridian Dayforce HCM is tooa user in Azure AD.</span></span> <span data-ttu-id="b41d4-138">즉, Azure AD 사용자 및 Ceridian Dayforce HCM에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-138">In other words, a link relationship between an Azure AD user and hello related user in Ceridian Dayforce HCM needs toobe established.</span></span>

<span data-ttu-id="b41d4-139">Ceridian Dayforce HCM에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-139">In Ceridian Dayforce HCM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b41d4-140">tooconfigure 및 Ceridian Dayforce HCM를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-140">tooconfigure and test Azure AD single sign-on with Ceridian Dayforce HCM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b41d4-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b41d4-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b41d4-143">**[Ceridian Dayforce HCM 테스트 사용자 만들기](#create-a-ceridian-dayforce-hcm-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Ceridian Dayforce HCM에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-143">**[Create a Ceridian Dayforce HCM test user](#create-a-ceridian-dayforce-hcm-test-user)** - toohave a counterpart of Britta Simon in Ceridian Dayforce HCM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b41d4-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b41d4-145">**[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="b41d4-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b41d4-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="b41d4-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b41d4-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Ceridian Dayforce HCM 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Ceridian Dayforce HCM application.</span></span>

<span data-ttu-id="b41d4-148">**Ceridian Dayforce HCM와 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b41d4-148">**tooconfigure Azure AD single sign-on with Ceridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="b41d4-149">Hello hello에 Azure 포털에서에서 **Ceridian Dayforce HCM** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-149">In hello Azure portal, on hello **Ceridian Dayforce HCM** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="b41d4-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_samlbase.png)

3. <span data-ttu-id="b41d4-153">Hello에 **Ceridian Dayforce HCM 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-153">On hello **Ceridian Dayforce HCM Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_url.png)
    
    <span data-ttu-id="b41d4-155">a.</span><span class="sxs-lookup"><span data-stu-id="b41d4-155">a.</span></span> <span data-ttu-id="b41d4-156">Hello에 **로그온 URL** 텍스트 상자에 사용자에 대 한 toosign tooyour Ceridian Dayforce HCM 응용 프로그램에서 사용 하는 hello URL 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-156">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Ceridian Dayforce HCM application.</span></span>
    
    | <span data-ttu-id="b41d4-157">Environment</span><span class="sxs-lookup"><span data-stu-id="b41d4-157">Environment</span></span> | <span data-ttu-id="b41d4-158">URL</span><span class="sxs-lookup"><span data-stu-id="b41d4-158">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="b41d4-159">프로덕션</span><span class="sxs-lookup"><span data-stu-id="b41d4-159">For production</span></span> | `https://sso.dayforcehcm.com/<DayforcehcmNamespace>` |
    | <span data-ttu-id="b41d4-160">테스트</span><span class="sxs-lookup"><span data-stu-id="b41d4-160">For test</span></span> | `https://ssotest.dayforcehcm.com/<DayforcehcmNamespace>` |
    
    <span data-ttu-id="b41d4-161">b.</span><span class="sxs-lookup"><span data-stu-id="b41d4-161">b.</span></span> <span data-ttu-id="b41d4-162">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:</span><span class="sxs-lookup"><span data-stu-id="b41d4-162">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    
    | <span data-ttu-id="b41d4-163">Environment</span><span class="sxs-lookup"><span data-stu-id="b41d4-163">Environment</span></span> | <span data-ttu-id="b41d4-164">URL</span><span class="sxs-lookup"><span data-stu-id="b41d4-164">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="b41d4-165">프로덕션</span><span class="sxs-lookup"><span data-stu-id="b41d4-165">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp` |
    | <span data-ttu-id="b41d4-166">테스트</span><span class="sxs-lookup"><span data-stu-id="b41d4-166">For test</span></span> | `https://fs-test.dayforcehcm.com/sp` |
    
    <span data-ttu-id="b41d4-167">c.</span><span class="sxs-lookup"><span data-stu-id="b41d4-167">c.</span></span> <span data-ttu-id="b41d4-168">Hello에 **회신 URL** textbox, Azure AD toopost hello 응답에서 사용 하는 hello URL 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-168">In hello **Reply URL** textbox, type hello URL used by Azure AD toopost hello response.</span></span>
    
    | <span data-ttu-id="b41d4-169">Environment</span><span class="sxs-lookup"><span data-stu-id="b41d4-169">Environment</span></span> | <span data-ttu-id="b41d4-170">URL</span><span class="sxs-lookup"><span data-stu-id="b41d4-170">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="b41d4-171">프로덕션</span><span class="sxs-lookup"><span data-stu-id="b41d4-171">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2` |
    | <span data-ttu-id="b41d4-172">테스트</span><span class="sxs-lookup"><span data-stu-id="b41d4-172">For test</span></span> | `https://fs-test.dayforcehcm.com/sp/ACS.saml2` |
    
    > [!NOTE] 
    > <span data-ttu-id="b41d4-173">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-173">These values are not real.</span></span> <span data-ttu-id="b41d4-174">이러한 항목을 업데이트 식별자, 회신 URL 및 로그온 URL 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-174">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="b41d4-175">연락처 [Ceridian Dayforce HCM 클라이언트 지원 팀](https://www.ceridian.com/contact-us/index.html) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-175">Contact [Ceridian Dayforce HCM Client support team](https://www.ceridian.com/contact-us/index.html) tooget these values.</span></span>

4. <span data-ttu-id="b41d4-176">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-176">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_certificate.png) 

5. <span data-ttu-id="b41d4-178">Ceridian Dayforce HCM 응용 프로그램에 특정 형식의 hello SAML 어설션 합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-178">Your Ceridian Dayforce HCM application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="b41d4-179">작업할 [Ceridian Dayforce HCM 지원 팀](https://www.ceridian.com/contact-us/index.html) 첫 번째 tooidentify hello 올바른 사용자 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-179">Work with [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) first tooidentify hello correct user identifier.</span></span> <span data-ttu-id="b41d4-180">Microsoft hello를 사용 하는 것이 좋습니다. **"name"** 사용자 식별자로는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-180">Microsoft recommends using hello **"name"** attribute as user identifier.</span></span> <span data-ttu-id="b41d4-181">Hello에서 이러한 특성의 hello 값을 관리할 수 있습니다 **사용자 특성** 응용 프로그램 통합 페이지에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="b41d4-181">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="b41d4-182">다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-182">hello following screenshot shows an example for this.</span></span>  

    ![Single Sign-on 구성](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

6. <span data-ttu-id="b41d4-184">Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 위의 hello 이미지에 나와 있는 것 처럼 SAML 토큰 특성을 구성 하 고 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-184">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="b41d4-185">특성 이름</span><span class="sxs-lookup"><span data-stu-id="b41d4-185">Attribute Name</span></span>  | <span data-ttu-id="b41d4-186">특성 값</span><span class="sxs-lookup"><span data-stu-id="b41d4-186">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="b41d4-187">name</span><span class="sxs-lookup"><span data-stu-id="b41d4-187">name</span></span>  | <span data-ttu-id="b41d4-188">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="b41d4-188">user.extensionattribute2</span></span> |    

    <span data-ttu-id="b41d4-189">a.</span><span class="sxs-lookup"><span data-stu-id="b41d4-189">a.</span></span> <span data-ttu-id="b41d4-190">클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="b41d4-190">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="b41d4-193">b.</span><span class="sxs-lookup"><span data-stu-id="b41d4-193">b.</span></span> <span data-ttu-id="b41d4-194">Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-194">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="b41d4-195">c.</span><span class="sxs-lookup"><span data-stu-id="b41d4-195">c.</span></span> <span data-ttu-id="b41d4-196">Hello에 **값** 목록, 선택 hello 사용자 특성을 toouse 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-196">In hello **Value** list, select hello user attribute you want toouse for your implementation.</span></span>
    <span data-ttu-id="b41d4-197">Toouse hello 고유한 사용자 식별자로 EmployeeID를 원하는 경우 ExtensionAttribute2 hello에 hello 특성 값을 저장 한 다음 선택 예를 들어 **user.extensionattribute2**합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-197">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select **user.extensionattribute2**.</span></span>
    
    <span data-ttu-id="b41d4-198">d.</span><span class="sxs-lookup"><span data-stu-id="b41d4-198">d.</span></span> <span data-ttu-id="b41d4-199">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-199">Click **Ok**.</span></span>

7. <span data-ttu-id="b41d4-200">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-200">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="b41d4-202">Hello에 **Ceridian Dayforce HCM 구성** 섹션에서 클릭 **Ceridian Dayforce HCM 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="b41d4-202">On hello **Ceridian Dayforce HCM Configuration** section, click **Configure Ceridian Dayforce HCM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b41d4-203">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="b41d4-203">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Ceridian Dayforce HCM 구성](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_configure.png) 

9. <span data-ttu-id="b41d4-205">tooconfigure single sign on에서 **Ceridian Dayforce HCM** toosend hello 다운로드 해야 쪽에서는 **메타 데이터 XML** 및 **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** 너무[Ceridian Dayforce HCM 지원 팀](https://www.ceridian.com/contact-us/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-205">tooconfigure single sign-on on **Ceridian Dayforce HCM** side, you need toosend hello downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html).</span></span>

> [!TIP]
> <span data-ttu-id="b41d4-206">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="b41d4-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b41d4-207">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="b41d4-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b41d4-208">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b41d4-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b41d4-209">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b41d4-209">Create an Azure AD test user</span></span>

<span data-ttu-id="b41d4-210">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="b41d4-212">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b41d4-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b41d4-213">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-213">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b41d4-215">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-215">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b41d4-217">tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="b41d4-217">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello 추가 단추](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b41d4-219">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-219">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello 사용자 대화 상자](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b41d4-221">a.</span><span class="sxs-lookup"><span data-stu-id="b41d4-221">a.</span></span> <span data-ttu-id="b41d4-222">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-222">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b41d4-223">b.</span><span class="sxs-lookup"><span data-stu-id="b41d4-223">b.</span></span> <span data-ttu-id="b41d4-224">Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-224">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="b41d4-225">c.</span><span class="sxs-lookup"><span data-stu-id="b41d4-225">c.</span></span> <span data-ttu-id="b41d4-226">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-226">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="b41d4-227">d.</span><span class="sxs-lookup"><span data-stu-id="b41d4-227">d.</span></span> <span data-ttu-id="b41d4-228">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-228">Click **Create**.</span></span>
 
### <a name="create-a-ceridian-dayforce-hcm-test-user"></a><span data-ttu-id="b41d4-229">Ceridian Dayforce HCM 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b41d4-229">Create a Ceridian Dayforce HCM test user</span></span>

<span data-ttu-id="b41d4-230">hello이이 섹션의 목적은 toocreate Britta Simon Ceridian Dayforce HCM에서 호출 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-230">hello objective of this section is toocreate a user called Britta Simon in Ceridian Dayforce HCM.</span></span> <span data-ttu-id="b41d4-231">Hello 작업할 [Ceridian Dayforce HCM 지원 팀](https://www.ceridian.com/contact-us/index.html) tooget 사용자 hello Ceridian Dayforce HCM 응용 프로그램에에서 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-231">Work with hello [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) tooget users added in hello Ceridian Dayforce HCM application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b41d4-232">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b41d4-233">이 섹션에서는 액세스 tooCeridian Dayforce HCM 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCeridian Dayforce HCM.</span></span>

![사용자 할당][200] 

<span data-ttu-id="b41d4-235">**tooassign Britta Simon tooCeridian Dayforce HCM hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b41d4-235">**tooassign Britta Simon tooCeridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="b41d4-236">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="b41d4-238">Hello 응용 프로그램 목록에서 선택 **Ceridian Dayforce HCM**합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-238">In hello applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png) 

3. <span data-ttu-id="b41d4-240">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="b41d4-242">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-242">Click **Add** button.</span></span> <span data-ttu-id="b41d4-243">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="b41d4-245">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b41d4-246">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b41d4-247">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-247">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b41d4-248">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-248">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b41d4-249">이 섹션에서는 액세스 tooCeridian Dayforce HCM 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-249">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCeridian Dayforce HCM.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="b41d4-251">**tooassign Britta Simon tooCeridian Dayforce HCM hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b41d4-251">**tooassign Britta Simon tooCeridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="b41d4-252">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-252">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="b41d4-254">Hello 응용 프로그램 목록에서 선택 **Ceridian Dayforce HCM**합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-254">In hello applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![hello 응용 프로그램 목록에서 hello Ceridian Dayforce HCM 링크](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png)  

3. <span data-ttu-id="b41d4-256">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-256">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="b41d4-258">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-258">Click **Add** button.</span></span> <span data-ttu-id="b41d4-259">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="b41d4-261">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-261">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b41d4-262">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b41d4-263">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b41d4-264">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="b41d4-264">Test single sign-on</span></span>

<span data-ttu-id="b41d4-265">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-265">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="b41d4-266">Hello 액세스 패널에서에서 hello Ceridian Dayforce HCM 타일을 클릭할 때 자동으로 로그온 tooyour Ceridian Dayforce HCM 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b41d4-266">When you click hello Ceridian Dayforce HCM tile in hello Access Panel, you should get automatically signed-on tooyour Ceridian Dayforce HCM application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b41d4-267">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b41d4-267">Additional resources</span></span>

* [<span data-ttu-id="b41d4-268">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="b41d4-268">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b41d4-269">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b41d4-269">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_203.png

