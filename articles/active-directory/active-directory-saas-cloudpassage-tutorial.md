---
title: "자습서: CloudPassage와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 CloudPassage 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfe1f14e-74e4-4680-ac9e-f7355e1c94cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 32fb007b90f071626c9b40fb5afc341dd3c1ae99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloudpassage"></a><span data-ttu-id="1dce1-103">자습서: CloudPassage와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="1dce1-103">Tutorial: Azure Active Directory integration with CloudPassage</span></span>

<span data-ttu-id="1dce1-104">이 자습서에 설명 어떻게 toointegrate CloudPassage Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1dce1-104">In this tutorial, you learn how toointegrate CloudPassage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1dce1-105">다음 이점을 hello로 제공 CloudPassage Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="1dce1-105">Integrating CloudPassage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1dce1-106">액세스 tooCloudPassage을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-106">You can control in Azure AD who has access tooCloudPassage</span></span>
- <span data-ttu-id="1dce1-107">프로그램 사용자 tooautomatically get 로그온 tooCloudPassage (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-107">You can enable your users tooautomatically get signed-on tooCloudPassage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1dce1-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1dce1-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1dce1-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1dce1-110">Prerequisites</span></span>

<span data-ttu-id="1dce1-111">다음 항목 hello가 필요 tooconfigure CloudPassage와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-111">tooconfigure Azure AD integration with CloudPassage, you need hello following items:</span></span>

- <span data-ttu-id="1dce1-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="1dce1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1dce1-113">CloudPassage Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="1dce1-113">A CloudPassage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1dce1-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1dce1-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1dce1-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="1dce1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1dce1-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1dce1-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="1dce1-118">Scenario description</span></span>
<span data-ttu-id="1dce1-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1dce1-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1dce1-121">CloudPassage는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="1dce1-121">Adding CloudPassage from hello gallery</span></span>
2. <span data-ttu-id="1dce1-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1dce1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloudpassage-from-hello-gallery"></a><span data-ttu-id="1dce1-123">CloudPassage는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="1dce1-123">Adding CloudPassage from hello gallery</span></span>
<span data-ttu-id="1dce1-124">tooconfigure hello와의 통합 CloudPassage Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 CloudPassage tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-124">tooconfigure hello integration of CloudPassage into Azure AD, you need tooadd CloudPassage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1dce1-125">**hello 갤러리에서 CloudPassage tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1dce1-125">**tooadd CloudPassage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1dce1-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1dce1-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1dce1-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="1dce1-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="1dce1-133">Hello 검색 상자에 입력 **CloudPassage**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-133">In hello search box, type **CloudPassage**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_search.png)

5. <span data-ttu-id="1dce1-135">Hello 결과 패널에서 선택 **CloudPassage**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-135">In hello results panel, select **CloudPassage**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1dce1-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1dce1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1dce1-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 CloudPassage에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-138">In this section, you configure and test Azure AD single sign-on with CloudPassage based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1dce1-139">Single sign on toowork에 대 한 Azure AD는 tooknow CloudPassage에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in CloudPassage is tooa user in Azure AD.</span></span> <span data-ttu-id="1dce1-140">즉, Azure AD 사용자 및 CloudPassage에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-140">In other words, a link relationship between an Azure AD user and hello related user in CloudPassage needs toobe established.</span></span>

<span data-ttu-id="1dce1-141">CloudPassage에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-141">In CloudPassage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1dce1-142">tooconfigure 및 CloudPassage 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-142">tooconfigure and test Azure AD single sign-on with CloudPassage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1dce1-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1dce1-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1dce1-145">**[CloudPassage 테스트 사용자 만들기](#creating-a-cloudpassage-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 CloudPassage에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-145">**[Creating a CloudPassage test user](#creating-a-cloudpassage-test-user)** - toohave a counterpart of Britta Simon in CloudPassage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1dce1-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1dce1-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="1dce1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1dce1-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="1dce1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1dce1-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 CloudPassage 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your CloudPassage application.</span></span>

<span data-ttu-id="1dce1-150">**tooconfigure Azure AD single sign on, CloudPassage와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1dce1-150">**tooconfigure Azure AD single sign-on with CloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="1dce1-151">Hello hello에 Azure 포털에서에서 **CloudPassage** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-151">In hello Azure portal, on hello **CloudPassage** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="1dce1-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_samlbase.png)

3. <span data-ttu-id="1dce1-155">Hello에 **CloudPassage 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-155">On hello **CloudPassage Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_url.png)

    <span data-ttu-id="1dce1-157">a.</span><span class="sxs-lookup"><span data-stu-id="1dce1-157">a.</span></span> <span data-ttu-id="1dce1-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://portal.cloudpassage.com/saml/init/accountid`</span><span class="sxs-lookup"><span data-stu-id="1dce1-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://portal.cloudpassage.com/saml/init/accountid`</span></span>

    <span data-ttu-id="1dce1-159">b.</span><span class="sxs-lookup"><span data-stu-id="1dce1-159">b.</span></span> <span data-ttu-id="1dce1-160">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL: `https://portal.cloudpassage.com/saml/consume/accountid`합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://portal.cloudpassage.com/saml/consume/accountid`.</span></span> <span data-ttu-id="1dce1-161">클릭 하 여이 특성에 대 한 사용자가 값을 가져올 수 있습니다 **SSO 설치 설명서** hello에 **Single Sign on 설정** CloudPassage 포털의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-161">You can get your value for this attribute by clicking **SSO Setup documentation** in hello **Single Sign-on Settings** section of your CloudPassage portal.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_05.png)
     
    > [!NOTE] 
    > <span data-ttu-id="1dce1-163">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-163">These values are not real.</span></span> <span data-ttu-id="1dce1-164">로그온 URL 및 hello 실제 회신 URL을 사용 하 여 이러한 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-164">Update these values with hello actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="1dce1-165">연락처 [CloudPassage 클라이언트 지원 팀](https://www.cloudpassage.com/company/contact/) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-165">Contact [CloudPassage Client support team](https://www.cloudpassage.com/company/contact/) tooget these values.</span></span> 

4. <span data-ttu-id="1dce1-166">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_certificate.png) 

5. <span data-ttu-id="1dce1-168">CloudPassage 응용 프로그램의 구성을 수행 해야 하면 tooadd 사용자 지정 특성 매핑을 tooyour SAML 토큰 특성을 특정 형식에서 hello SAML 어설션이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-168">Your CloudPassage application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span>   
<span data-ttu-id="1dce1-169">다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-169">hello following screenshot shows an example for this.</span></span>
   
   ![Single Sign-on 구성](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_25.png) 

6. <span data-ttu-id="1dce1-171">Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 위의 hello 이미지에 나와 있는 것 처럼 SAML 토큰 특성을 구성 하 고 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>

    | <span data-ttu-id="1dce1-172">특성 이름</span><span class="sxs-lookup"><span data-stu-id="1dce1-172">Attribute Name</span></span> | <span data-ttu-id="1dce1-173">특성 값</span><span class="sxs-lookup"><span data-stu-id="1dce1-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="1dce1-174">firstname</span><span class="sxs-lookup"><span data-stu-id="1dce1-174">firstname</span></span> |<span data-ttu-id="1dce1-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="1dce1-175">user.givenname</span></span> |
    | <span data-ttu-id="1dce1-176">lastname</span><span class="sxs-lookup"><span data-stu-id="1dce1-176">lastname</span></span> |<span data-ttu-id="1dce1-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="1dce1-177">user.surname</span></span> |
    | <span data-ttu-id="1dce1-178">email</span><span class="sxs-lookup"><span data-stu-id="1dce1-178">email</span></span> |<span data-ttu-id="1dce1-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="1dce1-179">user.mail</span></span> |
    
    <span data-ttu-id="1dce1-180">a.</span><span class="sxs-lookup"><span data-stu-id="1dce1-180">a.</span></span> <span data-ttu-id="1dce1-181">클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="1dce1-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_04.png)
    
    ![Single Sign-on 구성](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="1dce1-184">b.</span><span class="sxs-lookup"><span data-stu-id="1dce1-184">b.</span></span> <span data-ttu-id="1dce1-185">Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="1dce1-186">c.</span><span class="sxs-lookup"><span data-stu-id="1dce1-186">c.</span></span> <span data-ttu-id="1dce1-187">Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="1dce1-188">d.</span><span class="sxs-lookup"><span data-stu-id="1dce1-188">d.</span></span> <span data-ttu-id="1dce1-189">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-189">Click **Ok**.</span></span>

7. <span data-ttu-id="1dce1-190">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-190">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="1dce1-192">Hello에 **CloudPassage 구성** 섹션에서 클릭 **구성 CloudPassage** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="1dce1-192">On hello **CloudPassage Configuration** section, click **Configure CloudPassage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1dce1-193">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="1dce1-193">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_configure.png) 

9. <span data-ttu-id="1dce1-195">다른 브라우저 창에서 관리자 권한으로 로그온 tooyour CloudPassage 회사 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-195">In a different browser window, sign-on tooyour CloudPassage company site as administrator.</span></span>

10. <span data-ttu-id="1dce1-196">Hello 메뉴에서 hello 위에 표시를 클릭 **설정**, 클릭 하 고 **사이트 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-196">In hello menu on hello top, click **Settings**, and then click **Site Administration**.</span></span> 
   
    ![Single Sign-on 구성][12]

11. <span data-ttu-id="1dce1-198">Hello 클릭 **인증 설정** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-198">Click hello **Authentication Settings** tab.</span></span> 
   
    ![Single Sign-on 구성][13]

12. <span data-ttu-id="1dce1-200">Hello에 **Single Sign on 설정** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-200">In hello **Single Sign-on Settings** section, perform hello following steps:</span></span> 
   
    ![Single Sign-on 구성][14]

    <span data-ttu-id="1dce1-202">a.</span><span class="sxs-lookup"><span data-stu-id="1dce1-202">a.</span></span> <span data-ttu-id="1dce1-203">**SSO(Single Sign-On) 사용(SSO 설치 설명서)** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-203">Select **Enable Single sign-on(SSO)(SSO Setup Documentation)** checkbox.</span></span>
    
    <span data-ttu-id="1dce1-204">b.</span><span class="sxs-lookup"><span data-stu-id="1dce1-204">b.</span></span> <span data-ttu-id="1dce1-205">붙여넣기 **SAML 엔터티 ID** hello에 **SAML 발급자 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-205">Paste **SAML Entity ID** into hello **SAML issuer URL** textbox.</span></span>
  
    <span data-ttu-id="1dce1-206">c.</span><span class="sxs-lookup"><span data-stu-id="1dce1-206">c.</span></span> <span data-ttu-id="1dce1-207">붙여넣기 **SAML Single Sign-on 서비스 URL** hello에 **SAML 끝점 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-207">Paste **SAML Single Sign-On Service URL** into hello **SAML endpoint URL** textbox.</span></span>
  
    <span data-ttu-id="1dce1-208">d.</span><span class="sxs-lookup"><span data-stu-id="1dce1-208">d.</span></span> <span data-ttu-id="1dce1-209">붙여넣기 **Sign-Out URL** hello에 **로그 아웃 방문 페이지** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-209">Paste **Sign-Out URL** into hello **Logout landing page** textbox.</span></span>
  
    <span data-ttu-id="1dce1-210">e.</span><span class="sxs-lookup"><span data-stu-id="1dce1-210">e.</span></span> <span data-ttu-id="1dce1-211">클립보드에 다운로드 한 인증서의 콘텐츠 복사 hello 메모장에서 다운로드 한 인증서를 열고 hello에 붙여 넣습니다 **x509 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-211">Open your downloaded certificate in notepad, copy hello content of downloaded certificate into your clipboard, and then paste it into hello **x 509 certificate** textbox.</span></span>
  
    <span data-ttu-id="1dce1-212">f.</span><span class="sxs-lookup"><span data-stu-id="1dce1-212">f.</span></span> <span data-ttu-id="1dce1-213">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="1dce1-214">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="1dce1-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1dce1-215">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="1dce1-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1dce1-216">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1dce1-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1dce1-217">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1dce1-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="1dce1-218">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="1dce1-220">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1dce1-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1dce1-221">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1dce1-223">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1dce1-225">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1dce1-227">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1dce1-229">a.</span><span class="sxs-lookup"><span data-stu-id="1dce1-229">a.</span></span> <span data-ttu-id="1dce1-230">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1dce1-231">b.</span><span class="sxs-lookup"><span data-stu-id="1dce1-231">b.</span></span> <span data-ttu-id="1dce1-232">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1dce1-233">c.</span><span class="sxs-lookup"><span data-stu-id="1dce1-233">c.</span></span> <span data-ttu-id="1dce1-234">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1dce1-235">d.</span><span class="sxs-lookup"><span data-stu-id="1dce1-235">d.</span></span> <span data-ttu-id="1dce1-236">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-236">Click **Create**.</span></span>
 
### <a name="creating-a-cloudpassage-test-user"></a><span data-ttu-id="1dce1-237">CloudPassage 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1dce1-237">Creating a CloudPassage test user</span></span>

<span data-ttu-id="1dce1-238">hello이이 섹션의 목적은 toocreate Britta Simon CloudPassage에서 호출 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-238">hello objective of this section is toocreate a user called Britta Simon in CloudPassage.</span></span>

<span data-ttu-id="1dce1-239">**toocreate Britta Simon CloudPassage의 라는 사용자를 만들면 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1dce1-239">**toocreate a user called Britta Simon in CloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="1dce1-240">로그온 tooyour **CloudPassage** 회사 사이트에 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-240">Sign-on tooyour **CloudPassage** company site as an administrator.</span></span> 

2. <span data-ttu-id="1dce1-241">도구 모음의 hello hello 위쪽에 클릭 **설정**, 클릭 하 고 **사이트 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-241">In hello toolbar on hello top, click **Settings**, and then click **Site Administration**.</span></span> 
   
   ![CloudPassage 테스트 사용자 만들기][22] 

3. <span data-ttu-id="1dce1-243">Hello 클릭 **사용자** 탭을 클릭 한 다음 **새 사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-243">Click hello **Users** tab, and then click **Add New User**.</span></span> 
   
   ![CloudPassage 테스트 사용자 만들기][23]

4. <span data-ttu-id="1dce1-245">Hello에 **새 사용자 추가** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-245">In hello **Add New User** section, perform hello following steps:</span></span> 
   
   ![CloudPassage 테스트 사용자 만들기][24]
    
    <span data-ttu-id="1dce1-247">a.</span><span class="sxs-lookup"><span data-stu-id="1dce1-247">a.</span></span> <span data-ttu-id="1dce1-248">Hello에 **이름** textbox Britta를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-248">In hello **First Name** textbox, type Britta.</span></span> 
  
    <span data-ttu-id="1dce1-249">b.</span><span class="sxs-lookup"><span data-stu-id="1dce1-249">b.</span></span> <span data-ttu-id="1dce1-250">Hello에 **성** textbox Simon를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-250">In hello **Last Name** textbox, type Simon.</span></span>
  
    <span data-ttu-id="1dce1-251">c.</span><span class="sxs-lookup"><span data-stu-id="1dce1-251">c.</span></span> <span data-ttu-id="1dce1-252">Hello에 **사용자 이름** 텍스트 상자 hello **전자 메일** 텍스트 상자에 붙여넣습니다 및 hello **전자 메일을 다시 입력** 텍스트 상자 Azure AD에 Britta의 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-252">In hello **Username** textbox, hello **Email** textbox and hello **Retype Email** textbox, type Britta's user name in Azure AD.</span></span>
  
    <span data-ttu-id="1dce1-253">d.</span><span class="sxs-lookup"><span data-stu-id="1dce1-253">d.</span></span> <span data-ttu-id="1dce1-254">**액세스 유형**으로 **Halo 포털 액세스 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-254">As **Access Type**, select **Enable Halo Portal Access**.</span></span>
  
    <span data-ttu-id="1dce1-255">e.</span><span class="sxs-lookup"><span data-stu-id="1dce1-255">e.</span></span> <span data-ttu-id="1dce1-256">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-256">Click **Add**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1dce1-257">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1dce1-258">이 섹션에서는 tooCloudPassage 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCloudPassage.</span></span>

![사용자 할당][200] 

<span data-ttu-id="1dce1-260">**tooassign Britta Simon tooCloudPassage hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1dce1-260">**tooassign Britta Simon tooCloudPassage, perform hello following steps:**</span></span>

1. <span data-ttu-id="1dce1-261">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="1dce1-263">Hello 응용 프로그램 목록에서 선택 **CloudPassage**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-263">In hello applications list, select **CloudPassage**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_app.png) 

3. <span data-ttu-id="1dce1-265">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="1dce1-267">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-267">Click **Add** button.</span></span> <span data-ttu-id="1dce1-268">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="1dce1-270">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1dce1-271">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1dce1-272">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1dce1-273">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="1dce1-273">Testing single sign-on</span></span>

<span data-ttu-id="1dce1-274">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD SSO 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-274">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="1dce1-275">Hello 액세스 패널에서에서 hello CloudPassage 타일을 클릭할 때 자동으로 로그온 tooyour CloudPassage 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dce1-275">When you click hello CloudPassage tile in hello Access Panel, you should get automatically signed-on tooyour CloudPassage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1dce1-276">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1dce1-276">Additional resources</span></span>

* [<span data-ttu-id="1dce1-277">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="1dce1-277">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1dce1-278">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="1dce1-278">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_07.png
[13]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_08.png
[14]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_09.png
[15]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_10.png
[22]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_15.png
[23]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_16.png
[24]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_17.png

[100]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_203.png

