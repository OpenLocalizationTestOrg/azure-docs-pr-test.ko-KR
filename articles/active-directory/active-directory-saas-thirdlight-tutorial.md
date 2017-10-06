---
title: "자습서: ThirdLight와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 ThirdLight 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 168aae9a-54ee-4c2b-ab12-650a2c62b901
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: a510e514f6a8c4e89220b9a6f6db29668b451b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thirdlight"></a><span data-ttu-id="b5915-103">자습서: ThirdLight와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="b5915-103">Tutorial: Azure Active Directory integration with ThirdLight</span></span>

<span data-ttu-id="b5915-104">이 자습서에 설명 어떻게 toointegrate ThirdLight Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b5915-104">In this tutorial, you learn how toointegrate ThirdLight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b5915-105">다음 이점을 hello로 제공 ThirdLight Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="b5915-105">Integrating ThirdLight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b5915-106">액세스 tooThirdLight을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-106">You can control in Azure AD who has access tooThirdLight</span></span>
- <span data-ttu-id="b5915-107">프로그램 사용자 tooautomatically get 로그온 tooThirdLight (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-107">You can enable your users tooautomatically get signed-on tooThirdLight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b5915-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b5915-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5915-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b5915-110">Prerequisites</span></span>

<span data-ttu-id="b5915-111">다음 항목 hello가 필요 tooconfigure ThirdLight와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-111">tooconfigure Azure AD integration with ThirdLight, you need hello following items:</span></span>

- <span data-ttu-id="b5915-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="b5915-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b5915-113">ThirdLight Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="b5915-113">A ThirdLight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b5915-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b5915-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b5915-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b5915-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b5915-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b5915-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="b5915-118">Scenario description</span></span>
<span data-ttu-id="b5915-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b5915-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b5915-121">ThirdLight은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="b5915-121">Adding ThirdLight from hello gallery</span></span>
2. <span data-ttu-id="b5915-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b5915-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thirdlight-from-hello-gallery"></a><span data-ttu-id="b5915-123">ThirdLight은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="b5915-123">Adding ThirdLight from hello gallery</span></span>
<span data-ttu-id="b5915-124">tooconfigure hello와의 통합 ThirdLight Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 ThirdLight tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-124">tooconfigure hello integration of ThirdLight into Azure AD, you need tooadd ThirdLight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b5915-125">**hello 갤러리에서 ThirdLight tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b5915-125">**tooadd ThirdLight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5915-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b5915-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b5915-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="b5915-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="b5915-133">Hello 검색 상자에 입력 **ThirdLight**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-133">In hello search box, type **ThirdLight**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_search.png)

5. <span data-ttu-id="b5915-135">Hello 결과 패널에서 선택 **ThirdLight**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-135">In hello results panel, select **ThirdLight**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b5915-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b5915-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b5915-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 ThirdLight에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-138">In this section, you configure and test Azure AD single sign-on with ThirdLight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b5915-139">Single sign on toowork에 대 한 Azure AD는 tooknow ThirdLight에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ThirdLight is tooa user in Azure AD.</span></span> <span data-ttu-id="b5915-140">즉, Azure AD 사용자 및 ThirdLight에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-140">In other words, a link relationship between an Azure AD user and hello related user in ThirdLight needs toobe established.</span></span>

<span data-ttu-id="b5915-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** ThirdLight에 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ThirdLight.</span></span>

<span data-ttu-id="b5915-142">tooconfigure 및 ThirdLight 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-142">tooconfigure and test Azure AD single sign-on with ThirdLight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b5915-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b5915-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b5915-145">**[ThirdLight 테스트 사용자 만들기](#creating-a-thirdlight-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 ThirdLight에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-145">**[Creating a ThirdLight test user](#creating-a-thirdlight-test-user)** - toohave a counterpart of Britta Simon in ThirdLight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b5915-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b5915-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="b5915-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b5915-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="b5915-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b5915-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 ThirdLight 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ThirdLight application.</span></span>

<span data-ttu-id="b5915-150">**tooconfigure Azure AD single sign on, ThirdLight와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b5915-150">**tooconfigure Azure AD single sign-on with ThirdLight, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5915-151">Hello hello에 Azure 포털에서에서 **ThirdLight** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-151">In hello Azure portal, on hello **ThirdLight** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="b5915-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_samlbase.png)

3. <span data-ttu-id="b5915-155">Hello에 **ThirdLight 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-155">On hello **ThirdLight Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_url.png)

    <span data-ttu-id="b5915-157">a.</span><span class="sxs-lookup"><span data-stu-id="b5915-157">a.</span></span> <span data-ttu-id="b5915-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.thirdlight.com/`</span><span class="sxs-lookup"><span data-stu-id="b5915-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.thirdlight.com/`</span></span>

    <span data-ttu-id="b5915-159">b.</span><span class="sxs-lookup"><span data-stu-id="b5915-159">b.</span></span> <span data-ttu-id="b5915-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.thirdlight.com/saml/sp`</span><span class="sxs-lookup"><span data-stu-id="b5915-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.thirdlight.com/saml/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b5915-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-161">These values are not real.</span></span> <span data-ttu-id="b5915-162">이러한 항목을 업데이트 로그온 URL과 Identiifer 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-162">Update these values with hello actual Sign-On URL and Identiifer.</span></span> <span data-ttu-id="b5915-163">연락처 [ThirdLight 클라이언트 지원 팀](https://www.thirdlight.com/support) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-163">Contact [ThirdLight Client support team](https://www.thirdlight.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="b5915-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello XML 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_certificate.png) 

5. <span data-ttu-id="b5915-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-thirdlight-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b5915-168">다른 웹 브라우저 창에서 관리자 권한으로 tooyour ThirdLight 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-168">In a different web browser window, log in tooyour ThirdLight company site as an administrator.</span></span>

7. <span data-ttu-id="b5915-169">너무 이동**구성 \> 시스템 관리**, 클릭 하 고 **SAML2**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-169">Go too**Configuration \> System Administration**, and then click **SAML2**.</span></span>
   
    <span data-ttu-id="b5915-170">![시스템 관리](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "시스템 관리")</span><span class="sxs-lookup"><span data-stu-id="b5915-170">![System Administration](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "System Administration")</span></span>

8. <span data-ttu-id="b5915-171">토큰이 SAML2 hello 구성 섹션에서 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-171">In hello SAML2 configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="b5915-172">![SAML Single Sign-On](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "SAML Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="b5915-172">![SAML Single Sign-On](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "SAML Single Sign-On")</span></span>   

     <span data-ttu-id="b5915-173">a.</span><span class="sxs-lookup"><span data-stu-id="b5915-173">a.</span></span> <span data-ttu-id="b5915-174">**SAML2 Single Sign-On 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-174">Select **Enable SAML2 Single Sign-On**.</span></span>
 
     <span data-ttu-id="b5915-175">b.</span><span class="sxs-lookup"><span data-stu-id="b5915-175">b.</span></span> <span data-ttu-id="b5915-176">**IdP 메타데이터에 대한 원본**으로 **XML에서 IdP 메타데이터 로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-176">As **Source for IdP Metadata**, select **Load IdP Metadata from XML**.</span></span>
 
     <span data-ttu-id="b5915-177">c.</span><span class="sxs-lookup"><span data-stu-id="b5915-177">c.</span></span> <span data-ttu-id="b5915-178">Hello 다운로드 한 메타 데이터 파일을 열고 hello 콘텐츠 복사, hello에 붙여 넣습니다 **IdP 메타 데이터 XML** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-178">Open hello downloaded metadata file, copy hello content, and then paste it into hello **IdP Metadata XML** textbox.</span></span> 
     
     <span data-ttu-id="b5915-179">d.</span><span class="sxs-lookup"><span data-stu-id="b5915-179">d.</span></span> <span data-ttu-id="b5915-180">**SAML2 설정 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-180">Click **Save SAML2 settings**.</span></span>

> [!TIP]
> <span data-ttu-id="b5915-181">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="b5915-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b5915-182">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="b5915-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b5915-183">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b5915-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b5915-184">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b5915-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="b5915-185">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="b5915-187">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b5915-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5915-188">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b5915-190">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b5915-192">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b5915-194">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b5915-196">a.</span><span class="sxs-lookup"><span data-stu-id="b5915-196">a.</span></span> <span data-ttu-id="b5915-197">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b5915-198">b.</span><span class="sxs-lookup"><span data-stu-id="b5915-198">b.</span></span> <span data-ttu-id="b5915-199">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** Britta Simon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-199">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="b5915-200">c.</span><span class="sxs-lookup"><span data-stu-id="b5915-200">c.</span></span> <span data-ttu-id="b5915-201">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b5915-202">d.</span><span class="sxs-lookup"><span data-stu-id="b5915-202">d.</span></span> <span data-ttu-id="b5915-203">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-203">Click **Create**.</span></span>
 
### <a name="creating-a-thirdlight-test-user"></a><span data-ttu-id="b5915-204">ThirdLight 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b5915-204">Creating a ThirdLight test user</span></span>

<span data-ttu-id="b5915-205">tooenable Azure AD 사용자가 toolog tooThirdLight에서 이러한 해야에 프로 비전 ThirdLight 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-205">tooenable Azure AD users toolog in tooThirdLight, they must be provisioned into ThirdLight.</span></span>  
<span data-ttu-id="b5915-206">Hello ThirdLight의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-206">In hello case of ThirdLight, provisioning is a manual task.</span></span>

<span data-ttu-id="b5915-207">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b5915-207">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5915-208">Tooyour 로그인 **ThirdLight** 회사 사이트에 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-208">Log in tooyour **ThirdLight** company site as an administrator.</span></span>

2. <span data-ttu-id="b5915-209">너무 이동**사용자** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-209">Go too**Users** tab.</span></span>

3. <span data-ttu-id="b5915-210">**사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-210">Select **Users and Groups**.</span></span>

4. <span data-ttu-id="b5915-211">**새 사용자 추가** 버튼을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-211">Click **Add new User** button.</span></span>

5. <span data-ttu-id="b5915-212">입력 **hello 사용자 이름, 이름 또는 설명, 메일, 선택는 사전 설정 또는 새 멤버의 그룹** tooprovision 하려는 유효한 AAD 계정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-212">Enter **hello Username, Name or Description, Email, Choose a Preset or Group of New Members** of a valid AAD account you want tooprovision.</span></span>

6. <span data-ttu-id="b5915-213">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-213">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="b5915-214">다른 Thirdlight 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 Thirdlight tooprovision에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-214">You can use any other Thirdlight user account creation tools or APIs provided by Thirdlight tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b5915-215">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b5915-216">이 섹션에서는 tooThirdLight 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThirdLight.</span></span>

![사용자 할당][200] 

<span data-ttu-id="b5915-218">**tooassign Britta Simon tooThirdLight hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b5915-218">**tooassign Britta Simon tooThirdLight, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5915-219">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="b5915-221">Hello 응용 프로그램 목록에서 선택 **ThirdLight**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-221">In hello applications list, select **ThirdLight**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_app.png) 

3. <span data-ttu-id="b5915-223">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="b5915-225">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-225">Click **Add** button.</span></span> <span data-ttu-id="b5915-226">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="b5915-228">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b5915-229">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b5915-230">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b5915-231">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="b5915-231">Testing single sign-on</span></span>

<span data-ttu-id="b5915-232">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b5915-233">Hello 액세스 패널에서에서 hello ThirdLight 타일을 클릭할 때 자동으로 로그온 tooyour ThirdLight 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-233">When you click hello ThirdLight tile in hello Access Panel, you should get automatically signed-on tooyour ThirdLight application.</span></span>
<span data-ttu-id="b5915-234">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b5915-234">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b5915-235">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b5915-235">Additional resources</span></span>

* [<span data-ttu-id="b5915-236">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="b5915-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b5915-237">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b5915-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_203.png

