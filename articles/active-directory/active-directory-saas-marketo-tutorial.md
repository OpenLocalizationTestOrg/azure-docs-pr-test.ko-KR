---
title: "자습서: Marketo와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Marketo 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 87f88cde4f027f99a83c1ab3b318247bb4d658ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a><span data-ttu-id="c7305-103">자습서:Azure Active Directory와 Marketo 통합</span><span class="sxs-lookup"><span data-stu-id="c7305-103">Tutorial: Azure Active Directory integration with Marketo</span></span>

<span data-ttu-id="c7305-104">이 자습서에 설명 어떻게 toointegrate Marketo Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c7305-104">In this tutorial, you learn how toointegrate Marketo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c7305-105">Marketo Azure AD와 통합 hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-105">Integrating Marketo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c7305-106">액세스 tooMarketo을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-106">You can control in Azure AD who has access tooMarketo</span></span>
- <span data-ttu-id="c7305-107">프로그램 사용자 tooautomatically get 로그온 tooMarketo (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-107">You can enable your users tooautomatically get signed-on tooMarketo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c7305-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c7305-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7305-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c7305-110">Prerequisites</span></span>

<span data-ttu-id="c7305-111">Marketo와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-111">tooconfigure Azure AD integration with Marketo, you need hello following items:</span></span>

- <span data-ttu-id="c7305-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="c7305-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c7305-113">Marketo Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="c7305-113">A Marketo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c7305-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c7305-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c7305-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c7305-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c7305-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c7305-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="c7305-118">Scenario description</span></span>
<span data-ttu-id="c7305-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c7305-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c7305-121">Marketo는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="c7305-121">Adding Marketo from hello gallery</span></span>
2. <span data-ttu-id="c7305-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c7305-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-marketo-from-hello-gallery"></a><span data-ttu-id="c7305-123">Marketo는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="c7305-123">Adding Marketo from hello gallery</span></span>
<span data-ttu-id="c7305-124">tooconfigure hello와의 통합 Marketo Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Marketo tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-124">tooconfigure hello integration of Marketo into Azure AD, you need tooadd Marketo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c7305-125">**hello 갤러리에서 Marketo tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c7305-125">**tooadd Marketo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7305-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c7305-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c7305-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="c7305-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="c7305-133">Hello 검색 상자에 입력 **Marketo**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-133">In hello search box, type **Marketo**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. <span data-ttu-id="c7305-135">Hello 결과 패널에서 선택 **Marketo**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-135">In hello results panel, select **Marketo**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c7305-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c7305-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c7305-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Marketo에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-138">In this section, you configure and test Azure AD single sign-on with Marketo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c7305-139">Single sign on toowork에 대 한 Azure AD는 tooknow marketo에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Marketo is tooa user in Azure AD.</span></span> <span data-ttu-id="c7305-140">즉, Azure AD 사용자 및 marketo에서 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-140">In other words, a link relationship between an Azure AD user and hello related user in Marketo needs toobe established.</span></span>

<span data-ttu-id="c7305-141">Marketo에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-141">In Marketo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c7305-142">tooconfigure 및 Marketo와 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-142">tooconfigure and test Azure AD single sign-on with Marketo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c7305-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c7305-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c7305-145">**[Marketo 테스트 사용자 만들기](#creating-a-marketo-test-user)**  -toohave 사용자의 연결 된 Azure AD toohello 표현인 marketo Britta Simon의 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-145">**[Creating a Marketo test user](#creating-a-marketo-test-user)** - toohave a counterpart of Britta Simon in Marketo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c7305-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c7305-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="c7305-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c7305-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="c7305-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c7305-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Marketo 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Marketo application.</span></span>

<span data-ttu-id="c7305-150">**Azure AD tooconfigure single sign on Marketo와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c7305-150">**tooconfigure Azure AD single sign-on with Marketo, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7305-151">Hello hello에 Azure 포털에서에서 **Marketo** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-151">In hello Azure portal, on hello **Marketo** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="c7305-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. <span data-ttu-id="c7305-155">Hello에 **Marketo 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-155">On hello **Marketo Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    <span data-ttu-id="c7305-157">a.</span><span class="sxs-lookup"><span data-stu-id="c7305-157">a.</span></span> <span data-ttu-id="c7305-158">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://saml.marketo.com/sp`</span><span class="sxs-lookup"><span data-stu-id="c7305-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://saml.marketo.com/sp`</span></span>

    <span data-ttu-id="c7305-159">b.</span><span class="sxs-lookup"><span data-stu-id="c7305-159">b.</span></span> <span data-ttu-id="c7305-160">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://login.marketo.com/saml/assertion/\<munchkinid\>`</span><span class="sxs-lookup"><span data-stu-id="c7305-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c7305-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-161">These values are not real.</span></span> <span data-ttu-id="c7305-162">Hello 실제 식별자 및 회신 URL로이 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="c7305-163">연락처 [Marketo 지원 팀](http://investors.marketo.com/contactus.cfm) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-163">Contact [Marketo support team](http://investors.marketo.com/contactus.cfm) tooget these values.</span></span>
 
4. <span data-ttu-id="c7305-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. <span data-ttu-id="c7305-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c7305-168">Hello에 **Marketo 구성** 섹션에서 클릭 **구성 Marketo** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="c7305-168">On hello **Marketo Configuration** section, click **Configure Marketo** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c7305-169">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="c7305-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. <span data-ttu-id="c7305-171">tooMarketo 관리자 자격 증명을 사용 하 여 로그인 하 고 다음 작업을 수행 하는 응용 프로그램의 Munchkin Id tooget:</span><span class="sxs-lookup"><span data-stu-id="c7305-171">tooget Munchkin Id of your application, log in tooMarketo using admin credentials and perform following actions:</span></span>
   
    <span data-ttu-id="c7305-172">a.</span><span class="sxs-lookup"><span data-stu-id="c7305-172">a.</span></span> <span data-ttu-id="c7305-173">관리자 자격 증명을 사용 하 여 tooMarketo 앱에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-173">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="c7305-174">b.</span><span class="sxs-lookup"><span data-stu-id="c7305-174">b.</span></span> <span data-ttu-id="c7305-175">Hello 클릭 **Admin** hello 위쪽 탐색 창에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-175">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="c7305-177">c.</span><span class="sxs-lookup"><span data-stu-id="c7305-177">c.</span></span> <span data-ttu-id="c7305-178">Toohello 통합 메뉴를 탐색 하 고 hello 클릭 **Munchkin 링크**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-178">Navigate toohello Integration menu and click hello **Munchkin link**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    <span data-ttu-id="c7305-180">d.</span><span class="sxs-lookup"><span data-stu-id="c7305-180">d.</span></span> <span data-ttu-id="c7305-181">Hello hello 화면에 표시 된 Munchkin Id를 복사 하 고 회신 URL hello Azure AD 구성 마법사에서를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-181">Copy hello Munchkin Id shown on hello screen and complete your Reply URL in hello Azure AD configuration wizard.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. <span data-ttu-id="c7305-183">hello 응용 프로그램에 대 한 SSO tooconfigure hello hello 아래 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-183">tooconfigure hello SSO in hello application, follow hello below steps:</span></span>
   
    <span data-ttu-id="c7305-184">a.</span><span class="sxs-lookup"><span data-stu-id="c7305-184">a.</span></span> <span data-ttu-id="c7305-185">관리자 자격 증명을 사용 하 여 tooMarketo 앱에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-185">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="c7305-186">b.</span><span class="sxs-lookup"><span data-stu-id="c7305-186">b.</span></span> <span data-ttu-id="c7305-187">Hello 클릭 **Admin** hello 위쪽 탐색 창에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-187">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="c7305-189">c.</span><span class="sxs-lookup"><span data-stu-id="c7305-189">c.</span></span> <span data-ttu-id="c7305-190">Toohello 통합 메뉴를 탐색 하 고 클릭 **Single Sign On**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-190">Navigate toohello Integration menu and click **Single Sign On**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    <span data-ttu-id="c7305-192">d.</span><span class="sxs-lookup"><span data-stu-id="c7305-192">d.</span></span> <span data-ttu-id="c7305-193">SAML 설정 tooenable hello 클릭 **편집** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-193">tooenable hello SAML Settings, click **Edit** button.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    <span data-ttu-id="c7305-195">e.</span><span class="sxs-lookup"><span data-stu-id="c7305-195">e.</span></span> <span data-ttu-id="c7305-196">Single Sign-On 설정을 사용하도록 **설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-196">**Enabled** Single Sign-On settings.</span></span>
   
    <span data-ttu-id="c7305-197">f.</span><span class="sxs-lookup"><span data-stu-id="c7305-197">f.</span></span> <span data-ttu-id="c7305-198">붙여넣기 hello **SAML 엔터티 ID**, hello에 **발급자 ID** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-198">Paste hello **SAML Entity ID**, in hello **Issuer ID** textbox.</span></span>
   
    <span data-ttu-id="c7305-199">g.</span><span class="sxs-lookup"><span data-stu-id="c7305-199">g.</span></span> <span data-ttu-id="c7305-200">Hello에 **엔터티 ID** textbox hello URL로 입력 `http://saml.marketo.com/sp`합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-200">In hello **Entity ID** textbox, enter hello URL as `http://saml.marketo.com/sp`.</span></span>
   
    <span data-ttu-id="c7305-201">h.</span><span class="sxs-lookup"><span data-stu-id="c7305-201">h.</span></span> <span data-ttu-id="c7305-202">사용자 ID 위치 선택 hello로 **Name Identifier 요소**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-202">Select hello User ID Location as **Name Identifier element**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > <span data-ttu-id="c7305-204">사용자 식별자는 UPN 값 다음에 hello 특성 탭 hello 값 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-204">If your User Identifier is not UPN value then change hello value in hello Attribute tab.</span></span>
   
    <span data-ttu-id="c7305-205">i.</span><span class="sxs-lookup"><span data-stu-id="c7305-205">i.</span></span> <span data-ttu-id="c7305-206">Azure AD 구성 마법사에서 다운로드 한 hello 인증서를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-206">Upload hello certificate, which you have downloaded from Azure AD configuration wizard.</span></span> <span data-ttu-id="c7305-207">**저장** hello 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-207">**Save** hello settings.</span></span>
   
    <span data-ttu-id="c7305-208">j.</span><span class="sxs-lookup"><span data-stu-id="c7305-208">j.</span></span> <span data-ttu-id="c7305-209">Hello 리디렉션 페이지 설정을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-209">Edit hello Redirect Pages settings.</span></span>
   
    <span data-ttu-id="c7305-210">k.</span><span class="sxs-lookup"><span data-stu-id="c7305-210">k.</span></span> <span data-ttu-id="c7305-211">붙여넣기 hello **SAML Single Sign-on 서비스 URL** hello에 **로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-211">Paste hello **SAML Single Sign-On Service URL** in hello **Login URL** textbox.</span></span>
   
    <span data-ttu-id="c7305-212">l.</span><span class="sxs-lookup"><span data-stu-id="c7305-212">l.</span></span> <span data-ttu-id="c7305-213">붙여넣기 hello **Sign-Out URL** hello에 **로그 아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-213">Paste hello **Sign-Out URL** in hello **Logout URL** textbox.</span></span>
   
    <span data-ttu-id="c7305-214">m.</span><span class="sxs-lookup"><span data-stu-id="c7305-214">m.</span></span> <span data-ttu-id="c7305-215">Hello에 **오류 URL**, 복사 하면 **Marketo 인스턴스 URL** 클릭 **저장** toosave 설정 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-215">In hello **Error URL**, copy your **Marketo instance URL** and click **Save** button toosave settings.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. <span data-ttu-id="c7305-217">tooenable hello SSO 사용자에 대 한 작업을 수행 하는 전체 hello:</span><span class="sxs-lookup"><span data-stu-id="c7305-217">tooenable hello SSO for users, complete hello following actions:</span></span>
   
    <span data-ttu-id="c7305-218">a.</span><span class="sxs-lookup"><span data-stu-id="c7305-218">a.</span></span> <span data-ttu-id="c7305-219">관리자 자격 증명을 사용 하 여 tooMarketo 앱에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-219">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="c7305-220">b.</span><span class="sxs-lookup"><span data-stu-id="c7305-220">b.</span></span> <span data-ttu-id="c7305-221">Hello 클릭 **Admin** hello 위쪽 탐색 창에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-221">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="c7305-223">c.</span><span class="sxs-lookup"><span data-stu-id="c7305-223">c.</span></span> <span data-ttu-id="c7305-224">Toohello 이동 **보안** 메뉴 **로그인 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-224">Navigate toohello **Security** menu and click **Login Settings**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    <span data-ttu-id="c7305-226">d.</span><span class="sxs-lookup"><span data-stu-id="c7305-226">d.</span></span> <span data-ttu-id="c7305-227">Hello 확인 **필요 SSO** 옵션 및 **저장** hello 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-227">Check hello **Require SSO** option and **Save** hello settings.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> <span data-ttu-id="c7305-229">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="c7305-229">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c7305-230">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="c7305-230">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c7305-231">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c7305-231">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c7305-232">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c7305-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="c7305-233">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-233">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="c7305-235">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c7305-235">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7305-236">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-236">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c7305-238">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-238">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c7305-240">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-240">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c7305-242">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-242">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c7305-244">a.</span><span class="sxs-lookup"><span data-stu-id="c7305-244">a.</span></span> <span data-ttu-id="c7305-245">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-245">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c7305-246">b.</span><span class="sxs-lookup"><span data-stu-id="c7305-246">b.</span></span> <span data-ttu-id="c7305-247">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-247">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c7305-248">c.</span><span class="sxs-lookup"><span data-stu-id="c7305-248">c.</span></span> <span data-ttu-id="c7305-249">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-249">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c7305-250">d.</span><span class="sxs-lookup"><span data-stu-id="c7305-250">d.</span></span> <span data-ttu-id="c7305-251">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-251">Click **Create**.</span></span>
 
### <a name="creating-a-marketo-test-user"></a><span data-ttu-id="c7305-252">Marketo 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="c7305-252">Creating a Marketo test user</span></span>

<span data-ttu-id="c7305-253">이 섹션에서는 Marketo에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-253">In this section, you create a user called Britta Simon in Marketo.</span></span> <span data-ttu-id="c7305-254">이러한 단계 toocreate Marketo 플랫폼의 사용자를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-254">follow these steps toocreate a user in Marketo platform.</span></span>

1. <span data-ttu-id="c7305-255">관리자 자격 증명을 사용 하 여 tooMarketo 앱에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-255">Log in tooMarketo app using admin credentials.</span></span>

2. <span data-ttu-id="c7305-256">Hello 클릭 **Admin** hello 위쪽 탐색 창에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-256">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. <span data-ttu-id="c7305-258">Toohello 이동 **보안** 메뉴 **사용자 및 역할**</span><span class="sxs-lookup"><span data-stu-id="c7305-258">Navigate toohello **Security** menu and click **Users & Roles**</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. <span data-ttu-id="c7305-260">Hello 클릭 **새 사용자를 초대** hello 사용자 탭의 링크</span><span class="sxs-lookup"><span data-stu-id="c7305-260">Click hello **Invite New User** link on hello Users tab</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. <span data-ttu-id="c7305-262">Hello 새 사용자를 초대 마법사 채우기 hello 정보 다음에</span><span class="sxs-lookup"><span data-stu-id="c7305-262">In hello Invite New User wizard fill hello following information</span></span>
   
    <span data-ttu-id="c7305-263">a.</span><span class="sxs-lookup"><span data-stu-id="c7305-263">a.</span></span> <span data-ttu-id="c7305-264">Hello 사용자 입력 **전자 메일** hello 텍스트 상자에 주소</span><span class="sxs-lookup"><span data-stu-id="c7305-264">Enter hello user **Email** address in hello textbox</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    <span data-ttu-id="c7305-266">b.</span><span class="sxs-lookup"><span data-stu-id="c7305-266">b.</span></span> <span data-ttu-id="c7305-267">Hello 입력 **이름** hello 텍스트 상자에</span><span class="sxs-lookup"><span data-stu-id="c7305-267">Enter hello **First Name** in hello textbox</span></span>
   
    <span data-ttu-id="c7305-268">c.</span><span class="sxs-lookup"><span data-stu-id="c7305-268">c.</span></span> <span data-ttu-id="c7305-269">Hello 입력 **성** hello 텍스트 상자에</span><span class="sxs-lookup"><span data-stu-id="c7305-269">Enter hello **Last Name**  in hello textbox</span></span>
   
    <span data-ttu-id="c7305-270">d.</span><span class="sxs-lookup"><span data-stu-id="c7305-270">d.</span></span> <span data-ttu-id="c7305-271">**다음**을 누릅니다</span><span class="sxs-lookup"><span data-stu-id="c7305-271">Click **Next**</span></span>

6. <span data-ttu-id="c7305-272">Hello에 **권한을** 탭, 선택 hello **userRoles** 클릭 **다음**</span><span class="sxs-lookup"><span data-stu-id="c7305-272">In hello **Permissions** tab, select hello **userRoles** and click **Next**</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. <span data-ttu-id="c7305-274">Hello 클릭 **보낼** toosend hello 사용자 초대 단추</span><span class="sxs-lookup"><span data-stu-id="c7305-274">Click hello **Send** button toosend hello user invitation</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. <span data-ttu-id="c7305-276">사용자는 hello 전자 메일 알림을 수신 하 고 tooclick hello에 연결 하 고 hello 암호 tooactivate hello 계정을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-276">User receives hello email notification and has tooclick hello link and change hello password tooactivate hello account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c7305-277">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-277">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c7305-278">이 섹션에서는 tooMarketo 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-278">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMarketo.</span></span>

![사용자 할당][200] 

<span data-ttu-id="c7305-280">**tooassign Britta Simon tooMarketo hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c7305-280">**tooassign Britta Simon tooMarketo, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7305-281">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-281">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="c7305-283">Hello 응용 프로그램 목록에서 선택 **Marketo**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-283">In hello applications list, select **Marketo**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. <span data-ttu-id="c7305-285">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-285">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="c7305-287">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-287">Click **Add** button.</span></span> <span data-ttu-id="c7305-288">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-288">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="c7305-290">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-290">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c7305-291">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-291">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c7305-292">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-292">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c7305-293">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="c7305-293">Testing single sign-on</span></span>

<span data-ttu-id="c7305-294">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-294">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c7305-295">Hello 액세스 패널에서에서 hello Marketo 타일을 클릭할 때 자동으로 로그온 tooyour Marketo 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7305-295">When you click hello Marketo tile in hello Access Panel, you should get automatically signed-on tooyour Marketo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c7305-296">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="c7305-296">Additional resources</span></span>

* [<span data-ttu-id="c7305-297">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="c7305-297">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c7305-298">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="c7305-298">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

