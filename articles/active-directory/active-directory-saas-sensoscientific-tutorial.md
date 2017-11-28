---
title: "자습서: SensoScientific Wireless Temperature Monitoring System과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 SensoScientific 무선 온도 모니터링 시스템 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: 4eabf7fc6457c217fd5c0c2539ab88c8110055e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a><span data-ttu-id="a63dd-103">자습서: SensoScientific Wireless Temperature Monitoring System과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="a63dd-103">Tutorial: Azure Active Directory integration with SensoScientific Wireless Temperature Monitoring System</span></span>

<span data-ttu-id="a63dd-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 SensoScientific 무선 온도 모니터링 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-104">In this tutorial, you learn how toointegrate SensoScientific Wireless Temperature Monitoring System with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a63dd-105">다음 이점을 hello로 제공 SensoScientific 무선 온도 모니터링 시스템을 Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="a63dd-105">Integrating SensoScientific Wireless Temperature Monitoring System with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a63dd-106">액세스 tooSensoScientific 무선 온도 모니터링 시스템을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-106">You can control in Azure AD who has access tooSensoScientific Wireless Temperature Monitoring System</span></span>
- <span data-ttu-id="a63dd-107">Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooSensoScientific (Single Sign-on) 무선 온도 모니터링 시스템을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-107">You can enable your users tooautomatically get signed-on tooSensoScientific Wireless Temperature Monitoring System (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a63dd-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a63dd-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a63dd-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a63dd-110">Prerequisites</span></span>

<span data-ttu-id="a63dd-111">다음 항목 hello가 필요 tooconfigure SensoScientific 무선 온도 모니터링 시스템와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-111">tooconfigure Azure AD integration with SensoScientific Wireless Temperature Monitoring System, you need hello following items:</span></span>

- <span data-ttu-id="a63dd-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="a63dd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a63dd-113">SensoScientific Wireless Temperature Monitoring System Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="a63dd-113">A SensoScientific Wireless Temperature Monitoring System single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a63dd-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a63dd-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a63dd-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a63dd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a63dd-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a63dd-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="a63dd-118">Scenario description</span></span>
<span data-ttu-id="a63dd-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a63dd-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a63dd-121">Hello 갤러리에서 SensoScientific 무선 온도 모니터링 시스템을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-121">Adding SensoScientific Wireless Temperature Monitoring System from hello gallery</span></span>
2. <span data-ttu-id="a63dd-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a63dd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-hello-gallery"></a><span data-ttu-id="a63dd-123">Hello 갤러리에서 SensoScientific 무선 온도 모니터링 시스템을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-123">Adding SensoScientific Wireless Temperature Monitoring System from hello gallery</span></span>
<span data-ttu-id="a63dd-124">tooconfigure hello와의 통합 SensoScientific 무선 온도 모니터링 시스템 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 SensoScientific 무선 온도 모니터링 시스템 tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-124">tooconfigure hello integration of SensoScientific Wireless Temperature Monitoring System into Azure AD, you need tooadd SensoScientific Wireless Temperature Monitoring System from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a63dd-125">**hello 갤러리에서 SensoScientific 무선 온도 모니터링 시스템 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a63dd-125">**tooadd SensoScientific Wireless Temperature Monitoring System from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a63dd-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a63dd-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a63dd-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="a63dd-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="a63dd-133">Hello 검색 상자에 입력 **SensoScientific 무선 온도 모니터링 시스템**합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-133">In hello search box, type **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

5. <span data-ttu-id="a63dd-135">Hello 결과 패널에서 선택 **SensoScientific 무선 온도 모니터링 시스템**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-135">In hello results panel, select **SensoScientific Wireless Temperature Monitoring System**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a63dd-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a63dd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a63dd-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 SensoScientific Wireless Temperature Monitoring System에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-138">In this section, you configure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a63dd-139">Single sign on toowork에 대 한 Azure AD는 tooknow SensoScientific 무선 온도 모니터링 시스템에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SensoScientific Wireless Temperature Monitoring System is tooa user in Azure AD.</span></span> <span data-ttu-id="a63dd-140">즉, Azure AD 사용자 및 hello SensoScientific 무선 온도 모니터링 시스템에서 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-140">In other words, a link relationship between an Azure AD user and hello related user in SensoScientific Wireless Temperature Monitoring System needs toobe established.</span></span>

<span data-ttu-id="a63dd-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** SensoScientific 무선 온도 모니터링 시스템에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SensoScientific Wireless Temperature Monitoring System.</span></span>

<span data-ttu-id="a63dd-142">tooconfigure 및 SensoScientific 무선 온도 모니터링 시스템을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-142">tooconfigure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a63dd-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a63dd-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a63dd-145">**[SensoScientific 무선 온도 모니터링 시스템 테스트 사용자 만들기](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)**  -toohave Britta Simon SensoScientific 무선 온도 모니터링 시스템에는 상응 하는 연결의 Azure AD toohello 표현 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-145">**[Creating a SensoScientific Wireless Temperature Monitoring System test user](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)** - toohave a counterpart of Britta Simon in SensoScientific Wireless Temperature Monitoring System that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a63dd-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a63dd-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="a63dd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a63dd-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="a63dd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a63dd-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 SensoScientific 무선 온도 모니터링 시스템 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SensoScientific Wireless Temperature Monitoring System application.</span></span>

<span data-ttu-id="a63dd-150">**SensoScientific 무선 온도 모니터링 시스템에서는 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a63dd-150">**tooconfigure Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, perform hello following steps:**</span></span>

1. <span data-ttu-id="a63dd-151">Hello hello에 Azure 포털에서에서 **SensoScientific 무선 온도 모니터링 시스템** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-151">In hello Azure portal, on hello **SensoScientific Wireless Temperature Monitoring System** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="a63dd-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

3. <span data-ttu-id="a63dd-155">Hello에 **SensoScientific 무선 온도 모니터링 시스템 도메인 및 Url** 섹션 hello 응용 프로그램에 따라 단계는 Azure와 사전 통합 이미 필요 tooperform 없습니다:</span><span class="sxs-lookup"><span data-stu-id="a63dd-155">On hello **SensoScientific Wireless Temperature Monitoring System Domain and URLs** section, no need tooperform any steps as hello app is already pre-integrated with Azure:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

4. <span data-ttu-id="a63dd-157">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

5. <span data-ttu-id="a63dd-159">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-159">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a63dd-161">Hello에 **SensoScientific 무선 온도 모니터링 시스템 구성** 섹션에서 클릭 **SensoScientific 무선 온도 모니터링 시스템 구성** tooopen  **Sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="a63dd-161">On hello **SensoScientific Wireless Temperature Monitoring System Configuration** section, click **Configure SensoScientific Wireless Temperature Monitoring System** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a63dd-162">복사 hello **Sign-Out URL, SAML 엔터티 ID** 및 **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="a63dd-162">Copy hello **Sign-Out URL, SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

7. <span data-ttu-id="a63dd-164">Tooyour SensoScientific 무선 온도 모니터링 시스템 응용 프로그램 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-164">Sign on tooyour SensoScientific Wireless Temperature Monitoring System application as an administrator.</span></span>

8. <span data-ttu-id="a63dd-165">Hello 탐색 메뉴에서 hello 위에 표시를 클릭 **구성** 및 goto **구성** 아래 **Single Sign On** tooopen hello Single Sign-on 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-165">In hello navigation menu on hello top, click **Configuration** and goto **Configure** under **Single Sign On** tooopen hello Single Sign On Settings.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

9. <span data-ttu-id="a63dd-167">**Single Sign-on 설정** 양식 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-167">In **Single Sign On Settings** form perform hello following steps:</span></span>
 
    <span data-ttu-id="a63dd-168">a.</span><span class="sxs-lookup"><span data-stu-id="a63dd-168">a.</span></span> <span data-ttu-id="a63dd-169">**Issuer Name(발급자 이름)**을 Azure AD로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-169">Select **Issuer Name** as Azure AD.</span></span>
    
    <span data-ttu-id="a63dd-170">b.</span><span class="sxs-lookup"><span data-stu-id="a63dd-170">b.</span></span> <span data-ttu-id="a63dd-171">붙여넣기 hello **SAML 엔터티 ID** 발급자 URL 텍스트 상자에 Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-171">Paste hello **SAML Entity ID** which you have copied from Azure portal into Issuer URL textbox.</span></span>
    
    <span data-ttu-id="a63dd-172">c.</span><span class="sxs-lookup"><span data-stu-id="a63dd-172">c.</span></span> <span data-ttu-id="a63dd-173">붙여넣기 hello **SAML Single Sign-on 서비스 URL** Single Sign-on 서비스 URL 텍스트 상자에 Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-173">Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal into Single Sign-On Service URL textbox.</span></span>

    <span data-ttu-id="a63dd-174">d.</span><span class="sxs-lookup"><span data-stu-id="a63dd-174">d.</span></span> <span data-ttu-id="a63dd-175">붙여넣기 hello **Sign-Out URL** Single Sign-Out 서비스 URL 텍스트 상자에 Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-175">Paste hello **Sign-Out URL** which you have copied from Azure portal into Single Sign-Out Service URL textbox.</span></span>

    <span data-ttu-id="a63dd-176">e.</span><span class="sxs-lookup"><span data-stu-id="a63dd-176">e.</span></span> <span data-ttu-id="a63dd-177">Azure 포털에서 다운로드 하 고 여기에 업로드 하는 hello 인증서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-177">Browse hello certificate which you have downloaded from Azure portal and upload here.</span></span>
    
    <span data-ttu-id="a63dd-178">f.</span><span class="sxs-lookup"><span data-stu-id="a63dd-178">f.</span></span> <span data-ttu-id="a63dd-179">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-179">Click **Save**.</span></span>
  
> [!TIP]
> <span data-ttu-id="a63dd-180">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="a63dd-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a63dd-181">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="a63dd-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a63dd-182">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a63dd-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a63dd-183">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a63dd-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="a63dd-184">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="a63dd-186">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a63dd-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a63dd-187">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a63dd-189">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a63dd-191">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a63dd-193">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a63dd-195">a.</span><span class="sxs-lookup"><span data-stu-id="a63dd-195">a.</span></span> <span data-ttu-id="a63dd-196">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a63dd-197">b.</span><span class="sxs-lookup"><span data-stu-id="a63dd-197">b.</span></span> <span data-ttu-id="a63dd-198">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a63dd-199">c.</span><span class="sxs-lookup"><span data-stu-id="a63dd-199">c.</span></span> <span data-ttu-id="a63dd-200">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a63dd-201">d.</span><span class="sxs-lookup"><span data-stu-id="a63dd-201">d.</span></span> <span data-ttu-id="a63dd-202">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-202">Click **Create**.</span></span>
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a><span data-ttu-id="a63dd-203">SensoScientific Wireless Temperature Monitoring System 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a63dd-203">Creating a SensoScientific Wireless Temperature Monitoring System test user</span></span>

<span data-ttu-id="a63dd-204">tooenable Azure AD 사용자가 toolog tooSensoScientific 무선 온도 모니터링 시스템에서에서 이러한 해야에 프로 비전 SensoScientific 무선 온도 모니터링 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-204">tooenable Azure AD users toolog in tooSensoScientific Wireless Temperature Monitoring System, they must be provisioned into SensoScientific Wireless Temperature Monitoring System.</span></span> <span data-ttu-id="a63dd-205">작업할 [SensoScientific 무선 온도 모니터링 시스템 지원 팀](https://www.sensoscientific.com/contact-us/) hello 사용자 hello SensoScientific 무선 온도 모니터링 시스템 플랫폼을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-205">Work with [SensoScientific Wireless Temperature Monitoring System support team](https://www.sensoscientific.com/contact-us/) to add hello users in hello SensoScientific Wireless Temperature Monitoring System platform.</span></span> <span data-ttu-id="a63dd-206">Single Sign-On을 사용하려면 먼저 사용자를 만들고 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-206">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a63dd-207">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a63dd-208">이 섹션에서는 액세스 tooSensoScientific 무선 온도 모니터링 시스템을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSensoScientific Wireless Temperature Monitoring System.</span></span>

![사용자 할당][200] 

<span data-ttu-id="a63dd-210">**tooassign Britta Simon tooSensoScientific 무선 온도 모니터링 시스템 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a63dd-210">**tooassign Britta Simon tooSensoScientific Wireless Temperature Monitoring System, perform hello following steps:**</span></span>

1. <span data-ttu-id="a63dd-211">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="a63dd-213">Hello 응용 프로그램 목록에서 선택 **SensoScientific 무선 온도 모니터링 시스템**합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-213">In hello applications list, select **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

3. <span data-ttu-id="a63dd-215">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="a63dd-217">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-217">Click **Add** button.</span></span> <span data-ttu-id="a63dd-218">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="a63dd-220">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a63dd-221">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a63dd-222">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a63dd-223">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="a63dd-223">Testing single sign-on</span></span>

<span data-ttu-id="a63dd-224">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="a63dd-225">Hello SensoScientific 무선 온도 모니터링 시스템 타일을 클릭 hello 액세스 패널에서에서 자동으로 로그온 tooyour SensoScientific 무선 온도 모니터링 시스템 응용 프로그램 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a63dd-225">Click hello SensoScientific Wireless Temperature Monitoring System tile in hello Access Panel, you will be automatically signed-on tooyour SensoScientific Wireless Temperature Monitoring System application.</span></span> <span data-ttu-id="a63dd-226">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](https://msdn.microsoft.com/library/dn308586)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a63dd-226">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a63dd-227">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a63dd-227">Additional resources</span></span>

* [<span data-ttu-id="a63dd-228">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="a63dd-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a63dd-229">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="a63dd-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_203.png

