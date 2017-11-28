---
title: "자습서: Huddle과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Huddle 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8389ba4c-f5f8-4ede-b2f4-32eae844ceb0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 0b2f6c4d839943cdd07699a1ff95dc8f90505699
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-huddle"></a><span data-ttu-id="01f1b-103">자습서: Huddle과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="01f1b-103">Tutorial: Azure Active Directory integration with Huddle</span></span>

<span data-ttu-id="01f1b-104">이 자습서에 설명 toointegrate Azure Active Directory (Azure AD)와 Huddle 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-104">In this tutorial, you learn how toointegrate Huddle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="01f1b-105">Azure AD와 Huddle 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-105">Integrating Huddle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="01f1b-106">액세스 tooHuddle을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-106">You can control in Azure AD who has access tooHuddle</span></span>
- <span data-ttu-id="01f1b-107">프로그램 사용자 tooautomatically get 로그온 tooHuddle (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-107">You can enable your users tooautomatically get signed-on tooHuddle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="01f1b-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="01f1b-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01f1b-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="01f1b-110">Prerequisites</span></span>

<span data-ttu-id="01f1b-111">와 Huddle tooconfigure Azure AD 통합, 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-111">tooconfigure Azure AD integration with Huddle, you need hello following items:</span></span>

- <span data-ttu-id="01f1b-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="01f1b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="01f1b-113">Huddle Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="01f1b-113">A Huddle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="01f1b-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="01f1b-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="01f1b-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="01f1b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="01f1b-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="01f1b-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="01f1b-118">Scenario description</span></span>

<span data-ttu-id="01f1b-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="01f1b-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="01f1b-121">Huddle는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="01f1b-121">Adding Huddle from hello gallery</span></span>
2. <span data-ttu-id="01f1b-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="01f1b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-huddle-from-hello-gallery"></a><span data-ttu-id="01f1b-123">Huddle는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="01f1b-123">Adding Huddle from hello gallery</span></span>
<span data-ttu-id="01f1b-124">tooconfigure hello와의 통합 Huddle Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Huddle tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-124">tooconfigure hello integration of Huddle into Azure AD, you need tooadd Huddle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="01f1b-125">**Huddle hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="01f1b-125">**tooadd Huddle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="01f1b-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="01f1b-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="01f1b-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="01f1b-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="01f1b-133">Hello 검색 상자에 입력 **Huddle**합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-133">In hello search box, type **Huddle**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_search.png)

5. <span data-ttu-id="01f1b-135">Hello 결과 패널에서 선택 **Huddle**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-135">In hello results panel, select **Huddle**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="01f1b-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="01f1b-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="01f1b-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Huddle에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-138">In this section, you configure and test Azure AD single sign-on with Huddle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="01f1b-139">Single sign on toowork에 대 한 Azure AD는 tooknow Huddle에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Huddle is tooa user in Azure AD.</span></span> <span data-ttu-id="01f1b-140">즉, Azure AD 사용자와 Huddle 요구 toobe 설정에서 hello 관련된 사용자 간 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-140">In other words, a link relationship between an Azure AD user and hello related user in Huddle needs toobe established.</span></span>

<span data-ttu-id="01f1b-141">Huddle에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-141">In Huddle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="01f1b-142">tooconfigure와 Huddle 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-142">tooconfigure and test Azure AD single sign-on with Huddle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="01f1b-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>

2. <span data-ttu-id="01f1b-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>

3. <span data-ttu-id="01f1b-145">**[Huddle 테스트 사용자 만들기](#creating-a-huddle-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Huddle에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-145">**[Creating a Huddle test user](#creating-a-huddle-test-user)** - toohave a counterpart of Britta Simon in Huddle that is linked toohello Azure AD representation of user.</span></span>

4. <span data-ttu-id="01f1b-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>

5. <span data-ttu-id="01f1b-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="01f1b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="01f1b-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="01f1b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="01f1b-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Huddle 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Huddle application.</span></span>

<span data-ttu-id="01f1b-150">**와 Huddle Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="01f1b-150">**tooconfigure Azure AD single sign-on with Huddle, perform hello following steps:**</span></span>

1. <span data-ttu-id="01f1b-151">Hello hello에 Azure 포털에서에서 **Huddle** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-151">In hello Azure portal, on hello **Huddle** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="01f1b-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_samlbase.png)

3. <span data-ttu-id="01f1b-155">Hello에 **Huddle 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-155">On hello **Huddle Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_url.png)

    <span data-ttu-id="01f1b-157">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`http://<company name>.huddle.com`</span><span class="sxs-lookup"><span data-stu-id="01f1b-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<company name>.huddle.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="01f1b-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-158">This value is not real.</span></span> <span data-ttu-id="01f1b-159">Hello로이 값을 업데이트 합니다. 실제 로그온 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="01f1b-160">연락처 [클라이언트 Huddle 지원 팀](https://huddle.zendesk.com) tooget이이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-160">Contact [Huddle Client support team](https://huddle.zendesk.com) tooget this value.</span></span> 

4. <span data-ttu-id="01f1b-161">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_certificate.png) 

5. <span data-ttu-id="01f1b-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-huddle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="01f1b-165">Hello에 **Huddle 구성** 섹션에서 클릭 **Huddle 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="01f1b-165">On hello **Huddle Configuration** section, click **Configure Huddle** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="01f1b-166">복사 hello **SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="01f1b-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_configure.png) 
    
7. <span data-ttu-id="01f1b-168">다운로드 toosend hello tooconfigure single sign on Huddle 쪽, 필요한 **인증서**, **SAML Single Sign-on 서비스 URL**, 및 **SAML 엔터티 ID** 너무[클라이언트 huddle 지원 팀](https://huddle.zendesk.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-168">tooconfigure single sign-on on Huddle side, you need toosend hello downloaded  **Certificate**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** too[Huddle Client support team](https://huddle.zendesk.com).</span></span> <span data-ttu-id="01f1b-169">이 설정은 toohave hello 양쪽 모두에 제대로 설정 하는 SAML SSO 연결 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>  
   
    >[!NOTE]
    > <span data-ttu-id="01f1b-170">Single sign on toobe hello Huddle 지원 팀에서 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-170">Single sign-on needs toobe enabled by hello Huddle support team.</span></span> <span data-ttu-id="01f1b-171">Hello 구성이 완료 되 면 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-171">You get a notification when hello configuration has been completed.</span></span> 
    > 

> [!TIP]
> <span data-ttu-id="01f1b-172">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="01f1b-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="01f1b-173">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="01f1b-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="01f1b-174">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="01f1b-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
   
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="01f1b-175">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="01f1b-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="01f1b-176">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="01f1b-178">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="01f1b-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="01f1b-179">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-huddle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="01f1b-181">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-huddle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="01f1b-183">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-huddle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="01f1b-185">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-huddle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="01f1b-187">a.</span><span class="sxs-lookup"><span data-stu-id="01f1b-187">a.</span></span> <span data-ttu-id="01f1b-188">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="01f1b-189">b.</span><span class="sxs-lookup"><span data-stu-id="01f1b-189">b.</span></span> <span data-ttu-id="01f1b-190">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="01f1b-191">c.</span><span class="sxs-lookup"><span data-stu-id="01f1b-191">c.</span></span> <span data-ttu-id="01f1b-192">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="01f1b-193">d.</span><span class="sxs-lookup"><span data-stu-id="01f1b-193">d.</span></span> <span data-ttu-id="01f1b-194">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-194">Click **Create**.</span></span>
 
### <a name="creating-a-huddle-test-user"></a><span data-ttu-id="01f1b-195">Huddle 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="01f1b-195">Creating a Huddle test user</span></span>

<span data-ttu-id="01f1b-196">tooenable Azure AD 사용자가 toolog tooHuddle에서 프로 비전 해야 Huddle에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-196">tooenable Azure AD users toolog in tooHuddle, they must be provisioned into Huddle.</span></span> <span data-ttu-id="01f1b-197">Hello Huddle의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-197">In hello case of Huddle, provisioning is a manual task.</span></span>

<span data-ttu-id="01f1b-198">**tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:**</span><span class="sxs-lookup"><span data-stu-id="01f1b-198">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="01f1b-199">Tooyour 로그인 **Huddle** 회사 사이트에서 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-199">Log in tooyour **Huddle** company site as administrator.</span></span>
2. <span data-ttu-id="01f1b-200">**작업 영역**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-200">Click **Workspace**.</span></span>
3. <span data-ttu-id="01f1b-201">**피플 \> 피플 초대**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-201">Click **People \> Invite People**.</span></span>
   
   <span data-ttu-id="01f1b-202">![사람](./media/active-directory-saas-huddle-tutorial/IC787838.png "사람")</span><span class="sxs-lookup"><span data-stu-id="01f1b-202">![People](./media/active-directory-saas-huddle-tutorial/IC787838.png "People")</span></span>

4. <span data-ttu-id="01f1b-203">Hello에 **새 초대 만들기** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-203">In hello **Create a new invitation** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="01f1b-204">![새 초대](./media/active-directory-saas-huddle-tutorial/IC787839.png "새 초대")</span><span class="sxs-lookup"><span data-stu-id="01f1b-204">![New Invitation](./media/active-directory-saas-huddle-tutorial/IC787839.png "New Invitation")</span></span>
   
   <span data-ttu-id="01f1b-205">a.</span><span class="sxs-lookup"><span data-stu-id="01f1b-205">a.</span></span> <span data-ttu-id="01f1b-206">Hello에 **선택 팀 tooinvite 사람 toojoin** 목록에서 **팀**합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-206">In hello **Choose a team tooinvite people toojoin** list, select **team**.</span></span>

   <span data-ttu-id="01f1b-207">b.</span><span class="sxs-lookup"><span data-stu-id="01f1b-207">b.</span></span> <span data-ttu-id="01f1b-208">형식 hello **전자 메일 주소** 유효한 Azure AD의 계정에 포함 하려는 tooprovision 너무**Enter 전자 메일 주소를 위한 tooinvite 원할 것** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-208">Type hello **Email Address** of a valid Azure AD account you want tooprovision in too**Enter email address for people you'd like tooinvite** textbox.</span></span>

   <span data-ttu-id="01f1b-209">c.</span><span class="sxs-lookup"><span data-stu-id="01f1b-209">c.</span></span> <span data-ttu-id="01f1b-210">**초대**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-210">Click **Invite**.</span></span>   
   
    >[!NOTE]
    > <span data-ttu-id="01f1b-211">hello Azure AD 계정 소유자 따라 활성화 tooconfirm hello 계정 연결을 포함 하 여 전자 메일을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-211">hello Azure AD account holder will receive an email including a link tooconfirm hello account before it becomes active.</span></span> 
    > 

>[!NOTE]
><span data-ttu-id="01f1b-212">다른 Huddle 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 Azure AD 사용자 계정을 tooprovision Huddle에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-212">You can use any other Huddle user account creation tools or APIs provided by Huddle tooprovision Azure AD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="01f1b-213">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="01f1b-214">이 섹션에서는 tooHuddle 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHuddle.</span></span>

![사용자 할당][200] 

<span data-ttu-id="01f1b-216">**tooassign Britta Simon tooHuddle hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="01f1b-216">**tooassign Britta Simon tooHuddle, perform hello following steps:**</span></span>

1. <span data-ttu-id="01f1b-217">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="01f1b-219">Hello 응용 프로그램 목록에서 선택 **Huddle**합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-219">In hello applications list, select **Huddle**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_app.png) 

3. <span data-ttu-id="01f1b-221">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="01f1b-223">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-223">Click **Add** button.</span></span> <span data-ttu-id="01f1b-224">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="01f1b-226">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="01f1b-227">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="01f1b-228">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="01f1b-229">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="01f1b-229">Testing single sign-on</span></span>

<span data-ttu-id="01f1b-230">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="01f1b-231">Hello 액세스 패널에서에서 hello Huddle 타일을 클릭할 때를 받아야 하며 자동으로 Huddle 응용 프로그램의 로그인 페이지.</span><span class="sxs-lookup"><span data-stu-id="01f1b-231">When you click hello Huddle tile in hello Access Panel, you should get automatically login page of Huddle application.</span></span>
<span data-ttu-id="01f1b-232">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="01f1b-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="01f1b-233">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="01f1b-233">Additional resources</span></span>

* [<span data-ttu-id="01f1b-234">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="01f1b-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="01f1b-235">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="01f1b-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_203.png
