---
title: "자습서: LogicMonitor와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 LogicMonitor 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 496156c3-0e22-4492-b36f-2c29c055e087
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: ea5cb8b574d763cb114286e3b2a5c94ab5546756
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-logicmonitor"></a><span data-ttu-id="48b53-103">자습서: LogicMonitor와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="48b53-103">Tutorial: Azure Active Directory integration with LogicMonitor</span></span>

<span data-ttu-id="48b53-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 LogicMonitor 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-104">In this tutorial, you learn how toointegrate LogicMonitor with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="48b53-105">Azure AD와 LogicMonitor 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-105">Integrating LogicMonitor with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="48b53-106">액세스 tooLogicMonitor을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-106">You can control in Azure AD who has access tooLogicMonitor</span></span>
- <span data-ttu-id="48b53-107">프로그램 사용자 tooautomatically get 로그온 tooLogicMonitor (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-107">You can enable your users tooautomatically get signed-on tooLogicMonitor (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="48b53-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="48b53-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48b53-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="48b53-110">Prerequisites</span></span>

<span data-ttu-id="48b53-111">LogicMonitor와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-111">tooconfigure Azure AD integration with LogicMonitor, you need hello following items:</span></span>

- <span data-ttu-id="48b53-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="48b53-112">An Azure AD subscription</span></span>
- <span data-ttu-id="48b53-113">LogicMonitor Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="48b53-113">A LogicMonitor single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="48b53-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="48b53-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="48b53-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="48b53-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="48b53-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="48b53-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="48b53-118">Scenario description</span></span>
<span data-ttu-id="48b53-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="48b53-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="48b53-121">LogicMonitor는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="48b53-121">Adding LogicMonitor from hello gallery</span></span>
2. <span data-ttu-id="48b53-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="48b53-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-logicmonitor-from-hello-gallery"></a><span data-ttu-id="48b53-123">LogicMonitor는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="48b53-123">Adding LogicMonitor from hello gallery</span></span>
<span data-ttu-id="48b53-124">tooconfigure hello와의 통합 LogicMonitor Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 LogicMonitor tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-124">tooconfigure hello integration of LogicMonitor into Azure AD, you need tooadd LogicMonitor from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="48b53-125">**LogicMonitor hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="48b53-125">**tooadd LogicMonitor from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="48b53-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="48b53-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="48b53-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="48b53-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="48b53-133">Hello 검색 상자에 입력 **LogicMonitor**합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-133">In hello search box, type **LogicMonitor**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_search.png)

5. <span data-ttu-id="48b53-135">Hello 결과 패널에서 선택 **LogicMonitor**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-135">In hello results panel, select **LogicMonitor**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="48b53-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="48b53-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="48b53-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 LogicMonitor에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-138">In this section, you configure and test Azure AD single sign-on with LogicMonitor based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="48b53-139">Single sign on toowork에 대 한 Azure AD는 tooknow LogicMonitor에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LogicMonitor is tooa user in Azure AD.</span></span> <span data-ttu-id="48b53-140">즉, Azure AD 사용자와 LogicMonitor에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-140">In other words, a link relationship between an Azure AD user and hello related user in LogicMonitor needs toobe established.</span></span>

<span data-ttu-id="48b53-141">Hello hello 값을 할당, LogicMonitor에서 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-141">In LogicMonitor, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="48b53-142">tooconfigure와 LogicMonitor 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-142">tooconfigure and test Azure AD single sign-on with LogicMonitor, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="48b53-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="48b53-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="48b53-145">**[LogicMonitor 테스트 사용자 만들기](#creating-a-logicmonitor-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 LogicMonitor에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-145">**[Creating a LogicMonitor test user](#creating-a-logicmonitor-test-user)** - toohave a counterpart of Britta Simon in LogicMonitor that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="48b53-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="48b53-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="48b53-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="48b53-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="48b53-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="48b53-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 LogicMonitor 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LogicMonitor application.</span></span>

<span data-ttu-id="48b53-150">**Azure AD tooconfigure single sign on와 LogicMonitor를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="48b53-150">**tooconfigure Azure AD single sign-on with LogicMonitor, perform hello following steps:**</span></span>

1. <span data-ttu-id="48b53-151">Hello hello에 Azure 포털에서에서 **LogicMonitor** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-151">In hello Azure portal, on hello **LogicMonitor** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="48b53-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_samlbase.png)

3. <span data-ttu-id="48b53-155">Hello에 **LogicMonitor 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-155">On hello **LogicMonitor Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_url.png)

    <span data-ttu-id="48b53-157">a.</span><span class="sxs-lookup"><span data-stu-id="48b53-157">a.</span></span> <span data-ttu-id="48b53-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="48b53-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    <span data-ttu-id="48b53-159">b.</span><span class="sxs-lookup"><span data-stu-id="48b53-159">b.</span></span> <span data-ttu-id="48b53-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="48b53-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="48b53-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-161">These values are not real.</span></span> <span data-ttu-id="48b53-162">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="48b53-163">연락처 [LogicMonitor 클라이언트 지원 팀](https://www.logicmonitor.com/contact/) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-163">Contact [LogicMonitor Client support team](https://www.logicmonitor.com/contact/) tooget these values.</span></span> 
 


4. <span data-ttu-id="48b53-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_certificate.png) 

5. <span data-ttu-id="48b53-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="48b53-168">Tooyour 로그인 **LogicMonitor** 회사 사이트에 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-168">Log in tooyour **LogicMonitor** company site as an administrator.</span></span>

7. <span data-ttu-id="48b53-169">Hello 메뉴에서 hello 위에 표시를 클릭 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-169">In hello menu on hello top, click **Settings**.</span></span>
   
   <span data-ttu-id="48b53-170">![설정](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "설정")</span><span class="sxs-lookup"><span data-stu-id="48b53-170">![Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Settings")</span></span>

8. <span data-ttu-id="48b53-171">Hello hello 왼쪽 탐색 창, 클릭 **Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="48b53-171">In hello navigation bat on hello left side, click **Single Sign On**</span></span>
   
   <span data-ttu-id="48b53-172">![Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="48b53-172">![Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Single Sign-On")</span></span>

9. <span data-ttu-id="48b53-173">Hello에 **Single sign-on (SSO) 설정을** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-173">In hello **Single Sign-on (SSO) settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="48b53-174">![Single Sign-On 설정](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Single Sign-On 설정")</span><span class="sxs-lookup"><span data-stu-id="48b53-174">![Single Sign-On Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="48b53-175">a.</span><span class="sxs-lookup"><span data-stu-id="48b53-175">a.</span></span> <span data-ttu-id="48b53-176">**Single Sign-On 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-176">Select **Enable Single Sign-on**.</span></span>

   <span data-ttu-id="48b53-177">b.</span><span class="sxs-lookup"><span data-stu-id="48b53-177">b.</span></span> <span data-ttu-id="48b53-178">**기본 역할 할당**으로 **readonly**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-178">As **Default Role Assignment**, select **readonly**.</span></span>
   
   <span data-ttu-id="48b53-179">c.</span><span class="sxs-lookup"><span data-stu-id="48b53-179">c.</span></span> <span data-ttu-id="48b53-180">메모장에서 다운로드 한 hello 메타 데이터 파일을 열고 hello에 hello 파일의 내용을 붙여 **Id 공급자 메타 데이터** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-180">Open hello downloaded metadata file in notepad, and then paste content of hello file into hello **Identity Provider Metadata** textbox.</span></span>
   
   <span data-ttu-id="48b53-181">d.</span><span class="sxs-lookup"><span data-stu-id="48b53-181">d.</span></span> <span data-ttu-id="48b53-182">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="48b53-183">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="48b53-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="48b53-184">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="48b53-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="48b53-185">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="48b53-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="48b53-186">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="48b53-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="48b53-187">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="48b53-189">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="48b53-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="48b53-190">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="48b53-192">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="48b53-194">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="48b53-196">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="48b53-198">a.</span><span class="sxs-lookup"><span data-stu-id="48b53-198">a.</span></span> <span data-ttu-id="48b53-199">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="48b53-200">b.</span><span class="sxs-lookup"><span data-stu-id="48b53-200">b.</span></span> <span data-ttu-id="48b53-201">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="48b53-202">c.</span><span class="sxs-lookup"><span data-stu-id="48b53-202">c.</span></span> <span data-ttu-id="48b53-203">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="48b53-204">d.</span><span class="sxs-lookup"><span data-stu-id="48b53-204">d.</span></span> <span data-ttu-id="48b53-205">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-205">Click **Create**.</span></span>
 
### <a name="creating-a-logicmonitor-test-user"></a><span data-ttu-id="48b53-206">LogicMonitor 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="48b53-206">Creating a LogicMonitor test user</span></span>

<span data-ttu-id="48b53-207">AAD 사용자 toobe 수 toosign에서, 프로 비전 된 toohello LogicMonitor 응용 프로그램의 경우 Azure Active Directory 사용자 이름을 사용 하 여 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-207">For AAD users toobe able toosign in, they must be provisioned toohello LogicMonitor application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="48b53-208">**tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:**</span><span class="sxs-lookup"><span data-stu-id="48b53-208">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="48b53-209">관리자 권한으로 LogicMonitor 회사 사이트 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-209">Log in tooyour LogicMonitor company site as an administrator.</span></span>

2. <span data-ttu-id="48b53-210">Hello 메뉴에서 hello 위에 표시를 클릭 **설정**, 클릭 하 고 **역할 및 사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-210">In hello menu on hello top, click **Settings**, and then click **Roles and Users**.</span></span>
   
   <span data-ttu-id="48b53-211">![역할 및 사용자](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "역할 및 사용자")</span><span class="sxs-lookup"><span data-stu-id="48b53-211">![Roles and Users](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Roles and Users")</span></span>

3. <span data-ttu-id="48b53-212">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-212">Click **Add**.</span></span>

4. <span data-ttu-id="48b53-213">Hello에 **계정 추가** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-213">In hello **Add an account** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="48b53-214">![계정 추가](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "계정 추가")</span><span class="sxs-lookup"><span data-stu-id="48b53-214">![Add an account](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Add an account")</span></span>
   
   <span data-ttu-id="48b53-215">a.</span><span class="sxs-lookup"><span data-stu-id="48b53-215">a.</span></span> <span data-ttu-id="48b53-216">형식 hello **Username**, **전자 메일**, **암호**, 및 **암호 다시 입력** 원하는 hello Azure Active Directory 사용자의 값 hello에 tooprovision 관련 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-216">Type hello **Username**, **Email**, **Password**, and **Retype password** values of hello Azure Active Directory user you want tooprovision into hello related textboxes.</span></span>
   
   <span data-ttu-id="48b53-217">b.</span><span class="sxs-lookup"><span data-stu-id="48b53-217">b.</span></span> <span data-ttu-id="48b53-218">선택 **역할**, **사용 권한 보기**, 및 hello **상태**합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-218">Select **Roles**, **View Permissions**, and hello **Status**.</span></span>
   
   <span data-ttu-id="48b53-219">c.</span><span class="sxs-lookup"><span data-stu-id="48b53-219">c.</span></span> <span data-ttu-id="48b53-220">**제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-220">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="48b53-221">다른 LogicMonitor 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 사용자 계정을 LogicMonitor tooprovision Azure Active Directory에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-221">You can use any other LogicMonitor user account creation tools or APIs provided by LogicMonitor tooprovision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="48b53-222">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-222">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="48b53-223">이 섹션에서는 tooLogicMonitor 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-223">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLogicMonitor.</span></span>

![사용자 할당][200] 

<span data-ttu-id="48b53-225">**tooassign Britta Simon tooLogicMonitor hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="48b53-225">**tooassign Britta Simon tooLogicMonitor, perform hello following steps:**</span></span>

1. <span data-ttu-id="48b53-226">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-226">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="48b53-228">Hello 응용 프로그램 목록에서 선택 **LogicMonitor**합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-228">In hello applications list, select **LogicMonitor**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_app.png) 

3. <span data-ttu-id="48b53-230">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-230">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="48b53-232">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-232">Click **Add** button.</span></span> <span data-ttu-id="48b53-233">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="48b53-235">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-235">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="48b53-236">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="48b53-237">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="48b53-238">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="48b53-238">Testing single sign-on</span></span>

<span data-ttu-id="48b53-239">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-239">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="48b53-240">Hello 액세스 패널에서에서 hello LogicMonitor 타일을 클릭할 때 자동으로 로그온 tooyour LogicMonitor 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-240">When you click hello LogicMonitor tile in hello Access Panel, you should get automatically signed-on tooyour LogicMonitor application.</span></span>
<span data-ttu-id="48b53-241">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="48b53-241">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="48b53-242">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="48b53-242">Additional resources</span></span>

* [<span data-ttu-id="48b53-243">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="48b53-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="48b53-244">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="48b53-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_203.png

