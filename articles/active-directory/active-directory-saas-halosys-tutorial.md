---
title: "자습서: Halosys와 Azure Active Directory 통합 | Microsoft Docs"
description: "방법을 toouse Halosys tooenable Azure Active Directory와 single sign on, 자동화 된 프로비저닝 및 더에 대해 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18043ed1b6f7ab45c59cfd36252bef1621618e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a><span data-ttu-id="b14a7-103">자습서: Halosys와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="b14a7-103">Tutorial: Azure Active Directory integration with Halosys</span></span>

<span data-ttu-id="b14a7-104">이 자습서에 설명 어떻게 toointegrate Halosys Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b14a7-104">In this tutorial, you learn how toointegrate Halosys with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b14a7-105">다음 이점을 hello로 제공 Halosys Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="b14a7-105">Integrating Halosys with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b14a7-106">액세스 tooHalosys을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-106">You can control in Azure AD who has access tooHalosys</span></span>
- <span data-ttu-id="b14a7-107">프로그램 사용자 tooautomatically get 로그온 tooHalosys (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-107">You can enable your users tooautomatically get signed-on tooHalosys (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b14a7-108">하나의 중앙 위치-hello Azure 클래식 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="b14a7-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b14a7-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b14a7-110">Prerequisites</span></span>

<span data-ttu-id="b14a7-111">다음 항목 hello가 필요 tooconfigure Halosys와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-111">tooconfigure Azure AD integration with Halosys, you need hello following items:</span></span>

- <span data-ttu-id="b14a7-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="b14a7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b14a7-113">Halosys Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="b14a7-113">A Halosys single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="b14a7-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="b14a7-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b14a7-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="b14a7-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="b14a7-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="b14a7-118">Scenario description</span></span>
<span data-ttu-id="b14a7-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="b14a7-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b14a7-121">Halosys는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="b14a7-121">Adding Halosys from hello gallery</span></span>
2. <span data-ttu-id="b14a7-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b14a7-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-halosys-from-hello-gallery"></a><span data-ttu-id="b14a7-123">Halosys는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="b14a7-123">Adding Halosys from hello gallery</span></span>
<span data-ttu-id="b14a7-124">tooconfigure hello와의 통합 Halosys Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Halosys tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-124">tooconfigure hello integration of Halosys into Azure AD, you need tooadd Halosys from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b14a7-125">**hello 갤러리에서 Halosys tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b14a7-125">**tooadd Halosys from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b14a7-126">Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]
2. <span data-ttu-id="b14a7-128">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="b14a7-129">tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![응용 프로그램][2]

4. <span data-ttu-id="b14a7-131">클릭 **추가** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-131">Click **Add** at hello bottom of hello page.</span></span>

    ![응용 프로그램][3]

5. <span data-ttu-id="b14a7-133">Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>

    ![응용 프로그램][4]

6. <span data-ttu-id="b14a7-135">Hello 검색 상자에 입력 **Halosys**합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-135">In hello search box, type **Halosys**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. <span data-ttu-id="b14a7-137">Hello 결과 창에서 선택 **Halosys**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-137">In hello results pane, select **Halosys**, and then click **Complete** tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b14a7-139">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b14a7-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b14a7-140">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Halosys에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-140">In this section, you configure and test Azure AD single sign-on with Halosys based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b14a7-141">Single sign on toowork에 대 한 Azure AD는 tooknow Halosys에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Halosys is tooa user in Azure AD.</span></span> <span data-ttu-id="b14a7-142">즉, Azure AD 사용자 및 Halosys에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-142">In other words, a link relationship between an Azure AD user and hello related user in Halosys needs toobe established.</span></span>

<span data-ttu-id="b14a7-143">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Halosys에 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Halosys.</span></span>

<span data-ttu-id="b14a7-144">tooconfigure 및 Halosys 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-144">tooconfigure and test Azure AD single sign-on with Halosys, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b14a7-145">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b14a7-146">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b14a7-147">**[Halosys 테스트 사용자 만들기](#creating-a-halosys-test-user)**  -toohave Britta Simon 그녀의 연결 된 Azure AD toohello 표현인 Halosys에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-147">**[Creating a Halosys test user](#creating-a-halosys-test-user)** - toohave a counterpart of Britta Simon in Halosys that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="b14a7-148">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b14a7-149">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="b14a7-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b14a7-150">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="b14a7-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b14a7-151">이 섹션에서는 Azure AD에서 single sign-on hello 클래식 포털의 설정 및 Halosys 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Halosys application.</span></span>


<span data-ttu-id="b14a7-152">**tooconfigure Azure AD single sign on, Halosys와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b14a7-152">**tooconfigure Azure AD single sign-on with Halosys, perform hello following steps:**</span></span>

1. <span data-ttu-id="b14a7-153">Hello에 hello 클래식 포털에서 **Halosys** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **구성 Single Sign-on** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="b14a7-153">In hello classic portal, on hello **Halosys** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
     
    ![Single Sign-on 구성][6] 

2. <span data-ttu-id="b14a7-155">Hello에 **어떻게 tooHalosys에 사용자가 toosign 보 시겠습니까** 페이지에서 **Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-155">On hello **How would you like users toosign on tooHalosys** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. <span data-ttu-id="b14a7-157">Hello에 **앱 설정 구성** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    <span data-ttu-id="b14a7-159">a.</span><span class="sxs-lookup"><span data-stu-id="b14a7-159">a.</span></span> <span data-ttu-id="b14a7-160">Hello에 **로그온 URL** 텍스트 패턴 hello를 사용 하 여 사용자에 대 한 toosign tooyour Halosys 응용 프로그램에서 사용 하는 hello URL 입력: `https://<company-name>.Halosys.com/client-api/api`합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-160">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Halosys application using hello following pattern: `https://<company-name>.Halosys.com/client-api/api`.</span></span>

    <span data-ttu-id="b14a7-161">임시로 hello **식별자 URL** 텍스트 패턴 hello에 hello URL 입력: `https://<company-name>.Halosys.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-161">b.In hello **Identifier URL** textbox, type hello URL in hello following pattern: `https://<company-name>.Halosys.com`.</span></span> 
         
4. <span data-ttu-id="b14a7-162">Hello에 **Halosys에서 single sign on 구성** 페이지 **메타 데이터 다운로드**, hello 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-162">On hello **Configure single sign-on at Halosys** page, click **Download metadata**, and then save hello file on your computer:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. <span data-ttu-id="b14a7-164">tooget SSO 응용 프로그램에 대해 구성 된 Halosys 지원 팀에 문의 하 고 hello 다음을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-164">tooget SSO configured for your application, contact Halosys support team and provide them with hello following:</span></span>

    <span data-ttu-id="b14a7-165">다운로드 한 • hello **메타 데이터 파일**</span><span class="sxs-lookup"><span data-stu-id="b14a7-165">• hello downloaded **metadata file**</span></span>
    
    <span data-ttu-id="b14a7-166">• hello **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="b14a7-166">• hello **SAML SSO URL**</span></span>
    

6. <span data-ttu-id="b14a7-167">Hello 클래식 포털의 hello single sign-on 구성 확인을 선택한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-167">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD Single Sign-On][10]

7. <span data-ttu-id="b14a7-169">Hello에 **Single sign on 확인** 페이지 **완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-169">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD Single Sign-On][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b14a7-171">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b14a7-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="b14a7-172">이 섹션에서는 Britta Simon 라는 hello 클래식 포털의 테스트 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-172">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>


![Azure AD 사용자 만들기][20]

<span data-ttu-id="b14a7-174">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b14a7-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b14a7-175">Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-175">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="b14a7-177">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-177">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="b14a7-178">toodisplay hello 목록이 hello 바탕 화면에서 hello 메뉴에서 사용자가 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-178">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b14a7-180">tooopen hello **사용자 추가** hello 아래쪽에 hello 도구 모음에서 대화 상자에서 클릭 **사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-180">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="b14a7-182">Hello에 **이 사용자에 대해 알리기** 대화 상자 페이지에서 수행할 단계를 수행 하는 hello: ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="b14a7-182">On hello **Tell us about this user** dialog page, perform hello following steps:  ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span></span> 

    <span data-ttu-id="b14a7-183">a.</span><span class="sxs-lookup"><span data-stu-id="b14a7-183">a.</span></span> <span data-ttu-id="b14a7-184">사용자 유형에서 조직의 새 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-184">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="b14a7-185">b.</span><span class="sxs-lookup"><span data-stu-id="b14a7-185">b.</span></span> <span data-ttu-id="b14a7-186">Hello 사용자 이름에서에서 **textbox**, 형식 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-186">In hello User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b14a7-187">c.</span><span class="sxs-lookup"><span data-stu-id="b14a7-187">c.</span></span> <span data-ttu-id="b14a7-188">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-188">Click **Next**.</span></span>

6.  <span data-ttu-id="b14a7-189">Hello에 **사용자 프로필** 대화 상자 페이지에서 수행할 단계를 수행 하는 hello: ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="b14a7-189">On hello **User Profile** dialog page, perform hello following steps: ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span></span> 

    <span data-ttu-id="b14a7-190">a.</span><span class="sxs-lookup"><span data-stu-id="b14a7-190">a.</span></span> <span data-ttu-id="b14a7-191">Hello에 **이름** 텍스트 상자에 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-191">In hello **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="b14a7-192">b.</span><span class="sxs-lookup"><span data-stu-id="b14a7-192">b.</span></span> <span data-ttu-id="b14a7-193">Hello에 **성** 텍스트 상자에, **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-193">In hello **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="b14a7-194">c.</span><span class="sxs-lookup"><span data-stu-id="b14a7-194">c.</span></span> <span data-ttu-id="b14a7-195">Hello에 **표시 이름** 텍스트 상자에 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-195">In hello **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="b14a7-196">d.</span><span class="sxs-lookup"><span data-stu-id="b14a7-196">d.</span></span> <span data-ttu-id="b14a7-197">Hello에 **역할** 목록에서 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-197">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="b14a7-198">e.</span><span class="sxs-lookup"><span data-stu-id="b14a7-198">e.</span></span> <span data-ttu-id="b14a7-199">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-199">Click **Next**.</span></span>

7. <span data-ttu-id="b14a7-200">Hello에 **임시 암호 가져오기** 대화 상자 페이지에서 클릭 **만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-200">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="b14a7-202">Hello에 **임시 암호 가져오기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="b14a7-204">a.</span><span class="sxs-lookup"><span data-stu-id="b14a7-204">a.</span></span> <span data-ttu-id="b14a7-205">Hello hello 값 적어 **새 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-205">Write down hello value of hello **New Password**.</span></span>

    <span data-ttu-id="b14a7-206">b.</span><span class="sxs-lookup"><span data-stu-id="b14a7-206">b.</span></span> <span data-ttu-id="b14a7-207">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-207">Click **Complete**.</span></span>   



### <a name="creating-a-halosys-test-user"></a><span data-ttu-id="b14a7-208">Halosys 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b14a7-208">Creating a Halosys test user</span></span>

<span data-ttu-id="b14a7-209">이 섹션에서는 Halosys에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-209">In this section, you create a user called Britta Simon in Halosys.</span></span> <span data-ttu-id="b14a7-210">와 협력 하세요 Halosys hello Halosys 플랫폼에서 지원 팀 tooadd hello 사용자.</span><span class="sxs-lookup"><span data-stu-id="b14a7-210">Please work with Halosys support team tooadd hello users in hello Halosys platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b14a7-211">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b14a7-212">이 섹션에서는 액세스 tooHalosys 그녀의 권한을 부여 하 여 Azure single sign on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooHalosys.</span></span>

![사용자 할당][200] 

<span data-ttu-id="b14a7-214">**tooassign Britta Simon tooHalosys hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b14a7-214">**tooassign Britta Simon tooHalosys, perform hello following steps:**</span></span>

1. <span data-ttu-id="b14a7-215">Hello 클래식 포털에서 tooopen hello 응용 프로그램 보기 hello 디렉터리 보기를 클릭 **응용 프로그램** hello 최상위 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-215">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="b14a7-217">Hello 응용 프로그램 목록에서 선택 **Halosys**합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-217">In hello applications list, select **Halosys**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. <span data-ttu-id="b14a7-219">Hello 메뉴에서 hello 위에 표시를 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-219">In hello menu on hello top, click **Users**.</span></span>

    ![사용자 할당][203]

4. <span data-ttu-id="b14a7-221">Hello [사용자] 목록에서 선택 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-221">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="b14a7-222">Hello 아래쪽에 hello 도구 모음에서 클릭 **할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-222">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![사용자 할당][205]


### <a name="testing-single-sign-on"></a><span data-ttu-id="b14a7-224">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="b14a7-224">Testing single sign-on</span></span>

<span data-ttu-id="b14a7-225">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b14a7-226">Hello Halosys hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour Halosys 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b14a7-226">When you click hello Halosys tile in hello Access Panel, you should get automatically signed-on tooyour Halosys application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="b14a7-227">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b14a7-227">Additional resources</span></span>

* [<span data-ttu-id="b14a7-228">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="b14a7-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b14a7-229">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b14a7-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
