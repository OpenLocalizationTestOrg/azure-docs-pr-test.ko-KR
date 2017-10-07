---
title: "자습서: NetDocuments와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 NetDocuments 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1a47dc42-1a17-48a2-965e-eca4cfb2f197
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ee9887553595a2492642aed4cb4abcd11d9cf599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netdocuments"></a><span data-ttu-id="36b12-103">자습서: NetDocuments와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="36b12-103">Tutorial: Azure Active Directory integration with NetDocuments</span></span>

<span data-ttu-id="36b12-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 NetDocuments 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-104">In this tutorial, you learn how toointegrate NetDocuments with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="36b12-105">Azure AD와 NetDocuments 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-105">Integrating NetDocuments with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="36b12-106">액세스 tooNetDocuments을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-106">You can control in Azure AD who has access tooNetDocuments</span></span>
- <span data-ttu-id="36b12-107">프로그램 사용자 tooautomatically get 로그온 tooNetDocuments (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-107">You can enable your users tooautomatically get signed-on tooNetDocuments (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="36b12-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="36b12-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36b12-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="36b12-110">Prerequisites</span></span>

<span data-ttu-id="36b12-111">NetDocuments와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-111">tooconfigure Azure AD integration with NetDocuments, you need hello following items:</span></span>

- <span data-ttu-id="36b12-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="36b12-112">An Azure AD subscription</span></span>
- <span data-ttu-id="36b12-113">NetDocuments Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="36b12-113">A NetDocuments single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="36b12-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="36b12-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="36b12-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="36b12-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="36b12-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="36b12-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="36b12-118">Scenario description</span></span>
<span data-ttu-id="36b12-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="36b12-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="36b12-121">NetDocuments는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="36b12-121">Adding NetDocuments from hello gallery</span></span>
2. <span data-ttu-id="36b12-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="36b12-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netdocuments-from-hello-gallery"></a><span data-ttu-id="36b12-123">NetDocuments는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="36b12-123">Adding NetDocuments from hello gallery</span></span>
<span data-ttu-id="36b12-124">tooconfigure hello와의 통합 NetDocuments Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 NetDocuments tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-124">tooconfigure hello integration of NetDocuments into Azure AD, you need tooadd NetDocuments from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="36b12-125">**NetDocuments hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="36b12-125">**tooadd NetDocuments from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="36b12-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="36b12-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="36b12-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="36b12-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="36b12-133">Hello 검색 상자에 입력 **NetDocuments**합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-133">In hello search box, type **NetDocuments**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_search.png)

5. <span data-ttu-id="36b12-135">Hello 결과 패널에서 선택 **NetDocuments**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-135">In hello results panel, select **NetDocuments**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="36b12-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="36b12-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="36b12-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 NetDocuments에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-138">In this section, you configure and test Azure AD single sign-on with NetDocuments based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="36b12-139">Single sign on toowork에 대 한 Azure AD는 tooknow NetDocuments에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in NetDocuments is tooa user in Azure AD.</span></span> <span data-ttu-id="36b12-140">즉, Azure AD 사용자와 NetDocuments에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-140">In other words, a link relationship between an Azure AD user and hello related user in NetDocuments needs toobe established.</span></span>

<span data-ttu-id="36b12-141">NetDocuments에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-141">In NetDocuments, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="36b12-142">tooconfigure와 NetDocuments 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-142">tooconfigure and test Azure AD single sign-on with NetDocuments, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="36b12-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="36b12-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="36b12-145">**[NetDocuments 테스트 사용자 만들기](#creating-a-netdocuments-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 NetDocuments에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-145">**[Creating a NetDocuments test user](#creating-a-netdocuments-test-user)** - toohave a counterpart of Britta Simon in NetDocuments that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="36b12-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="36b12-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="36b12-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="36b12-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="36b12-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="36b12-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 NetDocuments 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your NetDocuments application.</span></span>

<span data-ttu-id="36b12-150">**Azure AD tooconfigure single sign on와 NetDocuments를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="36b12-150">**tooconfigure Azure AD single sign-on with NetDocuments, perform hello following steps:**</span></span>

1. <span data-ttu-id="36b12-151">Hello hello에 Azure 포털에서에서 **NetDocuments** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-151">In hello Azure portal, on hello **NetDocuments** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="36b12-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_samlbase.png)

3. <span data-ttu-id="36b12-155">Hello에 **NetDocuments 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-155">On hello **NetDocuments Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_url.png)

    <span data-ttu-id="36b12-157">a.</span><span class="sxs-lookup"><span data-stu-id="36b12-157">a.</span></span> <span data-ttu-id="36b12-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="36b12-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    <span data-ttu-id="36b12-159">b.</span><span class="sxs-lookup"><span data-stu-id="36b12-159">b.</span></span> <span data-ttu-id="36b12-160">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="36b12-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="36b12-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-161">These values are not real.</span></span> <span data-ttu-id="36b12-162">Hello 실제 로그온 URL와 회신 URL이 이러한 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-162">Update these values with hello actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="36b12-163">연락처 [NetDocuments 지원 팀](https://support.netdocuments.com/hc/) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-163">Contact [NetDocuments support team](https://support.netdocuments.com/hc/) tooget these values.</span></span>
 
4. <span data-ttu-id="36b12-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_certificate.png) 

5. <span data-ttu-id="36b12-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-netdocuments-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="36b12-168">다른 웹 브라우저 창에서 NetDocuments 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-168">In a different web browser window, log into your NetDocuments company site as an administrator.</span></span>

7. <span data-ttu-id="36b12-169">너무 이동**Admin**합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-169">Go too**Admin**.</span></span>

8. <span data-ttu-id="36b12-170">**사용자와 그룹 추가 및 제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-170">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="36b12-171">![리포지토리](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "리포지토리")</span><span class="sxs-lookup"><span data-stu-id="36b12-171">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

9. <span data-ttu-id="36b12-172">**고급 인증 옵션 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-172">Click **Configure advanced authentication options**.</span></span>
    
    <span data-ttu-id="36b12-173">![고급 인증 옵션 구성](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "고급 인증 옵션 구성")</span><span class="sxs-lookup"><span data-stu-id="36b12-173">![Configure advanced authentication options](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configure advanced authentication options")</span></span>

10. <span data-ttu-id="36b12-174">Hello에 **페더레이션 Id** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-174">On hello **Federated Identity** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="36b12-175">![페더레이션 ID](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "페더레이션 ID")</span><span class="sxs-lookup"><span data-stu-id="36b12-175">![Federated Identitty](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Federated Identitty")</span></span>
   
    <span data-ttu-id="36b12-176">a.</span><span class="sxs-lookup"><span data-stu-id="36b12-176">a.</span></span> <span data-ttu-id="36b12-177">**페더레이션 ID 서버 유형**으로 **Active Directory Federation Services**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-177">As **Federated identity server type**, select **Active Directory Federation Services**.</span></span>
   
    <span data-ttu-id="36b12-178">b.</span><span class="sxs-lookup"><span data-stu-id="36b12-178">b.</span></span> <span data-ttu-id="36b12-179">클릭 **파일 선택**, tooupload hello Azure 포털에서 다운로드 한 메타 데이터 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-179">Click **Choose file**, tooupload hello downloaded metadata file which you have downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="36b12-180">c.</span><span class="sxs-lookup"><span data-stu-id="36b12-180">c.</span></span> <span data-ttu-id="36b12-181">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-181">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="36b12-182">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="36b12-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="36b12-183">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="36b12-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="36b12-184">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="36b12-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="36b12-185">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="36b12-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="36b12-186">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="36b12-188">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="36b12-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="36b12-189">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="36b12-191">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="36b12-193">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="36b12-195">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="36b12-197">a.</span><span class="sxs-lookup"><span data-stu-id="36b12-197">a.</span></span> <span data-ttu-id="36b12-198">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="36b12-199">b.</span><span class="sxs-lookup"><span data-stu-id="36b12-199">b.</span></span> <span data-ttu-id="36b12-200">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="36b12-201">c.</span><span class="sxs-lookup"><span data-stu-id="36b12-201">c.</span></span> <span data-ttu-id="36b12-202">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="36b12-203">d.</span><span class="sxs-lookup"><span data-stu-id="36b12-203">d.</span></span> <span data-ttu-id="36b12-204">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-204">Click **Create**.</span></span>
 
### <a name="creating-a-netdocuments-test-user"></a><span data-ttu-id="36b12-205">NetDocuments 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="36b12-205">Creating a NetDocuments test user</span></span>

<span data-ttu-id="36b12-206">tooenable Azure AD 사용자가 toolog tooNetDocuments에서 프로 비전 해야 NetDocuments에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-206">tooenable Azure AD users toolog in tooNetDocuments, they must be provisioned into NetDocuments.</span></span>  
<span data-ttu-id="36b12-207">Hello NetDocuments의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-207">In hello case of NetDocuments, provisioning is a manual task.</span></span>

<span data-ttu-id="36b12-208">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="36b12-208">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="36b12-209">Tooyour에 등록 하는 **NetDocuments** 회사 사이트에서 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-209">Sing on tooyour **NetDocuments** company site as administrator.</span></span>

2. <span data-ttu-id="36b12-210">Hello 메뉴에서 hello 위에 표시를 클릭 **Admin**합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-210">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="36b12-211">![관리자](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="36b12-211">![Admin](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Admin")</span></span>

3. <span data-ttu-id="36b12-212">**사용자와 그룹 추가 및 제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-212">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="36b12-213">![리포지토리](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "리포지토리")</span><span class="sxs-lookup"><span data-stu-id="36b12-213">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

4. <span data-ttu-id="36b12-214">Hello에 **전자 메일 주소** textbox tooprovision을 클릭 한 다음 유효한 Azure Active Directory 계정의 hello 전자 메일 주소를 입력 **사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-214">In hello **Email Address** textbox, type hello email address of a valid Azure Active Directory account you want tooprovision, and then click **Add User**.</span></span>
   
    <span data-ttu-id="36b12-215">![전자 메일 주소](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "전자 메일 주소")</span><span class="sxs-lookup"><span data-stu-id="36b12-215">![Email Address](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Email Address")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="36b12-216">hello Azure Active Directory 계정 소유자는 데이터베이스가 활성화 전에 tooconfirm hello 계정 연결을 포함 하는 전자 메일을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-216">hello Azure Active Directory account holder will get an email that includes a link tooconfirm hello account before it becomes active.</span></span> <span data-ttu-id="36b12-217">다른 NetDocuments 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 사용자 계정이 NetDocuments tooprovision Azure Active Directory에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-217">You can use any other NetDocuments user account creation tools or APIs provided by NetDocuments tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="36b12-218">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="36b12-219">이 섹션에서는 tooNetDocuments 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNetDocuments.</span></span>

![사용자 할당][200] 

<span data-ttu-id="36b12-221">**tooassign Britta Simon tooNetDocuments hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="36b12-221">**tooassign Britta Simon tooNetDocuments, perform hello following steps:**</span></span>

1. <span data-ttu-id="36b12-222">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="36b12-224">Hello 응용 프로그램 목록에서 선택 **NetDocuments**합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-224">In hello applications list, select **NetDocuments**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_app.png) 

3. <span data-ttu-id="36b12-226">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="36b12-228">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-228">Click **Add** button.</span></span> <span data-ttu-id="36b12-229">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="36b12-231">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="36b12-232">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="36b12-233">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="36b12-234">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="36b12-234">Testing single sign-on</span></span>

<span data-ttu-id="36b12-235">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="36b12-236">Hello NetDocuments hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour NetDocuments 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-236">When you click hello NetDocuments tile in hello Access Panel, you should get automatically signed-on tooyour NetDocuments application.</span></span>
<span data-ttu-id="36b12-237">액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="36b12-237">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="36b12-238">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="36b12-238">Additional resources</span></span>

* [<span data-ttu-id="36b12-239">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="36b12-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="36b12-240">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="36b12-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_203.png

