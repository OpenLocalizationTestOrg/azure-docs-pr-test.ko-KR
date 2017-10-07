---
title: "자습서: Lifesize Cloud와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Lifesize 클라우드 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ae599907e872571b3220de7122006c7db8db4a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a><span data-ttu-id="30d3d-103">자습서: Lifesize Cloud와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="30d3d-103">Tutorial: Azure Active Directory integration with Lifesize Cloud</span></span>

<span data-ttu-id="30d3d-104">이 자습서에 설명 toointegrate Lifesize 하 여 클라우드로 Azure Active Directory (Azure AD) 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-104">In this tutorial, you learn how toointegrate Lifesize Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="30d3d-105">다음 이점을 hello로 제공 Lifesize 클라우드 Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="30d3d-105">Integrating Lifesize Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="30d3d-106">클라우드 액세스 tooLifesize을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-106">You can control in Azure AD who has access tooLifesize Cloud</span></span>
- <span data-ttu-id="30d3d-107">에 사용자가 tooautomatically get 로그온 tooLifesize (Single Sign-on)는 클라우드는 Azure AD 계정 사용을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-107">You can enable your users tooautomatically get signed-on tooLifesize Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="30d3d-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="30d3d-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30d3d-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="30d3d-110">Prerequisites</span></span>

<span data-ttu-id="30d3d-111">다음 항목 hello가 필요 tooconfigure Lifesize 클라우드와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-111">tooconfigure Azure AD integration with Lifesize Cloud, you need hello following items:</span></span>

- <span data-ttu-id="30d3d-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="30d3d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="30d3d-113">Lifesize Cloud Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="30d3d-113">A Lifesize Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="30d3d-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="30d3d-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="30d3d-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="30d3d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="30d3d-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="30d3d-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="30d3d-118">Scenario description</span></span>
<span data-ttu-id="30d3d-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="30d3d-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="30d3d-121">Hello 갤러리에서 Lifesize 클라우드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-121">Adding Lifesize Cloud from hello gallery</span></span>
2. <span data-ttu-id="30d3d-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="30d3d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lifesize-cloud-from-hello-gallery"></a><span data-ttu-id="30d3d-123">Hello 갤러리에서 Lifesize 클라우드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-123">Adding Lifesize Cloud from hello gallery</span></span>
<span data-ttu-id="30d3d-124">tooconfigure hello와의 통합 Lifesize 클라우드 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Lifesize 클라우드 tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-124">tooconfigure hello integration of Lifesize Cloud into Azure AD, you need tooadd Lifesize Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="30d3d-125">**hello 갤러리에서 Lifesize 클라우드 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="30d3d-125">**tooadd Lifesize Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="30d3d-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="30d3d-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="30d3d-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="30d3d-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="30d3d-133">Hello 검색 상자에 입력 **Lifesize 클라우드**합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-133">In hello search box, type **Lifesize Cloud**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. <span data-ttu-id="30d3d-135">Hello 결과 패널에서 선택 **Lifesize 클라우드**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-135">In hello results panel, select **Lifesize Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="30d3d-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="30d3d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="30d3d-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Lifesize Cloud에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-138">In this section, you configure and test Azure AD single sign-on with Lifesize Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="30d3d-139">Single sign on toowork에 대 한 Azure AD는 tooknow Lifesize 클라우드에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lifesize Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="30d3d-140">즉, Azure AD 사용자 및 Lifesize 클라우드에서 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-140">In other words, a link relationship between an Azure AD user and hello related user in Lifesize Cloud needs toobe established.</span></span>

<span data-ttu-id="30d3d-141">Lifesize 클라우드에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-141">In Lifesize Cloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="30d3d-142">tooconfigure 및 Lifesize 클라우드를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-142">tooconfigure and test Azure AD single sign-on with Lifesize Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="30d3d-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="30d3d-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="30d3d-145">**[Lifesize 클라우드 테스트 사용자 만들기](#creating-a-lifesize-cloud-test-user)**  -toohave Lifesize 클라우드에서 사용자의 연결 된 Azure AD toohello 표현인 Britta Simon의 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-145">**[Creating a Lifesize Cloud test user](#creating-a-lifesize-cloud-test-user)** - toohave a counterpart of Britta Simon in Lifesize Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="30d3d-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="30d3d-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="30d3d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="30d3d-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="30d3d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="30d3d-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Lifesize 클라우드 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lifesize Cloud application.</span></span>

<span data-ttu-id="30d3d-150">**Azure AD tooconfigure single sign on Lifesize 클라우드와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="30d3d-150">**tooconfigure Azure AD single sign-on with Lifesize Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="30d3d-151">Hello hello에 Azure 포털에서에서 **Lifesize 클라우드** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-151">In hello Azure portal, on hello **Lifesize Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="30d3d-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. <span data-ttu-id="30d3d-155">Hello에 **Lifesize 클라우드 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-155">On hello **Lifesize Cloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    <span data-ttu-id="30d3d-157">a.</span><span class="sxs-lookup"><span data-stu-id="30d3d-157">a.</span></span> <span data-ttu-id="30d3d-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://login.lifesizecloud.com/ls/?acs`</span><span class="sxs-lookup"><span data-stu-id="30d3d-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://login.lifesizecloud.com/ls/?acs`</span></span>

    <span data-ttu-id="30d3d-159">b.</span><span class="sxs-lookup"><span data-stu-id="30d3d-159">b.</span></span> <span data-ttu-id="30d3d-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://login.lifesizecloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="30d3d-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://login.lifesizecloud.com/<companyname>`</span></span>

     
4. <span data-ttu-id="30d3d-161">확인 **고급 URL 설정 표시**, hello 단계 다음에 수행:</span><span class="sxs-lookup"><span data-stu-id="30d3d-161">Check **Show advanced URL settings**, perform hello following step:</span></span>  
   
    ![Single Sign-on 구성](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    <span data-ttu-id="30d3d-163">Hello에 **상태 릴레이** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://webapp.lifesizecloud.com/?ent=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="30d3d-163">In hello **Relay state** textbox, type a URL using hello following pattern: `https://webapp.lifesizecloud.com/?ent=<identifier>`</span></span>
   
   > [!NOTE] 
   ><span data-ttu-id="30d3d-164">이러한 없는지 hello 실제 값 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="30d3d-164">Please note that these are not hello real values.</span></span> <span data-ttu-id="30d3d-165">tooupdate hello로 이러한 값이 있는 실제 로그온 URL, 릴레이 상태 및 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-165">you have tooupdate these values with hello actual Sign-On URL, Relay State, and Identifier.</span></span> <span data-ttu-id="30d3d-166">연락처 [Lifesize 클라우드 클라이언트 지원 팀](https://www.lifesize.com/support) tooget 로그온 URL 및 식별자 값 hello 자습서의 뒷부분에서 설명 하는 SSO 구성에서 릴레이 상태 값을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-166">Contact [Lifesize Cloud Client support team](https://www.lifesize.com/support) tooget Sign-On URL, and Identifier values and you can get Relay State  value from SSO Configuration that is explained later in hello tutorial.</span></span>

4. <span data-ttu-id="30d3d-167">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-167">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. <span data-ttu-id="30d3d-169">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-169">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="30d3d-171">Hello에 **Lifesize 클라우드 구성** 섹션에서 클릭 **Lifesize 클라우드 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="30d3d-171">On hello **Lifesize Cloud Configuration** section, click **Configure Lifesize Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="30d3d-172">복사 hello **SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="30d3d-172">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. <span data-ttu-id="30d3d-174">tooget SSO 로그인 hello Lifesize 클라우드 응용 프로그램을 관리자 권한으로 응용 프로그램에 대해 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-174">tooget SSO configured for your application, login into hello Lifesize Cloud application with Admin privileges.</span></span>

8. <span data-ttu-id="30d3d-175">Hello 상단 오른쪽 모서리에서 사용자 이름을 클릭 하 고 hello 클릭 **이전 설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-175">In hello top right corner click on your name and then click on hello **Advance Settings**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. <span data-ttu-id="30d3d-177">고급 설정을 클릭 hello hello에 **SSO 구성** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-177">In hello Advance Settings now click on hello **SSO Configuration** link.</span></span> <span data-ttu-id="30d3d-178">인스턴스에 대 한 hello SSO 구성 페이지를 열립니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-178">It will open hello SSO Configuration page for your instance.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. <span data-ttu-id="30d3d-180">이제 다음 hello SSO 구성 UI에서에서 값에는 hello를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-180">Now configure hello following values in hello SSO configuration UI.</span></span>    
   
    ![Single Sign-on 구성](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    <span data-ttu-id="30d3d-182">a.</span><span class="sxs-lookup"><span data-stu-id="30d3d-182">a.</span></span> <span data-ttu-id="30d3d-183">**Id 공급자 발급자** 붙여넣기 hello 값의 텍스트 상자 **SAML 엔터티 ID** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-183">In **Identity Provider Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="30d3d-184">b.</span><span class="sxs-lookup"><span data-stu-id="30d3d-184">b.</span></span>  <span data-ttu-id="30d3d-185">**로그인 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-185">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="30d3d-186">c.</span><span class="sxs-lookup"><span data-stu-id="30d3d-186">c.</span></span> <span data-ttu-id="30d3d-187">콘텐츠를 클립보드에 복사 hello Azure 포털에서 다운로드 한 메모장에서 e-64로 인코딩된 인증서를 열고 toohello 붙여 **X.509 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-187">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="30d3d-188">d.</span><span class="sxs-lookup"><span data-stu-id="30d3d-188">d.</span></span> <span data-ttu-id="30d3d-189">SAML 특성 hello hello 이름 텍스트 상자에 대 한 매핑을 hello 값으로 입력 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span><span class="sxs-lookup"><span data-stu-id="30d3d-189">In hello SAML Attribute mappings for hello First Name text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span></span>
    
    <span data-ttu-id="30d3d-190">e.</span><span class="sxs-lookup"><span data-stu-id="30d3d-190">e.</span></span> <span data-ttu-id="30d3d-191">Hello에 대 한 hello SAML 특성 매핑에서 **성** 으로 hello 값을 입력 하는 텍스트 상자 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span><span class="sxs-lookup"><span data-stu-id="30d3d-191">In hello SAML Attribute mapping for hello **Last Name** text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span></span>
    
    <span data-ttu-id="30d3d-192">f.</span><span class="sxs-lookup"><span data-stu-id="30d3d-192">f.</span></span> <span data-ttu-id="30d3d-193">Hello에 대 한 hello SAML 특성 매핑에서 **전자 메일** 으로 hello 값을 입력 하는 텍스트 상자 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span><span class="sxs-lookup"><span data-stu-id="30d3d-193">In hello SAML Attribute mapping for hello **Email** text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span></span>

11. <span data-ttu-id="30d3d-194">hello에서 클릭할 수 있는 toocheck hello 구성 **테스트** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-194">toocheck hello configuration you can click on hello **Test** button.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="30d3d-195">성공적인 테스트에 대 한 Azure AD에서 toocomplete hello 구성 마법사가 필요 하 고 액세스 toousers 또는 hello 테스트를 수행할 수 있는 그룹을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-195">For successful testing you need toocomplete hello configuration wizard in Azure AD and also provide access toousers or groups who can perform hello test.</span></span>

12. <span data-ttu-id="30d3d-196">Hello을 확인 하 여 hello SSO를 사용 하도록 설정 **SSO 사용** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-196">Enable hello SSO by checking on hello **Enable SSO** button.</span></span>

13. <span data-ttu-id="30d3d-197">이제 hello 클릭 **업데이트** 단추 모든 hello 설정이 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-197">Now click on hello **Update** button so that all hello settings are saved.</span></span> <span data-ttu-id="30d3d-198">Hello RelayState 값으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-198">This will generate hello RelayState value.</span></span> <span data-ttu-id="30d3d-199">복사 hello hello 텍스트 상자에 생성 된 RelayState 값 hello에 붙여 **릴레이 상태** 아래 텍스트 상자에 붙여넣습니다 **Lifesize 클라우드 도메인 및 Url** 섹션.</span><span class="sxs-lookup"><span data-stu-id="30d3d-199">Copy hello RelayState value, which is generated in hello text box, paste it in hello **Relay State** textbox under **Lifesize Cloud Domain and URLs** section.</span></span> 

> [!TIP]
> <span data-ttu-id="30d3d-200">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="30d3d-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="30d3d-201">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="30d3d-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="30d3d-202">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="30d3d-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="30d3d-203">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="30d3d-203">Creating an Azure AD test user</span></span>

<span data-ttu-id="30d3d-204">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="30d3d-206">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="30d3d-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="30d3d-207">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="30d3d-209">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="30d3d-211">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="30d3d-213">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="30d3d-215">a.</span><span class="sxs-lookup"><span data-stu-id="30d3d-215">a.</span></span> <span data-ttu-id="30d3d-216">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="30d3d-217">b.</span><span class="sxs-lookup"><span data-stu-id="30d3d-217">b.</span></span> <span data-ttu-id="30d3d-218">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="30d3d-219">c.</span><span class="sxs-lookup"><span data-stu-id="30d3d-219">c.</span></span> <span data-ttu-id="30d3d-220">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="30d3d-221">d.</span><span class="sxs-lookup"><span data-stu-id="30d3d-221">d.</span></span> <span data-ttu-id="30d3d-222">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-222">Click **Create**.</span></span>
 
### <a name="creating-a-lifesize-cloud-test-user"></a><span data-ttu-id="30d3d-223">Lifesize Cloud 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="30d3d-223">Creating a Lifesize Cloud test user</span></span>

<span data-ttu-id="30d3d-224">이 섹션에서는 Lifesize Cloud에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-224">In this section, you create a user called Britta Simon in Lifesize Cloud.</span></span> <span data-ttu-id="30d3d-225">Lifesize Cloud는 자동 사용자 프로비전을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-225">Lifesize cloud does support automatic user provisioning.</span></span> <span data-ttu-id="30d3d-226">Azure AD에서 인증을 거친 후 hello 사용자 hello 응용 프로그램에 자동으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-226">After successful authentication at Azure AD, hello user will be automatically provisioned in hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="30d3d-227">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="30d3d-228">이 섹션에서는 액세스 tooLifesize 클라우드를 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLifesize Cloud.</span></span>

![사용자 할당][200] 

<span data-ttu-id="30d3d-230">**tooassign Britta Simon tooLifesize 클라우드에 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="30d3d-230">**tooassign Britta Simon tooLifesize Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="30d3d-231">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="30d3d-233">Hello 응용 프로그램 목록에서 선택 **Lifesize 클라우드**합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-233">In hello applications list, select **Lifesize Cloud**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. <span data-ttu-id="30d3d-235">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="30d3d-237">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-237">Click **Add** button.</span></span> <span data-ttu-id="30d3d-238">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="30d3d-240">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="30d3d-241">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="30d3d-242">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="30d3d-243">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="30d3d-243">Testing single sign-on</span></span>

<span data-ttu-id="30d3d-244">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="30d3d-245">Hello Lifesize 클라우드 hello 액세스 패널에서에서 타일을 클릭할 때 Lifesize 클라우드 응용 프로그램의 로그인 페이지를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-245">When you click hello Lifesize Cloud tile in hello Access Panel, you should get login page of Lifesize Cloud application.</span></span>
<span data-ttu-id="30d3d-246">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="30d3d-246">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="30d3d-247">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="30d3d-247">Additional resources</span></span>

* [<span data-ttu-id="30d3d-248">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="30d3d-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="30d3d-249">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="30d3d-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

