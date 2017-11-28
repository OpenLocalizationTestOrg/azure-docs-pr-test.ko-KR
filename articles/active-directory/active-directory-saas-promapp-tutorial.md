---
title: "자습서: Promapp과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Promapp 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 418d0601-6e7a-4997-a683-73fa30a2cfb5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 02de7679b0c86d7aa8cacb41762f900dbf2ff231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-promapp"></a><span data-ttu-id="c5125-103">자습서: Promapp과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="c5125-103">Tutorial: Azure Active Directory integration with Promapp</span></span>

<span data-ttu-id="c5125-104">이 자습서에 설명 어떻게 toointegrate Promapp Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c5125-104">In this tutorial, you learn how toointegrate Promapp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c5125-105">다음 이점을 hello로 제공 Promapp Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="c5125-105">Integrating Promapp with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c5125-106">액세스 tooPromapp을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-106">You can control in Azure AD who has access tooPromapp</span></span>
- <span data-ttu-id="c5125-107">프로그램 사용자 tooautomatically get 로그온 tooPromapp (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-107">You can enable your users tooautomatically get signed-on tooPromapp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c5125-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c5125-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5125-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c5125-110">Prerequisites</span></span>

<span data-ttu-id="c5125-111">다음 항목 hello가 필요 tooconfigure Promapp와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-111">tooconfigure Azure AD integration with Promapp, you need hello following items:</span></span>

- <span data-ttu-id="c5125-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="c5125-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c5125-113">Promapp Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="c5125-113">A Promapp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c5125-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c5125-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c5125-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c5125-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c5125-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c5125-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="c5125-118">Scenario description</span></span>
<span data-ttu-id="c5125-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c5125-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c5125-121">Promapp은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="c5125-121">Adding Promapp from hello gallery</span></span>
2. <span data-ttu-id="c5125-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c5125-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-promapp-from-hello-gallery"></a><span data-ttu-id="c5125-123">Promapp은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="c5125-123">Adding Promapp from hello gallery</span></span>
<span data-ttu-id="c5125-124">tooconfigure hello와의 통합 Promapp Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Promapp tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-124">tooconfigure hello integration of Promapp into Azure AD, you need tooadd Promapp from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c5125-125">**hello 갤러리에서 Promapp tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c5125-125">**tooadd Promapp from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5125-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c5125-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c5125-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="c5125-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="c5125-133">Hello 검색 상자에 입력 **Promapp**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-133">In hello search box, type **Promapp**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_search.png)

5. <span data-ttu-id="c5125-135">Hello 결과 패널에서 선택 **Promapp**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-135">In hello results panel, select **Promapp**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c5125-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c5125-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c5125-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Promapp에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-138">In this section, you configure and test Azure AD single sign-on with Promapp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c5125-139">Single sign on toowork에 대 한 Azure AD는 tooknow Promapp에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Promapp is tooa user in Azure AD.</span></span> <span data-ttu-id="c5125-140">즉, Azure AD 사용자 및 Promapp에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-140">In other words, a link relationship between an Azure AD user and hello related user in Promapp needs toobe established.</span></span>

<span data-ttu-id="c5125-141">Promapp에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-141">In Promapp, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c5125-142">tooconfigure 및 Promapp 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-142">tooconfigure and test Azure AD single sign-on with Promapp, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c5125-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c5125-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c5125-145">**[Promapp 테스트 사용자 만들기](#creating-a-promapp-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Promapp에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-145">**[Creating a Promapp test user](#creating-a-promapp-test-user)** - toohave a counterpart of Britta Simon in Promapp that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c5125-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c5125-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="c5125-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c5125-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="c5125-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c5125-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Promapp 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Promapp application.</span></span>

<span data-ttu-id="c5125-150">**tooconfigure Azure AD single sign on, Promapp와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c5125-150">**tooconfigure Azure AD single sign-on with Promapp, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5125-151">Hello hello에 Azure 포털에서에서 **Promapp** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-151">In hello Azure portal, on hello **Promapp** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="c5125-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_samlbase.png)

3. <span data-ttu-id="c5125-155">Hello에 **Promapp 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-155">On hello **Promapp Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_url.png)

    <span data-ttu-id="c5125-157">a.</span><span class="sxs-lookup"><span data-stu-id="c5125-157">a.</span></span> <span data-ttu-id="c5125-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span><span class="sxs-lookup"><span data-stu-id="c5125-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span></span>

    <span data-ttu-id="c5125-159">b.</span><span class="sxs-lookup"><span data-stu-id="c5125-159">b.</span></span> <span data-ttu-id="c5125-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://DOMAINNAME.promapp.com/TENANTNAME`</span><span class="sxs-lookup"><span data-stu-id="c5125-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c5125-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-161">These values are not real.</span></span> <span data-ttu-id="c5125-162">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c5125-163">연락처 [Promapp 클라이언트 지원 팀](https://www.promapp.com/about-us/contact-us/) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-163">Contact [Promapp Client support team](https://www.promapp.com/about-us/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="c5125-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_certificate.png) 

5. <span data-ttu-id="c5125-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-promapp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c5125-168">Hello에 **Promapp 구성** 섹션에서 클릭 **구성 Promapp** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="c5125-168">On hello **Promapp Configuration** section, click **Configure Promapp** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c5125-169">복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="c5125-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_configure.png) 

7. <span data-ttu-id="c5125-171">관리자 권한으로 로그온 tooyour Promapp 회사 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-171">Sign-on tooyour Promapp company site as administrator.</span></span> 

8. <span data-ttu-id="c5125-172">Hello 메뉴에서 hello 위에 표시를 클릭 **Admin**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-172">In hello menu on hello top, click **Admin**.</span></span> 
   
    ![Azure AD Single Sign-On][12]

9. <span data-ttu-id="c5125-174">**Configure**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-174">Click **Configure**.</span></span> 
   
    ![Azure AD Single Sign-On][13]

10. <span data-ttu-id="c5125-176">Hello에 **보안** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-176">On hello **Security** dialog, perform hello following steps:</span></span>
   
    ![Azure AD Single Sign-On][14]
    
    <span data-ttu-id="c5125-178">a.</span><span class="sxs-lookup"><span data-stu-id="c5125-178">a.</span></span> <span data-ttu-id="c5125-179">붙여넣기 **SAML Single Sign-on 서비스 URL**, hello에 hello Azure 포털에서에서 복사한 있는 **SSO 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-179">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **SSO-Login URL** textbox.</span></span>
    
    <span data-ttu-id="c5125-180">b.</span><span class="sxs-lookup"><span data-stu-id="c5125-180">b.</span></span> <span data-ttu-id="c5125-181">**SSO - Single Sign-On 모드**로 **옵션**을 선택한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-181">As **SSO - Single Sign-on Mode**, select **Optional**, and then click **Save**.</span></span>

    <span data-ttu-id="c5125-182">c.</span><span class="sxs-lookup"><span data-stu-id="c5125-182">c.</span></span> <span data-ttu-id="c5125-183">열기 hello hello 첫 번째 줄 (---BEGIN 인증서---) 및 hello 마지막 줄 (---END 인증서---) hello에 붙여 없이 복사 hello 인증서 내용 메모장에서 인증서를 다운로드 **SSO x.509 인증서** 입력란을 클릭 하 고 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-183">Open hello downloaded certificate in notepad, copy hello certificate content without hello first line (-----BEGIN CERTIFICATE-----) and hello last line (-----END CERTIFICATE-----), paste it into hello **SSO-x.509 Certificate** textbox, and then click **Save**.</span></span>
        
> [!TIP]
> <span data-ttu-id="c5125-184">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="c5125-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c5125-185">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="c5125-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c5125-186">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c5125-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c5125-187">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c5125-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="c5125-188">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="c5125-190">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c5125-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5125-191">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-promapp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c5125-193">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-promapp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c5125-195">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-promapp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c5125-197">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-promapp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c5125-199">a.</span><span class="sxs-lookup"><span data-stu-id="c5125-199">a.</span></span> <span data-ttu-id="c5125-200">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c5125-201">b.</span><span class="sxs-lookup"><span data-stu-id="c5125-201">b.</span></span> <span data-ttu-id="c5125-202">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c5125-203">c.</span><span class="sxs-lookup"><span data-stu-id="c5125-203">c.</span></span> <span data-ttu-id="c5125-204">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c5125-205">d.</span><span class="sxs-lookup"><span data-stu-id="c5125-205">d.</span></span> <span data-ttu-id="c5125-206">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-206">Click **Create**.</span></span>
 
### <a name="creating-a-promapp-test-user"></a><span data-ttu-id="c5125-207">Promapp 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c5125-207">Creating a Promapp test user</span></span>

<span data-ttu-id="c5125-208">hello Promapp 응용 프로그램 지원 Just in Time 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-208">hello Promapp application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="c5125-209">이 즉, 사용자 계정 하면 hello 액세스 패널을 사용 하는 시도 tooaccess hello 적용 하는 동안 필요한 경우 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-209">This means, a user account is automatically created if necessary during an attempt tooaccess hello application using hello Access Panel.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c5125-210">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c5125-211">이 섹션에서는 tooPromapp 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPromapp.</span></span>

![사용자 할당][200] 

<span data-ttu-id="c5125-213">**tooassign Britta Simon tooPromapp hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c5125-213">**tooassign Britta Simon tooPromapp, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5125-214">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="c5125-216">Hello 응용 프로그램 목록에서 선택 **Promapp**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-216">In hello applications list, select **Promapp**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_app.png) 

3. <span data-ttu-id="c5125-218">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="c5125-220">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-220">Click **Add** button.</span></span> <span data-ttu-id="c5125-221">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="c5125-223">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c5125-224">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c5125-225">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c5125-226">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="c5125-226">Testing single sign-on</span></span>

<span data-ttu-id="c5125-227">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD SSO 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="c5125-228">Hello 액세스 패널에서에서 hello Promapp 타일을 클릭할 때 자동으로 로그온 tooyour Promapp 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5125-228">When you click hello Promapp tile in hello Access Panel, you should get automatically signed-on tooyour Promapp application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c5125-229">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="c5125-229">Additional resources</span></span>

* [<span data-ttu-id="c5125-230">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="c5125-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c5125-231">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="c5125-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_05.png
[13]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_06.png
[14]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_07.png

[100]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_203.png

