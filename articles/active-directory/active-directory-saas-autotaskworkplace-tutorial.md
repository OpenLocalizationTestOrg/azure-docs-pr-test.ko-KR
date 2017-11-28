---
title: "자습서: Autotask Workplace와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Autotask 회사 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a9a7ff71-c389-4169-aafd-d7a505244797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 7f820f24e8e9493fa2e1c075f2ef61d7eaa84f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-autotask-workplace"></a><span data-ttu-id="43322-103">자습서: Autotask Workplace와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="43322-103">Tutorial: Azure Active Directory integration with Autotask Workplace</span></span>

<span data-ttu-id="43322-104">이 자습서에 설명 어떻게 toointegrate Autotask 작업 공간을 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="43322-104">In this tutorial, you learn how toointegrate Autotask Workplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="43322-105">다음 이점을 hello로 제공 Autotask 회사 Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="43322-105">Integrating Autotask Workplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="43322-106">Azure ad 액세스 tooAutotask 작업 공간을 가진 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43322-106">You can control in Azure AD who has access tooAutotask Workplace</span></span>
- <span data-ttu-id="43322-107">프로그램 사용자 tooautomatically get 로그온 tooAutotask (Single Sign-on)는 회사의 Azure AD 계정으로 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43322-107">You can enable your users tooautomatically get signed-on tooAutotask Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="43322-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43322-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="43322-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43322-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="43322-110">Prerequisites</span></span>

<span data-ttu-id="43322-111">다음 항목 hello가 필요 tooconfigure Autotask 회사와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-111">tooconfigure Azure AD integration with Autotask Workplace, you need hello following items:</span></span>

- <span data-ttu-id="43322-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="43322-112">An Azure AD subscription</span></span>
- <span data-ttu-id="43322-113">Autotask Workplace Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="43322-113">An Autotask Workplace single-sign on enabled subscription</span></span>
- <span data-ttu-id="43322-114">Workplace에서 관리자 또는 최고 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-114">You must be an administrator or super administrator in Workplace.</span></span>
- <span data-ttu-id="43322-115">Hello Azure AD에서에서 관리자 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-115">You must have an administrator account in hello Azure AD.</span></span>
- <span data-ttu-id="43322-116">이 기능을 활용 하는 hello 사용자 hello Azure AD 작업 공간 내에서 계정이 있어야 하 고 모두에 대 한 자신의 전자 메일 주소가 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-116">hello users that will utilize this feature must have accounts within Workplace and hello Azure AD, and their email addresses for both must match.</span></span>

> [!NOTE]
> <span data-ttu-id="43322-117">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-117">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="43322-118">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="43322-119">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="43322-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="43322-120">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43322-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="43322-121">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="43322-121">Scenario description</span></span>
<span data-ttu-id="43322-122">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="43322-123">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43322-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="43322-124">Hello 갤러리에서 Autotask 작업 공간을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-124">Adding Autotask Workplace from hello gallery</span></span>
2. <span data-ttu-id="43322-125">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="43322-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-autotask-workplace-from-hello-gallery"></a><span data-ttu-id="43322-126">Hello 갤러리에서 Autotask 작업 공간을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-126">Adding Autotask Workplace from hello gallery</span></span>
<span data-ttu-id="43322-127">tooconfigure hello와의 통합 Autotask 회사 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 작업 공간 Autotask tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-127">tooconfigure hello integration of Autotask Workplace into Azure AD, you need tooadd Autotask Workplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="43322-128">**hello 갤러리에서 작업 공간 Autotask tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="43322-128">**tooadd Autotask Workplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="43322-129">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="43322-129">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="43322-131">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-131">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="43322-132">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-132">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="43322-134">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="43322-134">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="43322-136">Hello 검색 상자에 입력 **Autotask 작업 공간**선택, **Autotask 작업 공간** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="43322-136">In hello search box, type **Autotask Workplace**, select  **Autotask Workplace**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Hello에 Autotask 작업 결과 목록](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="43322-138">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="43322-138">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="43322-139">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Autotask Workplace에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-139">In this section, you configure and test Azure AD single sign-on with Autotask Workplace based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="43322-140">Single sign on toowork에 대 한 Azure AD는 tooknow Autotask 직장에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Autotask Workplace is tooa user in Azure AD.</span></span> <span data-ttu-id="43322-141">즉, Azure AD 사용자 및 Autotask 직장에서 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-141">In other words, a link relationship between an Azure AD user and hello related user in Autotask Workplace needs toobe established.</span></span>

<span data-ttu-id="43322-142">Autotask 직장에서의 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="43322-142">In Autotask Workplace, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="43322-143">tooconfigure 및 Autotask 작업 공간을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-143">tooconfigure and test Azure AD single sign-on with Autotask Workplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="43322-144">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="43322-144">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="43322-145">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-145">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="43322-146">**[작업 공간 Autotask 테스트 사용자 만들기](#create-an-autotask-workplace-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Autotask 직장에서 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="43322-146">**[Create an Autotask Workplace test user](#create-an-autotask-workplace-test-user)** - toohave a counterpart of Britta Simon in Autotask Workplace that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="43322-147">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="43322-147">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="43322-148">**[Single Sign-on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="43322-148">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="43322-149">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="43322-149">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="43322-150">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Autotask 회사 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Autotask Workplace application.</span></span>

<span data-ttu-id="43322-151">**tooconfigure Azure AD single sign on Autotask 작업 공간으로 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="43322-151">**tooconfigure Azure AD single sign-on with Autotask Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="43322-152">Hello hello에 Azure 포털에서에서 **Autotask 작업 공간** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-152">In hello Azure portal, on hello **Autotask Workplace** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="43322-154">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="43322-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_samlbase.png)

3. <span data-ttu-id="43322-156">Tooconfigure hello 응용 프로그램에 필요한 경우 **IDP** 시작 모드를 hello hello에서 다음 단계를 수행 **Autotask 회사 도메인 및 Url** 섹션:</span><span class="sxs-lookup"><span data-stu-id="43322-156">If you wish tooconfigure hello application in **IDP** initiated mode, perform hello following steps on hello **Autotask Workplace Domain and URLs** section:</span></span>

    ![IDP에 대한 Autotask Workplace 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url.png)

    <span data-ttu-id="43322-158">a.</span><span class="sxs-lookup"><span data-stu-id="43322-158">a.</span></span> <span data-ttu-id="43322-159">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="43322-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span></span>

    <span data-ttu-id="43322-160">b.</span><span class="sxs-lookup"><span data-stu-id="43322-160">b.</span></span> <span data-ttu-id="43322-161">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="43322-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span></span>

4. <span data-ttu-id="43322-162">Tooconfigure hello 응용 프로그램에 필요한 경우 **SP** 시작 된 모드에서는 검사 **고급 URL 설정 표시** hello 다음 단계를 수행:</span><span class="sxs-lookup"><span data-stu-id="43322-162">If you wish tooconfigure hello application in **SP** initiated mode, check **Show advanced URL settings** and perform hello following steps:</span></span>

    ![SP에 대한 Autotask Workplace 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url1.png)

    <span data-ttu-id="43322-164">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.awp.autotask.net/loginsso`</span><span class="sxs-lookup"><span data-stu-id="43322-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/loginsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="43322-165">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="43322-165">These values are not real.</span></span> <span data-ttu-id="43322-166">이러한 항목을 업데이트 식별자, 회신 URL 및 로그온 URL 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="43322-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="43322-167">연락처 [Autotask 작업 공간 클라이언트 지원 팀](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="43322-167">Contact [Autotask Workplace Client support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget these values.</span></span> 

5. <span data-ttu-id="43322-168">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_certificate.png) 

6. <span data-ttu-id="43322-170">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-170">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="43322-172">다른 웹 브라우저 창에서 tooWorkplace 온라인 사용 하 여 로그인 관리자 자격 증명을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-172">In a different web browser window, Log in tooWorkplace Online using hello administrator credentials.</span></span>

    >[!Note]
    ><span data-ttu-id="43322-173">Hello IdP를 구성할 때 지정 된 toobe 하위 도메인에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-173">When configuring hello IdP, a subdomain will need toobe specified.</span></span> <span data-ttu-id="43322-174">tooconfirm hello 올바른에서는 하위 도메인 로그인 tooWorkplace 온라인입니다.</span><span class="sxs-lookup"><span data-stu-id="43322-174">tooconfirm hello correct subdomain, login tooWorkplace Online.</span></span> <span data-ttu-id="43322-175">로그인 한 hello URL에 참고 toohello 하위 도메인을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-175">Once logged in, make note toohello subdomain in hello URL.</span></span>
    ><span data-ttu-id="43322-176">hello 하위 도메인 hello "https://"와 ".awp.autotask.net/" 사이의 hello 부분 이며, eu, ca, 또는 au 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-176">hello subdomain is hello part between hello “https://“ and “.awp.autotask.net/“ and should be us, eu, ca, or au.</span></span>

8. <span data-ttu-id="43322-177">너무 이동**구성** > **Single Sign On** hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-177">Go too**Configuration** > **Single Sign-On** and perform hello following steps:</span></span>

    ![Autotask Single Sign-On 구성](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig1.png)
 
    <span data-ttu-id="43322-179">a.</span><span class="sxs-lookup"><span data-stu-id="43322-179">a.</span></span> <span data-ttu-id="43322-180">선택 hello **XML 메타 데이터 파일** 옵션을 선택한 다음 hello 업로드 **메타 데이터 XML** Azure 포털에서 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-180">Select hello **XML Metadata File** option, and then upload hello **Metadata XML** downloaded from Azure portal.</span></span>

    <span data-ttu-id="43322-181">b.</span><span class="sxs-lookup"><span data-stu-id="43322-181">b.</span></span> <span data-ttu-id="43322-182">**SSO 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-182">Click **Enable SSO**.</span></span>
    
    ![Autotask Single Sign-On 승인 구성](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig2.png)

    <span data-ttu-id="43322-184">c.</span><span class="sxs-lookup"><span data-stu-id="43322-184">c.</span></span> <span data-ttu-id="43322-185">선택 hello **을 확인 합니다.이 정보가 올바른지 그리고이 IdP 신뢰** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-185">Select hello **I confirm this information is correct and I trust this IdP** check box.</span></span>

    <span data-ttu-id="43322-186">d.</span><span class="sxs-lookup"><span data-stu-id="43322-186">d.</span></span> <span data-ttu-id="43322-187">**승인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-187">Click **Approve**.</span></span>
     
>[!Note]
><span data-ttu-id="43322-188">구성 Autotask 작업 공간 지원, 필요한 경우를 참조 하세요 [이 페이지](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget 회사 계정이 도움말을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-188">If you require assistance with configuring Autotask Workplace, please see [this page](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget assistance with your Workplace account.</span></span>

> [!TIP]
> <span data-ttu-id="43322-189">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="43322-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="43322-190">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="43322-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="43322-191">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="43322-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="43322-192">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="43322-192">Create an Azure AD test user</span></span>

<span data-ttu-id="43322-193">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="43322-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="43322-195">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="43322-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="43322-196">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="43322-196">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="43322-198">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-198">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="43322-200">tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="43322-200">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello 추가 단추](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="43322-202">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-202">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello 사용자 대화 상자](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="43322-204">a.</span><span class="sxs-lookup"><span data-stu-id="43322-204">a.</span></span> <span data-ttu-id="43322-205">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-205">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="43322-206">b.</span><span class="sxs-lookup"><span data-stu-id="43322-206">b.</span></span> <span data-ttu-id="43322-207">Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-207">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="43322-208">c.</span><span class="sxs-lookup"><span data-stu-id="43322-208">c.</span></span> <span data-ttu-id="43322-209">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="43322-209">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="43322-210">d.</span><span class="sxs-lookup"><span data-stu-id="43322-210">d.</span></span> <span data-ttu-id="43322-211">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-211">Click **Create**.</span></span>

### <a name="create-an-autotask-workplace-test-user"></a><span data-ttu-id="43322-212">Autotask Workplace 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="43322-212">Create an Autotask Workplace test user</span></span>

<span data-ttu-id="43322-213">이 섹션에서는 Autotask에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43322-213">In this section, you create a user called Britta Simon in Autotask.</span></span> <span data-ttu-id="43322-214">와 협력 하세요 [Autotask 작업 공간 지원 팀](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) hello Autotask 작업 공간 플랫폼의에서 tooadd hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="43322-214">Please work with [Autotask Workplace support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooadd hello users in hello Autotask Workplace platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="43322-215">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="43322-216">이 섹션에서는 액세스 tooAutotask 작업 공간을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAutotask Workplace.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="43322-218">**tooassign Britta Simon tooAutotask 직장에서 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="43322-218">**tooassign Britta Simon tooAutotask Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="43322-219">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="43322-221">Hello 응용 프로그램 목록에서 선택 **Autotask 작업 공간**합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-221">In hello applications list, select **Autotask Workplace**.</span></span>

    ![hello hello 응용 프로그램 목록에서 Autotask 작업 공간 연결](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_app.png) 

3. <span data-ttu-id="43322-223">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="43322-225">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-225">Click **Add** button.</span></span> <span data-ttu-id="43322-226">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="43322-228">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43322-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="43322-229">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="43322-230">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="43322-231">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="43322-231">Test single sign-on</span></span>

<span data-ttu-id="43322-232">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43322-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="43322-233">Hello Autotask 작업 공간 hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour Autotask 회사 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-233">When you click hello Autotask Workplace tile in hello Access Panel, you should get automatically signed-on tooyour Autotask Workplace application.</span></span>
<span data-ttu-id="43322-234">액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="43322-234">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="43322-235">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="43322-235">Additional resources</span></span>

* [<span data-ttu-id="43322-236">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="43322-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="43322-237">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="43322-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_203.png

