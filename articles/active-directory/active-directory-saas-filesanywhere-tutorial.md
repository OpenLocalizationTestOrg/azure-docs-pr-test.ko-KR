---
title: "자습서: FilesAnywhere와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 FilesAnywhere 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 376364a5c75f8d069ea6390c58586acb378cd8b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a><span data-ttu-id="6c4ec-103">자습서:FilesAnywhere와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="6c4ec-103">Tutorial: Azure Active Directory integration with FilesAnywhere</span></span>

<span data-ttu-id="6c4ec-104">이 자습서에 설명 어떻게 toointegrate FilesAnywhere Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6c4ec-104">In this tutorial, you learn how toointegrate FilesAnywhere with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6c4ec-105">다음 이점을 hello로 제공 FilesAnywhere Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="6c4ec-105">Integrating FilesAnywhere with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6c4ec-106">액세스 tooFilesAnywhere을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-106">You can control in Azure AD who has access tooFilesAnywhere</span></span>
- <span data-ttu-id="6c4ec-107">프로그램 사용자 tooautomatically get 로그온 tooFilesAnywhere (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-107">You can enable your users tooautomatically get signed-on tooFilesAnywhere (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6c4ec-108">하나의 중앙 위치-hello Azure 관리 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="6c4ec-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c4ec-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6c4ec-110">Prerequisites</span></span>

<span data-ttu-id="6c4ec-111">다음 항목 hello가 필요 tooconfigure FilesAnywhere와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-111">tooconfigure Azure AD integration with FilesAnywhere, you need hello following items:</span></span>

- <span data-ttu-id="6c4ec-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="6c4ec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6c4ec-113">FilesAnywhere Single Sign-On을 사용하도록 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="6c4ec-113">A FilesAnywhere single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="6c4ec-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="6c4ec-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6c4ec-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="6c4ec-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="6c4ec-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="6c4ec-118">Scenario description</span></span>
<span data-ttu-id="6c4ec-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6c4ec-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6c4ec-121">FilesAnywhere는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="6c4ec-121">Adding FilesAnywhere from hello gallery</span></span>
2. <span data-ttu-id="6c4ec-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="6c4ec-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-filesanywhere-from-hello-gallery"></a><span data-ttu-id="6c4ec-123">FilesAnywhere는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="6c4ec-123">Adding FilesAnywhere from hello gallery</span></span>
<span data-ttu-id="6c4ec-124">tooconfigure hello와의 통합 FilesAnywhere Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 FilesAnywhere tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-124">tooconfigure hello integration of FilesAnywhere into Azure AD, you need tooadd FilesAnywhere from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6c4ec-125">**hello 갤러리에서 FilesAnywhere tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6c4ec-125">**tooadd FilesAnywhere from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6c4ec-126">Hello에  **[Azure 관리 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6c4ec-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6c4ec-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="6c4ec-131">클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="6c4ec-133">Hello 검색 상자에 입력 **FilesAnywhere**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-133">In hello search box, type **FilesAnywhere**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. <span data-ttu-id="6c4ec-135">Hello 결과 패널에서 선택 **FilesAnywhere**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-135">In hello results panel, select **FilesAnywhere**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6c4ec-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="6c4ec-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6c4ec-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 FilesAnywhere에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-138">In this section, you configure and test Azure AD single sign-on with FilesAnywhere based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6c4ec-139">Single sign on toowork에 대 한 Azure AD는 tooknow FilesAnywhere에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FilesAnywhere is tooa user in Azure AD.</span></span> <span data-ttu-id="6c4ec-140">즉, Azure AD 사용자 및 FilesAnywhere에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-140">In other words, a link relationship between an Azure AD user and hello related user in FilesAnywhere needs toobe established.</span></span>

<span data-ttu-id="6c4ec-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** FilesAnywhere에 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FilesAnywhere.</span></span>

<span data-ttu-id="6c4ec-142">tooconfigure 및 FilesAnywhere 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-142">tooconfigure and test Azure AD single sign-on with FilesAnywhere, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6c4ec-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6c4ec-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6c4ec-145">**[FilesAnywhere 테스트 사용자 만들기](#creating-a-filesanywhere-test-user)**  -toohave Britta Simon 그녀의 연결 된 Azure AD toohello 표현인 FilesAnywhere에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-145">**[Creating a FilesAnywhere test user](#creating-a-filesanywhere-test-user)** - toohave a counterpart of Britta Simon in FilesAnywhere that is linked toohello Azure AD representation of her.</span></span>
3. <span data-ttu-id="6c4ec-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
4. <span data-ttu-id="6c4ec-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6c4ec-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="6c4ec-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6c4ec-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 관리 포털에서 설정 및 FilesAnywhere 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FilesAnywhere application.</span></span>

<span data-ttu-id="6c4ec-150">**tooconfigure Azure AD single sign on, FilesAnywhere와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6c4ec-150">**tooconfigure Azure AD single sign-on with FilesAnywhere, perform hello following steps:**</span></span>

1. <span data-ttu-id="6c4ec-151">Hello에 hello Azure 관리 포털에서 **FilesAnywhere** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-151">In hello Azure Management portal, on hello **FilesAnywhere** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="6c4ec-153">Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. <span data-ttu-id="6c4ec-155">Hello에 **FilesAnywhere 도메인 및 Url** tooconfigure hello 응용 프로그램에 필요한 경우 섹션 **IDP 시작 모드**:</span><span class="sxs-lookup"><span data-stu-id="6c4ec-155">On hello **FilesAnywhere Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    <span data-ttu-id="6c4ec-157">a.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-157">a.</span></span> <span data-ttu-id="6c4ec-158">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span><span class="sxs-lookup"><span data-stu-id="6c4ec-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span></span>
> [!NOTE]
> <span data-ttu-id="6c4ec-159">해당 hello 값 점에 유의 하십시오 **215** 는 **clientid** 은 예 시일 뿐 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-159">Please note that hello value **215** is a **clientid** and is just an example.</span></span> <span data-ttu-id="6c4ec-160">Tooreplace 필요한 hello 실제 clientid 값을 가진 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-160">You need tooreplace it with hello actual clientid value.</span></span>

4. <span data-ttu-id="6c4ec-161">Hello에 **FilesAnywhere 도메인 및 Url** 섹션 tooconfigure hello 응용 프로그램에 필요한 경우 **SP 시작 모드**, hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-161">On hello **FilesAnywhere Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    <span data-ttu-id="6c4ec-163">a.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-163">a.</span></span> <span data-ttu-id="6c4ec-164">Hello 클릭 **고급 URL 설정 표시** 옵션</span><span class="sxs-lookup"><span data-stu-id="6c4ec-164">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="6c4ec-165">b.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-165">b.</span></span> <span data-ttu-id="6c4ec-166">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<sub domain>.filesanywhere.com/`</span><span class="sxs-lookup"><span data-stu-id="6c4ec-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<sub domain>.filesanywhere.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6c4ec-167">이러한 없는지 hello 실제 값 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-167">Please note that these are not hello real values.</span></span> <span data-ttu-id="6c4ec-168">Tooupdate hello 실제 로그온 URL 및 회신 URL 사용 하 여 이러한 값 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-168">You have tooupdate these values with hello actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="6c4ec-169">연락처 [FilesAnywhere 지원 팀](mailto:support@FilesAnywhere.com) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-169">Contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) tooget these values.</span></span> 

5. <span data-ttu-id="6c4ec-170">FilesAnywhere 소프트웨어 응용 프로그램에는 특정 형식의 hello SAML 어설션 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-170">FilesAnywhere Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="6c4ec-171">이 응용 프로그램에 대 한 클레임을 따라 hello를 구성 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-171">Please configure hello following claims for this application.</span></span> <span data-ttu-id="6c4ec-172">Hello에서 이러한 특성의 hello 값을 관리할 수 있습니다 "**사용자 특성**" 응용 프로그램 통합 페이지에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-172">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="6c4ec-173">다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-173">hello following screenshot shows an example for this.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    <span data-ttu-id="6c4ec-175">FilesAnywhere 러 워 hello 값을 사용자가 로그인 하면 hello **clientid** 에서 특성 [FilesAnywhere 팀](mailto:support@FilesAnywhere.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-175">When hello users signs up with FilesAnywhere they get hello value of **clientid** attribute from [FilesAnywhere team](mailto:support@FilesAnywhere.com).</span></span> <span data-ttu-id="6c4ec-176">Hello FilesAnywhere에서 제공 되는 고유 값을 가진 tooadd hello "클라이언트 Id" 특성을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-176">You have tooadd hello "Client Id" attribute with hello unique value provided by FilesAnywhere.</span></span> <span data-ttu-id="6c4ec-177">위에 표시된 모든 특성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-177">All these attributes shown above are required.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="6c4ec-178">해당 hello 값 참고 **2331** 의 **clientid** 은 예 시일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-178">Please note that hello value **2331** of **clientid** is just an example.</span></span> <span data-ttu-id="6c4ec-179">Tooprovide hello에 대 한 실제 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-179">You need tooprovide hello actual value.</span></span>


6. <span data-ttu-id="6c4ec-180">Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 위의 hello 이미지에 나와 있는 것 처럼 SAML 토큰 특성을 구성 하 고 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-180">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="6c4ec-181">특성 이름</span><span class="sxs-lookup"><span data-stu-id="6c4ec-181">Attribute Name</span></span> | <span data-ttu-id="6c4ec-182">특성 값</span><span class="sxs-lookup"><span data-stu-id="6c4ec-182">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="6c4ec-183">clientid</span><span class="sxs-lookup"><span data-stu-id="6c4ec-183">clientid</span></span> | <span data-ttu-id="6c4ec-184">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="6c4ec-184">*"uniquevalue"*</span></span> |

    <span data-ttu-id="6c4ec-185">a.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-185">a.</span></span> <span data-ttu-id="6c4ec-186">클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-186">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    <span data-ttu-id="6c4ec-189">b.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-189">b.</span></span> <span data-ttu-id="6c4ec-190">Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-190">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="6c4ec-191">c.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-191">c.</span></span> <span data-ttu-id="6c4ec-192">Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-192">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="6c4ec-193">d.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-193">d.</span></span> <span data-ttu-id="6c4ec-194">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-194">Click **Ok**</span></span>

7. <span data-ttu-id="6c4ec-195">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-195">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="6c4ec-197">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-197">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. <span data-ttu-id="6c4ec-199">Hello에 **FilesAnywhere 구성** 섹션에서 클릭 **구성 FilesAnywhere** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-199">On hello **FilesAnywhere Configuration** section, click **Configure FilesAnywhere** tooopen **Configure sign-on** window.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. <span data-ttu-id="6c4ec-202">tooget SSO 구성 연락처 FilesAnywhere 끝 응용 프로그램에 대 한 완료 [FilesAnywhere 지원 팀](mailto:support@FilesAnywhere.com) 다운로드 하는 hello SAML 토큰 서명 인증서 및 단일 로그인 (SSO) URL을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-202">tooget SSO configuration complete for your application at FilesAnywhere end, contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) and provide them hello downloaded SAML token signing Certificate and Single Sign On (SSO) URL.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6c4ec-203">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="6c4ec-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="6c4ec-204">이 섹션의 hello 목표 toocreate Britta Simon 라는 hello Azure 관리 포털에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-204">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="6c4ec-206">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6c4ec-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6c4ec-207">Hello에 **Azure 관리 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-207">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6c4ec-209">너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-209">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6c4ec-211">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-211">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6c4ec-213">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6c4ec-215">a.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-215">a.</span></span> <span data-ttu-id="6c4ec-216">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6c4ec-217">b.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-217">b.</span></span> <span data-ttu-id="6c4ec-218">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6c4ec-219">c.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-219">c.</span></span> <span data-ttu-id="6c4ec-220">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6c4ec-221">d.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-221">d.</span></span> <span data-ttu-id="6c4ec-222">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-222">Click **Create**.</span></span> 



### <a name="creating-a-filesanywhere-test-user"></a><span data-ttu-id="6c4ec-223">FilesAnywhere 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="6c4ec-223">Creating a FilesAnywhere test user</span></span>

<span data-ttu-id="6c4ec-224">응용 프로그램 적시 사용자 프로 비전 및 인증 사용자 hello 응용 프로그램에서에 자동으로 생성 한 후 마법사를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-224">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6c4ec-225">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6c4ec-226">이 섹션에서는 액세스 tooFilesAnywhere 그녀의 권한을 부여 하 여 Azure single sign on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFilesAnywhere.</span></span>

![사용자 할당][200] 

<span data-ttu-id="6c4ec-228">**tooassign Britta Simon tooFilesAnywhere hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6c4ec-228">**tooassign Britta Simon tooFilesAnywhere, perform hello following steps:**</span></span>

1. <span data-ttu-id="6c4ec-229">Hello Azure 관리 포털에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-229">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="6c4ec-231">Hello 응용 프로그램 목록에서 선택 **FilesAnywhere**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-231">In hello applications list, select **FilesAnywhere**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. <span data-ttu-id="6c4ec-233">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="6c4ec-235">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-235">Click **Add** button.</span></span> <span data-ttu-id="6c4ec-236">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="6c4ec-238">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6c4ec-239">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6c4ec-240">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="6c4ec-241">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="6c4ec-241">Testing single sign-on</span></span>

<span data-ttu-id="6c4ec-242">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-242">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6c4ec-243">Hello 액세스 패널에서에서 hello FilesAnywhere 타일을 클릭할 때 자동으로 로그온 tooyour FilesAnywhere 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ec-243">When you click hello FilesAnywhere tile in hello Access Panel, you should get automatically signed-on tooyour FilesAnywhere application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="6c4ec-244">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="6c4ec-244">Additional resources</span></span>

* [<span data-ttu-id="6c4ec-245">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="6c4ec-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6c4ec-246">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="6c4ec-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
