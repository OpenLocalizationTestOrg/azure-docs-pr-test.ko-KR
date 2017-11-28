---
title: "자습서: Deputy와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 그 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5665c3ac-5689-4201-80fe-fcc677d4430d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 42f65b758682ce2513b6bb38ef40a19f955c88c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a><span data-ttu-id="d85a0-103">자습서: Deputy와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="d85a0-103">Tutorial: Azure Active Directory integration with Deputy</span></span>

<span data-ttu-id="d85a0-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 그 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-104">In this tutorial, you learn how toointegrate Deputy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d85a0-105">그 Azure AD와 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-105">Integrating Deputy with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d85a0-106">액세스 tooDeputy을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-106">You can control in Azure AD who has access tooDeputy</span></span>
- <span data-ttu-id="d85a0-107">프로그램 사용자 tooautomatically get 로그온 tooDeputy (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-107">You can enable your users tooautomatically get signed-on tooDeputy (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d85a0-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d85a0-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d85a0-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d85a0-110">Prerequisites</span></span>

<span data-ttu-id="d85a0-111">그와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-111">tooconfigure Azure AD integration with Deputy, you need hello following items:</span></span>

- <span data-ttu-id="d85a0-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="d85a0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d85a0-113">Deputy Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="d85a0-113">A Deputy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d85a0-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d85a0-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d85a0-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="d85a0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d85a0-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d85a0-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="d85a0-118">Scenario description</span></span>
<span data-ttu-id="d85a0-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d85a0-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d85a0-121">그는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="d85a0-121">Adding Deputy from hello gallery</span></span>
2. <span data-ttu-id="d85a0-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d85a0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-deputy-from-hello-gallery"></a><span data-ttu-id="d85a0-123">그는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="d85a0-123">Adding Deputy from hello gallery</span></span>
<span data-ttu-id="d85a0-124">tooconfigure hello와의 통합 작전 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 그 tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-124">tooconfigure hello integration of Deputy into Azure AD, you need tooadd Deputy from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d85a0-125">**hello 갤러리에서 그 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d85a0-125">**tooadd Deputy from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d85a0-126">Hello에 ** [Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d85a0-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d85a0-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="d85a0-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="d85a0-133">Hello 검색 상자에 입력 **작전**합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-133">In hello search box, type **Deputy**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_search.png)

5. <span data-ttu-id="d85a0-135">Hello 결과 패널에서 선택 **작전**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-135">In hello results panel, select **Deputy**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d85a0-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d85a0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d85a0-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Deputy에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-138">In this section, you configure and test Azure AD single sign-on with Deputy based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d85a0-139">Single sign on toowork에 대 한 Azure AD는 tooknow 그에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Deputy is tooa user in Azure AD.</span></span> <span data-ttu-id="d85a0-140">즉, Azure AD 사용자와 그에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-140">In other words, a link relationship between an Azure AD user and hello related user in Deputy needs toobe established.</span></span>

<span data-ttu-id="d85a0-141">Hello hello 값을 할당, 그에 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-141">In Deputy, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d85a0-142">tooconfigure 및 작전을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-142">tooconfigure and test Azure AD single sign-on with Deputy, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d85a0-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on) ** -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d85a0-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user) ** -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d85a0-145">**[그 테스트 사용자 만들기](#creating-a-deputy-test-user) ** -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 그에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-145">**[Creating a Deputy test user](#creating-a-deputy-test-user)** - toohave a counterpart of Britta Simon in Deputy that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d85a0-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d85a0-147">**[Single Sign-on 테스트](#testing-single-sign-on) ** -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="d85a0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d85a0-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="d85a0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d85a0-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 그 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Deputy application.</span></span>

<span data-ttu-id="d85a0-150">**Azure AD tooconfigure single sign on, 그와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d85a0-150">**tooconfigure Azure AD single sign-on with Deputy, perform hello following steps:**</span></span>

1. <span data-ttu-id="d85a0-151">Hello hello에 Azure 포털에서에서 **작전** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-151">In hello Azure portal, on hello **Deputy** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="d85a0-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_samlbase.png)

3. <span data-ttu-id="d85a0-155">Hello에 **그 도메인 및 Url** tooconfigure hello 응용 프로그램에 필요한 경우 섹션 **IDP** 시작 모드:</span><span class="sxs-lookup"><span data-stu-id="d85a0-155">On hello **Deputy Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url1.png)

    <span data-ttu-id="d85a0-157">a.</span><span class="sxs-lookup"><span data-stu-id="d85a0-157">a.</span></span> <span data-ttu-id="d85a0-158">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:</span><span class="sxs-lookup"><span data-stu-id="d85a0-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    |  |
    | ----|
    | `https://<subdomain>.<region>.au.deputy.com` |
    | `https://<subdomain>.<region>.ent-au.deputy.com` |
    | `https://<subdomain>.<region>.na.deputy.com`|
    | `https://<subdomain>.<region>.ent-na.deputy.com`|
    | `https://<subdomain>.<region>.eu.deputy.com` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com` |
    | `https://<subdomain>.<region>.as.deputy.com` |
    | `https://<subdomain>.<region>.ent-as.deputy.com` |
    | `https://<subdomain>.<region>.la.deputy.com` |
    | `https://<subdomain>.<region>.ent-la.deputy.com` |
    | `https://<subdomain>.<region>.af.deputy.com` |
    | `https://<subdomain>.<region>.ent-af.deputy.com` |
    | `https://<subdomain>.<region>.an.deputy.com` |
    | `https://<subdomain>.<region>.ent-an.deputy.com` |
    | `https://<subdomain>.<region>.deputy.com` |

    <span data-ttu-id="d85a0-159">b.</span><span class="sxs-lookup"><span data-stu-id="d85a0-159">b.</span></span> <span data-ttu-id="d85a0-160">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:</span><span class="sxs-lookup"><span data-stu-id="d85a0-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |----|
    | `https://<subdomain>.<region>.au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.deputy.com/exec/devapp/samlacs.` |

4. <span data-ttu-id="d85a0-161">**고급 URL 설정 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="d85a0-162">Tooconfigure hello 응용 프로그램에 필요한 경우 **SP** 시작 모드:</span><span class="sxs-lookup"><span data-stu-id="d85a0-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url2.png)

    <span data-ttu-id="d85a0-164">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<your-subdomain>.<region>.deputy.com`</span><span class="sxs-lookup"><span data-stu-id="d85a0-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<your-subdomain>.<region>.deputy.com`</span></span>
    
    >[!NOTE]
    > <span data-ttu-id="d85a0-165">Deputy 지역 접미사는 선택 사항이거나 au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an 중 하나를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-165">Deputy region suffix is optional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d85a0-166">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-166">These values are not real.</span></span> <span data-ttu-id="d85a0-167">이러한 항목을 업데이트 식별자, 회신 URL 및 로그온 URL 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-167">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="d85a0-168">연락처 [작전 지원 팀](https://www.deputy.com/call-centers-customer-support-scheduling-software) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-168">Contact [Deputy support team](https://www.deputy.com/call-centers-customer-support-scheduling-software) tooget these values.</span></span> 

5. <span data-ttu-id="d85a0-169">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-169">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_certificate.png) 

6. <span data-ttu-id="d85a0-171">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-171">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-deputy-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="d85a0-173">Hello에 **그 구성** 섹션에서 클릭 **구성 작전** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="d85a0-173">On hello **Deputy Configuration** section, click **Configure Deputy** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d85a0-174">복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="d85a0-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_configure.png) 

8. <span data-ttu-id="d85a0-176">Url toohello 이동:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config)합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-176">Navigate toohello following URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span></span> <span data-ttu-id="d85a0-177">너무 이동**보안 설정** 클릭 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-177">Go too**Security Settings** and click **Edit**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_004.png)

9. <span data-ttu-id="d85a0-179">이 **보안 설정** 페이지에서 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-179">On this **Security Settings** page, perform below steps.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_005.png)
    
    <span data-ttu-id="d85a0-181">a.</span><span class="sxs-lookup"><span data-stu-id="d85a0-181">a.</span></span> <span data-ttu-id="d85a0-182">**소셜 로그인**을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-182">Enable **Social Login**.</span></span>
   
    <span data-ttu-id="d85a0-183">b.</span><span class="sxs-lookup"><span data-stu-id="d85a0-183">b.</span></span> <span data-ttu-id="d85a0-184">메모장에서 콘텐츠를 클립보드에 복사 hello Azure 포털에서 다운로드 한 Base64 인코딩 인증서를 열고 toohello 붙여 **OpenSSL 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-184">Open your Base64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **OpenSSL Certificate** textbox.</span></span>
   
    <span data-ttu-id="d85a0-185">c.</span><span class="sxs-lookup"><span data-stu-id="d85a0-185">c.</span></span> <span data-ttu-id="d85a0-186">Hello SAML SSO URL 텍스트 상자에 입력`https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span><span class="sxs-lookup"><span data-stu-id="d85a0-186">In hello SAML SSO URL textbox, type `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span></span>
    
    <span data-ttu-id="d85a0-187">d.</span><span class="sxs-lookup"><span data-stu-id="d85a0-187">d.</span></span> <span data-ttu-id="d85a0-188">Hello SAML SSO URL 텍스트 상자에 대체 `<your subdomain>` 하위 도메인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-188">In hello SAML SSO URL textbox, replace `<your subdomain>` with your subdomain.</span></span>
   
    <span data-ttu-id="d85a0-189">e.</span><span class="sxs-lookup"><span data-stu-id="d85a0-189">e.</span></span> <span data-ttu-id="d85a0-190">Hello SAML SSO URL 텍스트 상자에 대체 `<saml sso url>` hello로 **SAML Single Sign-on 서비스 URL** hello Azure 포털에서에서 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-190">In hello SAML SSO URL textbox, replace `<saml sso url>` with hello **SAML Single Sign-On Service URL** you have copied from hello Azure portal.</span></span>
   
    <span data-ttu-id="d85a0-191">f.</span><span class="sxs-lookup"><span data-stu-id="d85a0-191">f.</span></span> <span data-ttu-id="d85a0-192">**설정 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-192">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="d85a0-193">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="d85a0-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d85a0-194">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서 ** 구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="d85a0-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d85a0-195">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d85a0-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d85a0-196">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d85a0-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="d85a0-197">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="d85a0-199">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d85a0-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d85a0-200">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-deputy-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d85a0-202">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-deputy-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d85a0-204">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-deputy-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d85a0-206">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-deputy-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d85a0-208">a.</span><span class="sxs-lookup"><span data-stu-id="d85a0-208">a.</span></span> <span data-ttu-id="d85a0-209">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d85a0-210">b.</span><span class="sxs-lookup"><span data-stu-id="d85a0-210">b.</span></span> <span data-ttu-id="d85a0-211">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d85a0-212">c.</span><span class="sxs-lookup"><span data-stu-id="d85a0-212">c.</span></span> <span data-ttu-id="d85a0-213">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d85a0-214">d.</span><span class="sxs-lookup"><span data-stu-id="d85a0-214">d.</span></span> <span data-ttu-id="d85a0-215">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-215">Click **Create**.</span></span>
 
### <a name="creating-a-deputy-test-user"></a><span data-ttu-id="d85a0-216">Deputy 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d85a0-216">Creating a Deputy test user</span></span>

<span data-ttu-id="d85a0-217">tooenable Azure AD 사용자가 toolog tooDeputy에서 이러한 해야에 프로 비전 작전 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-217">tooenable Azure AD users toolog in tooDeputy, they must be provisioned into Deputy.</span></span> <span data-ttu-id="d85a0-218">Deputy의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-218">In case of Deputy, provisioning is a manual task.</span></span>

#### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="d85a0-219">tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-219">tooprovision a user account, perform hello following steps:</span></span>
1. <span data-ttu-id="d85a0-220">관리자 권한으로 tooyour 작전 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-220">Log in tooyour Deputy company site as an administrator.</span></span>

2. <span data-ttu-id="d85a0-221">Hello 위쪽 탐색 창에서 클릭 **사람**합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-221">On hello top navigation pane, click **People**.</span></span>
   
   <span data-ttu-id="d85a0-222">![사람](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "사람")</span><span class="sxs-lookup"><span data-stu-id="d85a0-222">![People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "People")</span></span>

3. <span data-ttu-id="d85a0-223">Hello 클릭 **사람 추가** 단추를 클릭 하 고 **한 사람이 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-223">Click hello **Add People** button and click **Add a single person**.</span></span>
   
   <span data-ttu-id="d85a0-224">![피플 추가](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "피플 추가")</span><span class="sxs-lookup"><span data-stu-id="d85a0-224">![Add People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Add People")</span></span>

4. <span data-ttu-id="d85a0-225">Hello 다음 단계를 수행 하 고 클릭 **저장 및 초대 가능**합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-225">Perform hello following steps and click **Save & Invite**.</span></span>
   
   <span data-ttu-id="d85a0-226">![새 사용자](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "새 사용자")</span><span class="sxs-lookup"><span data-stu-id="d85a0-226">![New User](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "New User")</span></span>

   <span data-ttu-id="d85a0-227">a.</span><span class="sxs-lookup"><span data-stu-id="d85a0-227">a.</span></span> <span data-ttu-id="d85a0-228">Hello에 **이름** 같은 hello 사용자의 형식 이름 텍스트 상자 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-228">In hello **Name** textbox, type name of hello user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="d85a0-229">b.</span><span class="sxs-lookup"><span data-stu-id="d85a0-229">b.</span></span> <span data-ttu-id="d85a0-230">Hello에 **전자 메일** textbox tooprovision를 원하는 Azure AD 계정의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-230">In hello **Email** textbox, type hello email address of an Azure AD account you want tooprovision.</span></span>
   
   <span data-ttu-id="d85a0-231">c.</span><span class="sxs-lookup"><span data-stu-id="d85a0-231">c.</span></span> <span data-ttu-id="d85a0-232">Hello에 **에서 작업** 형식 hello 비즈니스 이름 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-232">In hello **Work at** textbox, type hello business name.</span></span>
   
   <span data-ttu-id="d85a0-233">d.</span><span class="sxs-lookup"><span data-stu-id="d85a0-233">d.</span></span> <span data-ttu-id="d85a0-234">**저장 및 초대** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-234">Click **Save & Invite** button.</span></span>

5. <span data-ttu-id="d85a0-235">hello AAD 계정 보유자는 전자 메일을 수신 하을 따라 활성화 링크 tooconfirm 자신의 계정의 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-235">hello AAD account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span> <span data-ttu-id="d85a0-236">다른 그 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 Api에서 제공 작전 tooprovision AAD 사용자 계정을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-236">You can use any other Deputy user account creation tools or APIs provided by Deputy tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d85a0-237">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d85a0-238">이 섹션에서는 tooDeputy 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDeputy.</span></span>

![사용자 할당][200] 

<span data-ttu-id="d85a0-240">**tooassign Britta Simon tooDeputy hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d85a0-240">**tooassign Britta Simon tooDeputy, perform hello following steps:**</span></span>

1. <span data-ttu-id="d85a0-241">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="d85a0-243">Hello 응용 프로그램 목록에서 선택 **작전**합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-243">In hello applications list, select **Deputy**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_app.png) 

3. <span data-ttu-id="d85a0-245">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="d85a0-247">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-247">Click **Add** button.</span></span> <span data-ttu-id="d85a0-248">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="d85a0-250">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d85a0-251">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d85a0-252">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d85a0-253">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="d85a0-253">Testing single sign-on</span></span>

<span data-ttu-id="d85a0-254">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD SSO 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-254">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="d85a0-255">Hello 작전 hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour 그 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85a0-255">When you click hello Deputy tile in hello Access Panel, you should get automatically signed-on tooyour Deputy application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d85a0-256">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d85a0-256">Additional resources</span></span>

* [<span data-ttu-id="d85a0-257">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="d85a0-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d85a0-258">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d85a0-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_203.png

