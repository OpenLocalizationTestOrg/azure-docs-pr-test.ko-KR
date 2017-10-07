---
title: "자습서: ScreenSteps와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 ScreenSteps 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: fd041e5fe4552727eeda2dabc1773d8043d410f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a><span data-ttu-id="9b9ce-103">자습서: ScreenSteps와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="9b9ce-103">Tutorial: Azure Active Directory integration with ScreenSteps</span></span>

<span data-ttu-id="9b9ce-104">이 자습서에 설명 어떻게 toointegrate ScreenSteps와 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9b9ce-104">In this tutorial, you learn how toointegrate ScreenSteps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9b9ce-105">Azure AD와 ScreenSteps 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-105">Integrating ScreenSteps with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9b9ce-106">액세스 tooScreenSteps을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-106">You can control in Azure AD who has access tooScreenSteps.</span></span>
- <span data-ttu-id="9b9ce-107">에 사용자가 tooautomatically get 로그온 tooScreenSteps (Single Sign-on)는 Azure AD 계정으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-107">You can enable your users tooautomatically get signed-on tooScreenSteps (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9b9ce-108">하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="9b9ce-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b9ce-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9b9ce-110">Prerequisites</span></span>

<span data-ttu-id="9b9ce-111">ScreenSteps와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-111">tooconfigure Azure AD integration with ScreenSteps, you need hello following items:</span></span>

- <span data-ttu-id="9b9ce-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="9b9ce-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9b9ce-113">ScreenSteps Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="9b9ce-113">A ScreenSteps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9b9ce-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9b9ce-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9b9ce-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9b9ce-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9b9ce-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="9b9ce-118">Scenario description</span></span>
<span data-ttu-id="9b9ce-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9b9ce-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9b9ce-121">ScreenSteps는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="9b9ce-121">Adding ScreenSteps from hello gallery</span></span>
2. <span data-ttu-id="9b9ce-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="9b9ce-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-screensteps-from-hello-gallery"></a><span data-ttu-id="9b9ce-123">ScreenSteps는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="9b9ce-123">Adding ScreenSteps from hello gallery</span></span>
<span data-ttu-id="9b9ce-124">tooconfigure hello와의 통합 ScreenSteps Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 ScreenSteps tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-124">tooconfigure hello integration of ScreenSteps into Azure AD, you need tooadd ScreenSteps from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9b9ce-125">**hello 갤러리에서 ScreenSteps tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9b9ce-125">**tooadd ScreenSteps from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b9ce-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="9b9ce-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9b9ce-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="9b9ce-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="9b9ce-133">Hello 검색 상자에 입력 **ScreenSteps**선택, **ScreenSteps** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-133">In hello search box, type **ScreenSteps**, select **ScreenSteps** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ScreenSteps hello 결과 목록에서](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9b9ce-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="9b9ce-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9b9ce-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 ScreenSteps에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-136">In this section, you configure and test Azure AD single sign-on with ScreenSteps based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9b9ce-137">Single sign on toowork에 대 한 Azure AD는 tooknow ScreenSteps에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ScreenSteps is tooa user in Azure AD.</span></span> <span data-ttu-id="9b9ce-138">즉, Azure AD 사용자와 ScreenSteps에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-138">In other words, a link relationship between an Azure AD user and hello related user in ScreenSteps needs toobe established.</span></span>

<span data-ttu-id="9b9ce-139">Hello hello 값을 할당, ScreenSteps에서 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-139">In ScreenSteps, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9b9ce-140">tooconfigure와 ScreenSteps와 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-140">tooconfigure and test Azure AD single sign-on with ScreenSteps, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9b9ce-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9b9ce-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9b9ce-143">**[ScreenSteps 테스트 사용자 만들기](#create-a-screensteps-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 ScreenSteps에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-143">**[Create a ScreenSteps test user](#create-a-screensteps-test-user)** - toohave a counterpart of Britta Simon in ScreenSteps that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9b9ce-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9b9ce-145">**[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9b9ce-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="9b9ce-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9b9ce-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 ScreenSteps 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ScreenSteps application.</span></span>

<span data-ttu-id="9b9ce-148">**Azure AD tooconfigure single sign on와 ScreenSteps를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9b9ce-148">**tooconfigure Azure AD single sign-on with ScreenSteps, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b9ce-149">Hello hello에 Azure 포털에서에서 **ScreenSteps** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-149">In hello Azure portal, on hello **ScreenSteps** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="9b9ce-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. <span data-ttu-id="9b9ce-153">Hello에 **ScreenSteps 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-153">On hello **ScreenSteps Domain and URLs** section, perform hello following steps:</span></span>

    ![ScreenSteps 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    <span data-ttu-id="9b9ce-155">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<tenantname>.ScreenSteps.com`</span><span class="sxs-lookup"><span data-stu-id="9b9ce-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.ScreenSteps.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9b9ce-156">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-156">This value is not real.</span></span> <span data-ttu-id="9b9ce-157">Hello로이 값을 업데이트 합니다. 실제 로그온 URL,이 자습서의 뒷부분에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-157">Update this value with hello actual Sign-On URL, which is explained later in this tutorial.</span></span> 

4. <span data-ttu-id="9b9ce-158">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. <span data-ttu-id="9b9ce-160">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-160">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9b9ce-162">Hello에 **ScreenSteps 구성** 섹션에서 클릭 **구성 ScreenSteps** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-162">On hello **ScreenSteps Configuration** section, click **Configure ScreenSteps** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9b9ce-163">복사 hello **Sign-Out URL 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="9b9ce-163">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![ScreenSteps 구성](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. <span data-ttu-id="9b9ce-165">다른 웹 브라우저 창에서 ScreenSteps 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-165">In a different web browser window, log into your ScreenSteps company site as an administrator.</span></span>

8. <span data-ttu-id="9b9ce-166">**계정 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-166">Click **Account Settings**.</span></span>

    <span data-ttu-id="9b9ce-167">![계정 관리](./media/active-directory-saas-screensteps-tutorial/ic778523.png "계정 관리")</span><span class="sxs-lookup"><span data-stu-id="9b9ce-167">![Account management](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Account management")</span></span>

9. <span data-ttu-id="9b9ce-168">**Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-168">Click **Single Sign-on**.</span></span>

    <span data-ttu-id="9b9ce-169">![원격 인증](./media/active-directory-saas-screensteps-tutorial/ic778524.png "원격 인증")</span><span class="sxs-lookup"><span data-stu-id="9b9ce-169">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Remote authentication")</span></span>

10. <span data-ttu-id="9b9ce-170">**Single Sign-on 끝점 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-170">Click **Create Single Sign-on Endpoint**.</span></span>

    <span data-ttu-id="9b9ce-171">![원격 인증](./media/active-directory-saas-screensteps-tutorial/ic778525.png "원격 인증")</span><span class="sxs-lookup"><span data-stu-id="9b9ce-171">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Remote authentication")</span></span>

11. <span data-ttu-id="9b9ce-172">Hello에 **만들 Single sign-on 끝점** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-172">In hello **Create Single Sign-on Endpoint** section, perform hello following steps:</span></span>

    <span data-ttu-id="9b9ce-173">![인증 끝점 만들기](./media/active-directory-saas-screensteps-tutorial/ic778526.png "인증 끝점 만들기")</span><span class="sxs-lookup"><span data-stu-id="9b9ce-173">![Create an authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Create an authentication endpoint")</span></span>
    
    <span data-ttu-id="9b9ce-174">a.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-174">a.</span></span> <span data-ttu-id="9b9ce-175">Hello에 **제목** 텍스트 상자에 제목 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-175">In hello **Title** textbox, type a title.</span></span>
    
    <span data-ttu-id="9b9ce-176">b.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-176">b.</span></span> <span data-ttu-id="9b9ce-177">Hello에서 **모드** 목록에서 **SAML**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-177">From hello **Mode** list, select **SAML**.</span></span>
    
    <span data-ttu-id="9b9ce-178">c.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-178">c.</span></span> <span data-ttu-id="9b9ce-179">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-179">Click **Create**.</span></span>

12. <span data-ttu-id="9b9ce-180">**편집** hello 새 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-180">**Edit** hello new endpoint.</span></span>

    <span data-ttu-id="9b9ce-181">![끝점 편집](./media/active-directory-saas-screensteps-tutorial/ic778528.png "끝점 편집")</span><span class="sxs-lookup"><span data-stu-id="9b9ce-181">![Edit endpoint](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Edit endpoint")</span></span>

13. <span data-ttu-id="9b9ce-182">Hello에 **편집 Single sign-on 끝점** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-182">In hello **Edit Single Sign-on Endpoint** section, perform hello following steps:</span></span>

    <span data-ttu-id="9b9ce-183">![원격 인증 끝점](./media/active-directory-saas-screensteps-tutorial/ic778527.png "원격 인증 끝점")</span><span class="sxs-lookup"><span data-stu-id="9b9ce-183">![Remote authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Remote authentication endpoint")</span></span>

    <span data-ttu-id="9b9ce-184">a.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-184">a.</span></span> <span data-ttu-id="9b9ce-185">클릭 **새 SAML 인증서 파일 업로드**, 한 다음 업로드 hello 인증서를 Azure 포털에서 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-185">Click **Upload new SAML Certificate file**, and then upload hello certificate, which you have downloaded from Azure portal.</span></span>
    
    <span data-ttu-id="9b9ce-186">b.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-186">b.</span></span> <span data-ttu-id="9b9ce-187">붙여넣기 **SAML Single Sign-on 서비스 URL** hello에 hello Azure 포털에서에서 복사한 값 **원격 로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **Remote Login URL** textbox.</span></span>
    
    <span data-ttu-id="9b9ce-188">c.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-188">c.</span></span> <span data-ttu-id="9b9ce-189">붙여넣기 **Sign-Out URL** hello에 hello Azure 포털에서에서 복사한 값 **로그 아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-189">Paste **Sign-Out URL** value, which you have copied from hello Azure portal into hello **Log out URL** textbox.</span></span>
    
    <span data-ttu-id="9b9ce-190">d.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-190">d.</span></span> <span data-ttu-id="9b9ce-191">선택 된 **그룹** tooassign 사용자 toowhen 프로 비전 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-191">Select a **Group** tooassign users toowhen they are provisioned.</span></span>
    
    <span data-ttu-id="9b9ce-192">e.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-192">e.</span></span> <span data-ttu-id="9b9ce-193">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-193">Click **Update**.</span></span>

    <span data-ttu-id="9b9ce-194">f.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-194">f.</span></span> <span data-ttu-id="9b9ce-195">복사 hello **SAML 소비자 URL** toohello 클립보드 toohello에 붙여 **로그온 URL** 텍스트 상자로 **ScreenSteps 도메인 및 Url** 섹션.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-195">Copy hello **SAML Consumer URL** toohello clipboard and paste in toohello **Sign-on URL** textbox in **ScreenSteps Domain and URLs** section.</span></span>
    
    <span data-ttu-id="9b9ce-196">g.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-196">g.</span></span> <span data-ttu-id="9b9ce-197">Toohello 반환 **편집 Single sign-on 끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-197">Return toohello **Edit Single Sign-on Endpoint**.</span></span>
    
    <span data-ttu-id="9b9ce-198">h.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-198">h.</span></span> <span data-ttu-id="9b9ce-199">Hello 클릭 **계정에 대 한 기본 서버로 만들기** 단추 toouse이이 끝점에 대 한 모든 사용자에 게 ScreenSteps에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-199">Click hello **Make default for account** button toouse this endpoint for all users who log into ScreenSteps.</span></span> <span data-ttu-id="9b9ce-200">Hello 클릭 해도 **tooSite 추가** toouse이이 끝점에서 특정 사이트에 대 한 단추 **ScreenSteps**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-200">Alternatively you can click hello **Add tooSite** button toouse this endpoint for specific sites in **ScreenSteps**.</span></span>

> [!TIP]
> <span data-ttu-id="9b9ce-201">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="9b9ce-201">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9b9ce-202">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-202">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9b9ce-203">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9b9ce-203">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9b9ce-204">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="9b9ce-204">Create an Azure AD test user</span></span>

<span data-ttu-id="9b9ce-205">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-205">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="9b9ce-207">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9b9ce-207">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b9ce-208">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-208">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="9b9ce-210">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-210">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="9b9ce-212">tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-212">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello 추가 단추](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="9b9ce-214">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-214">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello 사용자 대화 상자](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9b9ce-216">a.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-216">a.</span></span> <span data-ttu-id="9b9ce-217">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-217">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9b9ce-218">b.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-218">b.</span></span> <span data-ttu-id="9b9ce-219">Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-219">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="9b9ce-220">c.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-220">c.</span></span> <span data-ttu-id="9b9ce-221">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-221">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="9b9ce-222">d.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-222">d.</span></span> <span data-ttu-id="9b9ce-223">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-223">Click **Create**.</span></span>
 
### <a name="create-a-screensteps-test-user"></a><span data-ttu-id="9b9ce-224">ScreenSteps 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="9b9ce-224">Create a ScreenSteps test user</span></span>

<span data-ttu-id="9b9ce-225">이 섹션에서는 ScreenSteps에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-225">In this section, you create a user called Britta Simon in ScreenSteps.</span></span> <span data-ttu-id="9b9ce-226">작업할 [ScreenSteps 클라이언트 지원 팀](https://www.screensteps.com/contact) hello 사용자 hello ScreenSteps 플랫폼을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-226">Work with [ScreenSteps Client support team](https://www.screensteps.com/contact) to add hello users in hello ScreenSteps platform.</span></span> <span data-ttu-id="9b9ce-227">Single Sign-On을 사용하려면 먼저 사용자를 만들고 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-227">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="9b9ce-228">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="9b9ce-229">이 섹션에서는 tooScreenSteps 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooScreenSteps.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="9b9ce-231">**tooassign Britta Simon tooScreenSteps hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="9b9ce-231">**tooassign Britta Simon tooScreenSteps, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b9ce-232">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="9b9ce-234">Hello 응용 프로그램 목록에서 선택 **ScreenSteps**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-234">In hello applications list, select **ScreenSteps**.</span></span>

    ![hello 응용 프로그램 목록에서 hello ScreenSteps 링크](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. <span data-ttu-id="9b9ce-236">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="9b9ce-238">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-238">Click **Add** button.</span></span> <span data-ttu-id="9b9ce-239">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="9b9ce-241">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9b9ce-242">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9b9ce-243">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9b9ce-244">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="9b9ce-244">Test single sign-on</span></span>

<span data-ttu-id="9b9ce-245">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9b9ce-246">Hello ScreenSteps hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour ScreenSteps 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-246">When you click hello ScreenSteps tile in hello Access Panel, you should get automatically signed-on tooyour ScreenSteps application.</span></span>
<span data-ttu-id="9b9ce-247">액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ce-247">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9b9ce-248">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="9b9ce-248">Additional resources</span></span>

* [<span data-ttu-id="9b9ce-249">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="9b9ce-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9b9ce-250">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="9b9ce-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

