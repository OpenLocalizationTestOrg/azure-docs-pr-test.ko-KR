---
title: "자습서: Proofpoint on Demand와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 필요에 따라 Proofpoint 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 773e7f7d-ec31-411b-860d-6a6633335d43
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 0f9472ddc01f2c18ffc9e8d2b59a17b3b595515e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-proofpoint-on-demand"></a><span data-ttu-id="b3b46-103">자습서: Proofpoint on Demand와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="b3b46-103">Tutorial: Azure Active Directory integration with Proofpoint on Demand</span></span>

<span data-ttu-id="b3b46-104">이 자습서에 설명 어떻게 toointegrate Proofpoint에서 요청 시 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b3b46-104">In this tutorial, you learn how toointegrate Proofpoint on Demand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b3b46-105">필요에 따라 Proofpoint Azure AD와 통합 이점을 다음 hello 제공:</span><span class="sxs-lookup"><span data-stu-id="b3b46-105">Integrating Proofpoint on Demand with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b3b46-106">필요에 따라 액세스 tooProofpoint 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-106">You can control in Azure AD who has access tooProofpoint on Demand</span></span>
- <span data-ttu-id="b3b46-107">프로그램 사용자 tooautomatically get 로그온 tooProofpoint (Single Sign-on)는 필요에 따라 자신의 Azure AD 계정으로 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-107">You can enable your users tooautomatically get signed-on tooProofpoint on Demand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b3b46-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b3b46-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3b46-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b3b46-110">Prerequisites</span></span>

<span data-ttu-id="b3b46-111">tooconfigure Azure AD 통합 hello 다음 항목 주문형 Proofpoint를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-111">tooconfigure Azure AD integration with Proofpoint on Demand, you need hello following items:</span></span>

- <span data-ttu-id="b3b46-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="b3b46-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b3b46-113">Proofpoint on Demand Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="b3b46-113">A Proofpoint on Demand single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b3b46-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b3b46-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b3b46-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b3b46-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b3b46-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b3b46-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="b3b46-118">Scenario description</span></span>
<span data-ttu-id="b3b46-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b3b46-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b3b46-121">Hello 갤러리에서 필요에 따라 Proofpoint 추가</span><span class="sxs-lookup"><span data-stu-id="b3b46-121">Adding Proofpoint on Demand from hello gallery</span></span>
2. <span data-ttu-id="b3b46-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b3b46-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-proofpoint-on-demand-from-hello-gallery"></a><span data-ttu-id="b3b46-123">Hello 갤러리에서 필요에 따라 Proofpoint 추가</span><span class="sxs-lookup"><span data-stu-id="b3b46-123">Adding Proofpoint on Demand from hello gallery</span></span>
<span data-ttu-id="b3b46-124">tooconfigure hello와의 통합 Proofpoint 필요에 따라 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 필요에 따라 Proofpoint tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-124">tooconfigure hello integration of Proofpoint on Demand into Azure AD, you need tooadd Proofpoint on Demand from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b3b46-125">**hello 갤러리에서 필요에 따라 Proofpoint tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b3b46-125">**tooadd Proofpoint on Demand from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3b46-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b3b46-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b3b46-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="b3b46-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="b3b46-133">Hello 검색 상자에 입력 **주문형 Proofpoint**합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-133">In hello search box, type **Proofpoint on Demand**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_search.png)

5. <span data-ttu-id="b3b46-135">Hello 결과 패널에서 선택 **주문형 Proofpoint**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-135">In hello results panel, select **Proofpoint on Demand**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b3b46-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b3b46-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b3b46-138">이 섹션에서는 Britta Simon이라는 테스트 사용자를 기반으로 Proofpoint on Demand에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-138">In this section, you configure and test Azure AD single sign-on with Proofpoint on Demand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b3b46-139">Single sign on toowork에 대 한 Azure AD는 tooknow 주문형 Proofpoint에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Proofpoint on Demand is tooa user in Azure AD.</span></span> <span data-ttu-id="b3b46-140">즉, Azure AD 사용자 및 필요에 따라 Proofpoint에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-140">In other words, a link relationship between an Azure AD user and hello related user in Proofpoint on Demand needs toobe established.</span></span>

<span data-ttu-id="b3b46-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **사용자 이름** 주문형 Proofpoint에 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Proofpoint on Demand.</span></span>

<span data-ttu-id="b3b46-142">tooconfigure 및 테스트 Azure AD single sign on 구성 요소를 다음 toocomplete hello 해야 주문형 Proofpoint,:</span><span class="sxs-lookup"><span data-stu-id="b3b46-142">tooconfigure and test Azure AD single sign-on with Proofpoint on Demand, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b3b46-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b3b46-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b3b46-145">**[테스트 사용자 요청에는 Proofpoint 만드는](#creating-a-proofpoint-on-demand-test-user)**  -toohave Britta Simon Proofpoint 표현인 연결 된 toohello Azure AD 사용자의 요청 시에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-145">**[Creating a Proofpoint on Demand test user](#creating-a-proofpoint-on-demand-test-user)** - toohave a counterpart of Britta Simon in Proofpoint on Demand that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b3b46-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b3b46-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="b3b46-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b3b46-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="b3b46-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b3b46-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 및 요청 응용 프로그램에서 프로그램 Proofpoint에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Proofpoint on Demand application.</span></span>

<span data-ttu-id="b3b46-150">**tooconfigure Azure AD single sign on Proofpoint 주문형으로 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b3b46-150">**tooconfigure Azure AD single sign-on with Proofpoint on Demand, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3b46-151">Hello hello에 Azure 포털에서에서 **주문형 Proofpoint** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-151">In hello Azure portal, on hello **Proofpoint on Demand** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="b3b46-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
  
    ![Single Sign-on 구성](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_samlbase.png)

3. <span data-ttu-id="b3b46-155">Hello에 **필요 시 도메인 및 Url에 Proofpoint** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-155">On hello **Proofpoint on Demand Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_url.png)

    <span data-ttu-id="b3b46-157">a.In hello **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<hostname>.pphosted.com/ppssamlsp_hostname`</span><span class="sxs-lookup"><span data-stu-id="b3b46-157">a.In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com/ppssamlsp_hostname`</span></span>

    <span data-ttu-id="b3b46-158">b.</span><span class="sxs-lookup"><span data-stu-id="b3b46-158">b.</span></span> <span data-ttu-id="b3b46-159">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<hostname>.pphosted.com/ppssamlsp`</span><span class="sxs-lookup"><span data-stu-id="b3b46-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com/ppssamlsp`</span></span>

    <span data-ttu-id="b3b46-160">c.</span><span class="sxs-lookup"><span data-stu-id="b3b46-160">c.</span></span>  <span data-ttu-id="b3b46-161">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span><span class="sxs-lookup"><span data-stu-id="b3b46-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="b3b46-162">이러한 값은 실제 hello 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-162">These values are not hello real.</span></span> <span data-ttu-id="b3b46-163">이러한 항목을 업데이트 식별자, 회신 URL 및 로그온 URL 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-163">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="b3b46-164">연락처 [요청 시 클라이언트 지원 팀에 Proofpoint](https://www.proofpoint.com/us/support-services) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-164">Contact [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) tooget these values.</span></span> 

4. <span data-ttu-id="b3b46-165">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_certificate.png) 

5. <span data-ttu-id="b3b46-167">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-167">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="b3b46-169">Hello에 **요청 구성에 Proofpoint** 섹션에서 클릭 **주문형 Proofpoint 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="b3b46-169">On hello **Proofpoint on Demand Configuration** section, click **Configure Proofpoint on Demand** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b3b46-170">복사 hello **SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="b3b46-170">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_configure.png) 

7. <span data-ttu-id="b3b46-172">tooconfigure single sign on에서 **주문형 Proofpoint** toosend hello 다운로드 해야 쪽에서는 **Certificate(Base64)**,**SAML 엔터티 ID**, 및 **SAML Single Sign-on 서비스 URL** 너무[요청 시 클라이언트 지원 팀에 Proofpoint](https://www.proofpoint.com/us/support-services)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-172">tooconfigure single sign-on on **Proofpoint on Demand** side, you need toosend hello downloaded **Certificate(Base64)**,**SAML Entity ID**, and **SAML Single Sign-On Service URL** too[Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services).</span></span>

> [!TIP]
> <span data-ttu-id="b3b46-173">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="b3b46-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b3b46-174">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="b3b46-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b3b46-175">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b3b46-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b3b46-176">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b3b46-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="b3b46-177">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="b3b46-179">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b3b46-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3b46-180">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b3b46-182">이러한 값은 실제 hello 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-182">These values are not hello real.</span></span> <span data-ttu-id="b3b46-183">실제 hello로 이러한 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-183">Update these values with hello actual</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b3b46-185">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b3b46-187">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b3b46-189">a.</span><span class="sxs-lookup"><span data-stu-id="b3b46-189">a.</span></span> <span data-ttu-id="b3b46-190">Hello에 **이름** 텍스트 상자에 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-190">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="b3b46-191">b.</span><span class="sxs-lookup"><span data-stu-id="b3b46-191">b.</span></span> <span data-ttu-id="b3b46-192">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** Britta Simon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-192">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="b3b46-193">c.</span><span class="sxs-lookup"><span data-stu-id="b3b46-193">c.</span></span> <span data-ttu-id="b3b46-194">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b3b46-195">d.</span><span class="sxs-lookup"><span data-stu-id="b3b46-195">d.</span></span> <span data-ttu-id="b3b46-196">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-196">Click **Create**.</span></span>
 
### <a name="creating-a-proofpoint-on-demand-test-user"></a><span data-ttu-id="b3b46-197">Proofpoint on Demand 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b3b46-197">Creating a Proofpoint on Demand test user</span></span>

<span data-ttu-id="b3b46-198">이 섹션에서는 Proofpoint on Demand에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-198">In this section, you create a user called Britta Simon in Proofpoint on Demand.</span></span> <span data-ttu-id="b3b46-199">작업할 [요청 시 클라이언트 지원 팀에 Proofpoint](https://www.proofpoint.com/us/support-services) hello Proofpoint 요청 플랫폼에서의 tooadd 사용자.</span><span class="sxs-lookup"><span data-stu-id="b3b46-199">Work with [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) tooadd users in hello Proofpoint on Demand platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b3b46-200">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b3b46-201">이 섹션에서는 주문형 tooProofpoint 액세스 권한을 부여 하 여 Britta Simon toouse Azure single sign on을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooProofpoint on Demand.</span></span>

![사용자 할당][200] 

<span data-ttu-id="b3b46-203">**필요에 따라 Britta Simon tooProofpoint tooassign hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b3b46-203">**tooassign Britta Simon tooProofpoint on Demand, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3b46-204">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="b3b46-206">Hello 응용 프로그램 목록에서 선택 **주문형 Proofpoint**합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-206">In hello applications list, select **Proofpoint on Demand**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_app.png) 

3. <span data-ttu-id="b3b46-208">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="b3b46-210">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-210">Click **Add** button.</span></span> <span data-ttu-id="b3b46-211">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="b3b46-213">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b3b46-214">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b3b46-215">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b3b46-216">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="b3b46-216">Testing single sign-on</span></span>

<span data-ttu-id="b3b46-217">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b3b46-218">Hello를 클릭할 때 **주문형 Proofpoint** 타일 hello 액세스 패널에서 필요 시 응용 프로그램에서 Proofpoint tooyour에 자동으로 서명할 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-218">When you click hello **Proofpoint on Demand** tile on hello Access Panel, you should be automatically signed on tooyour Proofpoint on Demand application.</span></span>
<span data-ttu-id="b3b46-219">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b46-219">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>  

## <a name="additional-resources"></a><span data-ttu-id="b3b46-220">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b3b46-220">Additional resources</span></span>

* [<span data-ttu-id="b3b46-221">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="b3b46-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b3b46-222">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b3b46-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_203.png

