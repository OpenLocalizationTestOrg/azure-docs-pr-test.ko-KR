---
title: "자습서: Panopto와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Panopto 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89c88e23-93ce-4970-9baa-1104c4e8fe4a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 76b30e1cd2782bb5fba3d229378b8f82652b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panopto"></a><span data-ttu-id="5c8ee-103">자습서: Panopto와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="5c8ee-103">Tutorial: Azure Active Directory integration with Panopto</span></span>

<span data-ttu-id="5c8ee-104">이 자습서에 설명 어떻게 toointegrate Panopto와 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5c8ee-104">In this tutorial, you learn how toointegrate Panopto with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5c8ee-105">Azure AD와 Panopto 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-105">Integrating Panopto with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5c8ee-106">액세스 tooPanopto을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-106">You can control in Azure AD who has access tooPanopto</span></span>
- <span data-ttu-id="5c8ee-107">프로그램 사용자 tooautomatically get 로그온 tooPanopto (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-107">You can enable your users tooautomatically get signed-on tooPanopto (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5c8ee-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5c8ee-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c8ee-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5c8ee-110">Prerequisites</span></span>

<span data-ttu-id="5c8ee-111">Panopto와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-111">tooconfigure Azure AD integration with Panopto, you need hello following items:</span></span>

- <span data-ttu-id="5c8ee-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="5c8ee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5c8ee-113">Panopto Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="5c8ee-113">A Panopto single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5c8ee-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5c8ee-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5c8ee-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5c8ee-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5c8ee-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="5c8ee-118">Scenario description</span></span>
<span data-ttu-id="5c8ee-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5c8ee-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5c8ee-121">Panopto는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="5c8ee-121">Adding Panopto from hello gallery</span></span>
2. <span data-ttu-id="5c8ee-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5c8ee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panopto-from-hello-gallery"></a><span data-ttu-id="5c8ee-123">Panopto는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="5c8ee-123">Adding Panopto from hello gallery</span></span>
<span data-ttu-id="5c8ee-124">tooconfigure hello와의 통합 Panopto Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Panopto tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-124">tooconfigure hello integration of Panopto into Azure AD, you need tooadd Panopto from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5c8ee-125">**hello 갤러리에서 Panopto tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5c8ee-125">**tooadd Panopto from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c8ee-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5c8ee-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5c8ee-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="5c8ee-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="5c8ee-133">Hello 검색 상자에 입력 **Panopto**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-133">In hello search box, type **Panopto**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_search.png)

5. <span data-ttu-id="5c8ee-135">Hello 결과 패널에서 선택 **Panopto**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-135">In hello results panel, select **Panopto**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5c8ee-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5c8ee-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="5c8ee-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Panopto에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-138">In this section, you configure and test Azure AD single sign-on with Panopto based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5c8ee-139">Single sign on toowork에 대 한 Azure AD는 tooknow Panopto에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Panopto is tooa user in Azure AD.</span></span> <span data-ttu-id="5c8ee-140">즉, Azure AD 사용자와 Panopto에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-140">In other words, a link relationship between an Azure AD user and hello related user in Panopto needs toobe established.</span></span>

<span data-ttu-id="5c8ee-141">Hello hello 값을 할당, Panopto에서 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-141">In Panopto, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5c8ee-142">tooconfigure와 Panopto와 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-142">tooconfigure and test Azure AD single sign-on with Panopto, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5c8ee-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5c8ee-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5c8ee-145">**[Panopto 테스트 사용자 만들기](#creating-a-panopto-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Panopto에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-145">**[Creating a Panopto test user](#creating-a-panopto-test-user)** - toohave a counterpart of Britta Simon in Panopto that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5c8ee-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5c8ee-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5c8ee-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="5c8ee-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5c8ee-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Panopto 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Panopto application.</span></span>

<span data-ttu-id="5c8ee-150">**Azure AD tooconfigure single sign on와 Panopto를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5c8ee-150">**tooconfigure Azure AD single sign-on with Panopto, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c8ee-151">Hello hello에 Azure 포털에서에서 **Panopto** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-151">In hello Azure portal, on hello **Panopto** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="5c8ee-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_samlbase.png)

3. <span data-ttu-id="5c8ee-155">Hello에 **Panopto 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-155">On hello **Panopto Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_url.png)

    <span data-ttu-id="5c8ee-157">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<tenant-name>.panopto.com`</span><span class="sxs-lookup"><span data-stu-id="5c8ee-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.panopto.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5c8ee-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-158">This value is not real.</span></span> <span data-ttu-id="5c8ee-159">Hello로이 값을 업데이트 합니다. 실제 로그온 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="5c8ee-160">연락처 [Panopto 클라이언트 지원 팀](mailto:support@panopto.com‎) tooget이이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-160">Contact [Panopto Client support team](mailto:support@panopto.com‎) tooget this value.</span></span> 
 
4. <span data-ttu-id="5c8ee-161">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_certificate.png) 

5. <span data-ttu-id="5c8ee-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-panopto-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5c8ee-165">Hello에 **Panopto 구성** 섹션에서 클릭 **구성 Panopto** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-165">On hello **Panopto Configuration** section, click **Configure Panopto** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5c8ee-166">복사 hello **SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="5c8ee-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_configure.png) 

7. <span data-ttu-id="5c8ee-168">다른 웹 브라우저 창에서 관리자 권한으로 tooyour Panopto 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-168">In a different web browser window, log in tooyour Panopto company site as an administrator.</span></span>

8. <span data-ttu-id="5c8ee-169">Hello 왼쪽에 hello 도구 모음에서 클릭 **시스템**, 클릭 하 고 **Id 공급자**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-169">In hello toolbar on hello left, click **System**, and then click **Identity Providers**.</span></span>
   
   <span data-ttu-id="5c8ee-170">![시스템](./media/active-directory-saas-panopto-tutorial/ic777670.png "시스템")</span><span class="sxs-lookup"><span data-stu-id="5c8ee-170">![System](./media/active-directory-saas-panopto-tutorial/ic777670.png "System")</span></span>
9. <span data-ttu-id="5c8ee-171">**공급자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-171">Click **Add Provider**.</span></span>
   
   <span data-ttu-id="5c8ee-172">![ID 공급자](./media/active-directory-saas-panopto-tutorial/ic777671.png "ID 공급자")</span><span class="sxs-lookup"><span data-stu-id="5c8ee-172">![Identity Providers](./media/active-directory-saas-panopto-tutorial/ic777671.png "Identity Providers")</span></span>
   
10. <span data-ttu-id="5c8ee-173">SAML 공급자 섹션 hello hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-173">In hello SAML provider section, perform hello following steps:</span></span>
   
    <span data-ttu-id="5c8ee-174">![SaaS 구성](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS 구성")</span><span class="sxs-lookup"><span data-stu-id="5c8ee-174">![SaaS configuration](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS configuration")</span></span>
    
    <span data-ttu-id="5c8ee-175">a.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-175">a.</span></span> <span data-ttu-id="5c8ee-176">Hello에서 **공급자 유형** 목록에서 **SAML20**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-176">From hello **Provider Type** list, select **SAML20**.</span></span>    
    
    <span data-ttu-id="5c8ee-177">b.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-177">b.</span></span> <span data-ttu-id="5c8ee-178">Hello에 **인스턴스 이름을** 텍스트 상자 hello 인스턴스의 이름 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-178">In hello **Instance Name** textbox, type a name for hello instance.</span></span>

    <span data-ttu-id="5c8ee-179">c.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-179">c.</span></span> <span data-ttu-id="5c8ee-180">Hello에 **간단한 설명** 텍스트 상자에 간단한 설명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-180">In hello **Friendly Description** textbox, type a friendly description.</span></span>
    
    <span data-ttu-id="5c8ee-181">d.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-181">d.</span></span> <span data-ttu-id="5c8ee-182">**Bounce 페이지 Url** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-182">In **Bounce Page Url** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5c8ee-183">e.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-183">e.</span></span> <span data-ttu-id="5c8ee-184">Hello에 **발급자** 붙여넣기 hello 값의 텍스트 상자 **SAML 엔터티 ID**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-184">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5c8ee-185">f.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-185">f.</span></span> <span data-ttu-id="5c8ee-186">포털에서 복사의 Azure hello tooyour 클립보드의 콘텐츠를 다운로드 한 하 여 e-64로 인코딩된 인증서를 열고 다음 toohello **공개 키** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-186">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy hello content of it in tooyour clipboard, and then paste it toohello **Public Key**  textbox.</span></span>

11. <span data-ttu-id="5c8ee-187">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="5c8ee-188">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="5c8ee-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5c8ee-189">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5c8ee-190">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5c8ee-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5c8ee-191">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5c8ee-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="5c8ee-192">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="5c8ee-194">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5c8ee-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c8ee-195">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-panopto-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5c8ee-197">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-panopto-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5c8ee-199">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-panopto-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5c8ee-201">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-panopto-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5c8ee-203">a.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-203">a.</span></span> <span data-ttu-id="5c8ee-204">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5c8ee-205">b.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-205">b.</span></span> <span data-ttu-id="5c8ee-206">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5c8ee-207">c.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-207">c.</span></span> <span data-ttu-id="5c8ee-208">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5c8ee-209">d.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-209">d.</span></span> <span data-ttu-id="5c8ee-210">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-210">Click **Create**.</span></span>
 
### <a name="creating-a-panopto-test-user"></a><span data-ttu-id="5c8ee-211">Panopto 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5c8ee-211">Creating a Panopto test user</span></span>

<span data-ttu-id="5c8ee-212">사용자에 대 한 있습니다 tooconfigure tooPanopto 프로 비전 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-212">There is no action item for you tooconfigure user provisioning tooPanopto.</span></span>  
<span data-ttu-id="5c8ee-213">할당된 된 사용자의 hello 액세스 패널을 사용 하 여 tooPanopto toolog를 시도할 때 Panopto hello 사용자의 존재 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-213">When an assigned user tries toolog in tooPanopto using hello access panel, Panopto checks whether hello user exists.</span></span>  

<span data-ttu-id="5c8ee-214">사용할 수 있는 사용자 계정이 없으면 자동으로 Panopto에 의해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-214">If there is no user account available yet, it is automatically created by Panopto.</span></span>

>[!NOTE]
><span data-ttu-id="5c8ee-215">다른 Panopto 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 Azure AD 사용자 계정을 tooprovision Panopto에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-215">You can use any other Panopto user account creation tools or APIs provided by Panopto tooprovision Azure AD user accounts.</span></span>
>
>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5c8ee-216">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5c8ee-217">이 섹션에서는 tooPanopto 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPanopto.</span></span>

![사용자 할당][200] 

<span data-ttu-id="5c8ee-219">**tooassign Britta Simon tooPanopto hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5c8ee-219">**tooassign Britta Simon tooPanopto, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c8ee-220">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="5c8ee-222">Hello 응용 프로그램 목록에서 선택 **Panopto**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-222">In hello applications list, select **Panopto**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_app.png) 

3. <span data-ttu-id="5c8ee-224">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="5c8ee-226">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-226">Click **Add** button.</span></span> <span data-ttu-id="5c8ee-227">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="5c8ee-229">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5c8ee-230">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5c8ee-231">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5c8ee-232">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="5c8ee-232">Testing single sign-on</span></span>

<span data-ttu-id="5c8ee-233">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5c8ee-234">Hello 액세스 패널에서에서 hello Panopto 타일을 클릭할 때를 받아야 하며 자동으로 Panopto 응용 프로그램의 로그인 페이지.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-234">When you click hello Panopto tile in hello Access Panel, you should get automatically login page of Panopto application.</span></span>
<span data-ttu-id="5c8ee-235">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5c8ee-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5c8ee-236">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5c8ee-236">Additional resources</span></span>

* [<span data-ttu-id="5c8ee-237">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="5c8ee-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5c8ee-238">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="5c8ee-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_203.png

