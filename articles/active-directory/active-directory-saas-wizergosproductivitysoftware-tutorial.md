---
title: "자습서: Wizergos Productivity Software와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Wizergos 생산성 소프트웨어 간의 합니다."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: cdd186c38c426dde404ed8bb84700faf9c8c1a46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a><span data-ttu-id="119e7-103">자습서: Wizergos Productivity Software와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="119e7-103">Tutorial: Azure Active Directory integration with Wizergos Productivity Software</span></span>
<span data-ttu-id="119e7-104">이 자습서의 hello 목적은 tooshow 있습니다 어떻게 toointegrate Wizergos 생산성 소프트웨어와 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="119e7-104">hello objective of this tutorial is tooshow you how toointegrate Wizergos Productivity Software  with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="119e7-105">다음 이점을 hello로 제공 Wizergos 생산성 소프트웨어 Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="119e7-105">Integrating Wizergos Productivity Software with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="119e7-106">Azure ad 액세스 tooWizergos 생산성 소프트웨어를 가진 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-106">You can control in Azure AD who has access tooWizergos Productivity Software</span></span>
* <span data-ttu-id="119e7-107">Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooWizergos 생산성 소프트웨어 single sign on (SSO)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-107">You can enable your users tooautomatically get signed-on tooWizergos Productivity Software single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="119e7-108">하나의 중앙 위치-hello Azure 클래식 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="119e7-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="119e7-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="119e7-110">Prerequisites</span></span>
<span data-ttu-id="119e7-111">다음 항목 hello가 필요 tooconfigure Wizergos 생산성 소프트웨어와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-111">tooconfigure Azure AD integration with Wizergos Productivity Software, you need hello following items:</span></span>

* <span data-ttu-id="119e7-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="119e7-112">An Azure AD subscription</span></span>
* <span data-ttu-id="119e7-113">Wizergos Productivity Software SSO가 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="119e7-113">A Wizergos Productivity Software SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="119e7-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="119e7-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="119e7-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="119e7-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="119e7-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="119e7-118">Scenario description</span></span>
<span data-ttu-id="119e7-119">이 자습서의 hello 목적은 tooenable 있습니다 tootest Azure AD SSO 테스트 환경에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-119">hello objective of this tutorial is tooenable you tootest Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="119e7-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="119e7-121">Hello 갤러리에서 Wizergos 생산성 소프트웨어 추가</span><span class="sxs-lookup"><span data-stu-id="119e7-121">Adding Wizergos Productivity Software from hello gallery</span></span>
2. <span data-ttu-id="119e7-122">Azure AD SSO 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="119e7-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-wizergos-productivity-software-from-hello-gallery"></a><span data-ttu-id="119e7-123">Hello 갤러리에서 Wizergos 생산성 소프트웨어 추가</span><span class="sxs-lookup"><span data-stu-id="119e7-123">Adding Wizergos Productivity Software from hello gallery</span></span>
<span data-ttu-id="119e7-124">tooconfigure hello와의 통합 Wizergos 생산성 소프트웨어 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Wizergos 생산성 소프트웨어 tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-124">tooconfigure hello integration of Wizergos Productivity Software into Azure AD, you need tooadd Wizergos Productivity Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="119e7-125">**hello 갤러리에서 Wizergos 생산성 소프트웨어 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="119e7-125">**tooadd Wizergos Productivity Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="119e7-126">Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-126">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="119e7-128">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="119e7-129">tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![응용 프로그램][2]
4. <span data-ttu-id="119e7-131">클릭 **추가** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![응용 프로그램][3]
5. <span data-ttu-id="119e7-133">Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![응용 프로그램][4]
6. <span data-ttu-id="119e7-135">Hello 검색 상자에 입력 **Wizergos 생산성 소프트웨어**합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-135">In hello search box, type **Wizergos Productivity Software**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. <span data-ttu-id="119e7-137">Hello 결과 패널에서 선택 **Wizergos 생산성 소프트웨어**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-137">In hello results panel, select **Wizergos Productivity Software**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Hello 갤러리에서 hello 앱 선택](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="119e7-139">Azure AD SSO 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="119e7-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="119e7-140">이 섹션의 hello 목적은 tooshow "Britta Simon" 이라는 테스트 사용자에 따라 tooconfigure 및 Azure AD SSO Wizergos 생산성 소프트웨어 및 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD SSO with Wizergos Productivity Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="119e7-141">SSO toowork에 대 한 Azure AD는 tooknow Wizergos 생산성 소프트웨어 tooan 사용자 Azure ad에서에서 어떤 hello 테이블에 해당 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-141">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Wizergos Productivity Software tooan user in Azure AD is.</span></span> <span data-ttu-id="119e7-142">즉, Azure AD 사용자 및 Wizergos 생산성 소프트웨어에서 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-142">In other words, a link relationship between an Azure AD user and hello related user in Wizergos Productivity Software needs toobe established.</span></span>

<span data-ttu-id="119e7-143">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Wizergos 생산성 소프트웨어에서.</span><span class="sxs-lookup"><span data-stu-id="119e7-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Wizergos Productivity Software.</span></span>

<span data-ttu-id="119e7-144">tooconfigure 및 BynWizergos 생산성 Softwareder를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-144">tooconfigure and test Azure AD single sign-on with BynWizergos Productivity Softwareder, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="119e7-145">**[Azure AD single sign-on 구성](#configuring-azure-ad-single-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="119e7-146">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="119e7-147">**[Wizergos 생산성 소프트웨어 테스트 사용자 만들기](#creating-a-wizergos-productivity-software-test-user)**  -toohave 그녀의 연결 된 Azure AD toohello 표현인 Wizergos 생산성 소프트웨어에서 Britta Simon의 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-147">**[Creating a Wizergos Productivity Software test user](#creating-a-wizergos-productivity-software-test-user)** - toohave a counterpart of Britta Simon in Wizergos Productivity Software that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="119e7-148">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="119e7-149">**[Single sign on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="119e7-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="119e7-150">Azure AD SSO 구성</span><span class="sxs-lookup"><span data-stu-id="119e7-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="119e7-151">이 섹션에서는 Azure AD에서 single sign-on hello 클래식 포털의 설정 및 Wizergos 생산성 소프트웨어 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Wizergos Productivity Software application.</span></span>

<span data-ttu-id="119e7-152">**Wizergos 생산성 소프트웨어와 함께 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="119e7-152">**tooconfigure Azure AD single sign-on with Wizergos Productivity Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="119e7-153">Hello에 hello 클래식 포털에서 **Wizergos 생산성 소프트웨어** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **구성 Single Sign-on**대화 상자.</span><span class="sxs-lookup"><span data-stu-id="119e7-153">In hello classic portal, on hello **Wizergos Productivity Software** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Single Sign-on 구성][6] 
2. <span data-ttu-id="119e7-155">Hello에 **어떻게 tooWizergos 생산성 소프트웨어에서 사용자가 toosign 보 시겠습니까** 페이지에서 **Azure AD Single Sign-on**, 클릭 하 고 **다음**:</span><span class="sxs-lookup"><span data-stu-id="119e7-155">On hello **How would you like users toosign on tooWizergos Productivity Software** page, select **Azure AD Single Sign-On**, and then click **Next**:</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. <span data-ttu-id="119e7-157">Hello에 **앱 설정 구성** 대화 상자 페이지에서 클릭 **다음**:</span><span class="sxs-lookup"><span data-stu-id="119e7-157">On hello **Configure App Settings** dialog page, click **Next**:</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. <span data-ttu-id="119e7-159">Hello에 **Wizergos 생산성 Software에서 single sign on 구성** 페이지 **다운로드 인증서**, hello 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-159">On hello **Configure single sign-on at Wizergos Productivity Software** page, click **Download certificate**, and then save hello file on your computer:</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. <span data-ttu-id="119e7-161">다른 웹 브라우저 창에서 관리자 권한으로 로그온 tooyour Wizergos 생산성 소프트웨어 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-161">In a different web browser window, sign-on tooyour Wizergos Productivity Software tenant as an administrator.</span></span>
6. <span data-ttu-id="119e7-162">Hello 햄버거 메뉴에서 선택 **Admin**합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-162">From hello hamburger menu, select **Admin**.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. <span data-ttu-id="119e7-164">왼쪽 메뉴의 관리자 페이지에서 **인증**을 선택하고 **Azure AD**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-164">In Admin page on left hand menu select **AUTHENTICATION** and click on **Azure AD**.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. <span data-ttu-id="119e7-166">Hello 다음 단계를 수행 **인증** 섹션.</span><span class="sxs-lookup"><span data-stu-id="119e7-166">Perform hello following steps on **AUTHENTICATION** section.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. <span data-ttu-id="119e7-168">클릭 **업로드** 단추 tooupload hello Azure AD에서 인증서를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-168">Click **UPLOAD** button tooupload hello downloaded certificate from Azure AD.</span></span> 
  2. <span data-ttu-id="119e7-169">Hello에 **발급자 URL** textbox 배치의 hello 값 **발급자 URL** Azure AD 응용 프로그램 구성 마법사에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-169">In hello **Issuer URL** textbox put hello value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
  3. <span data-ttu-id="119e7-170">Hello에 **Single Sign On URL** textbox 배치의 hello 값 **Single sign-on 서비스 URL** Azure AD 응용 프로그램 구성 마법사에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-170">In hello **Single Sign-On URL** textbox put hello value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
  4. <span data-ttu-id="119e7-171">Hello에 **Single Sign-Out URL** textbox 배치의 hello 값 **Single Sign-out 서비스 URL** Azure AD 응용 프로그램 구성 마법사에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-171">In hello **Single Sign-Out URL** textbox put hello value of **Single Sign-out Service URL** from Azure AD application configuration wizard.</span></span>
  5. <span data-ttu-id="119e7-172">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-172">Click **Save** button.</span></span>
9. <span data-ttu-id="119e7-173">Hello 클래식 포털의 hello single sign-on 구성 확인을 선택한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-173">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
10. <span data-ttu-id="119e7-175">Hello에 **Single sign on 확인** 페이지 **완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-175">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="119e7-177">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="119e7-177">Create an Azure AD test user</span></span>
<span data-ttu-id="119e7-178">이 섹션의 hello 목표 Britta Simon 라는 hello 클래식 포털에서 toocreate 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-178">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][20]

<span data-ttu-id="119e7-180">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="119e7-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="119e7-181">Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-181">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="119e7-183">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-183">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="119e7-184">toodisplay hello 목록이 hello 바탕 화면에서 hello 메뉴에서 사용자가 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-184">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="119e7-186">tooopen hello **사용자 추가** hello 아래쪽에 hello 도구 모음에서 대화 상자에서 클릭 **사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-186">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="119e7-188">Hello에 **이 사용자에 대해 알리기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-188">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="119e7-190">사용자 유형에서 조직의 새 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="119e7-191">Hello 사용자 이름에서에서 **textbox**, 형식 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-191">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="119e7-192">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-192">Click **Next**.</span></span>
6. <span data-ttu-id="119e7-193">Hello에 **사용자 프로필** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-193">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="119e7-195">Hello에 **이름** 텍스트 상자에 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-195">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="119e7-196">Hello에 **성** 텍스트 상자에, **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-196">In hello **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="119e7-197">Hello에 **표시 이름** 텍스트 상자에 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-197">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="119e7-198">Hello에 **역할** 목록에서 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-198">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="119e7-199">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-199">Click **Next**.</span></span>
7. <span data-ttu-id="119e7-200">Hello에 **임시 암호 가져오기** 대화 상자 페이지에서 클릭 **만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-200">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="119e7-202">Hello에 **임시 암호 가져오기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="119e7-204">Hello hello 값 적어 **새 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-204">Write down hello value of hello **New Password**.</span></span>
  2. <span data-ttu-id="119e7-205">페이지 맨 아래에 있는 **완료**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="119e7-205">Click **Complete**.</span></span>   

### <a name="create-a-wizergos-productivity-software-test-user"></a><span data-ttu-id="119e7-206">Wizergos Productivity Software 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="119e7-206">Create a Wizergos Productivity Software test user</span></span>
<span data-ttu-id="119e7-207">이 섹션에서는 Wizergos Productivity Software에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-207">In this section, you create a user called Britta Simon in Wizergos Productivity Software.</span></span> <span data-ttu-id="119e7-208">통해 Wizergos 생산성 소프트웨어 지원 팀과 협력 하세요 [ support@wizergos.com ](emailTo:support@wizergos.com) hello Wizergos 생산성 소프트웨어 플랫폼의 tooadd hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-208">Please work with Wizergos Productivity Software support team via [support@wizergos.com](emailTo:support@wizergos.com) tooadd hello users in hello Wizergos Productivity Software platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="119e7-209">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-209">Assign hello Azure AD test user</span></span>
<span data-ttu-id="119e7-210">이 섹션의 hello 목표 그녀의 액세스 tooWizergos 생산성 소프트웨어를 부여 하 여 tooenabling Britta Simon toouse Azure SSO를입니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-210">hello objective of this section is tooenabling Britta Simon toouse Azure SSO by granting her access tooWizergos Productivity Software.</span></span>

  ![사용자 할당][200]

<span data-ttu-id="119e7-212">**tooassign Britta Simon tooWizergos 생산성 소프트웨어 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="119e7-212">**tooassign Britta Simon tooWizergos Productivity Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="119e7-213">Hello 클래식 포털에서 tooopen hello 응용 프로그램 보기 hello 디렉터리 보기를 클릭 **응용 프로그램** hello 최상위 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-213">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![사용자 할당][201]
2. <span data-ttu-id="119e7-215">Hello 응용 프로그램 목록에서 선택 **Wizergos 생산성 소프트웨어**합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-215">In hello applications list, select **Wizergos Productivity Software**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. <span data-ttu-id="119e7-217">Hello 메뉴에서 hello 위에 표시를 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-217">In hello menu on hello top, click **Users**.</span></span>
   
    ![사용자 할당][203]
4. <span data-ttu-id="119e7-219">Hello [사용자] 목록에서 선택 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-219">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="119e7-220">Hello 아래쪽에 hello 도구 모음에서 클릭 **할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-220">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![사용자 할당][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="119e7-222">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="119e7-222">Test single sign-on</span></span>
<span data-ttu-id="119e7-223">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD SSO 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-223">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="119e7-224">Hello 액세스 패널에서에서 hello Wizergos 생산성 소프트웨어 타일을 클릭할 때 자동으로 로그온 tooyour Wizergos 생산성 소프트웨어 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="119e7-224">When you click hello Wizergos Productivity Software tile in hello Access Panel, you should get automatically signed-on tooyour Wizergos Productivity Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="119e7-225">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="119e7-225">Additional resources</span></span>
* [<span data-ttu-id="119e7-226">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="119e7-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="119e7-227">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="119e7-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
