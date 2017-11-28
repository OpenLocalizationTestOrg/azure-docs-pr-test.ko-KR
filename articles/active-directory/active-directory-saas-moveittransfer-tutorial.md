---
title: "자습서: Azure Active Directory와 MOVEit Transfer - Azure AD 통합 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 MOVEit 전송-Azure AD 통합 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 5bbe4f2d952bd45c4d58d55ffc3467b4eb871fd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a><span data-ttu-id="78eab-103">자습서: Azure Active Directory와 MOVEit Transfer - Azure AD 통합 통합</span><span class="sxs-lookup"><span data-stu-id="78eab-103">Tutorial: Azure Active Directory integration with MOVEit Transfer - Azure AD integration</span></span>

<span data-ttu-id="78eab-104">이 자습서에 설명 어떻게 toointegrate MOVEit 전송-Azure Active Directory (Azure AD)와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-104">In this tutorial, you learn how toointegrate MOVEit Transfer - Azure AD integration with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="78eab-105">MOVEit 전송-Azure AD와 Azure AD 통합 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-105">Integrating MOVEit Transfer - Azure AD integration with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="78eab-106">액세스 tooMOVEit 전송-Azure AD 통합을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-106">You can control in Azure AD who has access tooMOVEit Transfer - Azure AD integration.</span></span>
- <span data-ttu-id="78eab-107">에 사용자가 tooautomatically get 로그온 tooMOVEit 전송-Azure AD 통합 (Single Sign-on)는 Azure AD 계정 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-107">You can enable your users tooautomatically get signed-on tooMOVEit Transfer - Azure AD integration (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="78eab-108">하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="78eab-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78eab-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="78eab-110">Prerequisites</span></span>

<span data-ttu-id="78eab-111">다음 항목 hello가 필요 tooconfigure MOVEit 전송-Azure AD 통합와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-111">tooconfigure Azure AD integration with MOVEit Transfer - Azure AD integration, you need hello following items:</span></span>

- <span data-ttu-id="78eab-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="78eab-112">An Azure AD subscription</span></span>
- <span data-ttu-id="78eab-113">MOVEit Transfer - Azure AD 통합 Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="78eab-113">A MOVEit Transfer - Azure AD integration single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="78eab-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="78eab-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="78eab-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="78eab-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="78eab-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="78eab-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="78eab-118">Scenario description</span></span>
<span data-ttu-id="78eab-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="78eab-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="78eab-121">추가 MOVEit 전송-hello 갤러리에서 Azure AD 통합</span><span class="sxs-lookup"><span data-stu-id="78eab-121">Adding MOVEit Transfer - Azure AD integration from hello gallery</span></span>
2. <span data-ttu-id="78eab-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="78eab-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moveit-transfer---azure-ad-integration-from-hello-gallery"></a><span data-ttu-id="78eab-123">추가 MOVEit 전송-hello 갤러리에서 Azure AD 통합</span><span class="sxs-lookup"><span data-stu-id="78eab-123">Adding MOVEit Transfer - Azure AD integration from hello gallery</span></span>
<span data-ttu-id="78eab-124">MOVEit 전송-Azure AD에 Azure AD 통합의 tooconfigure hello 통합 tooadd MOVEit 전송-hello 갤러리 tooyour 목록에서 관리 되는 SaaS 앱의 Azure AD 통합 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-124">tooconfigure hello integration of MOVEit Transfer - Azure AD integration into Azure AD, you need tooadd MOVEit Transfer - Azure AD integration from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="78eab-125">**MOVEit 전송-hello 갤러리에서 Azure AD 통합 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="78eab-125">**tooadd MOVEit Transfer - Azure AD integration from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="78eab-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="78eab-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="78eab-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="78eab-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="78eab-133">Hello 검색 상자에 입력 **MOVEit 전송-Azure AD 통합**선택, **MOVEit 전송-Azure AD 통합** 결과 패널에서 클릭 **추가** 단추 tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-133">In hello search box, type **MOVEit Transfer - Azure AD integration**, select **MOVEit Transfer - Azure AD integration** from result panel then click **Add** button tooadd hello application.</span></span>

    ![MOVEit 전송-hello 결과 목록에서 Azure AD 통합](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="78eab-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="78eab-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="78eab-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 MOVEit Transfer - Azure AD 통합에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-136">In this section, you configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="78eab-137">Single sign on toowork에 대 한 Azure AD는 tooknow hello 대응 사용자 MOVEit 전송에 필요-Azure AD에서 Azure AD 통합은 tooa 사용자.</span><span class="sxs-lookup"><span data-stu-id="78eab-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in MOVEit Transfer - Azure AD integration is tooa user in Azure AD.</span></span> <span data-ttu-id="78eab-138">즉, Azure AD 사용자 및 MOVEit 전송-에 hello 관련된 사용자 간 링크 관계를 Azure AD 통합 toobe 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-138">In other words, a link relationship between an Azure AD user and hello related user in MOVEit Transfer - Azure AD integration needs toobe established.</span></span>

<span data-ttu-id="78eab-139">MOVEit 전송-Azure AD 통합의에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-139">In MOVEit Transfer - Azure AD integration, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="78eab-140">tooconfigure 및 MOVEit 전송-Azure AD 통합을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-140">tooconfigure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="78eab-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="78eab-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="78eab-143">**[MOVEit 전송-Azure AD 통합 테스트 사용자 만들기](#create-a-moveit-transfer---azure-ad-integration-test-user)**  사용자의 연결 된 Azure AD toohello 표현인-toohave Britta Simon MOVEit 전송에 해당 하는 도구-Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-143">**[Create a MOVEit Transfer - Azure AD integration test user](#create-a-moveit-transfer---azure-ad-integration-test-user)** - toohave a counterpart of Britta Simon in MOVEit Transfer - Azure AD integration that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="78eab-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="78eab-145">**[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="78eab-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="78eab-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="78eab-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="78eab-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 프로그램 MOVEit 전송-Azure AD 통합 응용 프로그램에서에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your MOVEit Transfer - Azure AD integration application.</span></span>

<span data-ttu-id="78eab-148">**tooconfigure Azure AD single sign on MOVEit 전송-Azure AD 통합 된 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="78eab-148">**tooconfigure Azure AD single sign-on with MOVEit Transfer - Azure AD integration, perform hello following steps:**</span></span>

1. <span data-ttu-id="78eab-149">Hello hello에 Azure 포털에서에서 **MOVEit 전송-Azure AD 통합** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-149">In hello Azure portal, on hello **MOVEit Transfer - Azure AD integration** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="78eab-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. <span data-ttu-id="78eab-153">Hello에 **MOVEit 전송-Azure AD 통합 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-153">On hello **MOVEit Transfer - Azure AD integration Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    <span data-ttu-id="78eab-155">a.</span><span class="sxs-lookup"><span data-stu-id="78eab-155">a.</span></span> <span data-ttu-id="78eab-156">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://contoso.com`</span><span class="sxs-lookup"><span data-stu-id="78eab-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://contoso.com`</span></span>

    <span data-ttu-id="78eab-157">b.</span><span class="sxs-lookup"><span data-stu-id="78eab-157">b.</span></span> <span data-ttu-id="78eab-158">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://contoso.com/<tenatid>`</span><span class="sxs-lookup"><span data-stu-id="78eab-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://contoso.com/<tenatid>`</span></span>

    <span data-ttu-id="78eab-159">c.</span><span class="sxs-lookup"><span data-stu-id="78eab-159">c.</span></span> <span data-ttu-id="78eab-160">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span><span class="sxs-lookup"><span data-stu-id="78eab-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="78eab-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-161">These values are not real.</span></span> <span data-ttu-id="78eab-162">이러한 항목을 업데이트 식별자, 회신 URL 및 로그온 URL 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-162">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="78eab-163">이러한 값 나중에 참조할 수 있습니다 **서비스 공급자 메타 데이터 URL** 섹션 또는 연락처 [MOVEit 전송-Azure AD 통합 클라이언트 지원 팀](https://community.ipswitch.com/s/support) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-163">You can refer these values later in **Service Provider Metadata URL** section or contact [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support) tooget these values.</span></span>

4. <span data-ttu-id="78eab-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. <span data-ttu-id="78eab-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-166">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="78eab-168">관리자 권한으로 테 넌 트 MOVEit 전송 tooyour 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-168">Sign on tooyour MOVEit Transfer tenant as an administrator.</span></span>

7. <span data-ttu-id="78eab-169">Hello 왼쪽된 탐색 창에서 클릭 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-169">On hello left navigation pane, click **Settings**.</span></span>

    ![앱 쪽의 설정 섹션](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. <span data-ttu-id="78eab-171">**보안 정책 -> 사용자 인증** 아래의 **Single Sign On** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-171">Click **Single Signon** link, which is under **Security Policies -> User Auth**.</span></span>

    ![앱 쪽의 보안 정책](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. <span data-ttu-id="78eab-173">Hello 메타 데이터 URL 링크 toodownload hello 메타 데이터 문서를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-173">Click hello Metadata URL link toodownload hello metadata document.</span></span>

    ![서비스 공급자 메타데이터 URL](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * <span data-ttu-id="78eab-175">확인 **entityID** 일치 **식별자** hello에 **MOVEit 전송-Azure AD 통합 도메인 및 Url** 섹션.</span><span class="sxs-lookup"><span data-stu-id="78eab-175">Verify **entityID** matches **Identifier** in hello **MOVEit Transfer - Azure AD integration Domain and URLs** section .</span></span>
    * <span data-ttu-id="78eab-176">확인 **AssertionConsumerService** 위치 URL 일치 **회신 URL** hello에 **MOVEit 전송-Azure AD 통합 도메인 및 Url** 섹션.</span><span class="sxs-lookup"><span data-stu-id="78eab-176">Verify **AssertionConsumerService** Location URL matches **REPLY URL** in hello **MOVEit Transfer - Azure AD integration Domain and URLs** section.</span></span>
    
    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. <span data-ttu-id="78eab-178">클릭 **Id 공급자 추가** tooadd 새 페더레이션 Id 공급자 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-178">Click **Add Identity Provider** button tooadd a new Federated Identity Provider.</span></span>

    ![ID 공급자 추가](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. <span data-ttu-id="78eab-180">클릭 **찾아보기...**  tooselect hello 메타 데이터 파일을 Azure 포털에서 다운로드 한 다음 클릭 **Id 공급자 추가** tooupload hello 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-180">Click **Browse...** tooselect hello metadata file which you downloaded from Azure portal, then click **Add Identity Provider** tooupload hello downloaded file.</span></span>

    ![SAML ID 공급자](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. <span data-ttu-id="78eab-182">선택 "**예**"으로 **Enabled** hello에 **페더레이션 Id 공급자 설정 편집...**  페이지 클릭 하 여 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-182">Select "**Yes**" as **Enabled** in hello **Edit Federated Identity Provider Settings...** page and click **Save**.</span></span>

    ![페더레이션 ID 공급자 설정](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. <span data-ttu-id="78eab-184">Hello에 **편집 페더레이션 Id 공급자 사용자 설정을** 페이지 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-184">In hello **Edit Federated Identity Provider User Settings** page, perform hello following actions:</span></span>
    
    ![페더레이션 ID 공급자 설정 편집](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    <span data-ttu-id="78eab-186">a.</span><span class="sxs-lookup"><span data-stu-id="78eab-186">a.</span></span> <span data-ttu-id="78eab-187">**로그인 이름**으로 **SAML NameID**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-187">Select **SAML NameID** as **Login name**.</span></span>
    
    <span data-ttu-id="78eab-188">b.</span><span class="sxs-lookup"><span data-stu-id="78eab-188">b.</span></span> <span data-ttu-id="78eab-189">선택 **다른** 으로 **전체 이름을** 및 hello **특성 이름** textbox hello 값 입력: `http://schemas.microsoft.com/identity/claims/displayname`합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-189">Select **Other** as **Full name** and in hello **Attribute name** textbox put hello value: `http://schemas.microsoft.com/identity/claims/displayname`.</span></span>
    
    <span data-ttu-id="78eab-190">c.</span><span class="sxs-lookup"><span data-stu-id="78eab-190">c.</span></span> <span data-ttu-id="78eab-191">선택 **다른** 으로 **전자 메일** 및 hello **특성 이름** textbox hello 값 입력: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-191">Select **Other** as **Email** and in hello **Attribute name** textbox put hello value: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="78eab-192">d.</span><span class="sxs-lookup"><span data-stu-id="78eab-192">d.</span></span> <span data-ttu-id="78eab-193">**SignOn에서 계정 자동 만들기**로 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-193">Select **Yes** as **Auto-create account on signon**.</span></span>
    
    <span data-ttu-id="78eab-194">e.</span><span class="sxs-lookup"><span data-stu-id="78eab-194">e.</span></span> <span data-ttu-id="78eab-195">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-195">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="78eab-196">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="78eab-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="78eab-197">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="78eab-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="78eab-198">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="78eab-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="78eab-199">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="78eab-199">Create an Azure AD test user</span></span>

<span data-ttu-id="78eab-200">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="78eab-202">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="78eab-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="78eab-203">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-203">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="78eab-205">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-205">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="78eab-207">tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="78eab-207">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello 추가 단추](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="78eab-209">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-209">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello 사용자 대화 상자](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    <span data-ttu-id="78eab-211">a.</span><span class="sxs-lookup"><span data-stu-id="78eab-211">a.</span></span> <span data-ttu-id="78eab-212">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-212">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="78eab-213">b.</span><span class="sxs-lookup"><span data-stu-id="78eab-213">b.</span></span> <span data-ttu-id="78eab-214">Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-214">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="78eab-215">c.</span><span class="sxs-lookup"><span data-stu-id="78eab-215">c.</span></span> <span data-ttu-id="78eab-216">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-216">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="78eab-217">d.</span><span class="sxs-lookup"><span data-stu-id="78eab-217">d.</span></span> <span data-ttu-id="78eab-218">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-218">Click **Create**.</span></span>
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a><span data-ttu-id="78eab-219">MOVEit Transfer - Azure AD 통합 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="78eab-219">Create a MOVEit Transfer - Azure AD integration test user</span></span>

<span data-ttu-id="78eab-220">이 섹션의 hello 목표 toocreate Britta Simon MOVEit 전송-Azure AD 통합의에서 라는 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-220">hello objective of this section is toocreate a user called Britta Simon in MOVEit Transfer - Azure AD integration.</span></span> <span data-ttu-id="78eab-221">MOVEit Transfer - Azure AD 통합은 적시에 프로비전을 지원하며 사용하도록 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-221">MOVEit Transfer - Azure AD integration supports just-in-time provisioning, which you have enabled.</span></span> <span data-ttu-id="78eab-222">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-222">There is no action item for you in this section.</span></span> <span data-ttu-id="78eab-223">새 사용자를 시도 tooaccess MOVEit 전송-아직 존재 하지 않는 경우 Azure AD 통합 하는 동안 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-223">A new user is created during an attempt tooaccess MOVEit Transfer - Azure AD integration if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="78eab-224">Toocontact hello toocreate 사용자를 수동으로 필요한 경우 필요한 [MOVEit 전송-Azure AD 통합 클라이언트 지원 팀](https://community.ipswitch.com/s/support)합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-224">If you need toocreate a user manually, you need toocontact hello [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="78eab-225">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="78eab-226">이 섹션에서는 tooMOVEit 전송-Azure AD 통합 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMOVEit Transfer - Azure AD integration.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="78eab-228">**tooassign Britta Simon tooMOVEit 전송-Azure AD 통합 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="78eab-228">**tooassign Britta Simon tooMOVEit Transfer - Azure AD integration, perform hello following steps:**</span></span>

1. <span data-ttu-id="78eab-229">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="78eab-231">Hello 응용 프로그램 목록에서 선택 **MOVEit 전송-Azure AD 통합**합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-231">In hello applications list, select **MOVEit Transfer - Azure AD integration**.</span></span>

    ![hello MOVEit 전송-hello 응용 프로그램 목록에 연결 된 Azure AD 통합](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. <span data-ttu-id="78eab-233">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="78eab-235">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-235">Click **Add** button.</span></span> <span data-ttu-id="78eab-236">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="78eab-238">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="78eab-239">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="78eab-240">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="78eab-241">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="78eab-241">Test single sign-on</span></span>

<span data-ttu-id="78eab-242">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD SSO 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="78eab-243">Hello MOVEit 전송-Azure AD 통합 타일을 클릭할 때 자동으로 로그온 tooyour MOVEit 전송-Azure AD 통합 응용 프로그램 액세스 패널 hello에서 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78eab-243">When you click hello MOVEit Transfer - Azure AD integration tile in hello Access Panel, you should get automatically signed-on tooyour MOVEit Transfer - Azure AD integration application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="78eab-244">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="78eab-244">Additional resources</span></span>

* [<span data-ttu-id="78eab-245">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="78eab-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="78eab-246">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="78eab-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

