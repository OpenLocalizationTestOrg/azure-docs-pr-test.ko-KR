---
title: "자습서: SciQuest Spend Director와 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory 및 SciQuest 지출 디렉터 사이입니다."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 47c46f1297054fd96b86c1d8c66e1a55ec151497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a><span data-ttu-id="459a0-103">자습서: SciQuest Spend Director와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="459a0-103">Tutorial: Azure Active Directory integration with SciQuest Spend Director</span></span>
<span data-ttu-id="459a0-104">이 자습서의 hello 목적은 tooshow 있습니다 어떻게 toointegrate Azure Active Directory (Azure AD)와 SciQuest 지출 감독 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-104">hello objective of this tutorial is tooshow you how toointegrate SciQuest Spend Director with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="459a0-105">이점 다음 hello로 제공 SciQuest 지출 Director Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="459a0-105">Integrating SciQuest Spend Director with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="459a0-106">액세스 tooSciQuest 지출 감독을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-106">You can control in Azure AD who has access tooSciQuest Spend Director</span></span> 
* <span data-ttu-id="459a0-107">에 사용자가 tooautomatically get 로그온 tooSciQuest (Single Sign-on)는 Azure AD 계정와 지출 감독을 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-107">You can enable your users tooautomatically get signed-on tooSciQuest Spend Director (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="459a0-108">하나의 중앙 위치-hello Azure 클래식 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="459a0-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="459a0-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="459a0-110">Prerequisites</span></span>
<span data-ttu-id="459a0-111">다음 항목 hello가 필요 tooconfigure SciQuest 지출 디렉터와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-111">tooconfigure Azure AD integration with SciQuest Spend Director, you need hello following items:</span></span>

* <span data-ttu-id="459a0-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="459a0-112">An Azure AD subscription</span></span>
* <span data-ttu-id="459a0-113">SciQuest Spend Director Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="459a0-113">A SciQuest Spend Director single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="459a0-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="459a0-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="459a0-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="459a0-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="459a0-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="459a0-118">Scenario Description</span></span>
<span data-ttu-id="459a0-119">이 자습서의 hello 목적은 tooenable 있습니다 tootest Azure AD에서 single sign-on 테스트 환경에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="459a0-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="459a0-121">SciQuest 지출 디렉터 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="459a0-121">Adding SciQuest Spend Director from hello gallery</span></span> 
2. <span data-ttu-id="459a0-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="459a0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sciquest-spend-director-from-hello-gallery"></a><span data-ttu-id="459a0-123">SciQuest 지출 디렉터 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="459a0-123">Adding SciQuest Spend Director from hello gallery</span></span>
<span data-ttu-id="459a0-124">tooconfigure hello 통합 SciQuest 지출 Director의 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 SciQuest 지출 디렉터 tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-124">tooconfigure hello integration of SciQuest Spend Director into Azure AD, you need tooadd SciQuest Spend Director from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="459a0-125">**hello 갤러리에서 SciQuest 지출 디렉터 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="459a0-125">**tooadd SciQuest Spend Director from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="459a0-126">Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="459a0-128">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="459a0-129">tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![응용 프로그램][2]

4. <span data-ttu-id="459a0-131">클릭 **추가** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![응용 프로그램][3]

5. <span data-ttu-id="459a0-133">Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![응용 프로그램][4]

6. <span data-ttu-id="459a0-135">Hello 검색 상자에 입력 **sciQuest 지출 director**합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-135">In hello search box, type **sciQuest spend director**.</span></span>
   
    ![응용 프로그램][5]

7. <span data-ttu-id="459a0-137">Hello 결과 창에서 선택 **SciQuest 지출 Director**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-137">In hello results pane, select **SciQuest Spend Director**, and then click **Complete** tooadd hello application.</span></span>
   
    ![응용 프로그램][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="459a0-139">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="459a0-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="459a0-140">이 섹션의 hello 목적은 tooshow "Britta Simon" 이라는 테스트 사용자에 따라 tooconfigure 및 SciQuest 지출 Director를 사용 하 여 Azure AD에서 single sign-on 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with SciQuest Spend Director based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="459a0-141">Single sign on toowork에 대 한 Azure AD는 tooknow SciQuest 지출 감독 tooan 사용자 Azure ad에서에서 어떤 hello 테이블에 해당 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SciQuest Spend Director tooan user in Azure AD is.</span></span> <span data-ttu-id="459a0-142">즉, Azure AD 사용자 및 SciQuest 지출 Director에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-142">In other words, a link relationship between an Azure AD user and hello related user in SciQuest Spend Director needs toobe established.</span></span>  
<span data-ttu-id="459a0-143">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** SciQuest 지출 Director에 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SciQuest Spend Director.</span></span>

<span data-ttu-id="459a0-144">tooconfigure 및 SciQuest 지출 Director를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-144">tooconfigure and test Azure AD single sign-on with SciQuest Spend Director, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="459a0-145">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-145">**[Configuring Azure AD Single Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="459a0-146">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="459a0-147">**[SciQuest 지출 감독 테스트 사용자 만들기](#creating-a-halogen-software-test-user)**  -toohave Britta Simon 표현인 연결 된 Azure AD toohello 그녀의 SciQuest 지출 Director에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-147">**[Creating a SciQuest Spend Director test user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in SciQuest Spend Director that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="459a0-148">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="459a0-149">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="459a0-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-single-sign-on"></a><span data-ttu-id="459a0-150">Azure AD Single Sign-on 구성</span><span class="sxs-lookup"><span data-stu-id="459a0-150">Configuring Azure AD Single Single Sign-On</span></span>
<span data-ttu-id="459a0-151">hello이이 섹션에서는 tooenable Azure AD에서 single sign-on hello Azure 클래식 포털에서에서 및 tooconfigure single sign on SciQuest 지출 Director 응용 프로그램에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-151">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your SciQuest Spend Director application.</span></span>

<span data-ttu-id="459a0-152">**SciQuest 지출 디렉터와 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="459a0-152">**tooconfigure Azure AD single sign-on with SciQuest Spend Director, perform hello following steps:**</span></span>

1. <span data-ttu-id="459a0-153">Hello hello에 Azure 클래식 포털에서에서 **SciQuest 지출 Director** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **구성 Single Sign-on**대화 상자.</span><span class="sxs-lookup"><span data-stu-id="459a0-153">In hello Azure classic portal, on hello **SciQuest Spend Director** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Single Sign-on 구성][8]

2. <span data-ttu-id="459a0-155">Hello에 **어떻게 tooSciQuest 지출 Director에 대 한 사용자가 toosign 보 시겠습니까** 페이지에서 **Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-155">On hello **How would you like users toosign on tooSciQuest Spend Director** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][9]

3. <span data-ttu-id="459a0-157">Hello에 **앱 설정 구성** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span> 
   
    ![앱 설정 구성][10]
   
     <span data-ttu-id="459a0-159">a.</span><span class="sxs-lookup"><span data-stu-id="459a0-159">a.</span></span> <span data-ttu-id="459a0-160">Hello에 **로그온 URL** 텍스트 상자에 URL는 사용 하면 사용자가 toosign tooyour SciQuest 지출 Director hello 패턴을 사용 하 여 응용 프로그램에 의해: *https://.* sciquest.com/.**</span><span class="sxs-lookup"><span data-stu-id="459a0-160">In hello **Sign On URL** textbox, type your URL used by your users toosign on tooyour SciQuest Spend Director application using hello following pattern: *https://.*sciquest.com/.**</span></span>
   
     <span data-ttu-id="459a0-161">b.</span><span class="sxs-lookup"><span data-stu-id="459a0-161">b.</span></span> <span data-ttu-id="459a0-162">Hello에 **회신 URL** 동일 값 텍스트 상자, 형식 hello hello에 입력 한 **로그온 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-162">In hello **Reply URL** textbox, type hello same value you have typed into hello **Sign On URL** textbox.</span></span> 
   
     <span data-ttu-id="459a0-163">c.</span><span class="sxs-lookup"><span data-stu-id="459a0-163">c.</span></span> <span data-ttu-id="459a0-164">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-164">Click **Next**.</span></span>

4. <span data-ttu-id="459a0-165">Hello에 **SciQuest 지출 Director에서 single sign on 구성** 페이지 **메타 데이터 다운로드**, hello 메타 데이터 파일을 컴퓨터에 로컬로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-165">On hello **Configure single sign-on at SciQuest Spend Director** page, click **Download metadata**, and then save hello metadata file locally on your computer.</span></span>
   
    ![Azure AD Connect의 정의][11]

5. <span data-ttu-id="459a0-167">SciQuest 지원 tooenable를 hello 위의 다운로드 한 메타 데이터를 사용 하 여이 인증 방법을 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="459a0-167">Contact SciQuest support tooenable this authentication method using hello above downloaded metadata.</span></span>

6. <span data-ttu-id="459a0-168">Azure 클래식 포털 hello에 hello single sign on 구성 확인을 선택한 다음 클릭 **완료** tooclose hello **Single Sign-on 구성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="459a0-168">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span> 
   
    ![Azure AD Connect의 정의][15]

7. <span data-ttu-id="459a0-170">Hello에 **Single sign on 확인** 페이지 **완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-170">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="459a0-171">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="459a0-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="459a0-172">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 클래식 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-172">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="459a0-173">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="459a0-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="459a0-174">Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-174">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Azure AD Connect의 정의][100] 

2. <span data-ttu-id="459a0-176">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-176">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="459a0-177">toodisplay hello 목록이 hello 바탕 화면에서 hello 메뉴에서 사용자가 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-177">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Azure AD Connect의 정의][101] 

4. <span data-ttu-id="459a0-179">tooopen hello **사용자 추가** hello 아래쪽에 hello 도구 모음에서 대화 상자에서 클릭 **사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-179">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Azure AD Connect의 정의][102] 

5. <span data-ttu-id="459a0-181">Hello에 **이 사용자에 대해 알리기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-181">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD Connect의 정의][103] 
   
    <span data-ttu-id="459a0-183">a.</span><span class="sxs-lookup"><span data-stu-id="459a0-183">a.</span></span> <span data-ttu-id="459a0-184">**사용자 유형**에서 **조직의 새 사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-184">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="459a0-185">b.</span><span class="sxs-lookup"><span data-stu-id="459a0-185">b.</span></span> <span data-ttu-id="459a0-186">Hello 사용자 이름에서에서 **textbox**, 형식 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-186">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="459a0-187">c.</span><span class="sxs-lookup"><span data-stu-id="459a0-187">c.</span></span> <span data-ttu-id="459a0-188">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-188">Click **Next**.</span></span>

6. <span data-ttu-id="459a0-189">Hello에 **사용자 프로필** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-189">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Azure AD Connect의 정의][104] 
   
    <span data-ttu-id="459a0-191">a.</span><span class="sxs-lookup"><span data-stu-id="459a0-191">a.</span></span> <span data-ttu-id="459a0-192">Hello에 **이름** 텍스트 상자에 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-192">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="459a0-193">b.</span><span class="sxs-lookup"><span data-stu-id="459a0-193">b.</span></span> <span data-ttu-id="459a0-194">Hello에 **성** txtbox, 형식, **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-194">In hello **Last Name** txtbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="459a0-195">c.</span><span class="sxs-lookup"><span data-stu-id="459a0-195">c.</span></span> <span data-ttu-id="459a0-196">Hello에 **표시 이름** 텍스트 상자에 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-196">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="459a0-197">d.</span><span class="sxs-lookup"><span data-stu-id="459a0-197">d.</span></span> <span data-ttu-id="459a0-198">Hello에 **역할** 목록에서 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-198">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="459a0-199">e.</span><span class="sxs-lookup"><span data-stu-id="459a0-199">e.</span></span> <span data-ttu-id="459a0-200">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-200">Click **Next**.</span></span>

7. <span data-ttu-id="459a0-201">Hello에 **임시 암호 가져오기** 대화 상자 페이지에서 클릭 **만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-201">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Azure AD Connect의 정의][105]  

8. <span data-ttu-id="459a0-203">Hello에 **임시 암호 가져오기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-203">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD Connect의 정의][106]   
   
    <span data-ttu-id="459a0-205">a.</span><span class="sxs-lookup"><span data-stu-id="459a0-205">a.</span></span> <span data-ttu-id="459a0-206">Hello hello 값 적어 **새 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-206">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="459a0-207">b.</span><span class="sxs-lookup"><span data-stu-id="459a0-207">b.</span></span> <span data-ttu-id="459a0-208">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-208">Click **Complete**.</span></span>   

### <a name="creating-a-sciquest-spend-director-test-user"></a><span data-ttu-id="459a0-209">SciQuest Spend Director 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="459a0-209">Creating a SciQuest Spend Director test user</span></span>
<span data-ttu-id="459a0-210">hello이이 섹션의 목적은 toocreate Britta Simon SciQuest 지출 Director에서 호출 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-210">hello objective of this section is toocreate a user called Britta Simon in SciQuest Spend Director.</span></span>

<span data-ttu-id="459a0-211">Toocontact SciQuest 지출 감독 지원 팀 필요 하 고 자신이 만들어진 테스트 계정 tooget 프로그램에 대 한 hello 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-211">You need toocontact your SciQuest Spend Director support team and provide them with hello details about your test account tooget it created.</span></span>

<span data-ttu-id="459a0-212">또는 SciQuest Spend Director에서 지원되는 Single Sign-On 기능인 Just-in-Tme 프로비저닝을 활용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-212">Alternatively, you can also leverage just-in-time provisioning, a single sign-on feature that is supported by SciQuest Spend Director.</span></span>  
<span data-ttu-id="459a0-213">Just-in-Tme 프로비전을 사용하도록 설정한 경우 계정이 없는 사용자가 Single Sign-On 시도를 수행하는 동안 SciQuest Spend Director에서 사용자 계정이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-213">If just-in-time provisioning is enabled, users are automatically created by SciQuest Spend Director during a single sign-on attempt if they don't exist.</span></span> <span data-ttu-id="459a0-214">이 기능은 hello 필요성 제거 toomanually single sign on 관련 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-214">This feature eliminates hello need toomanually create single sign-on counterpart users.</span></span>

<span data-ttu-id="459a0-215">tooget 적시에 프로 비전을 사용 하도록 설정 했으면 SciQuest 지출 감독 지원 팀 toocontact를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-215">tooget just-in-time provisioning enabled, you need toocontact your your SciQuest Spend Director support team.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="459a0-216">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-216">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="459a0-217">이 섹션의 hello 목표에는 자신의 액세스 tooSciQuest 지출 감독을 부여 하 여 tooenabling Britta Simon toouse Azure single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-217">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSciQuest Spend Director.</span></span>

![Azure AD Connect의 정의][200]

<span data-ttu-id="459a0-219">**tooassign Britta Simon tooSciQuest 지출 디렉터 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="459a0-219">**tooassign Britta Simon tooSciQuest Spend Director, perform hello following steps:**</span></span>

1. <span data-ttu-id="459a0-220">Hello Azure 클래식 포털 tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 최상위 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-220">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Azure AD Connect의 정의][201]

2. <span data-ttu-id="459a0-222">Hello 응용 프로그램 목록에서 선택 **SciQuest 지출 Director**합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-222">In hello applications list, select **SciQuest Spend Director**.</span></span>
   
    ![Azure AD Connect의 정의][202]

3. <span data-ttu-id="459a0-224">Hello 메뉴에서 hello 위에 표시를 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-224">In hello menu on hello top, click **Users**.</span></span>
   
    ![Azure AD Connect의 정의][203]

4. <span data-ttu-id="459a0-226">Hello [사용자] 목록에서 선택 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-226">In hello Users list, select **Britta Simon**.</span></span>
   
    ![Azure AD Connect의 정의][204]

5. <span data-ttu-id="459a0-228">Hello 아래쪽에 hello 도구 모음에서 클릭 **할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-228">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Azure AD Connect의 정의][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="459a0-230">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="459a0-230">Testing Single Sign-On</span></span>
<span data-ttu-id="459a0-231">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-231">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="459a0-232">Hello 액세스 패널에서에서 hello SciQuest 지출 Director 타일을 클릭할 때 자동으로 로그온 tooyour SciQuest 지출 Director 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="459a0-232">When you click hello SciQuest Spend Director tile in hello Access Panel, you should get automatically signed-on tooyour SciQuest Spend Director application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="459a0-233">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="459a0-233">Additional Resources</span></span>
* [<span data-ttu-id="459a0-234">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="459a0-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="459a0-235">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="459a0-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_01.png
[6]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_05.png
[8]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_07.png
[10]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_08.png
[11]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_03.png
[15]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_15.png 
[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_06.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_18.png
[204]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_19.png
[205]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_20.png

