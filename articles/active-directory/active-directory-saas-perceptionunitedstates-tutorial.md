---
title: "자습서: Azure Active Directory와 Perception United States(비 UltiPro) 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory에 대 한 인식 United States (비-UltiPro) 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 874b5da277b9c68504c4af2ac87ed90d2bbd93b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a><span data-ttu-id="96389-103">자습서: Azure Active Directory와 Perception United States(비 UltiPro) 통합</span><span class="sxs-lookup"><span data-stu-id="96389-103">Tutorial: Azure Active Directory integration with Perception United States (Non-UltiPro)</span></span>

<span data-ttu-id="96389-104">이 자습서에 설명 어떻게 toointegrate Azure Active directory (Azure AD)에 대 한 인식 United States (비-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="96389-104">In this tutorial, you learn how toointegrate Perception United States (Non-UltiPro) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="96389-105">에 대 한 인식 United States (비-UltiPro) Azure AD와 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-105">Integrating Perception United States (Non-UltiPro) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="96389-106">Azure ad 액세스 tooPerception 미국 (비-UltiPro)를 가진 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96389-106">You can control in Azure AD who has access tooPerception United States (Non-UltiPro).</span></span>
- <span data-ttu-id="96389-107">프로그램 사용자 tooautomatically get 로그온 tooPerception 미국 (비 UltiPro) (Single Sign-on)는 Azure AD 계정으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96389-107">You can enable your users tooautomatically get signed-on tooPerception United States (Non-UltiPro) (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="96389-108">하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96389-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="96389-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96389-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="96389-110">Prerequisites</span></span>

<span data-ttu-id="96389-111">Azure AD 통합에 대 한 인식 United States (비-UltiPro)와 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-111">tooconfigure Azure AD integration with Perception United States (Non-UltiPro), you need hello following items:</span></span>

- <span data-ttu-id="96389-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="96389-112">An Azure AD subscription</span></span>
- <span data-ttu-id="96389-113">Perception United States(비 UltiPro) Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="96389-113">A Perception United States (Non-UltiPro) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="96389-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="96389-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="96389-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="96389-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="96389-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96389-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="96389-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="96389-118">Scenario description</span></span>
<span data-ttu-id="96389-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="96389-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96389-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="96389-121">에 대 한 인식 United States (비-UltiPro) hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="96389-121">Adding Perception United States (Non-UltiPro) from hello gallery</span></span>
2. <span data-ttu-id="96389-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="96389-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-perception-united-states-non-ultipro-from-hello-gallery"></a><span data-ttu-id="96389-123">에 대 한 인식 United States (비-UltiPro) hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="96389-123">Adding Perception United States (Non-UltiPro) from hello gallery</span></span>
<span data-ttu-id="96389-124">tooconfigure hello 통합에 대 한 인식 United States (비-UltiPro)의 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 tooadd United States (비-UltiPro)에 대 한 인식 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96389-124">tooconfigure hello integration of Perception United States (Non-UltiPro) into Azure AD, you need tooadd Perception United States (Non-UltiPro) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="96389-125">**tooadd hello 갤러리에서에 대 한 인식 United States (비-UltiPro) hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="96389-125">**tooadd Perception United States (Non-UltiPro) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="96389-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="96389-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="96389-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="96389-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="96389-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="96389-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="96389-133">Hello 검색 상자에 입력 **에 대 한 인식 United States (비-UltiPro)**선택, **에 대 한 인식 United States (비-UltiPro)** 결과 패널에서 클릭 **추가** 단추 tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="96389-133">In hello search box, type **Perception United States (Non-UltiPro)**, select **Perception United States (Non-UltiPro)** from result panel then click **Add** button tooadd hello application.</span></span>

    ![에 대 한 인식 미국 (비-UltiPro) hello 결과 목록에서](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="96389-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="96389-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="96389-136">이 섹션에서는 Britta Simon이라는 테스트 사용자를 기반으로 Perception United States(비 UltiPro)에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-136">In this section, you configure and test Azure AD single sign-on with Perception United States (Non-UltiPro) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="96389-137">Single sign on toowork에 대 한 Azure AD는 tooknow hello 테이블에 해당 사용자에 대 한 인식 United States (비-UltiPro)에서 Azure AD에서 tooa 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Perception United States (Non-UltiPro) is tooa user in Azure AD.</span></span> <span data-ttu-id="96389-138">즉, Azure AD 사용자와 hello 관련된 사용자에 대 한 인식 미국 (비-UltiPro) 사이의 링크 관계를 toobe 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-138">In other words, a link relationship between an Azure AD user and hello related user in Perception United States (Non-UltiPro) needs toobe established.</span></span>

<span data-ttu-id="96389-139">에 대 한 인식 미국 (비-UltiPro) hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="96389-139">In Perception United States (Non-UltiPro), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="96389-140">tooconfigure 및 Azure AD에서 single sign-on 테스트에 대 한 인식 United States (비-UltiPro)와 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-140">tooconfigure and test Azure AD single sign-on with Perception United States (Non-UltiPro), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="96389-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="96389-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="96389-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="96389-143">**[에 대 한 인식 United States (비-UltiPro) 테스트 사용자 만들기](#create-a-perception-united-states-non-ultipro-test-user)**  -toohave Britta Simon에 대 한 인식 United States (비-UltiPro)는 사용자의 연결 된 Azure AD toohello 표현 하는 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="96389-143">**[Create a Perception United States (Non-UltiPro) test user](#create-a-perception-united-states-non-ultipro-test-user)** - toohave a counterpart of Britta Simon in Perception United States (Non-UltiPro) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="96389-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="96389-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="96389-145">**[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="96389-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="96389-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="96389-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="96389-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 및 United States (비-UltiPro)에 대 한 인식 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Perception United States (Non-UltiPro) application.</span></span>

<span data-ttu-id="96389-148">**tooconfigure Azure AD에서 single sign-on에 대 한 인식 United States (비-UltiPro)와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="96389-148">**tooconfigure Azure AD single sign-on with Perception United States (Non-UltiPro), perform hello following steps:**</span></span>

1. <span data-ttu-id="96389-149">Hello hello에 Azure 포털에서에서 **에 대 한 인식 United States (비-UltiPro)** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-149">In hello Azure portal, on hello **Perception United States (Non-UltiPro)** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="96389-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="96389-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

3. <span data-ttu-id="96389-153">Hello에 **에 대 한 인식 United States (비-UltiPro) 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-153">On hello **Perception United States (Non-UltiPro) Domain and URLs** section, perform hello following steps:</span></span>

    ![Perception United States(비 UltiPro) 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    <span data-ttu-id="96389-155">a.</span><span class="sxs-lookup"><span data-stu-id="96389-155">a.</span></span> <span data-ttu-id="96389-156">Hello에 **식별자** textbox hello URL 입력:`https://perception.kanjoya.com/sp`</span><span class="sxs-lookup"><span data-stu-id="96389-156">In hello **Identifier** textbox, type hello URL: `https://perception.kanjoya.com/sp`</span></span>

    <span data-ttu-id="96389-157">b.</span><span class="sxs-lookup"><span data-stu-id="96389-157">b.</span></span> <span data-ttu-id="96389-158">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://perception.kanjoya.com/sso?idp=<entity_id>`</span><span class="sxs-lookup"><span data-stu-id="96389-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://perception.kanjoya.com/sso?idp=<entity_id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="96389-159">hello 값이 실제 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="96389-159">hello value is not real.</span></span> <span data-ttu-id="96389-160">Hello 자습서의 뒷부분에 설명 되어 hello 실제 회신 URL로 hello 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-160">You will update hello value with hello actual Reply URL, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="96389-161">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

5. <span data-ttu-id="96389-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-163">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="96389-165">Hello에 **구성에 대 한 인식 United States (비-UltiPro)** 섹션에서 클릭 **구성에 대 한 인식 United States (비-UltiPro)** tooopen **sign on 구성** 창입니다.</span><span class="sxs-lookup"><span data-stu-id="96389-165">On hello **Perception United States (Non-UltiPro) Configuration** section, click **Configure Perception United States (Non-UltiPro)** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="96389-166">복사 hello **SAML 엔터티 ID** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="96389-166">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="96389-167">a.</span><span class="sxs-lookup"><span data-stu-id="96389-167">a.</span></span> <span data-ttu-id="96389-168">hello **에 대 한 인식 United States (비-UltiPro)** 응용 프로그램에 필요한 hello **SAML 엔터티 ID** 값으로를 복사한 toobe uri 인코딩이 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-168">hello **Perception United States (Non-UltiPro)** application requires hello **SAML Entity ID** value, which you have copied, toobe uri encoded.</span></span> <span data-ttu-id="96389-169">tooget hello uri 인코딩된 값을 사용 하 여 hello 링크:**http://www.url-encode-decode.com/**합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-169">tooget hello uri encoded value, use hello following link:**http://www.url-encode-decode.com/**.</span></span>

    <span data-ttu-id="96389-170">b.</span><span class="sxs-lookup"><span data-stu-id="96389-170">b.</span></span> <span data-ttu-id="96389-171">Hello uri를 받은 후 인코딩된 값와 결합 hello **회신 URL** 설명 했 듯이 아래-</span><span class="sxs-lookup"><span data-stu-id="96389-171">After getting hello uri encoded value combine it with hello **Reply URL** as mentioned below-</span></span>

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    <span data-ttu-id="96389-172">c.</span><span class="sxs-lookup"><span data-stu-id="96389-172">c.</span></span> <span data-ttu-id="96389-173">Hello에 대 한 값을 넘는 붙여넣기 hello **회신 URL** 텍스트 상자로 **에 대 한 인식 United States (비-UltiPro) 도메인 및 Url** 섹션.</span><span class="sxs-lookup"><span data-stu-id="96389-173">Paste hello above value in hello **Reply URL** textbox in **Perception United States (Non-UltiPro) Domain and URLs** section.</span></span>

    ![Perception United States(비 UltiPro) 구성](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

7. <span data-ttu-id="96389-175">다른 브라우저 창에서 관리자 권한으로 tooyour에 대 한 인식 United States (비-UltiPro) 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-175">In another browser window, sign on tooyour Perception United States (Non-UltiPro) company site as an administrator.</span></span>

8. <span data-ttu-id="96389-176">Hello 주 도구 모음에서 클릭 **계정 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-176">In hello main toolbar, click **Account Settings**.</span></span>

    ![Perception United States(비 UltiPro) 사용자](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

9. <span data-ttu-id="96389-178">Hello에 **계정 설정** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-178">On hello **Account Settings** page, perform hello following steps:</span></span>

    ![Perception United States(비 UltiPro) 사용자](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    <span data-ttu-id="96389-180">a.</span><span class="sxs-lookup"><span data-stu-id="96389-180">a.</span></span> <span data-ttu-id="96389-181">Hello에 **회사 이름** hello의 형식 hello 이름 텍스트 상자 **회사**합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-181">In hello **Company Name** textbox, type hello name of hello **Company**.</span></span>
    
    <span data-ttu-id="96389-182">b.</span><span class="sxs-lookup"><span data-stu-id="96389-182">b.</span></span> <span data-ttu-id="96389-183">Hello에 **계정 이름** hello의 형식 hello 이름 텍스트 상자 **계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-183">In hello **Account Name** textbox, type hello name of hello **Account**.</span></span>

    <span data-ttu-id="96389-184">c.</span><span class="sxs-lookup"><span data-stu-id="96389-184">c.</span></span> <span data-ttu-id="96389-185">**기본 회신 tooEmail** 텍스트 상자에서 올바른 형식 hello **전자 메일**합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-185">In **Default Reply-tooEmail** text box, type hello valid **Email**.</span></span>

    <span data-ttu-id="96389-186">d.</span><span class="sxs-lookup"><span data-stu-id="96389-186">d.</span></span> <span data-ttu-id="96389-187">**SAML 2.0**으로 **SSO ID 공급자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-187">Select **SSO Identity Provider** as **SAML 2.0**.</span></span>

10. <span data-ttu-id="96389-188">Hello에 **SSO 구성** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-188">On hello **SSO Configuration** page, perform hello following steps:</span></span>

    ![Perception United States(비 UltiPro) SSO 구성](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    <span data-ttu-id="96389-190">a.</span><span class="sxs-lookup"><span data-stu-id="96389-190">a.</span></span> <span data-ttu-id="96389-191">**전자 메일**로 **SAML NameID 유형**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-191">Select **SAML NameID Type** as **EMAIL**.</span></span>

    <span data-ttu-id="96389-192">b.</span><span class="sxs-lookup"><span data-stu-id="96389-192">b.</span></span> <span data-ttu-id="96389-193">Hello에 **SSO 구성 이름** 의 형식 hello 이름 텍스트 상자에 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-193">In hello **SSO Configuration Name** textbox, type hello name of your **Configuration**.</span></span>
    
    <span data-ttu-id="96389-194">c.</span><span class="sxs-lookup"><span data-stu-id="96389-194">c.</span></span> <span data-ttu-id="96389-195">**Id 공급자 이름** 붙여넣기 hello 값의 텍스트 상자 **SAML 엔터티 ID**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="96389-195">In **Identity Provider Name** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="96389-196">d.</span><span class="sxs-lookup"><span data-stu-id="96389-196">d.</span></span> <span data-ttu-id="96389-197">**SAML 도메인 텍스트 상자가**, 같은 hello 도메인을 입력  **@contoso.com** 합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-197">In **SAML Domain textbox**, enter hello domain like **@contoso.com**.</span></span>

    <span data-ttu-id="96389-198">e.</span><span class="sxs-lookup"><span data-stu-id="96389-198">e.</span></span> <span data-ttu-id="96389-199">클릭 **다시 업로드** tooupload hello **메타 데이터 XML** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="96389-199">Click on **Upload Again** tooupload hello **Metadata XML** file.</span></span>

    <span data-ttu-id="96389-200">f.</span><span class="sxs-lookup"><span data-stu-id="96389-200">f.</span></span> <span data-ttu-id="96389-201">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-201">Click **Update**.</span></span>


> [!TIP]
> <span data-ttu-id="96389-202">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="96389-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="96389-203">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="96389-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="96389-204">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="96389-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="96389-205">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="96389-205">Create an Azure AD test user</span></span>

<span data-ttu-id="96389-206">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="96389-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="96389-208">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="96389-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="96389-209">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="96389-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="96389-211">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="96389-213">tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="96389-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello 추가 단추](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="96389-215">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello 사용자 대화 상자](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_04.png)

    <span data-ttu-id="96389-217">a.</span><span class="sxs-lookup"><span data-stu-id="96389-217">a.</span></span> <span data-ttu-id="96389-218">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="96389-219">b.</span><span class="sxs-lookup"><span data-stu-id="96389-219">b.</span></span> <span data-ttu-id="96389-220">Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="96389-221">c.</span><span class="sxs-lookup"><span data-stu-id="96389-221">c.</span></span> <span data-ttu-id="96389-222">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="96389-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="96389-223">d.</span><span class="sxs-lookup"><span data-stu-id="96389-223">d.</span></span> <span data-ttu-id="96389-224">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-224">Click **Create**.</span></span>
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a><span data-ttu-id="96389-225">Perception United States(비 UltiPro) 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="96389-225">Create a Perception United States (Non-UltiPro) test user</span></span>

<span data-ttu-id="96389-226">이 섹션에서는 Perception United States(비 UltiPro)에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="96389-226">In this section, you create a user called Britta Simon in Perception United States (Non-UltiPro).</span></span> <span data-ttu-id="96389-227">작업할 [지원 팀에 대 한 인식 United States (비-UltiPro)](http://www.ultimatesoftware.com/Contact/ContactUs) hello에 대 한 인식 United States (비-UltiPro) 플랫폼의 tooadd hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="96389-227">Work with [Perception United States (Non-UltiPro) support team](http://www.ultimatesoftware.com/Contact/ContactUs) tooadd hello users in hello Perception United States (Non-UltiPro) platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="96389-228">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="96389-229">이 섹션에서는 액세스 tooPerception 미국 (비-UltiPro)을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPerception United States (Non-UltiPro).</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="96389-231">**tooassign Britta Simon tooPerception 미국 (비-UltiPro) hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="96389-231">**tooassign Britta Simon tooPerception United States (Non-UltiPro), perform hello following steps:**</span></span>

1. <span data-ttu-id="96389-232">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="96389-234">Hello 응용 프로그램 목록에서 선택 **에 대 한 인식 United States (비-UltiPro)**합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-234">In hello applications list, select **Perception United States (Non-UltiPro)**.</span></span>

    ![hello 응용 프로그램 목록에서 hello에 대 한 인식 United States (비-UltiPro) 링크](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

3. <span data-ttu-id="96389-236">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="96389-238">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-238">Click **Add** button.</span></span> <span data-ttu-id="96389-239">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="96389-241">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96389-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="96389-242">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="96389-243">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="96389-244">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="96389-244">Test single sign-on</span></span>

<span data-ttu-id="96389-245">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96389-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="96389-246">Hello 액세스 패널에에서 hello에 대 한 인식 United States (비-UltiPro) 타일을 클릭할 때 자동으로 로그온 tooyour 응용 프로그램에 대 한 인식 United States (비-UltiPro)을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-246">When you click hello Perception United States (Non-UltiPro) tile in hello Access Panel, you should get automatically signed-on tooyour Perception United States (Non-UltiPro) application.</span></span>
<span data-ttu-id="96389-247">액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="96389-247">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="96389-248">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="96389-248">Additional resources</span></span>

* [<span data-ttu-id="96389-249">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="96389-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="96389-250">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="96389-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_203.png

