---
title: "자습서: ServiceChannel과 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 ServiceChannel 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c3546eab-96b5-489b-a309-b895eb428053
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/3/2017
ms.author: jeedes
ms.openlocfilehash: 956371a1e99dcba4137c271ecfe8a62b9ec64a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a><span data-ttu-id="21a52-103">자습서: ServiceChannel과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="21a52-103">Tutorial: Azure Active Directory integration with ServiceChannel</span></span>

<span data-ttu-id="21a52-104">이 자습서에 설명 어떻게 toointegrate ServiceChannel Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="21a52-104">In this tutorial, you learn how toointegrate ServiceChannel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="21a52-105">ServiceChannel Azure AD와 통합 hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-105">Integrating ServiceChannel with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="21a52-106">액세스 tooServiceChannel을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-106">You can control in Azure AD who has access tooServiceChannel</span></span>
- <span data-ttu-id="21a52-107">프로그램 사용자 tooautomatically get 로그온 tooServiceChannel (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-107">You can enable your users tooautomatically get signed-on tooServiceChannel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="21a52-108">하나의 중앙 위치-hello Azure 관리 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="21a52-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21a52-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="21a52-110">Prerequisites</span></span>

<span data-ttu-id="21a52-111">ServiceChannel와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-111">tooconfigure Azure AD integration with ServiceChannel, you need hello following items:</span></span>

- <span data-ttu-id="21a52-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="21a52-112">An Azure AD subscription</span></span>
- <span data-ttu-id="21a52-113">ServiceChannel Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="21a52-113">A ServiceChannel single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="21a52-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="21a52-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="21a52-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="21a52-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="21a52-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="21a52-118">Scenario description</span></span>
<span data-ttu-id="21a52-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="21a52-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="21a52-121">ServiceChannel은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="21a52-121">Adding ServiceChannel from hello gallery</span></span>
2. <span data-ttu-id="21a52-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="21a52-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-servicechannel-from-hello-gallery"></a><span data-ttu-id="21a52-123">ServiceChannel은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="21a52-123">Adding ServiceChannel from hello gallery</span></span>
<span data-ttu-id="21a52-124">tooconfigure hello와의 통합 ServiceChannel Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 ServiceChannel tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-124">tooconfigure hello integration of ServiceChannel into Azure AD, you need tooadd ServiceChannel from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="21a52-125">**ServiceChannel hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="21a52-125">**tooadd ServiceChannel from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="21a52-126">Hello에  **[Azure 관리 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="21a52-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="21a52-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="21a52-131">클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="21a52-133">Hello 검색 상자에 입력 **ServiceChannel**합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-133">In hello search box, type **ServiceChannel**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_000.png)

5. <span data-ttu-id="21a52-135">Hello 결과 패널에서 선택 **ServiceChannel**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-135">In hello results panel, select **ServiceChannel**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="21a52-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="21a52-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="21a52-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 ServiceChannel에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-138">In this section, you configure and test Azure AD single sign-on with ServiceChannel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="21a52-139">Single sign on toowork에 대 한 Azure AD는 tooknow ServiceChannel에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ServiceChannel is tooa user in Azure AD.</span></span> <span data-ttu-id="21a52-140">즉, Azure AD 사용자 및 ServiceChannel에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-140">In other words, a link relationship between an Azure AD user and hello related user in ServiceChannel needs toobe established.</span></span>

<span data-ttu-id="21a52-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** ServiceChannel에 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ServiceChannel.</span></span>

<span data-ttu-id="21a52-142">tooconfigure 및 ServiceChannel 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-142">tooconfigure and test Azure AD single sign-on with ServiceChannel, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="21a52-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="21a52-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="21a52-145">**[ServiceChannel 테스트 사용자 만들기](#creating-a-servicechannel-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-145">**[Creating a ServiceChannel test user](#creating-a-servicechannel-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="21a52-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="21a52-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="21a52-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="21a52-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="21a52-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="21a52-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 관리 포털에서 설정 및 ServiceChannel 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your ServiceChannel application.</span></span>

<span data-ttu-id="21a52-150">**tooconfigure Azure AD single sign on, ServiceChannel와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="21a52-150">**tooconfigure Azure AD single sign-on with ServiceChannel, perform hello following steps:**</span></span>

1. <span data-ttu-id="21a52-151">Hello에 hello Azure 관리 포털에서 **ServiceChannel** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-151">In hello Azure Management portal, on hello **ServiceChannel** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="21a52-153">Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_01.png)

3. <span data-ttu-id="21a52-155">Hello에 **ServiceChannel 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-155">On hello **ServiceChannel Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_urls.png)

    <span data-ttu-id="21a52-157">a.</span><span class="sxs-lookup"><span data-stu-id="21a52-157">a.</span></span> <span data-ttu-id="21a52-158">Hello에 **식별자** 형식 hello 값으로 텍스트 상자:`http://adfs.<domain>.com/adfs/service/trust`</span><span class="sxs-lookup"><span data-stu-id="21a52-158">In hello **Identifier** textbox, type hello value as: `http://adfs.<domain>.com/adfs/service/trust`</span></span>

    <span data-ttu-id="21a52-159">b.</span><span class="sxs-lookup"><span data-stu-id="21a52-159">b.</span></span> <span data-ttu-id="21a52-160">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<customer domain>.servicechannel.com/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="21a52-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<customer domain>.servicechannel.com/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="21a52-161">이러한 없는지 hello 실제 값 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="21a52-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="21a52-162">Tooupdate hello 실제 식별자와 회신 URL 사용 하 여 이러한 값 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="21a52-163">여기 있습니다 toouse hello의 고유 값을 hello 식별자의에서 문자열을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="21a52-164">연락처 [ServiceChannel 지원 팀](https://servicechannel.zendesk.com/hc/en-us) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-164">Contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us) tooget these values.</span></span>

4. <span data-ttu-id="21a52-165">ServiceChannel 응용 프로그램의 구성을 수행 해야 하면 tooadd 사용자 지정 특성 매핑을 tooyour SAML 토큰 특성을 특정 형식에서 hello SAML 어설션이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-165">Your ServiceChannel application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="21a52-166">다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-166">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="21a52-167">**(사용자 식별자) NameIdentifier** 는 필수 클레임만 hello hello 기본값은 **user.userprincipalname** ServiceChannel와 매핑된이 toobe이 필요 하지만 **user.mail**합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-167">**NameIdentifier(User Identifier)** is hello only mandatory claim and hello default value is **user.userprincipalname** but ServiceChannel expects this toobe mapped with **user.mail**.</span></span> <span data-ttu-id="21a52-168">Tooenable Just In Time 사용자 프로 비전 하려는 경우 다음 아래와 같이 클레임 hello를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-168">If you are planning tooenable Just In Time user provisioning, then you should add hello following claims as shown below.</span></span> <span data-ttu-id="21a52-169">**역할** 클레임 필요한 너무 매핑된 toobe**user.assignedroles** hello 사용자의 hello 역할을 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-169">**Role** claim needs toobe mapped too**user.assignedroles** which contains hello role of hello user.</span></span>  

    <span data-ttu-id="21a52-170">클레임에 대한 자세한 지침은 [여기](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example)에서 ServiceChannel 가이드를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-170">You can refer ServiceChannel guide [here](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) for more guidance on claims.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > <span data-ttu-id="21a52-172">클릭 하십시오 [여기](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) tooknow 어떻게 tooconfigure **역할** Azure AD에서</span><span class="sxs-lookup"><span data-stu-id="21a52-172">Please click [here](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) tooknow how tooconfigure **Role** in Azure AD</span></span>

5. <span data-ttu-id="21a52-173">**사용자 특성** 섹션에서 클릭 **보기 및 다른 모든 사용자 특성 편집** hello 특성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span>

    | <span data-ttu-id="21a52-174">특성 이름</span><span class="sxs-lookup"><span data-stu-id="21a52-174">Attribute Name</span></span> | <span data-ttu-id="21a52-175">특성 값</span><span class="sxs-lookup"><span data-stu-id="21a52-175">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="21a52-176">역할</span><span class="sxs-lookup"><span data-stu-id="21a52-176">Role</span></span>| <span data-ttu-id="21a52-177">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="21a52-177">user.assignedroles</span></span> |

    <span data-ttu-id="21a52-178">a.</span><span class="sxs-lookup"><span data-stu-id="21a52-178">a.</span></span> <span data-ttu-id="21a52-179">클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="21a52-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    <span data-ttu-id="21a52-182">b.</span><span class="sxs-lookup"><span data-stu-id="21a52-182">b.</span></span> <span data-ttu-id="21a52-183">Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="21a52-184">c.</span><span class="sxs-lookup"><span data-stu-id="21a52-184">c.</span></span> <span data-ttu-id="21a52-185">Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="21a52-186">d.</span><span class="sxs-lookup"><span data-stu-id="21a52-186">d.</span></span> <span data-ttu-id="21a52-187">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-187">Click **Ok**</span></span>
    
6. <span data-ttu-id="21a52-188">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-188">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_05.png) 

7. <span data-ttu-id="21a52-190">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-190">Click **Save**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-servicechannel-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="21a52-192">Hello에 **ServiceChannel 구성** 섹션에서 클릭 **구성 ServiceChannel** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="21a52-192">On hello **ServiceChannel Configuration** section, click **Configure ServiceChannel** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="21a52-193">Hello 참고 **SAML Enitity ID** hello에서 **빠른 참조** 섹션.</span><span class="sxs-lookup"><span data-stu-id="21a52-193">Please note hello **SAML Enitity ID** from hello **Quick Reference** section.</span></span>

9. <span data-ttu-id="21a52-194">tooconfigure single sign on에서 **ServiceChannel** toosend hello 다운로드 해야 쪽에서는 **인증서 (Base64)** 및 **SAML 엔터티 ID** 너무[ ServiceChannel 지원 팀](https://servicechannel.zendesk.com/hc/en-us)합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-194">tooconfigure single sign-on on **ServiceChannel** side, you need toosend hello downloaded **certificate (Base64)** and **SAML Entity ID** too[ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us).</span></span> <span data-ttu-id="21a52-195">순서 toohave hello SAML SSO 연결 양쪽 모두에 제대로 설정에서 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-195">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="21a52-196">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="21a52-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="21a52-197">이 섹션의 hello 목표 toocreate Britta Simon 라는 hello Azure 관리 포털에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-197">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="21a52-199">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="21a52-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="21a52-200">Hello에 **Azure 관리 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-200">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="21a52-202">너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-202">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="21a52-204">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="21a52-204">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="21a52-206">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="21a52-208">a.</span><span class="sxs-lookup"><span data-stu-id="21a52-208">a.</span></span> <span data-ttu-id="21a52-209">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="21a52-210">b.</span><span class="sxs-lookup"><span data-stu-id="21a52-210">b.</span></span> <span data-ttu-id="21a52-211">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="21a52-212">c.</span><span class="sxs-lookup"><span data-stu-id="21a52-212">c.</span></span> <span data-ttu-id="21a52-213">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="21a52-214">d.</span><span class="sxs-lookup"><span data-stu-id="21a52-214">d.</span></span> <span data-ttu-id="21a52-215">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-215">Click **Create**.</span></span> 

### <a name="creating-a-servicechannel-test-user"></a><span data-ttu-id="21a52-216">ServiceChannel 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="21a52-216">Creating a ServiceChannel test user</span></span>

<span data-ttu-id="21a52-217">응용 프로그램 적시 사용자 프로 비전 및 인증 사용자 hello 응용 프로그램에서에 자동으로 생성 한 후 마법사를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-217">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="21a52-218">전체 사용자 프로비전은 [ServiceChannel 지원 팀](https://servicechannel.zendesk.com/hc/en-us)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="21a52-218">For full user provisioning, please contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us)</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="21a52-219">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="21a52-220">이 섹션에서는 액세스 tooServiceChannel 그녀의 권한을 부여 하 여 Azure single sign on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooServiceChannel.</span></span>

![사용자 할당][200] 

<span data-ttu-id="21a52-222">**tooassign Britta Simon tooServiceChannel hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="21a52-222">**tooassign Britta Simon tooServiceChannel, perform hello following steps:**</span></span>

1. <span data-ttu-id="21a52-223">Hello Azure 관리 포털에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-223">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="21a52-225">Hello 응용 프로그램 목록에서 선택 **ServiceChannel**합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-225">In hello applications list, select **ServiceChannel**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_app01.png) 

3. <span data-ttu-id="21a52-227">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="21a52-229">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-229">Click **Add** button.</span></span> <span data-ttu-id="21a52-230">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="21a52-232">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="21a52-233">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="21a52-234">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="21a52-235">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="21a52-235">Testing single sign-on</span></span>

<span data-ttu-id="21a52-236">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="21a52-237">Hello 액세스 패널에서에서 hello ServiceChannel 타일을 클릭할 때 자동으로 로그온 tooyour ServiceChannel 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21a52-237">When you click hello ServiceChannel tile in hello Access Panel, you should get automatically signed-on tooyour ServiceChannel application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="21a52-238">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="21a52-238">Additional resources</span></span>

* [<span data-ttu-id="21a52-239">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="21a52-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="21a52-240">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="21a52-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_203.png