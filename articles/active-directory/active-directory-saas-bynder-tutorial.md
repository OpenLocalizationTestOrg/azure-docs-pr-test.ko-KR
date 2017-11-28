---
title: "자습서: Bynder와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Bynder 사이입니다."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: a2a8477580d28fe422f2836f483dff286bc71c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a><span data-ttu-id="93e63-103">자습서: Bynder와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="93e63-103">Tutorial: Azure Active Directory integration with Bynder</span></span>
<span data-ttu-id="93e63-104">이 자습서의 hello 목적은 tooshow 있습니다 어떻게 toointegrate Bynder Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="93e63-104">hello objective of this tutorial is tooshow you how toointegrate Bynder with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="93e63-105">다음 이점을 hello로 제공 Bynder Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="93e63-105">Integrating Bynder with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="93e63-106">액세스 tooBynder을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-106">You can control in Azure AD who has access tooBynder</span></span>
* <span data-ttu-id="93e63-107">프로그램 사용자가 tooautomatically get 로그온 tooBynder single sign-on (SSO) 자신의 Azure AD 계정으로 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-107">You can enable your users tooautomatically get signed-on tooBynder single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="93e63-108">하나의 중앙 위치-hello Azure 클래식 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="93e63-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93e63-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="93e63-110">Prerequisites</span></span>
<span data-ttu-id="93e63-111">다음 항목 hello가 필요 tooconfigure Bynder와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-111">tooconfigure Azure AD integration with Bynder, you need hello following items:</span></span>

* <span data-ttu-id="93e63-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="93e63-112">An Azure AD subscription</span></span>
* <span data-ttu-id="93e63-113">Bynder SSO(Single Sign-On)가 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="93e63-113">A Bynder single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="93e63-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="93e63-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="93e63-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="93e63-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="93e63-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="93e63-118">Scenario description</span></span>
<span data-ttu-id="93e63-119">이 자습서의 hello 목적은 tooenable 있습니다 tootest Microsoft Azure AD SSO 테스트 환경에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-119">hello objective of this tutorial is tooenable you tootest Microsoft Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="93e63-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="93e63-121">Bynder는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="93e63-121">Adding Bynder from hello gallery</span></span>
2. <span data-ttu-id="93e63-122">Microsoft Azure AD SSO 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="93e63-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-bynder-from-hello-gallery"></a><span data-ttu-id="93e63-123">Bynder hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="93e63-123">Add Bynder from hello gallery</span></span>
<span data-ttu-id="93e63-124">tooconfigure hello와의 통합 Bynder Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Bynder tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-124">tooconfigure hello integration of Bynder into Azure AD, you need tooadd Bynder from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="93e63-125">**hello 갤러리에서 Bynder tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="93e63-125">**tooadd Bynder from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="93e63-126">Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-126">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="93e63-128">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="93e63-129">tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![응용 프로그램][2]
4. <span data-ttu-id="93e63-131">클릭 **추가** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![응용 프로그램][3]
5. <span data-ttu-id="93e63-133">Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![응용 프로그램][4]
6. <span data-ttu-id="93e63-135">Hello 검색 상자에 입력 **Bynder**합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-135">In hello search box, type **Bynder**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. <span data-ttu-id="93e63-137">Hello 결과 패널에서 선택 **Bynder**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-137">In hello results panel, select **Bynder**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Hello 갤러리에서 hello 앱 선택](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="93e63-139">Microsoft Azure AD SSO 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="93e63-139">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="93e63-140">이 섹션의 hello 목적은 tooshow "Britta Simon" 이라는 테스트 사용자에 따라 tooconfigure 및 Microsoft Azure AD SSO Bynder 및 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-140">hello objective of this section is tooshow you how tooconfigure and test Microsoft Azure AD SSO with Bynder based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="93e63-141">SSO toowork에 대 한 Azure AD는 tooknow Bynder tooan 사용자 Azure ad에서에서 어떤 hello 테이블에 해당 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-141">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Bynder tooan user in Azure AD is.</span></span> <span data-ttu-id="93e63-142">즉, Azure AD 사용자 및 Bynder에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-142">In other words, a link relationship between an Azure AD user and hello related user in Bynder needs toobe established.</span></span>

<span data-ttu-id="93e63-143">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Bynder에 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Bynder.</span></span>

<span data-ttu-id="93e63-144">tooconfigure 및 테스트 Bynder와 Microsoft Azure AD SSO 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-144">tooconfigure and test Microsoft Azure AD SSO with Bynder, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="93e63-145">**[Microsoft Azure AD single sign-on 구성](#configuring-azure-ad-single-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="93e63-146">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -Microsoft Azure AD Single Sign-on Britta Simon와 tootest 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="93e63-147">**[Bynder 테스트 사용자 만들기](#creating-a-bynder-test-user)**  -toohave Britta Simon 그녀의 연결 된 Azure AD toohello 표현인 Bynder에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-147">**[Creating a Bynder test user](#creating-a-bynder-test-user)** - toohave a counterpart of Britta Simon in Bynder that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="93e63-148">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -Microsoft Azure AD Single Sign-on Britta Simon toouse tooenable 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="93e63-149">**[Single sign on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="93e63-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-microsoft-azure-ad-sso"></a><span data-ttu-id="93e63-150">Microsoft Azure AD SSO 구성</span><span class="sxs-lookup"><span data-stu-id="93e63-150">Configuring Microsoft Azure AD SSO</span></span>
<span data-ttu-id="93e63-151">이 섹션에서는 Microsoft Azure AD SSO hello 클래식 포털에서 사용 하도록 설정 및 Bynder 응용 프로그램에서 SSO를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-151">In this section, you enable Microsoft Azure AD SSO in hello classic portal and configure SSO in your Bynder application.</span></span>

<span data-ttu-id="93e63-152">**tooconfigure Bynder와 Microsoft Azure AD SSO hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="93e63-152">**tooconfigure Microsoft Azure AD SSO with Bynder, perform hello following steps:**</span></span>

1. <span data-ttu-id="93e63-153">Hello에 hello 클래식 포털에서 **Bynder** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **구성 Single Sign-on** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="93e63-153">In hello classic portal, on hello **Bynder** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Single Sign-on 구성][6] 
2. <span data-ttu-id="93e63-155">Hello에 **어떻게 tooBynder에 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-155">On hello **How would you like users toosign on tooBynder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. <span data-ttu-id="93e63-157">Hello에 **앱 설정 구성** 대화 상자 페이지에서 tooconfigure hello 응용 프로그램에 필요한 경우 **IDP 시작 모드**hello 다음 단계를 수행 하 고 클릭, **다음**:</span><span class="sxs-lookup"><span data-stu-id="93e63-157">On hello **Configure App Settings** dialog page, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps and click **Next**:</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. <span data-ttu-id="93e63-159">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<company name>.getbynder.com/sso/SAML/authenticate/`</span><span class="sxs-lookup"><span data-stu-id="93e63-159">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span></span>
  2. <span data-ttu-id="93e63-160">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-160">Click **Next**.</span></span>
4. <span data-ttu-id="93e63-161">Tooconfigure hello 응용 프로그램에 필요한 경우 **SP 시작 모드** hello에 **앱 설정 구성** hello에는 클릭 하 여 대화 상자 페이지에서 **"표시 고급 설정 (선택 사항)"**hello를 입력 한 다음 **로그온 URL** 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-161">If you wish tooconfigure hello application in **SP initiated mode** on hello **Configure App Settings** dialog page, then click on hello **“Show advanced settings (optional)”** and then enter hello **Sign On URL** and click **Next**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. <span data-ttu-id="93e63-163">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<company name>.getbynder.com/login/`</span><span class="sxs-lookup"><span data-stu-id="93e63-163">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company name>.getbynder.com/login/`</span></span>
  2. <span data-ttu-id="93e63-164">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-164">Click **Next**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="93e63-165">이 자습서에서는 로그온 URL hello hello 값은 placeholfer 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-165">hello value for hello Sign On URL in this tutorial is just a placeholfer.</span></span> <span data-ttu-id="93e63-166">tooget hello 실제 값입니다 사용자 환경에 대 한 Bynder를 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="93e63-166">tooget hello actual vlaue for your environment, contact Bynder.</span></span>
   >

5. <span data-ttu-id="93e63-167">Hello에 **Bynder에서 single sign on 구성** 페이지 hello 다음 단계를 수행 하 고 클릭 **다음**:</span><span class="sxs-lookup"><span data-stu-id="93e63-167">On hello **Configure single sign-on at Bynder** page, perform hello following steps and click **Next**:</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. <span data-ttu-id="93e63-169">클릭 **메타 데이터 다운로드**, hello 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-169">Click **Download metadata**, and then save hello file on your computer.</span></span>
  2. <span data-ttu-id="93e63-170">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-170">Click **Next**.</span></span>
6. <span data-ttu-id="93e63-171">SSO 응용 프로그램에 대해 구성 된 tooget Bynder 지원 팀에 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-171">tooget SSO configured for your application, contact your Bynder support team.</span></span> <span data-ttu-id="93e63-172">Hello 다운로드 한 메타 데이터 파일을 첨부 하 고 편인 SSO Bynder 팀 tooset와 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-172">Attach hello downloaded metadata file and share it with Bynder team tooset up SSO on their side.</span></span>
7. <span data-ttu-id="93e63-173">Hello 클래식 포털의 hello single sign-on 구성 확인을 선택한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-173">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
8. <span data-ttu-id="93e63-175">Hello에 **Single sign on 확인** 페이지 **완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-175">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="93e63-177">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="93e63-177">Create an Azure AD test user</span></span>
<span data-ttu-id="93e63-178">이 섹션의 hello 목표 Britta Simon 라는 hello 클래식 포털에서 toocreate 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-178">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][20]

<span data-ttu-id="93e63-180">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="93e63-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="93e63-181">Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-181">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="93e63-183">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-183">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="93e63-184">toodisplay hello 목록이 hello 바탕 화면에서 hello 메뉴에서 사용자가 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-184">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="93e63-186">tooopen hello **사용자 추가** hello 아래쪽에 hello 도구 모음에서 대화 상자에서 클릭 **사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-186">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="93e63-188">Hello에 **이 사용자에 대해 알리기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-188">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="93e63-190">사용자 유형에서 조직의 새 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="93e63-191">Hello 사용자 이름에서에서 **textbox**, 형식 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-191">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="93e63-192">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-192">Click **Next**.</span></span>
6. <span data-ttu-id="93e63-193">Hello에 **사용자 프로필** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-193">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="93e63-195">Hello에 **이름** 텍스트 상자에 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-195">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="93e63-196">Hello에 **성** 텍스트 상자에, **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-196">In hello **Last Name** textbox, type, **Simon**.</span></span> 
  3. <span data-ttu-id="93e63-197">Hello에 **표시 이름** 텍스트 상자에 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-197">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="93e63-198">Hello에 **역할** 목록에서 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-198">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="93e63-199">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-199">Click **Next**.</span></span>
7. <span data-ttu-id="93e63-200">Hello에 **임시 암호 가져오기** 대화 상자 페이지에서 클릭 **만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-200">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="93e63-202">Hello에 **임시 암호 가져오기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. <span data-ttu-id="93e63-204">Hello hello 값 적어 **새 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-204">Write down hello value of hello **New Password**.</span></span>
   2. <span data-ttu-id="93e63-205">페이지 맨 아래에 있는 **완료**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93e63-205">Click **Complete**.</span></span>   

### <a name="create-a-bynder-test-user"></a><span data-ttu-id="93e63-206">Bynder 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="93e63-206">Create a Bynder test user</span></span>
<span data-ttu-id="93e63-207">hello이이 섹션의 목적은 toocreate Britta Simon Bynder에서 호출 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-207">hello objective of this section is toocreate a user called Britta Simon in Bynder.</span></span> <span data-ttu-id="93e63-208">Bynder는 적시에 프로비전을 지원하며 기본적으로 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-208">Bynder supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="93e63-209">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-209">There is no action item for you in this section.</span></span> <span data-ttu-id="93e63-210">새 사용자를 아직 존재 하지 않는 경우 시도 tooaccess Bynder 중 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-210">A new user will be created during an attempt tooaccess Bynder if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="93e63-211">Toocreate 된 사용자를 수동으로 해야 할 경우 toocontact hello Bynder 지원 팀을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-211">If you need toocreate an user manually, you need toocontact hello Bynder support team.</span></span> 
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="93e63-212">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-212">Assign hello Azure AD test user</span></span>
<span data-ttu-id="93e63-213">이 섹션의 hello 목표 액세스 tooBynder 그녀의 권한을 부여 하 여 tooenabling Britta Simon toouse Azure SSO를입니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-213">hello objective of this section is tooenabling Britta Simon toouse Azure SSO by granting her access tooBynder.</span></span>

   ![사용자 할당][200]

<span data-ttu-id="93e63-215">**tooassign Britta Simon tooBynder hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="93e63-215">**tooassign Britta Simon tooBynder, perform hello following steps:**</span></span>

1. <span data-ttu-id="93e63-216">Hello 클래식 포털에서 tooopen hello 응용 프로그램 보기 hello 디렉터리 보기를 클릭 **응용 프로그램** hello 최상위 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-216">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![사용자 할당][201]
2. <span data-ttu-id="93e63-218">Hello 응용 프로그램 목록에서 선택 **Bynder**합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-218">In hello applications list, select **Bynder**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. <span data-ttu-id="93e63-220">Hello 메뉴에서 hello 위에 표시를 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-220">In hello menu on hello top, click **Users**.</span></span>
   
    ![사용자 할당][203]
4. <span data-ttu-id="93e63-222">Hello [사용자] 목록에서 선택 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-222">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="93e63-223">Hello 아래쪽에 hello 도구 모음에서 클릭 **할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-223">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![사용자 할당][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="93e63-225">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="93e63-225">Test single sign-on</span></span>
<span data-ttu-id="93e63-226">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Microsoft Azure AD SSO 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-226">hello objective of this section is tootest your Microsoft Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="93e63-227">Hello 액세스 패널에서에서 hello Bynder 타일을 클릭할 때 자동으로 로그온 tooyour Bynder 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e63-227">When you click hello Bynder tile in hello Access Panel, you should get automatically signed-on tooyour Bynder application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="93e63-228">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="93e63-228">Additional resources</span></span>
* [<span data-ttu-id="93e63-229">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="93e63-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="93e63-230">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="93e63-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
