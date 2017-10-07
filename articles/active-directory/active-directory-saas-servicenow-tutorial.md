---
title: "자습서: ServiceNow와 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 ServiceNow ServiceNow Express 사이입니다."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: df6a07dd1aa437198fbdb9d0a04ea14f3a320249
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a><span data-ttu-id="7518a-103">자습서: ServiceNow와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="7518a-103">Tutorial: Azure Active Directory integration with ServiceNow</span></span>
<span data-ttu-id="7518a-104">이 자습서에 설명 어떻게 toointegrate ServiceNow와 Azure Active Directory (Azure AD)와 ServiceNow Express입니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-104">In this tutorial, you learn how toointegrate ServiceNow and ServiceNow Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7518a-105">Azure AD와 ServiceNow 및 Express ServiceNow를 통합 hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-105">Integrating ServiceNow and ServiceNow Express with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="7518a-106">액세스 tooServiceNow을 지닌 Azure AD와 ServiceNow Express에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-106">You can control in Azure AD who has access tooServiceNow and ServiceNow Express</span></span>
* <span data-ttu-id="7518a-107">Azure AD 계정을와 tooServiceNow 로그온 사용자 tooautomatically get 및 ServiceNow Express (Single Sign-on)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-107">You can enable your users tooautomatically get signed-on tooServiceNow and ServiceNow Express (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="7518a-108">하나의 중앙 위치-hello Azure 클래식 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="7518a-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7518a-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7518a-110">Prerequisites</span></span>
<span data-ttu-id="7518a-111">ServiceNow 및 Express ServiceNow와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-111">tooconfigure Azure AD integration with ServiceNow and ServiceNow Express, you need hello following items:</span></span>

* <span data-ttu-id="7518a-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="7518a-112">An Azure AD subscription</span></span>
* <span data-ttu-id="7518a-113">ServiceNow의 경우 ServiceNow의 인스턴스 또는 테넌트, Calgary 버전 이상</span><span class="sxs-lookup"><span data-stu-id="7518a-113">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span></span>
* <span data-ttu-id="7518a-114">ServiceNow Express의 경우 ServiceNow Express의 인스턴스, Helsinki 버전 이상</span><span class="sxs-lookup"><span data-stu-id="7518a-114">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span></span>
* <span data-ttu-id="7518a-115">hello ServiceNow 테 넌 트 hello 있어야 [여러 공급자 Single Sign에 플러그 인](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-115">hello ServiceNow tenant must have hello [Multiple Provider Single Sign On Plugin](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) enabled.</span></span> <span data-ttu-id="7518a-116">[서비스 요청을 제출](https://hi.service-now.com)하면 이렇게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-116">This can be done by [submitting a service request](https://hi.service-now.com).</span></span> 

> [!NOTE]
> <span data-ttu-id="7518a-117">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-117">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="7518a-118">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="7518a-119">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-119">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="7518a-120">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-120">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7518a-121">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="7518a-121">Scenario description</span></span>
<span data-ttu-id="7518a-122">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7518a-123">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7518a-124">ServiceNow는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="7518a-124">Adding ServiceNow from hello gallery</span></span>
2. <span data-ttu-id="7518a-125">ServiceNow 또는 ServiceNow Express에 대한 Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="7518a-125">Configuring and testing Azure AD single sign-on for ServiceNow or ServiceNow Express</span></span>

## <a name="adding-servicenow-from-hello-gallery"></a><span data-ttu-id="7518a-126">ServiceNow는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="7518a-126">Adding ServiceNow from hello gallery</span></span>
<span data-ttu-id="7518a-127">tooconfigure hello와의 통합 ServiceNow 또는 ServiceNow Express Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 ServiceNow tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-127">tooconfigure hello integration of ServiceNow or ServiceNow Express into Azure AD, you need tooadd ServiceNow from hello gallery tooyour list of managed SaaS apps.</span></span> 

<span data-ttu-id="7518a-128">**hello 갤러리에서 ServiceNow tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="7518a-128">**tooadd ServiceNow from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7518a-129">Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-129">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="7518a-131">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-131">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="7518a-132">tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-132">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![응용 프로그램][2]
4. <span data-ttu-id="7518a-134">클릭 **추가** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-134">Click **Add** at hello bottom of hello page.</span></span>
   
    ![응용 프로그램][3]
5. <span data-ttu-id="7518a-136">Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-136">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![응용 프로그램][4]
6. <span data-ttu-id="7518a-138">Hello 검색 상자에 입력 **ServiceNow**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-138">In hello search box, type **ServiceNow**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. <span data-ttu-id="7518a-140">Hello 결과 창에서 선택 **ServiceNow**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-140">In hello results pane, select **ServiceNow**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7518a-142">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="7518a-142">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7518a-143">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 ServiceNow 또는 ServiceNow Express에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-143">In this section, you configure and test Azure AD single sign-on with ServiceNow or ServiceNow Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7518a-144">Single sign on toowork에 대 한 Azure AD는 tooknow ServiceNow에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-144">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ServiceNow is tooa user in Azure AD.</span></span> <span data-ttu-id="7518a-145">즉, Azure AD 사용자와 ServiceNow의 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-145">In other words, a link relationship between an Azure AD user and hello related user in ServiceNow needs toobe established.</span></span>
<span data-ttu-id="7518a-146">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** ServiceNow에 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-146">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ServiceNow.</span></span> <span data-ttu-id="7518a-147">tooconfigure와 ServiceNow 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-147">tooconfigure and test Azure AD single sign-on with ServiceNow, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7518a-148">**[ServiceNow에 대 한 Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on-for-servicenow)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-148">**[Configuring Azure AD Single Sign-On for ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7518a-149">**[ServiceNow Express에 대 한 Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on-for-servicenow-express)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-149">**[Configuring Azure AD Single Sign-On for ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - tooenable your users toouse this feature.</span></span>
3. <span data-ttu-id="7518a-150">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-150">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="7518a-151">**[ServiceNow 테스트 사용자 만들기](#creating-a-servicenow-test-user)**  -toohave Britta Simon 그녀의 연결 된 Azure AD toohello 표현인 ServiceNow에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-151">**[Creating a ServiceNow test user](#creating-a-servicenow-test-user)** - toohave a counterpart of Britta Simon in ServiceNow that is linked toohello Azure AD representation of her.</span></span>
5. <span data-ttu-id="7518a-152">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-152">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="7518a-153">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="7518a-153">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

> [!NOTE]
> <span data-ttu-id="7518a-154">Tooconfigure ServiceNow를 원하는 경우에 2 단계를 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-154">If you want tooconfigure ServiceNow omit step 2.</span></span> <span data-ttu-id="7518a-155">마찬가지로, tooconfigure ServiceNow Express 하려면 1 단계를 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-155">Likewise, if you want tooconfigure ServiceNow Express omit step 1.</span></span>
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a><span data-ttu-id="7518a-156">ServiceNow에 대한 Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="7518a-156">Configuring Azure AD Single Sign-On for ServiceNow</span></span>
1. <span data-ttu-id="7518a-157">Hello에 Azure AD hello 클래식 포털에서 **ServiceNow** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **Single Sign-on 구성** 대화 상자 .</span><span class="sxs-lookup"><span data-stu-id="7518a-157">In hello Azure AD classic portal, on hello **ServiceNow** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="7518a-158">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-158">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="7518a-159">Hello에 **어떻게 tooServiceNow에 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-159">On hello **How would you like users toosign on tooServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="7518a-160">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-160">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="7518a-161">Hello에 **앱 설정 구성** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-161">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="7518a-162">![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/IC769497.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-162">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="7518a-163">a.</span><span class="sxs-lookup"><span data-stu-id="7518a-163">a.</span></span> <span data-ttu-id="7518a-164">hello에 **ServiceNow 로그온 URL** URL hello 패턴 사용자 toosign에 tooyour ServiceNow 응용 프로그램에서 사용할 텍스트 상자: `https://<instance-name>.service-now.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-164">in hello **ServiceNow Sign On URL** textbox, type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="7518a-165">b.</span><span class="sxs-lookup"><span data-stu-id="7518a-165">b.</span></span> <span data-ttu-id="7518a-166">Hello에 **식별자** URL hello 패턴 사용자 toosign에 tooyour ServiceNow 응용 프로그램에서 사용할 텍스트 상자: `https://<instance-name>.service-now.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-166">In hello **Identifier** textbox,type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="7518a-167">c.</span><span class="sxs-lookup"><span data-stu-id="7518a-167">c.</span></span> <span data-ttu-id="7518a-168">**다음**을 누릅니다</span><span class="sxs-lookup"><span data-stu-id="7518a-168">Click **Next**</span></span>

4. <span data-ttu-id="7518a-169">Azure AD toohave 자동으로 ServiceNow SAML 기반 인증에 대 한 구성, hello에 ServiceNow 인스턴스 이름, 관리자 사용자 이름 및 관리자 암호를 입력 **자동 single sign on 구성** 형태와 클릭  *구성*합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-169">toohave Azure AD automatically configure ServiceNow for SAML-based authentication, enter your ServiceNow instance name, admin username, and admin password in hello **Auto configure single sign-on** form and click *Configure*.</span></span> <span data-ttu-id="7518a-170">제공 된 해당 hello 관리자 권한을 가진 사용자는 hello 해야 **security_admin** 이 toowork에 대 한 ServiceNow에 할당 된 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-170">Note that hello admin username provided must have hello **security_admin** role assigned in ServiceNow for this toowork.</span></span> <span data-ttu-id="7518a-171">그렇지 않으면 toomanually ServiceNow toouse Azure AD SAML id 공급자로 구성, 클릭 **hello 응용 프로그램에 single sign-on에 대 한 수동 구성**, 클릭 **다음** 및 전체 hello 다음 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-171">Otherwise, toomanually configure ServiceNow toouse Azure AD as a SAML identity provider, click **Manually configure hello application for single sign-on**, then click **Next** and complete hello following steps.</span></span>
   
    <span data-ttu-id="7518a-172">![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-172">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="7518a-173">Hello에 **ServiceNow에서 single sign on 구성** 페이지 **다운로드 인증서**, hello 인증서 파일을 컴퓨터에 로컬로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-173">On hello **Configure single sign-on at ServiceNow** page, click **Download certificate**, save hello certificate file locally on your computer.</span></span>
   
    <span data-ttu-id="7518a-174">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-174">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="7518a-175">로그온 tooyour 관리자 권한으로 ServiceNow 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-175">Sign-on tooyour ServiceNow application as an administrator.</span></span>

7. <span data-ttu-id="7518a-176">Hello 활성화 *통합-여러 공급자 Single Sign-on 설치 관리자* 플러그 인에 따라 다음 단계를 hello:</span><span class="sxs-lookup"><span data-stu-id="7518a-176">Activate hello *Integration - Multiple Provider Single Sign-On Installer* plugin by following hello next steps:</span></span>
   
    <span data-ttu-id="7518a-177">a.</span><span class="sxs-lookup"><span data-stu-id="7518a-177">a.</span></span> <span data-ttu-id="7518a-178">Hello 왼쪽에 hello 탐색 창에서 이동 너무**시스템 정의** 섹션 및 클릭 **플러그 인**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-178">In hello navigation pane on hello left side, go too**System Definition** section and then click **Plugins**.</span></span>
   
    <span data-ttu-id="7518a-179">![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "플러그 인 활성화")</span><span class="sxs-lookup"><span data-stu-id="7518a-179">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")</span></span>
   
    <span data-ttu-id="7518a-180">b.</span><span class="sxs-lookup"><span data-stu-id="7518a-180">b.</span></span> <span data-ttu-id="7518a-181">*통합 - 여러 공급자 Single Sign-On 설치 관리자*를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-181">Search for *Integration - Multiple Provider Single Sign-On Installer*.</span></span>
   
    <span data-ttu-id="7518a-182">![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "플러그 인 활성화")</span><span class="sxs-lookup"><span data-stu-id="7518a-182">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")</span></span>
   
    <span data-ttu-id="7518a-183">c.</span><span class="sxs-lookup"><span data-stu-id="7518a-183">c.</span></span> <span data-ttu-id="7518a-184">Hello 플러그 인을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-184">Select hello plugin.</span></span> <span data-ttu-id="7518a-185">마우스 오른쪽을 클릭하고 **활성화/업그레이드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-185">Rigth click and select **Activate/Upgrade**.</span></span>
   
    <span data-ttu-id="7518a-186">d.</span><span class="sxs-lookup"><span data-stu-id="7518a-186">d.</span></span> <span data-ttu-id="7518a-187">Hello 클릭 **Activate** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-187">Click hello **Activate** button.</span></span>

8. <span data-ttu-id="7518a-188">Hello 왼쪽에 hello 탐색 창에서 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-188">In hello navigation pane on hello left side, click **Properties**.</span></span>  
   
    <span data-ttu-id="7518a-189">![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-189">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configure app URL")</span></span>

9. <span data-ttu-id="7518a-190">Hello에 **여러 공급자 SSO 속성** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-190">On hello **Multiple Provider SSO Properties** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="7518a-191">![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-191">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configure app URL")</span></span>
   
    <span data-ttu-id="7518a-192">a.</span><span class="sxs-lookup"><span data-stu-id="7518a-192">a.</span></span> <span data-ttu-id="7518a-193">**여러 공급자 SSO 사용**을 **예**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-193">As **Enable multiple provider SSO**, select **Yes**.</span></span>
   
    <span data-ttu-id="7518a-194">b.</span><span class="sxs-lookup"><span data-stu-id="7518a-194">b.</span></span> <span data-ttu-id="7518a-195">으로 **내용이 디버그 로깅을 사용 hello 여러 공급자 SSO 통합**선택, **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-195">As **Enable debug logging got hello multiple provider SSO integration**, select **Yes**.</span></span>
   
    <span data-ttu-id="7518a-196">c.</span><span class="sxs-lookup"><span data-stu-id="7518a-196">c.</span></span> <span data-ttu-id="7518a-197">**hello 사용자에 대 한 hello 필드는 테이블 중...**  텍스트 상자에 **user_name**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-197">In **hello field on hello user table that...** textbox, type **user_name**.</span></span>
   
    <span data-ttu-id="7518a-198">d.</span><span class="sxs-lookup"><span data-stu-id="7518a-198">d.</span></span> <span data-ttu-id="7518a-199">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-199">Click **Save**.</span></span>

10. <span data-ttu-id="7518a-200">Hello 왼쪽에 hello 탐색 창에서 클릭 **x509 인증서**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-200">In hello navigation pane on hello left side, click **x509 Certificates**.</span></span>
    
     <span data-ttu-id="7518a-201">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-201">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configure single sign-on")</span></span>

11. <span data-ttu-id="7518a-202">Hello에 **X.509 인증서** 대화 상자를 클릭 하 여 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-202">On hello **X.509 Certificates** dialog, click **New**.</span></span>
    
     <span data-ttu-id="7518a-203">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-203">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configure single sign-on")</span></span>

12. <span data-ttu-id="7518a-204">Hello에 **X.509 인증서** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-204">On hello **X.509 Certificates** dialog, perform hello following steps:</span></span>
    
     <span data-ttu-id="7518a-205">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-205">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
     <span data-ttu-id="7518a-206">a.</span><span class="sxs-lookup"><span data-stu-id="7518a-206">a.</span></span> <span data-ttu-id="7518a-207">**새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-207">Click **New**.</span></span>
    
     <span data-ttu-id="7518a-208">b.</span><span class="sxs-lookup"><span data-stu-id="7518a-208">b.</span></span> <span data-ttu-id="7518a-209">Hello에 **이름** 텍스트 상자 구성 이름 입력 합니다 (예:: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="7518a-209">In hello **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
     <span data-ttu-id="7518a-210">c.</span><span class="sxs-lookup"><span data-stu-id="7518a-210">c.</span></span> <span data-ttu-id="7518a-211">**활성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-211">Select **Active**.</span></span>
    
     <span data-ttu-id="7518a-212">d.</span><span class="sxs-lookup"><span data-stu-id="7518a-212">d.</span></span> <span data-ttu-id="7518a-213">**형식**으로 **PEM**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-213">As **Format**, select **PEM**.</span></span>
    
     <span data-ttu-id="7518a-214">e.</span><span class="sxs-lookup"><span data-stu-id="7518a-214">e.</span></span> <span data-ttu-id="7518a-215">**형식**으로 **저장소 인증서 신뢰**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-215">As **Type**, select **Trust Store Cert**.</span></span>
    
     <span data-ttu-id="7518a-216">f.</span><span class="sxs-lookup"><span data-stu-id="7518a-216">f.</span></span> <span data-ttu-id="7518a-217">메모장에 복사 hello 내용을 클립보드의 내용에 Base64 인코딩된 인증서를 열고 toohello 붙여 **PEM Certificate** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-217">Open your Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **PEM Certificate** textbox.</span></span>
    
     <span data-ttu-id="7518a-218">g.</span><span class="sxs-lookup"><span data-stu-id="7518a-218">g.</span></span> <span data-ttu-id="7518a-219">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-219">Click **Update**.</span></span>

13. <span data-ttu-id="7518a-220">Hello 왼쪽에 hello 탐색 창에서 클릭 **Id 공급자**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-220">In hello navigation pane on hello left side, click **Identity Providers**.</span></span>
    
     <span data-ttu-id="7518a-221">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-221">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span></span>

14. <span data-ttu-id="7518a-222">Hello에 **Id 공급자** 대화 상자를 클릭 하 여 **새로**:</span><span class="sxs-lookup"><span data-stu-id="7518a-222">On hello **Identity Providers** dialog, click **New**:</span></span>
    
     <span data-ttu-id="7518a-223">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-223">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configure single sign-on")</span></span>

15. <span data-ttu-id="7518a-224">Hello에 **Id 공급자** 대화 상자를 클릭 하 여 **SAML2 업데이트 1?**:</span><span class="sxs-lookup"><span data-stu-id="7518a-224">On hello **Identity Providers** dialog, click **SAML2 Update1?**:</span></span>
    
     <span data-ttu-id="7518a-225">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-225">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configure single sign-on")</span></span>

16. <span data-ttu-id="7518a-226">Hello SAML2 업데이트 1 속성 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-226">On hello SAML2 Update1 Properties dialog, perform hello following steps:</span></span>
    
     <span data-ttu-id="7518a-227">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-227">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configure single sign-on")</span></span>

    <span data-ttu-id="7518a-228">a.</span><span class="sxs-lookup"><span data-stu-id="7518a-228">a.</span></span> <span data-ttu-id="7518a-229">hello에 **이름** 텍스트 상자 구성 이름 입력 합니다 (예:: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="7518a-229">in hello **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="7518a-230">b.</span><span class="sxs-lookup"><span data-stu-id="7518a-230">b.</span></span> <span data-ttu-id="7518a-231">Hello에 **사용자 필드** 텍스트 상자에 **전자 메일** 또는 **user_name**, 사용 되는 필드에 따라 toouniquely ServiceNow 배포에서 사용자를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-231">In hello **User Field** textbox, type **email** or **user_name**, depending on which field is used toouniquely identify users in your ServiceNow deployment.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="7518a-232">Azure AD 구성 tooemit 어느 hello Azure AD 사용자 ID (사용자 계정 이름) 수 또는 toohello 이동 하 여 hello SAML 토큰의 고유 식별자를 hello으로 전자 메일 주소를 hello **ServiceNow > 특성 > Single Sign On** 의 섹션 Azure 클래식 포털 및 매핑 원하는 hello 필드 toohello hello **nameidentifier** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-232">You can configue Azure AD tooemit either hello Azure AD user ID (user principal name) or hello email address as hello unique identifier in hello SAML token by going toohello **ServiceNow > Attributes > Single Sign-On** section of hello Azure classic portal and mapping hello desired field toohello **nameidentifier** attribute.</span></span> <span data-ttu-id="7518a-233">hello 선택한 특성에 대 한 Azure AD (예: 사용자 계정 이름)에 저장 하는 hello 값에는 입력 한 hello 필드 (예: user_name)에 대 한 ServiceNow에 저장 된 hello 값과 일치 해야 합니다</span><span class="sxs-lookup"><span data-stu-id="7518a-233">hello value stored for hello selected attribute in Azure AD (e.g. user principal name) must match hello value stored in ServiceNow for hello entered field (e.g. user_name)</span></span>

    <span data-ttu-id="7518a-234">c.</span><span class="sxs-lookup"><span data-stu-id="7518a-234">c.</span></span> <span data-ttu-id="7518a-235">Azure AD hello 클래식 포털에서 복사 hello **Id 공급자 ID** 값을 복사한 다음 hello에 붙여 넣을 **Id 공급자 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-235">In hello Azure AD classic portal, copy hello **Identity Provider ID** value, and then paste it into hello **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="7518a-236">d.</span><span class="sxs-lookup"><span data-stu-id="7518a-236">d.</span></span> <span data-ttu-id="7518a-237">Azure AD hello 클래식 포털에서 복사 hello **인증 요청 URL** 값을 복사한 다음 hello에 붙여 넣을 **Id 공급자의 AuthnRequest** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-237">In hello Azure AD classic portal, copy hello **Authentication Request URL** value, and then paste it into hello **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="7518a-238">e.</span><span class="sxs-lookup"><span data-stu-id="7518a-238">e.</span></span> <span data-ttu-id="7518a-239">Azure AD hello 클래식 포털에서 복사 hello **Single Sign-Out 서비스 URL** 값을 복사한 다음 hello에 붙여 넣을 **Id 공급자의 SingleLogoutRequest** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-239">In hello Azure AD classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="7518a-240">f.</span><span class="sxs-lookup"><span data-stu-id="7518a-240">f.</span></span> <span data-ttu-id="7518a-241">Hello에 **ServiceNow 홈 페이지** 텍스트 상자에 ServiceNow 인스턴스 홈 페이지의 hello URL 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-241">In hello **ServiceNow Homepage** textbox, type hello URL of your ServiceNow instance homepage.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7518a-242">hello ServiceNow 인스턴스 홈 페이지는 연결의 프로그램 **ServieNow 테 넌 트 URL** 및 **/navpage.do** (예::`https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="7518a-242">hello ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.:`https://fabrikam.service-now.com/navpage.do`).</span></span>

    <span data-ttu-id="7518a-243">g.</span><span class="sxs-lookup"><span data-stu-id="7518a-243">g.</span></span> <span data-ttu-id="7518a-244">Hello에 **엔터티 ID / 발급자** textbox ServiceNow 테 넌 트의 hello URL 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-244">In hello **Entity ID / Issuer** textbox, type hello URL of your ServiceNow tenant.</span></span>

    <span data-ttu-id="7518a-245">h.</span><span class="sxs-lookup"><span data-stu-id="7518a-245">h.</span></span> <span data-ttu-id="7518a-246">Hello에 **Audience URL** textbox ServiceNow 테 넌 트의 hello URL 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-246">In hello **Audience URL** textbox, type hello URL of your ServiceNow tenant.</span></span> 

    <span data-ttu-id="7518a-247">i.</span><span class="sxs-lookup"><span data-stu-id="7518a-247">i.</span></span> <span data-ttu-id="7518a-248">Hello에 **hello IDP의 SingleLogoutRequest에 대 한 프로토콜 바인딩** 텍스트 상자에 **urn: oasis: 이름: tc: SAML:2.0:bindings:HTTP-리디렉션**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-248">In hello **Protocol Binding for hello IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>

    <span data-ttu-id="7518a-249">j.</span><span class="sxs-lookup"><span data-stu-id="7518a-249">j.</span></span> <span data-ttu-id="7518a-250">Hello NameID 정책 텍스트 상자에에서 입력 **urn: oasis: 이름: tc: SAML:1.1:nameid-형식: 지정 되지 않은**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-250">In hello NameID Policy textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>

    <span data-ttu-id="7518a-251">k.</span><span class="sxs-lookup"><span data-stu-id="7518a-251">k.</span></span> <span data-ttu-id="7518a-252">**AuthnContextClass 만들기**의 선택을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-252">Deselect **Create an AuthnContextClass**.</span></span>

    <span data-ttu-id="7518a-253">l.</span><span class="sxs-lookup"><span data-stu-id="7518a-253">l.</span></span> <span data-ttu-id="7518a-254">Hello에 **AuthnContextClassRef 메서드**, 형식 `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-254">In hello **AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span></span> <span data-ttu-id="7518a-255">클라우드 전용 조직인 경우에만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-255">This is only needed if you are cloud only organization.</span></span> <span data-ttu-id="7518a-256">인증으로 온-프레미스 ADFS 또는 MFA를 사용하는 경우 이 값을 구성하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-256">If you are using on-premises ADFS or MFA for authentication then you should not configure this value.</span></span> 

    <span data-ttu-id="7518a-257">m.</span><span class="sxs-lookup"><span data-stu-id="7518a-257">m.</span></span> <span data-ttu-id="7518a-258">**시계 기울이기** 텍스트 상자에 **60**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-258">In **Clock Skew** textbox, type **60**.</span></span>

    <span data-ttu-id="7518a-259">n.</span><span class="sxs-lookup"><span data-stu-id="7518a-259">n.</span></span> <span data-ttu-id="7518a-260">**Single Sign On 스크립트**로 **MultiSSO_SAML2_Update1**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-260">As **Single Sign On Script**, select **MultiSSO_SAML2_Update1**.</span></span>

    <span data-ttu-id="7518a-261">o.</span><span class="sxs-lookup"><span data-stu-id="7518a-261">o.</span></span> <span data-ttu-id="7518a-262">으로 **x509 인증서**선택, hello 이전 단계에서 만든 hello 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-262">As **x509 Certificate**, select hello certificate you have created in hello previous step.</span></span>

    <span data-ttu-id="7518a-263">p.</span><span class="sxs-lookup"><span data-stu-id="7518a-263">p.</span></span> <span data-ttu-id="7518a-264">**제출**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-264">Click **Submit**.</span></span> 

1. <span data-ttu-id="7518a-265">Azure AD hello 클래식 포털에서 hello single sign on 구성 확인을 선택한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-265">On hello Azure AD classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="7518a-266">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-266">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="7518a-267">Hello에 **Single sign on 확인** 페이지 **완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-267">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="7518a-268">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-268">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a><span data-ttu-id="7518a-269">ServiceNow Express에 대한 Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="7518a-269">Configuring Azure AD Single Sign-On for ServiceNow Express</span></span>
1. <span data-ttu-id="7518a-270">Hello에 Azure AD hello 클래식 포털에서 **ServiceNow** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **Single Sign-on 구성** 대화 상자 .</span><span class="sxs-lookup"><span data-stu-id="7518a-270">In hello Azure AD classic portal, on hello **ServiceNow** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="7518a-271">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-271">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="7518a-272">Hello에 **어떻게 tooServiceNow에 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-272">On hello **How would you like users toosign on tooServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="7518a-273">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-273">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="7518a-274">Hello에 **앱 설정 구성** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-274">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="7518a-275">![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/IC769497.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-275">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="7518a-276">a.</span><span class="sxs-lookup"><span data-stu-id="7518a-276">a.</span></span> <span data-ttu-id="7518a-277">hello에 **ServiceNow 로그온 URL** URL hello 패턴 사용자 toosign에 tooyour ServiceNow 응용 프로그램에서 사용할 텍스트 상자: `https://<instance-name>.service-now.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-277">in hello **ServiceNow Sign On URL** textbox, type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="7518a-278">b.</span><span class="sxs-lookup"><span data-stu-id="7518a-278">b.</span></span> <span data-ttu-id="7518a-279">Hello에 **발급자 URL** URL hello 패턴 사용자 toosign에 tooyour ServiceNow 응용 프로그램에서 사용할 텍스트 상자 `https://<instance-name>.service-now.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-279">In hello **Issuer URL** textbox,type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="7518a-280">c.</span><span class="sxs-lookup"><span data-stu-id="7518a-280">c.</span></span> <span data-ttu-id="7518a-281">**다음**을 누릅니다</span><span class="sxs-lookup"><span data-stu-id="7518a-281">Click **Next**</span></span>

4. <span data-ttu-id="7518a-282">클릭 **hello 응용 프로그램에 single sign-on에 대 한 수동 구성**, 클릭 **다음** 전체 hello 단계를 수행 하 고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-282">Click **Manually configure hello application for single sign-on**, then click **Next** and complete hello following steps.</span></span>
   
    <span data-ttu-id="7518a-283">![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-283">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="7518a-284">Hello에 **ServiceNow에서 single sign on 구성** 페이지 **다운로드 인증서**, hello 인증서 파일을 컴퓨터에 로컬로 저장 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-284">On hello **Configure single sign-on at ServiceNow** page, click **Download certificate**, save hello certificate file locally on your computer, and then click **Next**.</span></span>
   
    <span data-ttu-id="7518a-285">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-285">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="7518a-286">로그온 tooyour 관리자 권한으로 ServiceNow Express 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-286">Sign-on tooyour ServiceNow Express application as an administrator.</span></span>

7. <span data-ttu-id="7518a-287">Hello 왼쪽에 hello 탐색 창에서 클릭 **Single Sign On**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-287">In hello navigation pane on hello left side, click **Single Sign-On**.</span></span>  
   
    <span data-ttu-id="7518a-288">![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-288">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configure app URL")</span></span>

8. <span data-ttu-id="7518a-289">Hello에 **Single Sign On** 대화 상자에서 hello 구성 아이콘 hello 위 오른쪽과 설정 hello 다음 속성을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-289">On hello **Single Sign-On** dialog, click hello configuration icon on hello upper right and set hello following properties:</span></span>
   
    <span data-ttu-id="7518a-290">![앱 URL 구성](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "앱 URL 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-290">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configure app URL")</span></span>
   
    <span data-ttu-id="7518a-291">a.</span><span class="sxs-lookup"><span data-stu-id="7518a-291">a.</span></span> <span data-ttu-id="7518a-292">설정/해제 **여러 공급자 SSO 설정** toohello 오른쪽입니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-292">Toggle **Enable multiple provider SSO** toohello right.</span></span>
   
    <span data-ttu-id="7518a-293">b.</span><span class="sxs-lookup"><span data-stu-id="7518a-293">b.</span></span> <span data-ttu-id="7518a-294">설정/해제 **여러 공급자 SSO 통합 hello에 대 한 로깅을 사용 하도록 설정 디버그** toohello 오른쪽입니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-294">Toggle **Enable debug logging for hello multiple provider SSO integration** toohello right.</span></span>
   
    <span data-ttu-id="7518a-295">c.</span><span class="sxs-lookup"><span data-stu-id="7518a-295">c.</span></span> <span data-ttu-id="7518a-296">**hello 사용자에 대 한 hello 필드는 테이블 중...**  텍스트 상자에 **user_name**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-296">In **hello field on hello user table that...** textbox, type **user_name**.</span></span>
9. <span data-ttu-id="7518a-297">Hello에 **Single Sign On** 대화 상자를 클릭 하 여 **새 인증서 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-297">On hello **Single Sign-On** dialog, click **Add New Certificate**.</span></span>
   
    <span data-ttu-id="7518a-298">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-298">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configure single sign-on")</span></span>
10. <span data-ttu-id="7518a-299">Hello에 **X.509 인증서** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-299">On hello **X.509 Certificates** dialog, perform hello following steps:</span></span>
    
    <span data-ttu-id="7518a-300">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-300">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
    <span data-ttu-id="7518a-301">a.</span><span class="sxs-lookup"><span data-stu-id="7518a-301">a.</span></span> <span data-ttu-id="7518a-302">Hello에 **이름** 텍스트 상자 구성 이름 입력 합니다 (예:: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="7518a-302">In hello **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
    <span data-ttu-id="7518a-303">b.</span><span class="sxs-lookup"><span data-stu-id="7518a-303">b.</span></span> <span data-ttu-id="7518a-304">**활성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-304">Select **Active**.</span></span>
    
    <span data-ttu-id="7518a-305">c.</span><span class="sxs-lookup"><span data-stu-id="7518a-305">c.</span></span> <span data-ttu-id="7518a-306">**형식**으로 **PEM**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-306">As **Format**, select **PEM**.</span></span>
    
    <span data-ttu-id="7518a-307">d.</span><span class="sxs-lookup"><span data-stu-id="7518a-307">d.</span></span> <span data-ttu-id="7518a-308">**형식**으로 **저장소 인증서 신뢰**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-308">As **Type**, select **Trust Store Cert**.</span></span>
    
    <span data-ttu-id="7518a-309">e.</span><span class="sxs-lookup"><span data-stu-id="7518a-309">e.</span></span> <span data-ttu-id="7518a-310">다운로드한 인증서에서 Base64로 인코딩된 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-310">Create a Base64 encoded file from your downloaded certificate.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="7518a-311">자세한 내용은 참조 하십시오. [어떻게 tooconvert 이진은 텍스트 파일에을 인증서](http://youtu.be/PlgrzUZ-Y1o)합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-311">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
    > 
    > 
    
    <span data-ttu-id="7518a-312">f.</span><span class="sxs-lookup"><span data-stu-id="7518a-312">f.</span></span> <span data-ttu-id="7518a-313">메모장에 복사 hello 내용을 클립보드의 내용에 Base64 인코딩된 인증서를 열고 toohello 붙여 **PEM Certificate** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-313">Open your Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **PEM Certificate** textbox.</span></span>
    
    <span data-ttu-id="7518a-314">g.</span><span class="sxs-lookup"><span data-stu-id="7518a-314">g.</span></span> <span data-ttu-id="7518a-315">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-315">Click **Update**.</span></span>
11. <span data-ttu-id="7518a-316">Hello에 **Single Sign On** 대화 상자를 클릭 하 여 **새 IdP 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-316">On hello **Single Sign-On** dialog, click **Add New IdP**.</span></span>
    
    <span data-ttu-id="7518a-317">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-317">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configure single sign-on")</span></span>
12. <span data-ttu-id="7518a-318">Hello에 **새 Id 공급자 추가** 대화 아래 **Id 공급자 구성**, hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-318">On hello **Add New Identity Provider** dialog, under **Configure Identity Provider**, perform hello following steps:</span></span>
    
    <span data-ttu-id="7518a-319">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-319">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configure single sign-on")</span></span>

    <span data-ttu-id="7518a-320">a.</span><span class="sxs-lookup"><span data-stu-id="7518a-320">a.</span></span> <span data-ttu-id="7518a-321">hello에 **이름** 텍스트 상자 구성 이름 입력 합니다 (예:: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="7518a-321">In hello **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="7518a-322">b.</span><span class="sxs-lookup"><span data-stu-id="7518a-322">b.</span></span> <span data-ttu-id="7518a-323">Azure AD hello 클래식 포털에서 복사 hello **Id 공급자 ID** 값을 복사한 다음 hello에 붙여 넣을 **Id 공급자 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-323">In hello Azure AD classic portal, copy hello **Identity Provider ID** value, and then paste it into hello **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="7518a-324">c.</span><span class="sxs-lookup"><span data-stu-id="7518a-324">c.</span></span> <span data-ttu-id="7518a-325">Azure AD hello 클래식 포털에서 복사 hello **인증 요청 URL** 값을 복사한 다음 hello에 붙여 넣을 **Id 공급자의 AuthnRequest** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-325">In hello Azure AD classic portal, copy hello **Authentication Request URL** value, and then paste it into hello **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="7518a-326">d.</span><span class="sxs-lookup"><span data-stu-id="7518a-326">d.</span></span> <span data-ttu-id="7518a-327">Azure AD hello 클래식 포털에서 복사 hello **Single Sign-Out 서비스 URL** 값을 복사한 다음 hello에 붙여 넣을 **Id 공급자의 SingleLogoutRequest** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-327">In hello Azure AD classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="7518a-328">e.</span><span class="sxs-lookup"><span data-stu-id="7518a-328">e.</span></span> <span data-ttu-id="7518a-329">으로 **Id 공급자 인증서**선택, hello 이전 단계에서 만든 hello 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-329">As **Identity Provider Certificate**, select hello certificate you have created in hello previous step.</span></span>


1. <span data-ttu-id="7518a-330">클릭 **고급 설정**, 아래에서 **추가 Id 공급자 속성**, hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-330">Click **Advanced Settings**, and under **Additional Identity Provider Properties**, perform hello following steps:</span></span>
   
    <span data-ttu-id="7518a-331">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-331">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="7518a-332">a.</span><span class="sxs-lookup"><span data-stu-id="7518a-332">a.</span></span> <span data-ttu-id="7518a-333">Hello에 **hello IDP의 SingleLogoutRequest에 대 한 프로토콜 바인딩** 텍스트 상자에 **urn: oasis: 이름: tc: SAML:2.0:bindings:HTTP-리디렉션**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-333">In hello **Protocol Binding for hello IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>
   
    <span data-ttu-id="7518a-334">b.</span><span class="sxs-lookup"><span data-stu-id="7518a-334">b.</span></span> <span data-ttu-id="7518a-335">Hello에 **NameID 정책** 텍스트 상자에 **urn: oasis: 이름: tc: SAML:1.1:nameid-형식: 지정 되지 않은**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-335">In hello **NameID Policy** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>    
   
    <span data-ttu-id="7518a-336">c.</span><span class="sxs-lookup"><span data-stu-id="7518a-336">c.</span></span> <span data-ttu-id="7518a-337">Hello에 **AuthnContextClassRef 메서드**, 형식 **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-337">In hello **AuthnContextClassRef Method**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span></span>
   
    <span data-ttu-id="7518a-338">d.</span><span class="sxs-lookup"><span data-stu-id="7518a-338">d.</span></span> <span data-ttu-id="7518a-339">**AuthnContextClass 만들기**의 선택을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-339">Deselect **Create an AuthnContextClass**.</span></span>

2. <span data-ttu-id="7518a-340">아래 **추가 서비스 공급자 속성**, hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-340">Under **Additional Service Provider Properties**, perform hello following steps:</span></span>
   
    <span data-ttu-id="7518a-341">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-341">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="7518a-342">a.</span><span class="sxs-lookup"><span data-stu-id="7518a-342">a.</span></span> <span data-ttu-id="7518a-343">Hello에 **ServiceNow 홈 페이지** 텍스트 상자에 ServiceNow 인스턴스 홈 페이지의 hello URL 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-343">In hello **ServiceNow Homepage** textbox, type hello URL of your ServiceNow instance homepage.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="7518a-344">hello ServiceNow 인스턴스 홈 페이지는 연결의 프로그램 **ServieNow 테 넌 트 URL** 및 **/navpage.do** (예:: `https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="7518a-344">hello ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.: `https://fabrikam.service-now.com/navpage.do`).</span></span>
    > 
    > 
   
    <span data-ttu-id="7518a-345">b.</span><span class="sxs-lookup"><span data-stu-id="7518a-345">b.</span></span> <span data-ttu-id="7518a-346">Hello에 **엔터티 ID / 발급자** textbox ServiceNow 테 넌 트의 hello URL 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-346">In hello **Entity ID / Issuer** textbox, type hello URL of your ServiceNow tenant.</span></span>
   
    <span data-ttu-id="7518a-347">c.</span><span class="sxs-lookup"><span data-stu-id="7518a-347">c.</span></span> <span data-ttu-id="7518a-348">Hello에 **Audience URI** textbox ServiceNow 테 넌 트의 hello URL 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-348">In hello **Audience URI** textbox, type hello URL of your ServiceNow tenant.</span></span> 
   
    <span data-ttu-id="7518a-349">d.</span><span class="sxs-lookup"><span data-stu-id="7518a-349">d.</span></span> <span data-ttu-id="7518a-350">**시계 기울이기** 텍스트 상자에 **60**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-350">In **Clock Skew** textbox, type **60**.</span></span>
   
    <span data-ttu-id="7518a-351">e.</span><span class="sxs-lookup"><span data-stu-id="7518a-351">e.</span></span> <span data-ttu-id="7518a-352">Hello에 **사용자 필드** 텍스트 상자에 **전자 메일** 또는 **user_name**, 사용 되는 필드에 따라 toouniquely ServiceNow 배포에서 사용자를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-352">In hello **User Field** textbox, type **email** or **user_name**, depending on which field is used toouniquely identify users in your ServiceNow deployment.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="7518a-353">Azure AD 구성 tooemit 어느 hello Azure AD 사용자 ID (사용자 계정 이름) 수 또는 toohello 이동 하 여 hello SAML 토큰의 고유 식별자를 hello으로 전자 메일 주소를 hello **ServiceNow > 특성 > Single Sign On** 의 섹션 Azure 클래식 포털 및 매핑 원하는 hello 필드 toohello hello **nameidentifier** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-353">You can configue Azure AD tooemit either hello Azure AD user ID (user principal name) or hello email address as hello unique identifier in hello SAML token by going toohello **ServiceNow > Attributes > Single Sign-On** section of hello Azure classic portal and mapping hello desired field toohello **nameidentifier** attribute.</span></span> <span data-ttu-id="7518a-354">hello 선택한 특성에 대 한 Azure AD (예: 사용자 계정 이름)에 저장 하는 hello 값에는 입력 한 hello 필드 (예: user_name)에 대 한 ServiceNow에 저장 된 hello 값과 일치 해야 합니다</span><span class="sxs-lookup"><span data-stu-id="7518a-354">hello value stored for hello selected attribute in Azure AD (e.g. user principal name) must match hello value stored in ServiceNow for hello entered field (e.g. user_name)</span></span>
    > 
    > 
   
    <span data-ttu-id="7518a-355">f.</span><span class="sxs-lookup"><span data-stu-id="7518a-355">f.</span></span> <span data-ttu-id="7518a-356">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-356">Click **Save**.</span></span> 

3. <span data-ttu-id="7518a-357">Azure AD hello 클래식 포털에서 hello single sign on 구성 확인을 선택한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-357">On hello Azure AD classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="7518a-358">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-358">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

4. <span data-ttu-id="7518a-359">Hello에 **Single sign on 확인** 페이지 **완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-359">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="7518a-360">![Single Sign-On 구성](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Single Sign-On 구성")</span><span class="sxs-lookup"><span data-stu-id="7518a-360">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="7518a-361">사용자 프로비전 구성</span><span class="sxs-lookup"><span data-stu-id="7518a-361">Configuring user provisioning</span></span>
<span data-ttu-id="7518a-362">이 섹션의 hello 목적은 toooutline 어떻게 tooServiceNow 계정 tooenable Active Directory 사용자의 사용자 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-362">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooServiceNow.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="7518a-363">tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:</span><span class="sxs-lookup"><span data-stu-id="7518a-363">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="7518a-364">Hello에 hello 관리 Azure 클래식 포털에서 **ServiceNow** 응용 프로그램 통합 페이지에서 클릭 **사용자 프로비저닝을 구성할**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-364">In hello Azure Management classic portal, on hello **ServiceNow** application integration page, click **Configure user provisioning**.</span></span> 
   
    <span data-ttu-id="7518a-365">![사용자 프로비전](./media/active-directory-saas-servicenow-tutorial/IC769498.png "사용자 프로비전")</span><span class="sxs-lookup"><span data-stu-id="7518a-365">![User provisioning](./media/active-directory-saas-servicenow-tutorial/IC769498.png "User provisioning")</span></span>

2. <span data-ttu-id="7518a-366">Hello에 **프로그램 ServiceNow 자격 증명 tooenable 자동 사용자 프로비저닝 입력** 페이지 hello 다음 구성 설정을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-366">On hello **Enter your ServiceNow credentials tooenable automatic user provisioning** page, provide hello following configuration settings:</span></span>
   
     <span data-ttu-id="7518a-367">a.</span><span class="sxs-lookup"><span data-stu-id="7518a-367">a.</span></span> <span data-ttu-id="7518a-368">Hello에 **ServiceNow 인스턴스 이름을** 텍스트 형식 hello ServiceNow 인스턴스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-368">In hello **ServiceNow Instance Name** textbox, type hello ServiceNow instance name.</span></span>
   
     <span data-ttu-id="7518a-369">b.</span><span class="sxs-lookup"><span data-stu-id="7518a-369">b.</span></span> <span data-ttu-id="7518a-370">Hello에 **ServiceNow 관리자 사용자 이름** 텍스트 형식 hello 이름 hello ServiceNow 관리자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-370">In hello **ServiceNow Admin User Name** textbox, type hello name of hello ServiceNow admin account.</span></span>
   
     <span data-ttu-id="7518a-371">c.</span><span class="sxs-lookup"><span data-stu-id="7518a-371">c.</span></span> <span data-ttu-id="7518a-372">Hello에 **ServiceNow 관리자 암호** textbox를이 계정에 대 한 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-372">In hello **ServiceNow Admin Password** textbox, type hello password for this account.</span></span>
   
     <span data-ttu-id="7518a-373">d.</span><span class="sxs-lookup"><span data-stu-id="7518a-373">d.</span></span> <span data-ttu-id="7518a-374">클릭 **유효성을 검사** tooverify 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-374">Click **validate** tooverify your configuration.</span></span>
   
     <span data-ttu-id="7518a-375">e.</span><span class="sxs-lookup"><span data-stu-id="7518a-375">e.</span></span> <span data-ttu-id="7518a-376">Hello 클릭 **다음** 단추 tooopen hello **다음 단계** 페이지.</span><span class="sxs-lookup"><span data-stu-id="7518a-376">Click hello **Next** button tooopen hello **Next steps** page.</span></span>
   
     <span data-ttu-id="7518a-377">f.</span><span class="sxs-lookup"><span data-stu-id="7518a-377">f.</span></span> <span data-ttu-id="7518a-378">모든 사용자가 toothis 응용 프로그램 tooprovision 하려는 경우 선택 "**자동으로 hello 디렉터리 toothis 응용 프로그램의 모든 사용자 계정을 프로 비전**"입니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-378">If you want tooprovision all users toothis application, select “**Automatically provision all user accounts in hello directory toothis application**”.</span></span> 
   
    <span data-ttu-id="7518a-379">![다음 단계](./media/active-directory-saas-servicenow-tutorial/IC698804.png "다음 단계")</span><span class="sxs-lookup"><span data-stu-id="7518a-379">![Next Steps](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Next Steps")</span></span>
   
     <span data-ttu-id="7518a-380">g.</span><span class="sxs-lookup"><span data-stu-id="7518a-380">g.</span></span> <span data-ttu-id="7518a-381">Hello에 **다음 단계** 페이지 **완료** toosave 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-381">On hello **Next steps** page, click **Complete** toosave your configuration.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7518a-382">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="7518a-382">Creating an Azure AD test user</span></span>
<span data-ttu-id="7518a-383">이 섹션에서는 Britta Simon 라는 hello 클래식 포털의 테스트 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-383">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][20]

<span data-ttu-id="7518a-385">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="7518a-385">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7518a-386">Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-386">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="7518a-388">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-388">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="7518a-389">toodisplay hello 목록이 hello 바탕 화면에서 hello 메뉴에서 사용자가 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-389">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7518a-391">tooopen hello **사용자 추가** hello 아래쪽에 hello 도구 모음에서 대화 상자에서 클릭 **사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-391">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="7518a-393">Hello에 **이 사용자에 대해 알리기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-393">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="7518a-395">a.</span><span class="sxs-lookup"><span data-stu-id="7518a-395">a.</span></span> <span data-ttu-id="7518a-396">사용자 유형에서 조직의 새 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-396">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="7518a-397">b.</span><span class="sxs-lookup"><span data-stu-id="7518a-397">b.</span></span> <span data-ttu-id="7518a-398">Hello 사용자 이름에서에서 **textbox**, 형식 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-398">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="7518a-399">c.</span><span class="sxs-lookup"><span data-stu-id="7518a-399">c.</span></span> <span data-ttu-id="7518a-400">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-400">Click **Next**.</span></span>

6. <span data-ttu-id="7518a-401">Hello에 **사용자 프로필** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-401">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   <span data-ttu-id="7518a-403">a.</span><span class="sxs-lookup"><span data-stu-id="7518a-403">a.</span></span> <span data-ttu-id="7518a-404">Hello에 **이름** 텍스트 상자에 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-404">In hello **First Name** textbox, type **Britta**.</span></span>  
   
   <span data-ttu-id="7518a-405">b.</span><span class="sxs-lookup"><span data-stu-id="7518a-405">b.</span></span> <span data-ttu-id="7518a-406">Hello에 **성** 텍스트 상자에, **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-406">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
   <span data-ttu-id="7518a-407">c.</span><span class="sxs-lookup"><span data-stu-id="7518a-407">c.</span></span> <span data-ttu-id="7518a-408">Hello에 **표시 이름** 텍스트 상자에 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-408">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="7518a-409">d.</span><span class="sxs-lookup"><span data-stu-id="7518a-409">d.</span></span> <span data-ttu-id="7518a-410">Hello에 **역할** 목록에서 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-410">In hello **Role** list, select **User**.</span></span>
   
   <span data-ttu-id="7518a-411">e.</span><span class="sxs-lookup"><span data-stu-id="7518a-411">e.</span></span> <span data-ttu-id="7518a-412">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-412">Click **Next**.</span></span>

7. <span data-ttu-id="7518a-413">Hello에 **임시 암호 가져오기** 대화 상자 페이지에서 클릭 **만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-413">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="7518a-415">Hello에 **임시 암호 가져오기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-415">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="7518a-417">a.</span><span class="sxs-lookup"><span data-stu-id="7518a-417">a.</span></span> <span data-ttu-id="7518a-418">Hello hello 값 적어 **새 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-418">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="7518a-419">b.</span><span class="sxs-lookup"><span data-stu-id="7518a-419">b.</span></span> <span data-ttu-id="7518a-420">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-420">Click **Complete**.</span></span>   

### <a name="creating-a-servicenow-test-user"></a><span data-ttu-id="7518a-421">ServiceNow 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="7518a-421">Creating a ServiceNow test user</span></span>
<span data-ttu-id="7518a-422">이 섹션에서는 ServiceNow에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-422">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="7518a-423">이 섹션에서는 ServiceNow에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-423">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="7518a-424">ServiceNow 또는 ServiceNow Express에 있는 사용자 계정을 하는 tooadd 방법을 모르는 경우 ServiceNow 지원 팀에 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-424">If you don't know how tooadd a user in your ServiceNow or ServiceNow Express account, contact ServiceNow support team.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7518a-425">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-425">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="7518a-426">이 섹션에서는 액세스 tooServiceNow 그녀의 권한을 부여 하 여 Azure single sign on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-426">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooServiceNow.</span></span>

![사용자 할당][200] 

<span data-ttu-id="7518a-428">**tooassign Britta Simon tooServiceNow hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="7518a-428">**tooassign Britta Simon tooServiceNow, perform hello following steps:**</span></span>

1. <span data-ttu-id="7518a-429">Hello 클래식 포털에서 tooopen hello 응용 프로그램 보기 hello 디렉터리 보기를 클릭 **응용 프로그램** hello 최상위 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-429">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![사용자 할당][201] 

2. <span data-ttu-id="7518a-431">Hello 응용 프로그램 목록에서 선택 **ServiceNow**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-431">In hello applications list, select **ServiceNow**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. <span data-ttu-id="7518a-433">Hello 메뉴에서 hello 위에 표시를 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-433">In hello menu on hello top, click **Users**.</span></span>
   
    ![사용자 할당][203] 

4. <span data-ttu-id="7518a-435">Hello 모든 사용자가 목록에서 선택 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-435">In hello All Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="7518a-436">Hello 아래쪽에 hello 도구 모음에서 클릭 **할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-436">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![사용자 할당][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="7518a-438">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="7518a-438">Testing single sign-on</span></span>
<span data-ttu-id="7518a-439">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-439">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7518a-440">Hello 액세스 패널에서에서 hello ServiceNow 타일을 클릭할 때 자동으로 로그온 tooyour ServiceNow 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7518a-440">When you click hello ServiceNow tile in hello Access Panel, you should get automatically signed-on tooyour ServiceNow application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7518a-441">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="7518a-441">Additional resources</span></span>
* [<span data-ttu-id="7518a-442">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="7518a-442">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7518a-443">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="7518a-443">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
