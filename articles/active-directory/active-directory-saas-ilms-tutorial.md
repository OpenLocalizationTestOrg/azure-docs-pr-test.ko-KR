---
title: "자습서: Azure Active Directory와 iLMS 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 iLMS 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: da0936de23afcd5a4213aa6f699165f9bfa82c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a><span data-ttu-id="85a26-103">자습서: iLMS와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="85a26-103">Tutorial: Azure Active Directory integration with iLMS</span></span>

<span data-ttu-id="85a26-104">이 자습서에 설명 어떻게 toointegrate iLMS Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="85a26-104">In this tutorial, you learn how toointegrate iLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="85a26-105">다음 이점을 hello로 제공 iLMS Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="85a26-105">Integrating iLMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="85a26-106">액세스 tooiLMS을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-106">You can control in Azure AD who has access tooiLMS</span></span>
- <span data-ttu-id="85a26-107">프로그램 사용자 tooautomatically get 로그온 tooiLMS (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-107">You can enable your users tooautomatically get signed-on tooiLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="85a26-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="85a26-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85a26-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="85a26-110">Prerequisites</span></span>

<span data-ttu-id="85a26-111">다음 항목 hello가 필요 tooconfigure iLMS와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-111">tooconfigure Azure AD integration with iLMS, you need hello following items:</span></span>

- <span data-ttu-id="85a26-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="85a26-112">An Azure AD subscription</span></span>
- <span data-ttu-id="85a26-113">iLMS Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="85a26-113">An iLMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="85a26-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="85a26-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="85a26-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="85a26-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="85a26-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="85a26-118">Scenario description</span></span>
<span data-ttu-id="85a26-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="85a26-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="85a26-121">ILMS hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="85a26-121">Adding iLMS from hello gallery</span></span>
2. <span data-ttu-id="85a26-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="85a26-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ilms-from-hello-gallery"></a><span data-ttu-id="85a26-123">ILMS hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="85a26-123">Adding iLMS from hello gallery</span></span>
<span data-ttu-id="85a26-124">tooconfigure hello와의 통합 iLMS Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 tooadd iLMS 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-124">tooconfigure hello integration of iLMS into Azure AD, you need tooadd iLMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="85a26-125">**hello 갤러리에서 tooadd iLMS hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="85a26-125">**tooadd iLMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="85a26-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="85a26-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="85a26-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="85a26-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-131">tooadd new application, click **New application** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="85a26-133">Hello 검색 상자에 입력 **iLMS**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-133">In hello search box, type **iLMS**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. <span data-ttu-id="85a26-135">Hello 결과 패널에서 선택 **iLMS**, 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-135">In hello results panel, select **iLMS**, then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="85a26-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="85a26-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="85a26-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 iLMS에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-138">In this section, you configure and test Azure AD single sign-on with iLMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="85a26-139">Single sign on toowork에 대 한 Azure AD는 tooknow iLMS에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in iLMS is tooa user in Azure AD.</span></span> <span data-ttu-id="85a26-140">즉, Azure AD 사용자 및 iLMS에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-140">In other words, a link relationship between an Azure AD user and hello related user in iLMS needs toobe established.</span></span>

<span data-ttu-id="85a26-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** iLMS에 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in iLMS.</span></span>

<span data-ttu-id="85a26-142">tooconfigure 및 iLMS 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-142">tooconfigure and test Azure AD single sign-on with iLMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="85a26-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="85a26-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="85a26-145">**[ILMS 테스트 사용자 만들기](#creating-an-ilms-test-user)**  -toohave 그녀의 연결 된 Azure AD toohello 표현인 iLMS에 Britta Simon 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-145">**[Creating an iLMS test user](#creating-an-ilms-test-user)** - toohave a counterpart of Britta Simon in iLMS that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="85a26-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="85a26-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="85a26-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="85a26-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="85a26-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="85a26-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 iLMS 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your iLMS application.</span></span>

<span data-ttu-id="85a26-150">**tooconfigure Azure AD single sign on, iLMS와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="85a26-150">**tooconfigure Azure AD single sign-on with iLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="85a26-151">Hello hello에 Azure 포털에서에서 **iLMS** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-151">In hello Azure portal, on hello **iLMS** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="85a26-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. <span data-ttu-id="85a26-155">Hello에 **iLMS 도메인 및 Url** 섹션를 hello tooconfigure hello 응용 프로그램에 필요한 경우 다음 단계를 수행 **IDP** 시작 모드:</span><span class="sxs-lookup"><span data-stu-id="85a26-155">On hello **iLMS Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    <span data-ttu-id="85a26-157">a.</span><span class="sxs-lookup"><span data-stu-id="85a26-157">a.</span></span> <span data-ttu-id="85a26-158">Hello에 **식별자** 텍스트 붙여넣기 hello **식별자** 값에서 복사 **서비스 공급자** iLMS 관리자 포털에서 SAML 설정 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-158">In hello **Identifier** textbox, paste hello **Identifier** value you copy from **Service Provider** section of SAML settings in iLMS admin portal.</span></span>

    <span data-ttu-id="85a26-159">b.</span><span class="sxs-lookup"><span data-stu-id="85a26-159">b.</span></span> <span data-ttu-id="85a26-160">Hello에 **회신 URL** 텍스트 붙여넣기 hello **끝점 (URL)** 값에서 복사 **서비스 공급자** hello 다음을 있는 iLMS 관리자 포털에서 SAML 설정 섹션 패턴`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="85a26-160">In hello **Reply URL** textbox, paste hello **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal having hello following pattern `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>

    >[!Note]
    ><span data-ttu-id="85a26-161">여기서 '123456'은 식별자 값의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-161">This '123456' is an example value of identifier.</span></span>

4. <span data-ttu-id="85a26-162">확인 **고급 URL 설정 표시**tooconfigure hello 응용 프로그램에 필요한 경우, **SP** 시작 모드:</span><span class="sxs-lookup"><span data-stu-id="85a26-162">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    <span data-ttu-id="85a26-164">Hello에 **로그온 URL** 텍스트 붙여넣기 hello **끝점 (URL)** 값에서 복사 **서비스 공급자** 으로 iLMS 관리자 포털에서 SAML 설정 섹션`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="85a26-164">In hello **Sign-on URL** textbox, paste hello **Endpoint (URL)** value you copy from **Service Provider** section of SAML settings in iLMS admin portal as `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`</span></span>     

5. <span data-ttu-id="85a26-165">tooenable JIT 프로 비전, iLMS 응용 프로그램에는 hello SAML 어설션이 특정 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-165">tooenable JIT provisioning, iLMS application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="85a26-166">이 응용 프로그램에 대 한 클레임을 따라 hello를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-166">Configure hello following claims for this application.</span></span> <span data-ttu-id="85a26-167">Hello에서 이러한 특성의 hello 값을 관리할 수 있습니다 **사용자 특성** 응용 프로그램 통합 페이지에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="85a26-167">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="85a26-168">다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-168">hello following screenshot shows an example for this.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/4.png)
    
    <span data-ttu-id="85a26-170">만들 **부서, 지역** 및 **나누기** 특성과 iLMS에서 이러한 특성의 hello 이름을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-170">Create **Department, Region** and **Division** attributes and add hello name of these attributes in iLMS.</span></span> <span data-ttu-id="85a26-171">위에 표시된 모든 특성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-171">All these attributes shown above are required.</span></span>    

    > [!NOTE] 
    > <span data-ttu-id="85a26-172">Tooenable 있는 **Un-recognized 사용자 계정 만들기** iLMS toomap에서 이러한 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-172">You have tooenable **Create Un-recognized User Account** in iLMS toomap these attributes.</span></span> <span data-ttu-id="85a26-173">Hello 지침에 따라 [여기](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget hello 특성 구성에 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-173">Follow hello instructions [here](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget an idea on hello attributes configuration.</span></span>

6. <span data-ttu-id="85a26-174">Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 위의 hello 이미지에 나와 있는 것 처럼 SAML 토큰 특성을 구성 하 고 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-174">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="85a26-175">특성 이름</span><span class="sxs-lookup"><span data-stu-id="85a26-175">Attribute Name</span></span> | <span data-ttu-id="85a26-176">특성 값</span><span class="sxs-lookup"><span data-stu-id="85a26-176">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="85a26-177">division</span><span class="sxs-lookup"><span data-stu-id="85a26-177">division</span></span> | <span data-ttu-id="85a26-178">user.department</span><span class="sxs-lookup"><span data-stu-id="85a26-178">user.department</span></span> |
    | <span data-ttu-id="85a26-179">region</span><span class="sxs-lookup"><span data-stu-id="85a26-179">region</span></span> | <span data-ttu-id="85a26-180">user.state</span><span class="sxs-lookup"><span data-stu-id="85a26-180">user.state</span></span> |
    | <span data-ttu-id="85a26-181">department</span><span class="sxs-lookup"><span data-stu-id="85a26-181">department</span></span> | <span data-ttu-id="85a26-182">user.jobtitle</span><span class="sxs-lookup"><span data-stu-id="85a26-182">user.jobtitle</span></span> |

    <span data-ttu-id="85a26-183">a.</span><span class="sxs-lookup"><span data-stu-id="85a26-183">a.</span></span> <span data-ttu-id="85a26-184">클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="85a26-184">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    <span data-ttu-id="85a26-187">b.</span><span class="sxs-lookup"><span data-stu-id="85a26-187">b.</span></span> <span data-ttu-id="85a26-188">Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-188">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="85a26-189">c.</span><span class="sxs-lookup"><span data-stu-id="85a26-189">c.</span></span> <span data-ttu-id="85a26-190">Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-190">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="85a26-191">d.</span><span class="sxs-lookup"><span data-stu-id="85a26-191">d.</span></span> <span data-ttu-id="85a26-192">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-192">Click **Ok**</span></span>

7. <span data-ttu-id="85a26-193">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello XML 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-193">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. <span data-ttu-id="85a26-195">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-195">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="85a26-197">다른 웹 브라우저 창에서 tooyour에 로그인 **iLMS 관리자 포털** 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-197">In a different web browser window, log in tooyour **iLMS admin portal** as an administrator.</span></span>

10. <span data-ttu-id="85a26-198">클릭 **SSO:SAML** 아래 **설정** tooopen SAML 설정 탭 하 고 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-198">Click **SSO:SAML** under **Settings** tab tooopen SAML settings and perform hello following steps:</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/1.png) 

    <span data-ttu-id="85a26-200">a.</span><span class="sxs-lookup"><span data-stu-id="85a26-200">a.</span></span> <span data-ttu-id="85a26-201">Hello 확장 **서비스 공급자** 섹션 및 복사 hello **식별자** 및 **끝점 (URL)** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-201">Expand hello **Service Provider** section and copy hello **Identifier** and **Endpoint (URL)** value.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/2.png) 

    <span data-ttu-id="85a26-203">b.</span><span class="sxs-lookup"><span data-stu-id="85a26-203">b.</span></span> <span data-ttu-id="85a26-204">**Identity Provider(ID 공급자)** 섹션에서 **Import Metadata(메타데이터 가져오기)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-204">Under **Identity Provider** section, click **Import Metadata**.</span></span>
    
    <span data-ttu-id="85a26-205">c.</span><span class="sxs-lookup"><span data-stu-id="85a26-205">c.</span></span> <span data-ttu-id="85a26-206">선택 hello **메타 데이터** 에서 Azure 포털에서 다운로드 한 파일 **SAML 서명 인증서** 섹션.</span><span class="sxs-lookup"><span data-stu-id="85a26-206">Select hello **Metadata** file downloaded from Azure Portal from **SAML Signing Certificate** section.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    <span data-ttu-id="85a26-208">d.</span><span class="sxs-lookup"><span data-stu-id="85a26-208">d.</span></span> <span data-ttu-id="85a26-209">JIT tooenable 하려는 경우 계정 프로 비전 toocreate iLMS 취소에 대 한-사용자가 인식 아래 단계를 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="85a26-209">If you want tooenable JIT provisioning toocreate iLMS accounts for un-recognize users, follow below steps:</span></span>
        
       - <span data-ttu-id="85a26-210">**Create Un-recognized User Account(인식할 수 없는 사용자 계정 만들기)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-210">Check **Create Un-recognized User Account**.</span></span>
       
       ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  <span data-ttu-id="85a26-212">Hello 특성을 iLMS의 hello 특성으로 Azure AD에 매핑하십시오.</span><span class="sxs-lookup"><span data-stu-id="85a26-212">Map hello attributes in Azure AD with hello attributes in iLMS.</span></span> <span data-ttu-id="85a26-213">Hello 특성 열의 hello 특성 이름이 나 hello 기본값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-213">In hello attribute column, specify hello attributes name or hello default value.</span></span>

    <span data-ttu-id="85a26-214">e.</span><span class="sxs-lookup"><span data-stu-id="85a26-214">e.</span></span> <span data-ttu-id="85a26-215">너무 이동**비즈니스 규칙** 탭 하 고 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-215">Go too**Business Rules** tab and perform hello following steps:</span></span> 
        
       ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/5.png)

       - <span data-ttu-id="85a26-217">확인 **Un-recognized 영역 만들기, 사업부 및 부서가** toocreate 영역, 사업부와의 Single sign-on hello 시 아직 존재 하지 않는 부서입니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-217">Check **Create Un-recognized Regions, Divisions and Departments** toocreate Regions, Divisions, and Departments that do not already exist at hello time of Single Sign-on.</span></span>
        
       - <span data-ttu-id="85a26-218">확인 **업데이트 사용자 프로필 중 로그인** toospecify hello 사용자의 프로필 각 Single sign-on으로 업데이트 되는지 여부를 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-218">Check **Update User Profile During Sign-in** toospecify whether hello user’s profile is updated with each Single Sign-on.</span></span> 
        
       - <span data-ttu-id="85a26-219">경우 hello **"업데이트 빈 값에 대 한 비 필수 필드에 사용자 프로필"** 선택적 프로필 필드는 로그인 시 비어 있는 발생 하면 hello 사용자 iLMS 프로필 toocontain 빈 값이 해당 필드에 대 한, 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-219">If hello **“Update Blank Values for Non Mandatory Fields in User Profile”** option is checked, optional profile fields that are blank upon sign in will also cause hello user’s iLMS profile toocontain blank values for those fields.</span></span>
        
       - <span data-ttu-id="85a26-220">확인 **오류 알림 전자 메일 보내기** tooreceive hello 오류 알림 전자 메일을 원하는 hello 사용자의 hello 전자 메일을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-220">Check **Send Error Notification Email** and enter hello email of hello user where you want tooreceive hello error notification email.</span></span>

11. <span data-ttu-id="85a26-221">클릭 **저장** toosave hello 설정 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-221">Click **Save** button toosave hello settings.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="85a26-223">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="85a26-223">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="85a26-224">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="85a26-224">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="85a26-225">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="85a26-225">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
    
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="85a26-226">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="85a26-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="85a26-227">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-227">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="85a26-229">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="85a26-229">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="85a26-230">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-230">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="85a26-232">너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-232">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="85a26-234">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="85a26-234">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="85a26-236">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-236">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="85a26-238">a.</span><span class="sxs-lookup"><span data-stu-id="85a26-238">a.</span></span> <span data-ttu-id="85a26-239">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-239">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="85a26-240">b.</span><span class="sxs-lookup"><span data-stu-id="85a26-240">b.</span></span> <span data-ttu-id="85a26-241">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-241">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="85a26-242">c.</span><span class="sxs-lookup"><span data-stu-id="85a26-242">c.</span></span> <span data-ttu-id="85a26-243">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-243">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="85a26-244">d.</span><span class="sxs-lookup"><span data-stu-id="85a26-244">d.</span></span> <span data-ttu-id="85a26-245">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-245">Click **Create**.</span></span>
 
### <a name="creating-an-ilms-test-user"></a><span data-ttu-id="85a26-246">iLMS 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="85a26-246">Creating an iLMS test user</span></span>

<span data-ttu-id="85a26-247">응용 프로그램 적시 사용자 프로 비전 및 인증 사용자가 hello 응용 프로그램에서 자동으로 생성 한 후 마법사를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-247">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="85a26-248">hello를 클릭 한 경우 작동 JIT **Un-recognized 사용자 계정 만들기** iLMS 관리자 포털에서 SAML 구성 설정 하는 동안 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-248">JIT will work, if you have clicked hello **Create Un-recognized User Account** checkbox during SAML configuration setting at iLMS admin portal.</span></span>

<span data-ttu-id="85a26-249">Toocreate 된 사용자를 수동으로 필요한 경우 아래 단계에 따라 다음:</span><span class="sxs-lookup"><span data-stu-id="85a26-249">If you need toocreate an user manually, then follow below steps :</span></span>

1. <span data-ttu-id="85a26-250">관리자 권한으로 tooyour iLMS 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-250">Log in tooyour iLMS company site as an administrator.</span></span>

2. <span data-ttu-id="85a26-251">클릭 **"사용자 등록"** 아래 **사용자** tooopen 탭 **사용자 등록** 페이지.</span><span class="sxs-lookup"><span data-stu-id="85a26-251">Click **“Register User”** under **Users** tab tooopen **Register User** page.</span></span> 
   
   ![직원 추가](./media/active-directory-saas-ilms-tutorial/3.png)

3. <span data-ttu-id="85a26-253">Hello에 **"사용자 등록"** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-253">On hello **“Register User”** page, perform hello following steps.</span></span>

    ![직원 추가](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    <span data-ttu-id="85a26-255">a.</span><span class="sxs-lookup"><span data-stu-id="85a26-255">a.</span></span> <span data-ttu-id="85a26-256">Hello에 **이름** 형식 hello 이름 Britta 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-256">In hello **First Name** textbox, type hello first name Britta.</span></span>
   
    <span data-ttu-id="85a26-257">b.</span><span class="sxs-lookup"><span data-stu-id="85a26-257">b.</span></span> <span data-ttu-id="85a26-258">Hello에 **성** 텍스트 형식 hello 성 Simon 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-258">In hello **Last Name** textbox, type hello last name Simon.</span></span>

    <span data-ttu-id="85a26-259">c.</span><span class="sxs-lookup"><span data-stu-id="85a26-259">c.</span></span> <span data-ttu-id="85a26-260">Hello에 **전자 메일 ID** textbox Britta Simon 계정의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-260">In hello **Email ID** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="85a26-261">d.</span><span class="sxs-lookup"><span data-stu-id="85a26-261">d.</span></span> <span data-ttu-id="85a26-262">Hello에 **지역** 드롭다운에서 선택 hello 값 영역에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-262">In hello **Region** dropdown, select hello value for region.</span></span>

    <span data-ttu-id="85a26-263">e.</span><span class="sxs-lookup"><span data-stu-id="85a26-263">e.</span></span> <span data-ttu-id="85a26-264">Hello에 **나누기** 드롭다운에서 선택 hello 부문에 대해서는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-264">In hello **Division** dropdown, select hello value for division.</span></span>

    <span data-ttu-id="85a26-265">f.</span><span class="sxs-lookup"><span data-stu-id="85a26-265">f.</span></span> <span data-ttu-id="85a26-266">Hello에 **부서** 드롭다운에서 부서에 대 한 선택 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-266">In hello **Department** dropdown, select hello value for department.</span></span>

    <span data-ttu-id="85a26-267">g.</span><span class="sxs-lookup"><span data-stu-id="85a26-267">g.</span></span> <span data-ttu-id="85a26-268">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-268">Click **Save**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="85a26-269">선택 하 여 등록 메일 toouser를 보낼 수 있습니다 **등록 메일 보내기** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-269">You can send registration mail toouser by selecting **Send Registration Mail** checkbox.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="85a26-270">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-270">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="85a26-271">이 섹션에서는 액세스 tooiLMS 그녀의 권한을 부여 하 여 Azure single sign on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-271">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooiLMS.</span></span>

![사용자 할당][200] 

<span data-ttu-id="85a26-273">**tooassign Britta Simon tooiLMS hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="85a26-273">**tooassign Britta Simon tooiLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="85a26-274">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-274">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="85a26-276">Hello 응용 프로그램 목록에서 선택 **iLMS**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-276">In hello applications list, select **iLMS**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. <span data-ttu-id="85a26-278">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-278">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="85a26-280">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-280">Click **Add** button.</span></span> <span data-ttu-id="85a26-281">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-281">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="85a26-283">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-283">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="85a26-284">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-284">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="85a26-285">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-285">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="85a26-286">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="85a26-286">Testing single sign-on</span></span>

<span data-ttu-id="85a26-287">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-287">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="85a26-288">Hello iLMS hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour iLMS 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85a26-288">When you click hello iLMS tile in hello Access Panel, you should get automatically signed-on tooyour iLMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="85a26-289">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="85a26-289">Additional resources</span></span>

* [<span data-ttu-id="85a26-290">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="85a26-290">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="85a26-291">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="85a26-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

