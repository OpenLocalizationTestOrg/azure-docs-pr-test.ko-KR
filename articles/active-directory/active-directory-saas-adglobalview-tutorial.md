---
title: "자습서: ADP Globalview와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory 및 ADP Globalview 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffb6464f-714d-41a9-869a-2b7e5ae9f125
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: aee2d56f05b486d12facbc41c9503455094604ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-globalview"></a><span data-ttu-id="6ac42-103">자습서: ADP Globalview와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="6ac42-103">Tutorial: Azure Active Directory integration with ADP Globalview</span></span>

<span data-ttu-id="6ac42-104">이 자습서에 설명 어떻게 toointegrate ADP Globalview Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6ac42-104">In this tutorial, you learn how toointegrate ADP Globalview with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6ac42-105">다음 이점을 hello로 제공 ADP Globalview Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="6ac42-105">Integrating ADP Globalview with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6ac42-106">액세스 tooADP Globalview 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-106">You can control in Azure AD who has access tooADP Globalview</span></span>
- <span data-ttu-id="6ac42-107">프로그램 사용자 tooautomatically get 로그온 tooADP Globalview (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-107">You can enable your users tooautomatically get signed-on tooADP Globalview (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6ac42-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6ac42-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ac42-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6ac42-110">Prerequisites</span></span>

<span data-ttu-id="6ac42-111">다음 항목 hello가 필요 tooconfigure ADP Globalview와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-111">tooconfigure Azure AD integration with ADP Globalview, you need hello following items:</span></span>

- <span data-ttu-id="6ac42-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="6ac42-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6ac42-113">ADP Globalview Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="6ac42-113">An ADP Globalview single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6ac42-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6ac42-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6ac42-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="6ac42-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6ac42-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6ac42-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="6ac42-118">Scenario description</span></span>
<span data-ttu-id="6ac42-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6ac42-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6ac42-121">ADP Globalview hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="6ac42-121">Adding ADP Globalview from hello gallery</span></span>
2. <span data-ttu-id="6ac42-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="6ac42-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-globalview-from-hello-gallery"></a><span data-ttu-id="6ac42-123">ADP Globalview hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="6ac42-123">Adding ADP Globalview from hello gallery</span></span>
<span data-ttu-id="6ac42-124">tooconfigure hello와의 통합 ADP Globalview Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 ADP Globalview tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-124">tooconfigure hello integration of ADP Globalview into Azure AD, you need tooadd ADP Globalview from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6ac42-125">**hello 갤러리에서 ADP Globalview tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6ac42-125">**tooadd ADP Globalview from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ac42-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6ac42-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6ac42-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="6ac42-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="6ac42-133">Hello 검색 상자에 입력 **ADP Globalview**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-133">In hello search box, type **ADP Globalview**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_search.png)

5. <span data-ttu-id="6ac42-135">Hello 결과 패널에서 선택 **ADP Globalview**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-135">In hello results panel, select **ADP Globalview**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6ac42-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="6ac42-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6ac42-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 ADP Globalview에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-138">In this section, you configure and test Azure AD single sign-on with ADP Globalview based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6ac42-139">Single sign on toowork에 대 한 Azure AD는 tooknow ADP Globalview에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ADP Globalview is tooa user in Azure AD.</span></span> <span data-ttu-id="6ac42-140">즉, Azure AD 사용자 및 ADP Globalview에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-140">In other words, a link relationship between an Azure AD user and hello related user in ADP Globalview needs toobe established.</span></span>

<span data-ttu-id="6ac42-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** ADP Globalview에 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ADP Globalview.</span></span>

<span data-ttu-id="6ac42-142">tooconfigure 및 ADP Globalview를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-142">tooconfigure and test Azure AD single sign-on with ADP Globalview, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6ac42-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6ac42-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6ac42-145">**[ADP Globalview 테스트 사용자 만들기](#creating-an-adp-globalview-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 ADP Globalview에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-145">**[Creating an ADP Globalview test user](#creating-an-adp-globalview-test-user)** - toohave a counterpart of Britta Simon in ADP Globalview that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6ac42-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6ac42-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="6ac42-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6ac42-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="6ac42-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6ac42-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 ADP Globalview 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ADP Globalview application.</span></span>

<span data-ttu-id="6ac42-150">**Azure AD tooconfigure single sign on ADP Globalview와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6ac42-150">**tooconfigure Azure AD single sign-on with ADP Globalview, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ac42-151">Hello hello에 Azure 포털에서에서 **ADP Globalview** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-151">In hello Azure portal, on hello **ADP Globalview** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="6ac42-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_samlbase.png)

3. <span data-ttu-id="6ac42-155">Hello에 **ADP Globalview 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-155">On hello **ADP Globalview Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_url.png)

     <span data-ttu-id="6ac42-157">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL: `https://<subdomain>.globalview.adp.com/federate` 또는`https://<subdomain>.globalview.adp.com/federate2`</span><span class="sxs-lookup"><span data-stu-id="6ac42-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.globalview.adp.com/federate` or `https://<subdomain>.globalview.adp.com/federate2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6ac42-158">hello 값이 실제 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-158">hello value is not real.</span></span> <span data-ttu-id="6ac42-159">Hello로 hello 값을 업데이트 합니다. 실제 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-159">Update hello value with hello actual Identifier.</span></span> <span data-ttu-id="6ac42-160">연락처 [ADP Globalview 지원](https://www.adp.com/contact-us/overview.aspx) tooget hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-160">Contact [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) tooget hello value.</span></span>
 
4. <span data-ttu-id="6ac42-161">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_certificate.png) 

5. <span data-ttu-id="6ac42-163">hello ADP GlobalView 응용 프로그램 구성을 수행 해야 하면 tooadd 사용자 지정 특성 매핑을 tooyour SAML 토큰 특성을 특정 형식에서 hello SAML 어설션이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-163">hello ADP GlobalView application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> 

6. <span data-ttu-id="6ac42-164">다음 스크린 샷 hello에 대 한 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-164">hello following screenshot shows an example for it.</span></span> <span data-ttu-id="6ac42-165">hello 클레임 이름은 항상 이어야 **"PersonImmutableID"** hello 값의 포함 된 tooExtensionAttribute2 매핑한 म hello 사용자의 EmployeeID hello 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-165">hello claim names always be **"PersonImmutableID"** and hello value of which we have mapped tooExtensionAttribute2, which contains hello EmployeeID of hello user.</span></span> <span data-ttu-id="6ac42-166">여기에서 Azure AD tooADP GlobalView hello 사용자 매핑을 hello EmployeeID에 수행 되지만 tooa 다른 값도 응용 프로그램 설정에 따라 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-166">Here hello user mapping from Azure AD tooADP GlobalView is done on hello EmployeeID but you can map it tooa different value also based on your application settings.</span></span> <span data-ttu-id="6ac42-167">Hello ADP GlobalView 팀 첫 번째 toouse hello 올바른 식별자가 사용자를 사용 하 고 해당 값 hello로 매핑할 **"PersonImmutableID"** 클레임입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-167">You can work with hello ADP GlobalView team first toouse hello correct identifier of a user and map that value with hello **"PersonImmutableID"** claim.</span></span> <span data-ttu-id="6ac42-168">Hello 전자 메일 및 사용자 Id 클레임 hello 그림에 나와 있는 것 처럼 매핑할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-168">You can also map hello Email and UserID claim as shown in hello picture.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_attribute.png)

7. <span data-ttu-id="6ac42-170">Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 hello 이미지에 나와 있는 것 처럼 SAML 토큰 특성을 구성 하 고 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="6ac42-171">특성 이름</span><span class="sxs-lookup"><span data-stu-id="6ac42-171">Attribute Name</span></span> | <span data-ttu-id="6ac42-172">특성 값</span><span class="sxs-lookup"><span data-stu-id="6ac42-172">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="6ac42-173">personalimmutableid</span><span class="sxs-lookup"><span data-stu-id="6ac42-173">personalimmutableid</span></span> | <span data-ttu-id="6ac42-174">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="6ac42-174">user.extensionattribute2</span></span> |
    | <span data-ttu-id="6ac42-175">email</span><span class="sxs-lookup"><span data-stu-id="6ac42-175">email</span></span>               | <span data-ttu-id="6ac42-176">user.mail</span><span class="sxs-lookup"><span data-stu-id="6ac42-176">user.mail</span></span> |
    | <span data-ttu-id="6ac42-177">userid</span><span class="sxs-lookup"><span data-stu-id="6ac42-177">userid</span></span>              | <span data-ttu-id="6ac42-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="6ac42-178">user.userprincipalname</span></span>|
    
    <span data-ttu-id="6ac42-179">a.</span><span class="sxs-lookup"><span data-stu-id="6ac42-179">a.</span></span> <span data-ttu-id="6ac42-180">클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="6ac42-180">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="6ac42-183">b.</span><span class="sxs-lookup"><span data-stu-id="6ac42-183">b.</span></span> <span data-ttu-id="6ac42-184">Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="6ac42-185">c.</span><span class="sxs-lookup"><span data-stu-id="6ac42-185">c.</span></span> <span data-ttu-id="6ac42-186">Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-186">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="6ac42-187">d.</span><span class="sxs-lookup"><span data-stu-id="6ac42-187">d.</span></span> <span data-ttu-id="6ac42-188">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-188">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6ac42-189">Hello SAML 어설션이 구성 하려면 먼저 toocontact 프로그램 [ADP Globalview 지원](https://www.adp.com/contact-us/overview.aspx) 및 테 넌 트에 대 한 hello 고유 식별자 특성의 hello 값을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-189">Before you can configure hello SAML assertion, you need toocontact your [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="6ac42-190">이 값 tooconfigure hello 사용자 지정 클레임 응용 프로그램에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-190">You need this value tooconfigure hello custom claim for your application.</span></span> 

8. <span data-ttu-id="6ac42-191">Hello에 **ADP Globalview 구성** 섹션에서 클릭 **ADP Globalview 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="6ac42-191">On hello **ADP Globalview Configuration** section, click **Configure ADP Globalview** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6ac42-192">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="6ac42-192">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_configure.png) 

9. <span data-ttu-id="6ac42-194">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-194">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adglobalview-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="6ac42-196">tooconfigure single sign on에서 **ADP Globalview** toosend hello 다운로드 해야 쪽에서는 **인증서 (Base64)**, **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** 너무[ADP Globalview 지원](https://www.adp.com/contact-us/overview.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-196">tooconfigure single sign-on on **ADP Globalview** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[ADP Globalview support](https://www.adp.com/contact-us/overview.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="6ac42-197">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="6ac42-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6ac42-198">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="6ac42-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6ac42-199">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6ac42-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6ac42-200">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="6ac42-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="6ac42-201">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="6ac42-203">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6ac42-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ac42-204">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="6ac42-206">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6ac42-208">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6ac42-210">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6ac42-212">a.</span><span class="sxs-lookup"><span data-stu-id="6ac42-212">a.</span></span> <span data-ttu-id="6ac42-213">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6ac42-214">b.</span><span class="sxs-lookup"><span data-stu-id="6ac42-214">b.</span></span> <span data-ttu-id="6ac42-215">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6ac42-216">c.</span><span class="sxs-lookup"><span data-stu-id="6ac42-216">c.</span></span> <span data-ttu-id="6ac42-217">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6ac42-218">d.</span><span class="sxs-lookup"><span data-stu-id="6ac42-218">d.</span></span> <span data-ttu-id="6ac42-219">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-219">Click **Create**.</span></span>
 
### <a name="creating-an-adp-globalview-test-user"></a><span data-ttu-id="6ac42-220">ADP Globalview 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="6ac42-220">Creating an ADP Globalview test user</span></span>

<span data-ttu-id="6ac42-221">hello이이 섹션의 목적은 toocreate Britta Simon ADP GlobalView에서 호출 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-221">hello objective of this section is toocreate a user called Britta Simon in ADP GlobalView.</span></span> <span data-ttu-id="6ac42-222">작업할 [ADP Globalview 지원](https://www.adp.com/contact-us/overview.aspx) hello ADP GlobalView 계정에서에서 tooadd hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-222">Work with [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) tooadd hello users in hello ADP GlobalView account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6ac42-223">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6ac42-224">이 섹션에서는 액세스 tooADP Globalview 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooADP Globalview.</span></span>

![사용자 할당][200] 

<span data-ttu-id="6ac42-226">**tooassign Britta Simon tooADP Globalview, hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6ac42-226">**tooassign Britta Simon tooADP Globalview, perform hello following steps:**</span></span>

1. <span data-ttu-id="6ac42-227">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="6ac42-229">Hello 응용 프로그램 목록에서 선택 **ADP Globalview**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-229">In hello applications list, select **ADP Globalview**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_app.png) 

3. <span data-ttu-id="6ac42-231">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="6ac42-233">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-233">Click **Add** button.</span></span> <span data-ttu-id="6ac42-234">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="6ac42-236">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6ac42-237">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6ac42-238">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6ac42-239">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="6ac42-239">Testing single sign-on</span></span>

<span data-ttu-id="6ac42-240">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD SSO 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-240">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="6ac42-241">Hello ADP GlobalView hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour ADP GlobalView 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ac42-241">When you click hello ADP GlobalView tile in hello Access Panel, you should get automatically signed-on tooyour ADP GlobalView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6ac42-242">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="6ac42-242">Additional resources</span></span>

* [<span data-ttu-id="6ac42-243">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="6ac42-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6ac42-244">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="6ac42-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_203.png

