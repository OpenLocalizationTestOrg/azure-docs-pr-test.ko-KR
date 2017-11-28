---
title: "자습서: Azure Active Directory와 통합 @Task| Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory 간의 및 @Task합니다."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0840763622086a02a27cfafff3b741bc66cec498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a><span data-ttu-id="37898-103">자습서: @Task와(과) Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="37898-103">Tutorial: Azure Active Directory integration with @Task</span></span>
<span data-ttu-id="37898-104">이 자습서의 hello 목적은 tooshow 있습니다 어떻게 toointegrate @Task Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="37898-104">hello objective of this tutorial is tooshow you how toointegrate @Task with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="37898-105">통합 @Task Azure AD와 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-105">Integrating @Task with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="37898-106">액세스할 수 있는 Azure AD에서 제어할 수 있습니다.too@Task</span><span class="sxs-lookup"><span data-stu-id="37898-106">You can control in Azure AD who has access too@Task</span></span>
* <span data-ttu-id="37898-107">로그온 tooautomatically 가져올 사용자가 사용 하도록 설정할 수 too@Task (Single Sign-on)는 Azure AD 계정을 사용</span><span class="sxs-lookup"><span data-stu-id="37898-107">You can enable your users tooautomatically get signed-on too@Task (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="37898-108">하나의 중앙 위치-hello Azure 클래식 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37898-108">You can manage your accounts in one central location - hello Azure classic Portal</span></span>

<span data-ttu-id="37898-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37898-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="37898-110">Prerequisites</span></span>
<span data-ttu-id="37898-111">tooconfigure Azure AD와의 통합 @Task, hello 다음 항목을 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-111">tooconfigure Azure AD integration with @Task, you need hello following items:</span></span>

* <span data-ttu-id="37898-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="37898-112">An Azure AD subscription</span></span>
* <span data-ttu-id="37898-113">@Task Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="37898-113">An @Task single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="37898-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="37898-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="37898-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="37898-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37898-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="37898-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="37898-118">Scenario Description</span></span>
<span data-ttu-id="37898-119">이 자습서의 hello 목적은 tooenable 있습니다 tootest Azure AD에서 single sign-on 테스트 환경에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="37898-120">이 자습서에 설명 된 hello 시나리오 세 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37898-120">hello scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="37898-121">추가 @Task hello 갤러리에서</span><span class="sxs-lookup"><span data-stu-id="37898-121">Adding @Task from hello gallery</span></span> 
2. <span data-ttu-id="37898-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="37898-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-task-from-hello-gallery"></a><span data-ttu-id="37898-123">추가 @Task hello 갤러리에서</span><span class="sxs-lookup"><span data-stu-id="37898-123">Adding @Task from hello gallery</span></span>
<span data-ttu-id="37898-124">tooconfigure hello 통합 @Task tooadd 해야 Azure AD로 @Task 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-124">tooconfigure hello integration of @Task into Azure AD, you need tooadd @Task from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="37898-125">**tooadd @Task hello 갤러리에서 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="37898-125">**tooadd @Task from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="37898-126">Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1] 
2. <span data-ttu-id="37898-128">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="37898-129">tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![응용 프로그램][2] 
4. <span data-ttu-id="37898-131">클릭 **추가** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37898-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![응용 프로그램][3] 
5. <span data-ttu-id="37898-133">Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![응용 프로그램][4] 
6. <span data-ttu-id="37898-135">Hello 검색 상자에 입력  **@Task** 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-135">In hello search box, type **@Task**.</span></span>
   
    ![응용 프로그램][5] 
7. <span data-ttu-id="37898-137">Hello 결과 창에서 선택  **@Task** , 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="37898-137">In hello results pane, select **@Task**, and then click **Complete** tooadd hello application.</span></span>
   
    ![응용 프로그램][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="37898-139">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="37898-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="37898-140">hello이 섹션은 tooconfigure 및 테스트 Azure AD의 단일 하면 사용 하 여 로그온 tooshow @Task "Britta Simon" 이라는 테스트 사용자를 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with @Task based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="37898-141">Single sign on toowork에 대 한 Azure AD는 필요 tooknow hello 테이블에 해당 사용자의 @Task tooan Azure ad에서는 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37898-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in @Task tooan user in Azure AD is.</span></span> <span data-ttu-id="37898-142">즉, Azure AD 사용자와의 hello 관련된 사용자 간 링크 관계 @Task toobe 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-142">In other words, a link relationship between an Azure AD user and hello related user in @Task needs toobe established.</span></span>   
<span data-ttu-id="37898-143">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** 에서 @Task합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in @Task.</span></span>

<span data-ttu-id="37898-144">tooconfigure 및 테스트 Azure AD single sign on와 @Task, toocomplete hello 구성 요소를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-144">tooconfigure and test Azure AD single sign-on with @Task, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="37898-145">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="37898-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="37898-146">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="37898-147">**[만들기는 @Tasktest 사용자](#creating-a-halogen-software-test-user)**  -Britta Simon의 상응 하는 toohave @Taskthat 그녀의 연결 된 Azure AD toohello 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="37898-147">**[Creating a @Tasktest user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in @Taskthat is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="37898-148">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="37898-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="37898-149">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="37898-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="37898-150">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="37898-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="37898-151">이 섹션의 hello 목표는 tooenable Azure AD에서 single sign-on hello Azure 클래식 포털에서에서 및 tooconfigure single sign on에서 프로그램 @Task 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="37898-151">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your @Task application.</span></span>

<span data-ttu-id="37898-152">**와 Azure AD에서 single sign-on tooconfigure @Task, hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="37898-152">**tooconfigure Azure AD single sign-on with @Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="37898-153">Hello hello에 Azure 클래식 포털에서에서  **@Task**  응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **구성 Single Sign-on**  대화 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="37898-153">In hello Azure classic portal, on hello **@Task** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Single Sign-on 구성][6] 
2. <span data-ttu-id="37898-155">Hello에 **어떻게에 사용자가 toosign 보 시겠습니까 too@Task**  페이지에서 **Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-155">On hello **How would you like users toosign on too@Task** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][7] 
3. <span data-ttu-id="37898-157">Hello에 **앱 설정 구성** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>
   
    ![앱 설정 구성][8] 
   
     <span data-ttu-id="37898-159">a.</span><span class="sxs-lookup"><span data-stu-id="37898-159">a.</span></span> <span data-ttu-id="37898-160">Hello에 **로그온 URL** 텍스트 상자에 toosign tooyour 사용자에서 사용 하는 hello URL 입력 @Task 응용 프로그램 (예::*https://<Tenant name>.attask ondemand.com*).</span><span class="sxs-lookup"><span data-stu-id="37898-160">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour @Task application (e.g.:*https://<Tenant name>.attask-ondemand.com*).</span></span>
   
     <span data-ttu-id="37898-161">b.</span><span class="sxs-lookup"><span data-stu-id="37898-161">b.</span></span> <span data-ttu-id="37898-162">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="37898-162">Click **Next**.</span></span>
4. <span data-ttu-id="37898-163">Hello에 **single sign-on 구성에서 @Task**  페이지 **메타 데이터 다운로드**, hello 메타 데이터 파일을 컴퓨터에 로컬로 저장 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-163">On hello **Configure single sign-on at @Task** page, click **Download metadata**, save hello metadata file locally on your computer, and then click **Next**.</span></span>
   
    ![Azure AD Connect의 정의][9] 
5. <span data-ttu-id="37898-165">로그온 tooyour @Task 회사 사이트에서 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-165">Sign-on tooyour @Task company site as administrator.</span></span>
6. <span data-ttu-id="37898-166">너무 이동**Single Sign On 구성을**합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-166">Go too**Single Sign On Configuration**.</span></span>
7. <span data-ttu-id="37898-167">Hello에 **Single Sign On** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-167">On hello **Single Sign-On** dialog, perform hello following steps</span></span>
   
    ![Single Sign-on 구성][23]
   
    <span data-ttu-id="37898-169">a.</span><span class="sxs-lookup"><span data-stu-id="37898-169">a.</span></span> <span data-ttu-id="37898-170">**형식**으로 **SAML 2.0**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-170">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="37898-171">b.</span><span class="sxs-lookup"><span data-stu-id="37898-171">b.</span></span> <span data-ttu-id="37898-172">**서비스 공급자 ID**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-172">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="37898-173">c.</span><span class="sxs-lookup"><span data-stu-id="37898-173">c.</span></span> <span data-ttu-id="37898-174">Hello Azure 클래식 포털에서 복사 hello **원격 로그인 URL**, 다음 hello에 붙여 넣는 **로그인 포털 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="37898-174">On hello Azure classic portal, copy hello **Remote Login URL**, and then paste it into hello **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="37898-175">d.</span><span class="sxs-lookup"><span data-stu-id="37898-175">d.</span></span> <span data-ttu-id="37898-176">Hello Azure 클래식 포털에서 복사 hello **Single Sign-Out 서비스 URL**, 다음 hello에 붙여 넣는 **Sign-Out URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="37898-176">On hello Azure classic portal, copy hello **Single Sign-Out Service URL**, and then paste it into hello **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="37898-177">e.</span><span class="sxs-lookup"><span data-stu-id="37898-177">e.</span></span> <span data-ttu-id="37898-178">Hello Azure 클래식 포털에서 복사 hello **암호 변경 URL**, 다음 hello에 붙여 넣는 **암호 변경 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="37898-178">On hello Azure classic portal, copy hello **Change Password URL**, and then paste it into hello **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="37898-179">f.</span><span class="sxs-lookup"><span data-stu-id="37898-179">f.</span></span> <span data-ttu-id="37898-180">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-180">Click **Save**.</span></span>
8. <span data-ttu-id="37898-181">Azure 클래식 포털 hello에 hello single sign on 구성 확인을 선택한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-181">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Azure AD Connect의 정의][10]
9. <span data-ttu-id="37898-183">Hello에 **Single sign on 확인** 페이지 **완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-183">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Connect의 정의][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="37898-185">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="37898-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="37898-186">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 클래식 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="37898-186">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>  

![Azure AD 사용자 만들기][20]

<span data-ttu-id="37898-188">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="37898-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="37898-189">Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-189">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. <span data-ttu-id="37898-191">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-191">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="37898-192">toodisplay hello 목록이 hello 바탕 화면에서 hello 메뉴에서 사용자가 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-192">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="37898-194">tooopen hello **사용자 추가** hello 아래쪽에 hello 도구 모음에서 대화 상자에서 클릭 **사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-194">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="37898-196">Hello에 **이 사용자에 대해 알리기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-196">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span> 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="37898-198">a.</span><span class="sxs-lookup"><span data-stu-id="37898-198">a.</span></span> <span data-ttu-id="37898-199">사용자 유형에서 조직의 새 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-199">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="37898-200">b.</span><span class="sxs-lookup"><span data-stu-id="37898-200">b.</span></span> <span data-ttu-id="37898-201">Hello 사용자 이름에서에서 **textbox**, 형식 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-201">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="37898-202">c.</span><span class="sxs-lookup"><span data-stu-id="37898-202">c.</span></span> <span data-ttu-id="37898-203">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="37898-203">Click **Next**.</span></span>
6. <span data-ttu-id="37898-204">Hello에 **사용자 프로필** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-204">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="37898-206">a.</span><span class="sxs-lookup"><span data-stu-id="37898-206">a.</span></span> <span data-ttu-id="37898-207">Hello에 **이름** 텍스트 상자에 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-207">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="37898-208">b.</span><span class="sxs-lookup"><span data-stu-id="37898-208">b.</span></span> <span data-ttu-id="37898-209">Hello에 **성** 텍스트 상자에, **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-209">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="37898-210">c.</span><span class="sxs-lookup"><span data-stu-id="37898-210">c.</span></span> <span data-ttu-id="37898-211">Hello에 **표시 이름** 텍스트 상자에 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-211">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="37898-212">d.</span><span class="sxs-lookup"><span data-stu-id="37898-212">d.</span></span> <span data-ttu-id="37898-213">Hello에 **역할** 목록에서 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-213">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="37898-214">e.</span><span class="sxs-lookup"><span data-stu-id="37898-214">e.</span></span> <span data-ttu-id="37898-215">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="37898-215">Click **Next**.</span></span>

7. <span data-ttu-id="37898-216">Hello에 **임시 암호 가져오기** 대화 상자 페이지에서 클릭 **만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-216">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="37898-218">Hello에 **임시 암호 가져오기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-218">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="37898-220">a.</span><span class="sxs-lookup"><span data-stu-id="37898-220">a.</span></span> <span data-ttu-id="37898-221">Hello hello 값 적어 **새 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-221">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="37898-222">b.</span><span class="sxs-lookup"><span data-stu-id="37898-222">b.</span></span> <span data-ttu-id="37898-223">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-223">Click **Complete**.</span></span>   

### <a name="creating-an-task-test-user"></a><span data-ttu-id="37898-224">@Task 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="37898-224">Creating an @Task test user</span></span>
<span data-ttu-id="37898-225">이 섹션의 hello 목적은 toocreate Britta Simon 라는 사용자를 만들면 @Task합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-225">hello objective of this section is toocreate a user called Britta Simon in @Task.</span></span>

<span data-ttu-id="37898-226">**toocreate Britta Simon 라는 사용자를 만들면 @Task, hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="37898-226">**toocreate a user called Britta Simon in @Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="37898-227">Tooyour 로그온 @Task 회사 사이트에서 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-227">Sign on tooyour @Task company site as administrator.</span></span>
2. <span data-ttu-id="37898-228">Hello 메뉴에서 hello 위에 표시를 클릭 **사람**합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-228">In hello menu on hello top, click **People**.</span></span>
3. <span data-ttu-id="37898-229">**새 사람**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-229">Click **New Person**.</span></span> 
4. <span data-ttu-id="37898-230">Hello New Person 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-230">On hello New Person dialog, perform hello following steps:</span></span>
   
    ![@Task 테스트 사용자 만들기][21] 
   
    <span data-ttu-id="37898-232">a.</span><span class="sxs-lookup"><span data-stu-id="37898-232">a.</span></span> <span data-ttu-id="37898-233">Hello에 **이름** textbox "Britta"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-233">In hello **First Name** textbox, type "Britta".</span></span>
   
    <span data-ttu-id="37898-234">b.</span><span class="sxs-lookup"><span data-stu-id="37898-234">b.</span></span> <span data-ttu-id="37898-235">Hello에 **성** textbox "Simon"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-235">In hello **Last Name** textbox, type "Simon".</span></span>
   
    <span data-ttu-id="37898-236">c.</span><span class="sxs-lookup"><span data-stu-id="37898-236">c.</span></span> <span data-ttu-id="37898-237">Hello에 **전자 메일 주소** 텍스트 상자에 Azure Active Directory Britta Simon의 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-237">In hello **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="37898-238">d.</span><span class="sxs-lookup"><span data-stu-id="37898-238">d.</span></span> <span data-ttu-id="37898-239">**사람 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-239">Click **Add Person**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="37898-240">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-240">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="37898-241">이 섹션의 hello 목표 그녀의 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse tooenabling는 too@Task합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-241">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access too@Task.</span></span>

![사용자 할당][200] 

<span data-ttu-id="37898-243">**tooassign Britta Simon too@Task, hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="37898-243">**tooassign Britta Simon too@Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="37898-244">Hello Azure 클래식 포털 tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 최상위 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37898-244">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![사용자 할당][201] 
2. <span data-ttu-id="37898-246">Hello 응용 프로그램 목록에서 선택  **@Task** 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-246">In hello applications list, select **@Task**.</span></span>
   
    ![사용자 할당][202] 
3. <span data-ttu-id="37898-248">Hello 메뉴에서 hello 위에 표시를 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-248">In hello menu on hello top, click **Users**.</span></span>
   
    ![사용자 할당][203] 
4. <span data-ttu-id="37898-250">Hello [사용자] 목록에서 선택 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-250">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="37898-251">Hello 아래쪽에 hello 도구 모음에서 클릭 **할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-251">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![사용자 할당][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="37898-253">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="37898-253">Testing Single Sign-On</span></span>
<span data-ttu-id="37898-254">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="37898-254">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="37898-255">Hello를 클릭할 때 @Task 타일에 액세스 패널 hello, 자동으로 로그온 tooyour 얻어야 @Task 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="37898-255">When you click hello @Task tile in hello Access Panel, you should get automatically signed-on tooyour @Task application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="37898-256">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="37898-256">Additional Resources</span></span>
* [<span data-ttu-id="37898-257">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="37898-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="37898-258">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="37898-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






