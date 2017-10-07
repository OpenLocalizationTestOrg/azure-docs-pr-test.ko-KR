---
title: "자습서: PerformanceCentre와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 PerformanceCentre 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65288c32-f7e6-4eb3-a6dc-523c3d748d1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 19781c0087093a67c70dc90072cf1a119bb2ade0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-performancecentre"></a><span data-ttu-id="6348d-103">자습서: PerformanceCentre와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="6348d-103">Tutorial: Azure Active Directory integration with PerformanceCentre</span></span>

<span data-ttu-id="6348d-104">이 자습서에 설명 어떻게 toointegrate PerformanceCentre Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6348d-104">In this tutorial, you learn how toointegrate PerformanceCentre with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6348d-105">다음 이점을 hello로 제공 PerformanceCentre Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="6348d-105">Integrating PerformanceCentre with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6348d-106">액세스 tooPerformanceCentre을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-106">You can control in Azure AD who has access tooPerformanceCentre</span></span>
- <span data-ttu-id="6348d-107">프로그램 사용자 tooautomatically get 로그온 tooPerformanceCentre (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-107">You can enable your users tooautomatically get signed-on tooPerformanceCentre (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6348d-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6348d-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6348d-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6348d-110">Prerequisites</span></span>

<span data-ttu-id="6348d-111">다음 항목 hello가 필요 tooconfigure PerformanceCentre와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-111">tooconfigure Azure AD integration with PerformanceCentre, you need hello following items:</span></span>

- <span data-ttu-id="6348d-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="6348d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6348d-113">PerformanceCentre Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="6348d-113">A PerformanceCentre single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6348d-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6348d-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6348d-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="6348d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6348d-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6348d-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="6348d-118">Scenario description</span></span>
<span data-ttu-id="6348d-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6348d-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6348d-121">PerformanceCentre는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="6348d-121">Adding PerformanceCentre from hello gallery</span></span>
2. <span data-ttu-id="6348d-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="6348d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-performancecentre-from-hello-gallery"></a><span data-ttu-id="6348d-123">PerformanceCentre는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="6348d-123">Adding PerformanceCentre from hello gallery</span></span>
<span data-ttu-id="6348d-124">tooconfigure hello와의 통합 PerformanceCentre Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 PerformanceCentre tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-124">tooconfigure hello integration of PerformanceCentre into Azure AD, you need tooadd PerformanceCentre from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6348d-125">**hello 갤러리에서 PerformanceCentre tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6348d-125">**tooadd PerformanceCentre from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6348d-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6348d-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6348d-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="6348d-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="6348d-133">Hello 검색 상자에 입력 **PerformanceCentre**합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-133">In hello search box, type **PerformanceCentre**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_search.png)

5. <span data-ttu-id="6348d-135">Hello 결과 패널에서 선택 **PerformanceCentre**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-135">In hello results panel, select **PerformanceCentre**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6348d-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="6348d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6348d-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 PerformanceCentre에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-138">In this section, you configure and test Azure AD single sign-on with PerformanceCentre based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6348d-139">Single sign on toowork에 대 한 Azure AD는 tooknow PerformanceCentre에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PerformanceCentre is tooa user in Azure AD.</span></span> <span data-ttu-id="6348d-140">즉, Azure AD 사용자 및 PerformanceCentre에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-140">In other words, a link relationship between an Azure AD user and hello related user in PerformanceCentre needs toobe established.</span></span>

<span data-ttu-id="6348d-141">PerformanceCentre에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-141">In PerformanceCentre, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6348d-142">tooconfigure 및 PerformanceCentre 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-142">tooconfigure and test Azure AD single sign-on with PerformanceCentre, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6348d-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6348d-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6348d-145">**[PerformanceCentre 테스트 사용자 만들기](#creating-a-performancecentre-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 PerformanceCentre에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-145">**[Creating a PerformanceCentre test user](#creating-a-performancecentre-test-user)** - toohave a counterpart of Britta Simon in PerformanceCentre that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6348d-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6348d-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="6348d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6348d-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="6348d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6348d-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 PerformanceCentre 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PerformanceCentre application.</span></span>

<span data-ttu-id="6348d-150">**tooconfigure Azure AD single sign on, PerformanceCentre와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6348d-150">**tooconfigure Azure AD single sign-on with PerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="6348d-151">Hello hello에 Azure 포털에서에서 **PerformanceCentre** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-151">In hello Azure portal, on hello **PerformanceCentre** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="6348d-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_samlbase.png)

3. <span data-ttu-id="6348d-155">Hello에 **PerformanceCentre 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-155">On hello **PerformanceCentre Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_url.png)

    <span data-ttu-id="6348d-157">a.</span><span class="sxs-lookup"><span data-stu-id="6348d-157">a.</span></span> <span data-ttu-id="6348d-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`http://companyname.performancecentre.com/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="6348d-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://companyname.performancecentre.com/saml/SSO`</span></span>

    <span data-ttu-id="6348d-159">b.</span><span class="sxs-lookup"><span data-stu-id="6348d-159">b.</span></span> <span data-ttu-id="6348d-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`http://companyname.performancecentre.com`</span><span class="sxs-lookup"><span data-stu-id="6348d-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://companyname.performancecentre.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6348d-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-161">These values are not real.</span></span> <span data-ttu-id="6348d-162">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6348d-163">연락처 [PerformanceCentre 클라이언트 지원 팀](https://www.performancecentre.com/contact-us/) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-163">Contact [PerformanceCentre Client support team](https://www.performancecentre.com/contact-us/) tooget these values.</span></span> 

4. <span data-ttu-id="6348d-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_certificate.png) 

5. <span data-ttu-id="6348d-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-performancecentre-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6348d-168">Hello에 **PerformanceCentre 구성** 섹션에서 클릭 **구성 PerformanceCentre** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="6348d-168">On hello **PerformanceCentre Configuration** section, click **Configure PerformanceCentre** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6348d-169">복사 hello **SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="6348d-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_configure.png) 

7. <span data-ttu-id="6348d-171">로그온 tooyour **PerformanceCentre** 회사 사이트에서 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-171">Sign-on tooyour **PerformanceCentre** company site as administrator.</span></span>

8. <span data-ttu-id="6348d-172">Hello 왼쪽에 hello 탭을 클릭 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-172">In hello tab on hello left side, click **Configure**.</span></span>
   
    ![Azure AD Single Sign-On][10]

9. <span data-ttu-id="6348d-174">Hello 왼쪽에 hello 탭을 클릭 **기타**, 클릭 하 고 **Single Sign On**합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-174">In hello tab on hello left side, click **Miscellaneous**, and then click **Single Sign On**.</span></span>
   
    ![Azure AD Single Sign-On][11]

10. <span data-ttu-id="6348d-176">**프로토콜**로 **SAML**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-176">As **Protocol**, select **SAML**.</span></span>
   
    ![Azure AD Single Sign-On][12]

11. <span data-ttu-id="6348d-178">열기 hello 콘텐츠 복사를 메모장에서 다운로드 한 메타 데이터 파일에 붙여 넣을 hello **Id 공급자 메타 데이터** 입력란을 클릭 하 고 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-178">Open your downloaded metadata file in notepad, copy hello content, paste it into hello **Identity Provider Metadata** textbox, and then click **Save**.</span></span>
   
    ![Azure AD Single Sign-On][13]

12. <span data-ttu-id="6348d-180">에 대 한 hello 값 hello 있는지 확인 하십시오. **엔터티 기준 URL** 및 **엔터티 ID URL** 올바른지 합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-180">Verify that hello values for hello **Entity Base URL** and **Entity ID URL** are correct.</span></span>
    
     ![Azure AD Single Sign-On][14]

> [!TIP]
> <span data-ttu-id="6348d-182">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="6348d-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6348d-183">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="6348d-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6348d-184">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6348d-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6348d-185">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="6348d-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="6348d-186">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="6348d-188">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6348d-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6348d-189">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6348d-191">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6348d-193">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6348d-195">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6348d-197">a.</span><span class="sxs-lookup"><span data-stu-id="6348d-197">a.</span></span> <span data-ttu-id="6348d-198">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6348d-199">b.</span><span class="sxs-lookup"><span data-stu-id="6348d-199">b.</span></span> <span data-ttu-id="6348d-200">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6348d-201">c.</span><span class="sxs-lookup"><span data-stu-id="6348d-201">c.</span></span> <span data-ttu-id="6348d-202">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6348d-203">d.</span><span class="sxs-lookup"><span data-stu-id="6348d-203">d.</span></span> <span data-ttu-id="6348d-204">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-204">Click **Create**.</span></span>
 
### <a name="creating-a-performancecentre-test-user"></a><span data-ttu-id="6348d-205">PerformanceCentre 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="6348d-205">Creating a PerformanceCentre test user</span></span>

<span data-ttu-id="6348d-206">hello이이 섹션의 목적은 toocreate Britta Simon PerformanceCentre에서 호출 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-206">hello objective of this section is toocreate a user called Britta Simon in PerformanceCentre.</span></span>

<span data-ttu-id="6348d-207">**toocreate Britta Simon PerformanceCentre의 라는 사용자를 만들면 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6348d-207">**toocreate a user called Britta Simon in PerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="6348d-208">관리자 권한으로 PerformanceCentre 회사 사이트 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-208">Sign on tooyour PerformanceCentre company site as administrator.</span></span>

2. <span data-ttu-id="6348d-209">Hello hello 왼쪽 메뉴를 클릭 **Interrelate**, 클릭 하 고 **참가자 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-209">In hello menu on hello left, click **Interrelate**, and then click **Create Participant**.</span></span>
   
    ![사용자 만들기][400]

3. <span data-ttu-id="6348d-211">Hello에 **상호 연관 되어 있는지-참가자 만들기** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-211">On hello **Interrelate - Create Participant** dialog, perform hello following steps:</span></span>
   
    ![사용자 만들기][401]
    
    <span data-ttu-id="6348d-213">a.</span><span class="sxs-lookup"><span data-stu-id="6348d-213">a.</span></span> <span data-ttu-id="6348d-214">Britta Simon에 대 한 hello 필요한 특성을 관련된 텍스트 상자에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-214">Type hello required attributes for Britta Simon into related textboxes.</span></span>
    
    >[!IMPORTANT]
    ><span data-ttu-id="6348d-215">PerformanceCentre의 특성 해야 Britta의 사용자 이름 hello Azure AD에서 사용자 이름 hello와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-215">Britta's User Name attribute in PerformanceCentre must be hello same as hello User Name in Azure AD.</span></span>
    
    <span data-ttu-id="6348d-216">b.</span><span class="sxs-lookup"><span data-stu-id="6348d-216">b.</span></span> <span data-ttu-id="6348d-217">**클라이언트 관리자**로 **역할 선택**을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-217">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="6348d-218">c.</span><span class="sxs-lookup"><span data-stu-id="6348d-218">c.</span></span> <span data-ttu-id="6348d-219">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-219">Click **Save**.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6348d-220">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6348d-221">이 섹션에서는 tooPerformanceCentre 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPerformanceCentre.</span></span>

![사용자 할당][200] 

<span data-ttu-id="6348d-223">**tooassign Britta Simon tooPerformanceCentre hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6348d-223">**tooassign Britta Simon tooPerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="6348d-224">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="6348d-226">Hello 응용 프로그램 목록에서 선택 **PerformanceCentre**합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-226">In hello applications list, select **PerformanceCentre**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_app.png) 

3. <span data-ttu-id="6348d-228">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="6348d-230">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-230">Click **Add** button.</span></span> <span data-ttu-id="6348d-231">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="6348d-233">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6348d-234">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6348d-235">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6348d-236">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="6348d-236">Testing single sign-on</span></span>

<span data-ttu-id="6348d-237">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD SSO 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-237">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="6348d-238">Hello 액세스 패널에서에서 hello PerformanceCentre 타일을 클릭할 때 자동으로 로그온 tooyour PerformanceCentre 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6348d-238">When you click hello PerformanceCentre tile in hello Access Panel, you should get automatically signed-on tooyour PerformanceCentre application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6348d-239">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="6348d-239">Additional resources</span></span>

* [<span data-ttu-id="6348d-240">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="6348d-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6348d-241">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="6348d-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_06.png
[11]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_07.png
[12]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_08.png
[13]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_09.png
[14]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_10.png

[100]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_11.png
[401]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_12.png

