---
title: "자습서: ICIMS와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 ICIMS 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 72dbd649-e4b1-4d72-ad76-636d84922596
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 3fa970f008e64e84b0a1280f691f0181851b757c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icims"></a><span data-ttu-id="7b42b-103">자습서: ICIMS와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="7b42b-103">Tutorial: Azure Active Directory integration with ICIMS</span></span>

<span data-ttu-id="7b42b-104">이 자습서에 설명 어떻게 toointegrate ICIMS Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7b42b-104">In this tutorial, you learn how toointegrate ICIMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7b42b-105">다음 이점을 hello로 제공 ICIMS Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="7b42b-105">Integrating ICIMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7b42b-106">액세스 tooICIMS을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-106">You can control in Azure AD who has access tooICIMS</span></span>
- <span data-ttu-id="7b42b-107">프로그램 사용자 tooautomatically get 로그온 tooICIMS (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-107">You can enable your users tooautomatically get signed-on tooICIMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7b42b-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7b42b-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b42b-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7b42b-110">Prerequisites</span></span>

<span data-ttu-id="7b42b-111">다음 항목 hello가 필요 tooconfigure ICIMS와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-111">tooconfigure Azure AD integration with ICIMS, you need hello following items:</span></span>

- <span data-ttu-id="7b42b-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="7b42b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7b42b-113">ICIMS Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="7b42b-113">An ICIMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7b42b-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7b42b-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7b42b-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="7b42b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7b42b-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7b42b-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="7b42b-118">Scenario description</span></span>
<span data-ttu-id="7b42b-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7b42b-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7b42b-121">ICIMS는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="7b42b-121">Adding ICIMS from hello gallery</span></span>
2. <span data-ttu-id="7b42b-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="7b42b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-icims-from-hello-gallery"></a><span data-ttu-id="7b42b-123">ICIMS는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="7b42b-123">Adding ICIMS from hello gallery</span></span>
<span data-ttu-id="7b42b-124">tooconfigure hello와의 통합 ICIMS Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 ICIMS tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-124">tooconfigure hello integration of ICIMS into Azure AD, you need tooadd ICIMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7b42b-125">**hello 갤러리에서 ICIMS tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="7b42b-125">**tooadd ICIMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b42b-126">Hello에 ** [Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="7b42b-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7b42b-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="7b42b-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="7b42b-133">Hello 검색 상자에 입력 **ICIMS**선택, **ICIMS** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-133">In hello search box, type **ICIMS**, select **ICIMS** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ICIMS hello 결과 목록에서](./media/active-directory-saas-icims-tutorial/tutorial_icims_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7b42b-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="7b42b-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="7b42b-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 ICIMS에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-136">In this section, you configure and test Azure AD single sign-on with ICIMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7b42b-137">Single sign on toowork에 대 한 Azure AD는 tooknow ICIMS에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ICIMS is tooa user in Azure AD.</span></span> <span data-ttu-id="7b42b-138">즉, Azure AD 사용자 및 ICIMS에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-138">In other words, a link relationship between an Azure AD user and hello related user in ICIMS needs toobe established.</span></span>

<span data-ttu-id="7b42b-139">ICIMS에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-139">In ICIMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7b42b-140">tooconfigure 및 ICIMS 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-140">tooconfigure and test Azure AD single sign-on with ICIMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7b42b-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on) ** -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7b42b-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user) ** -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7b42b-143">**[ICIMS 테스트 사용자 만들기](#create-an-icims-test-user) ** -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 ICIMS에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-143">**[Create an ICIMS test user](#create-an-icims-test-user)** - toohave a counterpart of Britta Simon in ICIMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7b42b-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7b42b-145">**[Single Sign-on 테스트](#test-single-sign-on) ** -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="7b42b-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7b42b-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="7b42b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7b42b-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 ICIMS 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ICIMS application.</span></span>

<span data-ttu-id="7b42b-148">**tooconfigure Azure AD single sign on, ICIMS와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="7b42b-148">**tooconfigure Azure AD single sign-on with ICIMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b42b-149">Hello hello에 Azure 포털에서에서 **ICIMS** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-149">In hello Azure portal, on hello **ICIMS** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="7b42b-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-icims-tutorial/tutorial_icims_samlbase.png)

3. <span data-ttu-id="7b42b-153">Hello에 **ICIMS 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-153">On hello **ICIMS Domain and URLs** section, perform hello following steps:</span></span>

    ![ICIMS 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-icims-tutorial/tutorial_icims_url.png)

    <span data-ttu-id="7b42b-155">a.</span><span class="sxs-lookup"><span data-stu-id="7b42b-155">a.</span></span> <span data-ttu-id="7b42b-156">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="7b42b-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant name>.icims.com`</span></span>

    <span data-ttu-id="7b42b-157">b.</span><span class="sxs-lookup"><span data-stu-id="7b42b-157">b.</span></span> <span data-ttu-id="7b42b-158">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="7b42b-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant name>.icims.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7b42b-159">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-159">These values are not real.</span></span> <span data-ttu-id="7b42b-160">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7b42b-161">연락처 [ICIMS 클라이언트 지원 팀](https://www.icims.com/contact-us) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-161">Contact [ICIMS Client support team](https://www.icims.com/contact-us) tooget these values.</span></span> 
 
4. <span data-ttu-id="7b42b-162">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-icims-tutorial/tutorial_icims_certificate.png) 

5. <span data-ttu-id="7b42b-164">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-164">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-icims-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7b42b-166">Hello에 **ICIMS 구성** 섹션에서 클릭 **구성 ICIMS** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="7b42b-166">On hello **ICIMS Configuration** section, click **Configure ICIMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7b42b-167">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="7b42b-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![ICIMS 구성](./media/active-directory-saas-icims-tutorial/tutorial_icims_configure.png) 

7. <span data-ttu-id="7b42b-169">tooconfigure single sign on에서 **ICIMS** toosend hello 다운로드 해야 쪽에서는 **메타 데이터 XML**, **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** 너무 [ICIMS 지원 팀](https://www.icims.com/contact-us)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-169">tooconfigure single sign-on on **ICIMS** side, you need toosend hello downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[ICIMS support team](https://www.icims.com/contact-us).</span></span> <span data-ttu-id="7b42b-170">이 설정은 toohave hello 양쪽 모두에 제대로 설정 하는 SAML SSO 연결 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="7b42b-171">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="7b42b-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7b42b-172">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서 ** 구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="7b42b-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7b42b-173">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7b42b-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7b42b-174">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="7b42b-174">Create an Azure AD test user</span></span>
<span data-ttu-id="7b42b-175">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="7b42b-177">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="7b42b-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b42b-178">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-icims-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7b42b-180">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-icims-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7b42b-182">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![hello 추가 단추](./media/active-directory-saas-icims-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7b42b-184">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![hello 사용자 대화 상자](./media/active-directory-saas-icims-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7b42b-186">a.</span><span class="sxs-lookup"><span data-stu-id="7b42b-186">a.</span></span> <span data-ttu-id="7b42b-187">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7b42b-188">b.</span><span class="sxs-lookup"><span data-stu-id="7b42b-188">b.</span></span> <span data-ttu-id="7b42b-189">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7b42b-190">c.</span><span class="sxs-lookup"><span data-stu-id="7b42b-190">c.</span></span> <span data-ttu-id="7b42b-191">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7b42b-192">d.</span><span class="sxs-lookup"><span data-stu-id="7b42b-192">d.</span></span> <span data-ttu-id="7b42b-193">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-193">Click **Create**.</span></span>
 
### <a name="create-an-icims-test-user"></a><span data-ttu-id="7b42b-194">ICIMS 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="7b42b-194">Create an ICIMS test user</span></span>

<span data-ttu-id="7b42b-195">hello이이 섹션의 목적은 toocreate Britta Simon ICIMS에서 호출 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-195">hello objective of this section is toocreate a user called Britta Simon in ICIMS.</span></span> <span data-ttu-id="7b42b-196">작업할 [ICIMS 지원 팀](https://www.icims.com/contact-us) hello ICIMS 계정에서에서 tooadd hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-196">Work with [ICIMS support team](https://www.icims.com/contact-us) tooadd hello users in hello ICIMS account.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7b42b-197">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7b42b-198">이 섹션에서는 tooICIMS 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooICIMS.</span></span>

![Hello 사용자 역할 할당][200]

<span data-ttu-id="7b42b-200">**tooassign Britta Simon tooICIMS hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="7b42b-200">**tooassign Britta Simon tooICIMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b42b-201">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="7b42b-203">Hello 응용 프로그램 목록에서 선택 **ICIMS**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-203">In hello applications list, select **ICIMS**.</span></span>

    ![hello 응용 프로그램 목록에서 hello ICIMS 링크](./media/active-directory-saas-icims-tutorial/tutorial_icims_app.png) 

3. <span data-ttu-id="7b42b-205">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202] 

4. <span data-ttu-id="7b42b-207">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-207">Click **Add** button.</span></span> <span data-ttu-id="7b42b-208">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="7b42b-210">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7b42b-211">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7b42b-212">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7b42b-213">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="7b42b-213">Test single sign-on</span></span>

<span data-ttu-id="7b42b-214">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD SSO 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-214">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="7b42b-215">Hello ICIMS hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour ICIMS 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b42b-215">When you click hello ICIMS tile in hello Access Panel, you should get automatically signed-on tooyour ICIMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7b42b-216">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="7b42b-216">Additional resources</span></span>

* [<span data-ttu-id="7b42b-217">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="7b42b-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7b42b-218">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="7b42b-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icims-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icims-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icims-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icims-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icims-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icims-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icims-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icims-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icims-tutorial/tutorial_general_203.png

