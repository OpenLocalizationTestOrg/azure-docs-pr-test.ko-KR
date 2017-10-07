---
title: "자습서: Splunk Enterprise and Splunk Cloud와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Splunk 엔터프라이즈 Splunk 클라우드 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: 9bb6817cb31dce684cd9cc1c567fa3efc8906ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="d55a5-103">자습서: Splunk Enterprise and Splunk Cloud와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="d55a5-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="d55a5-104">이 자습서에 설명 어떻게 toointegrate Splunk Enterprise와 Azure Active Directory (Azure AD)와 Splunk 클라우드입니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-104">In this tutorial, you learn how toointegrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d55a5-105">이점 다음 hello로 제공 Splunk 엔터프라이즈 및 클라우드 Splunk Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="d55a5-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d55a5-106">TooSplunk 엔터프라이즈 및 클라우드 Splunk 액세스할 수 있는 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-106">You can control in Azure AD who has access tooSplunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="d55a5-107">Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooSplunk Splunk 클라우드 및 대기업 single sign on (SSO)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-107">You can enable your users tooautomatically get signed-on tooSplunk Enterprise and Splunk Cloud single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="d55a5-108">하나의 중앙 위치-hello Azure 클래식 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="d55a5-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d55a5-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d55a5-110">Prerequisites</span></span>

<span data-ttu-id="d55a5-111">다음 항목 hello가 필요 tooconfigure Splunk 엔터프라이즈 및 클라우드 Splunk와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-111">tooconfigure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need hello following items:</span></span>

- <span data-ttu-id="d55a5-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="d55a5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d55a5-113">Splunk Enterprise and Splunk Cloud SSO가 사용하도록 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="d55a5-113">A Splunk Enterprise or Splunk Cloud SSO enabled subscription</span></span>


>[!NOTE]
><span data-ttu-id="d55a5-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="d55a5-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d55a5-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d55a5-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="d55a5-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="d55a5-118">Scenario description</span></span>
<span data-ttu-id="d55a5-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="d55a5-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d55a5-121">Hello 갤러리에서 Splunk 엔터프라이즈 및 클라우드 Splunk 추가</span><span class="sxs-lookup"><span data-stu-id="d55a5-121">Adding Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
2. <span data-ttu-id="d55a5-122">Azure AD SSO 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d55a5-122">Configuring and testing Azure AD SSO</span></span>


## <a name="add-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a><span data-ttu-id="d55a5-123">Hello 갤러리에서 Splunk 엔터프라이즈 및 Splunk 클라우드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-123">Add Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
<span data-ttu-id="d55a5-124">tooconfigure hello와의 통합 Splunk 엔터프라이즈 및 클라우드 Splunk Azure AD로 tooadd Splunk 엔터프라이즈 및 hello 갤러리 tooyour 목록에서 Splunk 클라우드 SaaS 앱을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-124">tooconfigure hello integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need tooadd Splunk Enterprise and Splunk Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d55a5-125">**hello 갤러리에서 Splunk 클라우드 및 tooadd Splunk 대기업 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d55a5-125">**tooadd Splunk Enterprise and Splunk Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d55a5-126">Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]

2. <span data-ttu-id="d55a5-128">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="d55a5-129">tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![응용 프로그램][2]

4. <span data-ttu-id="d55a5-131">클릭 **추가** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-131">Click **Add** at hello bottom of hello page.</span></span>

    ![응용 프로그램][3]

5. <span data-ttu-id="d55a5-133">Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>

    ![응용 프로그램][4]

6. <span data-ttu-id="d55a5-135">Hello 검색 상자에 입력 **Splunk Enterprise 또는 Splunk 클라우드**합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-135">In hello search box, type **Splunk Enterprise or Splunk Cloud**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. <span data-ttu-id="d55a5-137">Hello 결과 창에서 선택 **Splunk 엔터프라이즈 및 클라우드 Splunk**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-137">In hello results pane, select **Splunk Enterprise and Splunk Cloud**, and then click **Complete** tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d55a5-139">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d55a5-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="d55a5-140">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Splunk Enterprise and Splunk Cloud에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-140">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d55a5-141">Single sign on toowork에 대 한 Azure AD는 tooknow Splunk 클라우드 및 Splunk 대기업에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Splunk Enterprise and Splunk Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="d55a5-142">즉, Azure AD 사용자 및 Splunk Enterprise 및 Splunk 클라우드 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-142">In other words, a link relationship between an Azure AD user and hello related user in Splunk Enterprise and Splunk Cloud needs toobe established.</span></span>

<span data-ttu-id="d55a5-143">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Splunk Enterprise 및 Splunk 클라우드입니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Splunk Enterprise and Splunk Cloud.</span></span>

<span data-ttu-id="d55a5-144">tooconfigure 및 Splunk 엔터프라이즈 및 Splunk 클라우드를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-144">tooconfigure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d55a5-145">**[Azure AD single sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d55a5-146">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d55a5-147">**[Splunk 엔터프라이즈 및 클라우드 Splunk 테스트 사용자 만들기](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  -toohave Splunk 기업의 Britta Simon 및 그녀의 연결 된 Azure AD toohello 표현인 Splunk 클라우드 상응 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-147">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - toohave a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="d55a5-148">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d55a5-149">**[Single sign on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="d55a5-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d55a5-150">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="d55a5-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d55a5-151">이 섹션에서는 hello 클래식 포털에서 Azure AD SSO를 사용 하도록 설정 및 Splunk 엔터프라이즈 및 Splunk 클라우드 응용 프로그램에서 SSO를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-151">In this section, you enable Azure AD SSO in hello classic portal and configure SSO in your Splunk Enterprise and Splunk Cloud application.</span></span>


<span data-ttu-id="d55a5-152">**Splunk 클라우드 Splunk Enterprise와 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d55a5-152">**tooconfigure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="d55a5-153">Hello에 hello 클래식 포털에서 **Splunk 엔터프라이즈 및 클라우드 Splunk** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **구성 Single Sign-on** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="d55a5-153">In hello classic portal, on hello **Splunk Enterprise and Splunk Cloud** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
     
    ![Single Sign-on 구성][6] 

2. <span data-ttu-id="d55a5-155">Hello에 **त ु म tooSplunk Enterprise에 사용자가 toosign 및 Splunk 클라우드** 페이지에서 **Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-155">On hello **How would you like users toosign on tooSplunk Enterprise and Splunk Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. <span data-ttu-id="d55a5-157">Hello에 **앱 설정 구성** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. <span data-ttu-id="d55a5-159">Hello에 **로그온 URL** textbox, 사용자에 대 한 toosign tooyour Splunk 엔터프라이즈 및 패턴 hello를 사용 하 여 Splunk 클라우드 응용 프로그램에서 사용 하는 hello URL 입력:`https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="d55a5-159">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Splunk Enterprise and Splunk Cloud application using hello following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
  2. <span data-ttu-id="d55a5-160">Hello에 **식별자** textbox Splunk 서버 hello URL 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-160">In hello **Identifier** textbox, type hello URL of your Splunk Server.</span></span>
  3. <span data-ttu-id="d55a5-161">Hello에 **회신 URL** 텍스트 패턴 hello로 hello URL 입력:`https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="d55a5-161">In hello **Reply URL** textbox, type hello URL with hello following pattern: `https://<splunkserver>/saml/acs`</span></span>
  4. <span data-ttu-id="d55a5-162">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-162">Click **Next**.</span></span>
 
4. <span data-ttu-id="d55a5-163">Hello에 **Splunk 클라우드 및 Splunk 대기업에서 single sign on 구성** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-163">On hello **Configure single sign-on at Splunk Enterprise and Splunk Cloud** page, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. <span data-ttu-id="d55a5-165">클릭 **메타 데이터 다운로드**, hello 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-165">Click **Download metadata**, and then save hello file on your computer.</span></span>
  2. <span data-ttu-id="d55a5-166">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-166">Click **Next**.</span></span>

5. <span data-ttu-id="d55a5-167">tooget SSO 응용 프로그램에 대해 구성 된 Splunk 엔터프라이즈 및 클라우드 Splunk 지원 팀에 문의 하 고 hello 다음을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-167">tooget SSO configured for your application, contact Splunk Enterprise and Splunk Cloud support team and provide them with hello following:</span></span>

    * <span data-ttu-id="d55a5-168">다운로드 한 hello **federaton 메타 데이터**</span><span class="sxs-lookup"><span data-stu-id="d55a5-168">hello downloaded **federaton metadata**</span></span>
6. <span data-ttu-id="d55a5-169">Hello 클래식 포털의 hello single sign-on 구성 확인을 선택한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-169">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD Single Sign-On][10]

7. <span data-ttu-id="d55a5-171">Hello에 **Single sign on 확인** 페이지 **완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-171">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d55a5-173">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d55a5-173">Create an Azure AD test user</span></span>
<span data-ttu-id="d55a5-174">이 섹션에서는 Britta Simon 라는 hello 클래식 포털의 테스트 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-174">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][20]

<span data-ttu-id="d55a5-176">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d55a5-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d55a5-177">Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-177">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="d55a5-179">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-179">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="d55a5-180">toodisplay hello 목록이 hello 바탕 화면에서 hello 메뉴에서 사용자가 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-180">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d55a5-182">tooopen hello **사용자 추가** hello 아래쪽에 hello 도구 모음에서 대화 상자에서 클릭 **사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-182">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="d55a5-184">Hello에 **이 사용자에 대해 알리기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-184">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="d55a5-186">사용자 유형에서 조직의 새 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-186">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="d55a5-187">Hello 사용자 이름에서에서 **textbox**, 형식 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-187">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="d55a5-188">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-188">Click **Next**.</span></span>

6.  <span data-ttu-id="d55a5-189">Hello에 **사용자 프로필** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-189">On hello **User Profile** dialog page, perform hello following steps:</span></span>
  
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="d55a5-191">Hello에 **이름** 텍스트 상자에 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-191">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="d55a5-192">Hello에 **성** 텍스트 상자에, **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-192">In hello **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="d55a5-193">Hello에 **표시 이름** 텍스트 상자에 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-193">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="d55a5-194">Hello에 **역할** 목록에서 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-194">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="d55a5-195">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-195">Click **Next**.</span></span>

7. <span data-ttu-id="d55a5-196">Hello에 **임시 암호 가져오기** 대화 상자 페이지에서 클릭 **만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-196">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="d55a5-198">Hello에 **임시 암호 가져오기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-198">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="d55a5-200">Hello hello 값 적어 **새 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-200">Write down hello value of hello **New Password**.</span></span>
  2. <span data-ttu-id="d55a5-201">페이지 맨 아래에 있는 **완료**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d55a5-201">Click **Complete**.</span></span>   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="d55a5-202">Splunk Enterprise and Splunk Cloud 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d55a5-202">Create a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="d55a5-203">이 섹션에서는 Splunk Enterprise and Splunk Cloud에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-203">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="d55a5-204">하십시오 작업할 Splunk 엔터프라이즈 및 클라우드 Splunk hello Splunk 엔터프라이즈 및 Splunk 클라우드 플랫폼에서 지원 팀 tooadd hello 사용자.</span><span class="sxs-lookup"><span data-stu-id="d55a5-204">Please work with Splunk Enterprise and Splunk Cloud support team tooadd hello users in hello Splunk Enterprise and Splunk Cloud platform.</span></span>


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="d55a5-205">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-205">Assign hello Azure AD test user</span></span>

<span data-ttu-id="d55a5-206">이 섹션에서는 Azure SSOy 그녀의 액세스 tooSplunk 엔터프라이즈 및 클라우드 Splunk 부여 Britta Simon toouse를 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-206">In this section, you enable Britta Simon toouse Azure SSOy granting her access tooSplunk Enterprise and Splunk Cloud.</span></span>

![사용자 할당][200] 

<span data-ttu-id="d55a5-208">**tooassign Britta Simon tooSplunk 엔터프라이즈 및 Splunk 클라우드 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d55a5-208">**tooassign Britta Simon tooSplunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="d55a5-209">Hello 클래식 포털에서 tooopen hello 응용 프로그램 보기 hello 디렉터리 보기를 클릭 **응용 프로그램** hello 최상위 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-209">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="d55a5-211">Hello 응용 프로그램 목록에서 선택 **Splunk 엔터프라이즈 및 클라우드 Splunk**합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-211">In hello applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. <span data-ttu-id="d55a5-213">Hello 메뉴에서 hello 위에 표시를 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-213">In hello menu on hello top, click **Users**.</span></span>

    ![사용자 할당][203]

4. <span data-ttu-id="d55a5-215">Hello [사용자] 목록에서 선택 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-215">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="d55a5-216">Hello 아래쪽에 hello 도구 모음에서 클릭 **할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-216">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![사용자 할당][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="d55a5-218">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="d55a5-218">Test single sign-on</span></span>

<span data-ttu-id="d55a5-219">이 섹션에서는 hello 액세스 패널을 사용 하 여 Azure AD SSOonfiguration 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-219">In this section, you test your Azure AD SSOonfiguration using hello Access Panel.</span></span>

<span data-ttu-id="d55a5-220">Hello Splunk 엔터프라이즈 및 hello 액세스 패널에서에서 Splunk 클라우드 타일을 클릭할 때 자동으로 로그온 tooyour Splunk Enterprise 및 Splunk 클라우드 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d55a5-220">When you click hello Splunk Enterprise and Splunk Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Splunk Enterprise and Splunk Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d55a5-221">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d55a5-221">Additional resources</span></span>

* [<span data-ttu-id="d55a5-222">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="d55a5-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d55a5-223">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d55a5-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
