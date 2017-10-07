---
title: "자습서: Soonr Workplace와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Soonr 회사 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: f950b45d0beceab2fa17b7690c9de81ec6603089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a><span data-ttu-id="3bc7e-103">자습서: Soonr Workplace와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="3bc7e-103">Tutorial: Azure Active Directory integration with Soonr Workplace</span></span>

<span data-ttu-id="3bc7e-104">이 자습서의 hello 목적은 tooshow 있습니다 어떻게 toointegrate Azure Active Directory (Azure AD)와 Soonr 작업 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-104">hello objective of this tutorial is tooshow you how toointegrate Soonr Workplace with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="3bc7e-105">다음 이점을 hello로 제공 Soonr 회사 Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="3bc7e-105">Integrating Soonr Workplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3bc7e-106">Azure ad 액세스 tooSoonr 작업 공간을 가진 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-106">You can control in Azure AD who has access tooSoonr Workplace</span></span>
- <span data-ttu-id="3bc7e-107">프로그램 사용자 tooautomatically get 로그온 tooSoonr (Single Sign-on)는 회사의 Azure AD 계정으로 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-107">You can enable your users tooautomatically get signed-on tooSoonr Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3bc7e-108">하나의 중앙 위치-hello Azure 클래식 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="3bc7e-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3bc7e-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3bc7e-110">Prerequisites</span></span>

<span data-ttu-id="3bc7e-111">다음 항목 hello가 필요 tooconfigure Soonr 회사와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-111">tooconfigure Azure AD integration with Soonr Workplace, you need hello following items:</span></span>

- <span data-ttu-id="3bc7e-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="3bc7e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3bc7e-113">Soonr Workplace Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="3bc7e-113">A Soonr Workplace single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="3bc7e-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="3bc7e-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3bc7e-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="3bc7e-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="3bc7e-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="3bc7e-118">Scenario description</span></span>
<span data-ttu-id="3bc7e-119">이 자습서의 hello 목적은 tooenable 있습니다 tootest Azure AD에서 single sign-on 테스트 환경에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="3bc7e-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3bc7e-121">Hello 갤러리에서 Soonr 작업 공간을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-121">Adding Soonr Workplace from hello gallery</span></span>
2. <span data-ttu-id="3bc7e-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3bc7e-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-soonr-workplace-from-hello-gallery"></a><span data-ttu-id="3bc7e-123">Hello 갤러리에서 Soonr 작업 공간을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-123">Adding Soonr Workplace from hello gallery</span></span>
<span data-ttu-id="3bc7e-124">tooconfigure hello와의 통합 Soonr 회사 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 작업 공간 Soonr tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-124">tooconfigure hello integration of Soonr Workplace into Azure AD, you need tooadd Soonr Workplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3bc7e-125">**hello 갤러리에서 작업 공간 Soonr tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="3bc7e-125">**tooadd Soonr Workplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3bc7e-126">Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3bc7e-128">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="3bc7e-129">tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![응용 프로그램][2]

4. <span data-ttu-id="3bc7e-131">클릭 **추가** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-131">Click **Add** at hello bottom of hello page.</span></span>

    ![응용 프로그램][3]

5. <span data-ttu-id="3bc7e-133">Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
 
    ![응용 프로그램][4]

6. <span data-ttu-id="3bc7e-135">Hello 검색 상자에 입력 **Soonr 작업 공간**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-135">In hello search box, type **Soonr Workplace**.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. <span data-ttu-id="3bc7e-137">Hello 결과 창에서 선택 **Soonr 작업 공간**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-137">In hello results pane, select **Soonr Workplace**, and then click **Complete** tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3bc7e-139">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3bc7e-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3bc7e-140">이 섹션의 hello 목적은 tooshow "Britta Simon" 이라는 테스트 사용자에 따라 tooconfigure 및 Soonr 작업 공간을 사용 하 여 Azure AD에서 single sign-on 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with Soonr Workplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3bc7e-141">Single sign on toowork에 대 한 Azure AD는 tooknow에 Azure AD의 직장 Soonr tooan 사용자의 어떤 hello 테이블에 해당 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Soonr Workplace tooan user in Azure AD is.</span></span> <span data-ttu-id="3bc7e-142">즉, Azure AD 사용자 및 Soonr 직장에서 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-142">In other words, a link relationship between an Azure AD user and hello related user in Soonr Workplace needs toobe established.</span></span>  

<span data-ttu-id="3bc7e-143">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Soonr 직장에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Soonr Workplace.</span></span>

<span data-ttu-id="3bc7e-144">tooconfigure 및 Soonr 작업 공간을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-144">tooconfigure and test Azure AD single sign-on with Soonr Workplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3bc7e-145">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3bc7e-146">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3bc7e-147">**[작업 공간 Soonr 테스트 사용자 만들기](#creating-a-soonr-workplace-test-user)**  -toohave Britta Simon 그녀의 연결 된 Azure AD toohello 표현인 Soonr 직장에서 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-147">**[Creating a Soonr Workplace test user](#creating-a-soonr-workplace-test-user)** - toohave a counterpart of Britta Simon in Soonr Workplace that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="3bc7e-148">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3bc7e-149">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3bc7e-150">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="3bc7e-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3bc7e-151">이 섹션에서는 Azure AD에서 single sign-on hello 클래식 포털의 설정 및 Soonr 회사 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Soonr Workplace application.</span></span>


<span data-ttu-id="3bc7e-152">**tooconfigure Azure AD single sign on Soonr 작업 공간으로 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="3bc7e-152">**tooconfigure Azure AD single sign-on with Soonr Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="3bc7e-153">Hello hello에 Azure 클래식 포털에서에서 **Soonr 작업 공간** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **구성 Single Sign-on**  대화 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-153">In hello Azure classic portal, on hello **Soonr Workplace** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>

    ![Single Sign-on 구성][6] 

2. <span data-ttu-id="3bc7e-155">Hello에 **어떻게 tooSoonr 작업 공간에 사용자가 toosign 보 시겠습니까** 페이지에서 **Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-155">On hello **How would you like users toosign on tooSoonr Workplace** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. <span data-ttu-id="3bc7e-157">Hello에 **앱 설정 구성** 대화 상자 페이지에서 수행할 단계를 수행 하는 hello: 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-157">On hello **Configure App Settings** dialog page, perform hello following steps:.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    <span data-ttu-id="3bc7e-159">a.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-159">a.</span></span> <span data-ttu-id="3bc7e-160">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL: `https://<server-name>.soonr.com/singlesignon/saml/SSO`합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-160">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span></span>

    <span data-ttu-id="3bc7e-161">b.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-161">b.</span></span> <span data-ttu-id="3bc7e-162">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-162">Click **Next**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3bc7e-163">Hello 진정한 가치 아닌지 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-163">Please note that this is not hello real value.</span></span> <span data-ttu-id="3bc7e-164">이 값을 실제 hello로 로그온 URL tooupdate를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-164">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="3bc7e-165">연락처 Soonr 작업 공간 팀 tooget이이 값을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-165">Contact Soonr Workplace support team tooget this value.</span></span>

4. <span data-ttu-id="3bc7e-166">Hello에 **Soonr 작업 공간에서 single sign on 구성** 페이지 **메타 데이터 다운로드** hello 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-166">On hello **Configure single sign-on at Soonr Workplace** page, click **Download metadata** and then save hello file on your computer:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. <span data-ttu-id="3bc7e-168">tooget SSO 응용 프로그램에 대해 구성 된 Soonr 작업 공간 지원 팀에 문의 하 고 hello 다음을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-168">tooget SSO configured for your application, contact your Soonr Workplace support team and provide them with hello following:</span></span> 

    <span data-ttu-id="3bc7e-169">다운로드 한 • hello **메타 데이터** 파일</span><span class="sxs-lookup"><span data-stu-id="3bc7e-169">•  hello downloaded **Metadata** file</span></span>

    <span data-ttu-id="3bc7e-170">• hello **발급자 URL**</span><span class="sxs-lookup"><span data-stu-id="3bc7e-170">•  hello **Issuer URL**</span></span>

    <span data-ttu-id="3bc7e-171">• hello **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="3bc7e-171">•  hello **SAML SSO URL**</span></span>

    <span data-ttu-id="3bc7e-172">• hello **Single Sign-Out 서비스 URL**</span><span class="sxs-lookup"><span data-stu-id="3bc7e-172">•  hello **Single Sign-Out Service URL**</span></span>

    >[!NOTE]
    ><span data-ttu-id="3bc7e-173">이 응용 프로그램으로 인해 교체 되 <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask 작업 공간</a> 참조할 수 있습니다 및 <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">이</a> Azure AD를 사용 하 여 hello 응용 프로그램 구성에 대 한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-173">This application is superseded by <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> and you can refer <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">this</a> tutorial for configuring hello application with Azure AD.</span></span>
   
6. <span data-ttu-id="3bc7e-174">Hello Azure 클래식 포털에서에서 hello single sign on 구성 확인을 선택한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-174">In hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Azure AD Single Sign-On][10]

7. <span data-ttu-id="3bc7e-176">Hello에 **Single sign on 확인** 페이지 **완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-176">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Azure AD Single Sign-On][11]



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3bc7e-178">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3bc7e-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="3bc7e-179">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 클래식 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-179">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>  

![Azure AD 사용자 만들기][20]

<span data-ttu-id="3bc7e-181">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="3bc7e-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3bc7e-182">Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-182">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="3bc7e-184">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-184">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="3bc7e-185">toodisplay hello 목록이 hello 바탕 화면에서 hello 메뉴에서 사용자가 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-185">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3bc7e-187">tooopen hello **사용자 추가** hello 아래쪽에 hello 도구 모음에서 대화 상자에서 클릭 **사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-187">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="3bc7e-189">Hello에 **이 사용자에 대해 알리기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-189">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    <span data-ttu-id="3bc7e-191">a.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-191">a.</span></span> <span data-ttu-id="3bc7e-192">사용자 유형에서 조직의 새 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-192">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="3bc7e-193">b.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-193">b.</span></span> <span data-ttu-id="3bc7e-194">Hello 사용자 이름에서에서 **textbox**, 형식 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-194">In hello User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3bc7e-195">c.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-195">c.</span></span> <span data-ttu-id="3bc7e-196">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-196">Click **Next**.</span></span>

6.  <span data-ttu-id="3bc7e-197">Hello에 **사용자 프로필** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-197">On hello **User Profile** dialog page, perform hello following steps:</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    <span data-ttu-id="3bc7e-199">a.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-199">a.</span></span> <span data-ttu-id="3bc7e-200">Hello에 **이름** 텍스트 상자에 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-200">In hello **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="3bc7e-201">b.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-201">b.</span></span> <span data-ttu-id="3bc7e-202">Hello에 **성** 텍스트 상자에, **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-202">In hello **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="3bc7e-203">c.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-203">c.</span></span> <span data-ttu-id="3bc7e-204">Hello에 **표시 이름** 텍스트 상자에 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-204">In hello **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="3bc7e-205">d.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-205">d.</span></span> <span data-ttu-id="3bc7e-206">Hello에 **역할** 목록에서 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-206">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="3bc7e-207">e.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-207">e.</span></span> <span data-ttu-id="3bc7e-208">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-208">Click **Next**.</span></span>

7. <span data-ttu-id="3bc7e-209">Hello에 **임시 암호 가져오기** 대화 상자 페이지에서 클릭 **만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-209">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="3bc7e-211">Hello에 **임시 암호 가져오기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-211">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="3bc7e-213">a.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-213">a.</span></span> <span data-ttu-id="3bc7e-214">Hello hello 값 적어 **새 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-214">Write down hello value of hello **New Password**.</span></span>

    <span data-ttu-id="3bc7e-215">b.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-215">b.</span></span> <span data-ttu-id="3bc7e-216">페이지 맨 아래에 있는 **완료**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-216">Click **Complete**.</span></span>   



### <a name="creating-a-soonr-workplace-test-user"></a><span data-ttu-id="3bc7e-217">Soonr Workplace 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3bc7e-217">Creating a Soonr Workplace test user</span></span>

<span data-ttu-id="3bc7e-218">hello이이 섹션의 목적은 toocreate Soonr 직장에서 Britta Simon 라고 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-218">hello objective of this section is toocreate a user called Britta Simon in Soonr Workplace.</span></span> <span data-ttu-id="3bc7e-219">와 협력 하세요 Soonr 작업 공간 지원 팀 toocreate hello 플랫폼의 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-219">Please work with Soonr Workplace support team toocreate a user in hello platform.</span></span> <span data-ttu-id="3bc7e-220">Hello에 지원 티켓에서 Soonr 발생 시킬 수 있습니다 <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">여기</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-220">You can raise hello support ticket with Soonr from <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">here</a>.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3bc7e-221">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3bc7e-222">이 섹션의 hello 목표에는 자신의 액세스 tooSoonr 작업 공간을 부여 하 여 Azure single sign on Britta Simon toouse tooenabling입니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-222">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSoonr Workplace.</span></span>

![사용자 할당][200] 

<span data-ttu-id="3bc7e-224">**tooassign Britta Simon tooSoonr 직장에서 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="3bc7e-224">**tooassign Britta Simon tooSoonr Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="3bc7e-225">Hello Azure 클래식 포털 tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 최상위 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-225">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="3bc7e-227">Hello 응용 프로그램 목록에서 선택 **Soonr 작업 공간**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-227">In hello applications list, select **Soonr Workplace**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. <span data-ttu-id="3bc7e-229">Hello 메뉴에서 hello 위에 표시를 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-229">In hello menu on hello top, click **Users**.</span></span>

    ![사용자 할당][203] 

1. <span data-ttu-id="3bc7e-231">Hello [사용자] 목록에서 선택 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-231">In hello Users list, select **Britta Simon**.</span></span>

2. <span data-ttu-id="3bc7e-232">Hello 아래쪽에 hello 도구 모음에서 클릭 **할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-232">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![사용자 할당][205]



### <a name="testing-single-sign-on"></a><span data-ttu-id="3bc7e-234">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="3bc7e-234">Testing single sign-on</span></span>

<span data-ttu-id="3bc7e-235">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="3bc7e-236">Hello Soonr 작업 공간 hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour Soonr 회사 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bc7e-236">When you click hello Soonr Workplace tile in hello Access Panel, you should get automatically signed-on tooyour Soonr Workplace application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="3bc7e-237">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="3bc7e-237">Additional resources</span></span>

* [<span data-ttu-id="3bc7e-238">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="3bc7e-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3bc7e-239">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="3bc7e-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
